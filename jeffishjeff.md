---
timezone: UTC+8
---

# Jeff Huang

**GitHub ID:** jeffishjeff

**Telegram:** @jeffishjeff

## Self-introduction

Learning web3

## Notes
<!-- Content_START -->
# 2025-10-25
<!-- DAILY_CHECKIN_2025-10-25_START -->
x402 spec:

**HTTP flow sequence**: Client requests resource → if payment needed server returns 402 Payment Required with payment instructions → client prepares payment payload → client re-sends request with X-PAYMENT header (or similar) containing the payment payload → server verifies payment (via “facilitator” or direct) → server settles payment → server returns resource (200 OK) with optional X-PAYMENT-RESPONSE header. 

**Payment Requirements Schema**: The server’s 402 response includes a JSON object such as:

{ "x402Version": 1, "accepts": \[ { /\* paymentRequirement objects \*/ } \], "error": "optional message" }

**Payment Payload (Client → Server)**: The client uses the selected scheme and network/asset details to construct a cryptographic payload (signature or authorization) and attaches it in the X-PAYMENT header. The spec doesn’t fix one token type or chain—it is “chain & token agnostic”.  

**Verification/Settlement**: The server may verify payment locally (e.g., check transaction hash) or call a facilitator endpoint (e.g., /verify or /settle) to confirm the payment and then settle it (directly or via facilitator).

**Headers and Metadata**: The spec defines standard headers such as X-PAYMENT, X-PAYMENT-RESPONSE, and uses the 402 Payment Required HTTP status code to initiate the payment handshake.

x402 use cases:

**Pay-per-request APIs**: Services can monetize access to endpoints on a per-call basis rather than via subscriptions or keys. This fits x402’s design for “any HTTP resource can require payment via HTTP 402”.

**AI or agent-to-agent payments**: Autonomous agents (software bots, AI models) can request services or data and pay programmatically without human intervention or traditional credit-card flows.

**Microcontent paywalls**: For example, per-article access, streaming micro-services (per second/ per view), tiny payments (fractions of a cent) become viable.

**Machine-to-machine commerce / IoT**: Devices or services consuming data, compute or APIs can transact directly without setting up accounts, API keys or pre-funded credits.
<!-- DAILY_CHECKIN_2025-10-25_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->

Moving on to x402:

x402 is an open-internet payment protocol built around the HTTP status code 402 “Payment Required”. With this standard, when a client (which could be a human or an autonomous agent) requests access to a resource (API endpoint, content, data service), the server can respond with HTTP 402 and embed payment instructions in the response. The client then submits a signed payment payload (often a stablecoin transfer) and retries the request; once verified, the server grants access. 

The key design goals are:

-   Seamless integration into existing HTTP workflows (no heavy SDKs or credentialing required). 
    
-   Chain- and token-agnosticism, allowing payments across multiple networks and tokens (though currently many implementations focus on EVM + USDC via EIP-3009). 
    
-   Enabling machine-to-machine (M2M) or agent-driven commerce (e.g., AI agents paying for API calls) without the friction of traditional payments (accounts, API keys, subscriptions).
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->


More on A2A’s task model:

**Task Creation:**

A client agent sends a createTask request to a server (or performer) agent, defining the task type, input data, and optional context (e.g., deadlines, payment conditions, or execution preferences).

**Lifecycle Management:**

Once created, a task goes through a series of states — typically pending → running → completed or failed — with optional intermediate checkpoints.

This allows agents to coordinate **long-running or streaming processes** (like data analysis, code generation, or negotiation) that may span minutes or hours, unlike typical stateless HTTP calls.

**Progress & Validation:**

The performer agent can emit **progress events** or **intermediate results** while working. The client can listen for these via server-sent events (SSE) or WebSocket channels.

When done, the performer agent sends a TaskCompleted message with outputs or references (URLs, hashes, structured data).

Optionally, validation or reputation logic—like ERC-8004’s Validation Registry—can be layered on top to confirm that the output matches expectations before any payment or next step is triggered.
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->



Moving on to A2A

The A2A protocol is an open standard developed to enable autonomous AI agents—potentially built by different vendors or operating on different platforms—to _discover each other_, _communicate securely_, and _collaborate on tasks_ in a unified way. It introduces the concept of an “Agent Card” (a JSON profile that describes an agent’s capabilities, endpoints and security requirements), and defines a task-lifecycle model in which a “client” agent issues a task and a “remote” agent performs it, with real-time updates, streaming modality support (text, audio, video) and well-defined message schemas. 

