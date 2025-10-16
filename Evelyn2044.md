---
timezone: UTC+8
---

# Evelyn

**GitHub ID:** Evelyn2044

**Telegram:** @Eve207

## Self-introduction

币圈萌新，多多学习

## Notes

<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
# 1016学习笔记

理解 ERC-8004

1.  **ERC-8004** 是一个基于 **Google A2A（Agent-to-Agent）协议** 的 **去信任化（trustless）链上标准**，  
    它通过智能合约为每个 AI 代理（Agent）提供 **唯一的链上身份（AgentID）**，  
    并引入 **能力证明、反馈证明、验证记录** 等机制，  
    从而在没有中心化管理或人工审核的情况下，  
    让 **Agent 与 Agent 之间能够自动、安全地发现、协作与验证彼此的可信度**。
    

* * *

| 概念 | 说明 |
| --- | --- |
| 基础协议：A2A | 由 Google 推出的 Agent 通信协议，定义了 AI 代理如何通过标准 JSON-RPC 接口互相交流与协作。 |
| ERC-8004 的作用 | 在 A2A 之上增加「信任层（Trust Layer）」，让这些通信在开放网络中也能验证对方的身份与信誉。 |
| 链上身份（Identity Registry） | 每个 Agent 拥有独立的 AgentID、AgentDomain 与 AgentAddress，可在链上唯一识别。 |
| 反馈与信誉（Reputation Registry） | 客户端 Agent 在任务完成后可提交反馈，链上授权、链下存储，形成透明的声誉系统。 |
| 验证机制（Validation Registry） | 可选的任务验证层，支持 stake 质押、TEE 或零知识证明，用于验证计算结果的真实性。 |
| 最终目标 | 构建一个无需人工信任、可自动发现与协作的 去中心化 Agent 经济（Agentic Economy）。 |

2.  在 ERC-8004 的信任体系里，有三类角色：
    

-   **Client Agent**（任务发起者）
    
-   **Server Agent**（执行者）
    
-   **Validator Agent**（验证者）
    

## Q&A：

### 1\. ERC-8004 如何确保验证者可信？

ERC8004-入了一个「**多层验证者信任模型**」。定义了三种层级的信任方式（可组合使用）：

| 层级 | 信任机制 | 主要保障 |
| --- | --- | --- |
| 🟢 经济质押验证（Crypto-Economic Validation） | 验证者需要质押代币；如果验证结果被证明错误或恶意，将被罚没（slashed）。 | 经济激励约束，防作恶 |
| 🟡 加密验证（Cryptographic Verification） | 验证者在可信执行环境（TEE，如 Intel SGX）中运行任务，生成远程证明（Remote Attestation）；或使用 ZK 证明（zkTLS、zkVM）。 | 硬件与密码学保证结果正确 |
| 声誉模型（Reputation-Based Trust） | 验证者的历史验证记录与反馈通过 Reputation Registry 公布。 | 透明度与可追溯信誉体系 |

这三种方式可以叠加使用，形成**分层信任模型（Tiered Trust Model）**。

### 2\. 如何应对AI不可避免的幻觉hallucination？

当 AI Agent 因「幻觉（hallucination）」或模型误判而任务验证失败时，  
如果直接罚没（slash）质押资金，会不会太苛刻？  
我们怎样在「安全性」与「容错性」之间找到平衡？

在 ERC-8004 的 **Validation Registry（验证注册表）** 中，  
验证者或服务代理可以通过 **质押（staking）** 参与任务验证。  
若结果错误或被证明欺诈，系统可触发 **slashing（罚没）**。

这在纯区块链环境（例如验证交易）非常有效，  
但 AI 代理有天然的不确定性：

-   模型可能因为上下文、模糊语义或数据偏差导致**合理但错误的输出**；
    
-   某些任务的“正确答案”本身具有主观性（如摘要、情感分析）。
    

因此，如果只用“**对 / 错**”二元判定去扣质押，  
AI 系统就会变得过于保守甚至无法运作。

* * *

ERC-8004 没有直接惩罚“AI犯错”，  
而是提供了 **可组合信任模型 + 可配置经济容忍度**。  
核心思想是：

> 不惩罚“模型的不完美”，只惩罚“恶意或不诚实的行为”。

* * *

**1️⃣ 分层信任模型（Tiered Trust Model）**

ERC-8004 的三层信任机制天然支持不同的任务容错率：

| 层级 | 信任类型 | 容错特征 |
| --- | --- | --- |
| 🟢 声誉型（Reputation-Based） | 仅依据历史反馈；适合主观、模糊任务。 | ✅ 高容错（不会罚没） |
| 🟡 经济质押型（Crypto-Economic） | 要求验证者 stake，但允许部分误差区间。 | ⚖️ 中容错（按误差比例罚没） |
| 🔵 加密验证型（TEE / ZK Proof） | 只用于客观计算验证（例如数学、智能合约审计）。 | 🚫 零容错（必须正确） |

