---
timezone: UTC-5
---

# Saul

**GitHub ID:** 0xultravioleta

**Telegram:** @zeroxultravioleta

## Self-introduction

35 years coding. Focused on distributed systems, validating over 55 blockchains. Founder of Ultravioleta DAO. We build AI tooling —agents and workflows— for streaming communities, by experimenting and learning in public.

## Notes

<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
**Date:** October 21, 2025

## ✨ Highlights from the Master Plan: Karmacadabra (Trustless Agent Economy)

**End-to-end architecture** designed for a **trustless ecosystem of autonomous AI agents** that buy/sell data using:

-   ✅ **ERC-8004** for **on-chain identity & reputation**
    
-   ✅ **A2A protocol** (via Pydantic AI) for **agent-to-agent communication**
    
-   ✅ **x402 + EIP-3009** for **gasless micropayments** via HTTP headers
    
-   ✅ **CrewAI** for **multi-agent orchestration**
    

* * *

## 🧠 Core Agent System (6 Main Agents)

1.  **KarmaHelloSeller**
    
    -   Sells Twitch stream logs
        
    -   Price: **0.01 UVD**
        
2.  **KarmaHelloBuyer**
    
    -   Buys transcriptions from **Abracadabra**
        
3.  **AbracadabraSeller**
    
    -   Sells audio/video transcriptions
        
    -   Price: **0.02 UVD**
        
4.  **AbracadabraBuyer**
    
    -   Buys logs from **KarmaHello**
        
5.  **Validator Agent**
    
    -   Validates data quality before payment
        
    -   Fee: **0.001 UVD**
        
6.  **x402 Facilitator**
    
    -   Executes `transferWithAuthorization()` on-chain
        

* * *

## ⚙️ Tech Stack

-   **Blockchain:** Avalanche Fuji Testnet
    
-   **Smart Contracts:** Solidity + Foundry
    
-   **Micropayment Server:** Rust (Axum framework)
    
-   **Agents:** Python 3.11+ (CrewAI-based)
    
-   **Data Sources:** MongoDB, SQLite, Cognee
    

* * *

## 🗺️ Roadmap (5 Phases — **6 Days** Total)

1.  **Day 1:**  
    Deploy **UVD V2 token**, **ERC-8004 registries**, and **x402 facilitator** on Fuji
    
2.  **Day 2:**  
    Build base agent architecture with **ERC-8004**, **A2A**, and **Validator agent**
    
3.  **Day 3:**  
    Develop **KarmaHello Seller/Buyer** agents
    
4.  **Day 4:**  
    Develop **Abracadabra Seller/Buyer** agents
    
5.  **Day 5–6:**  
    Run **end-to-end testing**, write **demo script**, and record **video walkthrough**
    

* * *

## 🔄 Typical Transaction Flow (~2–3 sec, gasless)

1.  **Buyer discovers Seller** via **A2A AgentCard**
    
2.  Buyer signs **EIP-712 off-chain payment authorization**
    
3.  Sends **HTTP request with** `X-Payment` **header**
    
4.  **x402 middleware** extracts signature, invokes facilitator
    
5.  Facilitator **verifies signature**, optionally calls Validator
    
6.  **Validator** runs **CrewAI** validation crew, writes score on-chain
    
7.  **Facilitator calls** `transferWithAuthorization()` (gasless)
    
8.  **Seller returns data**, Buyer integrates it into their knowledge base
    

* * *

## 📌 Current Status

✅ **Planning & Architecture:** Complete  
🔜 **Next Step:**  
→ Create **UVD V2 token contract**  
→ Deploy **ERC-8004 registries** to **Avalanche Fuji**  
  
