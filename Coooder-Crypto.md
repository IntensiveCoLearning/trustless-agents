---
timezone: UTC+8
---

# Coooder

**GitHub ID:** Coooder-Crypto

**Telegram:** @Coooder_Crypto

## Self-introduction

很早就看到了这个 ERC，想仔细学习一下

## Notes
<!-- Content_START -->
# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
## **设计动机**

现有协议（如 **MCP** 和 **A2A**）分别解决了：

-   **MCP**：服务器功能（prompts、tools、resources、completions）注册与调用；
    
-   **A2A**：代理身份验证、技能展示（AgentCards）、消息通信和任务编排。
    

但它们缺乏\*\*“发现”与“信任”**机制。**

**ERC-8004 的目标是让代理能够在**不可信环境中自动发现并建立信任\*\*，从而实现跨组织、跨平台的协作。

* * *

## **核心设计**

ERC-8004 定义了 **三类注册表（Registries）**，每个都可以单独部署在任何 L2 或主网中，用于不同层面的信任构建：

| 注册表 | 功能 | 技术基础 |
| --- | --- | --- |
| 1. Identity Registry | 基于 ERC-721 的代理身份注册表，提供去中心化身份（Agent ID），每个代理拥有唯一 NFT 作为身份标识。 | ERC-721 + URIStorage |
| 2. Reputation Registry | 管理反馈与评分系统，允许客户端为代理打分、附加反馈文件（IPFS URI），构建链上可组合的信誉信号。 | On-chain feedback + 可选 off-chain 数据 |
| 3. Validation Registry | 记录第三方验证者的独立验证（如 stake-secured 复执行、zkML 证明或 TEE 审计），实现可追踪的验证记录。 | Validator smart contracts |

* * *

## **技术要点**

### **Identity Registry（身份注册）**

-   每个代理用 ERC-721 NFT 表示，tokenId 即 agentId。
    
-   Token URI 指向注册文件（可在 IPFS / HTTPS / ENS / DID 等路径）。
    
-   注册文件包含：
    
    -   基础信息：name、description、image
        
    -   交互端点（endpoints）：支持 MCP、A2A、OASF、ENS、DID、agentWallet 等
        
    -   支持的信任模型（supportedTrust）：reputation / crypto-economic / TEE attestation
        

### **Reputation Registry（信誉注册）**

-   客户端（人或其他 Agent）可对代理打分（0-100），并可添加标签（tag1, tag2）。
    
-   支持链上查询汇总（getSummary、readFeedback），便于组合使用。
    
-   支持撤销或补充反馈（revokeFeedback、appendResponse）。
    
-   建议使用 IPFS 存储详细反馈文件，链上仅保留索引与完整性哈希。
    
-   **安全措施**：代理需预先签署 feedbackAuth 以授权反馈者，防止伪造。
    

### **Validation Registry（验证注册）**

-   允许代理主动请求验证（validationRequest），由指定验证合约响应（validationResponse）。
    
-   验证可以采用：
    
    -   **Stake-secured 复执行**
        
    -   **zkML（零知识机器学习）验证**
        
    -   **TEE（可信执行环境）证明**
        
-   验证结果为 0–100，可多次更新（支持软/硬终结状态）。
    
-   提供查询函数（getValidationStatus、getSummary 等）用于追踪验证进度。
    

* * *

## **体系特征**

| 特征 | 说明 |
| --- | --- |
| 可插拔信任模型 | 支持信誉、验证、TEE 三种信任机制，可按风险级别选择。 |
| 链上身份统一性 | 所有代理的注册、信誉、验证都可跨平台查询、组合。 |
| 开放互操作性 | 与 MCP / A2A / ENS / DID 等生态兼容，可构建统一 Agent 发现层。 |
| 安全性 | 数据完整性通过哈希或内容寻址（IPFS）保证，记录不可篡改。 |
| 可扩展性 | 可部署于任何 L2 或主网，兼容单例合约设计。 |

* * *

## **应用场景示例**

-   **Agent 浏览与市场**：使用 ERC-721 兼容应用展示和交易代理身份。
    
-   **信誉系统与保险池**：基于公开反馈信号构建评分体系与风险控制。
    
-   **任务验证与仲裁**：通过 Validation Registry 结合 stake 或 zkML 实现可信验证。
    
-   **跨链 Agent 经济**：同一代理可在多链注册并共享信誉与验证记录。
    

* * *

## **安全考虑**

-   **Sybil 攻击**：仅通过预授权部分缓解，仍需外部信誉系统辅助。
    
-   **审计追踪性**：链上哈希与事件记录不可删除，确保溯源。
    
-   **验证责任分离**：验证激励与惩罚由各验证协议管理，不在本 ERC 范围内。
    
