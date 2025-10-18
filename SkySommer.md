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
