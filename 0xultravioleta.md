---
timezone: UTC-5
---

# Saul

**GitHub ID:** 0xultravioleta

**Telegram:** @zeroxultravioleta

## Self-introduction

35 years coding. Focused on distributed systems, validating over 55 blockchains. Founder of Ultravioleta DAO. We build AI tooling —agents and workflows— for streaming communities, by experimenting and learning in public.

## Notes

<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
# Day 3 — Notes (Oct 17, 2025)

## 📖 Reading

**Article:** _The Story Behind ERC-8004 & Next Steps_ — Survival Tech  
**Link:** [https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879](https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879)

### Key Learnings

-   **Motivation & early traction:** ERC-8004 emerged as a critical proposal to bypass AI oligarchies and centralized platform gatekeeping, enabling a **distributed economy of agents**.
    
-   **Common language between AI projects:** It defines a protocol for **discovering and communicating** with agents across different organizations using standardized agent descriptors.
    
-   **On-chain entry, off-chain logic:** The standard keeps **core registries (identity, reputation, validation)** on-chain, while allowing **application-specific logic** to be handled **off-chain**.
    
-   **Permissionless & privacy-focused:** It promotes **censorship resistance**, **composability**, and **trustless interaction** — ideal for the AI + Web3 era.
    
-   **Decentralized registry system:** Not a global central server, but **per-chain singletons** acting as common entry points for discovery and interaction.
    

* * *

## 🛠 Hands-on

