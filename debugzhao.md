---
timezone: UTC+8
---

# Tyson

**GitHub ID:** debugzhao

**Telegram:** @CryptoTysonn

## Self-introduction

curious about everything

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
-   **A2A协议**
    

_1.为何采用它_

Agent协作之间没有统一的规则，A2A协议提供AI代理之间“开放沟通标准”，使得不同框架（如 TensorFlow、PyTorch）、不同公司开发的 AI 代理，能无缝通信、一起协作

eg：A 代理负责数据分析，B 代理负责生成报告，二者通过 A2A 高效配合

_2.解决问题场景示例_

用户使用AI Agent来货币换算服务

Currency Conversion Agent：专注于执行 “不同货币间的汇率查询与换算”，是 A2A 协议中的 “功能型代理”，和AI Assistant之间通过A2A协议进行通信。

Request和Result：代表用户与 AI 助手、AI 助手与代理之间的 “数据交互”，A2A 协议会规定这些交互的标准格式，确保不同代理能顺畅沟通。

ps: A2A带来的优势：靠 HTTPS 实现安全协作（代理互不可见）、打破Agent代理孤岛实现互作、保留代理自主权、标准化沟通降低集成复杂度、支持长时间运行协作与流式处理。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

**5W模型快速了解ERC-8004**

-   What — ERC-8004 是什么？
    
    ERC-8004是一个基于以太坊（Ethereum）的开放标准，用于为AI Agent提供去中心化的 身份（Identity）、信誉（Reputation）和 验证（Validation） 基础设施。
    
    简单说：它是一个让 AI 代理在不信任环境中互相发现、验证、协作的「信任层」。它是对 Google 提出的 A2A（Agent-to-Agent）协议 的区块链扩展，在 A2A 的通信框架之上，引入了 Web3 的加密信任机制，**从而实现无需预先信任的智能体经济（Agentic Economy）**
    
-   Why — 为什么需要 ERC-8004？
    
    **A2A 协议让不同组织的 AI Agent能互相通信**，但存在一个关键问题：它假设通信双方彼此信任。这在封闭企业内部没问题，但在开放的全球 AI 网络中就不现实。
    
    ERC-8004 的出现正是为了解决这一“信任缺口（Trust Gap）”：
    
    -   如何判断一个 AI 代理是否可信？
        
    -   如何确保对方完成任务、支付报酬？
        
    -   如何建立可移植的信誉系统？
        
    
    因此，ERC-8004 提供：
    
    -   **统一身份系统（Identity Registry）**：为每个代理分配唯一的 AgentID 与域名。
        
    -   **链上授权信誉系统（Reputation Registry）**：追踪反馈授权并生成声誉凭证。
        
    -   **任务验证系统（Validation Registry）**：通过质押验证或 TEE 加密证明任务执行真实性。
        
    
    这些机制共同让 **AI 代理可以在无需信任的环境下协作、验证与结算**。
    
-   Who — 谁使用 ERC-8004？
    
    -   开发 去中心化 AI 代理 的团队（例如 ISEK 网络）
        
    -   构建 AI 经济体、DeAI 应用、信任验证层 的项目
        
    -   需要跨组织代理通信的企业（结合 A2A 协议）
        
-   How — ERC-8004 如何工作？
    
    ERC-8004 定义了三大核心合约
    
    -   Identity Registry（身份注册表）
        
        每个 Agent 注册时会获得一个唯一 ID（AgentID）
        
        ```
        AgentDomain  // 域名（如 ai.example.com）
        AgentAddress // EVM 地址
        ​
        ```
        
        这个注册表用于身份解析与去重（避免 Sybil 攻击）。每个 Agent 需在 `https://{AgentDomain}/.well-known/agent-card.json` 上托管自己的 Agent Card。
        
    -   Reputation Registry（信誉注册表）
        
        负责记录任务反馈授权事件，并不直接存储分数，而是授权链下系统记录与评分：
        
        ```
        event AuthFeedback(uint256 AgentClientID, uint256 AgentServerID, bytes32 FeedbackAuthID);
        ```
        
        这样既节省 gas，又支持复杂的多维度声誉系统（EAS、链下评估等）
        
    -   Validation Registry（验证注册表）
        
        用于验证任务结果的真实性，可选验证方式
        
        -   **Crypto-Economic Validation**（质押验证）
            
        -   **TEE/zkTLS Cryptographic Validation**（加密证明验证）
            
        
        典型流程：
        
        1.  Client Agent 指派任务给 Server Agent
            
        2.  Server 执行任务 → 发布结果哈希
            
        3.  Validator Agent 验证结果（可重算或生成证明）
            
        4.  验证通过 → 触发支付释放或声誉更新
            
-   总结
    
    ERC-8004 = AI Agent的去信任身份证 + 信用体系 + 验证系统。**它让 AI Agent能在没有中心化信任的世界里，发现彼此、验证身份、建立信誉，并完成自动协作与交易。**
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
