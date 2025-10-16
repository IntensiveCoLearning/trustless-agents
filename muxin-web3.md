---
timezone: UTC+8
---

# Muxin

**GitHub ID:** muxin-web3

**Telegram:** @muxin_eth

## Self-introduction

test

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
I’m testing something for updating the study notes. 111111

-   test
    
-   test
    
-   test
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


Today I learned the ERC-8004 protocol: [https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)  
  
ERC-8004 defines a standard for creating, discovering, and trusting autonomous agents without centralized control. It introduces three on-chain registries to manage agents’ identity, reputation, and validation.

-   **Identity Registry**: An ERC-721 token contract for agent registration. Each agent is assigned a unique tokenId (`agentId`). The token URI resolves to a registration file (for example via IPFS or HTTPS) containing metadata like name, description, image, endpoints, supported trust models.
    
    -   Agents’ endpoints may include references to A2A, MCP, ENS names, DIDs, or wallet addresses.
        
    -   Agents SHOULD have at least one registration (multiple are possible), and all fields in the registration are mandatory.  
        The `supportedTrust` field is OPTIONAL. If absent or empty, this ERC is used only for discovery, not for trust.
        
    -   On-chain metadata support: the registry implements `getMetadata()` / `setMetadata()` functions for additional attributes.
        
    -   Registration functions (`register()`, etc) emit standard and custom events.
        
-   **Reputation Registry**: Allows clients (humans or agents) to submit feedback for an agent. Feedback includes a score (0-100), optional tags, an optional URI to more detail (e.g., IPFS JSON), and optional hash for integrity.
    
    -   Clients must be authorized by the agent (via a signed `feedbackAuth`).
        
    -   Supports revoking feedback and appending responses (e.g., agent or client can respond).
        
    -   Reading functions expose summary statistics (e.g., average score, count) and raw feedback, enabling on-chain composability or off-chain richer analysis.
        
-   **Validation Registry:** Allows an agent to request independent validators to audit or verify the agent’s work, and stores the result on-chain. For example validators might re-run a job and stake tokens, or use zkML verification, TEEs, etc.
    
    -   `validationRequest()` function to issue a request with URI + hash.
        
    -   `validationResponse()` function by the validator returns response code 0-100, optional response URI/hash, tag.
        
    -   Read functions provide status and summary (counts, averages) for an agent.
        
    -   Note: Incentives/slashing for validators are _outside_ the standard.
<!-- DAILY_CHECKIN_2025-10-15_END -->

<!-- Content_END -->
