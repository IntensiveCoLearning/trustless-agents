---
timezone: UTC+8
---

# SunSec

**GitHub ID:** SunWeb3Sec

**Telegram:** @huangSun

## Self-introduction

最近都在研究AI Payment and AI Security, 藉由此活動希望認識更多志同道合的朋友:D

## Notes
<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
# Identity Registry Learning Notes

## Today’s Goals

-   Understand the design principle of **“on-chain minimalism, off-chain richness.”**
    
-   Learn how **ERC-721 +** `tokenURI` serves as an **identity anchor.**
    
-   Develop your project’s **ID naming strategy** (trade-offs among ENS / DID / URL / Domain).
    

## Key Concepts

-   **Minimize on-chain data:**  
    Only store verifiable pointers and ownership on-chain.  
    Keep all other capabilities, keys, endpoints, and payment options off-chain (in a JSON descriptor).
    
-   **Identity as NFT:**  
    Each `tokenId` = one agent identity.  
    `ownerOf(tokenId)` = controller of that identity.
    
-   `tokenURI` **as the source of truth:**  
    Points to an off-chain file (IPFS / Arweave / HTTPS).  
    May contain public keys, service capabilities, payment options, and cross-references (ENS / DID / URL / Domain).
    
-   **Versioning and rotation:**  
    Append `?v=date` or `#v=commit` for auditability.  
    Key rotation records are stored off-chain, while updates are announced via on-chain events.
    
-   **Portability and interoperability:**  
    Maintain at least one **Primary ID** and a **mapping table** to avoid vendor lock-in by any single naming system.
    

## Interface and Flow (Conceptual)

-   **Interface:**  
    `registerAgent(agent, uri) → tokenId`;  
    `tokenURI(tokenId)`;  
    `ownerOf(tokenId)`;  
    Events: `AgentRegistered`, `AgentURIUpdated`.
    
-   **Flow:**  
    Registration → Query `tokenURI` to retrieve the Agent Card → Emit update events for indexers upon data changes.
    

## Security and Governance Notes

-   **Ownership control:** Only `ownerOf(tokenId)` can update the `uri`.
    
-   **Availability:** Ensure long-term accessibility of the JSON (`IPFS + pin`, `Arweave`, or version-controlled HTTPS).
    
-   **Auditability:** JSON should include version, publish time, and previous hash; emit events to mark version updates.
    
-   **Compatibility:** Reserve ENS/DID fields and consider multi-chain mirror URIs.
    
-   **Privacy:** Only expose public keys/endpoints; keep sensitive keys or credentials hashed or signed, not in plaintext.
    

## Your Project’s “5-Line Naming Strategy” (Replace with your own)

1.  **Primary ID:** Choose one (ENS / DID / URL / Domain) as your main external identifier.
    
2.  **Mapping:** Maintain a mapping table and verification method (signature/TXT record) for 2–3 other identifiers in `descriptor.json`.
    
3.  **URI Policy:** `tokenURI` points to IPFS (primary) + HTTPS (backup), with versioned filenames (e.g., `card.v2025-10-15.json`).
    
4.  **Versioning Standard:** Each update must include `version`, `prev_hash`, and `changelog`, and emit `AgentURIUpdated` on-chain.
    
5.  **Key Rotation:** JSON maintains `keys[{kid, use, alg, jwk_fingerprint, valid_from, valid_to, rotate_sig}]`.
    

## Example: `descriptor.json` (Structure Sample — Customize as Needed)

```
{
  "id_primary": "ens:youragent.eth",
  "mappings": {
    "did": "did:pkh:eip155:1:0xYourAddr",
    "url": "https://agents.example.com/youragent",
    "domain": "youragent.example.com"
  },
  "version": "2025-10-15",
  "prev_hash": "0x...",
  "capabilities": ["translate.v1", "route.v1"],
  "endpoints": {
    "jsonrpc": "https://api.example.com/rpc"
  },
  "payments": {
    "eip3009": true,
    "x402": true
  },
  "keys": [
    {
      "kid": "2025-q4",
      "use": "sign",
      "alg": "secp256k1",
      "jwk_fingerprint": "sha256-...",
      "valid_from": "2025-10-01T00:00:00Z",
      "rotate_sig": "0xRotationSignature"
    }
  ]
}
```
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025.10.16
<!-- DAILY_CHECKIN_2025-10-16_START -->
## 10/16 Workshop Summary — ERC-8004

