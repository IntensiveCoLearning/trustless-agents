---
timezone: UTC+8
---

# Oscar

**GitHub ID:** luffythink

**Telegram:** @lessaremore

## Self-introduction

A eco-lifelong learner. To surf🏄‍♀️ better in the Web3 world. Enjoy this challenging vibe and become cooler 🆒.

## Notes

<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
学习主题：[https://github.com/isekOS/ISEK](https://github.com/isekOS/ISEK)

重要笔记：

-   **ISEK** is a decentralized framework designed for building **AI Agent Network**. Instead of treating agents as isolated executors, it provides the missing layer of collaboration and coordination. Developers run their agents locally, and through peer-to-peer connections, these agents join the ISEK network. Once connected, they can discover other agents, form communities, and deliver services directly to users.
    
-   At the core of the network, **Google’s A2A protocol and ERC-8004 smart contracts enable identity registration, reputation building, and cooperative task-solving.** This transforms agents from standalone tools into participants in a shared ecosystem. We believe in self-organizing agent networks — systems that can share context, form teams, and reason collectively without central control.
    
-   Agent Explorer: [Agent explorer](https://isek-explorer.vercel.app/)
    
-   Registered Agents on block chain
    

!\[\]([https://github.com/isekOS/ISEK/raw/main/assets/blockchain.png](https://github.com/isekOS/ISEK/raw/main/assets/blockchain.png))

![](https://github.com/isekOS/ISEK/raw/main/assets/blockchain.png)
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->

学习主题：[https://a2a-protocol.org/latest/](https://a2a-protocol.org/latest/)

笔记：The Agent2Agent (A2A) Protocol is an open standard developed by Google and donated to the Linux Foundation designed to enable seamless communication and collaboration between AI agents.

Why use the A2A Protocol?

-   Interoperability
    
-   Complex Workflows
    
-   Secure & Opaque
    

How does A2A work with MCP?

!\[\]([https://a2a-protocol.org/latest/assets/a2a-mcp-readme.png](https://a2a-protocol.org/latest/assets/a2a-mcp-readme.png))

In a world where agents are built using diverse frameworks and by different vendors, A2A provides a common language, breaking down silos and fostering interoperability.
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->


学习主题：[https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879](https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879)

重要笔记：ERC-8004 Proposal and Vision

1\. The Core Problem:

-   The current AI landscape is dominated by centralized "AI Oligarchs" and "Platform Gatekeeping."
    
-   To counter this, we need decentralized agent economies.
    
-   A major hurdle is a lack of a common, standardized language for agents to discover, trust, and communicate with each other, leading to a "classic coordination problem."
    

2\. The Proposed Solution: ERC-8004

-   ERC-8004 is designed to be this common language, enabling decentralized agent coordination.
    
-   It is not a new blockchain; it uses existing Ethereum L1/L2s as a logically centralized entry point for visibility and data commitments.
    
-   Core Philosophy:
    
    -   Minimal and Unopinionated: It doesn't reinvent the wheel but builds on existing ideas (e.g., EigenLayer, TEEs). It provides a lightweight base for identity and trust, leaving specific reputation rules and calculations to the ecosystem.
        
    -   Solves Coordination: It gives everyone equal data and visibility to create an agent economy, without imposing strict rules.
        

3\. The Path to Creation:

-   The author identified a gap: Google's Agent2Agent (A2A) protocol, while well-made and credibly neutral, ignored Web3 and trustless use cases.
    
-   In collaboration with the Ethereum Foundation's AI Lead and Google, **they worked to expand the A2A protocol into the Web3 space, resulting in ERC-8004.**
    

4\. Overwhelming Community Response:

-   The proposal went viral, with thousands of engagements, translations, memes, and discussions.
    
-   This indicates massive latent demand in the ecosystem for applying Web3 principles (permissionless, decentralized, censorship-resistant) to AI.
    

5\. Next Steps and Governance:

-   A "building-first approach" will be adopted. Feedback and change requests will be prioritized from teams actually building on the standard.
    
-   **The goal is to drive adoption and make Ethereum the foundational infrastructure for the future of AI.**
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->



学习主题：[https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d](https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d)

重要笔记：

The recent proposal of ERC-8004, which acts as an extension of A2A protocol, aims to solidify Ethereum’s position as the substrate for AI coordination.

-   MCP created a universal framework for accessing tools
    
-   A2A built a universal communication layer for web2 agents to interoperate with one another
    
-   ERC-8004 serves as a blueprint to unlock new revenue streams and enhance user experience through trustless, interoperable agent-to-agent coordination using Ethereum.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->




学习主题：[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

重要笔记：

To foster an open, cross-organizational agent economy, we need mechanisms for discovering and trusting agents in untrusted settings. This ERC addresses this need through three lightweight registries, which can be deployed on any L2 or on Mainnet as per-chain singletons:

-   **Identity Registry** - A minimal on-chain handle based on [ERC-721](https://eips.ethereum.org/EIPS/eip-721) with URIStorage extension that resolves to an agent’s registration file, providing every agent with a portable, censorship-resistant identifier.
    
-   **Reputation Registry** - A standard interface for posting and fetching feedback signals. Scoring and aggregation occur both on-chain (for composability) and off-chain (for sophisticated algorithms), enabling an ecosystem of specialized services for agent scoring, auditor networks, and insurance pools.
    
-   **Validation Registry** - Generic hooks for requesting and recording independent validators checks (e.g. stakers re-running the job, zkML verifiers, TEE oracles, trusted judges).
    

ERC-8004针对当前 Agent 服务生态的最大问题——中心化信任瓶颈和数据孤岛，提出了一套开放、无需许可且可信中立的基础架构，使Agent服务能够真正跨组织、跨平台无缝交互，消除中心化平台对Agent服务的控制。ERC-8004不是孤立的标准，而是以Google等公司开源的Agent-to-Agent（A2A）通信协议为基础，补齐了原本A2A协议所缺乏的去中心化信任层，解决了A2A协议只适用于内部或受信环境的局限。
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
