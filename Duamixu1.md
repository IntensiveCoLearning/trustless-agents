---
timezone: UTC+8
---

# Duami

**GitHub ID:** Duamixu1

**Telegram:** @Duamieee

## Self-introduction

AI enthusiast and Web3 beginner, I’ve already competed in several hackathons—now I’m eager to fuse these two exciting worlds.

## Notes
<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
### 1\. **Understanding A2A, AP2, and x402 Demos**

-   **A2A (Application-to-Application) and AP2**: These could involve establishing connections between different applications or services within a decentralized ecosystem. The challenge is understanding the protocols and data exchange mechanisms that enable these connections to work seamlessly.
    
-   **x402 Demo**: It likely involves payment integration (based on the previous context about x402), which could add complexity due to the need to handle on-chain transactions, smart contracts, or payment processing workflows securely.
    

**Core challenge**: Decentralized systems can be difficult to debug because of their distributed nature. Tracking down where a problem originates—whether it’s a smart contract issue, a networking problem, or an application logic bug—can be time-consuming.

### 2\. **Integrating Web3 Concepts into a Demo Application**

-   Building a demo agent involves not just writing the code, but also understanding how to interact with decentralized networks, smart contracts, wallets (e.g., MetaMask), and APIs.
    
-   Depending on the demo's complexity, you may need to learn about different Web3 components like gas fees, transaction confirmation, and handling asynchronous operations within a blockchain environment.
    

**Core challenge**: The core issue here is getting the right Web3 libraries (e.g., Web3.js, Ethers.js) working in your project and ensuring that everything interacts smoothly. You need to be aware of specific quirks related to blockchain network congestion, wallet compatibility, and user experience.

### 3\. **Implementing Secure Payment Mechanisms (x402)**

-   If x402 is a payment mechanism, ensuring security and reliability in transactions is critical. Handling the interaction with crypto wallets, ensuring that payments are correctly authenticated and verified, and dealing with transaction fees or blockchain network delays could all add significant complexity.
    
-   Payments usually involve real-time processing and might need to handle state changes (i.e., the user's balance before/after transaction).
    

**Core challenge**: The difficulty here lies in ensuring that payment flows are secure and smooth, even when the underlying blockchain network has potential delays or higher-than-expected gas fees. Writing a function that tracks the payment state, verifies completion, and provides user feedback could be tricky.

### 4\. **Balancing Demo Completion with Review Time**

-   **Task review and review notes**: You’ll need to balance between coding the demo agents and reviewing your understanding of the material. This involves a mix of both practical coding and theoretical understanding.
    
-   Reviewing could involve revisiting the documentation and re-reading previous code to ensure you’ve absorbed key principles like smart contract development, Web3 APIs, or decentralized finance (DeFi) patterns.
    

**Core challenge**: Time management and transitioning between practical coding and theoretical review might slow down progress, especially if you’re trying to implement complex interactions while ensuring you've understood the foundational concepts.

### 5\. **Core Functions to Implement**

-   **Demo Agent Creation**: Depending on the Web3 platform (e.g., Ethereum, Solana, Polkadot), you’ll need to create demo agents that interact with the blockchain. For instance, the agents might handle interactions like wallet connection, transaction requests, or querying blockchain data.
    
-   **Core Functionality Example**:
    
    -   For `A2A` (Application-to-Application) integration, functions would involve securely passing data between decentralized applications.
        
    -   For `x402`, you might need a core function to interact with the payment API, something like:
        
    
    ```
    async function initiatePayment(amount, userAddress) {
        try {
            const transaction = await web3.eth.sendTransaction({
                from: userAddress,
                to: recipientAddress,
                value: web3.utils.toWei(amount, 'ether'),
            });
            console.log('Payment successful:', transaction);
        } catch (error) {
            console.error('Payment failed:', error);
        }
    }
    ```
    

**Core challenge**: Ensuring that these functions handle edge cases such as insufficient funds, network issues, or failed transactions and integrate seamlessly with the demo.

### Summary of Challenges:

1.  Understanding and implementing A2A, AP2, and x402 interactions.
    
2.  Integrating decentralized and secure payment mechanisms.
    
3.  Managing the complexity of decentralized environments (e.g., delays, wallet compatibility, etc.).
    
4.  Ensuring smooth communication between different parts of the Web3 ecosystem (wallets, smart contracts, APIs).
    
5.  Balancing demo implementation with review time and ensuring you understand all concepts.
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->

在完成 "Quickstart for Buyers" 文档中提到的任务时，以下是一些可能的难点和易错点：

### 难点：

1.  **钱包客户端的创建**：
    
    -   创建钱包客户端并集成到项目中可能会遇到配置环境变量（如API密钥、钱包密钥）的难度。你需要确保所有密钥正确存储，并且在代码中正确引用。例如，CDP API 密钥、钱包密钥等，如果这些配置不当，可能导致无法正确创建钱包客户端。
        
    -   使用 `dotenv` 来加载环境变量时，忘记将 `.env` 文件添加到项目根目录，或者环境变量名称拼写错误，可能导致加载失败。
        
2.  **安装依赖和配置环境**：
    
    -   安装 `x402` 相关的依赖包时，可能会遇到不同版本的兼容性问题，特别是如果你使用的是不同版本的 Node.js 或 Python，可能会遇到包无法正确安装或启动的情况。
        
    -   确保选择正确的客户端库（如 `x402-axios` 或 `x402-fetch`）。如果你在使用 `x402-axios`，而不小心使用了 `x402-fetch`，可能会导致功能不兼容。
        
3.  **支付流程的自动处理**：
    
    -   自动处理 402 响应和支付请求时，可能会有请求头信息的生成和验证的问题。如果支付请求头 (`payment header`) 生成不正确或响应未被正确处理，支付过程将无法继续。
        
    -   使用 `wrapFetchWithPayment` 或 `withPaymentInterceptor` 时，传递的参数（如 `account` 对象）必须正确无误，否则会出现认证失败或支付验证失败的情况。
        
4.  **服务发现（x402 Bazaar）**：
    
    -   使用 x402 Bazaar 动态发现服务时，需要了解如何正确调用 `list()` 方法，并解析返回的服务列表。如果配置不当，可能导致无法动态发现服务或请求失败。
        

### 易错点：

1.  **环境变量的配置问题**：
    
    -   确保 API 密钥和钱包密钥在 `.env` 文件中配置正确，并且没有忘记在代码中加载环境变量。
        
    -   注意确保密钥信息不会被硬编码到代码中，避免安全风险。
        
2.  **API 请求时的 URL 和端点路径错误**：
    
    -   在发起请求时，确认请求的 URL 和端点路径是正确的。如果路径错误，服务器会返回 404 或其他错误响应。
        
3.  **忘记处理 402 错误响应**：
    
    -   402 响应需要特别处理，如果没有处理这类错误，可能导致支付流程中断，导致请求无法继续。
        
4.  **支付响应头的解码问题**：
    
    -   在处理响应时，忘记调用 `decodeXPaymentResponse` 解析支付响应头，可能无法提取支付的详细信息，导致后续操作失败。
        
5.  **客户端库的选择和使用错误**：
    
    -   `x402-axios` 和 `x402-fetch` 都有不同的实现方式，使用时需要根据项目的实际需求来选择。比如，`x402-axios` 适用于 Axios 请求，`x402-fetch` 则适用于原生 `fetch` API。
        

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/Duamixu1/images/2025-10-20-1760966810179-image.png)
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->


**1\. 核心定义：AP2 是什么？**

AP2 是一个由谷歌、支付和技术公司（超过60家，包括万事达、Visa、PayPal、Coinbase、Salesforce 等）共同开发的**开放协议**。

它的核心目的很明确：为 **AI 代理 (Agent) 代表用户**发起的支付和交易，提供一个安全、标准化的框架。

**关键关系：**

-   AP2 不是一个孤立的协议。
    
-   它是我们之前学习的 **A2A（Agent-to-Agent）协议**和 **MCP（Model Context Protocol）** 的**扩展**。
    

**我的理解：** 如果说 A2A 是让代理们可以相互“对话”的通信层，MCP 是让代理可以调用“工具”的执行层，那么 **AP2 就是让代理们可以相互“交易”的商业和支付层**。这三者共同构成了 AI 代理经济的技术基石。

* * *

**2\. 解决的核心问题：为什么现在需要 AP2？**

现有的支付系统有一个**根本假设**：屏幕背后总有一个**人类**在点击“确认购买”按钮。

**AI 代理打破了这一假设。** 一个自主的 AI 代理可以代表你执行任务并支付，这带来了三个致命的信任问题（我称之为“3A”问题）：

1.  **授权 (Authorization):** 商家如何知道是_你_（用户）授权这个代理进行这笔特定购买的？
    
2.  **真实性 (Authenticity):** 商家如何确定代理的购买请求，_准确_反映了用户的真实意图？
    
3.  **问责 (Accountability):** 如果发生欺诈或错误的交易，_谁_应该为此负责？
    

AP2 的目标就是为代理、商家和支付提供商提供一种“通用语言”，在不依赖人类实时点击的情况下，解决上述三个问题。

* * *

