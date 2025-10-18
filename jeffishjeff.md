---
timezone: UTC+8
---

# Jeff Huang

**GitHub ID:** jeffishjeff

**Telegram:** @jeffishjeff

## Self-introduction

Learning web3

## Notes
<!-- Content_START -->
# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->
More on ERC8004, watched the 1st community call and ETH Panda call.

Points on deployment / operational side:

-   Singleton deployment and global discoverability. ERC-8004 is designed to function through a **singleton registry per chain**—one contract each for Identity, Reputation, and Validation—so all agents reference a **shared source of truth**. This prevents fragmentation (multiple competing registries) and makes agent discovery and reputation lookup consistent across ecosystems. It also simplifies cross-chain bridging: different chains can mirror or checkpoint the same singleton entries, allowing an agent’s identity and trust data to travel with it.
    
-   Spam filtering in reputation. The Reputation Registry is intentionally open, which creates room for **rating spam and sybil noise**. Instead of hard limits, ERC-8004 encourages off-chain filtering layers—indexers, scoring services, oracles—that weight ratings by validator stake, validation history, or cryptographic signatures. This shifts “spam resistance” to the reputation algorithm rather than the base protocol, maintaining permissionlessness while enabling **trust-weighted aggregation** to surface reliable signals.
    
-   Flexibility of validation methods. ERC-8004’s Validation Registry is **method-agnostic**: any validator contract implementing the interface can register a method. That means a network can start with simple manual attestations, then later plug in **economic staking**, **zk-proof verifiers**, or **TEE attestations** without changing the base standard. This modularity makes it future-proof—validation can evolve with advances in cryptography, economics, or AI audit techniques, all while remaining interoperable under one unified schema.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

### Learning ERC-8004

ERC-8004, also known as **“Trustless Agents,”** is a proposed Ethereum standard designed to enable autonomous or AI-driven agents to safely interact, transact, and collaborate with each other **without requiring pre-established trust**. It builds on the earlier Agent-to-Agent (A2A) protocol by introducing a **lightweight on-chain trust framework**, allowing agents from different domains or organizations to coordinate in an open ecosystem.

At its core, ERC-8004 defines three minimal registries: **Identity**, **Reputation**, and **Validation**. The **Identity Registry** lets agents publish verified metadata about who they are and what they can do; the **Reputation Registry** records community feedback after interactions; and the **Validation Registry** provides a mechanism for independent validators to attest that an agent’s claimed actions or outputs are correct. These registries serve as a shared trust substrate while leaving application-specific logic, payments, and data off-chain.

The motivation behind ERC-8004 is the rise of the **machine economy**—a world where AI agents negotiate services, exchange value, or manage digital assets on behalf of humans or organizations. By standardizing identity, reputation, and validation interfaces, ERC-8004 aims to make such autonomous systems interoperable and auditable across blockchains. In essence, it turns Ethereum into the **trust layer for AI and autonomous agents**, providing a minimal, composable foundation for decentralized cooperation between machines.
<!-- DAILY_CHECKIN_2025-10-15_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->

Deep dive on a couple ERC-8004 nuances:

-   **Identity: on-chain anchor, off-chain truth.** ERC-8004 lets any agent register an ID that points to an off-chain “AgentCard,” but it doesn’t enforce authenticity. Proving “who’s who” is done off-chain (DNS sigs, attestations, track record).
    

-   **Validation: a modular truth primitive.** Its Validation Registry records that “X validated result Y for task Z,” but doesn’t dictate how—you can use staking/slashing, zk/TEE proofs, or pure attestations. Because payouts/escrow can key off these records, validation becomes pluggable market infrastructure for trust, reusable across apps like an oracle for “was this done right?”.
    

Both feel vague and flimsy to be honest. While it's totally understandable why the standard is specified this way, would need to see more concrete/real world example to understand how it holds up and be useful.
<!-- DAILY_CHECKIN_2025-10-17_END -->
<!-- Content_END -->
