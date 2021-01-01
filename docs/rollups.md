---
id: rollups
title: Hotstuff Rollups
sidebar_label: Hotstuff Rollups
---

Rollups is a concept popularized by Vitalik Buterin and suggested as main scaling methodology for Ethereum till second version of network will be delivered. Main idea behind rollups lies in posting compressed transaction execution data to main chain. 

We use rollups to replicate state from side chain to main chain, it is useful for two main reasons 
- Moving execution to side chain
- Using Ethereum to communicate between side-chains

## How it works
<<graph>>
### Gagarin.network
Rollup plugin is used to add rollup logic to gagarin.network. Plugin implements three interfaces OnBlockCommit, OnReceiveProposal, OnNewBlockCreated.

For each block to be finalized it is necessary to have quorum certificate constructed on lock phase. Aggregated signature contained in quorum certificate is a cryptographic proof of block validity and acceptance, three certificates in a row is a cryptographic proof of block commitment. We use this fact to prove that prepared in the block rollup is valid and can be used to replicate side-chain state to main chain. Let's look how block data looks like:

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

Every time block is constructed rollup plugin constructs rollup data, serializes it with zssz serializer and writes it to blocks data field. Voters validates not only blocks and transactions in them but also rollup data for it correctness and equality to transaction receipts.
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
Accounts field is a dictionary of addresses which took part in gagarin.network transactions, rollup transaction is a structure which describes fund transfer, necessary to update balances.
### Ethereum contract