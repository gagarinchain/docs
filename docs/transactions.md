---
id: transactions
title: Transactions
sidebar_label: Transactions

---

Since we built Gagarin.network around stablecoin idea, transactions are the only way to mutate state of the system. Gagarin.network implements state replication machine logic. 
We have state transition function ```applyTx(pcurrent_state, tx_list)``` that receives current state and list of transactions (usually from block being processed) and returns new system state. If at least one transaction is invalid or not applicable, state transition do not happen and ```tx_list``` is rejected. 

Further common transaction structure
```proto
message Transaction {
    Type  type = 1;
    bytes to = 2;
    uint64 nonce = 3;
    int64 value = 4;
    int64 fee = 5;
    Signature signature = 6;
    bytes data = 7;
    bytes from = 8;

    enum Type {
        PAYMENT = 0;
        SLASHING = 1;
        SETTLEMENT = 2;
        AGREEMENT = 3;
        PROOF = 4;
        REDEEM = 5;
        STAKE = 6;
    }
}
```

Despite of their type transactions must provide all fields except optional ```from``` and ```data``` fields. 
```From``` is used to store information when signature is pruned while block commit. 
```Data``` can contain specific data used by plugins.

## Types
Every transaction type defines unique action with state. Lets look closely what every type is for:
- ```PAYMENT``` transactions are basic money transfer from Alice to Bob. 
- ```SLASHING``` is used for punishing malicious nodes in PoS consensus add-on.
- ```SETTLEMENT``` is used for some provable action, usually it is used for on-ramp operations, e. g. Rollups protocol uses it
- ```AGREEMENT``` is an intermediate single proof transaction, that settlement is valid
- ```PROOF``` is common proof transaction with n - f aggregated signatures, this transaction finally executes settlement 
- ```REDEEM``` is funds burn, usually it is used for off-ramp operations
- ```STAKE``` is money locking transaction for PoS consensus add-on

## Signatures
Default signature scheme for transactions is Boneh-Lynn-Shacham (BLS) crypto signatures on BLS12-381 curve. 
BLS signatures use parings and give us a lot of amazing features, such as identity schemes, ZK-proofs and so on. 
But they are pretty computational heavy and for some use cases can be too slow and expensive. For such use cases we provide Edwards-curve Digital Signature Algorithm (EdDSA) on Ed25519 curve.
These transactions are much faster and are suitable for transaction heavy loaded networks.

## Nonce
Since Gagarin.network doesn't use UTXO model like Bitcoin does it needs transaction ordering and account versioning. It is achieved by adding nonce field to transactions, the same way Ethereum does it. 
Nonce is an incremental integer which starts at 1 and increments without gaps. If transactions have equal nonces they are sorted by fee and transaction with higher fee is executed while others are rejected. It is common way to cancel mistaken transaction while it is still in tx_pool.

## Validation rules
>this section will be filled

## Transaction Pool
Transaction pool is an inmemory structure that stores all new coming valid transactions.  


## Transaction execution
Transactions to apply always come with new block for current blockchain fork. For every new block ```applyTransaction``` creates new empty snapshot which is linked to parent snapshot and inherits its state.  Every change transactions do in the state is stored in this snapshot.
If transaction is not applicable, the error occurs and snapshot becomes rejected. The result of transaction execution is receipt with execution log.  
Transaction is applicable when and only when it's 
- tx.nonce >= state.nonce + 1
- tx.from.balance >= tx.balance + tx.fee

If transaction is not currently applicable we keep it until it becomes applicable or transaction with bigger nonce is received and applied.

### Receipts
Receipt is a simple structure, that stores information about single account balance change:

```proto
message Receipt {
    bytes txHash = 1;
    bytes from = 2;
    bytes to = 3;
    int64 value = 4;
    int64 toValue = 5;
    int64 fromValue = 6;
}
```
