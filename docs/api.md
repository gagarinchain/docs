# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [api.proto](#api.proto)
    - [AfterProposedBlockAddedRequest](#gagarin.network.api.AfterProposedBlockAddedRequest)
    - [AfterProposedBlockAddedResponse](#gagarin.network.api.AfterProposedBlockAddedResponse)
    - [AfterVotedRequest](#gagarin.network.api.AfterVotedRequest)
    - [AfterVotedResponse](#gagarin.network.api.AfterVotedResponse)
    - [BeforeProposedBlockAddedRequest](#gagarin.network.api.BeforeProposedBlockAddedRequest)
    - [BeforeProposedBlockAddedResponse](#gagarin.network.api.BeforeProposedBlockAddedResponse)
    - [BeforeVotedRequest](#gagarin.network.api.BeforeVotedRequest)
    - [BeforeVotedResponse](#gagarin.network.api.BeforeVotedResponse)
    - [ContainsRequest](#gagarin.network.api.ContainsRequest)
    - [ContainsResponse](#gagarin.network.api.ContainsResponse)
    - [ExecuteTransactionRequest](#gagarin.network.api.ExecuteTransactionRequest)
    - [ExecuteTransactionResponse](#gagarin.network.api.ExecuteTransactionResponse)
    - [GetAccountRequest](#gagarin.network.api.GetAccountRequest)
    - [GetAccountResponse](#gagarin.network.api.GetAccountResponse)
    - [GetBlockByHashRequest](#gagarin.network.api.GetBlockByHashRequest)
    - [GetBlockByHashResponse](#gagarin.network.api.GetBlockByHashResponse)
    - [GetBlockByHeightRequest](#gagarin.network.api.GetBlockByHeightRequest)
    - [GetBlockByHeightResponse](#gagarin.network.api.GetBlockByHeightResponse)
    - [GetCommitteeRequest](#gagarin.network.api.GetCommitteeRequest)
    - [GetCommitteeResponse](#gagarin.network.api.GetCommitteeResponse)
    - [GetCurrentEpochRequest](#gagarin.network.api.GetCurrentEpochRequest)
    - [GetCurrentEpochResponse](#gagarin.network.api.GetCurrentEpochResponse)
    - [GetCurrentViewRequest](#gagarin.network.api.GetCurrentViewRequest)
    - [GetCurrentViewResponse](#gagarin.network.api.GetCurrentViewResponse)
    - [GetForkRequest](#gagarin.network.api.GetForkRequest)
    - [GetForkResponse](#gagarin.network.api.GetForkResponse)
    - [GetGenesisBlockRequest](#gagarin.network.api.GetGenesisBlockRequest)
    - [GetGenesisBlockResponse](#gagarin.network.api.GetGenesisBlockResponse)
    - [GetHeadRequest](#gagarin.network.api.GetHeadRequest)
    - [GetHeadResponse](#gagarin.network.api.GetHeadResponse)
    - [GetProposerForViewRequest](#gagarin.network.api.GetProposerForViewRequest)
    - [GetProposerForViewResponse](#gagarin.network.api.GetProposerForViewResponse)
    - [GetThreeChainRequest](#gagarin.network.api.GetThreeChainRequest)
    - [GetThreeChainResponse](#gagarin.network.api.GetThreeChainResponse)
    - [GetTopCommittedBlockRequest](#gagarin.network.api.GetTopCommittedBlockRequest)
    - [GetTopCommittedBlockResponse](#gagarin.network.api.GetTopCommittedBlockResponse)
    - [GetTopHeightBlockRequest](#gagarin.network.api.GetTopHeightBlockRequest)
    - [GetTopHeightBlockResponse](#gagarin.network.api.GetTopHeightBlockResponse)
    - [GetTopHeightRequest](#gagarin.network.api.GetTopHeightRequest)
    - [GetTopHeightResponse](#gagarin.network.api.GetTopHeightResponse)
    - [GetTransactionRequest](#gagarin.network.api.GetTransactionRequest)
    - [GetTransactionResponse](#gagarin.network.api.GetTransactionResponse)
    - [IsSiblingRequest](#gagarin.network.api.IsSiblingRequest)
    - [IsSiblingResponse](#gagarin.network.api.IsSiblingResponse)
    - [OnBlockCommitRequest](#gagarin.network.api.OnBlockCommitRequest)
    - [OnBlockCommitResponse](#gagarin.network.api.OnBlockCommitResponse)
    - [OnNewBlockCreatedRequest](#gagarin.network.api.OnNewBlockCreatedRequest)
    - [OnNewBlockCreatedResponse](#gagarin.network.api.OnNewBlockCreatedResponse)
    - [OnNextEpochRequest](#gagarin.network.api.OnNextEpochRequest)
    - [OnNextEpochResponse](#gagarin.network.api.OnNextEpochResponse)
    - [OnNextViewRequest](#gagarin.network.api.OnNextViewRequest)
    - [OnNextViewResponse](#gagarin.network.api.OnNextViewResponse)
    - [OnProposalRequest](#gagarin.network.api.OnProposalRequest)
    - [OnProposalResponse](#gagarin.network.api.OnProposalResponse)
    - [OnQCFinishedRequest](#gagarin.network.api.OnQCFinishedRequest)
    - [OnQCFinishedResponse](#gagarin.network.api.OnQCFinishedResponse)
    - [OnVoteReceivedRequest](#gagarin.network.api.OnVoteReceivedRequest)
    - [OnVoteReceivedResponse](#gagarin.network.api.OnVoteReceivedResponse)
  
    - [CommonService](#gagarin.network.api.CommonService)
    - [OnBlockCommit](#gagarin.network.api.OnBlockCommit)
    - [OnNewBlockCreated](#gagarin.network.api.OnNewBlockCreated)
    - [OnNextEpoch](#gagarin.network.api.OnNextEpoch)
    - [OnNextView](#gagarin.network.api.OnNextView)
    - [OnProposal](#gagarin.network.api.OnProposal)
    - [OnReceiveProposal](#gagarin.network.api.OnReceiveProposal)
    - [OnVoteReceived](#gagarin.network.api.OnVoteReceived)
  
- [event.proto](#event.proto)
    - [AccountE](#gagarin.network.event.AccountE)
    - [AccountRequestPayload](#gagarin.network.event.AccountRequestPayload)
    - [AccountResponsePayload](#gagarin.network.event.AccountResponsePayload)
    - [AccountUpdatedPayload](#gagarin.network.event.AccountUpdatedPayload)
    - [CommittedPayload](#gagarin.network.event.CommittedPayload)
    - [EpochStartedPayload](#gagarin.network.event.EpochStartedPayload)
    - [Event](#gagarin.network.event.Event)
    - [Request](#gagarin.network.event.Request)
    - [ViewChangedPayload](#gagarin.network.event.ViewChangedPayload)
  
    - [Event.EventType](#gagarin.network.event.Event.EventType)
    - [Request.RequestType](#gagarin.network.event.Request.RequestType)
  
- [storage.proto](#storage.proto)
    - [Account](#gagarin.network.storage.Account)
    - [BlockDataS](#gagarin.network.storage.BlockDataS)
    - [BlockHeaderS](#gagarin.network.storage.BlockHeaderS)
    - [BlockS](#gagarin.network.storage.BlockS)
    - [Entry](#gagarin.network.storage.Entry)
    - [Peer](#gagarin.network.storage.Peer)
    - [QuorumCertificateS](#gagarin.network.storage.QuorumCertificateS)
    - [Receipt](#gagarin.network.storage.Receipt)
    - [Record](#gagarin.network.storage.Record)
    - [SignatureAggregateS](#gagarin.network.storage.SignatureAggregateS)
    - [SignatureS](#gagarin.network.storage.SignatureS)
    - [Snapshot](#gagarin.network.storage.Snapshot)
    - [TransactionS](#gagarin.network.storage.TransactionS)
  
- [Scalar Value Types](#scalar-value-types)



<a name="api.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## api.proto



<a name="gagarin.network.api.AfterProposedBlockAddedRequest"></a>

### AfterProposedBlockAddedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| proposal | [gagarin.network.core.ProposalPayload](#gagarin.network.core.ProposalPayload) |  | Proposal that was added |
| receipts | [gagarin.network.storage.Receipt](#gagarin.network.storage.Receipt) | repeated | Receipts that was created during block&#39;s transactions application |






<a name="gagarin.network.api.AfterProposedBlockAddedResponse"></a>

### AfterProposedBlockAddedResponse







<a name="gagarin.network.api.AfterVotedRequest"></a>

### AfterVotedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| vote | [gagarin.network.core.VotePayload](#gagarin.network.core.VotePayload) |  | Vote message |






<a name="gagarin.network.api.AfterVotedResponse"></a>

### AfterVotedResponse







<a name="gagarin.network.api.BeforeProposedBlockAddedRequest"></a>

### BeforeProposedBlockAddedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| proposal | [gagarin.network.core.ProposalPayload](#gagarin.network.core.ProposalPayload) |  | Proposal to be added |






<a name="gagarin.network.api.BeforeProposedBlockAddedResponse"></a>

### BeforeProposedBlockAddedResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| proposal | [gagarin.network.core.ProposalPayload](#gagarin.network.core.ProposalPayload) |  | Proposal to be added |






<a name="gagarin.network.api.BeforeVotedRequest"></a>

### BeforeVotedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| vote | [gagarin.network.core.VotePayload](#gagarin.network.core.VotePayload) |  | Vote message |






<a name="gagarin.network.api.BeforeVotedResponse"></a>

### BeforeVotedResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| vote | [gagarin.network.core.VotePayload](#gagarin.network.core.VotePayload) |  | Vote message |






<a name="gagarin.network.api.ContainsRequest"></a>

### ContainsRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.ContainsResponse"></a>

### ContainsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| res | [bool](#bool) |  |  |






<a name="gagarin.network.api.ExecuteTransactionRequest"></a>

### ExecuteTransactionRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| tx | [gagarin.network.storage.TransactionS](#gagarin.network.storage.TransactionS) |  |  |






<a name="gagarin.network.api.ExecuteTransactionResponse"></a>

### ExecuteTransactionResponse







<a name="gagarin.network.api.GetAccountRequest"></a>

### GetAccountRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [bytes](#bytes) |  |  |
| hash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.GetAccountResponse"></a>

### GetAccountResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account | [gagarin.network.storage.Account](#gagarin.network.storage.Account) |  |  |






<a name="gagarin.network.api.GetBlockByHashRequest"></a>

### GetBlockByHashRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.GetBlockByHashResponse"></a>

### GetBlockByHashResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |






<a name="gagarin.network.api.GetBlockByHeightRequest"></a>

### GetBlockByHeightRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| height | [int32](#int32) |  |  |






<a name="gagarin.network.api.GetBlockByHeightResponse"></a>

### GetBlockByHeightResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| blocks | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) | repeated |  |






<a name="gagarin.network.api.GetCommitteeRequest"></a>

### GetCommitteeRequest







<a name="gagarin.network.api.GetCommitteeResponse"></a>

### GetCommitteeResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| peer | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) | repeated |  |






<a name="gagarin.network.api.GetCurrentEpochRequest"></a>

### GetCurrentEpochRequest







<a name="gagarin.network.api.GetCurrentEpochResponse"></a>

### GetCurrentEpochResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| epoch | [int32](#int32) |  |  |






<a name="gagarin.network.api.GetCurrentViewRequest"></a>

### GetCurrentViewRequest







<a name="gagarin.network.api.GetCurrentViewResponse"></a>

### GetCurrentViewResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| view | [int32](#int32) |  |  |






<a name="gagarin.network.api.GetForkRequest"></a>

### GetForkRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| height | [int32](#int32) |  |  |
| headHash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.GetForkResponse"></a>

### GetForkResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| blocks | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) | repeated |  |






<a name="gagarin.network.api.GetGenesisBlockRequest"></a>

### GetGenesisBlockRequest







<a name="gagarin.network.api.GetGenesisBlockResponse"></a>

### GetGenesisBlockResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |






<a name="gagarin.network.api.GetHeadRequest"></a>

### GetHeadRequest







<a name="gagarin.network.api.GetHeadResponse"></a>

### GetHeadResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |






<a name="gagarin.network.api.GetProposerForViewRequest"></a>

### GetProposerForViewRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| view | [int32](#int32) |  |  |






<a name="gagarin.network.api.GetProposerForViewResponse"></a>

### GetProposerForViewResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| peer | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  |  |






<a name="gagarin.network.api.GetThreeChainRequest"></a>

### GetThreeChainRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.GetThreeChainResponse"></a>

### GetThreeChainResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| zero | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |
| one | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |
| two | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |






<a name="gagarin.network.api.GetTopCommittedBlockRequest"></a>

### GetTopCommittedBlockRequest







<a name="gagarin.network.api.GetTopCommittedBlockResponse"></a>

### GetTopCommittedBlockResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |






<a name="gagarin.network.api.GetTopHeightBlockRequest"></a>

### GetTopHeightBlockRequest







<a name="gagarin.network.api.GetTopHeightBlockResponse"></a>

### GetTopHeightBlockResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  |  |






<a name="gagarin.network.api.GetTopHeightRequest"></a>

### GetTopHeightRequest







<a name="gagarin.network.api.GetTopHeightResponse"></a>

### GetTopHeightResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| height | [int32](#int32) |  |  |






<a name="gagarin.network.api.GetTransactionRequest"></a>

### GetTransactionRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.GetTransactionResponse"></a>

### GetTransactionResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| tx | [gagarin.network.storage.TransactionS](#gagarin.network.storage.TransactionS) |  |  |






<a name="gagarin.network.api.IsSiblingRequest"></a>

### IsSiblingRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| siblingHash | [bytes](#bytes) |  |  |
| ancestorHash | [bytes](#bytes) |  |  |






<a name="gagarin.network.api.IsSiblingResponse"></a>

### IsSiblingResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| res | [bool](#bool) |  |  |






<a name="gagarin.network.api.OnBlockCommitRequest"></a>

### OnBlockCommitRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  | Block that was committed |
| orphans | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) | repeated | Forked Blocks that were rejected during commit |






<a name="gagarin.network.api.OnBlockCommitResponse"></a>

### OnBlockCommitResponse







<a name="gagarin.network.api.OnNewBlockCreatedRequest"></a>

### OnNewBlockCreatedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  | Block that was created |
| receipts | [gagarin.network.storage.Receipt](#gagarin.network.storage.Receipt) | repeated | Receipts that was created during block&#39;s transactions application |






<a name="gagarin.network.api.OnNewBlockCreatedResponse"></a>

### OnNewBlockCreatedResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| block | [gagarin.network.storage.BlockS](#gagarin.network.storage.BlockS) |  | Modified block |






<a name="gagarin.network.api.OnNextEpochRequest"></a>

### OnNextEpochRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| newEpoch | [int32](#int32) |  | Epoch number |






<a name="gagarin.network.api.OnNextEpochResponse"></a>

### OnNextEpochResponse







<a name="gagarin.network.api.OnNextViewRequest"></a>

### OnNextViewRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| newView | [int32](#int32) |  | View number |






<a name="gagarin.network.api.OnNextViewResponse"></a>

### OnNextViewResponse







<a name="gagarin.network.api.OnProposalRequest"></a>

### OnProposalRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  |  |
| proposal | [gagarin.network.core.ProposalPayload](#gagarin.network.core.ProposalPayload) |  |  |






<a name="gagarin.network.api.OnProposalResponse"></a>

### OnProposalResponse







<a name="gagarin.network.api.OnQCFinishedRequest"></a>

### OnQCFinishedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| qc | [gagarin.network.storage.QuorumCertificateS](#gagarin.network.storage.QuorumCertificateS) |  | Created quorum certificate |






<a name="gagarin.network.api.OnQCFinishedResponse"></a>

### OnQCFinishedResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| qc | [gagarin.network.storage.QuorumCertificateS](#gagarin.network.storage.QuorumCertificateS) |  | Modified quorum certificate |






<a name="gagarin.network.api.OnVoteReceivedRequest"></a>

### OnVoteReceivedRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| me | [gagarin.network.storage.Peer](#gagarin.network.storage.Peer) |  | Self peer of this node |
| vote | [gagarin.network.core.VotePayload](#gagarin.network.core.VotePayload) |  | Vote message |






<a name="gagarin.network.api.OnVoteReceivedResponse"></a>

### OnVoteReceivedResponse






 

 

 


<a name="gagarin.network.api.CommonService"></a>

### CommonService
Pull service

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetBlockByHash | [GetBlockByHashRequest](#gagarin.network.api.GetBlockByHashRequest) | [GetBlockByHashResponse](#gagarin.network.api.GetBlockByHashResponse) | returns block if found by hash, or empty if absent |
| GetBlocksByHeight | [GetBlockByHeightRequest](#gagarin.network.api.GetBlockByHeightRequest) | [GetBlockByHeightResponse](#gagarin.network.api.GetBlockByHeightResponse) | returns blocks if found by height, or empty list if absent |
| GetFork | [GetForkRequest](#gagarin.network.api.GetForkRequest) | [GetForkResponse](#gagarin.network.api.GetForkResponse) | returns blocks fork with head at headHash and having height blocks in it, or empty list if absent |
| Contains | [ContainsRequest](#gagarin.network.api.ContainsRequest) | [ContainsResponse](#gagarin.network.api.ContainsResponse) | returns true if block with that hash is in the blockchain, or empty if absent |
| GetThreeChain | [GetThreeChainRequest](#gagarin.network.api.GetThreeChainRequest) | [GetThreeChainResponse](#gagarin.network.api.GetThreeChainResponse) | returns three chain starting at block with hash, or empty if absent |
| GetHead | [GetHeadRequest](#gagarin.network.api.GetHeadRequest) | [GetHeadResponse](#gagarin.network.api.GetHeadResponse) | returns block with max height of blockchain, we can&#39;t have more than one block on top height |
| GetTopHeight | [GetTopHeightRequest](#gagarin.network.api.GetTopHeightRequest) | [GetTopHeightResponse](#gagarin.network.api.GetTopHeightResponse) | returns max height of blockchain, we can&#39;t have more than one block on top height |
| GetTopHeightBlock | [GetTopHeightBlockRequest](#gagarin.network.api.GetTopHeightBlockRequest) | [GetTopHeightBlockResponse](#gagarin.network.api.GetTopHeightBlockResponse) | returns block with max height of blockchain, we can&#39;t have more than one block on top height |
| GetGenesisBlock | [GetGenesisBlockRequest](#gagarin.network.api.GetGenesisBlockRequest) | [GetGenesisBlockResponse](#gagarin.network.api.GetGenesisBlockResponse) | returns genesis block |
| IsSibling | [IsSiblingRequest](#gagarin.network.api.IsSiblingRequest) | [IsSiblingResponse](#gagarin.network.api.IsSiblingResponse) | returns true if two blocks with given hashes are reachable through their parent-child relationship |
| GetAccount | [GetAccountRequest](#gagarin.network.api.GetAccountRequest) | [GetAccountResponse](#gagarin.network.api.GetAccountResponse) | returns account at a given block by address and block hash, if hash is empty head version will be returned |
| GetTransaction | [GetTransactionRequest](#gagarin.network.api.GetTransactionRequest) | [GetTransactionResponse](#gagarin.network.api.GetTransactionResponse) | returns transaction by hash |
| GetProposerForView | [GetProposerForViewRequest](#gagarin.network.api.GetProposerForViewRequest) | [GetProposerForViewResponse](#gagarin.network.api.GetProposerForViewResponse) | returns peer, that proposed on given view number |
| GetCommittee | [GetCommitteeRequest](#gagarin.network.api.GetCommitteeRequest) | [GetCommitteeResponse](#gagarin.network.api.GetCommitteeResponse) | returns committee of peers |
| GetCurrentView | [GetCurrentViewRequest](#gagarin.network.api.GetCurrentViewRequest) | [GetCurrentViewResponse](#gagarin.network.api.GetCurrentViewResponse) | returns current view |
| GetCurrentEpoch | [GetCurrentEpochRequest](#gagarin.network.api.GetCurrentEpochRequest) | [GetCurrentEpochResponse](#gagarin.network.api.GetCurrentEpochResponse) | returns current epoch |
| GetTopCommittedBlock | [GetTopCommittedBlockRequest](#gagarin.network.api.GetTopCommittedBlockRequest) | [GetTopCommittedBlockResponse](#gagarin.network.api.GetTopCommittedBlockResponse) | returns top committed block |
| ExecuteTransaction | [ExecuteTransactionRequest](#gagarin.network.api.ExecuteTransactionRequest) | [ExecuteTransactionResponse](#gagarin.network.api.ExecuteTransactionResponse) | adds transaction to tx_pool |


<a name="gagarin.network.api.OnBlockCommit"></a>

### OnBlockCommit
Used when block is commited, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OnBlockCommit | [OnBlockCommitRequest](#gagarin.network.api.OnBlockCommitRequest) | [OnBlockCommitResponse](#gagarin.network.api.OnBlockCommitResponse) | Called after block is committed |


<a name="gagarin.network.api.OnNewBlockCreated"></a>

### OnNewBlockCreated
Used when new block is created, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OnNewBlockCreated | [OnNewBlockCreatedRequest](#gagarin.network.api.OnNewBlockCreatedRequest) | [OnNewBlockCreatedResponse](#gagarin.network.api.OnNewBlockCreatedResponse) | Called when transactions are applied and block is ready to be proposed |


<a name="gagarin.network.api.OnNextEpoch"></a>

### OnNextEpoch
Used when epoch is changed, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OnNextEpoch | [OnNextEpochRequest](#gagarin.network.api.OnNextEpochRequest) | [OnNextEpochResponse](#gagarin.network.api.OnNextEpochResponse) | Called when transitioned to next epoch |


<a name="gagarin.network.api.OnNextView"></a>

### OnNextView
Used when view is changed, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OnNextView | [OnNextViewRequest](#gagarin.network.api.OnNextViewRequest) | [OnNextViewResponse](#gagarin.network.api.OnNextViewResponse) | Called when transitioned to next view |


<a name="gagarin.network.api.OnProposal"></a>

### OnProposal
Used during proposing, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OnProposal | [OnProposalRequest](#gagarin.network.api.OnProposalRequest) | [OnProposalResponse](#gagarin.network.api.OnProposalResponse) | Called when proposal is created |


<a name="gagarin.network.api.OnReceiveProposal"></a>

### OnReceiveProposal
Used during processing proposal, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| BeforeProposedBlockAdded | [BeforeProposedBlockAddedRequest](#gagarin.network.api.BeforeProposedBlockAddedRequest) | [BeforeProposedBlockAddedResponse](#gagarin.network.api.BeforeProposedBlockAddedResponse) | Called before proposed block is added to blockchain |
| AfterProposedBlockAdded | [AfterProposedBlockAddedRequest](#gagarin.network.api.AfterProposedBlockAddedRequest) | [AfterProposedBlockAddedResponse](#gagarin.network.api.AfterProposedBlockAddedResponse) | Called after proposed block is added to blockchain |
| BeforeVoted | [BeforeVotedRequest](#gagarin.network.api.BeforeVotedRequest) | [BeforeVotedResponse](#gagarin.network.api.BeforeVotedResponse) | Called before replica voted for block |
| AfterVoted | [AfterVotedRequest](#gagarin.network.api.AfterVotedRequest) | [AfterVotedResponse](#gagarin.network.api.AfterVotedResponse) | Called after replica voted for block |


<a name="gagarin.network.api.OnVoteReceived"></a>

### OnVoteReceived
Used during processing received vote, synchronous

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OnVoteReceived | [OnVoteReceivedRequest](#gagarin.network.api.OnVoteReceivedRequest) | [OnVoteReceivedResponse](#gagarin.network.api.OnVoteReceivedResponse) | Called when vote is received |
| OnQCFinished | [OnQCFinishedRequest](#gagarin.network.api.OnQCFinishedRequest) | [OnQCFinishedResponse](#gagarin.network.api.OnQCFinishedResponse) | Called when quorum certificate is created |

 



<a name="event.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## event.proto



<a name="gagarin.network.event.AccountE"></a>

### AccountE



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [bytes](#bytes) |  |  |
| block | [bytes](#bytes) |  |  |
| nonce | [uint64](#uint64) |  |  |
| value | [uint64](#uint64) |  |  |
| proof | [bytes](#bytes) | repeated |  |






<a name="gagarin.network.event.AccountRequestPayload"></a>

### AccountRequestPayload



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [bytes](#bytes) |  |  |
| block | [bytes](#bytes) |  |  |






<a name="gagarin.network.event.AccountResponsePayload"></a>

### AccountResponsePayload



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account | [AccountE](#gagarin.network.event.AccountE) |  |  |






<a name="gagarin.network.event.AccountUpdatedPayload"></a>

### AccountUpdatedPayload



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| old | [AccountE](#gagarin.network.event.AccountE) |  |  |
| new | [AccountE](#gagarin.network.event.AccountE) |  |  |






<a name="gagarin.network.event.CommittedPayload"></a>

### CommittedPayload



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |






<a name="gagarin.network.event.EpochStartedPayload"></a>

### EpochStartedPayload



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| epoch | [int32](#int32) |  |  |






<a name="gagarin.network.event.Event"></a>

### Event



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| type | [Event.EventType](#gagarin.network.event.Event.EventType) |  |  |
| id | [bytes](#bytes) |  |  |
| payload | [google.protobuf.Any](#google.protobuf.Any) |  |  |






<a name="gagarin.network.event.Request"></a>

### Request



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| type | [Request.RequestType](#gagarin.network.event.Request.RequestType) |  |  |
| id | [bytes](#bytes) |  |  |
| payload | [google.protobuf.Any](#google.protobuf.Any) |  |  |






<a name="gagarin.network.event.ViewChangedPayload"></a>

### ViewChangedPayload



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| view | [int32](#int32) |  |  |





 


<a name="gagarin.network.event.Event.EventType"></a>

### Event.EventType


| Name | Number | Description |
| ---- | ------ | ----------- |
| RESERVED | 0 |  |
| BLOCK_ADDED | 1 |  |
| EPOCH_STARTED | 2 |  |
| VIEW_CHANGED | 3 |  |
| COMMITTED | 4 |  |
| ACCOUNT | 5 |  |
| BLOCK | 6 |  |



<a name="gagarin.network.event.Request.RequestType"></a>

### Request.RequestType


| Name | Number | Description |
| ---- | ------ | ----------- |
| ACCOUNT | 0 |  |
| BLOCK | 1 |  |


 

 

 



<a name="storage.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## storage.proto



<a name="gagarin.network.storage.Account"></a>

### Account



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| nonce | [uint64](#uint64) |  |  |
| value | [bytes](#bytes) |  |  |
| origin | [bytes](#bytes) |  |  |
| voters | [bytes](#bytes) | repeated |  |






<a name="gagarin.network.storage.BlockDataS"></a>

### BlockDataS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| data | [bytes](#bytes) |  |  |






<a name="gagarin.network.storage.BlockHeaderS"></a>

### BlockHeaderS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |
| parentHash | [bytes](#bytes) |  |  |
| qcHash | [bytes](#bytes) |  |  |
| dataHash | [bytes](#bytes) |  |  |
| txHash | [bytes](#bytes) |  |  |
| stateHash | [bytes](#bytes) |  |  |
| height | [int32](#int32) |  |  |
| timestamp | [int64](#int64) |  |  |






<a name="gagarin.network.storage.BlockS"></a>

### BlockS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| header | [BlockHeaderS](#gagarin.network.storage.BlockHeaderS) |  |  |
| cert | [QuorumCertificateS](#gagarin.network.storage.QuorumCertificateS) |  |  |
| signatureAggregate | [SignatureAggregateS](#gagarin.network.storage.SignatureAggregateS) |  |  |
| data | [BlockDataS](#gagarin.network.storage.BlockDataS) |  |  |
| txs | [TransactionS](#gagarin.network.storage.TransactionS) | repeated |  |
| receipts | [Receipt](#gagarin.network.storage.Receipt) | repeated |  |






<a name="gagarin.network.storage.Entry"></a>

### Entry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [bytes](#bytes) |  |  |
| account | [bytes](#bytes) |  |  |






<a name="gagarin.network.storage.Peer"></a>

### Peer



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [bytes](#bytes) |  |  |
| publicKey | [bytes](#bytes) |  |  |
| addrInfo | [bytes](#bytes) |  |  |






<a name="gagarin.network.storage.QuorumCertificateS"></a>

### QuorumCertificateS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| header | [BlockHeaderS](#gagarin.network.storage.BlockHeaderS) |  |  |
| signatureAggregate | [SignatureAggregateS](#gagarin.network.storage.SignatureAggregateS) |  |  |






<a name="gagarin.network.storage.Receipt"></a>

### Receipt



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| txHash | [bytes](#bytes) |  |  |
| from | [bytes](#bytes) |  |  |
| to | [bytes](#bytes) |  |  |
| value | [int64](#int64) |  |  |
| toValue | [int64](#int64) |  |  |
| fromValue | [int64](#int64) |  |  |






<a name="gagarin.network.storage.Record"></a>

### Record



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| snap | [bytes](#bytes) |  |  |
| parent | [bytes](#bytes) |  |  |
| siblings | [bytes](#bytes) | repeated |  |






<a name="gagarin.network.storage.SignatureAggregateS"></a>

### SignatureAggregateS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| bitmap | [bytes](#bytes) |  |  |
| signature | [bytes](#bytes) |  |  |






<a name="gagarin.network.storage.SignatureS"></a>

### SignatureS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| from | [bytes](#bytes) |  |  |
| signature | [bytes](#bytes) |  |  |






<a name="gagarin.network.storage.Snapshot"></a>

### Snapshot



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hash | [bytes](#bytes) |  |  |
| proposer | [bytes](#bytes) |  |  |
| entries | [Entry](#gagarin.network.storage.Entry) | repeated |  |






<a name="gagarin.network.storage.TransactionS"></a>

### TransactionS



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| type | [int32](#int32) |  |  |
| to | [bytes](#bytes) |  |  |
| from | [bytes](#bytes) |  |  |
| nonce | [uint64](#uint64) |  |  |
| value | [int64](#int64) |  |  |
| fee | [int64](#int64) |  |  |
| signature | [SignatureS](#gagarin.network.storage.SignatureS) |  |  |
| hash | [bytes](#bytes) |  |  |
| data | [bytes](#bytes) |  |  |





 

 

 

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

