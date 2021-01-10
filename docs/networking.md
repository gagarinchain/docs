---
id: networking
sidebar_label: Network
title: Network layer
---

Networking is a huge part of decentralized network. Together with consensus protocol, network framework is one of core elements which fully defines blockchain's functionality and especially its limitations.
It is an enormously hard task to create good network framework from scratch, moreover there are not many open source protocols to choose from. But luckily there is one that costs hundreds and it is Libp2p (https://libp2p.io/).

Libp2p is a modular system of protocols, specifications and libraries that enables the development of peer-to-peer network applications.
A peer-to-peer network is one where the participants (referred to as peers or nodes) communicate with one another directly, on more or less “equal footing”. This does not necessarily mean that all peers are identical; some may have different roles in the overall network. However, one of the defining characteristics of a peer-to-peer network is that they do not require a priviliged set of “servers” which behave completely differently from their “clients”, as is the case in the predominant client / server model.


## Transport
At the foundation of libp2p is the transport layer, which is responsible for the actual transmission and receipt of data from one peer to another. There are many ways to send data across networks in use today, with more in development and still more yet to be designed. 
libp2p provides a simple interface that can be adapted to support existing and future protocols, allowing libp2p applications to operate in many different runtime and networking environments.

libp2p supports “upgrading” a connection provided by a transport into a securely encrypted channel. The process is flexible, and can support multiple methods of encrypting communication. The current default is secio, with support for TLS 1.3 under development.

All communication in Gagarin.network is done via libp2p transport. We use several transport protocols provided by libp2p
 - secio over tcp/ip transport for p2p communication and message broadcasting
 - web socket transport over tcp/ip for monitoring buss service
 - relay transport for advanced network setups 

## Identity
Libp2p uses public key cryptography as the basis of peer identity, which serves two complementary purposes. First, it gives each peer a globally unique “name”, in the form of a PeerId. Second, the PeerId allows anyone to retrieve the public key for the identified peer, which enables secure communication between peers.

Every peer in Gagarin.network has its own identity. ECDSA keypair is generated on Secp256k1 curve to identify each peeer and use in secio transport 

### Permissions
>we will write about permission service soon

## Peer Routing
When you want to send a message to another peer, you need two key pieces of information: their PeerId, and a way to locate them on the network to open a connection.

There are many cases where we only have the PeerId for the peer we want to contact, and we need a way to discover their network address. Peer routing is the process of discovering peer addresses by leveraging the knowledge of other peers.

In a peer routing system, a peer can either give us the address we need if they have it, or else send our inquiry to another peer who’s more likely to have the answer. As we contact more and more peers, we not only increase our chances of finding the peer we’re looking for, libp2p builds a more complete view of the network in our own routing tables, which enables us to answer routing queries from others.
Libp2p uses a distributed hash table to iteratively route requests closer to the desired PeerId using the Kademlia routing algorithm.

In Gagarin.network peers do not necessarily take part in consensus, they can only provide networking services, such as peer discovery or transport relay. More about peer configuration see in configuration service.

## Messaging / PubSub
Sending messages to groups of interested receivers is at the heart of most Gagarin.network, and pubsub protocol of libp2p (short for publish / subscribe) is a very useful pattern for it.

Libp2p defines a pubsub interface for sending messages to all peers subscribed to a given “topic”. In Gagagrin.network we use gossipsub broadcast protocol, for reliable broadcasting of Hotstuff vote messages.