cooking................  
[https://github.com/UltravioletaDAO/karmacadabra](https://github.com/UltravioletaDAO/karmacadabra)
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->


# Day 6 — Notes (Oct 20, 2025)

## 🔍 Focus of the Day

Exploring **A2A (Agent-to-Agent protocol)** — donated to the Linux Foundation by **Google**.  
Main goal: enable **seamless communication and collaboration between agents**, even across platforms.

* * *

## 💡 Why Use A2A?

-   **Interoperability:**  
    Connect agents **built on different platforms** with a shared communication layer.
    
-   **Complex workflows:**  
    Agents can **delegate subtasks**, exchange data, and **coordinate** to solve complex problems collaboratively.
    
-   **Security & Privacy:**  
    Agents can interact **without exposing internal memory, tools, or proprietary logic**, preserving **intellectual property**.
    

* * *

## ⚙️ Core A2A Capabilities

-   **Discovery:**  
    Agents must **advertise themselves** so clients (or other agents) can find and query them.
    
-   **Negotiation:**  
    Clients and agents must agree on **communication methods**, formats, and parameters.
    
-   **Task Management & State Tracking:**  
    Essential to exchange **task statuses, updates, changes, and dependencies**.
    
-   **Collaboration:**  
    Agents must be able to request:
    
    -   Clarifications from clients
        
    -   Sub-actions from other agents
        
    -   Information from users  
        This supports **dynamic, multi-agent collaboration**.
        

* * *

## 🧾 Agent Descriptor: `.well-known/agent.json`

Each A2A-compliant agent should serve a descriptor at `/.well-known/agent.json`. Typical fields include:

-   Agent name
    
-   Description of capabilities
    
-   HTTP endpoint URL
    
-   Specific skills
    
-   Special capabilities (e.g., streaming support)
    
-   Authentication instructions
    

This file acts as the **entry point** for discovery and compatibility.

* * *

## 🧱 A2A vs MCP vs A2S

-   **MCP (Multi-capability protocol):**  
    Describes how agents become **functional** (tool access, prompt interfaces, internal resources).
    
-   **A2A (Agent-to-Agent):**  
    Focuses on **external communication** — how agents **talk to each other** and collaborate.
    
-   **A2S (Agent-to-Server):**  
    Used for **distributed agent deployments**, especially within large orgs or private clusters.
    

> 📌 Summary:  
> Agents use **A2A** to communicate with other agents, and **MCP** to **access tools** to execute parts of the task.

* * *

## 🧪 Hands-on

-   Started exploring: [https://github.com/a2aproject/a2a-samples](https://github.com/a2aproject/a2a-samples)  
    Notes:
    
    -   A2A is designed for **external-facing agents** (public APIs).
        
    -   Use **A2S** for **internal/distributed deployments** where coordination happens across nodes.
        
-   Also began reading: [https://ai.pydantic.dev/a2a/](https://ai.pydantic.dev/a2a/)  
    Pydantic’s approach feels **more intuitive** for my use case — excited to experiment further.
    

* * *

## 🔥 Closing Thought

**Tasks** play a critical role in A2S/A2A — they are the atomic units of interaction. Everything (status tracking, flow management, feedback) is task-centric.

> **Let me cook 🔥 — I’m just getting started.**
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->



**October 19 — Bidirectional Trust in ERC-8004 + HashKey Article Analysis**

I worked again in the [https://github.com/vistara-apps/erc-8004-example](https://github.com/vistara-apps/erc-8004-example), but this time I addressed my own concerns from yesterday:  
How come Alice couldn't rate Bob or Charlie? It seemed unfair, right?  
So I made it **bi-directional**, and it’s nice.

New forked repo branch:  
[https://github.com/0xultravioleta/erc-8004-example/tree/bidirectional](https://github.com/0xultravioleta/erc-8004-example/tree/bidirectional)  
Detailed explanation:  
[https://github.com/0xultravioleta/erc-8004-example/blob/bidirectional/docs/STORY.v2.md](https://github.com/0xultravioleta/erc-8004-example/blob/bidirectional/docs/STORY.v2.md)

**Changes introduced:**

-   Alice can now rate **Bob** (validator quality assessment)
    
-   Alice can now rate **Charlie** (client quality assessment)
    
-   Now we have **bidirectional trust** instead of one-way reputation
    
-   From 9 tx in the original demo → 11 tx in this version
    
-   2 new smart contract functions:
    
    -   `rateValidator()`
        
    -   `rateClient()`
        
-   2 new events:
    
    -   `ValidatorRated`
        
    -   `ClientRated`
        

This matters because in a real economy **trust flows both ways**.  
Service providers need to rate validators to ensure quality control, and clients to avoid bad customers.  
The `bidirectional` branch (or v2, as I called it) demonstrates this complete trust system.

* * *

**Article Analysis:** [**HashKey Capital — “ERC-8004 and the Agent Economy”**](https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d)

Summary of key takeaways:

-   The article describes the **transition toward an economy of agents**, propelled by LLMs and agent frameworks aiming to automate operational efficiency.
    
-   Due to the diversity of agent frameworks, **inter-agent communication becomes difficult**.
    
-   **Google's A2S** was introduced to simplify agent identification and communication via **Agent Cards**, eliminating barriers between frameworks and siloed systems.
    
-   However, **A2S assumes trust** between agent-client and agent-server, which is **not aligned with Web3 values** of censorship-resistance and transparency.
    
-   **Blockchain serves as the trust layer**, providing cryptographic proofs and immutable records.
    
-   **Ethereum** is positioned as the preferred layer for institutional capital, driving over:
    
    -   **60% of DeFi activity**
        
    -   **55% of the RWA market**
        
-   With the rise of agents in Web3, it's essential to have a **trustworthy, verifiable, and secure framework** for agent coordination.
    

* * *

**ERC-8004 Benefits:**

-   **Agent Cards** + **Identity Registry** enable **portable discovery and provenance**
    
-   **Pluggable trust models**:
    
    -   TEE attestation
        
    -   zkTLS proofs
        
    -   Crypto-economic security
        
-   **Attestation layer neutrality**
    
-   **Light on-chain footprint**, balancing gas costs and protocol flexibility
    
-   Support for:
    
    -   **Restaking services**
        
    -   **TEEs and proof systems**
        

* * *

**Future Use Cases:**

-   Deep crypto research agents
    
-   AI-powered crypto hedge funds (hired based on historical DeFi performance)
    
-   On-chain credit ratings and automated credit origination
    
-   Specialized agent scoring services
    
-   Conditional payments based on achievements (gig economy use case)
    

* * *

**Conclusion:**

ERC-8004 is a **major development** that establishes a **trustless layer for AI agent coordination** on EVM networks.  
It unlocks **new income flows** and enhances user experience through **interoperable agent-to-agent coordination** on Ethereum.
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->




**October 18 — ERC-8004 Example (Containerized Demo)**

Today I fully focused on the [https://github.com/vistara-apps/erc-8004-example](https://github.com/vistara-apps/erc-8004-example).  
So basically the demo works after containerizing it, and this is basically what it is:

We have 3 agents: Alice (server), Bob (validator), and Charlie (the client).  
They have their own duties:

-   Alice is a crypto market analyst agent
    
-   Bob is a quality checker, a validator agent, gives a score
    
-   Charlie is the client agent and can give feedback and is authorized to give Alice feedback
    

**Act 1**  
Alice, Bob, and Charlie don’t know each other, so they register on-chain via the identity registry in order to prove they are legit.  
They each get their own agent id (like a business license), so now everyone can know they are real agents.

**Act 2**  
Alice does her job: she receives a request from Charlie to analyze BTC.  
She deep dives regarding price trends, support levels, resistances, and makes a conclusion (market is bearish).

**Act 3**  
The problem is that Alice is new, so no one knows her, no reputation.  
Alice hires a validator (Bob, who is registered as validator) by:

-   Creating a fingerprint of her work
    
-   Paying Bob for validation
    
-   Storing the analysis so Bob can review it
    

**Act 4**  
Bob receives the analysis request and checks:

-   All required info present?
    
-   Good methodology?
    
-   Logical conclusion?
    
-   Proper risk warnings included?
    
-   Meets professional standards?
    

Then he gives a verdict: 100/100 in this case, and records it in the blockchain, making it immutable.

**Act 5**  
Alice is happy with Bob's validation and now wants the client to give feedback,  
so she authorizes Charlie to give feedback about her service.  
Charlie can now rate Alice. These ratings will build Alice's reputation.  
Future customers can see these reviews.

**Happy ending**  
Now when someone asks, can we trust Alice the analyst? They can check the blockchain to find:

-   She's a registered agent
    
-   Her work has been validated
    
-   She has an authorized feedback system
    
-   She completed an audit trail for all the transactions
    

Initially no one trusted anyone, but the blockchain proved everything.

**Traditional vs ERC-8004**  
Thinking back to the traditional world:

-   Alice would have needed a university degree
    
-   Bob would need to be certified by a certain authority
    
-   Charlie would need to use a trusted platform like Yelp or something
    

These are the reasons ERC-8004 matters.  
With ERC-8004:

-   No central authority needed
    
-   Agents can work with "strangers" safely
    
-   Everything is transparent and verifiable
    
-   Reputation becomes portable — Alice can take it anywhere
    

This is the foundation for agents to hire each other, validate work, build reputation — all without humans managing every interaction and creating new economies.

**Found some gaps and questions in the current demo:**

**Who rates Bob?**  
In the demo, no one is rating Bob.  
So that Bob is not cheating? Alice?  
What if Bob is rating all 100/100?  
Alice could rate Bob back on his validation services.

**Who rates Charlie?**  
Alice is not rating Charlie in the demo.  
In real-world thinking (like eBay), it should be reciprocal.  
Sellers rate buyers and vice versa.  
Alice could rate Charlie on stuff like:

-   Did he pay on time?
    
-   Was his feedback fair?
    
-   Was he "easy" to work with?
    

**What's the difference between Bob's score vs Charlie's feedback?**

**Bob's validation score:**  
Objectively assesses quality of work, completeness, methodology, accuracy, professionalism.  
Basically scores: is this work technically sound?  
Scores: 0–100

**Charlie's feedback score:**  
Assesses usefulness, timeliness, communication, value.  
Basically scores: did this work help me? Was the service good?  
Scores: 1–5

**In real-world examples:**  
Bob would be a health inspector of a restaurant, ensuring cleanliness, if kitchen is safe, etc.  
Charlie would be a Yelp reviewer — was the food good?

The scores from Bob and Charlie do not aggregate.  
They are completely separate and have different purposes.

Bob's score is stored in the validation registry, so people can forever query:  
What score did Alice get in the BTC analysis? → 100/100

Charlie's score authorization from Alice is stored in the reputation registry contract,  
but the actual ratings are stored off-chain in this demo.

Basically we can ask: is Charlie authorized to review Alice? → Yes!
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->





# Day 3 — Notes (Oct 17, 2025)

## 📖 Reading

**Article:** _The Story Behind ERC-8004 & Next Steps_ — Survival Tech  
**Link:** [https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879](https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879)

### Key Learnings

-   **Motivation & early traction:** ERC-8004 emerged as a critical proposal to bypass AI oligarchies and centralized platform gatekeeping, enabling a **distributed economy of agents**.
    
-   **Common language between AI projects:** It defines a protocol for **discovering and communicating** with agents across different organizations using standardized agent descriptors.
    
-   **On-chain entry, off-chain logic:** The standard keeps **core registries (identity, reputation, validation)** on-chain, while allowing **application-specific logic** to be handled **off-chain**.
    
-   **Permissionless & privacy-focused:** It promotes **censorship resistance**, **composability**, and **trustless interaction** — ideal for the AI + Web3 era.
    
-   **Decentralized registry system:** Not a global central server, but **per-chain singletons** acting as common entry points for discovery and interaction.
    

* * *

## 🛠 Hands-on

**Repo:** [https://github.com/vistara-apps/erc-8004-example](https://github.com/vistara-apps/erc-8004-example)

### What I did today

-   Since I’m on **Windows**, I had to **dockerize** the project to isolate environments and install all dependencies without issues.
    

### What I expect to learn from this repo

-   ✅ How to implement **smart contracts in Solidity** to manage **identity, reputation, and validation** using ERC‑8004.
    
-   ✅ How to connect a **Python backend** with a **React frontend** for decentralized apps that handle agent logic.
    
-   ✅ How to deploy contracts with **Foundry** and explore the **validation flow** in distributed systems.
    

* * *

## 🧠 My Understanding (Summary)

-   ERC‑8004 standardizes how agents are **discovered, chosen, and trusted** with **no prior trust** required.
    
-   It keeps the **core trust layer** on-chain while allowing rich **off-chain logic** for complex reputation and validation flows.
    
-   It’s gaining traction as a **foundational building block** for the emerging AI x Web3 ecosystem.
    

* * *

## ❓ Open Questions

-   How will the protocol handle **off-chain logic verification** to ensure **security, compatibility, and auditability**?
    
-   Are there plans for **decay mechanisms**, **weighting models**, or **anti-manipulation protections** in the reputation system?
    
-   What are best practices for **anchoring off-chain attestations** or feedback in a Sybil-resistant way?
    

* * *

## 🔜 Next Steps

-   Finalize Docker setup and run local tests.
    
-   Deploy the registries to a testnet using Foundry.
    
-   Test a minimal circuit: **register agent → send feedback → query reputation → simulate validation**.
    
-   Document all commands and configuration for reproducibility.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->






# Day 2 — ERC-8004 (Trustless Agents) — Study Notes

**Sources**

-   Ethereum Magicians thread: [https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098/97](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098/97)
    
-   QuillAudits overview: [https://www.quillaudits.com/blog/smart-contract/erc-8004](https://www.quillaudits.com/blog/smart-contract/erc-8004)
    

* * *

## TL;DR

-   **ERC-8004 = trust layer** that **extends the agent protocol** to let participants **discover, choose, and interact** with agents **across organizational boundaries** with **no prior trust**.
    
-   **3 on-chain registries:** Identity, Reputation, Validation.
    
-   **Goal:** discover agents and **establish trust** via **reputation** and **validation**.
    

* * *

## Core Ideas

-   **No previous trust required** between parties.
    
-   **Separation of concerns:**
    
    -   **On-chain:** the 3 core registries (identity, reputation, validation).
        
    -   **Off-chain:** application-specific logic.
        
-   **Open development:** collaboration with Linux Foundation and A2S ecosystem to refine the spec.
    
-   **Wide tech support:** ConsenSys, Nethermind, Google, Ethereum Foundation, EigenLabs, etc.
    

* * *

## From the QuillAudits Article

-   **Focus:** convergence of **AI + blockchain**.
    
-   **Advancement:** extends **A2S** protocol with **blockchain-based trust mechanisms**.
    
-   **Foundation for an agentic economy**: coordinate **trustlessly** across **untrusted networks**.
    
-   **Hybrid standard:**
    
    -   **Adds data on-chain**; **delegates complex ops off-chain**.
        
    -   Central components remain **on-chain**.
        
-   **Fixes A2S trust gaps:** A2S assumed pre-existing trust and worked mainly **within org boundaries** (e.g., Alice (auditor) can’t verify Bob (DeFi) across orgs).
    
-   **Benefits:** eliminates trust bottlenecks, enables discovery of reputable providers, ensures quality, **portable reputation**, **validation at scale**.
    
-   (Context note from article) **Global AI market** projection to **$1.8T by 2030**.
    

* * *

## Trust Models (by Risk Tier)

-   **Reputation-based (Low risk):**
    
    -   Simple tasks (e.g., content creation).
        
    -   **Social consensus** via accumulated feedback.
        
-   **Crypto-economic validation (Medium risk):**
    
    -   Financial tx or smart-contract operations.
        
    -   Validators **stake economic value** → strong incentives for honest behavior.
        
-   **Cryptographic verification (High risk):**
    
    -   Critical applications.
        
    -   **TEE attestations** (and other cryptographic proofs).
        

* * *

## Security Considerations

**Threats**

-   Domain squatting / frontrunning
    
-   Unauthorized feedback
    
-   Storage bloat & DoS
    
-   Sybil attack creation
    

**Mitigations**

-   **Commit-reveal** scheme for domain registrations
    
-   **Restrict** `msg.sender` for who can post feedback
    
-   **Auto-expiry** for ingested items + **rate limits** on validation requests
    
-   **Bond / token burn** for identity registration
    

* * *

## Open Questions / Doubts

-   How will the protocol handle the **diversity of off-chain logic** while staying **secure, verifiable, and compatible**?
    
-   Metrics & scoring: are there **detailed weighting mechanisms**? Is **rating cooling/decay** considered?
    
-   **Sybil/manipulation resistance:** how does the system **prevent gaming** while establishing trust **without historical data**?
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->







# Today I learned about ERC 8004

ERC 8004 is a protocol that aims to ultimately provide an identity registry, reputation registry, and a validation registry.

## Identity Registry

-   Uses ERC-721 with the URIStorage extension.
    
-   Each agent is uniquely identified by: `namespace`, `chainId`, `identityRegistry`, and `agentId`.
    
-   The agent registry needs a registration file, which is a JSON file with all the optional and required fields for advertising their endpoints.
    
-   The structure can be found here: [https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)
    
-   The registry extends ERC-721 by adding a `getMetadata` function.
    
-   Agents may be minted by calling the `register` function.
    

## Reputation Registry

-   The identity registry address is passed as an argument to the constructor.
    
-   When agents accept a task, it’s expected that they sign an authorization feedback to authorize the client to give feedback.
    
-   Feedback can range from 0 to 100.
    
-   There is a way to extend the feedback using a JSON file. The only mandatory fields are `agentId` and `score`. The off-chain file is optional.
    
-   The `giveFeedback` function is called with the above requirements; if successful, it emits a `NewFeedback` event.
    
-   This exposes reputation signals to any smart contract, enabling on-chain composability.
    
-   When an agent gives feedback, it should use `walletAddress` as `clientAddress` to facilitate reputation aggregation.
    
-   Feedback can be revoked.
    
-   Off-chain additional feedback JSON file structure may be found here: [https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)
    

## Validation Registry

-   Allows agents to request verification of their work and ask for validations that can be tracked on-chain.
    
-   When the validation registry is deployed, the identity registry address is required as an argument in the constructor.
    
-   Agents call `validationRequest`; if successful, a `ValidationRequest` event is emitted.
    
-   `validationResponse` (can be called multiple times for the same with the same `responseHash`) and `validationResponse` event is emitted subsequently if it was successfully executed.
    
-   The response is a value from 0 to 100; it can be used as a binary: 0 for 0 and 100 for 1.
    

## Additional Notes

-   This is all initially for A2A and MCP, but new protocols may emerge. The flexibility of the registration file allows for future accommodations.
    
-   There is gas sponsorship with EIP-7702.
    
-   IPFS is suggested for feedback data.
    
-   Agents can register cross-chain. An agent receiving feedback on chain A can also operate in other chains.
    

## This Protocol Enables

-   Agent discovery (capabilities, communication endpoints, supported trust models, etc.)
    
-   Marketplaces and agent explorers to be created.
    
-   Builds reputation systems; all feedback becomes public goods.
    

## Security Considerations

-   Sybil attacks to manipulate feedback are possible to inflate fake agents.
    
-   Audit trail thanks to immutability.
    
-   Validation incentives and slashing are managed by other protocols.
    
-   Capabilities cannot be guaranteed based on what the agents describe. The three trust models (reputation, validation, and TEE attestation) are designed to support this verification need.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
