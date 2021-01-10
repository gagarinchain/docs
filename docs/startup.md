---
id: startup
title: Configuration
sidebar_label: Configuration
---

## Node
We widely use [cobra](https://github.com/spf13/cobra) - a library for creating powerful modern CLI applications.

Node expose 2 different ports: 9080 for network communication between peers and 9180 for websocket communication
### Commands
Node can be run in different modes, which can be set with run commands
#### start
Is used to start network node
#### tx_send
Utilit program. Is used to send transactions to the network
#### rpc_send
Utilit program. Is used to send rpc calls to the network
#### version
Outputs network version

### Docker
Gagarin.network is provided as docker container, for example we start network here on single Docker machine
1. We optionally create local virtual network 
```docker network create --driver=bridge --subnet=172.18.0.0/16 gagarin	```

2. We run network
``` 
docker run --net gagarin --ip 172.18.0.10 -it \
                         -e GN_ME=0 \
                         -e GN_SETTINGS=/app/ext/settings.yaml \
                         -e COMMAND=start \
                         -e GN_RPC=172.18.0.10:9280 \
                         -v /Users/dabasov/static:/app/ext \
                         -p 9080:9080 -p 9180:9180 -p 9280:9280 start 243c98e959da
``` 
### Environment
 Environment variables can be passed in three different ways. Further you can find mapping
| Parameter (short) | Env | Settings | Desc |
|---|---|---|---|
| config | GN_SETTINGS | - | Path to settings.yaml file |
| me (m) | GN_INDEX | hotstuff.me | Current node index in committee |
| rpc.address (r) | GN_RPC | rpc.address | Enables grpc service on this address |
| extaddr (a) | GN_EXTADDR | network.ExtAddr | Current node external address for NAT lookup |
| plugins.address (p) | GN_PLUGIN | plugins.address | Plugin service address |
| plugins.interfaces (i) | GN_PLUGIN_I | plugins.interfaces | Plugin interfaces |

Variables are overridden in order. The most common variables are loaded from config, then more specific are taken from program parameters and then the most specific are loaded from ENV variables.

### Configuration files
#### peers.json 
This file describes all network peers and maps their blockchain addresses to network identities for fee accumulation. Address of peer with address = 16Uiu2HAmGgeX9Sr75ofG4rQbUhRiUH2AuKii5QCdD9h8NT83afo4 will be extended through peer discovery.
```
{
	"peers": [ #list of bootstrap peers
		{
			"addr": "0xDd9811Cfc24aB8d56036A8ecA90C7B8C75e35950",
			"pub": "8d00d7cea8f1f6edc961fe2867ffb94a1e78ef8b8eb416d6f5b7b3f6dd9811cfc24ab8d56036a8eca90c7b8c75e35950",
			"MultiAddress": "/ip4/172.18.0.10/tcp/9080/p2p/16Uiu2HAmGgeX9Sr75ofG4rQbUhRiUH2AuKii5QCdD9h8NT83afo4"
		},
  ...
```

- ``addr`` - blockchain addr
- ``pub`` - blockchain G1 public key, we need it to prevent rogue key attack and to aggregate signatures
- ``MultiAddress`` - libp2p multiaddr

#### peer(i).json
These N files (N for committee size) describe every peer in the network. Current node should have only one file where i equals its number in committe.
 
```
{
	"addr": "0xA60c85Be9c2b8980Dbd3F82cF8CE19DE12f3E829",
	"id": "16Uiu2HAmCRVJB9iKxon89fp8J25KvEgkEmgViLnaYi7A9aiZoSpy", 
	"pk": "4a157ef4295be2413c59613cd5dd4f3b0688ac6227709a9634608f33a49250ef",
	"pkpeer": "080212208ceba2eb4883bfd2638dd37807b9986ea9ce18319b4bcf663fafb007db3087e6" 
	"pub": "8d00d7cea8f1f6edc961fe2867ffb94a1e78ef8b8eb416d6f5b7b3f6dd9811cfc24ab8d56036a8eca90c7b8c75e35950"

}
```
- ``addr`` - blockchain addr
- ``id`` - libp2p peer id (public ECDSA key)
- ``pk`` - blockchain private key
- ``pkpeer`` - libp2p peer private ECDSA key
- ``pub`` - blockchain pub key

#### seed.json 
This file contains starting state
```
{
  "accounts": [ #account list
    {
      "address": "0xA60c85Be9c2b8980Dbd3F82cF8CE19DE12f3E829",
      "balance": 1000
    },
    ...
```
- ``address`` - blockchain address
- ``balance`` - starting balance

#### settings.yaml
Main config file that contains all node parameters
```
Hotstuff:
  CommitteeSize: 10
  Me: 0
  Delta: 5000
  BlockDelta: 10
  SeedPath: static/seed.json
Network: 
  ExtAddr: /ip4/10.10.13.161/tcp/9080
  MinPeerThreshold: 3 
  ReconnectPeriod: 10000 
  ConnectionTimeout: 3000
Storage:
  Dir: /var/folders/m7/c56_pk2n0dj4xbplcndc9d140000gn/T/
Static:
  Dir: /Users/dabasov/Projects/gagarin/network/static
Log:
  Level: INFO
Plugins:
  Address: 'localhost:9380'
  Interfaces: ['OnBlockCommit', 'OnReceiveProposal', 'OnNewBlockCreated'] 
Rpc:
  Address: 'localhost:9480'
  MaxConcurrentStreams: 10 
```

``Hotstuff`` - hotstuff settings 
- ``CommitteeSize`` - total node amount, must be 3 * n + 1, here n = 3
- ``Me`` - my index in committee
- ``Delta`` - stage duration in milliseconds, 2*Delta is v iew change duration, 4* Delta is GST
- ``BlockDelta`` - max time in milliseconds to wait for transactions 
- ``SeedPath`` - path to seed file 

``Network`` - network settings
- ``ExtAddr`` - address which us used to self introduce in network, can contain relay address
- ``MinPeerThreshold`` - minimum peer count to bootstrap connection, from bootstrap list
- ``ReconnectPeriod`` - period after watchdog checks bootstrap connections and reconnects whether count less then 
- ``ConnectionTimeout`` - common connection timeout

``Storage`` - storage settings
- ``Dir`` - storage dir

``Static`` - static settings
- ``Dir`` - path to static

``Log`` - log settings
- ``Level`` - log level 

``Plugins`` - plugins configuration
- ``Address`` - plugin address
- ``Interfaces`` - plugin supported services

``Rpc`` - gRpc settings
- ``Address`` - address to run rpc service on
- ``MaxConcurrentStreams`` - max concurrent service connections
