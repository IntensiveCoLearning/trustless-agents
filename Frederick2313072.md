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
