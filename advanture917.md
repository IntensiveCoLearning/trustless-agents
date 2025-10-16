---
timezone: UTC+8
---

# Zhaojie Li

**GitHub ID:** advanture917

**Telegram:** @liuguanyi17

## Self-introduction

I'm a senior student focusing on AI Agents and LLM toolchains, with experience in LangGraph and Python-based architectures. I'm exploring multi-agent collaborative and eager to learn how AI can integrate with blockchain through the Trustless Agents program while connecting with like-minded builders.

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
## **身份注册表**

-   用 ERC-721 标准来管理 agent 身份，使其可以用现有 NFT 工具展示、转移、组合。
    

-   每个 agent 有一个唯一的 `agentId`（即 ERC-721 的 `tokenId`）。
    

-   用 `tokenURI`（URIStorage 扩展）指向注册文件（注册元数据），可以是 `ipfs://...` 或 `https://...` 等。
    

一个注册文件结构如下：

```
 {
   "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1", 
   "name": "myAgentName",
   "description": "A natural language description of the Agent, which MAY include what it does, how it works, pricing, and interaction methods",
   "image": "https://example.com/agentimage.png",
     //以上字段是必备的元数据字段
     // endpoints 是可以选的
   "endpoints": [
     {
       "name": "A2A",
       "endpoint": "https://agent.example/.well-known/agent-card.json",
       "version": "0.3.0"
     },
     {
       "name": "MCP",
       "endpoint": "https://mcp.agent.eth/",
       "capabilities": {}, // OPTIONAL, as per MCP spec
       "version": "2025-06-18"
     },
     {
       "name": "OASF",
       "endpoint": "ipfs://{cid}",
       "version": "0.7" // https://github.com/agntcy/oasf/tree/v0.7.0
     },
     {
       "name": "ENS",
       "endpoint": "vitalik.eth",
       "version": "v1"
     },
     {
       "name": "DID",
       "endpoint": "did:method:foobar",
       "version": "v1"
     },
     {
       "name": "agentWallet",
       "endpoint": "eip155:1:0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb7"
     }
   ],
     // must ，Agent可以被多个地址注册
   "registrations": [
     {
       "agentId": 22,
       "agentRegistry": "eip155:1:{identityRegistry}"
     }
   ],
     //  Opitonal ,用于表示是否信任
   "supportedTrust": [
     "reputation",
     "crypto-economic",
     "tee-attestation"
   ]
 }
```

-   注册／更新／转移身份时要发出标准事件，并且返回一个 `agentId` 便于链上索引。
    

## **声誉注册表**

-   当Agent 接收任务的时候，他签署一个feedback 以授权clientAddress进行反馈（评分），这里可以附加tag 、指向链下附加信息的json文件的URI。
    

-   分析与聚合（平均分、筛选标签、筛选评价人等）可链上提供简单接口，也可由外部系统处理。
    
-   支持撤销反馈和追加响应。
    

## **验证注册表**

用于提供“任务验证”机制，让 agent 的结果可以被独立验证者核查，从而提高系统可信度，尤其在敏感或高价值任务场景。

-   Agents 可以请求别人对其输出进行验证（重做、zkML 验证、TEE 可信执行环境、预言机等机制）。
    
-   验证者（validators）向注册表提交响应（通过 `validationResponse`）表示验证结果（通过／失败／评分）。
    
-   可以对同一个请求发多次响应（象征“软终态 / 强终态”等不同阶段）
    
-   验证结果可被聚合、查询，用于信任判断。
    
-   激励机制（质押、惩罚、奖励）由外层验证协议管理，不强制在这个 registry 内部处理。
    

## [**erc-8004-example**](https://github.com/vistara-apps/erc-8004-example)

### **1\. 安装配置**

```
 git clone https://github.com/chaoschain/erc-8004-example.git
 cd erc-8004-example
 uv venv --python 3.10 
 uv pip install -r  requirements.txt
```

这里我是Windows环境(通过git bash 进入bash)

```
 .\bash.exe
 curl -L https://foundry.paradigm.xyz | bash
 foundryup
```

在`contracts\foundry.toml` 添加依赖项

```
 # Dependencies
 [dependencies]
 forge-std = { git = "https://github.com/foundry-rs/forge-std", version = "^1.0.0" }
```

```
 cd contracts
 forge install
 forge build
 cd .. && cp cp .env.example .env
 anvil
```

### **2\. 启动**

```
 python demo.py
```
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

### **了解 EIP-8004**

当前的Agent 协议更多是为了Agent的相互协作（如A2A），而EIP-8004 协议构建了一个信任层，为Agent提供了一个开放、可发现并且信任协作的设施。

该标准引入了三个注册表以实现信任层。

-   身份注册表：通过为每一个 Agent 分配一个基于 ERC-721 的唯一标识符，使得Agent 具有可移植、抗审查性。
    
-   声誉注册表：提供发布和获取反馈的接口，支持链上和链下的评分和聚合，促进代理之间的信任建立。
    
-   验证注册表：提供一个hook，用于请求和记录独立验证者的检查。（如重新执行验证、zkML等）
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
