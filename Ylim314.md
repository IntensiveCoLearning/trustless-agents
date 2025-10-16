---
timezone: UTC+8
---

# ChaplinX

**GitHub ID:** Ylim314

**Telegram:** @Tikey19

## Self-introduction

AI-WEB3-ETH

## Notes

<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
# 模块 1 - ERC-8004 信任基础

### 1\. 核心目标与解决的问题

-   **主题：** ERC-8004 协议（无需信任的代理）。
    
-   **目标：** 在去中心化、跨组织的 Web3 环境中，建立一个**无需预先信任**的 AI 代理经济体系。
    
-   **解决方案：** 最小化链上存储，通过**三个轻量级链上注册表**作为信任锚点。
    

### 2\. 三大核心支柱（注册表）

| 注册表 | 作用 | 核心机制和重要性 |
| 身份注册表 (Identity Registry) | 身份证件（ERC-721/NFT），用于发现代理。 | 代理身份是一个 NFT。其TOKENURL 指向一个链下 JSON 文件，文件包含代理能力、A2A/MCP 端点和钱包地址。 |
| 声誉注册表 (Reputation Registry) | 评论和评分区，用于评估代理信用。 | 客户端给分前，需代理提供 feedbackAuth 预授权（防止 Sybil 攻击）。链上存储评分（0-100）和标签，复杂评分逻辑在链下处理。反馈文件可集成 x402 支付证明，增加可信度。 |
| 验证注册表 (Validation Registry) | 第三方公证处，用于高风险任务审计。 | 提供了标准的ValidationRequest和 validationResponse接口。允许代理请求专业的验证器（如 ZK/TEE 证明）来审计任务结果。 |

### 3\. 学习挑战思考与个人观点

**挑战 ：代理身份系统**

-   **思考：** ERC-8004 的设计（基于 ERC-721AgentID）已经提供了一个坚实的链上主身份。因此，其他机制（如 ENS/DID/URL）都应作为其链下注册文件中的可选“端点”出现。
    
-   **原因：** ENS 或 DID 作为人类可读且去中心化的辅助身份是推荐的选择，但主身份应保持在 ERC-721 链上 ID。
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
