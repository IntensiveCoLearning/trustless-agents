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
