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
