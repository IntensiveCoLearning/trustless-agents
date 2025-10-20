---
timezone: UTC+13
---

# Bruce Xu

**GitHub ID:** brucexu-eth

**Telegram:** @brucexu_eth

## Self-introduction

All in ETH x AI. Exploring the real world use cases on this direction.

## Notes
<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
[https://www.x402.org/](https://www.x402.org/)

An open protocol for internet-native payments. **The best way to accept digital payments.**

Built around the [HTTP 402](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) status code, **x402 enables users to pay for resources via API** without registration, emails, OAuth, or complex signatures.

### **1 Line of Code to Accept Digital Dollars**

```
paymentMiddleware("0xYourAddress", {"/your-endpoint": "$0.01"});
```

TODO this is a bad example, doesn't make things easier.

If a request arrives without payment, the server responds with HTTP 402, prompting the client to pay and retry.

```
HTTP/1.1 402 Payment Required
```

x402 allows any web developer to accept crypto payments without the complexity of having to interact with the blockchain.

TODO build a x402 demo and trigger the digital payment.

Seems server will return a 402 code, and client need to capture it and handle, like popup the metamask modal, etc.

[https://x402.gitbook.io/x402](https://x402.gitbook.io/x402)

With x402, any web service can require payment before serving a response, using crypto-native payments for speed, privacy, and efficiency.

### Why Use x402?

x402 addresses key limitations of existing payment systems:

-   **High fees and friction** with traditional credit cards and fiat payment processors
    
-   **Incompatibility with machine-to-machine payments**, such as AI agents
    
-   **Lack of support for micropayments**, making it difficult to monetize usage-based services
    

### What Can You Build?

x402 enables a range of use cases, including:

-   API services paid per request
    
-   AI agents that autonomously pay for API access
    
-   [Paywalls](https://x.com/MurrLincoln/status/1935406976881803601) for digital content
    
-   Microservices and tooling monetized via microtransactions
    
-   Proxy services that aggregate and resell API capabilities
    

### How Does It Work?

At a high level, the flow is simple:

1.  A buyer requests a resource from a server.
    
2.  If payment is required, the server responds with `402 Payment Required`, including payment instructions.
    
3.  The buyer prepares and submits a payment payload.
    
4.  The server verifies and settles the payment using an x402 facilitator's /verify and /settle endpoints.
    
5.  If payment is valid, the server provides the requested resource.
    

For more detail, see:

-   Client / Server
    
-   Facilitator
    
-   HTTP 402
    

TODO crypto payment friendly. seems need to have some validators or validation service, for checking the tx.

### Why x402 Uses HTTP 402

The primary purpose of HTTP 402 is to enable frictionless, API-native payments for accessing web resources, especially for:

-   Machine-to-machine (M2M) payments (e.g., AI agents).
    
-   Pay-per-use models such as API calls or paywalled content.
    
-   Micropayments without account creation or traditional payment rails.
    

Using the 402 status code keeps x402 protocol natively web-compatible and easy to integrate into any HTTP-based service.

TODO build a demo for purchasing ticket with x402 payment + agents registered on erc8004 and provide feedback.

TODO run this demo [https://x402.gitbook.io/x402/getting-started/quickstart-for-sellers](https://x402.gitbook.io/x402/getting-started/quickstart-for-sellers) and [https://x402.gitbook.io/x402/getting-started/quickstart-for-buyers](https://x402.gitbook.io/x402/getting-started/quickstart-for-buyers)

TODO check [https://github.com/coinbase/x402/blob/main/README.md](https://github.com/coinbase/x402/blob/main/README.md)
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->

[https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)

To maximize the benefits from agentic AI, it is critical for these agents to be able to collaborate in a dynamic, multi-agent ecosystem across siloed data systems and applications.

The A2A protocol will allow AI agents to communicate with each other, securely exchange information, and coordinate actions on top of various enterprise platforms or applications.

-   **Secure by default**: A2A is designed to support enterprise-grade authentication and authorization, with parity to OpenAPI’s authentication schemes at launch.
    

A2A facilitates communication between a "client" agent and a “remote” agent. A client agent is responsible for formulating and communicating tasks, while the remote agent is responsible for acting on those tasks in an attempt to provide the correct information or take the correct action.

several key capabilities:

-   **Capability discovery:** Agents can advertise their capabilities using an “Agent Card” in JSON format, allowing the client agent to identify the best agent that can perform a task and leverage A2A to communicate with the remote agent.
    

-   **Task management:** The communication between a client and remote agent is oriented towards task completion, in which agents work to fulfill end-user requests. This “task” object is defined by the protocol and has a lifecycle. It can be completed immediately or, for long-running tasks, each of the agents can communicate to stay in sync with each other on the latest status of completing a task. The output of a task is known as an “artifact.”
    

-   **Collaboration:** Agents can send each other messages to communicate context, replies, artifacts, or user instructions.
    

-   **User experience negotiation:** Each message includes “parts,” which is a fully formed piece of content, like a generated image. Each part has a specified content type, allowing client and remote agents to negotiate the correct format needed and explicitly include negotiations of the user’s UI capabilities–e.g., iframes, video, web forms, and more.
    

[https://a2a-protocol.org/latest/](https://a2a-protocol.org/latest/)

A2A is situated within a broader agent stack, which includes:

-   **A2A:** Standardizes communication among agents deployed in different organizations and developed using diverse frameworks.
    
-   **MCP:** Connects models to data and external resources.
    
-   **Frameworks (like ADK):** Provide toolkits for constructing agents.
    
-   **Models:** Fundamental to an agent's reasoning, these can be any Large Language Model (LLM).
    

### A2A Request Lifecycle[¶](https://a2a-protocol.org/latest/topics/what-is-a2a/#a2a-request-lifecycle)

The A2A request lifecycle is a sequence that details the four main steps a request follows: agent discovery, authentication, `sendMessage` API, and `sendMessageStream` API.

## Core Actors in A2A Interactions[¶](https://a2a-protocol.org/latest/topics/key-concepts/#core-actors-in-a2a-interactions)

-   **User**: The end user, which can be a human operator or an automated service. The user initiates a request or defines a goal that requires assistance from one or more AI agents.
    
-   **A2A Client (Client Agent)**: An application, service, or another AI agent that acts on behalf of the user. The client initiates communication using the A2A protocol.
    
-   **A2A Server (Remote Agent)**: An AI agent or an agentic system that exposes an HTTP endpoint implementing the A2A protocol. It receives requests from clients, processes tasks, and returns results or status updates. From the client's perspective, the remote agent operates as an _opaque_ (black-box) system, meaning its internal workings, memory, or tools are not exposed.
    

## Fundamental Communication Elements[¶](https://a2a-protocol.org/latest/topics/key-concepts/#fundamental-communication-elements)

The following table describes the fundamental communication elements in A2A:

| Element | Description | Key Purpose |
| --- | --- | --- |
| Agent Card | A JSON metadata document describing an agent's identity, capabilities, endpoint, skills, and authentication requirements. | Enables clients to discover agents and understand how to interact with them securely and effectively. |
| Task | A stateful unit of work initiated by an agent, with a unique ID and defined lifecycle. | Facilitates tracking of long-running operations and enables multi-turn interactions and collaboration. |
| Message | A single turn of communication between a client and an agent, containing content and a role ("user" or "agent"). | Conveys instructions, context, questions, answers, or status updates that are not necessarily formal artifacts. |
| Part | The fundamental content container (for example, TextPart, FilePart, DataPart) used within Messages and Artifacts. | Provides flexibility for agents to exchange various content types within messages and artifacts. |
| Artifact | A tangible output generated by an agent during a task (for example, a document, image, or structured data). | Delivers the concrete results of an agent's work, ensuring structured and retrievable outputs. |
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->


[https://www.quillaudits.com/blog/smart-contract/erc-8004](https://www.quillaudits.com/blog/smart-contract/erc-8004)

ERC-8004 Trustless Agents represents a fundamental breakthrough extending Google's proven Agent-to-Agent (A2A) protocol with blockchain-based trust mechanisms that enable autonomous agents to discover, validate, and collaborate across untrusted networks.

Agentic Economy

However, as adoption grew across leading technology firms, a critical limitation emerged, the protocol assumed trust between communicating agents. This worked perfectly within organizational boundaries where IT departments could establish trust relationships, but it prevented the emergence of a truly open agent economy.

One of ERC-8004's most sophisticated features is its tiered security architecture, where trust mechanisms scale with the value at risk. This addresses the fundamental insight that ordering pizza requires different security guarantees than medical diagnosis.

![Blank (1).webp](https://www.quillaudits.com/_next/image?url=https%3A%2F%2Fambitious-kindness-505c138052.media.strapiapp.com%2FBlank_1_17ecc28b4a.webp&w=1920&q=75)

For simple tasks, such as content creation or basic queries, social consensus based on accumulated client feedback provides sufficient security.

For financial transactions or smart contract operations, validators must stake economic value that can be slashed for incorrect validations.

Validator checks and validates the result from the Service Agent for Client Agent to execute further operations, like release the fund, etc. So Validator will be very important for building trustless. TODO Validators will have a marketplace, for different cases and scenoria. This can be a public goods for LXDAO.

### **Cryptographic Verification (High Stakes)**

For critical applications, Trusted Execution Environment (TEE) attestations provide cryptographic guarantees that computations executed correctly in secure hardware enclaves. TEEs offer several critical properties:

-   **Integrity**: Cryptographic proof that code executed as intended
    
-   **Confidentiality**: Private data remains encrypted even from cloud providers
    
-   **Remote Attestation**: Third parties can verify execution environment authenticity
    

TEE（Trusted Execution Environment，可信执行环境）是处理器里一块受硬件保护的隔离区域。它让代码和数据在“加密内存”里运行，操作系统、云管理员、恶意软件都看不见、改不了；还可用“远程证明”向外界证明自己运行的是哪段代码。TEE 不是 ERC-8004 的一部分，但可作为 **validator 的实现手段**。它给 validator 提供“在硬件隔离里跑校验逻辑 + 远程证明”的能力，用来降低对单一运营方的信任。

关系与分层

-   ERC-8004 定义接口：`validationRequest(...)` → off-chain 校验 → `validationResponse(...)`。
    
-   validator 的职责：拿到 `requestUri/requestHash`，执行校验，回写结果。
    
-   TEE 的作用：让这段校验逻辑在受硬件保护的环境中运行，并产出可验证的 **attestation**（证明“确实用这段代码、在可接受的TCB版本上、针对这笔请求计算了这个结果”）
    

三种常见落地模式

1.  纯信任型
    
    -   直接信任某个 validator 地址（公司/社区运营）。无需 TEE/zk。实现简单，信任重。
        
2.  **TEE-backed validator（常用）**
    
    -   校验代码部署在 TEE（SGX/TDX/SEV/TrustZone 或机密虚机）中。
        
    -   输出包含：结果摘要 + TEE 证明（绑定 `requestHash` 与代码测量值 H）。
        
    -   上链做法：
        
        -   最简：合约只存 `responseHash/tag`；证明放 `responseUri`，由审计者或仲裁合约离链验证。
            
        -   强校验：用预言机把厂商证明链验证后，喂给合约一个可链上验证的签名/布尔值；或把“允许的测量值/公钥”登记在链上做白名单校验。
            
3.  ZK-validator
    
    -   用 zk 生成可链上验证的证明。信任最小，但对通用校验成本高。可与 TEE 组合（如 zktls/zkDCAP 把 TEE 证明压成可链上验证的简证）。
        

最小工作流（以“验证外卖订单是否成立”为例）

1.  Registry 记录允许的 validator 列表，以及可选的 **TEE 测量值 H 或 enclave 公钥**。
    
2.  Agent 调 `validationRequest(validatorAddress, agentId, requestUri, requestHash)`。
    
3.  validator 的 **TEE** 拉取 `requestUri`，校验 `requestHash`，调用商家 API/签名票据，完成校验。
    
4.  TEE 生成 attestation，把 {`requestHash`, 结果摘要, nonce, TCB版本} 绑定在证明里。
    
5.  validator 调 `validationResponse(..., responseUri, responseHash, tag)`；`responseUri` 中含 attestation。
    
6.  需要链上强校验时，由预言机/仲裁合约核验 attestation 是否匹配登记的测量值/公钥，再认可该响应。
    

关键设计点

-   `validatorAddress` 仍是一个正常地址（EOA/合约）。TEE 只改变其**实现与证明**，不改变地址形态。
    
-   绑定与防重放：把 `requestHash`、区块高度/截止时间写进 TEE 证明或响应摘要。
    

The security model must address three critical dimensions: **establishing trust without prior relationships**, maintaining **reputation integrity across organizational boundaries**, and **validating authenticity in adversarial environments**.

[https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879](https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879)

That’s why I was happy in June when Google [donated](https://developers.googleblog.com/en/google-cloud-donates-a2a-to-linux-foundation/) their Agent2Agent protocol to the Linux Foundation to make it credibly neutral, with many BigTech companies jumping on board. I was happy… until I studied the specs (very well done, btw) and realized Web3/trustless use cases were ignored. **A2A assumes usage within organizations** — discovery and trust assumptions were overlooked.

Stake-secured validation? Look at [EigenLayer](https://blog.eigencloud.xyz/introducing-verifiable-agents-on-eigenlayer/). TEE attestations? Check out [Phala](https://phala.network/) and [Near.AI](http://Near.AI).

[https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d](https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d)

## **How it Works**

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
     

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/brucexu-eth/images/2025-10-19-1760834568350-image.png)

（Generated with ChatGPT)

TEE attestation proofs：安全的 validator 代码读取官方第三方数据等，确保中间内容和数据没有被篡改。

zkTLS proof 是把一次 **TLS 会话** 的关键安全性（服务器身份、握手正确性、会话内容的完整性）转化为一份 **零知识证明**。验证者在不见明文、不信任第三方的前提下，确认“这些字节确实来自某域名在某次真实的 TLS 会话”。

典型用法（最小例）

-   你想让合约相信“[https://api.example.com](https://api.example.com) 返回的价格=123”。
    
-   你与服务器完成 TLS 1.3，会话中抽取“价格字段”和“时间戳”，生成 zkTLS 证明并绑定域名与会话摘要。
    
-   合约验证证明后采信该价格，无需喂价预言机，也不泄露其它响应内容。
    

优势与限制

-   优势：无需信任硬件或单一喂价方；可在链上直接验证来源与完整性
    
-   限制：电路复杂与证明成本高；对 TLS 版本与特性有子集支持；需处理证书根信任与新鲜度策略。
    

## **Key Beneficiaries**

-   **Restaking services:** ERC-8004’s Validation Registry gives restaking networks a neutral hook to prove that an agent’s job was checked (or challenged) and to post the outcome. Restaking network like EigenCloud can route validations through their crypto-economic model via an AVS. Slashing will be governed by each AVS.
    
-   **TEEs and proof systems:** ERC-8004 explicitly supports a crypto-verifiable trust model: agents run tasks in TEEs (e.g., Intel SGX-based TEEs) and/or attach ZK proofs; validators then post a `ValidationResponse` that others can verify. In practice, TEEs give fast execution with remote attestation, while zk-coprocessors make those claims succinct and chain-verifiable—ideal for model inference checks, confidential data use, or re-running heavy computations off-chain.
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->



[https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098)

Some notes from forum, credits from their authors:

Reputons are a standard defined: [RFC 7071 - A Media Type for Reputation Interchange](https://datatracker.ietf.org/doc/html/rfc7071)

Creating a single (aggregate) reputation score is dangerous. ?

TODO validation logic is a bit complex

Could you please include a simple Solidity example (e.g., two agents ordering a pizza) showing how the ERC is used for escrowed payment? (for understandable historical reasons)?

we need to create an ETH denominated economy in the AI agents space, just like we did with NFTs. I believe the best way forward is to create capable AI agents, who will perform valuable tasks and have them demand payment in ETH.

**Single domain well known location:** I might want to host many agents at different URLs in the same domain. This would be possible in A2A, wouldn’t it? So my suggestion would be to use URLs rather than domains as the way to point to the agent.

The protocol doesn’t cover payments. We considered requiring payment proofs for giving feedback. We know some groups are working on an A2A payment extension for agents, based on x402. We like this approach and are connecting with them to ensure that their extension and ours (ERC-8004) work perfectly together.

But payment proofs should be referenceable in Reputation: what we can standardize is the hook: allow Feedback/Rating records to carry a lightweight reference to a payment proof so indexers can correlate economic activity with feedback.

How validation works in simple use case

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/brucexu-eth/images/2025-10-18-1760748356648-image.png)

Some ideas about validation:

-   Validation used for verify the agents have done something, esp to the external system
    
-   Validator might be provided by the service providers, or Independent, or others. But the validation will trust that validator's response
    
-   Other contracts like Escrow contracts relies on the validation to send tokens
    

TODO make a fake hotel booking demo with validation logic, and protect the privacy, remove the private hotel booking info.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->





Yesterday's recording has been uploaded.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->






## **Validation Registry1**

**This registry enables agents to request verification of their work and allows validator smart contracts to provide responses that can be tracked on-chain**.

After an agent finishes the task, they can call “validationRequest” on this contract. External “validator” can check whether the work was done correctly.

This function MUST be called by the owner or operator of _agentId_. TODO, multi-owners or company cases?

```
function validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external
```

TODO How does zkML proof, a TEE oracle, or a stake-secured re-execution network work for validation?

Validators -> validationResponse to give feedback and check result.

```
function validationResponse(bytes32 requestHash, uint8 response, string responseUri, bytes32 responseHash, bytes32 tag) external
```

TODO what is unit8 response used for? A: The _response_ is a value between 0 and 100, which can be used as binary (0 for failed, 100 for passed) or with intermediate values for validations with a spectrum of outcomes.

This function MUST be called by the _validatorAddress_ specified in the original request. TODO Service Agents specify the validatorAddress when request validation? How can they know which validator can help? If they specify one validator, is it trustless?

They both on-chain events. The entire audit trail—who asked for validation, who validated, when, and what the outcome was—lives on Ethereum (or the chosen L2).

That makes the result tamper-proof and composable: reputation systems, insurance funds, or downstream contracts can _trustlessly_ reference the validation outcome without needing an off-chain oracle.

The workflow might be:

1.  Server agent finishes a translation task -> validationRequest()
    
2.  Validator contract re-executes the model with the given inputs and checks a zk proof?? -> validationResponse()
    
3.  Client agent (or any dApp) reads the registry and releases payment only if passed == true.
    

TODO Validator need to re-executes the model, cost twice tokens. And the model might return differently, how to generate or check the zk proof and give a passed signal?

## **Rationale**

-   Agent communication protocols: AI primitives (MCP, A2A) and Web3 primitives such as wallet addresses, DIDs, and ENS names.
    
-   Feedback
    
-   **Gas Sponsorship**: Since clients don’t need to be registered anymore, any application can implement frictionless feedback leveraging [EIP-7702](https://eips.ethereum.org/EIPS/eip-7702). TODO build a demo that use 7702 to sponsor the gas for agent?
    
-   **Deployment**: We expect the registries to be deployed with singletons per chain. **Note that an agent registered and receiving feedback on chain A can still operate and transact on other chains.** Agents can also be registered on multiple chains if desired. TODO interop or cross chain deployment issue. How to archive “an agent registered and receiving feedback on chain A can still operate and transact on other chains?”
    

## Questions:

-   Privacy? if the agent will ask validator to verify their work?
    
-   How to build a validator?
    
-   Because agent uri and the service behind it might change, how can we make sure they are trustless always? What if they got hacked and replaced?
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->











First day has started!

Use case: discover, choose, and interact with agents. Break the organizational boundaries; Enabling open-ended agent economies.

Three trust models:

-   Reputation systems using client feedback
    
-   Validation via stake-secured re-rexecution
    
-   zkML proofs or TEE oracles
    

The agent communication in A2A lack of agent discovery and trust across organizations. For example, if agents registered in Google, it will be hard to discover and use in Microsoft. And also, different companies might worry about the agents from their competitors. Therefore, Ethereum is the best platform to store the information for agents, so that it can be discovered by all ecosystem.

ERC-8004 provides three lightweight registries which can be deployed on any L2 or on Mainnet as per-chain singletons:

-   Identity Registry: ERC-721 + URIStorage -> agent's registration file (AgentCard)
    
-   Reputation Registry: Posting and fetching feedback signals. Scoring and aggregation occur both on-chain and off-chain.
    
-   Validation Registry: Generic hooks for requesting and recording independent validators checks (e.g. stakers re-running the job, zkML verifiers, TEE oracles, trusted judges). TODO use cases?
    

### Identity Registry

-   Each agent is an ERC-721 with URIStorage extension
    
-   Each agent is uniquely identified globally by:
    
    -   _namespace:_ `eip155` for EVM chains
        
    -   _chainId_: The blockchain network identifier
        
    -   _identityRegistry_: The address where the ERC-721 registry contract is deployed
        
    -   _agentId_: The ERC-721 tokenId assigned incrementally by the registry
        
-   The owner of the ERC-721 token is the owner of the agent and can transfer ownership or delegate management (e.g., updating the registration file) to operators, as supported by `ERC721URIStorage`.
    
-   The **_tokenURI_** MUST resolve to the agent registration file
    
-   registration file includes:
    
    -   basic info
        
    -   endpoints: different types of endpoint (name, endpoint, capabilities, version), point to an A2A agent card, and MCP endpoint, DID, etc.
        
    -   registrations: agentId and Registry (eip155:1:{identityRegistry})
        
    -   supportedTrust: reputation, tee-attestation, crypto-economic, etc. is Optional. ERC is used only for discovery, not for trust.
        

Registry extends getMetadata(uint256 agentId, string key) and setMetadata(uint256 agentId, string key, bytes value) functions for optional extra on-chain agent metadata.

### Registration

```
function register(string tokenURI, MetadataEntry[] calldata metadata) returns (uint256 agentId)
```

## Reputation Registry

**As an agent accepts a task, it’s expected to sign a _feedbackAuth_ to authorize the _clientAddress_ (human or agent) to give feedback**. The feedback consists of a _score_ (0-100), _tag1_ and _tag2_ (left to developers’ discretion to provide maximum on-chain composability and filtering), a file uri pointing to an off-chain JSON containing additional information, and its KECCAK-256 file hash to guarantee integrity. We suggest using IPFS or equivalent services to make feedback easily indexed by subgraphs or similar technologies. For IPFS uris, the hash is not required.

-   How to sign a feedbackAuth? What's the workflow?
    
-   How does clientAddress give feedback?
    
-   How does KECCAK-256 file hash to guarantee integrity? By signing a signature?
    

```
function giveFeedback(uint256 agentId, uint8 score, bytes32 tag1, bytes32 tag2, string calldata fileuri, bytes32 calldata filehash, bytes memory feedbackAuth) external
```

The _score_ MUST be between 0 and 100. _tag1_, _tag2_, and _uri_ are OPTIONAL.

_feedbackAuth_ is a tuple with the structure (_agentId_, _clientAddress_, _indexLimit_, _expiry_, _chainId_, _identityRegistry_, _signerAddress_) signed using [EIP-191](https://eips.ethereum.org/EIPS/eip-191) or [ERC-1271](https://eips.ethereum.org/EIPS/eip-1271) (if _clientAddress_ is a smart contract).

> seems agent owner will provide a feedbackAuth tuple to clientAddress, after they invoked the agent, they can give feedback with that tuple.

The _signerAddress_ field identifies the agent owner or operator who signed.  
Verification succeeds only if: _agentId_, _clientAddress_, _chainId_ and _identityRegistry_ are correct, blocktime < _expiry_ and _indexLimit_ is greater than the last index of feedback received by that client for that _agentId_.

While in most cases _indexLimit_ is simply lastIndex + 1, it can be much higher. This allows _agentId_ to pre-authorize multiple feedback submissions, useful for agent watch tower use cases. TODO go check logic in smart contract.

> An agent watchtower is an off-chain service that continuously evaluates an agent and posts pre-authorized feedback entries on-chain without a new signature each time.
> 
> `lastIndex[agentId][clientAddress] < indexLimit`. Then it increments `lastIndex` and records the feedback.
> 
> Practically `indexLimit` caps how many feedbacks that `clientAddress` can submit under one authorization.
> 
> Example: 5-min pings for 7 days → 2016; set ~2100 and renew weekly.

_clientAddress_ can revoke feedback by calling:

```
function revokeFeedback(uint256 agentId, uint64 feedbackIndex) external
```

```
function readFeedback(uint256 agentId, address clientAddress, uint64 index) external view returns (uint8 score, bytes32 tag1, bytes32 tag2, bool isRevoked)
```

### off-chain feedback file structure

-   proof\_of\_payment? TODO this can be used for x402 proof of payment, how?
    

## **Validation Registry**

**This registry enables agents to request verification of their work and allows validator smart contracts to provide responses that can be tracked on-chain**. Validator smart contracts could use, for example, stake-secured inference re-execution, zkML verifiers or TEE oracles to validate or reject requests.

TODO, how does validation work?

**Validation Request**

Agents request validation by calling:

```
function validationRequest(address validatorAddress, uint256 agentId, string requestUri, bytes32 requestHash) external
```

This function MUST be called by the owner or operator of _agentId_.

TODO ---

## Questions

-   How does zkML proofs and TEE oracles work?
    
-   How does agent authentication works in A2A?
    
-   Code and address of deployed ERC-8004 singletons?
    
-   Where to store the reputation data? On-chain? Too expensive? But it can against spam.
    
-   TODO build the demo with AA accounts.
    
-   How to implement admin of an agent, if owner of agent is the NFT owner. We might have multiple admins for managing one agent. And we need to think about the use case in a company.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