A2A is built with five key principles: leveraging existing web standards (HTTP, JSON-RPC, SSE) to reduce integration friction; being secure by default (authentication, authorization, auditability); supporting long-running workflows (not just instant calls); being modality-agnostic (not limited to text); and promoting agent-centric collaboration (rather than isolated tool-invocations). The goal is to move beyond isolated AI “agents” and instead enable an ecosystem of interoperable, specialized agents that can coordinate across organizational and technical boundaries.
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->




More on ERC8004, watched the 1st community call and ETH Panda call.

Points on deployment / operational side:

-   Singleton deployment and global discoverability. ERC-8004 is designed to function through a **singleton registry per chain**—one contract each for Identity, Reputation, and Validation—so all agents reference a **shared source of truth**. This prevents fragmentation (multiple competing registries) and makes agent discovery and reputation lookup consistent across ecosystems. It also simplifies cross-chain bridging: different chains can mirror or checkpoint the same singleton entries, allowing an agent’s identity and trust data to travel with it.
    
-   Spam filtering in reputation. The Reputation Registry is intentionally open, which creates room for **rating spam and sybil noise**. Instead of hard limits, ERC-8004 encourages off-chain filtering layers—indexers, scoring services, oracles—that weight ratings by validator stake, validation history, or cryptographic signatures. This shifts “spam resistance” to the reputation algorithm rather than the base protocol, maintaining permissionlessness while enabling **trust-weighted aggregation** to surface reliable signals.
    
-   Flexibility of validation methods. ERC-8004’s Validation Registry is **method-agnostic**: any validator contract implementing the interface can register a method. That means a network can start with simple manual attestations, then later plug in **economic staking**, **zk-proof verifiers**, or **TEE attestations** without changing the base standard. This modularity makes it future-proof—validation can evolve with advances in cryptography, economics, or AI audit techniques, all while remaining interoperable under one unified schema.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->





### Learning ERC-8004

ERC-8004, also known as **“Trustless Agents,”** is a proposed Ethereum standard designed to enable autonomous or AI-driven agents to safely interact, transact, and collaborate with each other **without requiring pre-established trust**. It builds on the earlier Agent-to-Agent (A2A) protocol by introducing a **lightweight on-chain trust framework**, allowing agents from different domains or organizations to coordinate in an open ecosystem.

At its core, ERC-8004 defines three minimal registries: **Identity**, **Reputation**, and **Validation**. The **Identity Registry** lets agents publish verified metadata about who they are and what they can do; the **Reputation Registry** records community feedback after interactions; and the **Validation Registry** provides a mechanism for independent validators to attest that an agent’s claimed actions or outputs are correct. These registries serve as a shared trust substrate while leaving application-specific logic, payments, and data off-chain.

The motivation behind ERC-8004 is the rise of the **machine economy**—a world where AI agents negotiate services, exchange value, or manage digital assets on behalf of humans or organizations. By standardizing identity, reputation, and validation interfaces, ERC-8004 aims to make such autonomous systems interoperable and auditable across blockchains. In essence, it turns Ethereum into the **trust layer for AI and autonomous agents**, providing a minimal, composable foundation for decentralized cooperation between machines.
<!-- DAILY_CHECKIN_2025-10-15_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->





Deep dive on a couple ERC-8004 nuances:

-   **Identity: on-chain anchor, off-chain truth.** ERC-8004 lets any agent register an ID that points to an off-chain “AgentCard,” but it doesn’t enforce authenticity. Proving “who’s who” is done off-chain (DNS sigs, attestations, track record).
    

-   **Validation: a modular truth primitive.** Its Validation Registry records that “X validated result Y for task Z,” but doesn’t dictate how—you can use staking/slashing, zk/TEE proofs, or pure attestations. Because payouts/escrow can key off these records, validation becomes pluggable market infrastructure for trust, reusable across apps like an oracle for “was this done right?”.
    

Both feel vague and flimsy to be honest. While it's totally understandable why the standard is specified this way, would need to see more concrete/real world example to understand how it holds up and be useful.
<!-- DAILY_CHECKIN_2025-10-17_END -->
<!-- Content_END -->
