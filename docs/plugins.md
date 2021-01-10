---
id: plugins
title: Plugins and Services
sidebar_label: Plugins
---
## AppChain model
Our vision is to make it easy for developers to build blockchain applications and let developers and product managers decide how much decentralisation they want right now by where they want to run their application. Applications can be run on public clouds such as AWS and Google Cloud, on private corporate clouds or on bare metal servers. 
With Gagarin.network, applications can maintain sovereignty, process transactions fast and communicate with each other through Ethereum or any other public or private blockchain, making it optimal for a variety of use cases. Although Gagarin.network is very good at enhancing Ethereum applications aka smart contracts, speeding them up and extending their functionality thanks to Hotstuff Rollups protocol.

Ethereum simplified the development of decentralized applications by providing a Smart Contract concept which is pretty good and only known successful model now for open blockchains. But for private and semi-private blockchains this concept seems excessive. We introduce AppChain model where applications are developed with loose coupling with blockchain and interract with it via gRpc calls through rich API. 
It allows to develop applications quicker in a programing language the developers are used to. Moreover it allows applications to interact with blockchain in more agile way and to react on events more sensitively.

## Plugin
Plugins are the way to develop financial products extending functionality of Gagarin.network. They are similar to Ethereum smart contracts, but have more power in extending underlying blockchain.  
API is a generalized framework that simplifies the process of building secure blockchain applications on top of Gagarin.network. Plugins help keep Gagarin.network highly modular and allows to create an ecosystem of modules that allows developers to easily spin up application-specific blockchains without having to code each bit of functionality of their application from scratch.
Anyone can create a module, and use of Services and other already built plugins in your product is as simple as communicating with service via gRpc. These modules can be used by another developer or a team if they build a new product and are allowed to use them.

Plugin is a piece of software which provides gRpc services and interacts with Gagarin.network via gRpc calls. Plugin implementers decide what data and events they need to receive from the blockchain and they implement only needed interfaces. Callbacks are synchronous way to receive needed event information from blockchain. Although there is asynchronous way for Plugin to obtain additional static data from  the blockchain through monitoring service and common requests. More about it is in [monitoring](monitoring.md) section. 

Services are docker containers, they should be run on the same virtual network where Gagarin.network runs. We strongly recommend to develop Plugins this way too, since docker containers fully meet our vision on cloud friendly blockchains. 

There is special plugin block in startup config. Please see how to enable plugin in [startup](startup.md) section. 

Plugins not necessary are run on every node in the network, for example it is pretty normal to run rollups on subset of nodes and to slightly reduce rollup security. Plugins always start before node and should be developed with this in mind. To update plugin we simply restart docker container and that's it. 

It is absolutely normal to run several plugins on single node. In this case plugins will be called in sequence, in order they are configured in settings.

## Service
Plugin developed and provided by our team is called service. Services usually use the same API provided for plugin development and additional built-in features. 
In [tutorial](tutorial.md) we discuss development of rollups plugin in details with code snippets.  
