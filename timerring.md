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
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
## Core Purpose and Solution

The main challenge A2A addresses is the **interoperability challenge** where agents, built using diverse frameworks and by different vendors, are unable to work together because each has its own bespoke development and deployment.

-   **What it is:** A common language and standardized methods/data structures for agents to communicate with one another, regardless of their underlying implementation.
    
-   **What it solves:** It allows autonomous agents from different organizations to **unite and work together** (e.g., orchestrating specialized agents like a Flight, Hotel, and Currency agent to fulfill a user's complex request for planning an international trip).
    
-   **Key Benefits:** Includes **secure collaboration**, true **interoperability** (breaking down silos), **agent autonomy**, and **reduced integration complexity**.
    

* * *

## How it Fits in the Agent Stack

A2A is situated within a broader agent stack alongside other components:

-   **A2A:** Standardizes **communication among agents** deployed in different organizations.
    
-   **MCP (Model Context Protocol):** Focused on connecting **models to data and external resources** (tools). A2A is positioned to complement MCP by allowing agents to collaborate in their native modalities rather than being constrained to tool-like interactions.
    
-   **Frameworks (like ADK):** Provide toolkits for **constructing agents**. A2A is framework-agnostic.
    
-   **Models:** The fundamental reasoning component (e.g., Large Language Models).
    

* * *

## Design Principles

The protocol is built on principles that prioritize broad adoption and enterprise needs:

-   **Simplicity:** Leverages existing standards like **HTTP, JSON-RPC, and Server-Sent Events (SSE)**.
    
-   **Enterprise Readiness:** Aligns with standard web practices for authentication, security, and monitoring.
    
-   **Asynchronous:** Natively supports **long-running operations (LRO)** and streaming.
    
-   **Opaque Execution:** Agents collaborate without exposing their internal logic or proprietary tools, which **preserves intellectual property** and enhances security.
    

Do you want to know more about a specific topic, like the **A2A Request Lifecycle** or the distinction between **A2A and MCP**?
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->

Based on the web page content, here is a detailed explanation of the **Agent2Agent (A2A) Protocol** using Markdown:

# Agent2Agent (A2A) Protocol

The **A2A Protocol** is an open standard designed to enable seamless communication and collaboration between $\\text{AI}$ agents. It was developed by Google and then donated to the [Linux Foundation](https://a2a-protocol.org/latest/).

## What it does

In a world where AI agents are built using diverse frameworks and by different vendors, A2A provides a **common language** to break down silos and foster **interoperability**.

It allows agents (remote, local, and human) to communicate, regardless of the framework they are built with (such as [ADK](https://google.github.io/adk-docs/)) or the tools they are equipped with (such as [MCP](https://modelcontextprotocol.io/)).

## Why use the A2A Protocol?

The key benefits of using the protocol include:

-   **Interoperability:** It connects agents built on different platforms (like $\\text{LangGraph}$, $\\text{CrewAI}$, $\\text{Semantic Kernel}$, or custom solutions) to create powerful, composite $\\text{AI}$ systems.
    
-   **Complex Workflows:** Agents can delegate sub-tasks, exchange information, and coordinate actions to solve complex problems that a single agent cannot.
    
-   **Secure & Opaque:** Agents interact without needing to share internal memory, tools, or proprietary logic, ensuring security and preserving intellectual property.
    

## A2A and Model Context Protocol (MCP)

A2A and Model Context Protocol (MCP) are **complementary standards**:

-   **Model Context Protocol (MCP)** provides **agent-to-tool communication**. It standardizes how an agent connects to its tools, $\\text{APIs}$, and resources to get information.
    
-   **A2A** provides **agent-to-agent communication**. It acts as a universal, decentralized standard—the "public internet"—that allows $\\text{AI}$ agents (including those using $\\text{MCP}$) to interoperate, collaborate, and share their findings.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->


This is the sequences diagram that I summarize from the official erc 8004 examples:

```
sequenceDiagram
    participant User as User/Client
    participant Alice as Server Agent<br/>(Alice - local)
    participant Bob as Validator Agent<br/>(Bob - local)
    participant Charlie as Client Agent<br/>(Charlie - local)
    participant IR as IdentityRegistry<br/>(on-chain contract)
    participant RR as ReputationRegistry<br/>(on-chain contract)
    participant VR as ValidationRegistry<br/>(on-chain contract)
    participant Storage as Local Storage<br/>(data/, validations/)
    
    Note over User,Storage: Step 1: Deploy contracts
    User->>IR: Deploy IdentityRegistry
    User->>RR: Deploy ReputationRegistry
    User->>VR: Deploy ValidationRegistry
    
    Note over User,Storage: Steps 2-3: Agent registration
    Alice->>IR: newAgent("alice.example.com", 0xAAA)
    IR-->>Alice: agentId = 1
    IR->>IR: emit AgentRegistered(1)
    
    Bob->>IR: newAgent("bob.example.com", 0xBBB)
    IR-->>Bob: agentId = 2
    IR->>IR: emit AgentRegistered(2)
    
    Charlie->>IR: newAgent("charlie.example.com", 0xCCC)
    IR-->>Charlie: agentId = 3
    IR->>IR: emit AgentRegistered(3)
    
    Note over User,Storage: Step 4: Market analysis workflow
    Alice->>Alice: analyze_market()<br/>CrewAI multi-agent workflow
    Alice->>Alice: Senior Market Analyst<br/>Analyze BTC trend
    Alice->>Alice: Risk Assessment Reviewer<br/>Assess risks
    Alice->>Storage: Write analysis result<br/>data/btc_analysis.json
    
    Note over User,Storage: Step 5: Request validation
    Alice->>VR: validationRequest(<br/>validatorId=2,<br/>serverId=1,<br/>dataHash)
    VR->>VR: Record validation request
    VR->>VR: emit ValidationRequestEvent(2, 1, dataHash)
    
    Note over User,Storage: Step 6: AI-driven validation
    Bob->>VR: Read validation request
    Bob->>Storage: Read analysis file<br/>data/btc_analysis.json
    Bob->>Bob: validate_analysis()<br/>CrewAI validation workflow
    Bob->>Bob: Senior Validator<br/>Review methodology
    Bob->>Bob: QA Specialist<br/>Final assessment
    Bob->>Storage: Write validation result<br/>validations/validation_result.json
    
    Note over User,Storage: Step 7: Submit validation response
    Bob->>VR: validationResponse(<br/>dataHash,<br/>score=96)
    VR->>VR: Record validation score
    VR->>VR: emit ValidationResponseEvent(2, 1, dataHash, 96)
    
    Note over User,Storage: Step 8: Feedback authorization
    Charlie->>RR: acceptFeedback(<br/>clientId=3,<br/>serverId=1)
    RR->>RR: Record authorization relation
    RR->>RR: emit AuthFeedback(3, 1, feedbackAuthId)
    
    Note over User,Storage: Step 9: Audit trail
    User->>IR: getAgent(1, 2, 3)
    IR-->>User: Return agent info
    User->>VR: getValidationResponse(dataHash)
    VR-->>User: Return validation score 96
    User->>RR: isFeedbackAuthorized(3, 1)
    RR-->>User: Return authorization status
```
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->



The ERC-8004 is not reinvent the wheel. The protocol not only expands A2A, but also bases trust assumptions on what builders are already thinking about. So, Stake-secured validation? Use \[EigenLayer\](https://blog.eigencloud.xyz/introducing-verifiable-agents-on-eigenlayer/). TEE attestations? Check out \[Phala\](https://phala.com/) its \[paper\](https://arxiv.org/pdf/2409.03992) and \[Near.AI\](https://near.ai/).

And there are already some [DeAI](https://deai.directory/) .
<!-- DAILY_CHECKIN_2025-10-16_END -->

<!-- DAILY_CHECKIN_2025-10-15_START -->

<!-- DAILY_CHECKIN_2025-10-15_START -->
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
