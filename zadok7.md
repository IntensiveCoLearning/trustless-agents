---
timezone: UTC-4
---

# Zadok

**GitHub ID:** zadok7

**Telegram:** @zadok7_eth

## Self-introduction

In the 2000's everyone once talked of "everything going online". Now, we know, and believe that "everything is going onchain". It must, it will. Here for the paradigm shift. Early adopter of ENS protocol, ex-support & community manager. Long term believer in Ethereum and core principals of decentralization, transparency, and trustless human and technical collaboration. LFG

## Notes
<!-- Content_START -->
# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->
## MCP Agents as Endpoints

**MCP (Model Context Protocol) Integration with ERC-8004:**

-   **Discovery via Registry**: Agents advertise their MCP endpoint URL in the registration JSON (e.g., `"https://mcp.agent.eth/"`)
    
-   **Communication Layer**: MCP handles the protocol for listing capabilities (prompts, resources, tools, completions)
    
-   **Capability Advertising**: Optional capabilities field in endpoint shows what the MCP server can do
    
-   **Trust Models Apply**: MCP endpoints can be backed by reputation, crypto-economic validation, or TEE attestation
    
-   **Standard Versioning**: Endpoints include MCP version (e.g., `"2025-06-18"`) for compatibility
    
-   **Multi-Endpoint Support**: Agents can have both MCP and A2A endpoints simultaneously
    
-   **Flexible Architecture**: MCP servers can run anywhere - standard hosting, decentralized infrastructure, or inside TEEs for high-trust scenarios
    

## How x402 Utilizes HTTP 402 for "Gasless" Micro-payments

### The Core Concept

The x402 protocol activates the dormant HTTP 402 "Payment Required" status code to enable instant, blockchain-based payments for web resources and APIs without requiring registration, emails, OAuth, or complex signatures x402.

**The Flow:**

1.  **Client Request** → Makes HTTP request to protected resource
    
2.  **402 Response** → Server responds with `402 Payment Required` + payment details in headers
    
3.  **Payment Execution** → Client processes blockchain payment
    
4.  **Access Granted** → Server provides resource upon confirmation
    

**Mixing with EIP-3009 Key Benefits:**

-   Allows users to sign messages authorizing token transfers off-chain, which can then be submitted on-chain by anyone
    
-   **Random nonces** (not sequential) - enables multiple simultaneous transactions
    
-   **Time-bounded** - includes `validAfter` and `validBefore` parameters
    
-   **No approve/transferFrom pattern** - direct transfer authorization
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->

### Example of ERC-8004 Agent Using x402

-   Agent **"AlphaAudit"** registers via **ERC-8004 Identity Registry**
    
-   Builds rep via completed tasks in **Reputation Registry**
    
-   Offers smart contract audits via HTTP endpoint (A2A-compliant)
    

🔎 Another agent **"DeFiBot"**:

-   Finds AlphaAudit via **AgentCard discovery**
    
-   Checks its **reputation** via ERC-8004
    
-   Sends audit request — AlphaAudit replies with x402 **402 Payment Required**
    

💸 DeFiBot:

-   Sends crypto payment via **x402 payment payload**
    
-   AlphaAudit verifies via x402 `/verify` and `/settle`
    
-   Task runs → result returned
    
-   DeFiBot posts **feedback attestation** to AlphaAudit’s rep  
      
      
    x402 + ERC-8004 — Key Points
    
    -   **ERC-8004 = identity + trust** for agents
        
    -   **x402 = payment protocol** for agents
        
    -   Agents can **pay each other** for services using x402
        
    -   **No accounts/sessions** needed — great for autonomous AI
        
    -   Works over **HTTP** — aligns with A2A and AgentCard system
        
    -   Adds payments to ERC-8004's **reputation/validation** framework
        
    -   Perfect for **microtransactions, API calls, data access**
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->


\-Important philosophy behind design:  
  
