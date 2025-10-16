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
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
## **论坛观点立场**

大家普遍认同 ERC-8004 的核心目标，但争议焦点集中在：**哪些数据应上链、如何平衡开销与可组合性、以及信任与支付之间的边界。**

### **On-chain vs Off-chain 的设计取舍**

-   **spengrah 等人认为：**
    
    ERC 目前过于偏向 off-chain 读取（依赖事件 logs），导致其他智能合约难以直接读取验证结果或反馈。
    
    建议保留部分核心字段（如评分、验证响应）在链上，使得**其他协议能基于这些数据进行组合（composability）**，例如自动化的质押、托管或惩罚逻辑。
    
-   **Marco-MetaMask（作者）回应：**
    
    设计上刻意保持轻量以降低 gas 成本，但欢迎增加可选接口或扩展 ERC 以支持 on-chain 读取。
    

### **声誉（Reputation）系统的结构**

-   **felixnorden：** 建议允许多个声誉提供者并行，为同一代理提供不同评分，形成聚合式声誉体系以避免偏见。
    
-   **daniel-ospina：** 反对单一聚合评分，认为信任应是**上下文相关的向量**而非全局数值。压缩为单一指标容易造成垄断或歧视，应保持模块化与多源输入。
    
-   **sbacha：** 提醒 RFC 7071 (“Reputons”) 曾定义过声誉数据交换标准，可参考其思路。
    

### **验证（Validation）与托管支付（Escrow）的结合**

-   多人提出希望将验证结果用于托管释放条件：
    
    当某任务通过验证（如多方投票、TEE 证明等）时，自动释放 escrow。
    
-   **mlegls 提供实例：**
    
    Alice 购买 Bob 的任务，可约定多种验证条件触发付款（投票、TEE、超时仲裁等）。
    
    建议 ERC 增加任务标识符（taskId）以便在上链前可引用任务，提升自动化托管适配性。
    
-   **Marco-MetaMask 与 gpt3\_eth：**
    
    认为支付应留在应用层，但 ERC 应允许\*\*反馈记录引用支付凭证（payment proof）\*\*以便索引。
    

### **身份（Identity）与域名绑定**

-   **pcarranzav：** 质疑 ERC 要求每个 Agent 必须在独立域名下注册，限制灵活性。建议改为 URL 级别。
    
    同时提出：合约如何验证域名所有权？可能需 zkTLS 或共识机制。
    
-   **Marco-MetaMask 回应：**
    
    当前方案要求每个代理使用子域名，并在未来版本中明确接口与数据类型。
    
    同时计划每条链仅有一个 singleton registry。
<!-- DAILY_CHECKIN_2025-10-16_END -->

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

# 2025-10-15
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
