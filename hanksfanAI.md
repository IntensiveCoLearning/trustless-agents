---
timezone: UTC+8
---

# Hanks Fan

**GitHub ID:** hanksfanAI

**Telegram:** @hanksfanAI

## Self-introduction

ETH x AI: the last economy

## Notes
<!-- Content_START -->
# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
3 bullets on ERC-8004 problems solves:  
  
1. On-chain discoverability and identity for agents  
Provides a standardized and verifiable on-chain identity layer (AgentCard) that allows AI agents to be discovered and authenticated without central intermediaries.  
  
2. Trust and reputation propagation  
Introduces a trustless reputation framework where validators can attest to agents’ reliability, reducing the risk of malicious or low-quality agents.  
  
3. Interoperability across ecosystems  
Creates a modular, cross-ecosystem trust and registration fabric, enabling agents and services from different platforms or chains to interact securely under a shared standard.
<!-- DAILY_CHECKIN_2025-10-15_END -->


# 2025.10.16
<!-- DAILY_CHECKIN_2025-10-16_START -->
ERC-8004 aims to build a trust and discovery layer for autonomous AI agents on Ethereum. The core idea is that each agent can have a chain-verifiable identity (e.g. via an AgentCard), reputation history, and validation proofs, all built on a shared set of on-chain registries (Identity, Reputation, Validation). By separating these trust primitives from the application logic, ERC-8004 allows multiple verification modes—TEE attestation, staking, zk proofs—without locking into a single payment or routing protocol.  
  
A key insight from the community discussion is that reputation is contextual: Alice’s trust in Bob may differ from Charlie’s, depending on domain and past interactions. Therefore, ERC-8004 emphasizes modularity—let different reputation providers or oracles run independently—and resists attempting to collapse all trust into one universal score. Also, the protocol deliberately does not mandate a specific payment or escrow mechanism, to avoid coupling trust infrastructure with payment systems; such logic is left to higher layers or applications.  
  
In practice, a useful workflow might be: use ERC-8004 to discover agents, check their reputations and validation proofs, then use another protocol or smart contract to mediate task assignment, escrow, result verification, and payment. The separation of concerns aims to keep the trust layer lean and future-proof, enabling permissionless innovation while preserving composability and security.
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
