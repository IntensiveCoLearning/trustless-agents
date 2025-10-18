---
timezone: UTC+8
---

# Draken

**GitHub ID:** Darkells

**Telegram:** @Allen_Draken

## Self-introduction

You'll never feel ready because ready isn't a feeling, it's a decision.

## Notes
<!-- Content_START -->
# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->
## What is the A2A?

A2A Protocol (Agent-to-Agent Protocol) is an open-source communication standard jointly developed by Google and over 50 partners (including the Linux Foundation). It is designed to enable AI agents to autonomously perform discovery, authentication, skill publishing, message passing, and task coordination.

Built upon the Model Context Protocol (MCP) — which is used to list capabilities such as prompts, tools, and completions — A2A focuses on agent collaboration in open environments, allowing agents from different organizations to cooperate without centralized intermediaries.

**Core Components and Functions:**

-   **AgentCards:** Standardized profiles where agents publish their skills, endpoints (such as MCP or A2A hooks), and capabilities.
    
-   **Task Lifecycle:** Manages authentication, direct messaging, and end-to-end task orchestration, supporting complex workflows (e.g., one agent hiring another to complete a subtask).
    
-   **Use Cases:** Enables the emerging **agent economy** in AI-driven applications, such as **DeFi automation**, **real-world asset (RWA) tokenization**, or **multi-agent research**, where agents can dynamically negotiate, execute, and verify tasks.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->

Reputation is a core component of the ERC-8004 trust model and is implemented through a reputation registry, a standardized interface for publishing and querying feedback reputation signals, helping agents accumulate a verifiable history of their behavior.

Question: How to ensure the reliability of agent reputation and prevent malicious reviews？

-   **Authorized Feedback & Economic Proof**: Feedback requires agent pre-authorization (feedbackAuth signature, limited by indexLimit to prevent spam) and optional x402 payment proof tied to real transactions, raising the cost of fake reviews.
    
-   **Sybil & Malicious Feedback Resistance**: Filters clientAddresses (prioritizing high-reputation reviewers); supports revokeFeedback and appendResponse for disputes; on-chain events and hashes ensure tamper-proof audits.
    
-   **Weighted Scoring & Aggregation**: On-chain average scores with tag filtering; off-chain advanced algorithms (e.g., reviewer reputation weighting); community audits detect time/pattern anomalies.
    
-   **Validation Backup**: Validation Registry uses TEE/zkML for independent checks, with external staking (e.g., EigenLayer AVS) and slashing to penalize malicious validators, providing objective proof.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->


simple flow:

```
1. Check Identity (Identity Registry)
   Employer A queries Employee B’s AgentCard (resume-like profile).

2. Reputation Assessment (Reputation Registry)
   A reviews B’s ratings (client feedback + validation records).

3. Task Assignment (Off-chain + Validation Registry)
   A assigns task to B → B executes → Optional third-party validation.

4. Submit Feedback (Reputation Registry)
   A submits rating + comments (with signature verification).

5. Update Reputation (Reputation + Validation Registries)
   B’s rating is updated for future employers to reference.

6. Market Loop
   B improves services → New employers join → Community governance.
```

TODO Agent life cycle and version management

-   The official/reference design of ERC-8004 supports metadata updates on the same NFT Agent (including adding or removing endpoints, updating descriptions, supporting trust models, etc.).
    
-   It does not mandate that model upgrades require the minting of new Agent NFTs.
    
-   The actual method for model upgrades (replacing NFTs or updating metadata) is flexible within the standard and is determined by the specific system/implementer.
    
-   The mechanisms provided by the standard (such as setMetadata and tokenURI updates) are sufficient to support a variety of upgrade strategies.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->



This is a very cutting-edge, and for me, very challenging course. On the first day, I will start by understanding the main content of EIP-8004, which is essentially a 'reputation system'.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