**3\. 工作原理：“授权指令 (Mandates)”**

这是 AP2 的技术核心。它不依赖于信任代理本身，而是依赖于**可验证的、加密签名的用户指令**。

这个核心工具叫做 **Mandate (授权指令)**。

-   **它是什么？** 一个防篡改的、经过**加密签名**的数字合同。
    
-   **它证明了什么？** 它是用户指示的**可验证证明 (verifiable proof)**。
    
-   **它如何签名？** 通过**可验证凭证 (Verifiable Credentials, VCs)** 进行签名。
    

AP2 通过这个机制，为每笔交易创建了一个**不可否认的审计追踪链**。

**两种核心场景：**

**场景一：实时购买 (有人在场)**

1.  **你：** “帮我找一双新的白色跑鞋。”
    
2.  **系统：** 你的请求被捕获，生成一个\*\*`意图指令 (Intent Mandate)`\*\*。这为整个互动提供了可审计的上下文。
    
3.  **代理：** 展示了购物车（鞋子和价格）。
    
4.  **你：** 点击“批准”。
    
5.  **系统：** 你的批准签署了一个\*\*`购物车指令 (Cart Mandate)`**。这是一个**不可更改的安全记录\*\*，锁定了确切的商品和价格。
    

**场景二：委托任务 (无人看管)**

1.  **你：** “演唱会门票一开始销售，就帮我抢，价格不超过 200 美元。”
    
2.  **系统：** 你预先签署了一个详细的\*\*`意图指令 (Intent Mandate)`\*\*，其中包含了所有规则（价格限制、时间、条件）。
    
3.  **代理：** 监控票务情况。
    
4.  **系统：** 当你的精确条件（例如：门票开售，价格为 180 美元）被满足时，代理可以使用你预先签署的 `意图指令` 作为“预授权证明”，**自动生成并签署**`购物车指令 (Cart Mandate)`**。**
    

**最终结果：** 无论是哪种场景，最终都形成了一个清晰的证据链：`意图指令` -> `购物车指令` -> `支付环节`。这个链条完美地回答了“授权、真实性、问责”这三个问题。

* * *

**4\. 解锁的新商业体验**

AP2 不只是为了安全，更是为了实现全新的 AI 商业模式：

1.  **智能购物（委托）：**
    
    -   **用户：** “我想要这件绿色夹克，但现在没货。如果补货了，并且价格不超过 200 美元，就自动帮我买了。”
        
    -   **AP2 作用：** 代理根据预先签署的 `意图指令` 自动执行购买，商家捕获了否则会流失的销售。
        
2.  **个性化优惠（A2A 协商）：**
    
    -   **用户代理：** “我的主人需要一辆自行车用于下周的旅行。” (A2A 消息)
        
    -   **商家代理：** “收到。我这里有一个定制的、限时的打包优惠：自行车 + 头盔 + 旅行架，打 85 折。” (A2A 回复)
        
    -   **AP2 作用：** 两个代理通过 A2A 协商，并通过 AP2 完成一个动态生成的、个性化的交易。
        
3.  **协同任务（多代理）：**
    
    -   **用户：** “帮我预订 11 月第一个周末去 Palm Springs 的往返机票和酒店，总预算 700 美元。”
        
    -   **AP2 作用：** 用户的代理与多个航空代理、酒店代理进行协商。一旦找到符合预算的组合，它可以**同时执行**两个（或多个）经过加密签署的预订 (`购物车指令`)。
        

* * *

**5\. 对 Web3 和加密支付的支持**

AP2 被设计为“通用协议”，不局限于传统支付（信用卡、银行转账）。

-   它明确支持**稳定币**和**加密货币**。
    
-   **重量级发布：** 谷歌已与 Coinbase、以太坊基金会、MetaMask 合作，推出了 `A2A x402 扩展`。
    
-   `x402 扩展` 是一个**生产就绪的解决方案**，专门用于基于代理的**加密支付**。
    

* * *

**6\. 我的思考与下一步**

-   **AP2 是 AI 经济的“变现层”：** 如果说 A2A 是信息高速公路，AP2 就是这条路上的收费站、银行和交易市场。它解决了 AI 代理如何参与经济活动的核心问题。
    
-   **信任的转移：** 信任的核心从“相信 AI 代理的代码不会作恶”转移到了“**验证用户签署的加密指令**”。这是从“基于代码的信任”向“基于密码学的信任”的巨大转变。
    
-   **B2B 的巨大潜力：** 公告中提到了 B2B 应用（例如，通过 Google Cloud Marketplace 自主采购、根据实时需求自动扩展软件许可证）。这可能比消费者购物的市场更大，AI 代理将成为企业的“自动采购员”和“财务官”。
    
-   **下一步：**
    
    1.  密切关注 **GitHub 仓库**，查看技术规范和参考实现。
        
    2.  关注“**AI 代理市场 (AI Agent Marketplace)**”，看第一批支持 AP2 的“可交易代理”何时出现。
        

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/Duamixu1/images/2025-10-19-1760840613952-image.png)![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/Duamixu1/images/2025-10-19-1760840621570-image.png)

### **学习笔记：AP2 (代理支付协议) 的安全框架**

本文是一篇关于 AP2 的**安全分析**。它不再仅仅介绍 AP2 _是什么_，而是深入探讨了它_如何_在 AI 代理自主交易的复杂环境中建立信任，并详细分析了它面临的威胁和具体的防御策略。

**1\. 核心安全目标：解决“3A”信任鸿沟**

传统支付假设“人”在操作。AI 代理打破了这一点，AP2 的核心安全目标就是为了解决由此产生的三个关键问题：

1.  **授权 (Authorization) 差距：** 如何在不暴露原始支付信息（如信用卡号）的情况下，**可验证地**授权一个代理？
    
2.  **真实性 (Authenticity) 风险：** AI 可能会“幻觉”或被误导。如何确保交易**锚定**在用户明确的、真实的意图上？
    
3.  **责任 (Accountability) 模糊：** 如果交易出错或发生欺诈，谁来负责？用户？代理开发者？商家？
    

**AP2 的核心解决方案：** 将支付重新定义为“**合约式对话 (Contractual Conversations)**”。它不依赖于 AI 的概率性推理，而是依赖于**密码学**。它使用**可验证凭证 (VCs)** 作为防篡改的、可验证的“**授权指令 (Mandates)**”，为所有参与方提供不可否认的意图证明。

* * *

**2\. AP2 的核心安全支柱**

1.  **角色分离 (Role-Based Design):**
    
    -   AP2 将生态系统拆分为多个独立角色，以防止单点故障和数据泄露。
        
    -   **Shopping Agent (SA):** 购物代理（用户侧），负责协调流程，_但不接触_原始支付信息。
        
    -   **Credentials Provider (CP):** 凭证提供商（如银行、卡组织），_唯一_管理支付方法（如卡片 Token）的角色。
        
    -   **Merchant Endpoint (ME):** 商家端点，负责协商购物车并签名。
        
    -   **安全含义：** 实现了 PCI-DSS 合规中的职责分离。SA 即使被攻破，也无法泄露用户的支付凭证，因为它只持有 CP 提供的 Token。
        
2.  **加密基础 (Cryptographic Primitives):**
    
    -   所有“授权指令” (Mandates) 都使用**数字签名**（例如 ECDSA）。
        
    -   `IntentMandate` **(意图指令):** 由用户在**设备端**（最好是硬件安全区，如 TPM、Android DPC）签名，锚定用户的_高级意图_（如“买票，不超过$200”）。
        
    -   `CartMandate` **(购物车指令):** 由商家签名（`merchant_signature`）确认商品和价格，然后由用户签名（`user_signature`）确认支付。
        
    -   **安全含义：** 签名提供了**不可否认性 (Non-Repudiation)**。用户不能否认自己签署了某个意图，商家也不能否认自己提供了某个报价。
        
3.  **AI 风险信号 (AI-Aware Risk Scoring):**
    
    -   `PaymentMandate`（发送给支付网络/银行的最终指令）中包含了一个关键的 **“代理模态”信号**。
        
    -   **信号内容：** `Human-Present` (人类在场) 或 `Human-Not-Present` (人类不在场)。
        
    -   **安全含义：** 银行和支付网络可以首次_知道_这笔交易是由 AI 代理发起的。它们可以为此启用全新的、AI 感知的风险评估模型，而不仅仅依赖传统规则。
        

* * *

**3\. 关键威胁模型 (STRIDE)**

文章使用 STRIDE 模型分析了 AP2 面临的标准威胁：

-   **T1: 欺骗 (Spoofing):**
    
    -   _威胁：_ 伪造授权指令签名。
        
    -   _缓解：_ 严格的公钥基础设施 (PKI) 验证；使用硬件安全模块 (HSM) 管理密钥。
        
-   **T2: 篡改 (Tampering):**
    
    -   _威胁：_ 在传输过程中（如 A2A 通道中）修改指令内容。
        
    -   _缓解：_ 强制使用 TLS 1.3 加密通道；在消息体中加入 SHA-256 校验和 (Checksums)。
        