### 1\. Core Objective

-   **ERC-8004** addresses the challenge of **AI agent discovery and trust** in decentralized economies.
    
-   It introduces three foundational registries that allow agents to **register identity**, **receive feedback**, and **validate their work**.
    
-   The goal is to create a **neutral information layer** on which developers and ecosystems can build their own applications.
    

* * *

### 2\. Identity Registry

-   Implemented using **ERC-721 (NFT standard)** — each registered agent receives a unique **Token ID (Agent ID)**.
    
-   The on-chain record stores a **URI** pointing to an off-chain JSON (e.g., on IPFS) that contains:
    
    -   Agent name, description, image
        
    -   Communication endpoints (A2A Gateway, MCP endpoint, etc.)
        
    -   Wallet address and metadata
        
-   Supports mapping with **ENS / DID / Wallets**.
    
-   Owners can **transfer** agents and **delegate operators** for URI updates and maintenance.
    

* * *

### 3\. Reputation Registry

-   Works like a **decentralized feedback system**:
    
    -   Clients can score agents from **0–100**.
        
    -   Before submitting feedback, a client must obtain a **signed “Feedback Authorization”** from the agent to prevent spam.
        
    -   Supports **custom tags** and **off-chain files** for richer context (e.g., proof of service).
        
-   Clients **don’t need to register** to leave feedback — enabling **gas-sponsored user experiences**.
    
-   The community is encouraged to build **indexing layers** (e.g., **The Graph Subgraphs**) to aggregate and query reputation data efficiently.
    
-   Potential use cases include:
    
    -   Decentralized reputation systems
        
    -   Game-like trust and collaboration models among AI agents
        

* * *

### 4\. Validation Registry

-   Enables **provable trust mechanisms** beyond simple reputation.
    
-   **Workflow:**
    
    1.  Agent submits a **Validation Request** to a validator smart contract, with off-chain payload.
        
    2.  The validator responds with a **validation score (0–100)**.
        
-   Three supported models:
    
    1.  **Full On-Chain Verification:** Entire request + attestation stored and verified on-chain (gas-intensive).
        
    2.  **TEE Oracle Model:** A trusted TEE Oracle performs the attestation check off-chain and signs the result.
        
    3.  **Public Key Registry Model:** Only verifies TEE-generated public keys — the envisioned direction for scalable, trust-minimized validation.
        
-   Compatible with **Zero-Knowledge Proofs (ZKPs)**, **Trusted Execution Environments (TEEs)**, and **Stake-Secured Inference**.
    
-   Supports **privacy-preserving validation** depending on implementation.
    

* * *

### 5\. Technical Implementation

-   Smart contracts are **deployed on the Sepolia testnet** and **open-sourced on GitHub**.
    
-   Supports **ERC-1271 (smart-contract wallet signatures)**.
    
-   Enables **gas-less user experiences**.
    
-   Built with an **event-based architecture**, making it index-friendly for tools like **The Graph**.
    
-   **Community SDKs** are available for developers to interact directly with the registries.
    

* * *

### 6\. Deployment and Governance

-   The goal is to maintain **singleton registries per network**.
    
-   The **Ethereum Foundation** will coordinate deployments across **mainnet**, **Layer-2s**, and **other L1s**.
    
-   Initial deployments will use a **multi-sig distributed governance** model.
    
-   **No single entity** will control production keys.
    
-   Mainnet deployment expected around **late October**, pending community feedback.
    

* * *

### 7\. Privacy and Data Security

-   Several privacy-preserving methods are under discussion:
    
    -   **ZKML (Zero-Knowledge Machine Learning):** Reveals only input/output, hides internal data.
        
    -   **Stake-Secured Inference:** Public computations backed by staked collateral.
        
    -   **TEE-based validation:** Relies on hardware-based isolation for private computations.
        
-   Off-chain storage options include **IPFS**, **HTTPS**, and other content-addressable schemes.
    

* * *

### 8\. Community and Ecosystem

-   The ERC-8004 community now includes **~750 members** contributing SDKs and tools.
    
