---
id: utils
title: Utilities
sidebar_label: Utilities
---
## tx_send
Tx_send is a test tool to send transactions to network. ``tx_send`` is a cobra runtime command to run peer node with. 

This tool can be run as 

``` gnetwork tx_send --scenario.path=./static/tx_send/scenario.yaml --senders.path=./static/tx_send/senders.yaml --rpc.address=localhost:9280```

### scenario.yaml
This file describes test scenario.
- First mapping key is height where this transactions are supposed to be sent 
- Second mapping key is a peer index in the committee  list we want transaction to be sent to. ``p`` is a given height proposer 
- List of transactions

``from`` and ``to`` are indexes of senders in senders.yaml, we can use real (e. g. 0x3db5e6f31B6b46ffeC25E512763FC61aEc42654c) address here.
Default type is `PAYMENT`, default nonce is a next nonce, this fields can be omitted.
Types have aliases
- "P" for payment
- "S" for settlemetns
- "A" for agreement
- "R" for redeem

```yaml
15:
  p:
    - fee: 1
      from: 1
      to: 1
      value: 10
    - fee: 1
      from: 1
      to: 2
      value: 10
    - fee: 1
      from: 1
      to: 3
      value: 10
    - fee: 1
      from: 2
      to: 0x3db5e6f31B6b46ffeC25E512763FC61aEc42654c
      nonce: 1
      value: 10
  1:
    - fee: 1
      from: 2
      to: 0x3db5e6f31B6b46ffeC25E512763FC61aEc42654c
      nonce: 2
      value: 10
  3:
    - fee: 1
      from: 1
      to: 1
      value: 10
    - fee: 1
      from: 2
      to: 0x3db5e6f31B6b46ffeC25E512763FC61aEc42654c
      nonce: 3
      value: 10
16:
  p:
    - fee: 1
      from: 1
      to: 1
      value: 10
```
In this scenario, on 15-th view tx_send will send:
- 4 transactions to proposer
- 1 transaction to first peer
- 2 transactions to third peer

Then on 16-th view it will sen 1 transaction to proposer and will exit successfully.

`Agreement` can look like this
```yaml
10:
  p:
    - type: A
      fee: 1
      from: 0
      to: 0x3db5e6f31B6b46ffeC25E512763FC61aEc42654c
      value: 0
```


### senders.yaml
This config defines list of private keys of senders, for example:

```yaml 
---
- 4a157ef4295be2413c59613cd5dd4f3b0688ac6227709a9634608f33a49250ef
- 2283cffa18be03d69516d73a979991574968cdeb2e44ff85ec699a9e6d225fe4
- 5abd006c4e2f3dcdb18b1d8f73653d2a3f94a7d260a3e2b38d9475b8249f9691
- 27c6206525a283acf67cc0a08230bad554e6572aa5e81e497f3a0172f6045282
- 0e5e5b4d425d374db7ecc98b1528a3f419abb7cff1e9ad40be6488c22ace366f
- 41fcf849e55efe34923532842dea21ba737ef6fc4722dab95bd7afe6216eeabf
- 2cee58a241c6f0aff8e79c3095bfa0407d2266825450f358cbda2d621087ba86
```

## rpc_send
Rpc_send is a test tool to send json messages from the disk to the network via gRpc. ``rpc_send`` is a cobra runtime command to run peer node with. 

This tool can be run with script 

``` gnetwork rpc_send --config=./static/settings.yaml --message.path=./static/rpc_send/getview.json --rpc.call=GetCurrentView --rpc.address=localhost:9280 -m2```

Rpc_send will read getview.json file, transform it to proto message and send via gRpc to GetCurrentView      

## Wallet
>Coming soon
