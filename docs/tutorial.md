---
id: tutorial
title: Tutorial
sidebar_label: Tutorial
---

## Functionality
To create plugin at first you need to decide what events and data you need to receive from blockchain. Usually we will have some diagram, for example for rollups plugin, which we will develop in the tutorial, we have sequence diagram in [rollups](rollups.md) section.

## Interfaces
Since we analyze requirements we found out interfaces we want to implement

To send data to Ethereum smart contract we need ```common_pb.OnBlockCommitServer```

To check received block's data for rollups validity we need ```common_pb.OnReceiveProposalServer```

To create rollup data from receipts and write it into ```block.data``` field we need ```common_pb.OnNewBlockCreatedServer```

## Method implementation
We will briefly implement methods here


### OnNewBlockCreatedServer
We use this interface to create rollup, when we propose block 
1. Return empty rollup in case it was empty block
2. Create rollup from receipts we calculated
3. Marshal and return new mutated block
```golang
func (r *RollupsPlugin) OnNewBlockCreated(ctx context.Context, in *common_pb.OnNewBlockCreatedRequest) (*common_pb.OnNewBlockCreatedResponse, error) {
	log.Debugf("Creating rollup for block %v", common.Bytes2Hex(in.Block.Header.Hash))
	//1
	if len(in.Receipts) == 0 {
		log.Infof("Block %v has no receipts", common.Bytes2Hex(in.Block.Header.Hash))
		return &common_pb.OnNewBlockCreatedResponse{
			Block: in.Block,
		}, nil
	}
	
    //2
	addresses, txs := r.createRollups(in.Receipts)
	roll := &Rollup{
		Accounts:     addresses,
		Transactions: txs,
	}

	log.Infof("Created rollup for %v block", common.Bytes2Hex(in.Block.Header.Hash))
	spew.Dump(roll)

    //3
	marshal, err := ssz.Marshal(roll)
	if err != nil {
		return nil, err
	}

	in.Block.Data.Data = marshal
	return &common_pb.OnNewBlockCreatedResponse{
		Block: in.Block,
	}, nil
```

