---
timezone: UTC+8
---

# Leo

**GitHub ID:** leopc999

**Telegram:** @elegant_5T

## Self-introduction

A web3 enthusiast in AI.

## Notes
<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
今天阅读了 QuillAudits 文章《ERC-8004: Infrastructure for Autonomous AI Agents》。

* * *

## 一、QuillAudits 视角：ERC-8004 的定位与价值

### 1\. 从 A2A 协议到区块链信任层的演进

-   QuillAudits 提到，Google 的 Agent-to-Agent (A2A) 协议（Agent Cards, JSON-RPC 通信, 能力协商等）确实在组织内部发挥了作用，但它默认假设通信方之间已有信任关系。QuillAudits 认为，这在跨组织、链上 / 跨平台的 Agent 生态中无法成立。
    
-   ERC-8004 的提出，则正是为了填补 “Agent 通信协议 + 信任机制”之间的空白：让 Agent 之间在没有预先信任的情况下也能进行合作。
    
-   从 QuillAudits 的表述看，他们强调的是：ERC-8004 不是单纯的 token / 能力协议，而是“信任基础设施”（trust backbone / trust layer）。
    

### 2\. 轻量链上 + 重量链下 = 混合设计（Hybrid Architecture）

-   QuillAudits 特别指出 ERC-8004 在设计上的**轻量链上**取向：链上只存储关键的授权 / 索引 / 校验逻辑，而把大多数声誉数据 / 验证细节 / Agent Card / 反馈文件都放在链下（通过 URI 引用）
    
-   这种设计有两个好处：
    
    1.  **减少 gas 成本 / 链上负担**
        
    2.  **更灵活 / 可扩展**：链下系统可以随意使用复杂的评分算法或验证逻辑，而不被链上效率约束
        
-   在 QuillAudits 的解读里，Reputation Registry 本身不保存实际评分数据，而只负责“**反馈授权（feedback authorization）**”的链上记录。真实的声誉计算留给链下系统。
    
-   类似地，Validation Registry 是一个通用钩子（hook），允许对某个数据 / 任务请求发出验证请求 / 记录响应。它不限定验证协议细节，而允许多种验证机制共存（staking 重运行、TEE attestation、密码学证明等）。
    

### 3\. 分层信任模型（Tiered Trust Models）

QuillAudits 引入一个“信任分层”概念，强调对不同风险 / 任务价值要用不同信任级别：

| 风险 / 任务价值级别 | 建议信任机制 |
| --- | --- |
| 低风险 / 日常任务 | 基于 Reputation（评价 / 反馈） 即可 |
| 中风险 / 涉及价值 / 资金 | 加入 Crypto-Economic 验证机制：验证者需抵押 / 被惩罚以保证诚实性 |
| 高风险 / 关键任务 | 使用 可信执行环境 (TEE) 证明 / 硬件证明 / 加密证明，以提供更强的保证 |

这种方式强调：信任机制应该与任务价值成正比，不要总用最严苛的方法，也不要总用最宽松的方法。

* * *

## 二、QuillAudits 补充的风险 / 安全考量 & 攻击向量

QuillAudits 在文章末尾列了几个他们认为设计者必须特别注意 / 防范的攻击 / 安全风险点。整理如下，并适当补充我的理解。

