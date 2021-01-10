---
id: overview
title: Overview
sidebar_label: Overview
---

Gagarin.network is a fast, secure and decentralized enterprise blockchain platform aiming to make stablecoins issuance easy and operation of existing ERC-20 tokens cheaper and faster.

With Gagarin.network you get:

- **Cloud-friendly model.** 
Using docker and kubernetes the Gagarin.network can be deployed and managed on any cloud platform and bare metal server. For early product development we can provide network that is set up in amazon or google cloud. Once the product becomes mature and consortium gets ready to run the network it can be easily migrated to a different environment.
- **Hotstuff consensus protocol.**
Hotstuff is a state of the art protocol designed by Cornel university and VMWare research scientists. Hotstuff is a BFT protocol developing PBFT, SBFT ideas. It has formal mathematical proof of liveness and correctness and is used by several leading blockchain projects. 
- **BLS cryptoraphy.**
We chose to use advanced crypto-schemes based on pairing friendly elliptic curve bls12-381. Cryptography based on bls12-381 allows to implement broad functionality via cryptographic primitives which we used to develop the following services: signatures aggregation, zero-knowledge private transactions, identity-based encryption. 
- **Libp2p networking.**
Libp2p is a network layer extracted from IPFS (the largest decentralized file system) which implements functionality necessary for a sophisticated decentralized application.
-  **App Chains.**
Each application or group of applications on Gagarin.network are an independent blockchain which consists of provided platform  and developed product plugins.  The product and the platform interact through API and system of oracles.  Such approach significantly facilitates deployment and development of applications, does not require the developer to study new program languages and allows fast start of development.
- **Utility token.**
We provide ready-to-use cryptocurrency and services for additional functionality. The cryptocurrency can be used for stablecoin or token issue, charging of fees, payments in the network and other utility functions and participation in PoS protocol. 
- **KyC AML.**
The service provides basic functions for client identification, granting and revoking access rights to conduct operations with the blockchain. Also the service provides tools for research and monitoring of clients' operations.
- **Wallet и Block explorer.**
Wallet and Block Explorer enable the users to interact with the blockchain in different ways: receive information on issued tokens, transactions, perform various actions to the tokens through the web interface.
- **Permission service.**
The service allows to autentificate participants of the network and authorize their actions. Each participant in the network has his own identificator which is given based on ECDSA encryption keys used to protect data sent in the network. The service allows to limit unauthorized actions by the participants, avoid unacceptable nodes from the network. This key is used also as node identificator in the network.
- **Hotstuff Rollups.**
We developed Hotstuff Rollups mechanism which is based on rollups and BLS signature as cryptographic proof data validity. The BLS signature is obtained as a result of aggregation of validators' signatures and is used in quorum certificate. Thus in the main chain we store a short summary on all transactions performed in Gagarin.network as well as proof that the network achieved consensus on this data and finalized it. A contract in the main-chain manages tokens, shows transactions of a product and synchronizes the state of two blockchains.
- **Interoperability.**
Full scale stablecoin operations require its integration with the outside world. Oracles are used to import facts from the outside world to the blockchain. Such import can be necessary, for expample, in order to lock resources in the real world as stablecoin's security. Participants of the network may need a service for locking funds on bank accounts, token issue, etc. 
-  **Oracle service.**
Any participant of the network can import events and facts from the real world to Gagarin.chain independently which helps to maintain high level of the platform decentralization. 
- **Proof of stake (TBD).**
Hotstuff just like any other BFT protocol ensures security and consensus if no more than one third of the participants are adversaries. Motivation of the network participant not to perform violations remains outside the protocol. In most cases it is enough for private blockchains as the validators of the network are always known in advance and there are many administrative methods to prevent violations. However  if the network participants would like to handle such a situation and set a procedure for slashing adversaries on the platform level we allowed for add-on to BTF consensus protocol in the form of proof-of-stake protocol.
- **Light clients (TBD).**
Light clients allow to avoid storing the state of the whole system by every network participant locally. A participant can process only data he needs and in the same time validate any block and make transactions, thus he does not differ from full scale nodes functionally. Use of light clients allows to avoid storing of signficant data amount locally without decrease of security level. It enables to create in-memory blockchain node that does not require use of local storage.
- **ZK privacy transactions (TBD).**
In order to withhold data on transactions between the participants of the network we created a second level protocol, added on Hotstuff consensus protocol, and a special second level network running that protocol.
