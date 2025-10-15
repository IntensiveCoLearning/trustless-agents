---
timezone: UTC+13
---

# Bruce Xu

**GitHub ID:** brucexu-eth

**Telegram:** @brucexu_eth

## Self-introduction

All in ETH x AI. Exploring the real world use cases on this direction.

## Notes
<!-- Content_START -->
# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->
First day has started!

Use case: discover, choose, and interact with agents. Break the organizational boundaries; Enabling open-ended agent economies.

Three trust models:

-   Reputation systems using client feedback
    
-   Validation via stake-secured re-rexecution
    
-   zkML proofs or TEE oracles
    

The agent communication in A2A lack of agent discovery and trust across organizations. For example, if agents registered in Google, it will be hard to discover and use in Microsoft. And also, different companies might worry about the agents from their competitors. Therefore, Ethereum is the best platform to store the information for agents, so that it can be discovered by all ecosystem.

ERC-8004 provides three lightweight registries which can be deployed on any L2 or on Mainnet as per-chain singletons:

-   Identity Registry: ERC-721 + URIStorage -> agent's registration file (AgentCard)
    
-   Reputation Registry: Posting and fetching feedback signals. Scoring and aggregation occur both on-chain and off-chain.
    
-   Validation Registry: Generic hooks for requesting and recording independent validators checks (e.g. stakers re-running the job, zkML verifiers, TEE oracles, trusted judges). TODO use cases?
    

### Identity Registry

-   Each agent is an ERC-721 with URIStorage extension
    
-   Each agent is uniquely identified globally by:
    
    -   _namespace:_ `eip155` for EVM chains
        
    -   _chainId_: The blockchain network identifier
        
    -   _identityRegistry_: The address where the ERC-721 registry contract is deployed
        
    -   _agentId_: The ERC-721 tokenId assigned incrementally by the registry
        
-   The owner of the ERC-721 token is the owner of the agent and can transfer ownership or delegate management (e.g., updating the registration file) to operators, as supported by `ERC721URIStorage`.
    
-   The **_tokenURI_** MUST resolve to the agent registration file
    
-   registration file includes:
    
    -   basic info
        
    -   endpoints: different types of endpoint (name, endpoint, capabilities, version), point to an A2A agent card, and MCP endpoint, DID, etc.
        
    -   registrations: agentId and Registry (eip155:1:{identityRegistry})
        
    -   supportedTrust: reputation, tee-attestation, crypto-economic, etc. is Optional. ERC is used only for discovery, not for trust.
        

Registry extends getMetadata(uint256 agentId, string key) and setMetadata(uint256 agentId, string key, bytes value) functions for optional extra on-chain agent metadata.

### Registration

```
function register(string tokenURI, MetadataEntry[] calldata metadata) returns (uint256 agentId)
```


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
First day has started!

Use case: discover, choose, and interact with agents. Break the organizational boundaries; Enabling open-ended agent economies.

Three trust models:

-   Reputation systems using client feedback
    
-   Validation via stake-secured re-rexecution
    
-   zkML proofs or TEE oracles
    

The agent communication in A2A lack of agent discovery and trust across organizations. For example, if agents registered in Google, it will be hard to discover and use in Microsoft. And also, different companies might worry about the agents from their competitors. Therefore, Ethereum is the best platform to store the information for agents, so that it can be discovered by all ecosystem.

ERC-8004 provides three lightweight registries which can be deployed on any L2 or on Mainnet as per-chain singletons:

-   Identity Registry: ERC-721 + URIStorage -> agent's registration file (AgentCard)
    
-   Reputation Registry: Posting and fetching feedback signals. Scoring and aggregation occur both on-chain and off-chain.
    
-   Validation Registry: Generic hooks for requesting and recording independent validators checks (e.g. stakers re-running the job, zkML verifiers, TEE oracles, trusted judges). TODO use cases?
    

### Identity Registry

-   Each agent is an ERC-721 with URIStorage extension
    
-   Each agent is uniquely identified globally by:
    
    -   _namespace:_ `eip155` for EVM chains
        
    -   _chainId_: The blockchain network identifier
        
    -   _identityRegistry_: The address where the ERC-721 registry contract is deployed
        
    -   _agentId_: The ERC-721 tokenId assigned incrementally by the registry
        
