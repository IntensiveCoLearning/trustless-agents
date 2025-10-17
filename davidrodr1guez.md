---
timezone: UTC-5
---

# David Rodriguez

**GitHub ID:** davidrodr1guez

**Telegram:** @daveitt

## Self-introduction

Hi everyone! My name is David, and I’m excited to be part of this programming course. I’m passionate about technology and eager to improve my coding skills to build real-world projects. I’m especially interested in how AI and automation can make people’s lives easier. I’m looking forward to learning from all of you and collaborating on creative ideas.

## Notes

<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
**Notes – ERC-8004**

ERC-8004 is about letting AI agents interact without needing to trust each other. It uses blockchain for identity, reputation, and validation — so agents can basically work and collaborate on their own. Kind of like a framework for this whole “agent economy” idea everyone’s talking about.

So, there are these three main parts:

-   **Identity registry:** each agent has an ID linked to its address + some metadata (name, description, endpoints, etc.). It’s like an NFT that represents the agent, so you can verify it and know who you’re dealing with.
    
-   **Reputation registry:** handles ratings and feedback between agents. It doesn’t store the actual score on-chain (too expensive), just the authorization. The rest lives off-chain. Makes it easier to build different reputation systems.
    
-   **Validation registry:** for checking if an agent’s output is legit. Can be through staking, zk proofs, or TEE (trusted execution environments). Basically, a way to confirm that an agent did what it said it would do.
    

The main problem this tries to solve is the lack of trust between agents. Before this, agents could talk to each other but only inside trusted systems (like Google’s A2A). This one lets them work across networks, even if they don’t know each other.

Example: imagine an auditing agent gets a job from a DeFi protocol agent. Without ERC-8004, neither can verify if the other is real or reliable. With this, both can check each other’s ID and past reviews before doing anything.

Also, the idea is to scale the trust system depending on how critical the task is.

-   for small stuff → reputation is enough
    
-   for more important stuff → use staking
    
-   for high-stakes tasks → use TEE to prove everything was done securely
    

There are still some risks like fake identities, spam registrations, or fake reviews. They propose using token bonds or zk-proofs to avoid that.

In the end, ERC-8004 is like the base layer for autonomous AI agents to work together safely. It doesn’t solve everything, but it gives them a way to identify, verify, and build trust without needing a middleman.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

Notes – ERC-8004 (Trustless Agents)

ERC-8004 is a proposal that allows agents (AI, bots, etc.) to interact with each other without needing prior trust. The idea is to use blockchain to manage identity, reputation, and validation — basically building an “open economy of agents.”

Main Structure

There are three main registries that make the system work:

Identity Registry

Each agent is registered as an NFT (ERC-721).

The NFT stores basic info about the agent (name, description, endpoints, image, etc.).

It helps identify and discover agents easily.

Reputation Registry

Lets users or agents leave ratings (0–100) and comments about others.

Data is stored both on-chain and off-chain for deeper analysis.

Reviews can be revoked or replied to.

Validation Registry

Agents can request to have their work verified.

Validators can use staking, zkML, or TEE oracles to check results.

Everything is recorded on-chain and can be audited.

Trust Models

Reputation: based on user or agent feedback.

Crypto-economic validation: through staking or proofs.

TEE attestation: done in secure environments.

Agents can use one or more of these models depending on the type of task.

Possible Uses

Marketplaces or explorers for agents.

Public and transparent reputation systems.

On-chain validation for AI outputs.

Collaboration between agents from different networks or organizations.

Security & Limitations

Data can’t be deleted — full traceability.

Risk of Sybil attacks (fake identities).

Doesn’t guarantee that an agent works well, only that its identity and reputation are verifiable.

Incentive and penalty mechanisms for validators aren’t defined yet.

Summary

In short, ERC-8004 aims to create a framework where agents can work together without relying on trust. It uses NFTs for identity, public feedback for reputation, and verifiable validation processes to make interactions between agents more transparent and reliable.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
