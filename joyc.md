---
timezone: UTC+9
---

# hython

**GitHub ID:** joyc

**Telegram:** @hython

## Self-introduction

Web3 Product PM

## Notes
<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
## 为什么需要设计三层注册：  
  
1\. 身份层（Identity Registry）——“我是谁？”

**目的：确立唯一、可验证的智能体身份。**

-   每个 Agent 必须在链上注册，获得唯一的 `AgentID`。
    
-   该 ID 与其域名（AgentDomain）和以太坊地址（AgentAddress）绑定。
    
-   所有注册信息公开透明，任何人都能解析并验证。
    
-   链下，智能体需要在 `/.well-known/agent-card.json` 处发布自己的「Agent Card」，描述能力、模型类型、验证方式等。
    

**意义**：  
身份层解决了最基础的「谁是谁」的问题——没有可信身份，后续的信誉与验证都无从谈起。它构建了去中心化的「身份命名系统」，类似于区块链世界的 DNS。

* * *

### 2\. 信誉层（Reputation Registry）——“我值不值得信任？”

**目的：建立可追踪的声誉系统。**

-   当客户端智能体（Client Agent）与服务端智能体（Server Agent）交互后，可以授权反馈。
    
-   合约不存储评分，而是仅生成一个「反馈授权事件（AuthFeedback）」。
    
-   真正的评分与评价数据存放在链下（例如 JSON 文件），可以由第三方信誉系统读取并计算综合分数。
    

**意义**：  
信誉层为智能体提供了社会性信任来源。它模拟人类社会中的“口碑”，为低风险、日常任务（如内容生成、信息查询）提供足够的信任基础，而不需要昂贵的链上验证。

* * *

### 3\. 验证层（Validation Registry）——“我能证明我做对了吗？”

**目的：在高风险场景下提供强验证。**

-   用于发起和记录验证请求（ValidationRequest / Response）。
    
-   支持两种验证模式：
    
    -   **加密经济验证（Crypto-Economic Validation）**：验证者（Validator）需质押一定资金，若验证错误将被惩罚（slashing）。
        
    -   **密码学验证（Cryptographic Validation）**：通过 TEE 可信执行环境、ZK 证明等方式提供可验证的执行结果。
        
-   适用于金融交易、智能合约审计、医疗或高价值任务等高风险场景。
    

**意义**：  
验证层是“硬信任”机制，用经济或密码学手段保证行为真实可靠。它防止恶意或错误的智能体执行关键任务。

* * *

### 为什么要“三层”？

因为不同任务的风险与成本不同，信任机制需要「分层而非统一」：

| 场景 | 所需信任强度 | 对应层级 | 示例 |
| --- | --- | --- | --- |
| 低风险（如生成文本） | 弱信任 | 信誉层 | “内容好不好”由反馈决定 |
| 中风险（如金融建模） | 中等信任 | 经济验证层 | 验证者重跑计算、质押保证 |
| 高风险（如医疗决策） | 强信任 | 密码学验证层 | 通过 TEE 或 ZK 证明执行正确性 |

**总的目标**：在「成本」与「信任」之间取得最优平衡。  
区块链不适合把一切都放在链上，ERC-8004 采用混合式架构：**只把最必要的信任锚点上链**，其余逻辑交给链下扩展系统处理。

* * *

> ERC-8004 的三层信任体系让 AI 智能体能在不同风险场景下自由选择信任级别，从“轻量级信誉”到“加密经济验证”，再到“硬件级密码证明”，既保持去中心化，又兼顾效率与安全。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

# **ERC-8004: Trustless Agents**

[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

**背景：**  
ERC-8004 把“发现、口碑、验证”三件事标准化为三套轻量注册表，为开放的 agent 经济提供可组合的信任层，补上 MCP/A2A 没覆盖的“谁、能不能信、谁来背书”的空白。

### **为什么有用（给产品/架构的直观价值）**

-   **可组合**：评分/验证事件在链上可被任意合约消费，离链再做复杂聚合；适合做 agent 目录、排行、质检与保险等上层生态。
    
-   **跨协议桥接**：注册文件里统一挂 **A2A、MCP、ENS、DID、钱包** 等端点，让通信层（会话/指令）与信任层（发现/评价/验证）解耦。
    
-   **成本/灵活度**：把大对象放离链（IPFS/HTTP）+ 链上存最小必要索引/哈希，既省 gas 又保留审计轨迹。围绕“哪些字段需要链上可读”社区仍在讨论中。
    

### **核心机制**

-   **Identity Registry（身份）**：把每个 agent 铸造成一枚 **ERC-721**（带 URIStorage），tokenURI 指向注册文件（含名称、说明、端点清单如 A2A/MCP/ENS/DID、agent 钱包等）。可多链/多注册，天然可浏览与转移。
    
-   **Reputation Registry（声誉）**：任何客户端地址（人/agent）都可在 agent 许可下提交 **0–100 分**的反馈，含可选标签与离链 JSON（IPFS 优先，链上存摘要/索引以便组合）。读接口支持按 reviewer/标签聚合。撤回与附加回应也有事件。
    
-   **Validation Registry（验证）**：agent 主动向某个 **validator 合约**发起验证请求（请求数据放离链 + 哈希承诺），validator 回写 **0–100** 的响应值与证据 URI（可多次更新，支持软/硬终局）。聚合读取接口可按 validator/tag 汇总。
    

> 提案刻意把**支付**排除在标准之外，但示例建议把 x402 支付证明等作为离链反馈字段一并记录。

### **最小落地路径**

1.  **部署 IdentityRegistry**（每链单例）→ register() 铸出 agentId → 设置 tokenURI 指向注册 JSON，填上 A2A/MCP/钱包等端点与 supportedTrust。
    
2.  **接单时**，agent 用 **EIP-191/ ERC-1271** 签出 feedbackAuth，授权某客户端地址可写反馈。客户端调用 giveFeedback(...) 上链；需要时可 revokeFeedback(...) 或附加 appendResponse(...)。查询用 getSummary(...) / readAllFeedback(...)。
    
3.  **需要强信任时**，调用 validationRequest(...) 指定 validator；待对方 validationResponse(...) 回写评分与证据。汇总用 getValidationStatus(...) / getSummary(...)。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
