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
# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->
[https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098)

Some notes from forum, credits from their authors:

Reputons are a standard defined: [RFC 7071 - A Media Type for Reputation Interchange](https://datatracker.ietf.org/doc/html/rfc7071)

Creating a single (aggregate) reputation score is dangerous. ?

TODO validation logic is a bit complex

Could you please include a simple Solidity example (e.g., two agents ordering a pizza) showing how the ERC is used for escrowed payment? (for understandable historical reasons)?

we need to create an ETH denominated economy in the AI agents space, just like we did with NFTs. I believe the best way forward is to create capable AI agents, who will perform valuable tasks and have them demand payment in ETH.

**Single domain well known location:** I might want to host many agents at different URLs in the same domain. This would be possible in A2A, wouldn’t it? So my suggestion would be to use URLs rather than domains as the way to point to the agent.

The protocol doesn’t cover payments. We considered requiring payment proofs for giving feedback. We know some groups are working on an A2A payment extension for agents, based on x402. We like this approach and are connecting with them to ensure that their extension and ours (ERC-8004) work perfectly together.

But payment proofs should be referenceable in Reputation: what we can standardize is the hook: allow Feedback/Rating records to carry a lightweight reference to a payment proof so indexers can correlate economic activity with feedback.

How validation works in simple use case

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/brucexu-eth/images/2025-10-18-1760748356648-image.png)

Some ideas about validation:

-   Validation used for verify the agents have done something, esp to the external system
    
-   Validator might be provided by the service providers, or Independent, or others. But the validation will trust that validator's response
    
-   Other contracts like Escrow contracts relies on the validation to send tokens
    

TODO make a fake hotel booking demo with validation logic, and protect the privacy, remove the private hotel booking info.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->


Yesterday's recording has been uploaded.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->



## **Validation Registry1**

**This registry enables agents to request verification of their work and allows validator smart contracts to provide responses that can be tracked on-chain**.

After an agent finishes the task, they can call “validationRequest” on this contract. External “validator” can check whether the work was done correctly.

This function MUST be called by the owner or operator of _agentId_. TODO, multi-owners or company cases?

```
function validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external
```

TODO How does zkML proof, a TEE oracle, or a stake-secured re-execution network work for validation?

Validators -> validationResponse to give feedback and check result.

```
function validationResponse(bytes32 requestHash, uint8 response, string responseUri, bytes32 responseHash, bytes32 tag) external
```

TODO what is unit8 response used for? A: The _response_ is a value between 0 and 100, which can be used as binary (0 for failed, 100 for passed) or with intermediate values for validations with a spectrum of outcomes.

This function MUST be called by the _validatorAddress_ specified in the original request. TODO Service Agents specify the validatorAddress when request validation? How can they know which validator can help? If they specify one validator, is it trustless?

They both on-chain events. The entire audit trail—who asked for validation, who validated, when, and what the outcome was—lives on Ethereum (or the chosen L2).

That makes the result tamper-proof and composable: reputation systems, insurance funds, or downstream contracts can _trustlessly_ reference the validation outcome without needing an off-chain oracle.

The workflow might be:

1.  Server agent finishes a translation task -> validationRequest()
    
2.  Validator contract re-executes the model with the given inputs and checks a zk proof?? -> validationResponse()
    
3.  Client agent (or any dApp) reads the registry and releases payment only if passed == true.
    

TODO Validator need to re-executes the model, cost twice tokens. And the model might return differently, how to generate or check the zk proof and give a passed signal?

## **Rationale**

-   Agent communication protocols: AI primitives (MCP, A2A) and Web3 primitives such as wallet addresses, DIDs, and ENS names.
    
-   Feedback
    
-   **Gas Sponsorship**: Since clients don’t need to be registered anymore, any application can implement frictionless feedback leveraging [EIP-7702](https://eips.ethereum.org/EIPS/eip-7702). TODO build a demo that use 7702 to sponsor the gas for agent?
    
-   **Deployment**: We expect the registries to be deployed with singletons per chain. **Note that an agent registered and receiving feedback on chain A can still operate and transact on other chains.** Agents can also be registered on multiple chains if desired. TODO interop or cross chain deployment issue. How to archive “an agent registered and receiving feedback on chain A can still operate and transact on other chains?”
    

## Questions:

-   Privacy? if the agent will ask validator to verify their work?
    
-   How to build a validator?
    
-   Because agent uri and the service behind it might change, how can we make sure they are trustless always? What if they got hacked and replaced?
<!-- DAILY_CHECKIN_2025-10-16_END -->

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
