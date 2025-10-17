---
timezone: UTC+8
---

# prefert

**GitHub ID:** YarenTang

**Telegram:** @one_h1t_wonder

## Self-introduction

bring self to web3

## Notes
<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
# ERC-8004 Demo

##   
1\. 合约层

```
contract AgentIdentityRegistry is ERC721 {
```

```
    struct Agent {
```

```
        string name;
```

```
        string description;
```

```
        string endpoint;      // MCP / A2A / HTTPS 等
```

```
        string metadataURI;   // 指向 IPFS JSON
```

```
        address owner;
```

```
    }
```

```
    mapping(uint256 => Agent) public agents;
```

```
    function registerAgent(string memory name, string memory description, string memory endpoint, string memory metadataURI) public {
```

```
        uint256 tokenId = totalSupply() + 1;
```

```
        agents[tokenId] = Agent(name, description, endpoint, metadataURI, msg.sender);
```

```
        _mint(msg.sender, tokenId);
```

```
    }
```

```
    function getAgent(uint256 id) public view returns (Agent memory) {
```

```
        return agents[id];
```

```
    }
```

```
}
```

## 2\. 声誉层

```
contract ReputationRegistry {
```

```
    struct Feedback {
```

```
        uint256 agentId;
```

```
        uint8 score;         // 0 - 100
```

```
        string comment;
```

```
        string uri;          // 可选 IPFS 反馈数据
```

```
        address from;
```

```
    }
```

```
    mapping(uint256 => Feedback[]) public feedbacks;
```

```
    function submitFeedback(uint256 agentId, uint8 score, string memory comment, string memory uri) public {
```

```
        feedbacks[agentId].push(Feedback(agentId, score, comment, uri, msg.sender));
```

```
    }
```

```
    function getAverageScore(uint256 agentId) public view returns (uint256) {
```

```
        uint256 total;
```

```
        for (Feedback f in feedbacks[agentId]) {
```

```
            total += f.score;
```

```
        }
```

```
        return total / feedbacks[agentId].length;
```

```
    }
```

```
}
```

## 3\. 验证层

```
contract ValidationRegistry {
```

```
    struct Validation {
```

```
        uint256 agentId;
```

```
        bool valid;
```

```
        string method;       // "stake", "zkML", "TEE", "manual"
```

```
        string proofURI;     // IPFS proof
```

```
        address validator;
```

```
    }
```

```
    mapping(uint256 => Validation[]) public validations;
```

```
    function submitValidation(uint256 agentId, bool valid, string memory method, string memory proofURI) public {
```

```
        validations[agentId].push(Validation(agentId, valid, method, proofURI, msg.sender));
```

```
    }
```

```
    function isAgentTrusted(uint256 agentId) public view returns (bool) {
```

```
        uint256 positive = 0;
```

```
        for (Validation v in validations[agentId]) {
```

```
            if (v.valid) positive++;
```

```
        }
```

```
        return positive > (validations[agentId].length / 2);
```

```
    }
```

```
}
```

## 结合DeepSeek的应用逻辑 belike

```
// 注册一个 DeepSeek AI agent
```

```
const agent = await AgentRegistry.registerAgent({
```

```
  name: "DeepSeek LLM Node Demo",
```

```
  description: "A trustless LLM service with DeepSeek model",
```

```
  endpoint: "https://deepseek-node.example/api",
```

```
  metadataURI: "ipfs://Qm...agent-metadata.json"
```

```
});
```

```
// 模拟用户任务调用
```

```
const response = await fetch(agent.endpoint + "/infer", {
```

```
  method: "POST",
```

```
  body: JSON.stringify({ prompt: "summarize this text..." }),
```

```
});
```

```
// 任务完成后提交声誉反馈
```

```
await ReputationRegistry.submitFeedback(agent.id, 95, "Accurate and fast", "ipfs://Qm...result.json");
```

```
// 验证者执行 zkML proof / stake 复验
```

```
await ValidationRegistry.submitValidation(agent.id, true, "zkML", "ipfs://Qm...proof.json");
```

```
// 最终信任评估
```

```
const trusted = await ValidationRegistry.isAgentTrusted(agent.id);
```

```
console.log("Agent Trusted:", trusted);
```

## **以上可实现**

-   去信任的 AI 节点注册；
    
-   用户端反馈形成声誉；
    
