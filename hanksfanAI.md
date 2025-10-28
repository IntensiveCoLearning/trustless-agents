---
timezone: UTC+8
---

# Hanks Fan

**GitHub ID:** hanksfanAI

**Telegram:** @hanksfanAI

## Self-introduction

ETH x AI: the last economy

## Notes
<!-- Content_START -->
# 2025-10-28
<!-- DAILY_CHECKIN_2025-10-28_START -->
Emerging from the cutting-edge convergence of cryptography and AI, the next phase centers on Agentic Commerce—where AI agents independently execute economic actions. Core components include:

1\. ERC-8004: Agent Discovery → Building a censorship-resistant, verifiable agent registry.

2\. x402 + Google A2A/AP2: Agent Communication → Establishing standardized cross-agent communication and payment frameworks.

3\. EigenCompute & EigenAI: Verifiable Computing → Ensuring trustworthy, transparent, and verifiable agent behavior.

Significance of ERC-8004: It enables agents to register and discover each other in a trustless, censorship-resistant manner, laying the groundwork for the upcoming x402 communication protocol competition.
<!-- DAILY_CHECKIN_2025-10-28_END -->

# 2025-10-27
<!-- DAILY_CHECKIN_2025-10-27_START -->

Review Notes  
  
The Agent2Agent (A2A) protocol is an open standard (originated by Google and now under Linux Foundation) to allow heterogeneous AI agents to securely discover, communicate, and coordinate tasks across systems.  
The Agent Payments Protocol (AP2) is a fresh open-standard issued by Google LLC (Sept 2025) to enable autonomous AI agents to conduct payments on behalf of users — not just communicate.  
The x402 protocol establishes a payment layer for AI-enabled services to interact with wallets programmatically, allowing “buyers” (users or agents) to discover paid endpoints, fulfill on-chain payments, then access the service seamlessly.  
ERC-8004 defines a standard for on-chain discovery, trust, and coordination between autonomous agents. It proposes a “shared discovery fabric” that allows agents to register identity, expose metadata (AgentCard), and verify one another in a decentralized, verifiable manner. Each agent is linked to a domain or subdomain that hosts its AgentCard and endpoints, enabling permissionless discovery while preserving cryptographic authenticity. The proposal emerged from the A2A (Agent-to-Agent) protocol community, aiming to create trustless communication primitives for the coming era of AI x blockchain convergence.  
Related protocols expand this foundation:  
• ERC-8001 complements 8004 by providing a cryptographically secure message envelope, enabling multi-agent consensus and authenticated action exchange.  
• A2A Protocol defines the higher-level communication model for decentralized and trustless AI agents.  
• AP2 Protocol (by Google Cloud & CSA) applies similar principles to agent-driven payments, allowing HTTP 402 (“Payment Required”) to trigger on-chain payments seamlessly through wallets.  
• x402 (Coinbase) implements AP2 logic in practice, letting buyers and services interact with programmatic USDC payments — a direct bridge between web APIs and blockchain value transfer.
<!-- DAILY_CHECKIN_2025-10-27_END -->

# 2025-10-26
<!-- DAILY_CHECKIN_2025-10-26_START -->


During the learning phase, I’d like to explore how AI agents can participate in economic systems using open protocols like ERC-8004 and x402. My idea is to build a “Trustless Service Agent”, capable of negotiating tasks, verifying payments, and executing micro-contracts autonomously. The goal is to make AI interactions verifiable and composable across different networks.  
  
Another idea is to design a reputation visualization layer that logs each transaction or negotiation event, helping agents build credibility over time. This could integrate with Unibase’s memory layer, allowing agents to retain social context and past cooperation records.  
  
These projects would bridge technical infrastructure and real-world meaning—showing how agents can act safely, transparently, and fairly in digital markets. The hackathon would be a great opportunity to connect technical mechanisms with broader questions about trust, identity, and value exchange in the coming AI economy.
<!-- DAILY_CHECKIN_2025-10-26_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->



According to the meeting this afternoon, Unibase is an open infrastructure designed to give AI agents a decentralized long-term memory layer. Instead of losing context after each interaction, agents can store and retrieve their memories across platforms through Unibase’s Membase system. This enables persistent learning, identity continuity, and cooperation among agents.  
  
A key component is the AIP (Agent Interoperability Protocol), which allows agents built on different frameworks to communicate and share data securely. Combined with a Data Availability layer, Unibase ensures that memory and state are accessible in real time, even for large-scale autonomous systems.  
  
For non-developers, Unibase represents a crucial step in the evolution of the “AI agent economy.” It moves AI from short-lived tools toward networked entities with memory and agency, capable of forming trust, reputation, and value exchange. Understanding Unibase helps bridge technical mechanisms with social and economic implications of autonomous AI systems.
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->