| 风险 | 描述 | 缓解 / 对策 |
| --- | --- | --- |
| Domain 抢注 / 前置（Front-Running） | 在 AgentDomain 注册时，有人可能监测到交易池，然后抢在你之前注册同一个域名（domain squatting） | 使用 commit–reveal 机制 或隐藏提交（即先提交哈希、稍后公开）来防止抢注 |
| 反馈授权滥用 | 如果 AcceptFeedback(agentClient, agentServer) 没有权限检查，任何地址都能调用这个接口，生成假的 AuthFeedback 记录，污染反馈授权体系 | 在合约里加入权限校验，比如仅 msg.sender == serverAgentAddress 才能生成授权，确保只有被评价的 Agent 本身或其授权方可以发授权 |
| 存储膨胀 / DoS 攻击 | 如果 ValidationRequest 被大量调用，则请求记录会在链上长期占用存储（直到超时 /清除），可能导致未来 gas / 存储成本变高或恶意阻塞 | 设计超时清除（expire）机制、限制每个 AgentServerID 可挂起请求数、对提交请求收取保证金 / bond 并在完成后返还 |
| Sybil 身份滥用 | 恶意方可批量注册 Agent 身份（Domain + 地址）来操纵声誉系统 / 做协调攻击 | 要求注册时最低保证金 / 销毁 /锁定 / probation 期后返还；或者通过零知识证明 / 唯一性签名机制限制一个经济实体能控制的身份数量 |

QuillAudits 的这些补充是非常实用的“落地建议 /安全提醒”，很值得在真是部署实现时一一考虑。

* * *

## 三、QuillAudits 解读的新增视角总结

1.  **定位侧重点：信任基础设施，而非能力 / 通信协议**
    
    -   强调 ERC-8004 是为 Agent 生态提供信任层，构建信誉、验证机制基础。
        
    -   它与 A2A / 能力协议 / 任务调度协议并不冲突，而是互补。
        
2.  **链上 ↔ 链下 混合架构是关键设计权衡**
    
    -   链上尽可能简洁，只做授权 / 索引 / 事件记录
        
    -   链下承担复杂评分 / 反馈 / 验证细节
        
    -   这样能在保持透明 / 可组合性的基础上，提高效率、扩展性、灵活性。
        
3.  **信任模型按业务价值分层**
    
    -   不是所有任务都要求最高级验证机制
        
    -   低风险任务只依赖评价，重要任务依赖 staking / 硬件证明
        
    -   这种分层信任设计让系统更实用、成本更可控
        
4.  **现实风险 / 攻击场景不可忽略**
    
    -   抢注、授权滥用、存储 bloat、Sybil 等都是现实攻击路径
        
    -   在实现时，不仅要遵照 ERC-8004 的接口规范，也要在合约层、经济机制层做防护设计
        
5.  **实现示例 / 伪代码**
    
    -   文章里给出了 Identity Registry / Reputation Registry / Validation Registry 的伪代码示例（简化版）
        
    -   特别在 Reputation Registry 部分，只做 `AcceptFeedback`，而不直接存评分数据，是一种“授权记录 + 反馈在链下”的轻量化方案
        
    -   在 Validation Registry 中，用 mapping 存 request，再在验证回应时做清除、emit event 等。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->

# 构建无信任代理（Trustless Agents）：ERC-8004 Workshop

本次会议围绕“无信任代理（Trustless Agents）”相关的 ERC-8004 标准展开，涵盖标准背景、核心功能、技术实现及后续规划，我参会后，对核心内容进行了总结。

## 一、ERC-8004 标准核心价值与背景

1\. **解决的核心问题**：随着 AI 在经济活动中（如供需匹配、信息交互）的作用增强，需建立类似“物理世界”的去中心化系统——让 AI 代理能自主发现、交互，避免依赖中心化中介（如应用商店）。

2\. **标准定位**：通过区块链智能合约构建“中性信息基础设施”，为 AI 代理提供身份、声誉、验证三大核心能力，支撑开放的“代理经济”。

## 二、ERC-8004 三大核心结构

### 1\. 身份注册表（Identity Registry）

\- **功能**：为 AI 代理提供“全球通讯录”，支持代理注册、信息展示与发现。

\- **技术实现**：基于 NFT（ERC-721）标准，注册时需提供指向链下 JSON 文件的 URI（含代理名称、技能、通信端点等信息），生成唯一“代理 ID”（即 NFT 的 Token ID）。

\- **灵活操作**：支持代理转移、指定“操作员”（代维护代理信息），且兼容现有 NFT 生态（如市场、浏览器可直接展示代理信息）。

### 2\. 声誉注册表（Reputation Registry）

