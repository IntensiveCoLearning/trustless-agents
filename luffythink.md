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
