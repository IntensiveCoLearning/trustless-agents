---
timezone: UTC+8
---

# li

**GitHub ID:** xuruohan709-glitch

**Telegram:** @li

## Self-introduction

学习!

## Notes
<!-- Content_START -->
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
Here’s a concise summary you can use:

* * *

### **A2A (Agent-to-Agent) Protocol Summary**

**A2A** is a standardized protocol that enables **secure, interoperable communication between AI agents**, regardless of their framework or platform. It allows agents to collaborate seamlessly while maintaining autonomy and protecting proprietary logic.

**Key Benefits**

-   **Secure collaboration:** Uses HTTPS and opaque operations for privacy.
    
-   **Interoperability:** Connects agents across different ecosystems.
    
-   **Autonomy:** Agents retain their own reasoning and capabilities.
    
-   **Simplified integration:** Reduces custom connection work.
    
-   **Supports long operations:** Handles streaming and asynchronous tasks.
    

**Design Principles**

-   Built on familiar web standards (HTTP, JSON-RPC, SSE).
    
-   Enterprise-ready with authentication, tracing, and monitoring.
    
-   Asynchronous and modality-independent (works beyond text).
    
-   Opaque execution ensures IP and data protection.
    

**Place in the AI Stack**

-   **A2A:** Standardizes agent-to-agent communication.
    
-   **MCP (Model Context Protocol):** Connects models to tools and data.
    
-   **Frameworks (e.g., ADK, LangGraph):** Build and manage agents.
    
-   **Models (LLMs):** Perform reasoning and generation.
    

**A2A vs MCP**

-   **A2A** focuses on **multi-agent collaboration**.
    
-   **MCP** focuses on **connecting models with tools and data**.  
    They complement each other in the AI ecosystem.
    

**Lifecycle Overview**

1.  Agent discovery
    
2.  Authentication
    
3.  API communication
    
4.  Long-running or streaming operations
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->

1.  初始化代理并将其注册到身份注册表。有 3 种类型的代理。客户端代理将任务分配给服务器代理并提供反馈。服务器代理接受任务和反馈。验证器代理利用不同的信任模型验证任务。
    
2.  客户端代理通过读取代理卡来发现服务器代理，然后协商作业输出。这种谈判是在链下完成的。
    
3.  当服务器代理接受作业请求时，它还会在任务完成后接受来自客户端代理的反馈。
    
4.  服务器代理执行任务并发布数据哈希，该数据哈希提交重新运行作业所需的所有信息。
    
5.  然后，服务器代理还通过 _请求验证。_`ValidationRequest`
    
6.  验证器代理监视这些请求，并使用加密经济安全或加密验证进行验证。
    
7.  如果验证成功，验证器代理会以 **_._**`ValidationResponse`
    
8.  通过 ，这种无需信任的设置可确保正确执行各种服务的付款可以从托管中释放。`ValidationResponse`
    
9.  看到验证后，客户端代理会发布一个反馈证明，其中嵌入了数据哈希、参与者、8004 请求/响应 ID，从而允许结果可查询。
    
10.  ERC-8004 中不考虑支付、归因、激励、削减，为任务执行期间和执行后的设计灵活性留出了空间。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


### **一、协议核心目标与信任模型**

该协议旨在弥补现有 MCP 和 A2A 代理通信协议的不足，在无预先信任的环境中，让代理能跨组织边界被发现、选择并交互。

1.  **信任模型设计**：采用可插拔、分层模式，安全性与任务风险挂钩（如低风险披萨订购 vs 高风险医疗诊断）。
    
2.  **三类可选信任模型**：
    
    -   基于客户端反馈的声誉系统
        
    -   依托权益安全的重新执行验证
        
    -   基于 zkML 证明或 TEE 预言机的技术验证
        

* * *

### **二、三大核心注册表详解**

协议通过三个可部署在任意 L2 或主网的 “每链单例” 注册表，实现核心功能。

**1\. 身份注册表（Identity Registry）**

-   **核心作用**：为每个代理提供唯一、可移植、抗审查的链上身份。
    
-   **技术基础**：基于 ERC-721 标准，扩展 URIStorage 功能，每个代理对应一个 ERC-721 代币（tokenId 即 agentId）。
    
-   **关键信息**：
    
    -   代理身份由 “命名空间（eip155）+chainId + 注册表地址 + agentId” 唯一标识。
        
    -   tokenURI 需解析为包含代理名称、描述、图像、通信端点（MCP/A2A/ENS 等）、支持信任模型的注册文件。
        
    -   扩展链上元数据功能，可通过`getMetadata`和`setMetadata`函数读写代理额外信息（如钱包地址）。
        

**2\. 信誉注册表（Reputation Registry）**

-   **核心作用**：提供标准化接口，用于发布和获取代理的反馈信号，构建代理声誉体系。
    
-   **反馈机制**：
    
    -   客户端需凭代理预授权的`feedbackAuth`（符合 EIP-191/ERC-1271）提交反馈，内容包括 0-100 分的分数、标签、可选的链下详细文件及哈希。
        
    -   支持反馈和追加回应，所有操作均会触发对应链上事件。
        
-   **数据查询**：提供`getSummary`、`readFeedback`等函数，支持按客户端、标签过滤，链上可做简单聚合（如平均分），复杂分析需在链下完成。
    

**3\. 验证注册表（Validation Registry）**

-   **核心作用**：为代理提供工作验证的标准化接口，支持验证者提交验证结果，增强代理可信度。
    
-   **核心流程**：
    
    -   **验证请求**：代理所有者 / 操作员调用`validationRequest`，指定验证者地址、请求 URI（含验证所需数据）及可选哈希，触发`ValidationRequest`事件。
        
    -   **验证响应**：指定验证者调用`validationResponse`，返回 0-100 分的验证结果（可表示通过 / 失败或中间状态）、可选的结果 URI 及标签，触发`ValidationResponse`事件。
        
-   **数据查询**：提供`getValidationStatus`、`getSummary`等函数，支持查询代理的验证记录与统计数据。
    

* * *

### **三、协议补充说明**

1.  **支付相关**：协议不涉及支付逻辑，但支持结合 x402 付款证明丰富反馈信号。
    
2.  **部署与兼容性**：
    
    -   注册表建议按 “每链单例” 部署，代理可在多链注册，且在 A 链注册的代理可在其他链交互。
        
    -   基于 ERC-721 标准，兼容所有 ERC-721 应用，可用于构建代理浏览器、市场等。
        
3.  **安全注意事项**：
    
    -   反馈预授权仅部分防垃圾邮件，仍需应对女巫攻击，需依赖第三方声誉系统按审阅者过滤。
        
    -   链上指针与哈希不可删除，确保审计跟踪完整，但无法保证代理宣传功能真实非恶意。
        
    -   验证者的激励与惩罚由具体验证协议管理，不在本 ERC 范围内。
        

* * *

### **四、协议支持的关键场景**

1.  抓取代理信息：从指定端点获取代理的基础信息、功能、通信方式及支持的信任模型。
    
2.  构建生态工具：利用 ERC-721 兼容性，开发代理浏览器、市场，实现代理的浏览、传输与管理。
    
3.  搭建声誉体系：通过链上简单聚合或链下复杂分析，生成代理声誉数据（公共产品属性）。
    
4.  筛选与验证代理：快速识别支持权益安全 /zkML 验证的代理，并通过标准化接口发起验证请求。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