\- **功能**：收集用户对代理的反馈，形成可验证的声誉数据。

\- **反馈规则**：用户无需注册即可提交反馈，但需提供代理签署的“反馈授权凭证”（避免未交互就评分的垃圾反馈）；反馈含“0 - 100 分”、可选标签及链下详细信息链接。

\- **数据使用**：可在链上直接查询代理声誉（如筛选特定用户、特定标签的评分），也支持基于此构建上层应用（如游戏中代理组队信任判断）。

### 3\. 验证注册表（Validation Registry）

\- **功能**：为代理的“工作成果”提供验证通道，适用于需证明真实性的场景（如 AI 任务执行结果）。

\- **操作流程**：代理完成任务后，向指定智能合约提交“验证请求”（含任务数据链接，支持 IPFS 或中心化存储）；仅指定的“验证者”可提交“验证响应”（0 - 100分，支持“失败/通过”二元判断）。

\- **兼容方案**：支持零知识证明（zkML）、质押安全推理（Stake Secure Inference）、可信执行环境（TEE）等多种验证技术，兼顾隐私与公开验证需求。

### 四、技术落地与使用细节

1\. **当前进展**：已发布参考实现代码（开源），并部署至 Sepolia 测试网；提供 SDK（社区也在开发适配工具），支持通过 Hardhat 本地运行测试（`npm run local` 启动节点 `npm test` 运行测试用例）。

2\. **用户体验优化**：支持 EIP-1271 标准，可实现“无 Gas 费交互”（智能合约钱包签名），降低开发者使用门槛。

### 五、关键规划与问题解答

1\. 主网部署与治理

\- **时间线**：最坏情况 10 月底部署以太坊主网，具体取决于社区反馈；

\- **治理机制**：采用多签钱包（Multisig）分布式治理，以太坊基金会协调部署，避免单一主体控制；初期保留合约升级灵活性，后续可能转为不可变合约。

2\. 常见问题回应

\- **数据隐私**：验证数据隐私性取决于技术方案——zkML 可隐藏私有输入，质押安全推理需公开数据，TEE 可通过加密实现隐私；

\- **恶意评分过滤**：支持通过规则筛选恶意反馈，但暂无法实现“完全防攻击”，需依赖上层应用优化；

\- **链上/链下数据**：核心信息（如代理 ID、评分）链上存储，详细信息（如任务描述）链下存储（IPFS 为主）；计划通过 The Graph等工具实现多链数据索引。

### 六、后续行动

\- 社区持续收集反馈，优化标准与实现；

\- 近期将召开会议讨论“链上 TEE 验证数据标准化”，欢迎开发者参与；

\- 建议开发者加入社区（已超 750 人），获取最新 SDK 与部署动态。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


\# ERC-8004 学习笔记：Trustless Agents 标准

