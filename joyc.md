---
timezone: UTC+9
---

# hython

**GitHub ID:** joyc

**Telegram:** @hython

## Self-introduction

Web3 Product PM

## Notes
<!-- Content_START -->
# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
# **ERC-8004: Trustless Agents**

[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

**背景：**  
ERC-8004 把“发现、口碑、验证”三件事标准化为三套轻量注册表，为开放的 agent 经济提供可组合的信任层，补上 MCP/A2A 没覆盖的“谁、能不能信、谁来背书”的空白。

### **为什么有用（给产品/架构的直观价值）**

-   **可组合**：评分/验证事件在链上可被任意合约消费，离链再做复杂聚合；适合做 agent 目录、排行、质检与保险等上层生态。
    
-   **跨协议桥接**：注册文件里统一挂 **A2A、MCP、ENS、DID、钱包** 等端点，让通信层（会话/指令）与信任层（发现/评价/验证）解耦。
    
-   **成本/灵活度**：把大对象放离链（IPFS/HTTP）+ 链上存最小必要索引/哈希，既省 gas 又保留审计轨迹。围绕“哪些字段需要链上可读”社区仍在讨论中。
    

### **核心机制**

-   **Identity Registry（身份）**：把每个 agent 铸造成一枚 **ERC-721**（带 URIStorage），tokenURI 指向注册文件（含名称、说明、端点清单如 A2A/MCP/ENS/DID、agent 钱包等）。可多链/多注册，天然可浏览与转移。
    
-   **Reputation Registry（声誉）**：任何客户端地址（人/agent）都可在 agent 许可下提交 **0–100 分**的反馈，含可选标签与离链 JSON（IPFS 优先，链上存摘要/索引以便组合）。读接口支持按 reviewer/标签聚合。撤回与附加回应也有事件。
    
-   **Validation Registry（验证）**：agent 主动向某个 **validator 合约**发起验证请求（请求数据放离链 + 哈希承诺），validator 回写 **0–100** 的响应值与证据 URI（可多次更新，支持软/硬终局）。聚合读取接口可按 validator/tag 汇总。
    

> 提案刻意把**支付**排除在标准之外，但示例建议把 x402 支付证明等作为离链反馈字段一并记录。

### **最小落地路径**

1.  **部署 IdentityRegistry**（每链单例）→ register() 铸出 agentId → 设置 tokenURI 指向注册 JSON，填上 A2A/MCP/钱包等端点与 supportedTrust。
    
2.  **接单时**，agent 用 **EIP-191/ ERC-1271** 签出 feedbackAuth，授权某客户端地址可写反馈。客户端调用 giveFeedback(...) 上链；需要时可 revokeFeedback(...) 或附加 appendResponse(...)。查询用 getSummary(...) / readAllFeedback(...)。
    
3.  **需要强信任时**，调用 validationRequest(...) 指定 validator；待对方 validationResponse(...) 回写评分与证据。汇总用 getValidationStatus(...) / getSummary(...)。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
