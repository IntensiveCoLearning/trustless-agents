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
# 2025-10-28
<!-- DAILY_CHECKIN_2025-10-28_START -->
Checked others' learning notes
<!-- DAILY_CHECKIN_2025-10-28_END -->

# 2025-10-27
<!-- DAILY_CHECKIN_2025-10-27_START -->

Checked x402 ecosystem.
<!-- DAILY_CHECKIN_2025-10-27_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->


Checked the document of [ISEK](https://github.com/isekOS/ISEK) .
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->



It's been a busy day. Nothing much to update.
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->




Some questions about x402

-   What is x402?
    
-   When using x402, is a TCP-like connection needed? How does it handle situations where service provider needs time to prepare for the result?
    
-   How does authentication and identification work here?
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->





### Questions

-   For Reputation Registry, what are recorded on-chain, how is the on-chain data connected with off-chain data?
    
-   For Validation Registry,
    
    -   How many validators can it be for one validation?
        
    -   How to prove the validator really does the validation, instead of submitting random result?
        
    -   Is there a way to validate the validation from a validator?
        
-   In ERC8004, what kind of tasks are we talking about? If validation can be done directly on-chain, what is the purpose of this protocol?
    
-   What is the difference between ERC8004 and a oracle?
    
-   What is TEE and how does it work?
    
-   What is Google's A2A protocol?
    
-   What is AP2 protocol?
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->






Checked A2A protocol
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->







It is Sunday today.
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->








Keep reading the document and check the discussions.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->









It's been a busy day, and I only checked others' notes for learning. Nothing more.
<!-- DAILY_CHECKIN_2025-10-17_END -->

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
<!-- Content_END -->