-   The owner of the ERC-721 token is the owner of the agent and can transfer ownership or delegate management (e.g., updating the registration file) to operators, as supported by `ERC721URIStorage`.
    
-   The **_tokenURI_** MUST resolve to the agent registration file
    
-   registration file includes:
    
    -   basic info
        
    -   endpoints: different types of endpoint (name, endpoint, capabilities, version), point to an A2A agent card, and MCP endpoint, DID, etc.
        
    -   registrations: agentId and Registry (eip155:1:{identityRegistry})
        
    -   supportedTrust: reputation, tee-attestation, crypto-economic, etc. is Optional. ERC is used only for discovery, not for trust.
        

Registry extends getMetadata(uint256 agentId, string key) and setMetadata(uint256 agentId, string key, bytes value) functions for optional extra on-chain agent metadata.

### Registration

```
function register(string tokenURI, MetadataEntry[] calldata metadata) returns (uint256 agentId)
```

## Reputation Registry

**As an agent accepts a task, it’s expected to sign a _feedbackAuth_ to authorize the _clientAddress_ (human or agent) to give feedback**. The feedback consists of a _score_ (0-100), _tag1_ and _tag2_ (left to developers’ discretion to provide maximum on-chain composability and filtering), a file uri pointing to an off-chain JSON containing additional information, and its KECCAK-256 file hash to guarantee integrity. We suggest using IPFS or equivalent services to make feedback easily indexed by subgraphs or similar technologies. For IPFS uris, the hash is not required.

-   How to sign a feedbackAuth? What's the workflow?
    
-   How does clientAddress give feedback?
    
-   How does KECCAK-256 file hash to guarantee integrity? By signing a signature?
    

```
function giveFeedback(uint256 agentId, uint8 score, bytes32 tag1, bytes32 tag2, string calldata fileuri, bytes32 calldata filehash, bytes memory feedbackAuth) external
```

The _score_ MUST be between 0 and 100. _tag1_, _tag2_, and _uri_ are OPTIONAL.