-   Developers are encouraged to test the **reference implementation on Sepolia** and provide feedback.
    
-   Collaborations are underway with projects like **File Network, AIGLayer, and ChaosChain** to advance **TEE and ZK standardization**.
    

* * *

## 🎯 Key Takeaways

-   **ERC-8004** lays the foundation for **AI agent interoperability, discovery, and verifiable trust** in decentralized networks.
    
-   By registering agents as NFTs and combining **feedback** with **provable validation**, it creates a trust layer for autonomous AI economies.
    
-   The standard is still **early-stage**, but it provides a clear blueprint for the next generation of **open, AI-driven Web3 ecosystems**.
    
-   Developers and researchers are encouraged to join the community, test the framework, and contribute to its evolution.
    

REF

8004 singletons are available on Testnet, so you can start building on it. Clap to Leonard @lentan & all the 8004 contributors for making this happen 🙏👏

Source code: [https://github.com/erc-8004/erc-8004-contracts](https://github.com/erc-8004/erc-8004-contracts)

Sepolia

-   Identity: [https://sepolia.etherscan.io/address/0x8004a6090Cd10A7288092483047B097295Fb8847](https://sepolia.etherscan.io/address/0x8004a6090Cd10A7288092483047B097295Fb8847)
    
-   Reputation: [https://sepolia.etherscan.io/address/0x8004B8FD1A363aa02fDC07635C0c5F94f6Af5B7E](https://sepolia.etherscan.io/address/0x8004B8FD1A363aa02fDC07635C0c5F94f6Af5B7E)
    
-   Validation: [https://sepolia.etherscan.io/address/0x8004CB39f29c09145F24Ad9dDe2A108C1A2cdfC5](https://sepolia.etherscan.io/address/0x8004CB39f29c09145F24Ad9dDe2A108C1A2cdfC5)
    

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SunWeb3Sec/images/2025-10-16-1760603077585-image.png)
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
ERC-8004 Overview & Trust Layer Primer

Objective (today)

\- Understand **what ERC-8004 is solving**, its **three registries** (Identity / Reputation / Validation), and the **“events-first”** design.

\---

Why ERC-8004 (problem framing)

Modern agents need to discover each other, establish minimal trust, and settle outcomes across org or platform boundaries. ERC-8004 proposes a **credibly neutral trust layer** on Ethereum so agents can be **discovered, chosen, verified, and audited** without pre-existing trust. It does this by standardizing on-chain registries while pushing complex scoring and analytics off-chain for flexibility.

ERC-8004 — Three Registries (Implementation-Oriented Explainer)

1.  **Identity Registry**
    

What (Purpose)  
Provide each agent with a portable, censorship-resistant on-chain identifier. Keep the on-chain footprint minimal (a pointer), and store rich metadata off-chain (Agent Card/descriptor, DID doc, JSON).

How (Data model)

-   ERC-721 + URIStorage: each tokenId = one agent identity
    
-   tokenURI(tokenId) points to a registration file describing capabilities, endpoints, public keys, payment options, etc.
    
-   Off-chain file may include mappings across identifiers (ENS/DID/URL/Domain). On-chain keeps only the primary URI.
    

Minimal Interface (example)  
interface IIdentityRegistry {  
event AgentRegistered(address agent, uint256 tokenId, string uri);  
event AgentURIUpdated(uint256 tokenId, string oldUri, string newUri);

```
function registerAgent(address agent, string calldata uri)
    external returns (uint256 tokenId);

function tokenURI(uint256 tokenId) external view returns (string memory);
function ownerOf(uint256 tokenId) external view returns (address);
}
```

Typical Flow

1.  Caller invokes registerAgent(agent, uri) → mints an ERC-721 as the identity anchor
    
2.  Anyone calls tokenURI(id) → fetches the off-chain Agent Card (descriptor/public keys/services)
    
3.  To update metadata, emit AgentURIUpdated so indexers can track versions
    

Design Notes

-   Primary ID + mapping table: choose ENS or DID as the primary; publish mappings to avoid lock-in
    
-   Versioning: append commit/version hints to the URI (e.g., …/card.json#v=2025-10-13) for auditability
    
-   Key rotation: keep rotation data/signatures in the off-chain file; restrict updates via ownerOf(tokenId)
    

* * *

2.  **Reputation Registry**
    

What (Purpose)  
Record interaction outcomes and quality signals as events (success/failure, latency percentiles, refund/dispute flags, settlement references). Avoid a single global score; enable a signal marketplace where third parties aggregate or weight differently.

How (Data model)

-   Prefer events as the canonical record of facts
    
-   Optionally expose a tiny set of view helpers (e.g., recent N entries) for convenience
    
-   Standardize event fields to make third-party indexing easy
    
-   Authorization flow: when the Server Agent accepts a task, it pre-authorizes the Client Agent to submit feedback after completion
    

```
Events & Interface (example)
interface IReputationRegistry {
event ReputationEvent(
bytes32 traceId,
address actor,
address counterparty,
string capability,
bool success,
uint64 latencyMsP95,
bytes32 paymentRef,
bytes32 integrityHash,
string evidenceURI
);
```

```
function emitReputation(
    bytes32 traceId,
    address actor,
    address counterparty,
    string calldata capability,
    bool success,
    uint64 latencyMsP95,
    bytes32 paymentRef,
    bytes32 integrityHash,
    string calldata evidenceURI
) external;

function getRecent(address agent, uint256 limit)
    external view returns (/* compact array type */);
}
```

Typical Flow

1.  After a call completes, your business/agent contract emits ReputationEvent
    
2.  Indexers pull events → warehouse (e.g., BigQuery/ClickHouse) → dashboards & KPIs
    
3.  External raters/auditors/insurers build scene-specific scores by weighting signals differently
    

Anti-abuse Tips

-   Sybil/self-dealing: perform graph analysis on counterparty; require validation evidence on a sample
    
-   Replay: enforce unique traceId/paymentRef; include nonce + deadline where applicable
    
-   Auditability: align integrityHash with (masked) input/output; host immutable evidenceURI (IPFS or versioned storage)
    

* * *

3.  **Validation Registry**
    

What (Purpose)  
Standardize independent verification: request checks by third parties (re-execution, ZK, TEE, human judges) and record results on-chain. Produce an auditable chain of evidence tied to a reputation record.

How (Data model)

-   Two-phase events: Request → Recorded Result
    
-   Identify method as an enum or string: "sampling" | "zk" | "tee" | "judge"
    

Interface (example)  
interface IValidationRegistry {  
enum Method { Sampling, ZK, TEE, Judge }

```
event ValidationRequested(
    bytes32 jobRef,
    address requestor,
    Method  method,
    string  evidenceURI
);

event ValidationRecorded(
    bytes32 jobRef,
    Method  method,
    bool    verdict,
    string  proofRef,
    bytes32 relatedHash
);

function requestValidation(
    bytes32 jobRef,
    Method method,
    string calldata evidenceURI
) external;

function recordValidation(
    bytes32 jobRef,
    Method method,
    bool verdict,
    string calldata proofRef,
    bytes32 relatedHash
) external;
}
```

Typical Flow

1.  Someone calls requestValidation(jobRef, method, evidenceURI) (buyer/auditor/policy bot)
    
2.  Validator runs off-chain (re-executes, builds ZK proof, produces TEE attestation, or renders judgment)
    
3.  Validator (or an authorized recorder) calls recordValidation → on-chain verdict/proofRef cross-linked via relatedHash
    

Security/Governance

-   Who can record? Whitelisted validators or staked sets subject to slashing
    
-   Evidence availability: proofRef must resolve (ZK proof, TEE quote/attestation, logs + hashes)
    
-   Sampling policy: e.g., 1/N random checks or mandatory for high-value/high-risk requests
    

* * *

How the Three Registries Work Together (End-to-End)

1.  Identity: agent registers → tokenURI → descriptor.json
    
2.  Interaction & Settlement: call service / pay (x402 / EIP-3009 etc.)
    
3.  Reputation: emit event with outcome, latency, paymentRef, integrityHash
    
4.  Validation (optional/sampled): request a check for jobRef/traceId → record verdict/proofRef
    
5.  Index & Aggregate: third parties combine Reputation + Validation to produce auditable scores and risk signals
    

[**ERC-8004 workflow**](https://x.com/FourPillarsFP/status/1974038601328701625)

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SunWeb3Sec/images/2025-10-15-1760496171325-image.png)
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
