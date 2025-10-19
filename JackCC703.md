---
timezone: UTC+8
---

# 陈灿

**GitHub ID:** JackCC703

**Telegram:** @jackchencc

## Self-introduction

“大家好，我是陈灿，很高兴能参与’Let’s Build Trustless Agents (ERC-8004)’活动。我对区块链技术和去中心化AI代理有浓厚的兴趣，拥有ethdapp的开发和nft铸造的经验，熟悉erc721标准。我期待通过这次活动学习更多知识，与大家合作构建创新的解决方案。谢谢！”

## Notes
<!-- Content_START -->
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
**Agent Payments Protocol (AP2) 的安全使用框架**

-   **AP2 概述：** 它是 Agent2Agent (A2A) 和 Model Context Protocol (MCP) 的开放扩展，通过可验证凭证（VCs）形式的加密签名“授权书”（Mandates）来建立信任，而非仅依赖概率性 AI 推理。
    
-   **核心安全机制：** 使用签名授权书来要求确定的用户批准，以对抗 AI 幻觉和虚假交易。
    
-   **实施最佳实践包括：**
    
    -   **密钥管理：** 使用 TPM/HSM 进行签名；每 90 天轮换密钥；通过 DID 方法撤销受损密钥。
        
    -   **授权书验证：** 交易前验证商户签名；签署后检查哈希匹配。
        
    -   **注册表设置：** 使用类似于以太坊的账本为代理构建允许列表。
        
    -   **加密：** 对授权书有效载荷使用 AES-GCM-256；对跨角色传输使用 PGP。
        
    -   **升级协议：** 集成 3DS2；对于 Android，利用 GMSCore DPC 进行生物识别确认。
        
    -   **日志记录：** 将授权书存储在防篡改账本中；包括时间戳和代理 ID。
        

**目标：** 使开发者能够安全部署 AP2，同时促进代理商务创新。

**Google Agent Payments Protocol (AP2) 公告要点**

-   **发布方和日期：** Google Cloud 于 2025 年 9 月 16 日宣布。
    
-   **定义：** AP2 是一个开放、共享的协议，旨在安全地发起和执行由 AI 代理主导的跨平台支付交易，为代理和商户提供通用语言，防止生态系统碎片化。
    
-   **互操作性：** 它是 Agent2Agent (A2A) 协议和 Model Context Protocol (MCP) 的开放扩展。
    
-   **核心安全机制：**
    
    -   **授权书（Mandates）：** AP2 通过使用“授权书”（经过加密签名的防篡改数字合同）来构建信任。
        
    -   **可验证证据：** 授权书以可验证凭证（VCs）签名，作为用户指令的可验证证据，是每笔交易的基础。
        
-   **支持的支付类型：** 支持多种支付方式，包括信用卡、借记卡、稳定币和实时银行转账。
    
-   **生态合作：** 协议的发布得到了包括 Mastercard、American Express、PayPal、Coinbase、Adyen 等 60 多家公司的支持与贡献。
    
-   **重要性：** AP2 旨在解决现有支付系统在 AI 代理进行交易时出现的授权、真实性和问责制等挑战，为 AI 驱动的商务建立安全、可互操作的生态系统。
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->

运行的时候一直在报错，排查不出原因

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/JackCC703/images/2025-10-18-1760763722256-image.png)
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->


## **ERC-8004目标**

**ERC-8004** 旨在解决代理跨越组织边界进行交互时的信任问题，提供一个标准的发现框架，使自治 AI 代理能够去信任地发现和交易。

## 内容

**三个核心注册表**

1\. **身份（Identity）**：每个 8004 代理都有一个唯一的 ID、地址和域指针。代理的能力（如技能、支持的协议和信任模型）存储在链下 JSON 文件中，链上注册表仅维护 ID 与其当前能力的不可变链接。

2\. **声誉（Reputation）**：当代理接受任务时，它会预授权客户留下反馈。实际数据存在链下，但授权事件会在链上创建永久的审计追踪，任何人都可以爬取反馈历史并构建自己的声誉算法。

3\. **验证（Validation）**：代理可以通过两种主要机制进行独立验证：

• **加密经济验证（Crypto-economic validation）**：验证者质押资本并重新执行计算，如果验证错误则会被罚没（slashed）。

• **密码学验证（Cryptographic validation）**：使用 TEE（可信执行环境）或 ZK（零知识证明）来证明执行的正确性。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->



今天部署了ERC-8004合约并与之交互了

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/JackCC703/images/2025-10-16-1760614208342-image.png)

并且在本地部署

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/JackCC703/images/2025-10-16-1760614283552-image.png)![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/JackCC703/images/2025-10-16-1760614330679-image.png)
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->




### Problems Solved by ERC-8004

1.  **Agent Discovery Challenge**: Existing protocols cannot efficiently discover cross-organizational agents in a trustless environment. ERC-8004 provides portable NFT identifiers and registration files through the Identity Registry (based on ERC-721), achieving globally unique and browsable agent discovery.
    
2.  **Trust Deficiency Issue**: The lack of standardized trust mechanisms makes it difficult to open up the agent economy. ERC-8004 introduces the Reputation Registry, supporting on-chain/off-chain feedback aggregation (such as scores and tags), building a reputation system based on customer feedback, and mitigating Sybil attacks.
    
3.  **Insufficient Risk-Stratified Verification**: Low/high-risk tasks (such as ordering pizza vs. medical diagnosis) require proportional security, but there are no universal hooks. The Validation Registry of ERC-8004 provides pluggable models (such as zkML, TEE), allowing requests for independent verification to ensure output reliability.
    

### **My question**

**ERC-8004 How to solve the behavior of someone maliciously scoring low or scoring?**
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
