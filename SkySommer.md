---
timezone: UTC+8
---

# Sky

**GitHub ID:** SkySommer

**Telegram:** @skysommer0317

## Self-introduction

Web3 PM and developer, LXDAO Designer, AI enthusiast.

## Notes
<!-- Content_START -->
# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->
**A2A (Agent-to-Agent)** 协议可以理解为一个为 AI 代理（Agent）之间进行**通信和协作而设计的标准化语言和规则**。

在我们讨论 ERC-8004 的语境下，您可以将 A2A 协议想象成 AI 代理们在互联网上互相“说话”和“协同工作”的基础设施，就像人类使用 HTTP 协议浏览网页一样。

### A2A 协议解决了什么问题？

在 A2A 出现之前，不同的 AI 代理（比如由谷歌、微软或苹果开发的不同智能助手）之间很难互相理解和协作。它们就像说不同语言的人，无法有效沟通。

A2A 协议旨在解决这个“沟通障碍”，它主要规范了以下几个方面：

1.  **能力发现 (Capability Discovery)**：一个代理如何向外界宣告“我能做什么？”。例如，一个代理可以通过标准格式的“**代理卡片 (Agent Card)**”来声明自己具备“市场分析”或“图片生成”等技能。
    
2.  **任务协商 (Task Negotiation)**：当一个代理（客户）需要另一个代理（服务商）完成一项任务时，它们如何就任务的具体要求、输入和输出格式达成一致。
    
3.  **数据交换**：代理之间如何使用标准化的数据格式（如 JSON-RPC 2.0）来交换信息和任务成果，确保双方都能正确解析。
    
4.  **任务生命周期管理**：如何管理一个任务从开始、执行到完成的整个过程。
    

### A2A 的局限性：信任鸿沟

A2A 协议非常成功地解决了 AI 代理之间的**技术沟通问题**，但它有一个核心的假设：**参与通信的代理之间是相互信任的**。

这在同一个公司或组织内部是行得通的，因为公司内部有IT部门可以建立信任关系。但当你想创建一个**开放的、全球性的代理经济**时，问题就来了：

-   一个来自A公司的代理，如何信任一个来自B公司的、素未谋面的代理？
    
-   我如何确定这个代理真的具备它所声称的能力？
    
-   如果我付费了，它提供的服务质量如何保证？
    

这就是 A2A 协议的\*\*“信任鸿沟”\*\*。

### ERC-8004 如何扩展 A2A

ERC-8004 正是为了解决 A2A 的信任鸿沟而诞生的。它并没有取代 A2A，而是作为 A2A 协议的一个**信任增强层**，将区块链的去中心化信任机制引入其中。

您可以这样理解它们的关系：

-   **A2A 协议**：负责代理之间的**通信**。它定义了代理如何“说话”。
    
-   **ERC-8004 协议**：负责代理之间的**信任**。它定义了如何验证对方“说的话”是可信的。
    

正如您上传的 `README.md` 和 `FRONTEND.md` 文件中所述，ERC-8004 **扩展了 A2A 协议**，它通过三大注册表（身份、声誉、验证）为 A2A 通信增加了链上锚点：

-   当一个代理通过 A2A 出示它的“代理卡片”时，你可以通过 ERC-8004 的**身份注册表**去验证这个身份是否真实存在于链上。
    
-   当一个代理通过 A2A 提供服务后，你可以通过 ERC-8004 的**验证注册表**查看它的工作成果是否被第三方独立验证过。
    
-   在与一个代理长期协作前，你可以通过 ERC-8004 的**声誉注册表**相关的链下系统，查询它的历史信誉。
    

### 总结

-   **A2A** 是一个让不同 AI 代理能够互相**沟通和理解**的通信标准。
    
-   它的主要缺陷是**假设参与者之间相互信任**，这限制了其在开放网络中的应用。
    
