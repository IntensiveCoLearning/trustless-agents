---
timezone: UTC+8
---

# Cooper

**GitHub ID:** qingfengzxr

**Telegram:** @icooperhero

## Self-introduction

大家好，我叫Cooper，一名区块链开发工程师，Web3爱好者。

## Notes
<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
## 什么是AP2?

  
**Agent Payments Protocol (AP2)** 是一个由 Google 与领先的支付和技术公司（超过 60 家，包括 Adyen、American Express、Mastercard、Paypal 等）共同开发和宣布的\*\*开放协议\*\*。

它旨在为 **AI 代理（Agent）** 主导的支付提供一个安全的、跨平台的交易启动和执行框架。AP2 可以作为 Agent2Agent (A2A) 协议和 Model Context Protocol (MCP) 的扩展使用。它建立了一个与具体支付方式无关的框架，让用户、商家和支付服务提供商能够通过各种支付方式（如信用卡、借记卡、稳定币和实时银行转账）自信地进行交易。

**AP2 的核心作用是解决 AI 代理能够代表用户进行交易时所产生的\*\*信任、安全和责任问题\*\*。**

AP2 的灵活设计为**新型商业模式提供了基础**，例如：

\- **更智能的购物**：代理可以根据用户预先设定的条件（如“愿意多付 20% 购买绿色夹克”）自动监控价格和库存，并在条件满足时执行安全购买。

\- **个性化优惠**：代理可以代表用户向商家传达意图（如旅行日期），商家的代理可以据此创建定制的、有时效性的捆绑优惠。

\- **协调任务**：代理可以同时与多个服务（如航空公司和酒店）的代理进行交互，并在符合用户总预算时，同步执行多项加密签名的预订。

## 什么是x402?
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->

观看ERC-8004的Workshop:  
[https://www.bilibili.com/video/BV1ChWkzvEdf/?vd\_source=a5b3dc7305ae6e3f310852f7273a82a2](https://www.bilibili.com/video/BV1ChWkzvEdf/?vd_source=a5b3dc7305ae6e3f310852f7273a82a2)
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->


## 什么是A2A协议？

The A2A protocol is an open standard that enables seamless communication and collaboration between AI agents. It provides a common language for agents built using diverse frameworks and by different vendors, fostering interoperability and breaking down silos. Agents are autonomous problem-solvers that act independently within their environment. A2A allows agents from different developers, built on different frameworks, and owned by different organizations to unite and work together.

## 没有A2A协议，代理间互相协作会遇到的挑战有哪些？

Without A2A, integrating these diverse agents presents several challenges:

-   **Agent Exposure**: Developers often wrap agents as tools to expose them to other agents, similar to how tools are exposed in a Multi-agent Control Platform (Model Context Protocol). However, this approach is inefficient because agents are designed to negotiate directly. Wrapping agents as tools limits their capabilities. A2A allows agents to be exposed as they are, without requiring this wrapping.
    
-   **Custom Integrations**: Each interaction requires custom, point-to-point solutions, creating significant engineering overhead.
    
-   **Slow Innovation**: Bespoke development for each new integration slows innovation.
    
-   **Scalability Issues**: Systems become difficult to scale and maintain as the number of agents and interactions grows.
    
-   **Interoperability**: This approach limits interoperability, preventing the organic formation of complex AI ecosystems.
    
-   **Security Gaps**: Ad hoc communication often lacks consistent security measures.
    

The A2A protocol addresses these challenges by establishing interoperability for AI agents to interact reliably and securely.

## MCP和A2A协议的差别是什么？

-   **MCP's Focus:** Reducing the complexity involved in connecting agents with tools and data. Tools are typically stateless and perform specific, predefined functions (e.g., a calculator, a database query).
    
-   **A2A's Focus:** Enabling agents to collaborate within their native modalities, allowing them to communicate as agents (or as users) rather than being constrained to tool-like interactions. This enables complex, multi-turn interactions where agents reason, plan, and delegate tasks to other agents. For example, this facilitates multi-turn interactions, such as those involving negotiation or clarification when placing an order.
    

MCP和A2A都在不同的层级发挥它们的作用，二者都非常重要。

例如：一个智能应用可能主要使用 A2A 与其他智能体进行通信。每个独立的智能体内部使用 MCP 与其特定的工具和资源进行交互。

![Diagram showing A2A and MCP working together. A User interacts with Agent A using A2A. Agent A interacts with Agent B using A2A. Agent B uses MCP to interact with Tool 1 and Tool 2.](https://a2a-protocol.org/latest/assets/a2a-mcp.png)

Agent are not tools 文章：[https://discuss.google.dev/t/agents-are-not-tools/192812](https://discuss.google.dev/t/agents-are-not-tools/192812)  
**将代理封装为工具是由局限性的，因为它无法解放代理的全部能力。**

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/qingfengzxr/images/2025-10-17-1760671157255-image.png)
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->



## 1.阅读了其他同学的笔记，获得了对ERC-8004的一些新的想法。

## **This Protocol Enables**

-   Agent discovery (capabilities, communication endpoints, supported trust models, etc.)
    
-   Marketplaces and agent explorers to be created.
    
-   Builds reputation systems; all feedback becomes public goods.
    

## **Security Considerations**

-   Sybil attacks to manipulate feedback are possible to inflate fake agents.
    
-   Audit trail thanks to immutability.
    
-   Validation incentives and slashing are managed by other protocols.
    
-   Capabilities cannot be guaranteed based on what the agents describe. The three trust models (reputation, validation, and TEE attestation) are designed to support this verification need.
    

## 2.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->




首先阅读了EIP-8004的提案内容：[https://eips.ethereum.org/EIPS/eip-8004。](https://eips.ethereum.org/EIPS/eip-8004。)

了解到了EIP-8004是对于A2A协议的一个扩展，以加入使用区块链技术来实现TrustLess的目标。协议主要利用TokenURI来进行链下协作，信任问题则由链上解决。

以下为关键内容的引用：

* * *

为了构建一个开放的、跨组织的代理经济，我们需要在不可信环境下发现并信任代理的机制。本 ERC 通过三个轻量级注册中心来满足这一需求，这些注册中心可以作为单例部署在任何 L2 或主网上：

**Identity Registry** - A minimal on-chain handle based on [ERC-721](https://eips.ethereum.org/EIPS/eip-721) with URIStorage extension that resolves to an agent’s registration file, providing every agent with a portable, censorship-resistant identifier.

**Reputation Registry** - A standard interface for posting and fetching feedback signals. Scoring and aggregation occur both on-chain (for composability) and off-chain (for sophisticated algorithms), enabling an ecosystem of specialized services for agent scoring, auditor networks, and insurance pools.

**Validation Registry** - Generic hooks for requesting and recording independent validators checks (e.g. stakers re-running the job, zkML verifiers, TEE oracles, trusted judges).
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