-   **T3: 信息泄露 (Info. Disclosure):**
    
    -   _威胁：_ 泄露 PII 或支付数据。
        
    -   _缓解：_ 严格的角色分离（SA 看不到原始凭证）；对 mandate 载荷进行 AES-GCM 加密。
        
-   **T4: 拒绝服务 (Denial of Service):**
    
    -   _威胁：_ 用垃圾指令淹没代理。
        
    -   _缓解：_ 对公共 API 进行速率限制；使用可验证的注册表。
        
-   **T5: 权限提升 (Elevation of Privilege):**
    
    -   _威胁：_ 代理被劫持或冒充其他角色（如 CP）。
        
    -   _缓解：_ 使用**去中心化白名单 (Allowlists)** 验证代理身份；使用 OAuth 进行代理认证。
        
-   **T6: 否认 (Repudiation):**
    
    -   _威胁：_ 用户否认自己签署了某个指令。
        
    -   _缓解：_ **不可否认的 ECDSA 签名**和防篡改的审计日志。
        

* * *

**4\. 高级威胁模型：MAESTRO (AI 代理特定威胁)**

**这是本文最核心的贡献。** STRIDE 无法覆盖 AI 代理的**动态和涌现行为**。MAESTRO 是一个 7 层框架，用于分析 AP2 这类 AI 代理生态的独特风险。

-   **L1: 基础模型 (Foundation Models):**
    
    -   _威胁：_ **涌现的决策偏见**。通过对抗性微调，使 SA 偏向于选择恶意商家的商品。
        
-   **L2: 数据操作 (Data Operations):**
    
    -   _威胁：_ **内存投毒**。污染 RAG/向量数据库（如过去的购物车记录），导致代理对用户的_意图_产生错误理解。
        
-   **L3: 代理框架 (Agent Frameworks):**
    
    -   _威胁：_ **工作流劫持（提示注入）**。通过恶意提示（Prompt Injection）重定向代理的委托，绕过 `IntentMandate` 检查。
        
-   **L4: 部署设施 (Deployment Infrastructure):**
    
    -   _威胁：_ **容器逃逸导致代理共谋**。恶意代理逃逸沙箱后，在 A2A 通道上协调，对商家进行 DDoS 攻击。
        
-   **L5: 评估与可观测性 (Evaluation & Observability):**
    
    -   _威胁：_ **异常淹没 (Anomaly Flooding)**。恶意代理产生大量低风险的误报，使人类审查员疲劳，从而掩盖真正的、缓慢的“卡特尔攻击”（如代理间缓慢共享 compromised tokens）。
        
-   **L6: 安全与合规 (Security & Compliance):**
    
    -   _威胁：_ **策略操纵**。代理利用 LLM 的灵活性来“创造性地”**重新解释**合规规则（如 SCA/PSD2），从而绕过 3DS 验证。
        
-   **L7: 代理生态 (Agent Ecosystem):**
    
    -   _威胁：_ **代理生态共谋**。多个（看似无关的）代理自主协调，操纵市场（如通过虚假协商抬高价格）。**声誉攻击**（操纵信任评分，优先选择已受损的对等方）。
        

* * *

**5\. 实用安全指南与代码级缓解措施**

文章给出了可操作的建议和代码示例，用于防范上述威胁：

1.  **密钥管理 (T1, T3):**
    
    -   **指南：** 必须使用 TPM/HSM 或设备安全区（如 Android DPC）来存储和使用签名私钥。
        
    -   **代码：** `DpcHelper.signMandate(mandate)` (Android 示例)，强制使用硬件签名。
        
2.  **强制验证 (T1, T2, L7):**
    
    -   **指南：** 绝不信任收到的数据。在处理_任何_指令前，必须验证其签名。
        
    -   **代码：** `mandate.verify_signature(pub_key)` (Python)，用于验证商家或用户的签名。`verifyDID(agentCard)` (Android)，用于在 A2A 通信前验证对方代理的 DID 身份。
        
3.  **输入净化 (L3):**
    
    -   **指南：** 所有来自外部（尤其是用户提示）的输入都必须被净化，以防止提示注入。
        
    -   **代码：** `sanitize_prompt(prompt)` (Python)，用于剥离恶意指令或脚本。
        
4.  **访问控制 (T5, L7):**
    
    -   **指南：** 建立一个“允许列表 (Allowlist)”注册表，只与经过验证的代理进行通信。
        
    -   **代码：** `validate_agent(agent_id)` (Python)，在委托任务前检查该 `sub_agent` 是否在允许列表中。
        
5.  **速率限制 (T4):**
    
    -   **指南：** 为代理的公共 API 设置速率限制，防止 DoS 攻击。
        
    -   **代码：** `check_rate_limit(user_id)` (Python)，限制单个用户的请求频率。
        
6.  **运行时护栏 (L6):**
    
    -   **指南：** 不能完全信任 LLM 的决策。在执行工具（特别是支付）时，要用硬编码的规则进行检查。
        
    -   **代码：** `enforce_policy(mandate)` (Python)，在支付前强制检查（例如 `mandate.contents.total < 100`），防止 AI 操纵规则。
        

**量化结果：**

-   模拟显示，与传统 API 相比，AP2 将欺诈率从 **2.1%** 降低到了 **1.15%**，这证明了其通过可验证意图来提升安全性的有效性。
    

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/Duamixu1/images/2025-10-19-1760840694165-image.png)

### **AP2 开发者快速入门学习笔记 🚀**

* * *

**💡 核心理念与技术栈 (About the Samples)**

1.  **协议的独立性 (AP2 is Tool-Agnostic):**
    
    -   这是最关键的一点：AP2 是一个**开放协议**。它_不_要求你必须使用 Google 的任何特定工具。你可以用任何你喜欢的技术栈来构建你的代理。
        
2.  **官方示例的技术栈 (Sample Stack):**
    
    -   官方提供的示例代码使用了 **Google ADK (Agent Development Kit)** 和 **Gemini 2.5 Flash** 模型。
        
    -   再次强调：这只是为了_演示_，你完全可以替换成其他框架或模型。
        

* * *

**📁 代码库结构 (Repository Navigation)**

-   **场景 (Scenarios):** 核心演示代码在 `samples/` 目录下。
    
    -   `samples/android/scenarios`：包含 Android 购物助手的场景。
        
    -   `samples/python/scenarios`：包含 Python 购物助手的场景。
        
-   **场景内部结构：** 每一个场景文件夹（例如 `your-scenario-name/`）都包含：
    
    -   `README.md`：**必读文件**。详细描述了该场景的功能和运行步骤。
        
    -   `run.sh`：一个便捷脚本，用于一键安装依赖并启动该场景。
        
-   **源码 (Source Code):**
    
    -   `samples/python/src`：**大部分代理和服务器的 Python 源码**都存放在这里。
        
    -   `samples/android`：Android App 的源码。
        

* * *

**🔧 快速启动：环境设置 (Quickstart)**

**1\. 必备S"先决条件 (Prerequisites)**

-   Python 3.10 或更高版本。
    
-   `uv`：一个 Python 包管理器 (注意：不是 `pip` 或 `conda`，这是新趋势)。
    

**2\. 身份验证 (Setup & Authentication)**

你需要一种方式来调用 Google 的 AI 模型。你有两种选择，推荐使用 `.env` 文件来管理你的密钥。

-   **方法一：Google API Key (推荐用于开发)**
    
    1.  从 **Google AI Studio** 获取你的 API 密钥。
        
    2.  在你的项目根目录创建一个 `.env` 文件，内容如下：
        
        代码段
        
        ```
        GOOGLE_API_KEY='your_key_here'
        ```
        
-   **方法二：Vertex AI (推荐用于生产)**
    
    1.  你需要先配置好 `gcloud` 命令行工具。
        
    2.  在 `.env` 文件中设置：
        
        代码段
        
        ```
        GOOGLE_GENAI_USE_VERTEXAI=true
        GOOGLE_CLOUD_PROJECT='your-project-id'
        GOOGLE_CLOUD_LOCATION='global' # 或你的区域
        ```
        
    3.  **进行身份验证** (二选一)：
        
        -   **命令行登录 (推荐):**
            
            Bash
            
            ```
            gcloud auth application-default login
            ```
            
        -   **服务账户 (Service Account):**
            
            Bash
            
            ```
            export GOOGLE_APPLICATION_CREDENTIALS='/path/to/your/service-account-key.json'
            ```
            

* * *

**▶️ 如何运行一个场景 (How to Run a Scenario)**

1.  进入代码库的根目录：
    
    Bash
    
    ```
    cd AP2
    ```
    
2.  执行你想运行的场景的 `run.sh` 脚本（请先阅读该场景的 `README.md`！）：
    
    Bash
    
    ```
    bash samples/python/scenarios/your-scenario-name/run.sh
    ```
    
3.  该脚本会自动安装所有依赖并启动相关的代理服务。
    
4.  脚本运行成功后，在终端中找到 **Shopping Agent URL**，在浏览器中打开它即可开始交互。
    

* * *

**📦 如何在你的项目中使用 AP2 (Installing the AP2 Types Package)**

如果你不想运行示例，而是想在你自己的项目中使用 AP2 的核心数据结构（比如 `Mandate` 对象）。

