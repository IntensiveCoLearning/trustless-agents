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
