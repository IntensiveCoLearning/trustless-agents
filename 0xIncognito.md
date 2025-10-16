---
timezone: UTC+8
---

# 0xIncognito

**GitHub ID:** 0xIncognito

**Telegram:** @Real0xIncognito

## Self-introduction

Open to learn new techniques.

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
今天听了 ERC-8004 相关的 workshop 会议，稍微多了一些了解吧
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->



# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
## 摘要

该协议旨在利用区块链实现跨组织边界的代理（agent）发现、选择与交互，无需事先建立信任关系。

信任模型是可插拔且分层的，可根据任务价值设定不同安全级别。开发者可以选择三种信任模型：

\- 基于声誉（reputation）的系统

\- 基于质押与重新执行 / zkML / TEE oracles 的验证机制

\- TEE 认证

## 动机

现有代理通信协议（如 MCP、A2A）支持能力披露、消息传递与任务编排，但不内建代理发现与信任机制。

为实现开放的跨组织代理经济，本 ERC 提出三种轻量注册表（registries）：

\- 身份注册表（Identity Registry）

\- 声誉注册表（Reputation Registry）

\- 验证注册表（Validation Registry）

这些注册表可部署于任意 L2 或 Mainnet 作为链上单例。

### Identity Registry

\- 基于 **ERC-721 + URIStorage** 扩展，用作代理注册与身份标识。

\- 每个代理由一个唯一的 `agentId` 标识（对应 ERC-721 的 tokenId）。

\- `tokenURI` 指向代理注册文件（可以是 `ipfs://https://` 等 URI）。

\- 注册文件（JSON）结构范例：

\`\`\`json

{

“type”: “[https://eips.ethereum.org/EIPS/eip-8004#registration-v1](https://eips.ethereum.org/EIPS/eip-8004#registration-v1)”,

“name”: “myAgentName”,

“description”: “…”,

“image”: “…”,

“endpoints”: \[

{ “name”: “A2A”, “endpoint”: “…”, “version”: “0.3.0” },

{ “name”: “MCP”, “endpoint”: “…”, “version”: “2025-06-18” }

// … 可按需增补

\],

“registrations”: \[

{

“agentId”: 22,

“agentRegistry”: “eip155:1:{identityRegistry}”

}

\],

“supportedTrust”: \[

“reputation”,

“crypto-economic”,

“tee-attestation”

\]

}

-   注册与元数据更新接口包括 `register(...)`、`setMetadata(...)` 等。
    
-   还支持链上额外 metadata（如 `"agentWallet"`、`"agentName"` 等键值对）。
    

### **Reputation Registry**

-   部署时需传入对应的 `identityRegistry` 地址。
    
-   通过 `giveFeedback(...)` 接口提交声誉反馈，包含：
    
    -   `score`（0–100）
        
    -   可选标签 `tag1` / `tag2`
        
    -   可选指向离链 JSON 的 URI 与其哈希
        
    -   `feedbackAuth` 用于验证反馈授权
        
-   支持撤销反馈（`revokeFeedback(...)`）与响应（`appendResponse(...)`）。
    
-   读取接口如 `getSummary(...)`、`readFeedback(...)`、`readAllFeedback(...)` 等。
    
-   离链反馈文件示例结构（JSON）可含更多上下文、支付证明等字段。
    

### **Validation Registry**

-   允许代理提交验证请求（`validationRequest(...)`），并由验证者响应（`validationResponse(...)`）。
    
-   `response` 值在 0–100 间：可作为二值验证或阶段性验证结果。
    
-   支持多次响应（例如软终结性 / 强终结性机制）和带标签的验证。
    
-   查询接口包括 `getValidationStatus(...)`、`getSummary(...)`、`getAgentValidations(...)` 等。
    
-   与质押、惩罚机制相关的激励逻辑在具体验证协议中设计，不在该注册表范围之内。
    

## **Rationale**

-   **连接链上与链下**：注册文件允许代理灵活配置端点（MCP、A2A、ENS、DID、钱包地址等）。
    
-   **声誉信号既可链上聚合**（便于合约可组合性），**也可离线复杂计算**。
    
-   **支持 gas 补助机制**，使客户端无需注册也可提供反馈（参考 EIP-7702）。
    
-   **利于子图 / 索引器构建**，使代理发现与浏览体验更好。
    
-   **允许同一个代理在多个链上注册与运营**。
    

## **Test Cases & Use Cases**

-   从中心化入口开始爬取代理信息：名称、能力、端点、信任模型等。
    
-   构建代理市场、浏览器、探索器：可用标准 ERC-721 接口管理代理。
    
-   构建声誉系统：链上提供基础聚合，离线可进行复杂评分算法。
    
-   查询哪些代理支持验证、如何请求验证等操作。
    

## **Security Considerations**

-   虚假评价 / Sybil 攻击仍是风险，协议仅提供公开信号与基础过滤能力。
    
-   链上指针与哈希不可删除，保留审计轨迹。
    
-   协议不能保证能力与行为本身的正确性，需依赖三种信任模型机制。
    
-   验证者的激励 / 惩罚机制须由特定验证协议设计保障安全性。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## 摘要

该协议旨在利用区块链实现跨组织边界的代理（agent）发现、选择与交互，无需事先建立信任关系。

信任模型是可插拔且分层的，可根据任务价值设定不同安全级别。开发者可以选择三种信任模型：

\- 基于声誉（reputation）的系统

\- 基于质押与重新执行 / zkML / TEE oracles 的验证机制

\- TEE 认证

## 动机

现有代理通信协议（如 MCP、A2A）支持能力披露、消息传递与任务编排，但不内建代理发现与信任机制。

为实现开放的跨组织代理经济，本 ERC 提出三种轻量注册表（registries）：

\- 身份注册表（Identity Registry）

\- 声誉注册表（Reputation Registry）

\- 验证注册表（Validation Registry）

这些注册表可部署于任意 L2 或 Mainnet 作为链上单例。

### Identity Registry

\- 基于 **ERC-721 + URIStorage** 扩展，用作代理注册与身份标识。

\- 每个代理由一个唯一的 `agentId` 标识（对应 ERC-721 的 tokenId）。

\- `tokenURI` 指向代理注册文件（可以是 `ipfs://https://` 等 URI）。

