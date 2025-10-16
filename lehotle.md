---
timezone: UTC+8
---

# HD

**GitHub ID:** lehotle

**Telegram:** @lehotle

## Self-introduction

小芯片公司程序员
python, C/C++
业余研究 web3，AI
喜欢欣赏底层逻辑

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
ERC-8004 extends Google’s **Agent-to-Agent (A2A)** protocol by adding a **blockchain-based trust layer**, allowing autonomous agents to interact, verify each other, and build reputation **without centralized control or pre-existing trust**.

Tthree lightweight on-chain registries:

1.  **Identity Registry** — Provides each agent with a global, censorship-resistant ID (AgentID) that maps to its domain and Ethereum address. This registry enables agent discovery and verification.
    
2.  **Reputation Registry** — Handles authorization of feedback between agents. Reputation data lives off-chain, allowing flexible scoring systems while maintaining an immutable on-chain audit trail.
    
3.  **Validation Registry** — Records independent verifications (via staking or cryptographic proofs such as TEEs). It supports both **crypto-economic validation** and **cryptographic attestation** models.
    

Agents register via the Identity Registry, communicate and exchange tasks using A2A, and use the Reputation and Validation Registries to authorize feedback or request third-party verification. This hybrid model keeps essential trust data on-chain and heavier operations off-chain for scalability.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

First day, I tried to read the ERC-8004 original document, and haven't finished.

> This protocol proposes to use blockchains to **discover, choose, and interact with agents across organizational boundaries** without pre-existing trust, thus **enabling open-ended agent economies**.

Different trust models can be used according to requirement:

-   Reputation systems using client feedback
    
-   Validation via stake-secured re-execution
    
-   zkML proofs, or TEE oracles
    

Would continue tomorrow.
<!-- DAILY_CHECKIN_2025-10-15_END -->

# 2025.10.15
<!-- Content_END -->