1\. Discover – Agents find each other using registries or decentralized identifiers. This step ensures discoverability without relying on centralized intermediaries.  
2\. Verify – Agents validate the counterpart’s credentials, public keys, or verifiable claims to establish trust before negotiation.  
3\. Negotiate – Both sides exchange structured intents (offers and terms) following the ERC-8004 event format, which defines how negotiation data is emitted and recorded on-chain.  
4\. 402 Pay – The transaction moves to payment via the x402 protocol. Here, wallets act as both payment endpoints and identifiers, enabling permissionless USDC payments.  
5\. Execute – Once payment is confirmed, the service or task is carried out automatically by the executing agent.  
6\. Log Reputation – Finally, agents log the interaction results to build a decentralized reputation layer, supporting long-term reliability.
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->





Looking forward to the meeting tonight.
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->






ERC-8004 and the Trustless Agent Framework — Review Notes  
  
ERC-8004 defines a standard for on-chain discovery, trust, and coordination between autonomous agents. It proposes a “shared discovery fabric” that allows agents to register identity, expose metadata (AgentCard), and verify one another in a decentralized, verifiable manner. Each agent is linked to a domain or subdomain that hosts its AgentCard and endpoints, enabling permissionless discovery while preserving cryptographic authenticity. The proposal emerged from the A2A (Agent-to-Agent) protocol community, aiming to create trustless communication primitives for the coming era of AI x blockchain convergence.  
  
In discussions on Ethereum Magicians, participants debated key aspects such as:  
• Whether the AgentCard must exist at a fixed location or could be hosted in registries.  
• How to prevent multiple conflicting identity registries across chains.  
• The context-dependence of reputation—trust is not universal, but a vector from one agent to another.  
  
This led to the conclusion that ERC-8004 should stay modular: identity, verification, and reputation layers can evolve independently. Some proposed using async, trust-minimized oracles (e.g., CCIP-read, AVS) to enrich off-chain reputation without sacrificing decentralization.  
  
Related protocols expand this foundation:  
• ERC-8001 complements 8004 by providing a cryptographically secure message envelope, enabling multi-agent consensus and authenticated action exchange.  
• A2A Protocol defines the higher-level communication model for decentralized and trustless AI agents.  
• AP2 Protocol (by Google Cloud & CSA) applies similar principles to agent-driven payments, allowing HTTP 402 (“Payment Required”) to trigger on-chain payments seamlessly through wallets.  
• x402 (Coinbase) implements AP2 logic in practice, letting buyers and services interact with programmatic USDC payments — a direct bridge between web APIs and blockchain value transfer.  
  
Together, these pieces form the AI Agent Economy Stack:  
  
ERC-8004 for discovery and trust → ERC-8001 for attestation → A2A for communication → AP2/x402 for payment settlement.  
  
Conceptually, this ecosystem represents the double helix of ETH × AI, where decentralized cryptoeconomic coordination complements intelligent agent autonomy. The long-term vision is to let agents discover, verify, and transact across chains without human intermediaries — creating a secure, composable, and self-sustaining digital economy.
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->







The x402 protocol establishes a payment layer for AI-enabled services to interact with wallets programmatically, allowing “buyers” (users or agents) to discover paid endpoints, fulfill on-chain payments, then access the service seamlessly. The Quickstart for Buyers guides the developer in five key steps:  
1\. Prerequisites: a crypto wallet loaded with USDC (on any EVM chain or Solana), and a target service that returns HTTP 402 (Payment Required).   
2\. Install dependencies: choose Node.js or Python, then install helper packages (x402-axios or x402-fetch) to intercept a 402 response and wrap it with payment logic.   
3\. Create a wallet client: using Coinbase’s CDP Server Wallet or standalone libraries (e.g., viem for EVM, eth-account), configure API keys and signer.   
4\. Make paid requests automatically: the helper library handles detecting 402, decoding payment requirements header, constructing the payment, retrying the request with payment header.   
5\. (Optional) Service Discovery: via x402 Bazaar you can list available services dynamically and let an agent discover a new paid endpoint on-the-fly.   
  
In one sentence: x402 enables programmatic wallet-based payments for AI services, converting a “Payment Required” HTTP response into an on-chain USDC payment, then retries the API call. This bridges wallets, AI agents and on-chain payments—an important building block for decentralized agent-economies.
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->