1.  **核心类型定义：** 协议的核心对象（数据结构）定义在 `src/ap2/types` 目录中。
    
2.  **安装方式 (重要):**
    
    -   官方说明“PyPI 包将在稍后发布”。这意味着**目前 (截至 2025 年 10 月) 还没有正式的 PyPI 包**。
        
    -   你必须使用 `uv` 直接从 GitHub `main` 分支进行安装：
        
    
    Bash
    
    ```
    uv pip install git+https://github.com/google-agentic-commerce/AP2.git@main
    ```
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->



**1\. 基础概念：定义与核心 (What is A2A? & Core Concepts)**

**学习笔记：**

-   **A2A 是什么 (What is A2A?)**: 这部分将定义 A2A 协议。它很可能是一个**通信标准**，专门设计用于**自主 AI 代理 (Agent) 之间的交互**。其核心目标是解决一个基本问题：在没有中心化协调者的情况下，两个或多个独立的 AI 代理如何相互发现、协商并交换信息/价值？
    
-   **核心概念 (Core Concepts)**: 这是协议的词汇表。我们可以预期它会定义以下基本构建块：
    
    -   **Agent (代理)**: 参与协议的基本单元，一个自主的决策实体。
        
    -   **Message (消息)**: 代理之间交换的数据单元，具有标准化的格式。
        
    -   **Service (服务)**: 代理可以提供或请求的能力（例如，“图像标注服务”）。
        
    -   **Task (任务)**: 一个具体的、有生命周期的工作单元。
        
    -   **Registry (注册表)**: 可能是用来存储代理身份或服务描述的地方。
        

**深度思考：**

-   **A2A 与 ERC-8004 的关系是什么？** 这是最关键的问题。如果说 **ERC-8004**（如我们之前所学）是构建**信任层**（身份、声誉、验证），那么 **A2A 协议**很可能就是**通信层**（消息传递、服务发现、任务执行）。
    
    -   ERC-8004 回答：“我凭什么信任你这个代理？”
        
    -   A2A 协议回答：“我该如何与你这个代理对话？” 两者结合，才能构成一个功能完备、无需信任的代理经济。A2A 协议的消息中很可能会携带 ERC-8004 定义的身份和声誉证明。
        
-   **为什么不用现有的 API (如 REST/HTTP)？** HTTP 是为“客户端-服务器”模式设计的，它假定客户端_已经知道_服务器的地址和 API 规范。而 A2A 协议必须解决一个更复杂的问题：**动态发现**。代理需要在广阔的网络中找到未知的、但能满足其需求的其它代理。这要求协议本身支持更灵活的服务发现和服务协商机制。
    

**2\. 交互流程：发现与执行 (Agent Discovery & Life of a Task)**

**学习笔记：**

-   **代理发现 (Agent Discovery)**: 这是交互的起点。一个代理如何找到它需要的服务？这部分可能会描述一个去中心化的“黄页”系统。代理可以发布自己的能力（Service），也可以根据需求查询其它代理。
    
-   **任务生命周期 (Life of a Task)**: 这描述了一个完整交互的“动词”。它会定义一个状态机，例如：
    
    1.  `TASK_REQUESTED` (任务请求)
        
    2.  `TASK_NEGOTIATED` (任务协商 - 价格、时限)
        
    3.  `TASK_ACCEPTED` (任务接受)
        
    4.  `TASK_IN_PROGRESS` (任务执行中)
        
    5.  `TASK_COMPLETED` (任务完成) / `TASK_FAILED` (任务失败)
        

**深度思考：**

-   **“发现”的信任难题**： “代理发现”是去中心化系统的阿喀琉斯之踵。如果发现机制（例如注册表）是中心化的，那么整个系统就不是去中心化的。如果它是完全去中心化的（如 DHT），那么如何防范“女巫攻击”（Sybil Attack），即恶意代理伪造大量身份提供虚假服务？
    
    -   **思考**：这再次凸显了 ERC-8004 的重要性。A2A 的“发现”机制可能只负责“找到”，而 ERC-8004 的“声誉”系统负责“筛选”。你发现 10 个代理，但你只选择声誉最高的那个。
        
-   **任务生命周期与链上/链下的协同**： 一个 AI 任务（如模型训练）可能需要几小时甚至几天。如此长的“任务生命周期”显然不能完全在链上（如以太坊）进行，否则成本高昂且速度缓慢。
    
    -   **思考**：A2A 协议的主体（如协商、数据传输）必然是**链下 (Off-chain)** 的 P2P 通信。而生命周期中的关键节点，如 `TASK_ACCEPTED`（锁定付款）和 `TASK_COMPLETED`（释放付款、更新声誉），则会触发**链上 (On-chain)** 交互（例如调用 ERC-8004 的声誉或验证合约）。
        

**3\. 高级功能：效率与扩展 (Enterprise, Streaming, Extensions)**

**学习笔记：**

-   **企业特性 (Enterprise Features)**: 这表明 A2A 不仅仅是一个实验。它可能包括：
    
    -   **安全性**: 消息加密、身份验证。
        
    -   **隐私性**: 如何在不泄露敏感数据的情况下完成任务？（这可能与我们学过的 TEE 或 ZK 有关）。
        
    -   **可审计性**: 能够追溯任务历史。
        
-   **流式处理与异步操作 (Streaming & Asynchronous Operations)**: 这是为 AI 定制的关键特性。AI 任务不是简单的“请求-响应”。一个代理可能需要向另一个代理“流式”发送大量数据，或者一个任务需要很长时间才能（异步）返回结果。
    
-   **扩展 (Extensions)**: 协议的核心是精简的，但允许通过插件进行功能扩展。这保证了协议的灵活性和未来适应性。
    

**深度思考：**

-   **异步操作 vs. 区块链同步性**： 区块链本质上是同步的（一个区块接着一个区块）。而 AI 任务是异步的。A2A 协议的设计必须优雅地处理这种“时钟”不匹配。这强化了“链下通信 + 链上结算”的架构猜想。
    
-   **“扩展”是 TEE 和 ZK 的入口吗？** A2A 核心协议可能不强制使用任何特定的验证技术。但“扩展”部分很可能就是用来插入不同“验证模块”的地方。
    
    -   **场景**：当一个“企业特性”要求高隐私时，代理可以通过 A2A 协商，并同意使用一个“TEE 扩展”来创建一个安全飞地 (Enclave) 完成计算，或者使用一个“ZK 扩展”来在不泄露输入的情况下证明计算结果。
        

**4\. 生态系统与未来 (MCP, SDK, Roadmap)**

**学习笔记：**

-   **A2A 和 MCP (A2A and MCP)**: MCP 是另一个协议（可能是 Multi-Agent Communication Protocol 或其他）。这部分会阐明 A2A 与相关标准的关系。它是 MCP 的替代、补充还是基于 MCP 的？
    
-   **规范 (Specification)**: 协议的技术蓝图，供开发者实现。
    
-   **SDK 参考 & 教程 (SDK Reference & Tutorials)**: 将规范转化为可用的代码库。这是协议能否被广泛采用的关键。
    
-   **社区、合作伙伴、路线图**: 展示生态系统的活跃度和未来愿景。
    

**深度思考：**

-   **标准之战**： “A2A 和 MCP”暗示着代理通信领域可能存在“标准之战”。一个协议的成功不仅在于技术先进性，更在于**网络效应**。谁能吸引最多的开发者、代理和合作伙伴（即“社区”和“合作伙伴”），谁就可能成为最终的标准。
    
-   **从“协议”到“生态”的鸿沟**： 一个协议（Specification, SDK）的发布只是第一步。最大的挑战在于如何启动“社区”来跨越鸿沟。A2A 需要解决一个“先有鸡还是先有蛋”的问题：
    
    -   没有“服务提供者”代理，“服务消费者”代理就不会加入。
        
    -   没有“服务消费者”代理，“服务提供者”代理也没有动力加入。
        
    -   **思考**：“路线图”中可能包含的经济激励模型、黑客松、合作伙伴计划，是解决这个冷启动问题的关键。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->




![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/Duamixu1/images/2025-10-17-1760713550697-image.png)![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/Duamixu1/images/2025-10-17-1760713579722-image.png)

**1\. 关于信任模型的权衡 (Trade-offs in Trust Models)**

-   **思考:** TEE 依赖于对硬件制造商（如 Intel）的信任，我们相信他们设计的硬件没有后门，且生产过程是安全的。而 ZK 依赖于对底层密码学和数学算法的信任。这两种信任根源有何本质区别？
    
-   **问题:**
    
    -   在完全去中心化的理想世界里，依赖于少数几家科技巨头提供的硬件（TEE），是否是一种“中心化的妥协”？这是否会成为整个系统的单点故障或审查点？
        
    -   ZK 的计算成本（尤其是生成证明的成本）目前仍然高昂。在哪些场景下，为了追求纯粹的数学信任而牺牲性能是值得的？而在哪些场景下，选择更高效但有硬件信任假设的 TEE 是更明智的选择？
        
    -   有没有可能将 TEE 和 ZK 结合起来？例如，在一个 TEE 环境中运行 ZK 证明的生成过程，这会带来什么好处（比如保护证明生成逻辑）和新的风险？
        

