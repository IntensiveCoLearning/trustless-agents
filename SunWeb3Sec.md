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
