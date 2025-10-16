---
timezone: UTC+8
---

# Sky

**GitHub ID:** SkySommer

**Telegram:** @skysommer0317

## Self-introduction

Web3 PM and developer, LXDAO Designer, AI enthusiast.

## Notes
<!-- Content_START -->
# 2025.10.16
<!-- DAILY_CHECKIN_2025-10-16_START -->
### **Learning Report on ERC-8004: The Agentic Economy**

* * *

**1\. Core Concept: What is ERC-8004?**

ERC-8004 is an Ethereum standard designed for AI Agents, with the core objective of establishing a **trustless "trust layer"** for interactions between agents across different, untrusted organizational boundaries. While collaborations in current AI applications are often confined to closed or centralized systems, ERC-8004 addresses the key challenge of how AI agents can discover each other, verify the quality of their work, and build reputations in an open network.

The standard aims to foster an open and transparent "Agentic Economy," where AI agents can act as independent economic participants, autonomously providing services, collaborating, and earning credibility.

**2\. Key Protocol Components: The Three Core Registries**

The infrastructure of ERC-8004 is built upon three core smart contract registries, which work together to form a complete trust lifecycle.

-   **Identity Registry**:
    
    -   **Purpose**: To provide each AI agent with a unique, censorship-resistant on-chain identity (`agentId`).
        
    -   **How it Works**: An agent registers by mapping its domain (`agentDomain`) and wallet address (`agentAddress`) to a globally unique ID, creating a queryable "yellow pages" for agents.
        
-   **Reputation Registry**:
    
    -   **Purpose**: To establish a lightweight, on-chain mechanism for authorizing feedback.
        
    -   **How it Works**: Instead of storing costly reputation scores on-chain, it allows a server agent to authorize a client agent to provide feedback. This "authorization" event is recorded on-chain, while the actual reputation scoring and aggregation are left to off-chain services, balancing trust with flexibility.
        
-   **Validation Registry**:
    
    -   **Purpose**: To provide a generic, auditable workflow for work verification.
        
    -   **How it Works**: After completing a task, a server agent can submit a hash of its work to the chain and assign a validator agent. The validator, after reviewing the work, submits the result (e.g., a score) on-chain. This provides a decentralized proof of quality for complex AI tasks.
        

**3\. Key Roles: What is an "AI Agent"?**

In this project, an "AI Agent" is a composite concept, more than just a large language model. It is an **off-chain computational entity with an on-chain identity, capable of autonomously performing specialized tasks.**

-   **Technically**: It is powered by an AI framework (like `CrewAI`) and is assigned a clear role (e.g., Market Analyst), executable tools, and specific workflows.
    
-   **Economically**: Through the `ERC8004BaseAgent` class, each agent has its own wallet private key and on-chain identity, enabling it to independently sign transactions and participate in on-chain economic activities.
    

**4\. Practical Application: A Complete Workflow**

By analyzing the `demo.py` script, the application flow of ERC-8004 becomes clear:

1.  **Registration**: A Server Agent (Alice), a Validator Agent (Bob), and a Client Agent (Charlie) register on the `IdentityRegistry` to obtain their on-chain identities.
    
2.  **Execution**: Alice performs a complex AI task off-chain (e.g., market analysis).
    
3.  **Validation**: Alice submits a hash of her work to the `ValidationRegistry`, requesting validation from Bob. Bob validates the work and submits a score back on-chain.
    
4.  **Feedback**: Alice authorizes Charlie on the `ReputationRegistry` to provide feedback for the service rendered.
    
5.  **Audit**: All critical steps leave an immutable record on the blockchain, creating a complete trail of trust and auditability.
    

**5\. Conclusion & Insights**

The ERC-8004 protocol, by combining complex off-chain AI computation with lightweight on-chain trust records, provides an elegant and practical framework for building decentralized AI applications and service marketplaces. It not only solves the trust problem between AI agents but also offers standardized solutions for **proof-of-work, quality assessment, and reputation building**. For developers looking to build decentralized AI platforms, this protocol provides a modular and ready-to-use infrastructure, marking a significant milestone on the path toward the future "Agentic Economy."
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
