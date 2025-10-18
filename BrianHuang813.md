---
timezone: UTC+8
---

# 黃楷修

**GitHub ID:** BrianHuang813

**Telegram:** @BrianHuangk

## Self-introduction

目前在 Web2 工作
努力學習 AI blockchain，期待有天能在這個領域發光發熱

## Notes

<!-- Content_START -->
# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->
**Day 4 A2A Fundamental**

**什麼是A2A Agent to Agent：**

簡單說，A2A就是一個可以讓未來世界的AI Agent互相溝通合作的開放標準。讓所有來自不同框架，不同標準，不同環境設計出來的Agent可以透過這個標準互相溝 通，如此可以大大提升Agent的能力和可能性，以及使用場景。

**為什麼要使用A2A協議？**

如果我們期待未來的世界裡，只需要下提示詞，就可以請Agent代理我們去處理我們要求的任務，就需要賦予他們足夠的權限和能力。但如果需要為每個工具都去設計 使用協議，整體會變得非嘗複雜和難以擴展。但若能讓Agent各司其職而互相溝通合作，則能大大擴展其能力和效率。

**如何實作？**

標準定義了以下幾個關鍵要素：

1.  Agent Client：對A2A Server提出請求的Agent 或 App
    
2.  Agent Server：A2A網路節點，一個可以被呼叫溝通的Agent
    
3.  Agent Card：對Agent身份的詳細敘述，包括ID 能力 驗證方式 節點 溝通協議
    
4.  Message & Task：請求訊息及任務等敘述
    
5.  Transport Protocol：Agent間可以使用的溝通協議
    
6.  Streaming Transport：Agent間可以連線溝通的溝通協議
    

**與MCP的差異：**

兩者是相輔相成的存在。MCP定義了Agent如何去使用種種的工具和服務。A2A則定義了擁有使用這些工具技能的Agent如何互相溝通。我們都知道，一個萬能的系 統一定不會有最好的效率，分工合作才能帶來最大的成效。

透過MCP去使用工具，透過A2A去與擁有不同MCP的Agent合作。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->

The Overview of ERC-8004

**EIP-8004（Trustless Agents）** 是一個讓「AI Agents」或「自動化代理」能在鏈上**被註冊、發現、評價與驗證**的標準。

EIP-8004 = ERC-721 (身份) + 鏈上聲譽系統 + 鏈上驗證框架。

它的目標是讓不同開發者建立的代理能夠在**去中心化環境下互相信任與協作**，不需要中心伺服器或預先信任關係。

簡單來說，這個協議可以讓Agent在鏈上有身份，聲譽，且可驗證，並且會留有記錄。

**如何實作**

主要設計了三種合約：

1.  Identity Registry （身份註冊）：使用 ERC-721 和 URIStorage 擴展進行代理註冊，使**所有代理都可以立即瀏覽和轉移與 NFT 兼容的應用程序。metadata裡面會包含關於agent以下的資料：**
    
    -   名稱、描述、圖像
        
    -   通訊方式（如 A2A、MCP、ENS、DID）
        
    -   支援的信任機制（Reputation、TEE、加密質押等
        

呼叫register()創建一個NFT並上傳JSON metadata。而ERC-721 中的 tokenId 稱為 agentId。ERC-721 代幣的所有者是代理的所有者

目的：讓agent擁有鏈上身份

2.  Reputation Registry（聲譽註冊）：Client Address可以對agent提供回饋分數（1 - 100），由agent先簽署feedbackAuth授權，避免隨意刷評價
    

呼叫 getIdentityRegistry( ) 獲得，_identityRegistry_ 位址會傳遞至建構函式

呼叫 giveFeedBack( ) 來進行回饋，帶入有效註冊的agentID

呼叫 revokeFeedback( ) 來撤銷回饋

目的：讓agent擁有鏈上聲譽，供他人選擇

3.  Validation Registry（驗證註冊）：Agent 可以要求第三方驗證者（validator）審查自己的工作結果。驗證者回覆分數（0–100）或「通過／不通過」，可附 URI 指向報告。
    

agent呼叫validationRequest( )來請求驗證，且必須由擁有者來呼叫。rrequestUrl指向鏈下數據，包含所有驗證者所需要的驗證資料。

驗證者呼叫 validationResponse( ) 來回應驗證

目的：建立可被驗證的驗證層

| 功能 | 合約型別 | 實作基礎 | | 身份註冊 | ERC-721 | register() → 建立 Agent NFT | | 聲譽註冊 | Custom Contract | submitFeedback() + getSummary() | | 驗證註冊 | Custom Contract | validationRequest() + validationResponse() |

外部資料（例如回饋文件、驗證報告）通常放在 **IPFS / Arweave**，鏈上只儲存 URI + Hash。

問題：

有沒有可能讓鏈上存有更多數據，畢竟既然這些數據是經過驗證可信任的，如果這些數據可以供其他合約使用的話會不會可以擴展更多可能性？
<!-- DAILY_CHECKIN_2025-10-17_END -->
<!-- Content_END -->