**Repo:** [https://github.com/vistara-apps/erc-8004-example](https://github.com/vistara-apps/erc-8004-example)

### What I did today

-   Since I’m on **Windows**, I had to **dockerize** the project to isolate environments and install all dependencies without issues.
    

### What I expect to learn from this repo

-   ✅ How to implement **smart contracts in Solidity** to manage **identity, reputation, and validation** using ERC‑8004.
    
-   ✅ How to connect a **Python backend** with a **React frontend** for decentralized apps that handle agent logic.
    
-   ✅ How to deploy contracts with **Foundry** and explore the **validation flow** in distributed systems.
    

* * *

## 🧠 My Understanding (Summary)

-   ERC‑8004 standardizes how agents are **discovered, chosen, and trusted** with **no prior trust** required.
    
-   It keeps the **core trust layer** on-chain while allowing rich **off-chain logic** for complex reputation and validation flows.
    
-   It’s gaining traction as a **foundational building block** for the emerging AI x Web3 ecosystem.
    

* * *

## ❓ Open Questions

-   How will the protocol handle **off-chain logic verification** to ensure **security, compatibility, and auditability**?
    
-   Are there plans for **decay mechanisms**, **weighting models**, or **anti-manipulation protections** in the reputation system?
    
-   What are best practices for **anchoring off-chain attestations** or feedback in a Sybil-resistant way?
    

* * *

## 🔜 Next Steps

-   Finalize Docker setup and run local tests.
    
-   Deploy the registries to a testnet using Foundry.
    
-   Test a minimal circuit: **register agent → send feedback → query reputation → simulate validation**.
    
-   Document all commands and configuration for reproducibility.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->

# Day 2 — ERC-8004 (Trustless Agents) — Study Notes

**Sources**

-   Ethereum Magicians thread: [https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098/97](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098/97)
    
-   QuillAudits overview: [https://www.quillaudits.com/blog/smart-contract/erc-8004](https://www.quillaudits.com/blog/smart-contract/erc-8004)
    

* * *

## TL;DR

-   **ERC-8004 = trust layer** that **extends the agent protocol** to let participants **discover, choose, and interact** with agents **across organizational boundaries** with **no prior trust**.
    
-   **3 on-chain registries:** Identity, Reputation, Validation.
    
-   **Goal:** discover agents and **establish trust** via **reputation** and **validation**.
    

* * *

## Core Ideas

-   **No previous trust required** between parties.
    
-   **Separation of concerns:**
    
    -   **On-chain:** the 3 core registries (identity, reputation, validation).
        
    -   **Off-chain:** application-specific logic.
        
-   **Open development:** collaboration with Linux Foundation and A2S ecosystem to refine the spec.
    
-   **Wide tech support:** ConsenSys, Nethermind, Google, Ethereum Foundation, EigenLabs, etc.
    

* * *

## From the QuillAudits Article

-   **Focus:** convergence of **AI + blockchain**.
    
-   **Advancement:** extends **A2S** protocol with **blockchain-based trust mechanisms**.
    
-   **Foundation for an agentic economy**: coordinate **trustlessly** across **untrusted networks**.
    
-   **Hybrid standard:**
    
    -   **Adds data on-chain**; **delegates complex ops off-chain**.
        
    -   Central components remain **on-chain**.
        
-   **Fixes A2S trust gaps:** A2S assumed pre-existing trust and worked mainly **within org boundaries** (e.g., Alice (auditor) can’t verify Bob (DeFi) across orgs).
    
-   **Benefits:** eliminates trust bottlenecks, enables discovery of reputable providers, ensures quality, **portable reputation**, **validation at scale**.
    
-   (Context note from article) **Global AI market** projection to **$1.8T by 2030**.
    

* * *

## Trust Models (by Risk Tier)

-   **Reputation-based (Low risk):**
    
    -   Simple tasks (e.g., content creation).
        
    -   **Social consensus** via accumulated feedback.
        
-   **Crypto-economic validation (Medium risk):**
    
    -   Financial tx or smart-contract operations.
        
    -   Validators **stake economic value** → strong incentives for honest behavior.
        
-   **Cryptographic verification (High risk):**
    
    -   Critical applications.
        
    -   **TEE attestations** (and other cryptographic proofs).
        

* * *

## Security Considerations

**Threats**

-   Domain squatting / frontrunning
    
-   Unauthorized feedback
    
-   Storage bloat & DoS
    
-   Sybil attack creation
    

**Mitigations**

-   **Commit-reveal** scheme for domain registrations
    
-   **Restrict** `msg.sender` for who can post feedback
    
-   **Auto-expiry** for ingested items + **rate limits** on validation requests
    
-   **Bond / token burn** for identity registration
    

* * *

## Open Questions / Doubts

-   How will the protocol handle the **diversity of off-chain logic** while staying **secure, verifiable, and compatible**?
    
-   Metrics & scoring: are there **detailed weighting mechanisms**? Is **rating cooling/decay** considered?
    
-   **Sybil/manipulation resistance:** how does the system **prevent gaming** while establishing trust **without historical data**?
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


# Today I learned about ERC 8004

ERC 8004 is a protocol that aims to ultimately provide an identity registry, reputation registry, and a validation registry.

## Identity Registry

-   Uses ERC-721 with the URIStorage extension.
    
-   Each agent is uniquely identified by: `namespace`, `chainId`, `identityRegistry`, and `agentId`.
    
-   The agent registry needs a registration file, which is a JSON file with all the optional and required fields for advertising their endpoints.
    
-   The structure can be found here: [https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)
    
-   The registry extends ERC-721 by adding a `getMetadata` function.
    
-   Agents may be minted by calling the `register` function.
    

## Reputation Registry

-   The identity registry address is passed as an argument to the constructor.
    
-   When agents accept a task, it’s expected that they sign an authorization feedback to authorize the client to give feedback.
    
-   Feedback can range from 0 to 100.
    
-   There is a way to extend the feedback using a JSON file. The only mandatory fields are `agentId` and `score`. The off-chain file is optional.
    
-   The `giveFeedback` function is called with the above requirements; if successful, it emits a `NewFeedback` event.
    
-   This exposes reputation signals to any smart contract, enabling on-chain composability.
    
-   When an agent gives feedback, it should use `walletAddress` as `clientAddress` to facilitate reputation aggregation.
    
-   Feedback can be revoked.
    
-   Off-chain additional feedback JSON file structure may be found here: [https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)
    

## Validation Registry

-   Allows agents to request verification of their work and ask for validations that can be tracked on-chain.
    
-   When the validation registry is deployed, the identity registry address is required as an argument in the constructor.
    
-   Agents call `validationRequest`; if successful, a `ValidationRequest` event is emitted.
    
-   `validationResponse` (can be called multiple times for the same with the same `responseHash`) and `validationResponse` event is emitted subsequently if it was successfully executed.
    
-   The response is a value from 0 to 100; it can be used as a binary: 0 for 0 and 100 for 1.
    

## Additional Notes

-   This is all initially for A2A and MCP, but new protocols may emerge. The flexibility of the registration file allows for future accommodations.
    
-   There is gas sponsorship with EIP-7702.
    
-   IPFS is suggested for feedback data.
    
-   Agents can register cross-chain. An agent receiving feedback on chain A can also operate in other chains.
    

## This Protocol Enables

-   Agent discovery (capabilities, communication endpoints, supported trust models, etc.)
    
-   Marketplaces and agent explorers to be created.
    
-   Builds reputation systems; all feedback becomes public goods.
    

## Security Considerations

-   Sybil attacks to manipulate feedback are possible to inflate fake agents.
    
-   Audit trail thanks to immutability.
    
-   Validation incentives and slashing are managed by other protocols.
    
-   Capabilities cannot be guaranteed based on what the agents describe. The three trust models (reputation, validation, and TEE attestation) are designed to support this verification need.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
