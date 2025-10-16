---
timezone: UTC+8
---

# timerring

**GitHub ID:** timerring

**Telegram:** @timerring

## Self-introduction

Keep Buidler

## Notes
<!-- Content_START -->
# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->


# 2025.10.16
<!-- DAILY_CHECKIN_2025-10-16_START -->
The ERC-8004 is not reinvent the wheel. The protocol not only expands A2A, but also bases trust assumptions on what builders are already thinking about. So, Stake-secured validation? Use \[EigenLayer\](https://blog.eigencloud.xyz/introducing-verifiable-agents-on-eigenlayer/). TEE attestations? Check out \[Phala\](https://phala.com/) its \[paper\](https://arxiv.org/pdf/2409.03992) and \[Near.AI\](https://near.ai/).

And there are already some [DeAI](https://deai.directory/) .
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
## ERC-8004: Trustless Agents Notes

### I. Core Objective and Motivation

-   **Goal:** To enable **discovery, selection, and interaction with agents across organizational boundaries without pre-existing trust**, thereby fostering an **open-ended agent economy** utilizing blockchain infrastructure.
    
-   **Problem Solved:** Existing agent communication protocols (like A2A and MCP) lack native **agent discovery** and **trust establishment** mechanisms.
    
-   **Trust Model:** It employs a **pluggable and tiered** trust model, where security is proportional to the value at risk (Reputation → Cryptoeconomic Verification/TEE).
    

### II. Three Core Registries (Lightweight Registries)

ERC-8004 defines three minimal on-chain registries to achieve its trust layer:

1\. Identity Registry

-   **Basis:** Built on [**ERC-721**](https://eips.ethereum.org/EIPS/eip-8004#identity-registry) (with `URIStorage` extension), making Agents portable, censorship-resistant NFT assets.
    
-   **Unique ID:** An Agent's identity is uniquely defined by `eip155:chainId:identityRegistry:agentId`.
    
-   **Core Data:** The `tokenURI` must resolve to an **Agent Registration File** (JSON metadata).
    

**Agent Registration File Example (Key Structure)**

```
{
  // Mandatory fields for ERC-721 compatibility and Agent description
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "myAgentName",
  "description": "A natural language description of the Agent, its function, pricing, etc.",
  "image": "https://example.com/agentimage.png",
  
  // Endpoints for communication and interaction
  "endpoints": [
    { "name": "A2A", "endpoint": "..." }, // Agent-to-Agent communication protocol endpoint
    { "name": "MCP", "endpoint": "..." }, // Model-Capability-Prompt protocol endpoint
    { "name": "DID", "endpoint": "did:method:foobar", "version": "v1" },
    { "name": "agentWallet", "endpoint": "eip155:1:0x..." } // Wallet address for transactions or verification
  ],
  
  // Trust mechanisms supported or required by the Agent
  "supportedTrust": [
    "reputation",         // Supports reputation system based on client feedback
    "crypto-economic",    // Supports cryptoeconomic verification (e.g., stake-secured re-execution)
    "tee-attestation"     // Supports Trusted Execution Environment proofs
  ]
}
```

**Key Registration Code**

```
// Function to register a new Agent, returning its unique agentId
function register(string tokenURI, MetadataEntry[] calldata metadata) returns (uint256 agentId) 
// Registration Event
event Registered (
    uint256 indexed agentId, 
    string tokenURI, 
    address indexed owner
)
```

2\. Reputation Registry

-   **Purpose:** To collect and share client feedback signals for Agent performance.
    
-   **Data:** Score (0-100), optional tags (`tag1`, `tag2`), and a URI pointing to off-chain data/comment.
    
-   **Mechanism:** Agents are expected to issue a signed `feedbackAuth` to allow clients to post feedback.
    

**Core Code**

```
// Client submits feedback
function giveFeedback (
    uint256 agentId, 
    uint8 score,         // Score (0-100), mandatory field
    bytes32 tag1,        // Optional tag 1
    bytes32 tag2,        // Optional tag 2
    string calldata fileuri, 
    bytes32 calldata filehash, 
    bytes memory feedbackAuth // Signature authorizing the feedback submission
) external

// Aggregated read function (actual aggregation is often done off-chain)
function getSummary (
    uint256 agentId, 
    address [] calldata clientAddresses, // Optional: Filter by reviewer (for Sybil mitigation)
    bytes32 tag1, 
    bytes32 tag2
) external view returns (uint64 count, uint8 averageScore)
```

3\. Validation Registry

-   **Purpose:** To allow Agents to **request** independent verification of their work, and for **Validators** to submit verifiable responses.
    
-   **Verification Types:** Supports cryptoeconomic staking, zkML proofs, or TEE oracles.
    

**Core Code**

```
// Agent requests verification
function validationRequest (
    address validatorAddress,  // The specific Validator to be engaged
    uint256 agentId, 
    string requestUri,         // URI pointing to the data required for validation
    bytes32 requestHash        // Commitment/hash of the request data
) external

// Validator responds
function validationResponse (
    bytes32 requestHash,  // Must match the hash of the original request
    uint8 response,       // Validation result (0-100, e.g., 0=Fail, 100=Pass)
    string responseUri,   // Optional: URI pointing to validation evidence or audit report
    bytes32 responseHash, 
    bytes32 tag           // Optional: Tag for specific validation status
) external

// Read the validation status
function getValidationStatus (
    bytes32 requestHash
) external view returns (
    address validatorAddress, 
    uint256 agentId, 
    uint8 response, 
    bytes32 tag, 
    uint256 lastUpdate
)
```

### III. Security Considerations

-   **Sybil Attacks:** The Reputation system is susceptible to Sybil attacks. The protocol addresses this by making all signals **public** and allowing filtering based on the reporter's address, encouraging the development of external **reviewer reputation systems**.
    
-   **Capability Guarantee:** ERC-8004 guarantees the integrity of the Agent's identity and registration file, but it **does not** guarantee that the advertised capability is **functional or non-malicious**. This relies on the **tiered trust models** (reputation, validation, TEE attestation) for verification.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## ERC-8004: Trustless Agents Notes

### I. Core Objective and Motivation

-   **Goal:** To enable **discovery, selection, and interaction with agents across organizational boundaries without pre-existing trust**, thereby fostering an **open-ended agent economy** utilizing blockchain infrastructure.
    
-   **Problem Solved:** Existing agent communication protocols (like A2A and MCP) lack native **agent discovery** and **trust establishment** mechanisms.
    
-   **Trust Model:** It employs a **pluggable and tiered** trust model, where security is proportional to the value at risk (Reputation → Cryptoeconomic Verification/TEE).
    

### II. Three Core Registries (Lightweight Registries)

ERC-8004 defines three minimal on-chain registries to achieve its trust layer:

1\. Identity Registry

-   **Basis:** Built on [**ERC-721**](https://eips.ethereum.org/EIPS/eip-8004#identity-registry) (with `URIStorage` extension), making Agents portable, censorship-resistant NFT assets.
    
-   **Unique ID:** An Agent's identity is uniquely defined by `eip155:chainId:identityRegistry:agentId`.
    
-   **Core Data:** The `tokenURI` must resolve to an **Agent Registration File** (JSON metadata).
    

**Agent Registration File Example (Key Structure)**

```
{
  // Mandatory fields for ERC-721 compatibility and Agent description
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "myAgentName",
  "description": "A natural language description of the Agent, its function, pricing, etc.",
  "image": "https://example.com/agentimage.png",
  
  // Endpoints for communication and interaction
  "endpoints": [
    { "name": "A2A", "endpoint": "..." }, // Agent-to-Agent communication protocol endpoint
    { "name": "MCP", "endpoint": "..." }, // Model-Capability-Prompt protocol endpoint
    { "name": "DID", "endpoint": "did:method:foobar", "version": "v1" },
    { "name": "agentWallet", "endpoint": "eip155:1:0x..." } // Wallet address for transactions or verification
  ],
  
  // Trust mechanisms supported or required by the Agent
  "supportedTrust": [
    "reputation",         // Supports reputation system based on client feedback
    "crypto-economic",    // Supports cryptoeconomic verification (e.g., stake-secured re-execution)
    "tee-attestation"     // Supports Trusted Execution Environment proofs
  ]
}
```

**Key Registration Code**

```
// Function to register a new Agent, returning its unique agentId
function register(string tokenURI, MetadataEntry[] calldata metadata) returns (uint256 agentId) 
// Registration Event
event Registered (
    uint256 indexed agentId, 
    string tokenURI, 
    address indexed owner
)
```

2\. Reputation Registry

-   **Purpose:** To collect and share client feedback signals for Agent performance.
    
-   **Data:** Score (0-100), optional tags (`tag1`, `tag2`), and a URI pointing to off-chain data/comment.
    
-   **Mechanism:** Agents are expected to issue a signed `feedbackAuth` to allow clients to post feedback.
    

**Core Code**

```
// Client submits feedback
function giveFeedback (
    uint256 agentId, 
    uint8 score,         // Score (0-100), mandatory field
    bytes32 tag1,        // Optional tag 1
    bytes32 tag2,        // Optional tag 2
    string calldata fileuri, 
    bytes32 calldata filehash, 
    bytes memory feedbackAuth // Signature authorizing the feedback submission
) external

// Aggregated read function (actual aggregation is often done off-chain)
function getSummary (
    uint256 agentId, 
    address [] calldata clientAddresses, // Optional: Filter by reviewer (for Sybil mitigation)
    bytes32 tag1, 
    bytes32 tag2
) external view returns (uint64 count, uint8 averageScore)
```

3\. Validation Registry

-   **Purpose:** To allow Agents to **request** independent verification of their work, and for **Validators** to submit verifiable responses.
    
-   **Verification Types:** Supports cryptoeconomic staking, zkML proofs, or TEE oracles.
    

**Core Code**

```
// Agent requests verification
function validationRequest (
    address validatorAddress,  // The specific Validator to be engaged
    uint256 agentId, 
    string requestUri,         // URI pointing to the data required for validation
    bytes32 requestHash        // Commitment/hash of the request data
) external

// Validator responds
function validationResponse (
    bytes32 requestHash,  // Must match the hash of the original request
    uint8 response,       // Validation result (0-100, e.g., 0=Fail, 100=Pass)
    string responseUri,   // Optional: URI pointing to validation evidence or audit report
    bytes32 responseHash, 
    bytes32 tag           // Optional: Tag for specific validation status
) external

// Read the validation status
function getValidationStatus (
    bytes32 requestHash
) external view returns (
    address validatorAddress, 
    uint256 agentId, 
    uint8 response, 
    bytes32 tag, 
    uint256 lastUpdate
)
```

### III. Security Considerations

-   **Sybil Attacks:** The Reputation system is susceptible to Sybil attacks. The protocol addresses this by making all signals **public** and allowing filtering based on the reporter's address, encouraging the development of external **reviewer reputation systems**.
    
-   **Capability Guarantee:** ERC-8004 guarantees the integrity of the Agent's identity and registration file, but it **does not** guarantee that the advertised capability is **functional or non-malicious**. This relies on the **tiered trust models** (reputation, validation, TEE attestation) for verification.
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