### OnReceiveProposalServer
``OnReceiveProposalServer`` interface has 4 functions, since we want to validate rollup we need to implement our logic only in ``AfterProposedBlockAdded``. We leave other functions dummy implemented.
1. We get transactions receipts, which we get after ```applyTx()```  and calculate our version of rollup for this block
2. Do validations and equality checks on this block, in case of error return error, which will reject this block
```golang
func (r *RollupsPlugin) BeforeProposedBlockAdded(ctx context.Context,
	in *common_pb.BeforeProposedBlockAddedRequest) (*common_pb.BeforeProposedBlockAddedResponse, error) {
	return &common_pb.BeforeProposedBlockAddedResponse{
		Proposal: in.Proposal,
	}, nil
}
	
func (r *RollupsPlugin) AfterProposedBlockAdded(ctx context.Context, in *common_pb.AfterProposedBlockAddedRequest) (*common_pb.AfterProposedBlockAddedResponse, error) {
	log.Debugf("After proposed block %v added", common.Bytes2Hex(in.Proposal.Block.Header.Hash))

    //1
	mapping, transactions := r.createRollups(in.Receipts)

    //2
	rm := &Rollup{}
	if len(in.GetProposal().GetBlock().GetData().GetData()) > 0 {
		if err := ssz.Unmarshal(in.GetProposal().GetBlock().GetData().GetData(), rm); err != nil {
			log.Error("Bad received rollup format", err)
			return nil, err
		}
		if len(mapping) != len(rm.Accounts) || len(transactions) != len(rm.Transactions) {
			err := errors.New("lengths of rollups are not equal")
			log.Debug("Lengths of rollups structures do not match(cr:r), accounts[%v:%v], transactions:[%v:%v]",
				len(mapping), len(rm.Accounts), len(transactions), len(rm.Transactions))
			return nil, err
		}
		...
    }

	log.Infof("Valid rollup for %v block", common.Bytes2Hex(in.Proposal.Block.Header.Hash))
	return &common_pb.AfterProposedBlockAddedResponse{}, nil
}	
	
func (r *RollupsPlugin) BeforeVoted(ctx context.Context, in *common_pb.BeforeVotedRequest) (*common_pb.BeforeVotedResponse, error) {
	return &common_pb.BeforeVotedResponse{
		Vote: in.Vote,
	}, nil
}

func (r *RollupsPlugin) AfterVoted(ctx context.Context, in *common_pb.AfterVotedRequest) (*common_pb.AfterVotedResponse, error) {
	return &common_pb.AfterVotedResponse{}, nil
}
```
### OnBlockCommitServer
```OnBlockCommitServer``` interface has one function to implement
1. In this function we will run Settlement watcher, that will match ``Settlement`` transactions with pending deposit in smart contract to send ``Agreement``
2. Get last height of processed rollup and calculate needed blocks to send rollups from
3. For each block create rollup message and send it
```golang
func (r *RollupsPlugin) OnBlockCommit(ctx context.Context, req *common_pb.OnBlockCommitRequest) (*common_pb.OnBlockCommitResponse, error) {
    log.Debug("On block commit")
    
    //1
    for _, t := range req.GetBlock().Txs {
        if t.Type == int32(api.Settlement) && bytes.Equal([]byte("lock"), t.Data) {
            r.watchPending(ctx, t)
        }
    }
    ...	
    
    //2
    contractHeight, err := r.rollupApi.GetTopHeight(&bind.CallOpts{})
    var fork []*common_pb.BlockS
    if req.Block.Header.Height > int32(contractHeight) + 1 {
        log.Infof("Loading fork starting at %v to %v", contractHeight, req.Block.Header.Height)
        loaded, err := r.client.Pbc().GetFork(ctx, &common_pb.GetForkRequest{
            Height:   int32(contractHeight) + 1,
            HeadHash: req.Block.Header.ParentHash,
        })
        if err != nil {
            log.Error("Get fork failed", err)
            return nil, err
        }

        sort.Sort(ByHeight(loaded.GetBlocks()))

        fork = append(loaded.Blocks, req.Block)
    }
    ...
    
    //3
    
    for _, b := range fork {
        h := &SendableHeader{
            Height:    uint32(b.GetHeader().GetHeight()),
            Hash:      hash,
            TxHash:    txHash,
            StateHash: stateHash,
            DataHash:  dataHash,
            QcHash:    qcHash,
            Parent:    parentHash,
            Timestamp: uint64(b.GetHeader().GetTimestamp()),
        }

        mh, err := ssz.Marshal(h)
        if err != nil {
            log.Error(err)
            return nil, err
        }
        
        r.refreshNonce()

        _, err = r.rollupApi.AddBlock(r.txOpts, mh, emptyBytes(b.Data.Data), make([]byte, 0))
        if err != nil {
            log.Error("AddBlock failed", err)
            return nil, err
        }
    }
    ... 
    
    log.Infof("%v sent %v rollups", common.Bytes2Hex(req.Me.GetAddress()), len(fork))
    return &common_pb.OnBlockCommitResponse{}, nil
	
```

### Bootstrap
We want to implement some starting routines here

```golang
func (r *RollupsPlugin) Bootstrap(cfg Config) error {
	log.Info("Bootstrapping rollups plugin")
	lis, err := net.Listen("tcp", cfg.Address)
	if err != nil {
		return err
	}

	opts := []grpc.ServerOption{grpc.MaxConcurrentStreams(cfg.MaxConcurrentStreams)}
	grpcServer := grpc.NewServer(opts...)
	common_pb.RegisterOnBlockCommitServer(grpcServer, r)
	common_pb.RegisterOnReceiveProposalServer(grpcServer, r)
	common_pb.RegisterOnNewBlockCreatedServer(grpcServer, r)
	go func() {
		if err := grpcServer.Serve(lis); err != nil {
			log.Error(err)
		}
	}()
	log.Info("Rollups plugin bootstrapped")
	return nil
}
```

## Configuration
Here we configure rollups as first plugin. We have another plugin called prover just for to show how we can configure more than one plugin in Settings.yaml
```yaml
...
Plugins:
    #rollups
  - Address: 172.18.0.98:9380
    Interfaces: ['OnBlockCommit', 'OnReceiveProposal', 'OnNewBlockCreated']
    #proover
  - Address: 172.18.0.99:9380
    Interfaces: ['OnBlockCommit']
...
```

## Conclusion
In this short tutorial we've shown how fast and easy developers can create complex products using Gagarin.network. For more information see [api](api.md) section. 