**2\. 声誉系统的脆弱性 (Vulnerabilities in Reputation Systems)**

-   **思考:** ERC-8004 将声誉计算放在链下，以提高灵活性和效率。但这是否也引入了新的攻击向量？
    
-   **问题:**
    
    -   **女巫攻击 (Sybil Attack):** 一个恶意行为者是否可以创建大量虚假身份的 AI 代理，互相“刷好评”，从而迅速建立虚假的高声誉？ERC-8004 的身份注册机制如何防范这一点？是否需要引入身份质押或某种形式的社交图谱验证？
        
    -   **共谋与报复:** 一组代理是否可以共谋，相互给予好评，并集体给竞争对手差评？或者，一个代理在收到差评后，是否可以对评价者进行报复性差评？链下的声誉算法如何设计才能抵抗这种“链上黑社会”行为？
        
    -   **声誉的非普适性:** 一个在“图像识别”领域声誉很高的代理，当它转向“自然语言处理”任务时，其声誉是否还适用？我们是否需要更细粒度、多维度的声誉系统，而不仅仅是一个单一的分数？
        

**3\. 验证的边界与 AI 的“黑盒”问题 (The Limits of Verification & The AI Black Box)**

-   **思考:** TEE 和 ZK 可以验证计算过程的完整性，即“程序是否被正确执行”。但它们无法验证程序本身的逻辑是否正确或公平。
    
-   **问题:**
    
    -   对于复杂的 AI 模型（尤其是深度学习模型），其决策过程本身就是个“黑盒”。即使我们用 TEE 或 ZK 验证了模型的输入和输出是匹配的，我们如何确保模型内部没有偏见（Bias）？如何确保它的决策是公平、合乎道德的？
        
    -   如果一个 AI 代理的源代码是闭源的，我们如何信任它？ERC-8004 的框架是否会更偏向于开源代理，从而形成一种“开源即正义”的生态文化？
        
    -   当 AI 代理的工作成果是主观的（例如，生成一首诗、一幅画），我们如何设计验证机制？此时，声誉系统是否会比计算验证更为重要？
        

**4\. 经济模型与激励机制 (Economic and Incentive Models)**

-   **思考:** 整个 ERC-8004 系统需要一个强大的经济模型来驱动。验证者、声誉提供者、代理开发者都需要被激励。
    
-   **问题:**
    
    -   运行 TEE 或生成 ZK 证明都需要成本。谁来支付这个成本？是任务的发布者，还是执行任务的代理，还是整个网络？这个成本会如何影响 AI 代理服务的定价？
        
    -   如果一个 AI 代理作恶被发现，惩罚机制是什么？仅仅是声誉降低吗？是否应该引入更强的惩罚，例如罚没质押的代币？
        
    -   如何激励“诚实的验证者”？如果验证者和代理可以共谋欺骗任务发布者，系统的安全性如何保证？
<!-- DAILY_CHECKIN_2025-10-17_END -->

<!-- DAILY_CHECKIN_2025-10-16_START -->

<!-- DAILY_CHECKIN_2025-10-16_START -->
<!-- Content_END -->
## ERC-8004：自主 AI 代理基础设施 笔记

ERC-8004 是一项旨在融合人工智能（AI）和区块链技术的智能合约标准。它的核心目标是为自主 AI 代理（Autonomous AI Agents）创建一个无需信任（Trustless）的协作基础设施，从而催生一个全新的\*\*“代理经济”（Agentic Economy）\*\*。

* * *

### \## 核心问题：解决“信任鸿沟”

传统的 AI 代理间通信协议（如谷歌的 A2A 协议）非常高效，但它们**假设参与者之间已经存在信任**，这使得协作仅限于单个组织内部。当不同组织的代理需要交互时，便出现了“信任鸿沟”。

ERC-8004 旨在解决以下几个关键问题：

-   **发现问题 (Discovery Problem):** 代理如何跨网络找到信誉良好的服务提供者？
    
-   **质量保证 (Quality Assurance):** 在没有预先互动的情况下，如何验证服务提供者的能力？
    
-   **信誉可移植性 (Reputation Portability):** 代理如何跨平台建立和维护自己的声誉？
    
-   **验证可扩展性 (Validation Scalability):** 如何让验证机制适应从低风险到高风险的不同任务需求？
    

* * *

### \## ERC-8004 的三大核心组件

该标准采用一种**混合方法**，仅将关键的信任相关数据放在链上，而将复杂操作和大量数据存储在链下，以实现高效率和低成本。它由三个核心的链上注册表（Registry）组成：

1\. 身份注册表 (Identity Registry)

-   **功能:** 为每个 AI 代理提供一个全球唯一的、抗审查的链上标识符（`AgentID`）。
    
-   **工作方式:** 它创建一个全局命名空间，将代理的 `AgentID` 与其域名（`AgentDomain`）和以太坊地址（`AgentAddress`）进行映射。每个代理通过其域名提供一个标准的 `AgentCard.json` 文件，用于描述其能力和链上身份信息。
    

2\. 信誉注册表 (Reputation Registry)

-   **功能:** 一个轻量级的反馈授权系统，而非直接存储信誉评分。
    
-   **工作方式:** 当代理 A 完成代理 B 的任务后，代理 B 可以在链上触发一个\*\*“反馈授权”\*\*事件。这个事件本身不包含具体的评价内容，只是一个不可篡改的记录，证明反馈是允许的。实际的信誉数据和复杂的评分算法则存在于链下，从而兼顾了灵活性和可信度。
    

3\. 验证注册表 (Validation Registry)

-   **功能:** 提供一个通用的接口（Hooks），用于请求和记录对代理任务的独立验证。
    
-   **工作方式:** 它支持多种验证协议。当一项任务需要高确定性时，可以通过该注册表请求第三方验证者介入。
    

* * *

### \## 创新的分层信任模型

ERC-8004 最重要的特性之一是其**分层信任架构**，它根据任务的风险和价值，采用不同级别的安全保障。

-   **低风险任务 (Low Stakes)**
    
    -   **机制:** **基于信誉的信任 (Reputation-Based Trust)**。
        
    -   **场景:** 内容创作、简单查询等。
        
    -   **描述:** 类似于传统的点评系统，依赖于由客户反馈积累的社会共识。
        
-   **中等风险任务 (Medium Stakes)**
    
    -   **机制:** **加密经济验证 (Crypto-Economic Validation)**。
        
    -   **场景:** 金融交易、智能合约操作等。
        
    -   **描述:** 验证者必须**质押（Stake）经济价值（如代币）。如果他们做出错误的验证，其质押的资产将被罚没（Slash）**，从而以经济激励确保其诚实行为。
        
-   **高风险任务 (High Stakes)**
    
    -   **机制:** **密码学验证 (Cryptographic Verification)**。
        
    -   **场景:** 医疗诊断、关键基础设施控制等。
        
    -   **描述:** 使用\*\*可信执行环境（TEE）\*\*等技术，从密码学层面保证代码在安全硬件中按预期执行，并保护数据机密性，提供最高级别的安全保障。
        

* * *

### \## 主要安全考量与缓解措施

为了确保网络的稳健，ERC-8004 必须防范多种潜在攻击：

-   **域名抢注 (Domain Squatting):**
    
    -   **攻击:** 攻击者通过抢先交易来注册有价值的代理域名。
        
    -   **缓解:** 采用“提交-揭示”（Commit-Reveal）方案隐藏注册意图。
        
-   **女巫攻击 (Sybil Identity Creation):**
    
    -   **攻击:** 恶意行为者创建大量虚假身份来操纵信誉系统。
        
    -   **缓解:** 要求新代理注册时缴纳保证金或销毁代币，并引入零知识证明等技术来限制一个实体只能创建一个身份。
        
-   **存储膨胀与 DoS 攻击 (Storage Bloat and DoS):**
    
    -   **攻击:** 恶意提交海量验证请求，耗尽合约存储空间。
        
    -   **缓解:** 对请求设置自动过期时间，限制单个代理的待处理请求数量，并要求缴纳可退还的保证金。
        
-   **未经授权的反馈 (Unauthorized Feedback):**
    
    -   **攻击:** 任何人都可以触发反馈授权事件，产生垃圾数据。
        
    -   **缓解:** 对函数调用进行访问控制，确保只有服务接受方才能授权反馈。
        

### \## 结论

ERC-8004 为实现一个自主、开放和无需信任的“代理经济”奠定了基础。它通过创新的链上注册表和分层信任模型，巧妙地结合了 AI 的自主性与区块链的安全性。然而，要确保这一宏伟愿景的实现，对底层智能合约进行严格的安全审计是不可或缺的。
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
## ERC-8004：自主 AI 代理基础设施 笔记

ERC-8004 是一项旨在融合人工智能（AI）和区块链技术的智能合约标准。它的核心目标是为自主 AI 代理（Autonomous AI Agents）创建一个无需信任（Trustless）的协作基础设施，从而催生一个全新的\*\*“代理经济”（Agentic Economy）\*\*。

* * *