-   验证节点复验模型输出；
    
-   跨链共享可信 Agent 生态；
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->

## 整体运行流程

1.  **注册身份** → Agent 在 Identity Registry 注册。
    
2.  **发布任务** → Client Agent 找到 Server Agent。
    
3.  **执行任务** → Server Agent 完成工作。
    
4.  **请求验证** → Validator Agent 验证任务结果。
    
5.  **提交反馈** → Client Agent 授权反馈给 Server。
    
6.  **形成信誉** → 所有验证和反馈可在链上查询。  
    

| 特点 | 对开发者的好处 |
| --- | --- |
| 轻量级设计 | 只把必要的信任信息放链上，不烧 gas |
| 可插拔信任模型 | 可以选用“反馈制”或“质押制”验证 |
| 与 A2A 完全兼容 | 可直接在 A2A AgentCard 中添加链上身份字段 |
| 防伪造身份 | 使用签名和 CAIP-10 地址确保唯一性 |
| 开放生态 | 任意语言、框架的 Agent 都能接入 |
| 支持经济激励 | 可以结合 x402 支付协议进行结算 |
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->



# ERC 8004


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
# ERC 8004

## 背景

当前已有的 Agent 通信协议（例如 MCP、A2A）能够在网络中实现交互与协作，但缺乏：

-   agent 身份真实性保证；
    
-   跨组织的信任与发现机制。
    

EIP-8004 因此提出一个“轻量级链上信任层”，通过注册、声誉与验证机制，让 Agent 网络能够在无需中心化信任的前提下进行自治协作。

* * *

## 三要素

### 1\. Identity Registry

-   使用 **ERC-721 + URIStorage** 实现，每个 agent 对应一个 NFT。
    
-   `tokenURI` 指向注册文件，可存放在 IPFS 或 HTTPS。
    
-   注册文件包含：
    
    -   `name`, `description`, `image`
        
    -   多种 endpoint（A2A、MCP、ENS、DID、Wallet 等）
        
    -   支持的信任模型说明
        
-   提供基础的 discoverability（可发现性）和注册一致性。
    

### 2\. Reputation Registry

-   agent 在交互后可授权客户端提交反馈。
    
-   反馈结构包括：
    
    -   `score`（0–100）
        
    -   `tag1`, `tag2`
        
    -   `uri`（可选的 IPFS JSON 文件）
        
    -   `hash`（完整性校验）
        
-   链上存储核心指标，链下可扩展复杂评分算法与历史分析。
    

### 3\. Validation Registry

-   记录独立验证者的验证结果，用于增强 agent 信任度。
    
-   支持多种验证方式：
    
    -   stake-based re-execution
        
    -   zkML proof
        
    -   TEE attestation
        
    -   Trusted judge
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## 背景

当前已有的 Agent 通信协议（例如 MCP、A2A）能够在网络中实现交互与协作，但缺乏：

-   agent 身份真实性保证；
    
-   跨组织的信任与发现机制。
    

EIP-8004 因此提出一个“轻量级链上信任层”，通过注册、声誉与验证机制，让 Agent 网络能够在无需中心化信任的前提下进行自治协作。

* * *

## 三要素

### 1\. Identity Registry

-   使用 **ERC-721 + URIStorage** 实现，每个 agent 对应一个 NFT。
    
-   `tokenURI` 指向注册文件，可存放在 IPFS 或 HTTPS。
    
-   注册文件包含：
    
    -   `name`, `description`, `image`
        
    -   多种 endpoint（A2A、MCP、ENS、DID、Wallet 等）
        
    -   支持的信任模型说明
        
-   提供基础的 discoverability（可发现性）和注册一致性。
    

### 2\. Reputation Registry

-   agent 在交互后可授权客户端提交反馈。
    
-   反馈结构包括：
    
    -   `score`（0–100）
        
    -   `tag1`, `tag2`
        
    -   `uri`（可选的 IPFS JSON 文件）
        
    -   `hash`（完整性校验）
        
-   链上存储核心指标，链下可扩展复杂评分算法与历史分析。
    

### 3\. Validation Registry

-   记录独立验证者的验证结果，用于增强 agent 信任度。
    
-   支持多种验证方式：
    
    -   stake-based re-execution
        
    -   zkML proof
        
    -   TEE attestation
        
    -   Trusted judge
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