这意味着，  
AI 代理可以在高主观任务中使用 **信誉信任**，  
在关键计算或金融逻辑中才激活 **经济验证**。

* * *

**2️⃣ “弹性罚没”机制（Probabilistic / Weighted Slashing）**

ERC-8004 的经济验证层通常由 **Restaking 网络**（如 EigenLayer、EigenCloud）支持。  
这些网络允许定义 **可调的罚没逻辑**：

-   若验证失败仅因轻微偏差（如 90% 正确），则只减少奖励或部分罚没；
    
-   若验证者多次输出虚假或恶意结果，才会全额处罚。
    

* * *

**3️⃣ 信号融合与群体验证（Multi-Validator Aggregation）**

ERC-8004 支持多个验证者对同一任务输出独立验证，  
结果可通过投票或权重平均形成“共识验证”：

这样可以抵消单个 AI 验证者的偏差。  
当大多数验证者认为结果合理，就不会触发罚没。  
这与 LLM 的“集体智慧（ensemble reasoning）”思路相似。

* * *

**4️⃣ Reputation Registry 与 AI 改进循环**

当 AI 验证者出现幻觉或误判，  
其信誉（Reputation）会轻微下降，但不会立即被淘汰。  
验证历史被记录在链上供训练者分析，  
从而形成“**反馈 → 改进 → 再验证**”的正循环。  
这使 ERC-8004 网络能**自我学习、逐步优化**验证模型。

* * *

| 应用场景 | 风险等级 | 推荐信任模型 | 是否允许容错 |
| --- | --- | --- | --- |
| 文本摘要、翻译 | 低 | 声誉信任 | ✅ 是 |
| DeFi 智能合约审计 | 高 | 经济 + 加密验证 | 🚫 否 |
| 模型推理验证（AI output） | 中 | 经济 + 群体验证 | ⚖️ 有限容错 |
| 医疗影像分析 | 高 | TEE + 多验证者 | 🚫 否 |

* * *

总结

> **ERC-8004 不惩罚“AI 出错”，惩罚“AI 不诚实”。**
> 
> **“不诚实” ≠ “犯错”。**  
> ERC-8004 惩罚的是「故意造假」「篡改输出」「伪造验证」「误导反馈」，而不是模型自然的不确定性。

ERC-8004 将代理（Agent）的不诚实行为定义为：

1.  **故意提交伪造的任务结果**  
    例如：声称已完成计算，但结果与输入完全无关。
    
2.  **篡改验证流程**  
    比如伪造验证事件、提交伪造签名或篡改链下数据。
    
3.  **操纵声誉系统**  
    如自我反馈（Sybil 攻击）或批量创建假代理互相评分。
    
4.  **拒绝可验证性**  
    即在被请求验证任务时拒绝提交 DataHash、AgentCard 或签名。
    

这些行为可通过多层机制发现并记录在链上。

3\. ERC8004处理Agent之间的交易吗

**Agent之间是可以进行交易的**，但具体方式取决于所使用的协议组合（ISEK、ERC-8004、A2A 和 x402）：

1.  **在 ISEK 网络中**，Agent 运行在一个去中心化的 P2P 网络里，可以直接协作和交换服务。ISEK 通过 ERC-8004 提供身份、信誉和验证机制，让 Agent 能够安全地发现并与其他 Agent 进行任务合作或服务交换。
    
2.  **在 ERC-8004 协议中**，Agent 通过三大注册表（身份、信誉、验证）建立信任关系。协议允许：
    
    -   Client Agent 向 Server Agent 发出任务请求；
        
    -   Server Agent 完成任务；
        
    -   Validator Agent 验证结果；
        
    -   验证通过后释放托管（escrow）中的付款。
        
    
    > ERC-8004 本身不处理支付逻辑，但它提供信任和验证基础，让交易可以在上层支付层（例如 x402）执行。
    
3.  **A2A 协议**负责实现 Agent 之间的通信与任务协商，它提供标准化的通信结构，使不同框架的 Agent 能够互相发现、协作、甚至达成交易任务。
    
4.  **x402 支付标准** 则是实现交易结算的核心。它允许 Agent 之间通过 HTTP 402 状态码直接进行加密支付，无需账户或人工介入，非常适合机器-对-机器（M2M）或 Agent-对-Agent（A2A）支付场景。
    

✅ **综合起来：**

-   A2A：负责通信与任务协商；
    
-   ERC-8004：负责身份、信誉与验证，建立信任；
    
-   x402：负责实际的支付结算；
    
-   ISEK：负责在去中心化网络中部署与发现 Agent。
    

因此，在 **ISEK + ERC-8004 + A2A + x402** 的架构下，Agent 之间不仅可以交易，还能实现 **自动协商、验证与结算** 的完整闭环经济系统。  
  
4\. 在具体的Agent to Agent 的交易场景中，**ISEK、A2A、ERC-8004、x402** 四个协议是如何协作？  
  