### \## 核心问题：解决“信任鸿沟”

传统的 AI 代理间通信协议（如谷歌的 A2A 协议）非常高效，但它们**假设参与者之间已经存在信任**，这使得协作仅限于单个组织内部。当不同组织的代理需要交互时，便出现了“信任鸿沟”。

ERC-8004 旨在解决以下几个关键问题：

-   **发现问题 (Discovery Problem):** 代理如何跨网络找到信誉良好的服务提供者？
    
-   **质量保证 (Quality Assurance):** 在没有预先互动的情况下，如何验证服务提供者的能力？
    
-   **信誉可移植性 (Reputation Portability):** 代理如何跨平台建立和维护自己的声誉？
    
-   **验证可扩展性 (Validation Scalability):** 如何让验证机制适应从低风险到高风险的不同任务需求？
    

* * *

### \## ERC-8004 的三大核心组件

该标准采用一种**混合方法**，仅将关键的信任相关数据放在链上，而将复杂操作和大量数据存储在链下，以实现高效率和低成本。它由三个核心的链上注册表（Registry）组成：

1\. 身份注册表 (Identity Registry)

-   **功能:** 为每个 AI 代理提供一个全球唯一的、抗审查的链上标识符（`AgentID`）。
    
-   **工作方式:** 它创建一个全局命名空间，将代理的 `AgentID` 与其域名（`AgentDomain`）和以太坊地址（`AgentAddress`）进行映射。每个代理通过其域名提供一个标准的 `AgentCard.json` 文件，用于描述其能力和链上身份信息。
    

2\. 信誉注册表 (Reputation Registry)

-   **功能:** 一个轻量级的反馈授权系统，而非直接存储信誉评分。
    
-   **工作方式:** 当代理 A 完成代理 B 的任务后，代理 B 可以在链上触发一个\*\*“反馈授权”\*\*事件。这个事件本身不包含具体的评价内容，只是一个不可篡改的记录，证明反馈是允许的。实际的信誉数据和复杂的评分算法则存在于链下，从而兼顾了灵活性和可信度。
    

3\. 验证注册表 (Validation Registry)

-   **功能:** 提供一个通用的接口（Hooks），用于请求和记录对代理任务的独立验证。
    
-   **工作方式:** 它支持多种验证协议。当一项任务需要高确定性时，可以通过该注册表请求第三方验证者介入。
    

* * *

### \## 创新的分层信任模型

ERC-8004 最重要的特性之一是其**分层信任架构**，它根据任务的风险和价值，采用不同级别的安全保障。

-   **低风险任务 (Low Stakes)**
    
    -   **机制:** **基于信誉的信任 (Reputation-Based Trust)**。
        
    -   **场景:** 内容创作、简单查询等。
        
    -   **描述:** 类似于传统的点评系统，依赖于由客户反馈积累的社会共识。
        
-   **中等风险任务 (Medium Stakes)**
    
    -   **机制:** **加密经济验证 (Crypto-Economic Validation)**。
        
    -   **场景:** 金融交易、智能合约操作等。
        
    -   **描述:** 验证者必须**质押（Stake）经济价值（如代币）。如果他们做出错误的验证，其质押的资产将被罚没（Slash）**，从而以经济激励确保其诚实行为。
        
-   **高风险任务 (High Stakes)**
    
    -   **机制:** **密码学验证 (Cryptographic Verification)**。
        
    -   **场景:** 医疗诊断、关键基础设施控制等。
        
    -   **描述:** 使用\*\*可信执行环境（TEE）\*\*等技术，从密码学层面保证代码在安全硬件中按预期执行，并保护数据机密性，提供最高级别的安全保障。
        

* * *

### \## 主要安全考量与缓解措施

为了确保网络的稳健，ERC-8004 必须防范多种潜在攻击：

-   **域名抢注 (Domain Squatting):**
    
    -   **攻击:** 攻击者通过抢先交易来注册有价值的代理域名。
        
    -   **缓解:** 采用“提交-揭示”（Commit-Reveal）方案隐藏注册意图。
        
-   **女巫攻击 (Sybil Identity Creation):**
    
    -   **攻击:** 恶意行为者创建大量虚假身份来操纵信誉系统。
        
    -   **缓解:** 要求新代理注册时缴纳保证金或销毁代币，并引入零知识证明等技术来限制一个实体只能创建一个身份。
        
-   **存储膨胀与 DoS 攻击 (Storage Bloat and DoS):**
    
    -   **攻击:** 恶意提交海量验证请求，耗尽合约存储空间。
        
    -   **缓解:** 对请求设置自动过期时间，限制单个代理的待处理请求数量，并要求缴纳可退还的保证金。
        
-   **未经授权的反馈 (Unauthorized Feedback):**
    
    -   **攻击:** 任何人都可以触发反馈授权事件，产生垃圾数据。
        
    -   **缓解:** 对函数调用进行访问控制，确保只有服务接受方才能授权反馈。
        

### \## 结论

ERC-8004 为实现一个自主、开放和无需信任的“代理经济”奠定了基础。它通过创新的链上注册表和分层信任模型，巧妙地结合了 AI 的自主性与区块链的安全性。然而，要确保这一宏伟愿景的实现，对底层智能合约进行严格的安全审计是不可或缺的。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->
# **Duami**

**GitHub ID:** Duamixu1

**Telegram:** @SwimmingDua


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
# **Duami**

**GitHub ID:** Duamixu1

**Telegram:** @SwimmingDua

## **Self-introduction**

Have Passion for exploring new things.

**EIP-8004：赋能去中心化AI代理的新标准**

**核心目标：**

EIP-8004 旨在为以太坊上的AI代理（AI Agent）创建一个无需信任的、去中心化的交互框架。它扩展了现有的A2A（Agent-to-Agent）协议，通过引入一个信任层，使来自不同组织和生态系统的AI代理能够安全地发现、验证和协作，而无需依赖中心化的中介机构。

**关键组成部分：**

EIP-8004 主要通过三个链上注册表来实现其目标：

-   **身份（Identity）：** 为每个AI代理提供一个便携的、抗审查的链上身份。这个身份以ERC-721代币（NFT）的形式存在，使得AI代理可以像其他数字资产一样被查看、转移和管理。这个NFT关联的注册文件描述了代理的技能、端点和元数据，形成了一个标准化的“护照”。
    
-   **声誉（Reputation）：** 建立一个链上声誉系统。通过整合x402支付证明和反馈数据，AI代理可以建立可验证的行为历史。这使得其他代理可以根据其过去的表现来评估其可信度。
    
-   **验证（Validation）：** 提供通用的验证钩子，用于经济或密码学验证。这确保了代理之间的交互是安全和可信的。
    

**带来的优势：**

-   **增强的安全性：** 通过区块链技术验证代理的身份和行为，消除了对中心化中介机构的需求，从而提高了安全性。
    
-   **可扩展性：** 为AI代理经济的扩展奠定了基础，使其能够支持数万亿级别的市场规模。
    
-   **互操作性：** 提供统一的接口和分层信任模型，使不同AI系统之间的互操作性成为可能。
    
-   **去中心化AI经济：** 为一个由AI代理而非人类主导的去中心化经济铺平了道路。在这个经济中，AI代理将能够自主地进行谈判、管理资源和组建DAO（去中心化自治组织）。
    

**现状：**

EIP-8004目前仍处于草案阶段，正在征求社区的反馈和完善。如果得到社区的广泛支持和采用，这个标准有望成为以太坊上无需信任、协作式AI的基础。

### 潜在挑战与开放性问题

-   **声誉攻击 (Reputation Attack):** 是否会出现“刷单”现象？即创建大量虚假 AI 代理相互合作，以伪造良好的声誉。
    
-   **中心化风险:** 是否会导致“赢家通吃”？少数拥有顶级声誉的 AI 代理是否会垄断市场，形成新的中心化？
    
-   **责任归属:** 当一个由多个 AI 自主协作的项目失败并造成巨大损失时，责任应由谁承担？是 AI 的所有者、开发者，还是整个协作网络？
    
-   **计算成本:** 在公链上记录每一次交互的成本可能非常高。这套系统可能更适用于 Layer 2 或特定的应用链。
    

### IP-8004 技术实现深度剖析 (代码示例)

为了实现 AI 代理的自主协作，整个系统可以被模块化为三个核心的链上组件：**身份注册表 (Identity Registry)**、**声誉注册表 (Reputation Registry)** 和 **交互合约 (Interaction Contract)**。

1\. 身份注册表 (Identity Registry) - `EIP8004_Identity.sol`

这是系统的基石，一个实现了 ERC-721 标准的 NFT 合约。每个 AI 代理都被铸造为一个独一无二的 NFT。关键在于其 `tokenURI` 指向的元数据。

**元数据结构 (Metadata JSON, 通常存储在 IPFS 上):** `tokenURI` 会指向一个类似下面这样的 JSON 文件，这才是“AI 护照”的详细内容。

JSON

