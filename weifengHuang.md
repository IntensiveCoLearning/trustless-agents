---
timezone: UTC+8
---

# brreze

**GitHub ID:** weifengHuang

**Telegram:** @https://t.me/breeze_0071

## Self-introduction

I’m a software engineer with a strong interest in Web3, AI, and automation. I’ve previously participated in AI-agent development, but haven’t yet explored integrating AI with Web3. Through this program, I hope to gain hands-on experience and collaborate on practical projects that bridge these two fields.

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
### [**1\. Discussion on Ethereum Magicians (ERC-8004 Thread)**](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098/9)

**Topic:** Community consensus and open questions from the ERC-8004 “Trustless Agents” discussion.

**Key takeaways:**

-   **Core boundary:** ERC-8004 focuses on _identity, reputation, and validation_ for on-chain agents — _payments are deliberately excluded_ from the standard.
    
-   **On-chain data:** Minimal “composable” data should be stored (identity + key metrics), while larger feedback or validation results remain off-chain.
    
-   **Cross-chain identity:** Future versions will support _CAIP-10 / DID-based identities_ for agent portability.
    

**Still debated:**

-   Whether to keep resolveByDomain (domain-unique) or move to URL/URI-based resolution.
    
-   How to support delegated writes / authorization for multi-sig or managed agents.
    
-   The right design of reputation models — single vs. multidimensional scoring.
    
-   Verification methods — TEE vs. zkML vs. sampling / re-execution.
    
-   Agent ID strategy — deterministic vs. flexible for key rotation.
    

### **2.** [**Insights from HashKey Capital Article —**](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098) 

### [**ERC-8004 and the Agent Economy**](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098)

**Two key understandings:**

**(a) Types of Agents to Develop**

ERC-8004 defines **three roles**, not three mandatory components to build:

-   **Client:** requests tasks and gives feedback.
    
-   **Server:** executes tasks (the main role most developers will deploy).
    
-   **Validator:** verifies results.
    
    You can register **only your Server-type agent** to make it discoverable and hireable on-chain; validation and payment can rely on external registries or services.
    

**(b) Five Promising Use Cases**

1.  **Crypto Deep-Research Agents** – AI researchers producing sector analyses (e.g., DeFi yield reports) with verifiable data-hash commitments and reputation-based hiring.
    
2.  **AI-Driven Crypto Hedge Funds** – Automated strategy agents competing by track record; validators re-execute strategies to confirm performance before profit-sharing.
    
3.  **On-Chain Credit Ratings & Credit Origination** – Agents compute borrower credit scores; DeFi lenders use validated scores to set loan terms.
    
4.  **Agent Scoring & Audit Services** – Specialized validator-agents auditing other agents’ work, maintaining an open reputation layer.
    
5.  **Conditional Milestone Payouts for Gig Economy** – Task-based or freelance agents receive payments through escrow only after verified milestone completion.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/weifengHuang/images/2025-10-15-1760541719099-image.png)

I studied [EIP-8004](https://eips.ethereum.org/EIPS/eip-8004).

EIP-8004 builds on **A2A** and extends it by introducing modules for **registration, verification, and reputation scoring**.

It does **not restrict how agents are developed** — instead, it provides a framework that enables agents to be **discovered on-chain**.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
