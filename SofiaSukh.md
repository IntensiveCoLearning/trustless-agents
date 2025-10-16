---
timezone: UTC+1
---

# Sofia

**GitHub ID:** SofiaSukh

**Telegram:** @sonkiski

## Self-introduction

I am a business development manager who is currently learning to code. I am very much interested in what is happening within the Ethereum x AI space, and I would appreciate learning more and going on a deep dive with the topic. I have some basic Python skills (had to learn for developing my scraping tools for work), and I am currently learning Solidity.

## Notes

<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
Today, I read through the ERC-8004 standard and the related articles to it, basically, everything that is in Module 1.

ERC-8004 is the **“trust foundation”** (or trustless coordination layer) of decentralised AI agents. It is not a new chain or token; it’s about giving agents a **shared language of identity and verification.** It's an extension of Google’s A2A (Agent-to-Agent) protocol, but for Ethereum-grade verification. BUT! Google’s A2A assumes internal trust, while ERC-8004 makes open-network collaboration possible.

**Three registries**: identity (_“who are you?”,_ a censorship-resistant, portable ID (EVM address + domain + token URI, storage: off-chain agent-card.json), reputation (_“how have you behaved?”,_ records feedback events between agents; real data lives off-chain (IPFS, HTTP), feedback hashers + auth events), and validation (_“did you actually do what you said?”,_ requests/responses from independent validators (stakers, zk verifiers, TEE oracles), validation metadata + events). Autonomous agents can **discover, collaborate, and verify each other** without prior trust.

Lean on-chain but powerful off-chain! (or light-on-chain / rich off-chain), minimal by design, where only proofs and references go on-chain -> lower gas, higher flexibility

Identities and attestations become portable across chains via **CAIP-10.**

**From QuillAudits analysis** of the ERC-8004 standard:

-   Domain Squatting via Front-Running (to prevent front-running)
    
-   Unauthorized Feedback Authorization (avoid spam)
    
-   Storage Bloat and DoS (prevent DoS)
    
-   Sybil Identity Creation (bond and burn per agent)
    

\------

_Vistara example - I need to dig deeper into that, but for now, what I could understand is that there are three register agents (Server, Validator, Client) working together without pre-existing trust through the execute - validate - feedback cycle that is recorded on-chain._

**trustless doesn’t mean trust-free**

**it means verifiable**

TO-DO: go line through line @ Vistara, so that I can do my hands-on task later on
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