_feedbackAuth_ is a tuple with the structure (_agentId_, _clientAddress_, _indexLimit_, _expiry_, _chainId_, _identityRegistry_, _signerAddress_) signed using [EIP-191](https://eips.ethereum.org/EIPS/eip-191) or [ERC-1271](https://eips.ethereum.org/EIPS/eip-1271) (if _clientAddress_ is a smart contract).

> seems agent owner will provide a feedbackAuth tuple to clientAddress, after they invoked the agent, they can give feedback with that tuple.

The _signerAddress_ field identifies the agent owner or operator who signed.  
Verification succeeds only if: _agentId_, _clientAddress_, _chainId_ and _identityRegistry_ are correct, blocktime < _expiry_ and _indexLimit_ is greater than the last index of feedback received by that client for that _agentId_.

While in most cases _indexLimit_ is simply lastIndex + 1, it can be much higher. This allows _agentId_ to pre-authorize multiple feedback submissions, useful for agent watch tower use cases. TODO go check logic in smart contract.

> An agent watchtower is an off-chain service that continuously evaluates an agent and posts pre-authorized feedback entries on-chain without a new signature each time.
> 
> `lastIndex[agentId][clientAddress] < indexLimit`. Then it increments `lastIndex` and records the feedback.
> 
> Practically `indexLimit` caps how many feedbacks that `clientAddress` can submit under one authorization.
> 
> Example: 5-min pings for 7 days → 2016; set ~2100 and renew weekly.

_clientAddress_ can revoke feedback by calling:

```
function revokeFeedback(uint256 agentId, uint64 feedbackIndex) external
```

```
function readFeedback(uint256 agentId, address clientAddress, uint64 index) external view returns (uint8 score, bytes32 tag1, bytes32 tag2, bool isRevoked)
```

### off-chain feedback file structure

-   proof\_of\_payment? TODO this can be used for x402 proof of payment, how?
    

## **Validation Registry**

**This registry enables agents to request verification of their work and allows validator smart contracts to provide responses that can be tracked on-chain**. Validator smart contracts could use, for example, stake-secured inference re-execution, zkML verifiers or TEE oracles to validate or reject requests.

TODO, how does validation work?

**Validation Request**

Agents request validation by calling:

```
function validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external
```

This function MUST be called by the owner or operator of _agentId_.

TODO ---

## Questions

-   How does zkML proofs and TEE oracles work?
    
-   How does agent authentication works in A2A?
    
-   Code and address of deployed ERC-8004 singletons?
    
-   Where to store the reputation data? On-chain? Too expensive? But it can against spam.
    
-   TODO build the demo with AA accounts.
    
-   How to implement admin of an agent, if owner of agent is the NFT owner. We might have multiple admins for managing one agent. And we need to think about the use case in a company.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## Reputation Registry

**As an agent accepts a task, it’s expected to sign a _feedbackAuth_ to authorize the _clientAddress_ (human or agent) to give feedback**. The feedback consists of a _score_ (0-100), _tag1_ and _tag2_ (left to developers’ discretion to provide maximum on-chain composability and filtering), a file uri pointing to an off-chain JSON containing additional information, and its KECCAK-256 file hash to guarantee integrity. We suggest using IPFS or equivalent services to make feedback easily indexed by subgraphs or similar technologies. For IPFS uris, the hash is not required.

-   How to sign a feedbackAuth? What's the workflow?
    
-   How does clientAddress give feedback?
    
-   How does KECCAK-256 file hash to guarantee integrity? By signing a signature?
    

```
function giveFeedback(uint256 agentId, uint8 score, bytes32 tag1, bytes32 tag2, string calldata fileuri, bytes32 calldata filehash, bytes memory feedbackAuth) external
```

The _score_ MUST be between 0 and 100. _tag1_, _tag2_, and _uri_ are OPTIONAL.

_feedbackAuth_ is a tuple with the structure (_agentId_, _clientAddress_, _indexLimit_, _expiry_, _chainId_, _identityRegistry_, _signerAddress_) signed using [EIP-191](https://eips.ethereum.org/EIPS/eip-191) or [ERC-1271](https://eips.ethereum.org/EIPS/eip-1271) (if _clientAddress_ is a smart contract).

> seems agent owner will provide a feedbackAuth tuple to clientAddress, after they invoked the agent, they can give feedback with that tuple.

The _signerAddress_ field identifies the agent owner or operator who signed.  
Verification succeeds only if: _agentId_, _clientAddress_, _chainId_ and _identityRegistry_ are correct, blocktime < _expiry_ and _indexLimit_ is greater than the last index of feedback received by that client for that _agentId_.

While in most cases _indexLimit_ is simply lastIndex + 1, it can be much higher. This allows _agentId_ to pre-authorize multiple feedback submissions, useful for agent watch tower use cases. TODO go check logic in smart contract.

> An agent watchtower is an off-chain service that continuously evaluates an agent and posts pre-authorized feedback entries on-chain without a new signature each time.
> 
> `lastIndex[agentId][clientAddress] < indexLimit`. Then it increments `lastIndex` and records the feedback.
> 
> Practically `indexLimit` caps how many feedbacks that `clientAddress` can submit under one authorization.
> 
> Example: 5-min pings for 7 days → 2016; set ~2100 and renew weekly.

_clientAddress_ can revoke feedback by calling:

```
function revokeFeedback(uint256 agentId, uint64 feedbackIndex) external
```

```
function readFeedback(uint256 agentId, address clientAddress, uint64 index) external view returns (uint8 score, bytes32 tag1, bytes32 tag2, bool isRevoked)
```

### off-chain feedback file structure

-   proof\_of\_payment? TODO this can be used for x402 proof of payment, how?
    

## **Validation Registry**

**This registry enables agents to request verification of their work and allows validator smart contracts to provide responses that can be tracked on-chain**. Validator smart contracts could use, for example, stake-secured inference re-execution, zkML verifiers or TEE oracles to validate or reject requests.

TODO, how does validation work?

**Validation Request**

Agents request validation by calling:

```
function validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external
```

This function MUST be called by the owner or operator of _agentId_.

TODO ---

## Questions

-   How does zkML proofs and TEE oracles work?
    
-   How does agent authentication works in A2A?
    
-   Code and address of deployed ERC-8004 singletons?
    
-   Where to store the reputation data? On-chain? Too expensive? But it can against spam.
    
-   TODO build the demo with AA accounts.
    
-   How to implement admin of an agent, if owner of agent is the NFT owner. We might have multiple admins for managing one agent. And we need to think about the use case in a company.
<!-- DAILY_CHECKIN_2025-10-15_END -->

# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
First day has started!
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
