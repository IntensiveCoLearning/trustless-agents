---
timezone: UTC+8
---

# brreze

**GitHub ID:** weifengHuang

**Telegram:** @https://t.me/breeze_0071

## Self-introduction

I’m a software engineer with a strong interest in Web3, AI, and automation. I’ve previously participated in AI-agent development, but haven’t yet explored integrating AI with Web3. Through this program, I hope to gain hands-on experience and collaborate on practical projects that bridge these two fields.

## Notes
<!-- Content_START -->
# 2025-10-29
<!-- DAILY_CHECKIN_2025-10-29_START -->
Today was the **final day** of this phase. I went through the remaining materials on [**Trustless Agents**](https://intensivecolearn.ing/programs/trustless-agents) quite quickly. Most of the current progress still focuses on **theoretical understanding**, while the **coding implementation** is still ongoing. This feels like just the **beginning** — the real learning will come from **hands-on practice** and building through experience.
<!-- DAILY_CHECKIN_2025-10-29_END -->

# 2025-10-26
<!-- DAILY_CHECKIN_2025-10-26_START -->

Today, I initialized a project framework using **Coinbase’s AgentKit**. The main technical stack is based on **Vercel** for deployment, with **OpenRouter** providing the API layer. I integrated **Gemini** through a **BYOK (Bring Your Own Key)** setup. Additionally, I registered a **developer account and wallet** on **Coinbase Developer Platform**, and successfully tested the agent’s flow to **request and receive test tokens**.
<!-- DAILY_CHECKIN_2025-10-26_END -->

# 2025-10-25
<!-- DAILY_CHECKIN_2025-10-25_START -->


Today I studied the **Coinbase Developer documentation**, focusing on [https://docs.cdp.coinbase.com/x402/welcome](https://docs.cdp.coinbase.com/x402/welcome).

Key takeaways:

-   Explored the **AgentKit framework**, including integrations with **OpenAI**, **Vercel**, and **LangChain**.
    
-   Decided that future technical implementation will **prioritize Vercel AI** as the main platform.
    
-   Reviewed code examples for both **seller** and **buyer** flows, understanding how they are implemented on the **server** and **frontend** sides.
    
-   Next step: plan to **apply these fundamentals to build a practical on-chain Agent use case**, though the specific direction is still under consideration.
<!-- DAILY_CHECKIN_2025-10-25_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->



### **x402 Payment Protocol**

**1\. Difference from Traditional Coinbase Payment SDKs (e.g., Stripe-like Systems)**

Unlike earlier Coinbase USDC payment SDKs that focused on human-initiated web payments (checkout, subscriptions, invoices), **x402 is a protocol-level standard** designed for machine-native transactions.

It embeds payments directly into the HTTP layer via status code **402 (Payment Required)**, allowing **autonomous or pay-per-use** access without accounts, API keys, or manual billing.

In short, the old SDK was built **for humans**, while x402 is built **for agents and APIs**.

**2\. Agent Payment Authorization Models**

For AI agents, x402 enables either:

-   **Assisted Mode** — the human confirms each payment through a wallet UI (EIP-712 signing).
    
-   **Delegated Mode** — the agent is granted a **limited wallet or spending allowance**, allowing it to pay autonomously for small, predefined transactions.
    
    This ensures security while still enabling true **autonomous micro-payments** for API calls or data access.
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->




study ISEK ，[https://github.com/isekOS/ISEK](https://github.com/isekOS/ISEK)

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/weifengHuang/images/2025-10-23-1761233360744-image.png)
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->





I continued reading the A2A protocol and ran **a2a-samples-js**. I found an issue: the default model **gemini-2.5-pro-exp-03-25** is unavailable, so I switched it to **gemini-2.5-flash**.

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/weifengHuang/images/2025-10-21-1761059480750-image.png)![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/weifengHuang/images/2025-10-21-1761059411492-image.png)
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->






Today I continued studying the A2A protocol, focusing on **Agent Cards**, and examined two examples — one simple and one complex, real-world case.

```
{
  "protocolVersion": "0.3.0",
  "name": "Hello World Agent",
  "description": "Simple text skill",
  "url": "https://hello.example.com/a2a/v1",
  "preferredTransport": "JSONRPC",
  "version": "1.0.0",
  "capabilities": { "streaming": true },
  "defaultInputModes": ["text/plain"],
  "defaultOutputModes": ["text/plain"],
  "skills": [{ "id": "hello", "name": "Say Hello", "description": "Returns greeting" }]
}
```

```
{
  "protocolVersion": "0.3.0",
  "name": "ProcureGuard – Purchasing Risk Auditor",
  "description": "Performs risk checks on purchase orders/invoices, sanctions screening for suppliers, and orchestrates RPA actions (e.g., hold/freeze, evidence collection).",
  "url": "https://procureguard.example.com/a2a/v1",
  "preferredTransport": "JSONRPC",
  "additionalInterfaces": [
    { "url": "https://procureguard.example.com/a2a/v1",  "transport": "JSONRPC" },
    { "url": "https://procureguard.example.com/a2a/grpc", "transport": "GRPC"   },
    { "url": "https://procureguard.example.com/a2a/rest", "transport": "HTTP+JSON" }
  ],
  "provider": { "organization": "Example Fintech Ltd.", "url": "https://fintech.example.com" },
  "iconUrl": "https://procureguard.example.com/icon.png",
  "version": "1.2.3",
  "documentationUrl": "https://docs.fintech.example.com/procureguard",
  "capabilities": { "streaming": true, "pushNotifications": true, "stateTransitionHistory": true },
  "securitySchemes": {
    "oauth": {
      "type": "oauth2",
      "flows": {
        "clientCredentials": {
          "tokenUrl": "https://auth.example.com/oauth/token",
          "scopes": {
            "a2a.call": "Call A2A endpoints",
            "risk.read": "Read risk reports",
            "rpa.invoke": "Invoke RPA actions"
          }
        }
      }
    },
    "api-key": { "type": "apiKey", "in": "header", "name": "X-API-Key" },
    "mtls": { "type": "mutualTLS" }
  },
  "security": [
    { "oauth": ["a2a.call", "risk.read"] },
    { "api-key": [], "mtls": [] }
  ],
  "defaultInputModes":  ["application/json", "text/plain"],
  "defaultOutputModes": ["application/json", "application/pdf"],
  "skills": [
    {
      "id": "invoice-risk-check",
      "name": "Invoice & PO Risk Check",
      "description": "Validate invoice/PO consistency, anomaly scoring (amount splits, repeated vendors), contract linkage, VAT checks.",
      "tags": ["risk", "invoice", "po", "finance", "compliance"],
      "examples": [
        "Check risks for PO #A-2025-0912 and Invoice INV-88901.",
        "{\"poId\":\"A-2025-0912\",\"invoiceId\":\"INV-88901\",\"rules\":[\"split-detect\",\"vat-valid\"],\"attachments\":[\"a2a:file:po.pdf\",\"a2a:file:inv.pdf\"]}"
      ],
      "inputModes": ["application/json"],
      "outputModes": ["application/json", "application/pdf"]
    },
    {
      "id": "supplier-sanctions-screening",
      "name": "Supplier Sanctions & Watchlist Screening",
      "description": "Screen supplier against global sanctions (OFAC, EU), PEP lists, adverse media; return evidence bundle.",
      "tags": ["kyb", "sanctions", "compliance"],
      "examples": [
        "Screen supplier CN-8821 with legal name and registration number.",
        "{\"supplierId\":\"CN-8821\",\"legalName\":\"Hangzhou ABC Tech Co., Ltd.\",\"registrationNo\":\"91330100MA...\"}"
      ],
      "inputModes": ["application/json"],
      "outputModes": ["application/json"]
    },
    {
      "id": "rpa-bot-orchestration",
      "name": "RPA Bot Orchestration",
      "description": "Trigger RPA bots to freeze PO, request extra docs from requester, or escalate to compliance.",
      "tags": ["rpa", "workflow", "orchestration"],
      "examples": [
        "Freeze PO A-2025-0912 and notify requester for missing contract.",
        "{\"action\":\"freeze-po\",\"poId\":\"A-2025-0912\",\"reason\":\"missing-contract\"}"
      ],
      "inputModes": ["application/json"],
      "outputModes": ["application/json"]
    }
  ],
  "supportsAuthenticatedExtendedCard": true,
  "signatures": [
    {
      "protected": "eyJhbGciOiJFUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJrZXktMSJ9",
      "signature": "m2T6yPqP...k39Q",
      "header": { "kid": "key-1", "jku": "https://procureguard.example.com/jwks.json" }
    }
  ]
}
```
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->







Today, I continued reading the MCP-related protocols and examined their implementation in the official **Chrome DevTools MCP** repository.

In addition, I successfully ran the local environment for the repository [**vistara-apps/erc-8004-example**](https://github.com/vistara-apps/erc-8004-example), although the **agent** component still requires further review and understanding.
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->








Today I explored **Google’s A2A protocol** and compared it with **Model Context Protocol (MCP)**.

Although I’ve used several MCP-based tools before, I wasn’t very familiar with its underlying design, so I took a deeper look into the **architecture and transport layers** of MCP.

One key insight that differed from my previous understanding is that **MCP is not just a unified function-calling standard**.

It defines a complete protocol stack — including **transport mechanisms (stdio / streamable HTTP)** and **data formats (JSON-RPC 2.0)** — to standardize communication between models, clients, and tools.

More importantly, **MCP enables even models without native function-calling capability** to access and invoke tools.

This is achieved through the **client layer**, which interprets the model’s intent and executes tool calls using the **context and resources provided by MCP**, effectively extending tool-use capabilities beyond the model itself.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->









### [**1\. Discussion on Ethereum Magicians (ERC-8004 Thread)**](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098/9)

**Topic:** Community consensus and open questions from the ERC-8004 “Trustless Agents” discussion.

**Key takeaways:**

-   **Core boundary:** ERC-8004 focuses on _identity, reputation, and validation_ for on-chain agents — _payments are deliberately excluded_ from the standard.
    
-   **On-chain data:** Minimal “composable” data should be stored (identity + key metrics), while larger feedback or validation results remain off-chain.
    
-   **Cross-chain identity:** Future versions will support _CAIP-10 / DID-based identities_ for agent portability.
    

**Still debated:**

-   Whether to keep resolveByDomain (domain-unique) or move to URL/URI-based resolution.
    
-   How to support delegated writes / authorization for multi-sig or managed agents.
    
-   The right design of reputation models — single vs. multidimensional scoring.
    
-   Verification methods — TEE vs. zkML vs. sampling / re-execution.
    
-   Agent ID strategy — deterministic vs. flexible for key rotation.
    

### **2.** [**Insights from HashKey Capital Article —**](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098) 

### [**ERC-8004 and the Agent Economy**](https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098)

**Two key understandings:**

**(a) Types of Agents to Develop**

ERC-8004 defines **three roles**, not three mandatory components to build:

-   **Client:** requests tasks and gives feedback.
    
-   **Server:** executes tasks (the main role most developers will deploy).
    
-   **Validator:** verifies results.
    
    You can register **only your Server-type agent** to make it discoverable and hireable on-chain; validation and payment can rely on external registries or services.
    

**(b) Five Promising Use Cases**

1.  **Crypto Deep-Research Agents** – AI researchers producing sector analyses (e.g., DeFi yield reports) with verifiable data-hash commitments and reputation-based hiring.
    
2.  **AI-Driven Crypto Hedge Funds** – Automated strategy agents competing by track record; validators re-execute strategies to confirm performance before profit-sharing.
    
3.  **On-Chain Credit Ratings & Credit Origination** – Agents compute borrower credit scores; DeFi lenders use validated scores to set loan terms.
    
4.  **Agent Scoring & Audit Services** – Specialized validator-agents auditing other agents’ work, maintaining an open reputation layer.
    
5.  **Conditional Milestone Payouts for Gig Economy** – Task-based or freelance agents receive payments through escrow only after verified milestone completion.
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->










![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/weifengHuang/images/2025-10-15-1760541719099-image.png)

I studied [EIP-8004](https://eips.ethereum.org/EIPS/eip-8004).

EIP-8004 builds on **A2A** and extends it by introducing modules for **registration, verification, and reputation scoring**.

It does **not restrict how agents are developed** — instead, it provides a framework that enables agents to be **discovered on-chain**.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
