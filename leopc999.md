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
