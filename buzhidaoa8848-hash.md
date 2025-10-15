---
timezone: UTC+8
---

# 离人泪很远了

**GitHub ID:** buzhidaoa8848-hash

**Telegram:** @18029320251

## Self-introduction

两财一贸大数据

## Notes
<!-- Content_START -->
# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
## 一、核心目标：开放式、跨组织的代理经济（Agent Economy）

> **关键问题**：如何在**没有预先信任的环境中**发现、选择、验证 AI Agent？  
> **解决方案**：通过三类链上注册表（Registries）建立信任基础。

* * *

## 🧱 二、架构组成（3 Registries）

| 注册中心 | 功能 | 技术基底 | 核心接口 |
| --- | --- | --- | --- |
| 🪪 Identity Registry | 提供代理唯一身份（Agent Identity） | ERC-721 + URIStorage | register(), _setTokenURI() |
| ⭐ Reputation Registry | 管理任务反馈与评分（Feedback & Scores） | 可链上或链下聚合 | giveFeedback(), getSummary() |
| 🔒 Validation Registry | 支持验证机制（验证执行、zkML、TEE等） | 可扩展验证协议 | validationRequest(), validationResponse() |

* * *

## 🧠 三、信任模型（Trust Models）

| 模型类型 | 机制 | 应用场景 |
| --- | --- | --- |
| 🧍‍♂️ Reputation-based | 客户端反馈评分系统 | 普通低风险任务（如订购服务） |
| 💰 Crypto-economic | 抵押金 + 再执行验证（stake & re-run） | 中等风险任务（审计、数据分析） |
| 🧬 zkML / TEE | 零知识验证或可信执行环境 | 高风险任务（医疗诊断、金融交易） |

> 三层信任模型可插拔且分层，风险越高 → 信任要求越强。

* * *

## 📡 四、代理注册文件结构（Registration JSON）

```
{
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "myAgentName",
  "description": "...",
  "image": "https://example.com/agent.png",
  "endpoints": [
    {"name": "A2A", "endpoint": "...", "version": "0.3.0"},
    {"name": "MCP", "endpoint": "...", "version": "2025-06-18"}
  ],
  "registrations": [
    {"agentId": 22, "agentRegistry": "eip155:1:{identityRegistry}"}
  ],
  "supportedTrust": ["reputation", "crypto-economic", "tee-attestation"]
}
```

**关键点：**

-   `tokenURI` 必须解析到上述结构；
    
-   端点可扩展（A2A、MCP、ENS、DID、Wallet等）；
    
-   支持多链注册（eip155 命名空间）。
    

* * *

## 🪙 五、反馈机制（Reputation Registry）

### 🔧 提交反馈

`giveFeedback(agentId, score, tag1, tag2, uri, hash, feedbackAuth)`

-   分数范围 0–100
    
-   `feedbackAuth` = 代理签名授权
    
-   可包含链下 JSON（IPFS），含任务、支付凭证 (x402 proof)
    

### 📊 查询与撤销

-   `getSummary()`：聚合得分
    
-   `revokeFeedback()`：撤销反馈
    
-   `appendResponse()`：代理追加说明或反驳
    

### 🧾 链下反馈文件示例

```
{
  "agentRegistry": "eip155:1:{registry}",
  "agentId": 22,
  "clientAddress": "...",
  "createdAt": "2025-09-23T12:00:00Z",
  "score": 100,
  "capability": "tools",
  "proof_of_payment": { "txHash": "0x..." }
}
```

* * *

## 🔍 六、验证机制（Validation Registry）

### 1️⃣ 发起验证请求

`validationRequest(validator, agentId, requestUri, requestHash)`

-   验证器类型可多样：re-run、zkML、TEE
    
-   `requestUri` 指向链下任务数据
    

### 2️⃣ 返回验证结果

`validationResponse(requestHash, response, responseUri, responseHash, tag)`

-   response ∈ \[0,100\]
    
-   可多次更新（例如软 / 硬最终性）
    

* * *

## 🪄 七、生态与扩展性

| 维度 | 实现机制 | 意义 |
| --- | --- | --- |
| 🧭 发现 | 任何兼容 ERC-721 的浏览器均可索引代理 | 构建“代理市场” |
| 🔄 声誉聚合 | 链上平均 + 链下复杂聚合 | 公共信号，可组合 |
| 🧠 验证 | zkML / TEE / stake | 安全性层次化 |
| ⛽ Gas 赞助 | 支持 EIP-7702 无摩擦反馈 | 用户体验优化 |
| 📡 跨链 | 同一代理可在多链操作 | 互操作性增强 |

* * *

## ⚙️ 八、安全与治理

-   公开声誉信号，防 Sybil 但仍需防女巫攻击；
    
-   不可删除链上指针与哈希，保证可审计性；
    
-   验证者激励与惩罚由各验证协议管理；
    
-   本 ERC 仅保证注册文件真实性，不保证功能安全。
    

* * *

## 📚 九、引用与版权

