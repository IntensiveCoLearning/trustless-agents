---
timezone: UTC+8
---

# mora

**GitHub ID:** moraqaq

**Telegram:** @morazh

## Self-introduction

我从 2020 年开始参与区块链公司和社区项目建设，管理过十几个官方推特账户，和行业内各类角色对话密切。2023 年起开始探索AI+Web3 结合，是App Store 上首个AI 占星app 的首席占星师，并且协助该公司完成了一轮web2+web3的融资。之前一直专注于叙事和项目运营层面，现在希望深入学习一些技术相关的内容。

## Notes

<!-- Content_START -->
# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->
1.  **Open Standard for Agent Interoperability:** A2A is an open standard protocol designed to enable seamless communication and collaboration between diverse AI agents.
    
2.  **Breaks Down Silos:** It provides a common language that allows agents built with different frameworks and by various vendors to work together effectively.
    
3.  **Enables Complex Collaboration:** It solves the challenge of orchestrating multiple specialized agents (e.g., for planning a complex international trip) without the need for custom, point-to-point integrations.
    
4.  **Secure Communication:** The protocol uses HTTPS for secure communication and ensures "opaque execution" to protect the internal logic and intellectual property of collaborating agents.
    
5.  **Retains Agent Autonomy:** A2A allows agents to interact as autonomous entities, enabling complex, multi-turn interactions like negotiation or delegation, rather than being constrained as simple, stateless tools.
    
6.  **Leverages Existing Web Standards:** It promotes simplicity and adoption by building upon established technologies like HTTP, JSON-RPC, and Server-Sent Events (SSE).
    
7.  **Supports Asynchronous Operations (LRO):** The protocol natively handles long-running operations and streaming data, crucial for enterprise-level tasks where agents may not remain continuously connected.
    
8.  **Enterprise Readiness:** A2A is designed with critical enterprise needs in mind, supporting robust authentication, authorization, tracing, and monitoring.
    
9.  **Modality Independent:** It allows agents to communicate using a wide variety of content types, enabling rich and flexible interactions beyond plain text.
    
10.  **Complements MCP:** A2A focuses specifically on standardizing **Agent-to-Agent** communication, complementing protocols like the Model Context Protocol (MCP) which focuses on connecting models to tools and data.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->

-   **ERC-8004** is a **proposed Ethereum standard** that defines a **trustless discovery framework** for autonomous AI agents, built upon Google's Agent-to-Agent (A2A) protocol.
    
-   Its design is **intentionally lean** and does not directly solve trust but facilitates visibility, allowing the ecosystem to build diverse trust solutions.
    
-   The standard is built on **three core onchain registries**: **Identity**, **Reputation**, and **Validation**.
    
-   The **Identity registry** links an agent's unique ID to its off-chain capabilities file (skills, protocols, trust models).
    
-   The **Reputation registry** uses **onchain authorization events** for accepted jobs, creating an audit trail for off-chain feedback history.
    
-   **Flexible Trust Models** are supported, ranging from social consensus (simple tasks) to **crypto-economic validation** (staking capital) and **cryptographic validation** (TEE/ZK) for critical applications.
    
-   **ROFL (Runtime Off-chain Logic)**, a **TEE framework**, is a key mechanism for cryptographic validation, ensuring **compute integrity** and **confidentiality** for sensitive AI workloads.
    
-   ROFL enables **truly trustless agents** by separating the creator from the agent, allowing users to trust the code.
    
-   ERC-8004 is complemented by the **x402 payment protocol**, which is already live in A2A and championed by organizations like Cloudflare for agent-to-agent payments across the internet.
    
-   The standard is moving toward a stable v2 specification, including support for **NFT-based agent ownership (ERC-721)** and cleaner integration with x402.
<!-- DAILY_CHECKIN_2025-10-17_END -->
<!-- Content_END -->
