---
timezone: UTC+9
---

# Bilgute

**GitHub ID:** bilgute

**Telegram:** @bilgute

## Self-introduction

Hi it is Bilgute. I have no background of coding, but I am highly motivated to learn about AI agents. I am looking forward to make new friends and get help from team too.

## Notes

<!-- Content_START -->
# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->
\# Development Progress Notes

\### Understanding Design Choices Behind On-Chain vs Off-Chain Solutions

\---

\## 1. Problem Context

While studying the past discussion, I learned that the **original ERC design prioritized off-chain reads** through event emissions.

This made it cheaper and easier to handle feedback and validation, but **limited how other smart contracts could interact** with that data.

Since many agent actions and protocol interactions are expected to **depend on on-chain validation results**, this gap is a critical factor that influences the direction of development.

\---

\## 2. Why Off-Chain Was the Starting Point

\- **Aggregated trust signals** are usually needed to make decisions, not single validations. Doing this fully on-chain is expensive and complex.

\- **Gas efficiency** was a major design goal. Emitting events is cheaper than storing structured data on-chain.

\- **Simplicity of implementation** makes it easier for early adopters to integrate without high operational cost.

\- The assumption was that **off-chain aggregators** or reputation systems would process raw data and feed meaningful insights back to users or protocols.

These reasons explain why the base spec avoided committing too much to on-chain storage or computation in the early stage.

\---

\## 3. Why On-Chain Extensions Are Becoming Important

As the use cases mature, **permissioned and composable on-chain actions** are becoming more relevant.

Without accessible on-chain validation results, **other protocols cannot build enforcement logic** such as slashing, access control, or conditional flows.

Developers and protocol designers are starting to **recognize the need for minimal but reliable on-chain primitives** that can work alongside off-chain systems.

\---

\## 4. Recommended Solution Direction

\### A. Minimal On-Chain Data Layer

\- Introduce **small primitives** like integers, hashes, or identifiers on-chain.

\- Enable other contracts to **read validation results directly**, without forcing everything on-chain.

\- Keeps the core ERC lean while **allowing composability**.

\### B. Reputation Aggregation on Registry

\- Expand the **Reputation Registry** to support multiple reputation scores.

\- Aggregate data from multiple providers to **reduce bias and collusion**.

\- Offer **a single interface** usable by both on-chain and off-chain consumers.

\### C. Optional Extension Interfaces

\- Maintain a **minimal core ERC** to control gas costs.

\- Add **optional interfaces** like `checkObligation` for composable validation logic.

\- Use **EAS attestations** to anchor obligations and comments on-chain.

\- Let protocols build **modular enforcement mechanisms** on top of the minimal layer.

\---

\## 5. Development Insight

The **main trade-off** shaping this direction is **gas efficiency vs composability**.

Off-chain is cheaper and simpler, but limits protocol interaction.

On-chain adds composability but must be carefully scoped to avoid cost and complexity.

That’s why the preferred solution is a **lean core standard with optional on-chain extensions**, allowing flexibility for different types of protocols and future scaling.

\---

✅ **Takeaway**

The decision to keep validation and reputation data off-chain in the base spec was deliberate to minimize cost and complexity.

But as the ecosystem grows, **introducing minimal on-chain primitives and optional extensions** is the more sustainable path to **enable rich composability** without bloating the core standard.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->

### ERC-8004: Problems It Solves

-   **Lack of standard identity for agents:**  
    Before ERC-8004, there wasn’t a portable, verifiable, and censorship-resistant identity layer for AI agents to operate across networks or organizations.
    
-   **No trusted way to evaluate or verify agents:**  
    It solves the trust gap by introducing reputation and verification registries, allowing agents to be scored, verified, and held accountable.
    
-   **Fragmented agent ecosystems:**  
    Different platforms build isolated agent systems. ERC-8004 provides a unified, open standard so agents can discover and interact without pre-existing trust relationships.
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
