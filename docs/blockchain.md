---
id: blockchain
title: Blockchain 
sidebar_label: Blockchain
---

Gagarin.network blockchain is in many ways similar to the blockchains in popular open networks such as Ethereum and Bitcoin. Blockchain is a sequence of blocks starting from special genesis block, every block has link to parent block and genesis block is reachable from every block through its parent recursively. Moreover every block has height such as height of parent block is less than children's height by one, so no gaps in height is allowed in  the blockchain. 

```proto
message BlockS {
    BlockHeaderS header = 1;
    QuorumCertificateS cert = 2;
    SignatureAggregateS signatureAggregate = 3;
    BlockDataS data = 4;
    repeated TransactionS txs = 5;
    repeated Receipt receipts = 6;
}

message BlockHeaderS {
    bytes hash = 1;
    bytes parentHash = 2;
    bytes qcHash = 3;
    bytes dataHash = 4;
    bytes txHash = 5;
    bytes stateHash = 6;
    int32 height = 7;
    int64 timestamp = 8;
}
```

In the same time the blockchain in Gagarin.network does have some differences. 

First, our blockchain has additional link to predecessor block. This link is formed via Quorum Certificate included in every block and is used for fast commits in the blockchain. How QCs are formed and used during commit phase is described in Hotstuff docs. 

Second, our blockchain does not have rich forking, Gagarin.network tree looks more like a palm, with long committed trunk and rich crown on top of committed height. Hotstuff guarantees that there will be at least one new committed block every epoch and all concurrent forks can successfully be omitted. 

Third, when block is committed we use aggregated signature, formed during voting for proposal with this block as cryptographic proof of block validity. With this proof we can get rid of all transaction signatures in this block, making block size less and further processing of this block faster.      

## Block validation 
>We will fill this section soon


## Synchronization algorithm
When node starts or it receives unknown block it must synchronize local blockchain and download missing blocks.
Further algorithm will describe this process in details:

1. Discover current blockchain height and optionally top blockchain height from the network (via hello message)

2. Request chain chunk

3. We can receive chunk less than m+d height, it's normal. The only requirement is that we must receive correct subchain without block absence, orphans will be filtered.
If chunk is incorrect, we add ban score and retry request to other peers

4. We can receive chunk without head on height m, it is normal, since previous responser could not have this exact fork. In this case we start requesting block headers of potential fork sequentially, until we find parent in current blockchain or hit depthLimit.

5. If we received correct chunk and we are able to add it to existing chain and new chain is correct, we start to download block bodies in parallel.
It is possible not to receive arbitrary block. In this case we simply drop chunk till this height and request blocks on next height again repeating 3-4 steps
For each request we have peer group (f + 1), we send query to first one and expect to receive correct request in time. If we can't, we go to next peer in group. If we asked every peer, we report error.

Request and response messages:
```golang
BlockHeadersRequest {
  low: m
  high: m + d
}
```
```golang
BlockHeadersResponse{
  headers []*BlockHeader
}
```