-   **ERC-8004** 通过引入区块链注册表，为 A2A 协议**增加了一个去中心化的信任层**，使得陌生代理之间无需预先信任即可进行安全的发现、验证和协作，为真正的“代理经济”奠定了基础。
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->

ERC-8004 的运作流程可以理解为一个**链上和链下协同工作**的完整生命周期，旨在为 AI 代理（Agent）之间的交互建立可信的记录。这个流程的核心思想是：**复杂的计算和任务在链下高效执行，而关键的信任锚点（如身份、工作证明、验证结果和反馈授权）则被永久记录在链上**，从而实现无需信任的协作。

根据 `demo.py` 脚本中的示例，将整个流程分解为以下几个关键步骤：

* * *

### 第 1 步：基础设施部署（准备阶段）

在任何代理交互之前，必须先在区块链上部署 ERC-8004 的核心基础设施。

-   **动作**：通过 `deploy.py` 脚本，将三个核心的智能合约部署到链上：
    
    1.  `IdentityRegistry.sol`：身份注册表。
        
    2.  `ReputationRegistry.sol`：声誉注册表。
        
    3.  `ValidationRegistry.sol`：验证注册表。
        
-   **目的**：为所有未来的 AI 代理交互创建一个公共、可信的底层账本。
    

### 第 2 步：代理身份注册（获取链上“身份证”）

每个想要参与这个生态的 AI 代理，首先需要一个公开可验证的身份。

-   **动作**：
    
    -   AI 代理（例如，服务提供者 Alice）在链下被初始化，拥有自己的钱包地址。
        
    -   代理调用 `IdentityRegistry` 合约的 `newAgent` 函数，将自己的钱包地址和域名等信息上链，以换取一个独一无二的 `agentId`。
        
-   **目的**：使代理的身份在链上可被发现和验证，这是所有后续信任活动的基础。
    

### 第 3 步：执行任务与请求验证（“我完成了工作，求见证”）

当服务代理（Alice）完成一项任务后，它需要一种方式来证明其工作成果的质量。

-   **动作**：
    
    1.  **链下执行**：Alice 在链下执行复杂的 AI 任务，例如进行一次详细的市场分析。
        
    2.  **链上请求**：Alice 计算分析报告内容的哈希值（`dataHash`），然后调用 `ValidationRegistry` 合约的 `validationRequest` 函数，将这个哈希和她指定的验证者代理（Bob）的 `agentId` 一同提交上链。
        
-   **目的**：创建一个公开的、不可篡改的验证请求，将链下的工作成果与一个链上凭证锚定。
    

### 第 4 步：执行验证并提交响应（“我已验证，结果如下”）

验证者代理（Bob）响应请求，对工作进行评估。

-   **动作**：
    
    1.  **链下验证**：Bob 监听到链上的验证请求后，从 Alice 那里获取完整的分析报告（通过 IPFS 或其他方式），并使用自己的 AI 模型进行评估，最终给出一个分数。
        
    2.  **链上响应**：Bob 调用 `ValidationRegistry` 合约的 `validationResponse` 函数，将原始的 `dataHash` 和他给出的验证分数提交上链。
        
-   **目的**：将工作的质量评估结果永久记录在链上，完成信任闭环。
    

### 第 5 步：授权反馈（建立声誉）

为了长期建立声誉，服务代理需要客户的反馈。

-   **动作**：服务代理（Alice）调用 `ReputationRegistry` 合约的 `acceptFeedback` 函数，授权客户代理（Charlie）为本次服务提供反馈。
    
-   **目的**：在链上创建一个“许可证明”，表明服务方愿意接受监督和评价，这是声誉系统运作的前提。
    

### 最终成果：一个完整的链上审计轨迹

当以上所有流程走完后，一个关于 AI 代理交互的、完整且不可篡改的**审计轨迹**就形成了。任何人都可以通过查询区块链来验证：

-   **谁**参与了交互（身份）。
    
-   **做了什么**工作（通过验证请求的哈希）。
    
-   工作**质量如何**（验证结果）。
    
-   服务方是否**接受评价**（反馈授权）。
    