-   **功能真实性**：协议保证身份与注册文件一致，但不保证功能真实性，需依赖验证模型（reputation / zkML / TEE）。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## **设计动机**

现有协议（如 **MCP** 和 **A2A**）分别解决了：

-   **MCP**：服务器功能（prompts、tools、resources、completions）注册与调用；
    
-   **A2A**：代理身份验证、技能展示（AgentCards）、消息通信和任务编排。
    

但它们缺乏\*\*“发现”与“信任”**机制。**

**ERC-8004 的目标是让代理能够在**不可信环境中自动发现并建立信任\*\*，从而实现跨组织、跨平台的协作。

* * *

## **核心设计**

ERC-8004 定义了 **三类注册表（Registries）**，每个都可以单独部署在任何 L2 或主网中，用于不同层面的信任构建：

| 注册表 | 功能 | 技术基础 |
| --- | --- | --- |
| 1. Identity Registry | 基于 ERC-721 的代理身份注册表，提供去中心化身份（Agent ID），每个代理拥有唯一 NFT 作为身份标识。 | ERC-721 + URIStorage |
| 2. Reputation Registry | 管理反馈与评分系统，允许客户端为代理打分、附加反馈文件（IPFS URI），构建链上可组合的信誉信号。 | On-chain feedback + 可选 off-chain 数据 |
| 3. Validation Registry | 记录第三方验证者的独立验证（如 stake-secured 复执行、zkML 证明或 TEE 审计），实现可追踪的验证记录。 | Validator smart contracts |

* * *

## **技术要点**

### **Identity Registry（身份注册）**

-   每个代理用 ERC-721 NFT 表示，tokenId 即 agentId。
    
-   Token URI 指向注册文件（可在 IPFS / HTTPS / ENS / DID 等路径）。
    
-   注册文件包含：
    
    -   基础信息：name、description、image
        
    -   交互端点（endpoints）：支持 MCP、A2A、OASF、ENS、DID、agentWallet 等
        
    -   支持的信任模型（supportedTrust）：reputation / crypto-economic / TEE attestation
        

### **Reputation Registry（信誉注册）**

-   客户端（人或其他 Agent）可对代理打分（0-100），并可添加标签（tag1, tag2）。
    
-   支持链上查询汇总（getSummary、readFeedback），便于组合使用。
    
-   支持撤销或补充反馈（revokeFeedback、appendResponse）。
    
-   建议使用 IPFS 存储详细反馈文件，链上仅保留索引与完整性哈希。
    
-   **安全措施**：代理需预先签署 feedbackAuth 以授权反馈者，防止伪造。
    

### **Validation Registry（验证注册）**

-   允许代理主动请求验证（validationRequest），由指定验证合约响应（validationResponse）。
    
-   验证可以采用：
    
    -   **Stake-secured 复执行**
        
    -   **zkML（零知识机器学习）验证**
        
    -   **TEE（可信执行环境）证明**
        
-   验证结果为 0–100，可多次更新（支持软/硬终结状态）。
    
-   提供查询函数（getValidationStatus、getSummary 等）用于追踪验证进度。
    

* * *

## **体系特征**

| 特征 | 说明 |
| --- | --- |
| 可插拔信任模型 | 支持信誉、验证、TEE 三种信任机制，可按风险级别选择。 |
| 链上身份统一性 | 所有代理的注册、信誉、验证都可跨平台查询、组合。 |
| 开放互操作性 | 与 MCP / A2A / ENS / DID 等生态兼容，可构建统一 Agent 发现层。 |
| 安全性 | 数据完整性通过哈希或内容寻址（IPFS）保证，记录不可篡改。 |
| 可扩展性 | 可部署于任何 L2 或主网，兼容单例合约设计。 |

* * *

## **应用场景示例**

-   **Agent 浏览与市场**：使用 ERC-721 兼容应用展示和交易代理身份。
    
-   **信誉系统与保险池**：基于公开反馈信号构建评分体系与风险控制。
    
-   **任务验证与仲裁**：通过 Validation Registry 结合 stake 或 zkML 实现可信验证。
    
-   **跨链 Agent 经济**：同一代理可在多链注册并共享信誉与验证记录。
    

* * *

## **安全考虑**

-   **Sybil 攻击**：仅通过预授权部分缓解，仍需外部信誉系统辅助。
    
-   **审计追踪性**：链上哈希与事件记录不可删除，确保溯源。
    
-   **验证责任分离**：验证激励与惩罚由各验证协议管理，不在本 ERC 范围内。
    
-   **功能真实性**：协议保证身份与注册文件一致，但不保证功能真实性，需依赖验证模型（reputation / zkML / TEE）。
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