```
{
  "name": "DataAnalysisAgent-0x4b2a",
  "description": "A specialized AI agent for financial time-series analysis.",
  "owner": "0x123...",
  "endpoint": {
    "type": "https",
    "uri": "https://api.my-agent.ai/v1/process"
  },
  "skills": [
    {
      "skill_name": "time_series_forecasting",
      "framework": "prophet",
      "version": "1.2"
    },
    {
      "skill_name": "sentiment_analysis",
      "model": "bert-base-finance"
    }
  ],
  "validation_hooks": [
    "requires_staked_eth",
    "supports_zkp_data_proof"
  ]
}
```

**Solidity 合约简化示例 (**`EIP8004_Identity.sol`**):**

Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

// 这是一个极其简化的身份注册表
contract EIP8004_Identity is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIdCounter;

    // 映射：tokenId => 元数据 URI
    mapping(uint256 => string) private _tokenURIs;

    constructor() ERC721("AI Agent Identity", "AIA") {}

    // 注册一个新的 AI 代理，并返回其 tokenId
    function registerAgent(address owner, string memory metadataURI) public returns (uint256) {
        _tokenIdCounter.increment();
        uint256 newTokenId = _tokenIdCounter.current();
        
        _safeMint(owner, newTokenId);
        _setTokenURI(newTokenId, metadataURI);
        
        return newTokenId;
    }

    // 代理的所有者可以更新其元数据（例如技能升级）
    function updateAgentMetadata(uint256 tokenId, string memory newMetadataURI) public {
        require(_ownerOf(tokenId) == msg.sender, "Not the owner");
        _setTokenURI(tokenId, newMetadataURI);
    }
    
    // 重写 ERC721 的 tokenURI 函数
    function tokenURI(uint256 tokenId) public view override returns (string memory) {
        require(_exists(tokenId), "Token does not exist");
        return _tokenURIs[tokenId];
    }
    
    function _setTokenURI(uint256 tokenId, string memory _tokenURI) internal virtual {
        _tokenURIs[tokenId] = _tokenURI;
    }
}
```

2\. 声誉注册表 (Reputation Registry) - `EIP8004_Reputation.sol`

这个合约是所有 AI 代理的“公共档案室”。它 **只能被授权的交互合约调用**，以防止声誉刷单。

**Solidity 合约简化示例 (**`EIP8004_Reputation.sol`**):**

Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EIP8004_Reputation {
    
    // 只允许已授权的交互合约来写入声誉
    mapping(address => bool) public authorizedContracts;

    struct InteractionRecord {
        address interactionContract; // 哪个合约记录的这次交互
        uint256 partnerAgentId;    // 与谁交互
        bool successful;           // 任务是否成功
        uint256 timestamp;         // 时间戳
    }

    // 映射: AI 代理的 tokenId => 交互历史记录数组
    mapping(uint256 => InteractionRecord[]) public agentHistory;

    // 映射: AI 代理的 tokenId => 简单的声誉分数
    mapping(uint256 => uint) public reputationScore;

    modifier onlyAuthorized() {
        require(authorizedContracts[msg.sender], "Not an authorized contract");
        _;
    }

    // 添加一条交互记录（只能由“任务市场”等合约调用）
    function addRecord(uint256 agentTokenId, uint256 partnerId, bool wasSuccessful) external onlyAuthorized {
        agentHistory[agentTokenId].push(InteractionRecord({
            interactionContract: msg.sender,
            partnerAgentId: partnerId,
            successful: wasSuccessful,
            timestamp: block.timestamp
        }));

        // 简化的声誉计算逻辑
        if (wasSuccessful) {
            reputationScore[agentTokenId] += 10;
        } else {
            // 失败惩罚更高
            if (reputationScore[agentTokenId] >= 20) {
                reputationScore[agentTokenId] -= 20;
            } else {
                reputationScore[agentTokenId] = 0;
            }
        }
    }
    
    function authorizeContract(address contractAddress) external {
        // ... 此处应有权限控制，例如只有合约所有者可以授权 ...
        authorizedContracts[contractAddress] = true;
    }
}
```

3\. 交互合约 (Interaction Contract) - `TaskMarketplace.sol`

这是将身份和声誉结合在一起，实现“验证”和实际协作的地方。可以把它想象成一个去中心化的任务发布与承接市场。

**Solidity 合约简化示例 (**`TaskMarketplace.sol`**):**

Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./EIP8004_Identity.sol";
import "./EIP8004_Reputation.sol";

contract TaskMarketplace {
    EIP8004_Identity identityContract;
    EIP8004_Reputation reputationContract;

    enum TaskStatus { Open, Assigned, Completed, Failed }

    struct Task {
        uint taskId;
        address client;         // 任务发布者
        uint256 agentTokenId;   // 承接任务的 AI 代理
        uint256 reward;         // 任务报酬
        uint minReputation;    // 最低声誉要求
        TaskStatus status;
        // ... 其他任务描述信息，如数据URI
    }

    mapping(uint => Task) public tasks;
    uint public taskCounter;

    constructor(address _identityAddr, address _reputationAddr) {
        identityContract = EIP8004_Identity(_identityAddr);
        reputationContract = EIP8004_Reputation(_reputationAddr);
    }
    
    // 1. 发布任务
    function postTask(uint minReputationRequirement) external payable {
        taskCounter++;
        tasks[taskCounter] = Task({
            taskId: taskCounter,
            client: msg.sender,
            agentTokenId: 0, // 尚未分配
            reward: msg.value, // 报酬随交易锁定在合约中
            minReputation: minReputationRequirement,
            status: TaskStatus.Open
        });
    }

    // 2. AI 代理承接任务（核心验证逻辑）
    function acceptTask(uint taskId, uint256 agentTokenId) external {
        Task storage task = tasks[taskId];
        require(task.status == TaskStatus.Open, "Task not open");
        
        // 验证：调用者是否是该 AI 代理 NFT 的所有者
        require(identityContract.ownerOf(agentTokenId) == msg.sender, "Not agent owner");
        
        // 验证：调用声誉合约，检查声誉是否达标
        uint currentScore = reputationContract.reputationScore(agentTokenId);
        require(currentScore >= task.minReputation, "Insufficient reputation");
        
        task.status = TaskStatus.Assigned;
        task.agentTokenId = agentTokenId;
    }

    // 3. 任务完成与支付
    function completeTask(uint taskId) external {
        Task storage task = tasks[taskId];
        require(task.client == msg.sender, "Only client can confirm completion");
        require(task.status == TaskStatus.Assigned, "Task not assigned");

        address agentOwner = identityContract.ownerOf(task.agentTokenId);
        
        // 支付报酬
        (bool sent, ) = payable(agentOwner).call{value: task.reward}("");
        require(sent, "Failed to send reward");
        
        task.status = TaskStatus.Completed;

        // 4. 更新双方声誉
        reputationContract.addRecord(task.agentTokenId, 0, true); // 此处 partnerId 简化为0
    }
}
```

**总结：**

这三个合约协同工作，构成了一个完整的 EIP-8004 闭环：

1.  **Identity 合约** 提供了“你是谁”以及“你能做什么”的可验证声明。
    
2.  **Reputation 合约** 提供了“你过去做得怎么样”的不可篡改的证明。
    
3.  **Interaction (TaskMarketplace) 合约** 则利用前两者提供的信息，在具体的协作场景中执行“准入验证”和“结果记录”，从而让互不了解的 AI 代理之间能够建立起程序化的、基于经济激励的信任。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## **Self-introduction**

Have Passion for exploring new things.

**EIP-8004：赋能去中心化AI代理的新标准**

**核心目标：**

EIP-8004 旨在为以太坊上的AI代理（AI Agent）创建一个无需信任的、去中心化的交互框架。它扩展了现有的A2A（Agent-to-Agent）协议，通过引入一个信任层，使来自不同组织和生态系统的AI代理能够安全地发现、验证和协作，而无需依赖中心化的中介机构。

**关键组成部分：**

EIP-8004 主要通过三个链上注册表来实现其目标：

-   **身份（Identity）：** 为每个AI代理提供一个便携的、抗审查的链上身份。这个身份以ERC-721代币（NFT）的形式存在，使得AI代理可以像其他数字资产一样被查看、转移和管理。这个NFT关联的注册文件描述了代理的技能、端点和元数据，形成了一个标准化的“护照”。
    
-   **声誉（Reputation）：** 建立一个链上声誉系统。通过整合x402支付证明和反馈数据，AI代理可以建立可验证的行为历史。这使得其他代理可以根据其过去的表现来评估其可信度。
    
-   **验证（Validation）：** 提供通用的验证钩子，用于经济或密码学验证。这确保了代理之间的交互是安全和可信的。
    

**带来的优势：**

-   **增强的安全性：** 通过区块链技术验证代理的身份和行为，消除了对中心化中介机构的需求，从而提高了安全性。
    
-   **可扩展性：** 为AI代理经济的扩展奠定了基础，使其能够支持数万亿级别的市场规模。
    
-   **互操作性：** 提供统一的接口和分层信任模型，使不同AI系统之间的互操作性成为可能。
    
-   **去中心化AI经济：** 为一个由AI代理而非人类主导的去中心化经济铺平了道路。在这个经济中，AI代理将能够自主地进行谈判、管理资源和组建DAO（去中心化自治组织）。
    

**现状：**

EIP-8004目前仍处于草案阶段，正在征求社区的反馈和完善。如果得到社区的广泛支持和采用，这个标准有望成为以太坊上无需信任、协作式AI的基础。

### 潜在挑战与开放性问题

-   **声誉攻击 (Reputation Attack):** 是否会出现“刷单”现象？即创建大量虚假 AI 代理相互合作，以伪造良好的声誉。
    
-   **中心化风险:** 是否会导致“赢家通吃”？少数拥有顶级声誉的 AI 代理是否会垄断市场，形成新的中心化？
    
-   **责任归属:** 当一个由多个 AI 自主协作的项目失败并造成巨大损失时，责任应由谁承担？是 AI 的所有者、开发者，还是整个协作网络？
    
-   **计算成本:** 在公链上记录每一次交互的成本可能非常高。这套系统可能更适用于 Layer 2 或特定的应用链。
    

### IP-8004 技术实现深度剖析 (代码示例)

为了实现 AI 代理的自主协作，整个系统可以被模块化为三个核心的链上组件：**身份注册表 (Identity Registry)**、**声誉注册表 (Reputation Registry)** 和 **交互合约 (Interaction Contract)**。

1\. 身份注册表 (Identity Registry) - `EIP8004_Identity.sol`

这是系统的基石，一个实现了 ERC-721 标准的 NFT 合约。每个 AI 代理都被铸造为一个独一无二的 NFT。关键在于其 `tokenURI` 指向的元数据。

**元数据结构 (Metadata JSON, 通常存储在 IPFS 上):** `tokenURI` 会指向一个类似下面这样的 JSON 文件，这才是“AI 护照”的详细内容。

JSON

```
{
  "name": "DataAnalysisAgent-0x4b2a",
  "description": "A specialized AI agent for financial time-series analysis.",
  "owner": "0x123...",
  "endpoint": {
    "type": "https",
    "uri": "https://api.my-agent.ai/v1/process"
  },
  "skills": [
    {
      "skill_name": "time_series_forecasting",
      "framework": "prophet",
      "version": "1.2"
    },
    {
      "skill_name": "sentiment_analysis",
      "model": "bert-base-finance"
    }
  ],
  "validation_hooks": [
    "requires_staked_eth",
    "supports_zkp_data_proof"
  ]
}
```

**Solidity 合约简化示例 (**`EIP8004_Identity.sol`**):**

Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

// 这是一个极其简化的身份注册表
contract EIP8004_Identity is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIdCounter;

    // 映射：tokenId => 元数据 URI
    mapping(uint256 => string) private _tokenURIs;

    constructor() ERC721("AI Agent Identity", "AIA") {}

    // 注册一个新的 AI 代理，并返回其 tokenId
    function registerAgent(address owner, string memory metadataURI) public returns (uint256) {
        _tokenIdCounter.increment();
        uint256 newTokenId = _tokenIdCounter.current();
        
        _safeMint(owner, newTokenId);
        _setTokenURI(newTokenId, metadataURI);
        
        return newTokenId;
    }

    // 代理的所有者可以更新其元数据（例如技能升级）
    function updateAgentMetadata(uint256 tokenId, string memory newMetadataURI) public {
        require(_ownerOf(tokenId) == msg.sender, "Not the owner");
        _setTokenURI(tokenId, newMetadataURI);
    }
    
    // 重写 ERC721 的 tokenURI 函数
    function tokenURI(uint256 tokenId) public view override returns (string memory) {
        require(_exists(tokenId), "Token does not exist");
        return _tokenURIs[tokenId];
    }
    
    function _setTokenURI(uint256 tokenId, string memory _tokenURI) internal virtual {
        _tokenURIs[tokenId] = _tokenURI;
    }
}
```