\> 标准链接：[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

\> 目标：为 **去中心化 Agent（含 AI agents）** 提供\*\*信任基础设施\*\*，实现 **身份注册 + 声誉反馈 + 结果验证**。

\---

\## ✨ 一、为什么需要 ERC-8004？

在去中心化 Agent 生态中，Agent 之间要协作或交易，但存在三个核心问题：

| 问题 | 描述 | 需要的能力 |

|------|------|------------|

| 我如何找到一个 Agent？ | 缺乏全局标准身份 | **身份注册** |

| 我能信任它吗？ | 无法评估质量可靠性 | **声誉系统** |

| 它给的结果是真的吗？ | 结果可能被操控或出错 | **结果验证机制** |

✅ ERC-8004 提出解决方案：三个链上注册表（Registry）构成的\*\*可组合信任层\*\*。

\---

\## 🧱 二、核心组成（3 大 Registry）

\### 1. **Identity Registry（身份注册表）**

为每个 Agent 分配一个链上身份`agentId`（基于 ERC-721）

| 功能 | 说明 |

|------|------|

| 注册 Agent | 每个 Agent 拥有唯一 ID |

| 关联元数据 | tokenURI 指向 Agent JSON 描述文件 |

| 支持扩展 | 可存额外 metadata |

✅ 解决的问题：\*Agent 可发现、可识别、有公开接口描述\*

\---

\### 2. **Reputation Registry（声誉反馈注册表）**

记录用户/客户端对 Agent 的服务评分与反馈

| 支持的内容 | 说明 |

|------------|------|

| 评分（0–100） | 质量分 |

| 标签（tag1, tag2） | 用于分类或评价维度 |

| feedback URI + hash | 指向详细反馈的链下文件 |

| 撤销反馈 | 支持撤回 |

| 反馈可回应 | Agent 可回应用户评论 |

✅ 解决的问题：\*让 Agent 有“链上信用历史”\*

\---

\### 3. **Validation Registry（验证注册表）**

允许验证者对 Agent 的执行结果进行验证登记（验证可信性）

| 功能 | 描述 |

|------|------|

| 提交验证请求 | Agent 或用户提交验证任务 |

| 验证者回应 | 给出 response 分数 + URI 证明 |

| 多次验证 | 支持软/硬最终性验证 |

| 可过滤统计 | 按 agent / validator / tag 查询验证情况 |

✅ 解决的问题：\*结果可验证，信任不是嘴上说说\*

\---

\## 🔧 三、支持的信任模型（可组合）

Agent 可声明支持哪些信任方式：

\- ✅ Reputation Trust（声誉信任）

\- ✅ Crypto-economic Trust（质押+验证）

\- ✅ Hardware Attestation（TEE）

\- ✅ zkML / Proof-based Trust

\- ✅ 甚至未来扩展其他模型

📌 这些在 Agent 注册文件 `tokenURI JSON`) 中的 `supportedTrust` 字段声明。

\---

\## 🔄 四、工作流程示意

