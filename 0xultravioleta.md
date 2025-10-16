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
