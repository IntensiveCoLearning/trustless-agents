---
timezone: UTC+8
---

# Cooper

**GitHub ID:** qingfengzxr

**Telegram:** @icooperhero

## Self-introduction

大家好，我叫Cooper，一名区块链开发工程师，Web3爱好者。

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
## 1.阅读了其他同学的笔记，获得了对ERC-8004的一些新的想法。

## **This Protocol Enables**

-   Agent discovery (capabilities, communication endpoints, supported trust models, etc.)
    
-   Marketplaces and agent explorers to be created.
    
-   Builds reputation systems; all feedback becomes public goods.
    

## **Security Considerations**

-   Sybil attacks to manipulate feedback are possible to inflate fake agents.
    
-   Audit trail thanks to immutability.
    
-   Validation incentives and slashing are managed by other protocols.
    
-   Capabilities cannot be guaranteed based on what the agents describe. The three trust models (reputation, validation, and TEE attestation) are designed to support this verification need.
    

## 2.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

首先阅读了EIP-8004的提案内容：[https://eips.ethereum.org/EIPS/eip-8004。](https://eips.ethereum.org/EIPS/eip-8004。)

了解到了EIP-8004是对于A2A协议的一个扩展，以加入使用区块链技术来实现TrustLess的目标。协议主要利用TokenURI来进行链下协作，信任问题则由链上解决。

以下为关键内容的引用：

* * *

为了构建一个开放的、跨组织的代理经济，我们需要在不可信环境下发现并信任代理的机制。本 ERC 通过三个轻量级注册中心来满足这一需求，这些注册中心可以作为单例部署在任何 L2 或主网上：

**Identity Registry** - A minimal on-chain handle based on [ERC-721](https://eips.ethereum.org/EIPS/eip-721) with URIStorage extension that resolves to an agent’s registration file, providing every agent with a portable, censorship-resistant identifier.

**Reputation Registry** - A standard interface for posting and fetching feedback signals. Scoring and aggregation occur both on-chain (for composability) and off-chain (for sophisticated algorithms), enabling an ecosystem of specialized services for agent scoring, auditor networks, and insurance pools.

**Validation Registry** - Generic hooks for requesting and recording independent validators checks (e.g. stakers re-running the job, zkML verifiers, TEE oracles, trusted judges).
<!-- DAILY_CHECKIN_2025-10-15_END -->

# 2025.10.15
<!-- Content_END -->
