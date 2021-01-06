---
id: rollups
title: Hotstuff Rollups
sidebar_label: Rollups
---

Rollups are a concept popularized by Vitalik Buterin and suggested as main scaling methodology for Ethereum till second version of the network will be delivered. The main idea behind rollups lies in posting compressed transaction execution data to the main chain. 

We use rollups to replicate state from the side chain to the main chain which is useful for two main reasons: 
- Moving execution to the side chain
- Using Ethereum to communicate between side-chains

## How it works
<<graph>>
### Gagarin.network
Rollup plugin is used to add rollup logic to gagarin.network. Plugin implements three interfaces OnBlockCommit, OnReceiveProposal, OnNewBlockCreated.

For each block to be finalized it is necessary to have quorum certificate constructed in lock phase. Aggregated signature contained in quorum certificate is a cryptographic proof of block validity and acceptance, three certificates in a row are a cryptographic proof of block commitment. We use this fact to prove that prepared in the block rollup is valid and can be used to replicate side-chain state to the main chain. Please see below what block data looks like:

```golang
type BlockImpl struct {
   header    *HeaderImpl
   qc        api.QuorumCertificate
   signature *crypto.SignatureAggregate
   txs       []api.Transaction 
   receipts  []api.Receipt 
   data      []byte
}
```

Every time a block is constructed rollup plugin constructs rollup data, serializes it with zssz serializer and writes it to the block.data field. Voters validate not only blocks and transactions in them but also rollup data for correctness and equality to transaction receipts.
```golang
type Rollup struct {
   Accounts     [][20]byte
   Transactions []*Transaction
}
```

```golang
type Transaction struct {
   From  int32
   To    int32
   Value uint64
}
```
Rollup.Accounts field is a dictionary of addresses which were used in gagarin.network transactions. Rollup transaction is a structure which describes fund transfer necessary to update balances.
### Ethereum contract
