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
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->


# 2025.10.16
<!-- DAILY_CHECKIN_2025-10-16_START -->
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