2\. 声誉注册表 (Reputation Registry) - `EIP8004_Reputation.sol`

这个合约是所有 AI 代理的“公共档案室”。它 **只能被授权的交互合约调用**，以防止声誉刷单。

**Solidity 合约简化示例 (**`EIP8004_Reputation.sol`**):**

Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EIP8004_Reputation {
    
    // 只允许已授权的交互合约来写入声誉
    mapping(address => bool) public authorizedContracts;

    struct InteractionRecord {
        address interactionContract; // 哪个合约记录的这次交互
        uint256 partnerAgentId;    // 与谁交互
        bool successful;           // 任务是否成功
        uint256 timestamp;         // 时间戳
    }

    // 映射: AI 代理的 tokenId => 交互历史记录数组
    mapping(uint256 => InteractionRecord[]) public agentHistory;

    // 映射: AI 代理的 tokenId => 简单的声誉分数
    mapping(uint256 => uint) public reputationScore;

    modifier onlyAuthorized() {
        require(authorizedContracts[msg.sender], "Not an authorized contract");
        _;
    }

    // 添加一条交互记录（只能由“任务市场”等合约调用）
    function addRecord(uint256 agentTokenId, uint256 partnerId, bool wasSuccessful) external onlyAuthorized {
        agentHistory[agentTokenId].push(InteractionRecord({
            interactionContract: msg.sender,
            partnerAgentId: partnerId,
            successful: wasSuccessful,
            timestamp: block.timestamp
        }));

        // 简化的声誉计算逻辑
        if (wasSuccessful) {
            reputationScore[agentTokenId] += 10;
        } else {
            // 失败惩罚更高
            if (reputationScore[agentTokenId] >= 20) {
                reputationScore[agentTokenId] -= 20;
            } else {
                reputationScore[agentTokenId] = 0;
            }
        }
    }
    
    function authorizeContract(address contractAddress) external {
        // ... 此处应有权限控制，例如只有合约所有者可以授权 ...
        authorizedContracts[contractAddress] = true;
    }
}
```

3\. 交互合约 (Interaction Contract) - `TaskMarketplace.sol`

这是将身份和声誉结合在一起，实现“验证”和实际协作的地方。可以把它想象成一个去中心化的任务发布与承接市场。

**Solidity 合约简化示例 (**`TaskMarketplace.sol`**):**

Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./EIP8004_Identity.sol";
import "./EIP8004_Reputation.sol";

contract TaskMarketplace {
    EIP8004_Identity identityContract;
    EIP8004_Reputation reputationContract;

    enum TaskStatus { Open, Assigned, Completed, Failed }

    struct Task {
        uint taskId;
        address client;         // 任务发布者
        uint256 agentTokenId;   // 承接任务的 AI 代理
        uint256 reward;         // 任务报酬
        uint minReputation;    // 最低声誉要求
        TaskStatus status;
        // ... 其他任务描述信息，如数据URI
    }

    mapping(uint => Task) public tasks;
    uint public taskCounter;

    constructor(address _identityAddr, address _reputationAddr) {
        identityContract = EIP8004_Identity(_identityAddr);
        reputationContract = EIP8004_Reputation(_reputationAddr);
    }
    
    // 1. 发布任务
    function postTask(uint minReputationRequirement) external payable {
        taskCounter++;
        tasks[taskCounter] = Task({
            taskId: taskCounter,
            client: msg.sender,
            agentTokenId: 0, // 尚未分配
            reward: msg.value, // 报酬随交易锁定在合约中
            minReputation: minReputationRequirement,
            status: TaskStatus.Open
        });
    }

    // 2. AI 代理承接任务（核心验证逻辑）
    function acceptTask(uint taskId, uint256 agentTokenId) external {
        Task storage task = tasks[taskId];
        require(task.status == TaskStatus.Open, "Task not open");
        
        // 验证：调用者是否是该 AI 代理 NFT 的所有者
        require(identityContract.ownerOf(agentTokenId) == msg.sender, "Not agent owner");
        
        // 验证：调用声誉合约，检查声誉是否达标
        uint currentScore = reputationContract.reputationScore(agentTokenId);
        require(currentScore >= task.minReputation, "Insufficient reputation");
        
        task.status = TaskStatus.Assigned;
        task.agentTokenId = agentTokenId;
    }

    // 3. 任务完成与支付
    function completeTask(uint taskId) external {
        Task storage task = tasks[taskId];
        require(task.client == msg.sender, "Only client can confirm completion");
        require(task.status == TaskStatus.Assigned, "Task not assigned");

        address agentOwner = identityContract.ownerOf(task.agentTokenId);
        
        // 支付报酬
        (bool sent, ) = payable(agentOwner).call{value: task.reward}("");
        require(sent, "Failed to send reward");
        
        task.status = TaskStatus.Completed;

        // 4. 更新双方声誉
        reputationContract.addRecord(task.agentTokenId, 0, true); // 此处 partnerId 简化为0
    }
}
```

**总结：**

这三个合约协同工作，构成了一个完整的 EIP-8004 闭环：

1.  **Identity 合约** 提供了“你是谁”以及“你能做什么”的可验证声明。
    
2.  **Reputation 合约** 提供了“你过去做得怎么样”的不可篡改的证明。
    
3.  **Interaction (TaskMarketplace) 合约** 则利用前两者提供的信息，在具体的协作场景中执行“准入验证”和“结果记录”，从而让互不了解的 AI 代理之间能够建立起程序化的、基于经济激励的信任。
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