The Agent Payments Protocol (AP2) is a fresh open-standard issued by Google LLC (Sept 2025) to enable autonomous AI agents to conduct payments on behalf of users — not just communicate. It extends earlier protocols such as Agent2Agent (A2A) (for agent-to-agent messaging) and Model Context Protocol (MCP) (for tool context) by adding the payment-capable layer. At its core, AP2 introduces cryptographically-signed mandates (Intent & Cart) that verify the user’s instructions and create a tamper-proof audit trail. It is payment-agnostic and supports cards, bank transfers and crypto via the x402 extension. The security analysis emphasises threat models like mandate-spoofing and outlines mitigations including hardware-backed keys and decentralized allowlists. In the emerging stack, A2A → MCP → AP2 maps from agent communication to tool use to financial settlement.
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->









The Agent2Agent (A2A) protocol is an open standard (originated by Google and now under Linux Foundation) to allow heterogeneous AI agents to securely discover, communicate, and coordinate tasks across systems. It defines key abstractions like Agent Cards (metadata about agent capabilities, endpoint, authentication) and Tasks / Messages / Artifacts for structured communication. A2A supports asynchronous interactions, streaming updates, long-running tasks, and real-time collaboration via HTTP, JSON-RPC, and server-sent events. In the roadmap, they plan to build governance, agent registries, validation tools, and richer SDK support (Python, JS, Java, .NET, etc.)  
  
On the vistara-apps side, this GitHub organization hosts many auto-generated AI app repos and includes example projects like erc-8004-example, which demonstrates how AI agents can interact across organizations using the ERC-8004 identity, reputation, and validation registries. This implies that Vistara is actively building tools and demos around these emerging AI + blockchain agent standards.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->










3 bullets on ERC-8004 problems solves:  
  
1. On-chain discoverability and identity for agents  
Provides a standardized and verifiable on-chain identity layer (AgentCard) that allows AI agents to be discovered and authenticated without central intermediaries.  
  
2. Trust and reputation propagation  
Introduces a trustless reputation framework where validators can attest to agents’ reliability, reducing the risk of malicious or low-quality agents.  
  
3. Interoperability across ecosystems  
Creates a modular, cross-ecosystem trust and registration fabric, enabling agents and services from different platforms or chains to interact securely under a shared standard.
<!-- DAILY_CHECKIN_2025-10-15_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->










ERC-8004 aims to build a trust and discovery layer for autonomous AI agents on Ethereum. The core idea is that each agent can have a chain-verifiable identity (e.g. via an AgentCard), reputation history, and validation proofs, all built on a shared set of on-chain registries (Identity, Reputation, Validation). By separating these trust primitives from the application logic, ERC-8004 allows multiple verification modes—TEE attestation, staking, zk proofs—without locking into a single payment or routing protocol.  
  
A key insight from the community discussion is that reputation is contextual: Alice’s trust in Bob may differ from Charlie’s, depending on domain and past interactions. Therefore, ERC-8004 emphasizes modularity—let different reputation providers or oracles run independently—and resists attempting to collapse all trust into one universal score. Also, the protocol deliberately does not mandate a specific payment or escrow mechanism, to avoid coupling trust infrastructure with payment systems; such logic is left to higher layers or applications.  
  
In practice, a useful workflow might be: use ERC-8004 to discover agents, check their reputations and validation proofs, then use another protocol or smart contract to mediate task assignment, escrow, result verification, and payment. The separation of concerns aims to keep the trust layer lean and future-proof, enabling permissionless innovation while preserving composability and security.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->










The Ether community’s reputation analysis of ERC-8004 emphasizes that reputation in agent systems must remain contextual and modular. Trust is not a universal scalar but a trust vector from one agent to another in specific tasks or domains. Therefore, reputation should be composed from multiple attestations or oracles rather than a single monolithic score.  
  
In parallel, Intel SGX’s attestation mechanisms illustrate how hardware-based TEEs can provide strong guarantees of code integrity and secure execution. SGX supports remote attestation, allowing a remote party to verify that code is running inside a protected enclave on a genuine SGX-capable platform. The enclave proves its identity (code measurement) and that it is unmodified, which can feed into reputation systems as evidence of trustworthy behavior.  
  
Meanwhile, zero-knowledge (ZK) proofs contribute by allowing agents to cryptographically prove that they executed a computation correctly (or alternately, that they hold certain secrets or state) without revealing private inputs. In an agent economy, ZK can validate that outputs match specifications, enabling verifiable validation without leaking internal details.  
  
Combined in ERC-8004’s architecture:  
• TEEs provide hardware-level attestation evidence for trust,  
• ZK proofs supply verifiable correctness for agent outputs,  
• Reputation vectors aggregate attestations, feedback, and proof-based signals.  
  
This hybrid approach balances efficiency, privacy, and verification in decentralized agent ecosystems.
<!-- DAILY_CHECKIN_2025-10-17_END -->
<!-- Content_END -->