这个流程优雅地解决了在去中心化世界中如何信任和评估 AI 服务的问题，为构建一个庞大的、无需许可的代理经济奠定了基础。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->


### **Learning Report on ERC-8004: The Agentic Economy**

* * *

**1\. Core Concept: What is ERC-8004?**

ERC-8004 is an Ethereum standard designed for AI Agents, with the core objective of establishing a **trustless "trust layer"** for interactions between agents across different, untrusted organizational boundaries. While collaborations in current AI applications are often confined to closed or centralized systems, ERC-8004 addresses the key challenge of how AI agents can discover each other, verify the quality of their work, and build reputations in an open network.

The standard aims to foster an open and transparent "Agentic Economy," where AI agents can act as independent economic participants, autonomously providing services, collaborating, and earning credibility.

**2\. Key Protocol Components: The Three Core Registries**

The infrastructure of ERC-8004 is built upon three core smart contract registries, which work together to form a complete trust lifecycle.

-   **Identity Registry**:
    
    -   **Purpose**: To provide each AI agent with a unique, censorship-resistant on-chain identity (`agentId`).
        
    -   **How it Works**: An agent registers by mapping its domain (`agentDomain`) and wallet address (`agentAddress`) to a globally unique ID, creating a queryable "yellow pages" for agents.
        
-   **Reputation Registry**:
    
    -   **Purpose**: To establish a lightweight, on-chain mechanism for authorizing feedback.
        
    -   **How it Works**: Instead of storing costly reputation scores on-chain, it allows a server agent to authorize a client agent to provide feedback. This "authorization" event is recorded on-chain, while the actual reputation scoring and aggregation are left to off-chain services, balancing trust with flexibility.
        
-   **Validation Registry**:
    
    -   **Purpose**: To provide a generic, auditable workflow for work verification.
        
    -   **How it Works**: After completing a task, a server agent can submit a hash of its work to the chain and assign a validator agent. The validator, after reviewing the work, submits the result (e.g., a score) on-chain. This provides a decentralized proof of quality for complex AI tasks.
        

**3\. Key Roles: What is an "AI Agent"?**

In this project, an "AI Agent" is a composite concept, more than just a large language model. It is an **off-chain computational entity with an on-chain identity, capable of autonomously performing specialized tasks.**

-   **Technically**: It is powered by an AI framework (like `CrewAI`) and is assigned a clear role (e.g., Market Analyst), executable tools, and specific workflows.
    
-   **Economically**: Through the `ERC8004BaseAgent` class, each agent has its own wallet private key and on-chain identity, enabling it to independently sign transactions and participate in on-chain economic activities.
    

**4\. Practical Application: A Complete Workflow**

By analyzing the `demo.py` script, the application flow of ERC-8004 becomes clear:

1.  **Registration**: A Server Agent (Alice), a Validator Agent (Bob), and a Client Agent (Charlie) register on the `IdentityRegistry` to obtain their on-chain identities.
    
2.  **Execution**: Alice performs a complex AI task off-chain (e.g., market analysis).
    
3.  **Validation**: Alice submits a hash of her work to the `ValidationRegistry`, requesting validation from Bob. Bob validates the work and submits a score back on-chain.
    
4.  **Feedback**: Alice authorizes Charlie on the `ReputationRegistry` to provide feedback for the service rendered.
    
5.  **Audit**: All critical steps leave an immutable record on the blockchain, creating a complete trail of trust and auditability.
    

**5\. Conclusion & Insights**

The ERC-8004 protocol, by combining complex off-chain AI computation with lightweight on-chain trust records, provides an elegant and practical framework for building decentralized AI applications and service marketplaces. It not only solves the trust problem between AI agents but also offers standardized solutions for **proof-of-work, quality assessment, and reputation building**. For developers looking to build decentralized AI platforms, this protocol provides a modular and ready-to-use infrastructure, marking a significant milestone on the path toward the future "Agentic Economy."
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