> Marco De Rossi（MetaMask）、Davide Crapis（Ethereum Foundation）、Jordan Ellis（Google）、Erik Reppel（Coinbase）  
> 《ERC-8004：Trustless Agents》，EIP-8004 草案，2025-08，CC0 公共领域
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## 一、核心目标：开放式、跨组织的代理经济（Agent Economy）

> **关键问题**：如何在**没有预先信任的环境中**发现、选择、验证 AI Agent？  
> **解决方案**：通过三类链上注册表（Registries）建立信任基础。

* * *

## 🧱 二、架构组成（3 Registries）

| 注册中心 | 功能 | 技术基底 | 核心接口 |
| --- | --- | --- | --- |
| 🪪 Identity Registry | 提供代理唯一身份（Agent Identity） | ERC-721 + URIStorage | register(), _setTokenURI() |
| ⭐ Reputation Registry | 管理任务反馈与评分（Feedback & Scores） | 可链上或链下聚合 | giveFeedback(), getSummary() |
| 🔒 Validation Registry | 支持验证机制（验证执行、zkML、TEE等） | 可扩展验证协议 | validationRequest(), validationResponse() |

* * *

## 🧠 三、信任模型（Trust Models）

| 模型类型 | 机制 | 应用场景 |
| --- | --- | --- |
| 🧍‍♂️ Reputation-based | 客户端反馈评分系统 | 普通低风险任务（如订购服务） |
| 💰 Crypto-economic | 抵押金 + 再执行验证（stake & re-run） | 中等风险任务（审计、数据分析） |
| 🧬 zkML / TEE | 零知识验证或可信执行环境 | 高风险任务（医疗诊断、金融交易） |

> 三层信任模型可插拔且分层，风险越高 → 信任要求越强。

* * *

## 📡 四、代理注册文件结构（Registration JSON）

```
{
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "myAgentName",
  "description": "...",
  "image": "https://example.com/agent.png",
  "endpoints": [
    {"name": "A2A", "endpoint": "...", "version": "0.3.0"},
    {"name": "MCP", "endpoint": "...", "version": "2025-06-18"}
  ],
  "registrations": [
    {"agentId": 22, "agentRegistry": "eip155:1:{identityRegistry}"}
  ],
  "supportedTrust": ["reputation", "crypto-economic", "tee-attestation"]
}
```

**关键点：**

-   `tokenURI` 必须解析到上述结构；
    
-   端点可扩展（A2A、MCP、ENS、DID、Wallet等）；
    
-   支持多链注册（eip155 命名空间）。
    

* * *

## 🪙 五、反馈机制（Reputation Registry）

### 🔧 提交反馈

`giveFeedback(agentId, score, tag1, tag2, uri, hash, feedbackAuth)`

-   分数范围 0–100
    
-   `feedbackAuth` = 代理签名授权
    
-   可包含链下 JSON（IPFS），含任务、支付凭证 (x402 proof)
    

### 📊 查询与撤销

-   `getSummary()`：聚合得分
    
-   `revokeFeedback()`：撤销反馈
    
-   `appendResponse()`：代理追加说明或反驳
    

### 🧾 链下反馈文件示例

```
{
  "agentRegistry": "eip155:1:{registry}",
  "agentId": 22,
  "clientAddress": "...",
  "createdAt": "2025-09-23T12:00:00Z",
  "score": 100,
  "capability": "tools",
  "proof_of_payment": { "txHash": "0x..." }
}
```

* * *

## 🔍 六、验证机制（Validation Registry）

### 1️⃣ 发起验证请求

`validationRequest(validator, agentId, requestUri, requestHash)`

-   验证器类型可多样：re-run、zkML、TEE
    
-   `requestUri` 指向链下任务数据
    

### 2️⃣ 返回验证结果

`validationResponse(requestHash, response, responseUri, responseHash, tag)`

-   response ∈ \[0,100\]
    
-   可多次更新（例如软 / 硬最终性）
    

* * *

## 🪄 七、生态与扩展性

| 维度 | 实现机制 | 意义 |
| --- | --- | --- |
| 🧭 发现 | 任何兼容 ERC-721 的浏览器均可索引代理 | 构建“代理市场” |
| 🔄 声誉聚合 | 链上平均 + 链下复杂聚合 | 公共信号，可组合 |
| 🧠 验证 | zkML / TEE / stake | 安全性层次化 |
| ⛽ Gas 赞助 | 支持 EIP-7702 无摩擦反馈 | 用户体验优化 |
| 📡 跨链 | 同一代理可在多链操作 | 互操作性增强 |

* * *

## ⚙️ 八、安全与治理

-   公开声誉信号，防 Sybil 但仍需防女巫攻击；
    
-   不可删除链上指针与哈希，保证可审计性；
    
-   验证者激励与惩罚由各验证协议管理；
    
-   本 ERC 仅保证注册文件真实性，不保证功能安全。
    

* * *

## 📚 九、引用与版权

> Marco De Rossi（MetaMask）、Davide Crapis（Ethereum Foundation）、Jordan Ellis（Google）、Erik Reppel（Coinbase）  
> 《ERC-8004：Trustless Agents》，EIP-8004 草案，2025-08，CC0 公共领域
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
