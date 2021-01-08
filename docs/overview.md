---
id: overview
title: Overview
sidebar_label: Overview
---

Gagarin.network is a fast, secure and decentralized enterprise blockchain platform aiming to make stablecoins issuance easy and operation of existing ERC-20 tokens cheaper and faster.

With Gagarin.network you get:

- Cloud-friendly model 
Using docker and kubernetes the network can be deployed and managed on any cloud platform and bare metal server. For early product development we can provide network that is set up in amazon or google cloud. Once the product becomes mature and consortium gets ready to run the network it can be easily migrated to a different environment.
- Hotstuff consensus protocol
Hotstuff is a state of the art protocol designed by Cornel university scientists. Hotstuff is a BFT protocol developing PBFT ideas. It has formal mathematical proof of liveness and correctness and is used by several leading blockchain projects. 
- BLS cryptoraphy
We chose to use advanced crypto-schemes based on elliptic curve bls12-381. Cryptography based on bls12-381 allows to materialize broad functionality via cryptographic primitives which we used to develop the following services: signatures aggregation, zero-knowledge private transactions, identity-based keys issuence. 
Мы выбрали современные крипто-схемы, основанные на  эллиптической кривой bls12-381. Криптография, основанная на bls12-381 позволяет с помощью криптографических примитивов реализовывать широкий функционал, который мы используем для построения сервисов: Агрегация подписей, zero-knowledge private transactions, identity-based keys issuence.
- Libp2p networking
Libp2p is a network layer extracted from IPFS (the largest decentralized file system) which materializes functionality necessary for a sophisticated decentralized application.
Libp2p - выделенный из IPFS (крупнейшая децентрализованная файловая система) сетевой слой, который реализует весь необходимый для современного децентрализованного приложения функционал.
-  App Chains
Each application or group of applications on Gagarin.network form an independent blockchain which consists of platform code and plugin code.  The product and the platform interact through API and system of oracles.  Such approach significantly facilitates deployment and development of applications, does not require the developer to study new program languages and allows fast start of development.
Каждое приложение на Gagarin.network или семейтво приложений является независимым блокчейном, состоящим из кода платформы и кода плагина. Взаимодействие между продуктом и платформой происходит через API и систему ораклов.
Такой подход существенно облегчает деплоймент и разработку приложений, не требует от разработчика изученияновых языков программирования и позволяет быстро приступить к разработке продукта.
- Utility-token
We provide ready-to-use cryptocurrency and services for additional fuctionality. The cryptocurrency can be used for stablecoin or token issue, charging of fees, payments in the network and other utility functions and participation in PoS protocol. 
Мы предоставляем готовую к использованию криптовалюту и облегчающие ее использование сервисы. 
Криптовалюта может быть использована  для: создания стейблкоина или токена, взимания комиссий, осуществления расчетов внутри сети  и других utility функций, участия в PoS протоколе
- KyC AML
The service provides basic functions for client identification, granting and termination of access rights to conduct operations with the blockchain. Also the service provides tools for research and monitoring of clients' operations.
Сервис предлагает базовые функции по идентификации клиента, предоставлению и отзыву права осуществлять операции с блокчейном.
Также сервис предоставляет механизмы поиска и мониторинга операций клиента.
- Wallet и Block explorer
Wallet and Block Explorer enable the users to interact with the blockchain in different ways: recieve information on issued tokens, transactions, perform various actions to the tokens through the web interface.
Wallet и Block Explorer дают возможность пользователям системы различными способами взаимодействовать с блокчейном: получать информацию о выпущенных блоках, транзакциях,  осуществлять различные действия с токенами через web интерфейс.
- Permission сервис
The service allows to autentificate participants of the network and authorize their actions. Each participant in the network has his own identificator which is given based on ECDSA encryption keys used to protect data sent in the network. The service allows to limit unauthorized actions by the participants, avoid unacceptable nodes from the network, perform transactions. Network key is used also as node identificator in the blockchain.
Сервис предоставляет возможность аутентифицировать участников сети и авторизовывать их действия. Каждый участник в системе имеет уникальный идентификатор, который выдается на основании ECDSA ключей шифрования, участвующих в защите передаваемых по сети данных. Сервис позволяет ограничивать участников в осуществлении несанкционированных действий, исключать нежелательные ноды из сети, осуществлять транзакции. Сетевой ключ используется также в качестве идентификатора нода в сети блокчейна.
- Hotstuff Rollups
We developed Hotstuff Rollup mechanism which is based on rollups and adds BLS signature to them.The BLS signature is obtained as a result of aggregation of validators' signatures and is used in quorum certificate. Thus in the main chain we store a short summary on all transactions performed in Gagarin.network as well as proof that the network achieved consensus on this data and finalized it. A contract in the main-chain manages tokens, shows transactions of a product and synchronizes the state of two blockchains.
Мы разработали механизм Hotstuff Rollup, который базируется на свертках и добавляет к ним BLS подпись, полученную в результате агрегации подписей валидаторов и используемую в quorum certificate. Таким образом в main-chain хранится краткая информация о всех операциях Gagarin.network, а также подтверждение того, что эти транзакции получены в результате консенсуса и финализированы. Контракт в main-chain управляет токенами, отражает транзакции продукта и синхронизирует состояния двух блокчейнов. 
- Interoperability
Full scale stablecoin operations require its integration with the outside world. Oracles are used to import facts from the outside world to the blockchain. Such import can be necessary, for expample, in order to lock resources in the real world as stablecoin's security. Participants of the network may need a service for locking funds on bank accounts, token issue, etc. Для полноценной работы стейблкоина необходима его интеграция с внешним миром. Ораклы предназначены для импорта фактов из внешнего мира в блокчейн. Такой импорт может потребоваться, например, для блокировки ресурсов в реальном мире под обеспечение стейблкоина. Участникам сети может понадобиться сервис по блокировке средств на банковских счетах, для эмиссии токенов и т.д.
-   Oracle service
Any participant of the network can import events and facts from the real world to Gagarin.chain independently which helps to maintain high level of the platform decentralization. Импорт событий и фактов из внешнего мира в Gagarin.chain осуществляется каждым участником сети независимо друг от друга, что призвано сохранить высокий уровень децентрализации всей платформы. 
- Proof of stake (TBD)
Hotstuff just like any other BFT protocol ensures security and consensus if no more than one third of the participants are violators. Motivation of the network participant not to perform violations remains outside the protocol. In most cases it is enough for private blockchains as the validators of the network are always known in advance and there are many administrative methods to prevent violations. However  if the network participants would like to create an algorythm for such a situation and set a procudure for sanctions against violators on the platform level we allowed for add-on to BTF consensus protocol in the form of proof-of-stake protocol.
Hotstuff, как и любой протокол семейства BFT, обеспечивает безопасность и консенсус в присутствии не более, чем трети злоумышленников. Стимул участника сети не совершать нарушения остается вне протокола. В большинстве случаев private блокчейнов этого достаточно, так как валидаторы сети всегда известны заранее и имеется множество разнообразных административных методов по борьбе с нарушениями. Однако для случаев, когда участники сети хотят алгоритмизировать эту ситуацию и прописать правила наказания злоумышленника на уровне платформы, мы предусмотрели надстройку над BFT протоколом консенсуса в виде proof-of-stake протокола. 
- Light clients (TBD)
Light clients allow to avoid storing the state of the whole system by every network participant locally. A participant can process only data he needs and in the same time validate and vote for any block, thus he does not differ from full scale nodes funtionally. Use of light clients allows to avoid storing of signficant data amount locally without decrease of security level. It enables to create in-memory blockchain node that does not require use of local stogare.
Легкие клиенты позволяют не хранить стейт всей системы локально у каждого участника сети. Участник может обрабатывать только необходимую информацию и при этом валидировать и голосовать за любые блоки, таким образом функционально он не будет никак отличаться от полноценных нодов. Использование light clients позволит отказаться от хранения существенных объемов информации локально без ущерба безопасности. Это позволит создать in-memory блокчейн нод, для работы которого не требуется локальное хранилище.
- ZK privacy transactions (TBD)
In order to withhold data on transactions between the participants of the network we created a second level protocol, added on Hotstuff consensus protocol, and a special second level network running that protocol. Common nodes-validators ensure the network operations. Для сокрытия информации об операциях между участниками сети создается протокол второго уровня, построенный над протоколом консенсуса Hotstuff, и специальная сеть второго уровня, реализующая этот протокол. Работу сетей обеспечивают общие ноды-валидаторы.
