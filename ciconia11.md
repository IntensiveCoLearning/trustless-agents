---
timezone: UTC+8
---

# LI

**GitHub ID:** ciconia11

**Telegram:** @ciconia

## Self-introduction

Backend and smart contract developers, full of learning enthusiasm

## Notes

<!-- Content_START -->
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
# **ERC-8004：**

## **Identity Registry：**

The Identity Registry uses ERC-721 with the URIStorage extension for agent registration, making **all agents immediately browsable and transferable with NFTs-compliant apps**. Each agent is uniquely identified globally by:

-   _namespace_
    
-   _chainId_
    
-   _identityRegistry_
    
-   _agentId_
    

## **Reputation Registry：**

### **Giving Feedback**

```
function giveFeedback(uint256 agentId, uint8 score, bytes32 tag1, bytes32 tag2, string calldata fileuri, bytes32 calldata filehash, bytes memory feedbackAuth) external

event NewFeedback(uint256 indexed agentId, address indexed clientAddress, uint8 score, bytes32 indexed tag1, bytes32 tag2, string fileuri, bytes32 filehash)
```

**Revoking Feedback**

```
function revokeFeedback(uint256 agentId, uint64 feedbackIndex) external

function appendResponse(uint256 agentId, address clientAddress, uint64 feedbackIndex, string calldata responseUri, bytes32 calldata responseHash) external

event ResponseAppended(uint256 indexed agentId, address indexed clientAddress, uint64 feedbackIndex, address indexed responder, string responseUri)
```

**Read Functions**

```
function getSummary(uint256 agentId, address[] calldata clientAddresses, bytes32 tag1, bytes32 tag2) external view returns (uint64 count, uint8 averageScore)
//agentId is the only mandatory parameter; others are optional filters.
//Without filtering by clientAddresses, results are subject to Sybil/spam attacks. See Security Considerations for details

function readFeedback(uint256 agentId, address clientAddress, uint64 index) external view returns (uint8 score, bytes32 tag1, bytes32 tag2, bool isRevoked)

function readAllFeedback(uint256 agentId, address[] calldata clientAddresses, bytes32 tag1, bytes32 tag2, bool includeRevoked) external view returns (address[] memory clientAddresses, uint8[] memory scores, bytes32[] memory tag1s, bytes32[] memory tag2s, bool[] memory revokedStatuses)
//agentId is the only mandatory parameter; others are optional filters. Revoked feedback are omitted.

function getResponseCount(uint256 agentId, address clientAddress, uint64 feedbackIndex, address[] responders) external view returns (uint64)
//agentId is the only mandatory parameter; others are optional filters.

function getClients(uint256 agentId) external view returns (address[] memory)

function getLastIndex(uint256 agentId, address clientAddress) external view returns (uint64)
```

**Off-Chain Feedback File Structure**

```
{
  //MUST FIELDS
  "agentRegistry": "eip155:1:{identityRegistry}",
  "agentId": 22,
  "clientAddress": "eip155:1:{clientAddress}",
  "createdAt": "2025-09-23T12:00:00Z",
  "feedbackAuth": "...",
  "score": 100,

  //MAY FIELDS
  "tag1": "foo",
  "tag2": "bar",
  "skill": "as-defined-by-A2A",
  "context": "as-defined-by-A2A",
  "task": "as-defined-by-A2A",
  "capability": "tools", // As per MCP: "prompts", "resources", "tools" or "completions"
  "name": "Put the name of the MCP tool you liked!", // As per MCP: the name of the prompt, resource or tool
  "proof_of_payment": {
	"fromAddress": "0x00...",
	"toAddress": "0x00...",
	"chainId": "1",
	"txHash": "0x00..." 
   }, // this can be used for x402 proof of payment
 
 // Other fields
  " ... ": { " ... " } // MAY
}
```

## **Validation Registry**

**This registry enables agents to request verification of their work and allows validator smart contracts to provide responses that can be tracked on-chain**

**Validation Request**

```
function validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external

event ValidationRequest(address indexed validatorAddress, uint256 indexed agentId, string requestUri, bytes32 indexed requestHash)
```

**Validation Response**

```
function validationResponse(bytes32 requestHash, uint8 response, string responseUri, bytes32 responseHash, bytes32 tag) external

event ValidationResponse(address indexed validatorAddress, uint256 indexed agentId, bytes32 indexed requestHash, uint8 response, string responseUri, bytes32 tag)
```

**Read Functions**

```
function getValidationStatus(bytes32 requestHash) external view returns (address validatorAddress, uint256 agentId, uint8 response, bytes32 tag, uint256 lastUpdate)

function getSummary(uint256 agentId, address[] calldata validatorAddresses, bytes32 tag) external view returns (uint64 count, uint8 avgResponse)
//Returns aggregated validation statistics for an agent. agentId is the only mandatory parameter; validatorAddresses and tag are optional filters

function getAgentValidations(uint256 agentId) external view returns (bytes32[] memory requestHashes)

function getValidatorRequests(address validatorAddress) external view returns (bytes32[] memory requestHashes)
```
<!-- DAILY_CHECKIN_2025-10-19_END -->
<!-- Content_END -->