\- 注册文件（JSON）结构范例：

\`\`\`json

{

“type”: “[https://eips.ethereum.org/EIPS/eip-8004#registration-v1](https://eips.ethereum.org/EIPS/eip-8004#registration-v1)”,

“name”: “myAgentName”,

“description”: “…”,

“image”: “…”,

“endpoints”: \[

{ “name”: “A2A”, “endpoint”: “…”, “version”: “0.3.0” },

{ “name”: “MCP”, “endpoint”: “…”, “version”: “2025-06-18” }

// … 可按需增补

\],

“registrations”: \[

{

“agentId”: 22,

“agentRegistry”: “eip155:1:{identityRegistry}”

}

\],

“supportedTrust”: \[

“reputation”,

“crypto-economic”,

“tee-attestation”

\]

}

-   注册与元数据更新接口包括 `register(...)`、`setMetadata(...)` 等。
    
-   还支持链上额外 metadata（如 `"agentWallet"`、`"agentName"` 等键值对）。
    

### **Reputation Registry**

-   部署时需传入对应的 `identityRegistry` 地址。
    
-   通过 `giveFeedback(...)` 接口提交声誉反馈，包含：
    
    -   `score`（0–100）
        
    -   可选标签 `tag1` / `tag2`
        
    -   可选指向离链 JSON 的 URI 与其哈希
        
    -   `feedbackAuth` 用于验证反馈授权
        
-   支持撤销反馈（`revokeFeedback(...)`）与响应（`appendResponse(...)`）。
    
-   读取接口如 `getSummary(...)`、`readFeedback(...)`、`readAllFeedback(...)` 等。
    
-   离链反馈文件示例结构（JSON）可含更多上下文、支付证明等字段。
    

### **Validation Registry**

-   允许代理提交验证请求（`validationRequest(...)`），并由验证者响应（`validationResponse(...)`）。
    
-   `response` 值在 0–100 间：可作为二值验证或阶段性验证结果。
    
-   支持多次响应（例如软终结性 / 强终结性机制）和带标签的验证。
    
-   查询接口包括 `getValidationStatus(...)`、`getSummary(...)`、`getAgentValidations(...)` 等。
    
-   与质押、惩罚机制相关的激励逻辑在具体验证协议中设计，不在该注册表范围之内。
    

## **Rationale**

-   **连接链上与链下**：注册文件允许代理灵活配置端点（MCP、A2A、ENS、DID、钱包地址等）。
    
-   **声誉信号既可链上聚合**（便于合约可组合性），**也可离线复杂计算**。
    
-   **支持 gas 补助机制**，使客户端无需注册也可提供反馈（参考 EIP-7702）。
    
-   **利于子图 / 索引器构建**，使代理发现与浏览体验更好。
    
-   **允许同一个代理在多个链上注册与运营**。
    

## **Test Cases & Use Cases**

-   从中心化入口开始爬取代理信息：名称、能力、端点、信任模型等。
    
-   构建代理市场、浏览器、探索器：可用标准 ERC-721 接口管理代理。
    
-   构建声誉系统：链上提供基础聚合，离线可进行复杂评分算法。
    
-   查询哪些代理支持验证、如何请求验证等操作。
    

## **Security Considerations**

-   虚假评价 / Sybil 攻击仍是风险，协议仅提供公开信号与基础过滤能力。
    
-   链上指针与哈希不可删除，保留审计轨迹。
    
-   协议不能保证能力与行为本身的正确性，需依赖三种信任模型机制。
    
-   验证者的激励 / 惩罚机制须由特定验证协议设计保障安全性。
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
