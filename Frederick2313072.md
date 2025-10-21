---
timezone: UTC+8
---

# frederick

**GitHub ID:** Frederick2313072

**Telegram:** @chocolatealike

## Self-introduction

ai转web3，小白捏，希望一起学习

## Notes

<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
x402 is an open payments protocol developed by Coinbase that enables AI agents to complete transactions autonomously. It is powered by onchain technology and digital currencies (primarily stablecoins like USDC) and provides a lightweight, secure, and instantaneous payment system that we hope can help accelerate the adoption of M2M payments and agentic commerce. The x402 protocol utilizes the long-reserved HTTP 402 ”Payment Required” status code to require a payment to complete an API request or load a webpage. If an API request lacks payment, x402 responds with an HTTP 402 Payment Required status, prompting the client to pay and retry. With this simple protocol, x402 removes the need for API keys, accounts, and subscriptions. x402 enables any API or content provider to accept pay-per-use payments through a lightweight middleware that integrates seamlessly into existing infrastructures.
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->

## Core Actors in A2A Interactions[¶](https://a2a-protocol.org/latest/topics/key-concepts/#core-actors-in-a2a-interactions)

-   **User**: The end user, which can be a human operator or an automated service. The user initiates a request or defines a goal that requires assistance from one or more AI agents.
    
-   **A2A Client (Client Agent)**: An application, service, or another AI agent that acts on behalf of the user. The client initiates communication using the A2A protocol.
    
-   **A2A Server (Remote Agent)**: An AI agent or an agentic system that exposes an HTTP endpoint implementing the A2A protocol. It receives requests from clients, processes tasks, and returns results or status updates. From the client's perspective, the remote agent operates as an _opaque_ (black-box) system, meaning its internal workings, memory, or tools are not exposed.
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->


1.  Initialize and register agents to the identity registry. There are 3 types of agents. Client agent assigns task to server agent and provides feedback. Server agent accepts task and feedback. Validator agent validates task, leveraging different trust models.
    
2.  Client agent discovers server agent by reading agent cards, then negotiates the job outputs. This negotiation is done offchain.
    
3.  When the server agent accepts the job request, it also accepts feedback from the client agent once the task is completed.
    
4.  Server agent executes the task and publishes a data hash that commits to all the information needed to re-run the job.
    
5.  Server agent then also requests for a validation via `ValidationRequest`_._
    
6.  Validator agent watches for these requests and validates using crypto-economic security or crypto verification.
    
7.  If successfully verified, the validator agent responds with a `ValidationResponse`**_._**
    
8.  With the `ValidationResponse` , this trustless setup ensures that payment can be released from escrow for various services executed correctly.
    
9.  After seeing the validation, the client agent publishes a feedback attestation that embeds the datahash, participants, 8004-request/response IDs, allowing the results to be queryable.
    
10.  Payments, attribution, incentives, slashing are not accounted for in ERC-8004, leaving room for design flexibility during and post task execution.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->



## EIP-8004 Official Standard

**EIP-8004 (ERC-8004)** 是一项**以太坊改进提案** ，旨在为跨去中心化网络运行的**自主 AI 代理引入一种无需信任的协调标准** 。它并非 ERC-20 那样的代币标准，而是一个协议基础架构，它通过基于区块链的**身份、声誉和验证层**扩展了 Google 的**代理到代理 (A2A)** 通信框架。

### 组件

Identity Registry

基于 [ERC-721](https://eips.ethereum.org/EIPS/eip-721) 的最小链上句柄，带有 URIStorage 扩展，可解析为代理的注册文件，为每个代理提供可移植的、抗审查的标识符。

身份注册中心使用 ERC-721 和 URIStorage 扩展进行代理注册，使**所有代理均可立即通过兼容 NFT 的应用程序进行浏览和转移** 。每个代理都通过以下方式进行全局唯一标识：

-   _namespace:_ `eip155` for EVM chains
    
    _命名空间：_ EVM 链的 `eip155`
    
-   _chainId_: The blockchain network identifier
    
    _chainId_ ：区块链网络标识符
    
-   _identityRegistry_: The address where the ERC-721 registry contract is deployed
    
    _identityRegistry_ ：部署 ERC-721 注册合约的地址
    
-   _agentId_: The ERC-721 tokenId assigned incrementally by the registry
    
    _agentId_ ：注册表逐步分配的 ERC-721 tokenId
    

如何设置链上原数据？

通过添加 getMetadata(uint256 agentId, string key) 和 setMetadata(uint256 agentId, string key, bytes value) 函数来扩展 ERC-721，以获得可选的额外链上代理元数据。

如何register？

```python
struct MetadataEntry {
string key;
bytes value;
}

function register(string tokenURI, MetadataEntry[] calldata metadata) returns (uint256 agentId)

function register(string tokenURI) returns (uint256 agentId)

// tokenURI is added later with _setTokenURI()
function register() returns (uint256 agentId)
```

Reputation Registry

用于发布和获取反馈信号的标准接口。评分和聚合既可以在链上进行（以实现可组合性），也可以在链下进行（以实现复杂的算法），从而为代理人评分、审计师网络和保险池打造一个专业化的服务生态系统。

当部署信誉注册表时， _identityRegistry_ 地址将传递给构造函数，并通过调用以下方式公开显示：

```python
**function** getIdentityRegistry() external view returns (address identityRegistry)
```

为什么链下数据不是必须的？

**当代理接受任务时，需要签署一个 _feedbackAuth_ 以授权 _clientAddress_ （人或代理）提供反馈** 。反馈包含一个_分数_ (0-100)、 _tag1_ 和 _tag2_ （由开发者自行决定，以提供最大的链上可组合性和过滤功能）、一个指向包含附加信息的链下 JSON 文件 URI，以及用于保证完整性的 KECCAK-256 文件哈希。建议使用 IPFS 或同等服务，以便反馈能够轻松地通过子图或类似技术进行索引。对于 IPFS URI，哈希值并非必需。除_分数_之外的所有字段都是可选的，因此链下文件不是必需的，可以省略。

feedback

1.验证

验证仅当 _agentId_ 、 _clientAddress_ 、 _chainId_ 和 _identityRegistry_ 正确，blocktime < _到期_ ，且 _indexLimit_ 大于该客户端针对该 _agentId_ 收到的最后一个反馈索引时才成功。虽然在大多数情况下 _indexLimit_ 等于 lastIndex + 1，但实际值可以更高。

2.事件

```python

event NewFeedback(uint256 indexed agentId, address indexed clientAddress, uint8 score, bytes32 indexed tag1, bytes32 tag2, string fileuri, bytes32 filehash)
```

3.聚合

当代理给出反馈时（即客户端是代理），代理应该使用链上可选 walletAddress 元数据中设置的地址作为 clientAddress，以促进声誉聚合。

Validation Registry

用于请求和记录独立验证器检查的通用挂钩（例如，重新运行作业的利益相关者、zkML 验证者、TEE 预言机、受信任的法官）。

代理通过以下方式请求验证：

```python
**function** validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external
```
<!-- DAILY_CHECKIN_2025-10-17_END -->
<!-- Content_END -->