\`\`\`mermaid

sequenceDiagram

participant U as 用户

participant IR as Identity Registry

participant RR as Reputation

participant VR as Validation

participant A as Agent

A->>IR: 注册 agentId

U->>A: 调用任务

U->>RR: 提交评分/反馈

U->>VR: (可选) 请求验证

VR->>U: 返回验证记录


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
\# ERC-8004 学习笔记：Trustless Agents 标准

\> 标准链接：[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

\> 目标：为 **去中心化 Agent（含 AI agents）** 提供\*\*信任基础设施\*\*，实现 **身份注册 + 声誉反馈 + 结果验证**。

\---

\## ✨ 一、为什么需要 ERC-8004？

在去中心化 Agent 生态中，Agent 之间要协作或交易，但存在三个核心问题：

| 问题 | 描述 | 需要的能力 |

|------|------|------------|

| 我如何找到一个 Agent？ | 缺乏全局标准身份 | **身份注册** |

| 我能信任它吗？ | 无法评估质量可靠性 | **声誉系统** |

| 它给的结果是真的吗？ | 结果可能被操控或出错 | **结果验证机制** |

✅ ERC-8004 提出解决方案：三个链上注册表（Registry）构成的\*\*可组合信任层\*\*。

\---

\## 🧱 二、核心组成（3 大 Registry）

\### 1. **Identity Registry（身份注册表）**

为每个 Agent 分配一个链上身份`agentId`（基于 ERC-721）

| 功能 | 说明 |

|------|------|

| 注册 Agent | 每个 Agent 拥有唯一 ID |

| 关联元数据 | tokenURI 指向 Agent JSON 描述文件 |

| 支持扩展 | 可存额外 metadata |

✅ 解决的问题：\*Agent 可发现、可识别、有公开接口描述\*

\---

\### 2. **Reputation Registry（声誉反馈注册表）**

记录用户/客户端对 Agent 的服务评分与反馈

| 支持的内容 | 说明 |

|------------|------|

| 评分（0–100） | 质量分 |

| 标签（tag1, tag2） | 用于分类或评价维度 |

| feedback URI + hash | 指向详细反馈的链下文件 |

| 撤销反馈 | 支持撤回 |

| 反馈可回应 | Agent 可回应用户评论 |

✅ 解决的问题：\*让 Agent 有“链上信用历史”\*

\---

\### 3. **Validation Registry（验证注册表）**

允许验证者对 Agent 的执行结果进行验证登记（验证可信性）

| 功能 | 描述 |

|------|------|

| 提交验证请求 | Agent 或用户提交验证任务 |

| 验证者回应 | 给出 response 分数 + URI 证明 |

| 多次验证 | 支持软/硬最终性验证 |

| 可过滤统计 | 按 agent / validator / tag 查询验证情况 |

✅ 解决的问题：\*结果可验证，信任不是嘴上说说\*

\---

\## 🔧 三、支持的信任模型（可组合）

Agent 可声明支持哪些信任方式：

\- ✅ Reputation Trust（声誉信任）

\- ✅ Crypto-economic Trust（质押+验证）

\- ✅ Hardware Attestation（TEE）

\- ✅ zkML / Proof-based Trust

\- ✅ 甚至未来扩展其他模型

📌 这些在 Agent 注册文件 `tokenURI JSON`) 中的 `supportedTrust` 字段声明。

\---

\## 🔄 四、工作流程示意

\`\`\`mermaid

sequenceDiagram

participant U as 用户

participant IR as Identity Registry

participant RR as Reputation

participant VR as Validation

participant A as Agent

A->>IR: 注册 agentId

U->>A: 调用任务

U->>RR: 提交评分/反馈

U->>VR: (可选) 请求验证

VR->>U: 返回验证记录

## 五、优点

| 优点 | 描述 |
| --- | --- |
| 模块化 | 身份/声誉/验证分层设计 |
| 可组合 | 任意协议可基于它扩展 |
| 链上可信 | 数据可审计、可追溯 |
| 去中心化 Agent 基础设施 | 与 MCP、A2A 互补 |

## 六、风险与挑战

| 风险 | 说明 |
| --- | --- |
| Sybil 攻击 | 恶意刷声誉 |
| 验证经济未定义 | Slashing/Staking 需外部标准补充 |
| 结果依赖链下 URI | 需要可靠存储如 IPFS |
| 数据量扩展 | 声誉写入可能昂贵 |

## 七、小结

-   ERC-8004 是 **Agent 信任层基础设施**。
    
-   通过三个 Registry 建立 **身份 + 声誉 + 验证**。
    
-   使 **链上 Agent 市场 & AI Agent Economy 成为可能**。
    
-   与通信协议（如 MCP/A2A）互补，而非竞争。
    
-   下一步生态重点将围绕：  
    ✅ 信任模型扩展  
    ✅ 验证协议  
    ✅ Agent Marketplace 搭建
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## 五、优点

| 优点 | 描述 |
| --- | --- |
| 模块化 | 身份/声誉/验证分层设计 |
| 可组合 | 任意协议可基于它扩展 |
| 链上可信 | 数据可审计、可追溯 |
| 去中心化 Agent 基础设施 | 与 MCP、A2A 互补 |

## 六、风险与挑战

| 风险 | 说明 |
| --- | --- |
| Sybil 攻击 | 恶意刷声誉 |
| 验证经济未定义 | Slashing/Staking 需外部标准补充 |
| 结果依赖链下 URI | 需要可靠存储如 IPFS |
| 数据量扩展 | 声誉写入可能昂贵 |

## 七、小结

-   ERC-8004 是 **Agent 信任层基础设施**。
    
-   通过三个 Registry 建立 **身份 + 声誉 + 验证**。
    
-   使 **链上 Agent 市场 & AI Agent Economy 成为可能**。
    
-   与通信协议（如 MCP/A2A）互补，而非竞争。
    
-   下一步生态重点将围绕：  
    ✅ 信任模型扩展  
    ✅ 验证协议  
    ✅ Agent Marketplace 搭建
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