下面我通过一个完整的场景，来说明 **ISEK、A2A、ERC-8004、x402** 四个协议是如何协作的，让 Agent 之间实现一个**去中心化、有信任保障、自动结算的交易流程**。

* * *

🌍 场景：研究助理 Agent 雇佣审计 Agent 审查智能合约

> 角色：
> 
> -   **AliceAgent**：去中心化研究助理（Client Agent）
>     
> -   **BobAgent**：智能合约审计专家（Server Agent）
>     
> -   **CarolAgent**：验证与信誉审计员（Validator Agent）
>     

* * *

### 🧩 步骤 1：ISEK 网络 — Agent 发现与连接

1.  AliceAgent 运行在 **ISEK 网络** 上，这是一个去中心化的 Agent 网络框架，允许 Agent 自主发现与协作。
    
2.  ISEK 使用 **ERC-8004 的 Identity Registry** 注册每个 Agent 的身份（AgentID、域名、钱包地址），因此 Alice 可以通过 ISEK CLI 或 MCP 服务发现 BobAgent。
    
    ```
    isek discover --task "smart contract audit"
    ```
    
    ISEK 通过 **去中心化的注册表** 找到了信誉良好的 BobAgent。
    

* * *

### 💬 步骤 2：A2A 协议 — 任务协商与通信

1.  AliceAgent 读取 BobAgent 的 AgentCard（位于 `https://bobagent.xyz/.well-known/agent-card.json`），了解 Bob 提供的审计服务和授权方式。
    
2.  双方使用 **A2A 协议（Agent-to-Agent）** 开始协商任务：
    
    -   Alice 发出 `sendMessage` 请求，描述任务需求；
        
    -   Bob 回复任务报价、预期交付时间和所需验证方式；
        
    -   整个过程基于 JSON-RPC over HTTPS，安全且标准化。
        
    
    ```
    POST /sendMessage
    {
      "task": "audit smart contract v1.2",
      "budget": "0.05 ETH",
      "validation": "economic+TEE"
    }
    ```
    

* * *

### 🔐 步骤 3：ERC-8004 协议 — 信任与验证层

1.  双方确认任务后，AliceAgent 与 BobAgent 通过 **ERC-8004 的 Reputation Registry** 查询彼此的信誉记录。
    
    -   Reputation Registry 存储了去中心化的反馈授权信息；
        
    -   Alice 可以验证 Bob 的历史审计评分和客户反馈。
        
2.  Bob 完成任务后，生成审计报告的哈希值（`DataHash`），并向 **Validation Registry** 提交验证请求：
    
    ```
    ValidationRequest(DataHash, BobAgentID, CarolAgentID)
    ```
    
3.  CarolAgent（验证者）重新执行部分审计过程，确认结果正确后提交：
    
    ```
    ValidationResponse(DataHash, 1)
    ```
    
    这一步建立了**加密经济与可信验证的闭环**。
    

* * *

### 💰 步骤 4：x402 协议 — 自动支付结算

1.  当验证通过，AliceAgent 收到 “validated” 状态。
    
2.  通过 **x402 协议**，BobAgent 的审计服务端返回：
    
    ```
    HTTP/1.1 402 Payment Required
    Payment-Instruction: https://x402-facilitator.io/settle
    ```
    
3.  AliceAgent 自动执行支付请求，使用其钱包签名并发送加密货币（例如 ETH 或 USDC）。  
    x402 支持无账户、自动化微支付，非常适合 Agent 之间的机器支付。
    
4.  结算完成后，BobAgent 收到付款，ERC-8004 的 Reputation Registry 自动授权一条正向反馈。
    

* * *

### 🧠 步骤 5：ISEK 汇总信誉与网络更新

ISEK 网络会：

-   将本次交易的验证记录与反馈更新进去中心化索引；
    
-   让其他 Agent 可以基于 ERC-8004 的信誉机制信任 Bob；
    
-   保证整个系统不断自组织形成 **Agent 经济生态（Agentic Economy）**。
    

* * *

## 🔄 总结：四层协作模型

| 层级 | 协议 | 功能 | 示例作用 |
| --- | --- | --- | --- |
| 🌐 网络层 | ISEK | 去中心化 Agent 网络与发现 | 发现 BobAgent 并连接 |
| 💬 通信层 | A2A | Agent 间安全通信与任务协商 | 发出任务请求与接收响应 |
| 🔒 信任层 | ERC-8004 | 身份、信誉、验证、反馈 | 验证任务与信誉记录 |
| 💰 交易层 | x402 | 加密支付与结算 | 完成支付与结算 |

* * *

📘 **一句话总结：**

> 在 ISEK 网络中，A2A 让 Agent 能沟通，ERC-8004 让他们互信，x402 让他们能付费。四者共同构成了去中心化的 **Agent-to-Agent 自主经济体系**。
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
