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
