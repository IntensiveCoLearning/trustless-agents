---
timezone: UTC+8
---

# Lucas

**GitHub ID:** tikpen

**Telegram:** @fearbekilled

## Self-introduction

Strong interest in Web3, I want to learn cutting-edge technologies.
Web front-end developer.

## Notes
<!-- Content_START -->
# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->
觉得ERC-8004与MCP有些相似，做一些对比

| 项目 | ERC-8004 | MCP（Model Context Protocol） |
| --- | --- | --- |

| 所属领域 | Web3 / 以太坊生态 | AI / 模型生态 |

| 定义 | 一种以太坊的 ERC标准，用于描述和发现链上 资源上下文（Resource Context） | 一种 AI模型上下文协议，让模型能够与外部工具、数据源、插件通信 |

| 核心目标 | 让链上资产或资源（如NFT、数据、服务）能以标准化方式被发现和交互 | 让AI模型能通过统一接口访问“上下文”——如文件、数据库、API、插件等 |

| 设计动机 | 为 Web3 内容和资源建立 互操作性标准 | 为 AI 模型建立 跨系统上下文标准 |

## 相似点（理念层面的）

1.  **都是“上下文协议”**
    
    -   ERC-8004 是为链上资源定义“上下文描述”（例如资源元数据、引用、关系）。
        
    -   MCP 则是为 AI 模型定义“上下文来源”（例如数据库、网页、插件）。  
        → 二者都强调：**系统之间要共享上下文，避免孤岛化。**
        
2.  **都是开放标准**
    
    -   ERC 是以太坊社区提出的公开提案。
        
    -   MCP 是 OpenAI 等推动的开放协议，任何模型或客户端都可实现。  
        → 都希望建立一个**可扩展、可互操作的生态系统**。
        
3.  **都促进“智能实体之间的协作”**
    
    -   ERC-8004 让不同智能合约、DApp 理解同一资源。
        
    -   MCP 让不同模型、工具理解同一任务上下文。  
        → 都让“智能体”更容易协同。
        

## 不同点（技术与应用层面）

| 对比项 | ERC-8004 | MCP |
| --- | --- | --- |
| 协议层级 | 区块链协议（L1-L2 上的智能合约） | 应用层协议（AI runtime与工具之间） |
| 数据来源 | 去中心化（链上或IPFS等） | 中心化或混合（本地文件、API、知识库等） |
| 通信方式 | JSON / ABI 调用 / 智能合约接口 | JSON RPC / WebSocket / HTTP 协议 |
| 参与方 | 智能合约、DApp、钱包 | AI 模型、插件、Agent、工具提供商 |
| 使用示例 | ERC-8004 定义一个 NFT 的动态元数据资源引用 | MCP 让 GPT 访问你的数据库或外部 API 获取上下文 |
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->

# x402协议

### 使用HTTP与区块链结合，实现internet-native payments

### 客户端请求一个 Web 资源（API／内容／服务） → 如果需要支付，服务端返回 HTTP 402 状态 + 支付提示 → 客户端按照协议进行链上支付或其他形式的支付 → 请求成功

-   **无费用**
    

x402 作为一种协议，对客户或商家均不收取任何费用。

-   **即时结算**
    

以区块链的速度接受付款。2 秒即可将款项存入您的钱包，无需 T+2。

-   **区块链不可知论者**
    

x402 不与任何特定的区块链或代币绑定，它是一个向所有人开放的中立标准。

-   **无摩擦**
    

只需在现有 Web 服务器堆栈中添加一行中间件代码或配置，即可开始收款。客户和代理无需创建账户或提供任何个人信息。

-   **通过开放标准实现安全和信任**
    

任何人都可以实现或扩展 x402。它不受任何中心化提供商的约束，并鼓励广泛的社区参与。

-   **Web 原生**
    

激活休眠的 402 HTTP 状态代码，并适用于任何 HTTP 堆栈。它只需通过现有 HTTP 服务器上的标头和状态代码即可工作。
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->


Today, I learned what the A2A and AP2 protocols do.

A2A: Agents can interact with each other.

AP2: Let the Agent interact on behalf of the user and complete certain operations.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->



ERC-8004 is a protocol standard that enables on-chain AI agents to discover, verify and interact in a trustless manner.

And it meets three characteristics: identity registration, reputation registration, and verification registration
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