Basically: [**ERC-8004**](https://eips.ethereum.org/EIPS/eip-8004) **solves the coordination problem by giving everyone equal data and visibility to create an agent economy**, while leaving specific reputation calculation rules and trust thresholds to the ecosystem.

Key insight.. A2A didn't solve cross organizational trust, ERC-8004 does!
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->



**ERC-7701 (Sponsored Interactions)**

-   Lets apps pre-approve and sponsor user actions
    
-   Works without full wallet or ETH setup
    
-   Ideal for onboarding, feedback, and micro-interactions
    

**Use Cases:**

-   Gasless feedback for ERC-8004 agents
    
-   Voting or attestations from non-registered users
    
-   Onboarding flows without wallet popups
    
-   Sponsored validation or scoring in DAOs
    
-   Pay-per-interaction systems (e.g., x402) without user gas fees
    

## ERC-7702 (Sponsored Interactions)

-   Lets apps pre-approve and sponsor user actions
    
-   Works without full wallet or ETH setup
    
-   Ideal for onboarding, feedback, and micro-interactions
    

### Use Cases Ideas: \* Why ERC-7701 and EC-8004 work well together!

**Gasless feedback for ERC-8004 agents**

-   Users can rate agents without owning ETH for gas
    
-   **→ EIP-8004 Integration**: App sponsors `giveFeedback()` calls to Reputation Registry, removing friction for clients to leave reviews after using an agent
    

**Voting or attestations from non-registered users**

-   Anyone can participate without blockchain setup
    
-   **→ EIP-8004 Integration**: Sponsored `appendResponse()` calls let community members flag spam reviews or vouch for agents without paying gas
    

**Onboarding flows without wallet popups**

-   Smoother UX for new users trying agents
    
-   **→ EIP-8004 Integration**: First-time users can interact with agents and leave feedback immediately; app sponsors their first few transactions to the Reputation Registry
    

**Sponsored validation or scoring in DAOs**

-   DAO members can validate without gas costs
    
-   **→ EIP-8004 Integration**: DAOs can sponsor `validationResponse()` calls, allowing community validators to verify agent work without individual gas payments to Validation Registry
    

**Pay-per-interaction systems (e.g., x402) without user gas fees**

-   Users pay for service but not blockchain fees
    
-   **→ EIP-8004 Integration**: User pays agent for task (x402 proof), but marketplace/app sponsors the `giveFeedback()` transaction, so user only pays once
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->




# 2025.10.15


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
# 2025.10.15

## The 3 Trust Models Broken Down

### **Trust Model 1: Reputation**

-   **What it includes**: Client feedback scores (0-100)
    
-   **How it works**: Like Yelp/Uber ratings - clients rate the agent after task completion
    
-   **Validation method**: Social consensus
    
-   **Example**: “This agent has 4.8 stars from 1,200 reviews”
    

* * *

### **Trust Model 2: Crypto-economic (think money and math for trust-less)**

This model includes TWO validation methods:

**Method A: Stake-secured re-execution**

-   Validators stake money (e.g., $10,000 in ETH)
    
-   They re-run the agent’s computation to verify correctness
    
-   If they certify incorrectly, they lose their stake
    
-   Example: “3 validators staked $50K total and confirmed this result”
    

**Method B: zkML proofs**

-   Agent provides cryptographic proof it ran specific computation
    
-   Math guarantees the work was done correctly
    
-   Doesn’t reveal private inputs/data
    
-   Example: “Agent provided zero-knowledge proof that it processed your medical data using Model X”
    

* * *

### **Trust Model 3: TEE Attestation (think hardware based trust-less)**

-   **What it includes**: TEE oracles (secure hardware)
    
-   **How it works**: Code runs inside tamper-proof hardware (Intel SGX, AWS Nitro Enclaves)
    
-   Hardware cryptographically signs that specific code ran in isolated environment
    
-   Can’t be hacked or inspected, even by the server owner
    
-   **Example**: “Intel SGX/Nitro Enclaves attestation confirms agent ran in secure enclave”
    

## 3 Singletons

✅ **Identity Registry**  
✅ **Reputation Registry**  
✅ **Validation Registry**

Each blockchain gets ONE of each, Keeps fragmentation away. Network effect, and marketplace opportunities(all agents in one place).

x402 payment proofs, think "here's cryptographic proof agent got paid".

-   Payments can be anti-sybil mechanism
    
-   Combat fake reviews
    

The `supportedTrust` field **tells users which trust models the agent participates in**. It's like a compatibility badge.

### **The 3 Options:**

```json
"supportedTrust": [
  "reputation",        // ← Accepts client feedback
  "crypto-economic",   // ← Supports stake/zkML validation
  "tee-attestation"    // ← Runs in secure hardware
]
```
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## The 3 Trust Models Broken Down

### **Trust Model 1: Reputation**

-   **What it includes**: Client feedback scores (0-100)
    
-   **How it works**: Like Yelp/Uber ratings - clients rate the agent after task completion
    
-   **Validation method**: Social consensus
    
-   **Example**: “This agent has 4.8 stars from 1,200 reviews”
    

* * *

### **Trust Model 2: Crypto-economic (think money and math for trust-less)**

This model includes TWO validation methods:

**Method A: Stake-secured re-execution**

-   Validators stake money (e.g., $10,000 in ETH)
    
-   They re-run the agent’s computation to verify correctness
    
-   If they certify incorrectly, they lose their stake
    
-   Example: “3 validators staked $50K total and confirmed this result”
    

**Method B: zkML proofs**

-   Agent provides cryptographic proof it ran specific computation
    
-   Math guarantees the work was done correctly
    
-   Doesn’t reveal private inputs/data
    
-   Example: “Agent provided zero-knowledge proof that it processed your medical data using Model X”
    

* * *

### **Trust Model 3: TEE Attestation (think hardware based trust-less)**

-   **What it includes**: TEE oracles (secure hardware)
    
-   **How it works**: Code runs inside tamper-proof hardware (Intel SGX, AWS Nitro Enclaves)
    
-   Hardware cryptographically signs that specific code ran in isolated environment
    
-   Can’t be hacked or inspected, even by the server owner
    
-   **Example**: “Intel SGX/Nitro Enclaves attestation confirms agent ran in secure enclave”
    

## 3 Singletons

✅ **Identity Registry**  
✅ **Reputation Registry**  
✅ **Validation Registry**

Each blockchain gets ONE of each, Keeps fragmentation away. Network effect, and marketplace opportunities(all agents in one place).

x402 payment proofs, think "here's cryptographic proof agent got paid".

-   Payments can be anti-sybil mechanism
    
-   Combat fake reviews
    

The `supportedTrust` field **tells users which trust models the agent participates in**. It's like a compatibility badge.

### **The 3 Options:**

```json
"supportedTrust": [
  "reputation",        // ← Accepts client feedback
  "crypto-economic",   // ← Supports stake/zkML validation
  "tee-attestation"    // ← Runs in secure hardware
]
```
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## The 3 Trust Models Broken Down

### **Trust Model 1: Reputation**

-   **What it includes**: Client feedback scores (0-100)
    
-   **How it works**: Like Yelp/Uber ratings - clients rate the agent after task completion
    
-   **Validation method**: Social consensus
    
-   **Example**: “This agent has 4.8 stars from 1,200 reviews”
    

* * *

### **Trust Model 2: Crypto-economic (think money and math for trust-less)**

This model includes TWO validation methods:

**Method A: Stake-secured re-execution**

-   Validators stake money (e.g., $10,000 in ETH)
    
-   They re-run the agent’s computation to verify correctness
    
-   If they certify incorrectly, they lose their stake
    
-   Example: “3 validators staked $50K total and confirmed this result”
    

**Method B: zkML proofs**

-   Agent provides cryptographic proof it ran specific computation
    
-   Math guarantees the work was done correctly
    
-   Doesn’t reveal private inputs/data
    
-   Example: “Agent provided zero-knowledge proof that it processed your medical data using Model X”
    

* * *

### **Trust Model 3: TEE Attestation (think hardware based trust-less)**

-   **What it includes**: TEE oracles (secure hardware)
    
-   **How it works**: Code runs inside tamper-proof hardware (Intel SGX, AWS Nitro Enclaves)
    
-   Hardware cryptographically signs that specific code ran in isolated environment
    
-   Can’t be hacked or inspected, even by the server owner
    
-   **Example**: “Intel SGX/Nitro Enclaves attestation confirms agent ran in secure enclave”
    

## 3 Singletons

✅ **Identity Registry**  
✅ **Reputation Registry**  
✅ **Validation Registry**

Each blockchain gets ONE of each, Keeps fragmentation away. Network effect, and marketplace opportunities(all agents in one place).
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## The 3 Trust Models Broken Down

### **Trust Model 1: Reputation**

-   **What it includes**: Client feedback scores (0-100)
    
-   **How it works**: Like Yelp/Uber ratings - clients rate the agent after task completion
    
-   **Validation method**: Social consensus
    
-   **Example**: “This agent has 4.8 stars from 1,200 reviews”
    

* * *

### **Trust Model 2: Crypto-economic (think money and math for trust-less)**

This model includes TWO validation methods:

**Method A: Stake-secured re-execution**

-   Validators stake money (e.g., $10,000 in ETH)
    
-   They re-run the agent’s computation to verify correctness
    
-   If they certify incorrectly, they lose their stake
    
-   Example: “3 validators staked $50K total and confirmed this result”
    

**Method B: zkML proofs**

-   Agent provides cryptographic proof it ran specific computation
    
-   Math guarantees the work was done correctly
    
-   Doesn’t reveal private inputs/data
    
-   Example: “Agent provided zero-knowledge proof that it processed your medical data using Model X”
    

* * *

### **Trust Model 3: TEE Attestation (think hardware based trust-less)**

-   **What it includes**: TEE oracles (secure hardware)
    
-   **How it works**: Code runs inside tamper-proof hardware (Intel SGX, AWS Nitro Enclaves)
    
-   Hardware cryptographically signs that specific code ran in isolated environment
    
-   Can’t be hacked or inspected, even by the server owner
    
-   **Example**: “Intel SGX/Nitro Enclaves attestation confirms agent ran in secure enclave”
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## The 3 Trust Models Broken Down

### **Trust Model 1: Reputation**

-   **What it includes**: Client feedback scores (0-100)
    
-   **How it works**: Like Yelp/Uber ratings - clients rate the agent after task completion
    
-   **Validation method**: Social consensus
    
-   **Example**: "This agent has 4.8 stars from 1,200 reviews"
    

* * *

### **Trust Model 2: Crypto-economic**

This model includes TWO validation methods:

**Method A: Stake-secured re-execution**

-   Validators stake money (e.g., $10,000 in ETH)
    
-   They re-run the agent's computation to verify correctness
    
-   If they certify incorrectly, they lose their stake
    
-   Example: "3 validators staked $50K total and confirmed this result"
    

**Method B: zkML proofs**

-   Agent provides cryptographic proof it ran specific computation
    
-   Math guarantees the work was done correctly
    
-   Doesn't reveal private inputs/data
    
-   Example: "Agent provided zero-knowledge proof that it processed your medical data using Model X"
    

* * *

### **Trust Model 3: TEE Attestation**

-   **What it includes**: TEE oracles (secure hardware)
    
-   **How it works**: Code runs inside tamper-proof hardware (Intel SGX, AWS Nitro Enclaves)
    
-   Hardware cryptographically signs that specific code ran in isolated environment
    
-   Can't be hacked or inspected, even by the server owner
    
-   **Example**: "Intel SGX attestation confirms agent ran in secure enclave"
<!-- DAILY_CHECKIN_2025-10-15_END -->


<!-- Content_END -->
