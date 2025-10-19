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
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
## A2A

### Definition & Purpose:

-   A2A is an open standard protocol designed to enable **seamless communication and collaboration among AI agents** — we’re talking about autonomous agents built by different vendors, on different frameworks, in different organisations.
    
-   The goal is to allow those agents to interoperate (so they can talk to each other, delegate work, combine efforts) rather than being isolated silos.
    

**Problems A2A Addresses**

-   In complex tasks (e.g., “plan an international trip”), you might need many specialist agents (flight-booking agent, hotel-reservation agent, currency conversion agent, local tours agent). Without a standard, you have:
    
    -   Each agent built as a tool requiring custom integration (high engineering overhead)
        
    -   Limited interoperability, making scaling difficult
        
    -   Security / maintenance issues due to ad-hoc integration
        
-   A2A aims to solve these by offering a standardised protocol for agent-to-agent communication.
    

**Example Scenario**

-   A user gives a complex prompt (“Plan an international trip”).
    
-   The assistant recognises that specialised agents are needed (flight booking, hotel, currency, tours).
    
-   With A2A: These agents can communicate via standardised interfaces, the orchestrating assistant collects and integrates results, and the user sees a seamless, unified answer.
    

**Core Benefits**

-   **Secure collaboration**: Uses established web-protocols (HTTPS) and ensures agents operate as black boxes (i.e., don’t expose inner logic) so others can use them without internal access.
    
-   **Interoperability**: Break down silos between agents from different vendors or frameworks.
    
-   **Agent autonomy**: Agents remain independent, with their own capabilities, yet able to collaborate.
    
-   **Reduced integration complexity**: Because the protocol is standardised, developers can focus on agent logic rather than custom communication plumbing.
    
-   **Support for long-running operations (LROs)**: The protocol supports asynchronous/streaming operations (so agents can handle tasks that take time).
    

**Key Design Principles**

-   **Simplicity**: Leverages existing standards (HTTP, JSON-RPC, Server-Sent Events (SSE)) to make adoption easier.
    
-   **Enterprise Readiness**: Security, authorization, privacy, traceability are built-in.
    
-   **Asynchronous**: Native support for long-running, disconnected, streaming tasks.
    
-   **Modality Independence**: Agents can communicate in different media/content types — not limited to text.
    
-   **Opaque Execution**: Agents don’t have to expose internal logic, memory, or tools — they operate as autonomous black boxes, which supports IP protection and security.
    

**Positioning in the Agent Stack**

-   A2A deals with inter-agent communication.
    
-   In comparison:
    
    -   The Model Context Protocol (MCP) focuses on linking models to data/tools.
        
    -   Agent development frameworks (e.g., ADK) provide toolkits for building agents.
        
-   So, A2A sits at the communication/collaboration layer among agents across organisations/frameworks.
    

**A2A Request Lifecycle**

1.  **Agent Discovery**: A client queries the server’s “/.well-known/agent-card” endpoint to obtain the agent’s metadata (Agent Card).
    
2.  **Authentication**: The client parses the Agent Card’s securitySchemes. If e.g., openIdConnect, the client obtains a JWT via the auth server.
    
3.  **sendMessage API**: Client posts to `/sendMessage` (with JWT). Server processes the message, creates a task, returns a response.
    
4.  **sendMessageStream API**: Client posts to `/sendMessageStream` (with JWT). Server streams status updates, artifacts (via SSE), until task complete.
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->

![image](https://github.com/user-attachments/assets/25f30523-2dc5-4721-bce8-80d4ea9c36c7)
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
