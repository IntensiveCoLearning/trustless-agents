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
# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->
**Day 5 A2A handshake & AP2 overview**

**x402協議：**

原本是一個HTTP設計時留下的一個狀態碼，為了給網路世界需要支付時使用。但礙於當時並沒有適當的網路支付設計和基礎設施，而一直都是個未使用過的狀態碼。

然而許多現行的支付方式都是為了人類設計，像是實體刷卡，授權，付費，沒有為了AI而設計的支付方式。

但區塊鏈穩定幣這種數位貨幣就變得非常適合這樣的使用場景，也因此催生出x402這樣的協議。不需要再額外去設計，利用現有的網路協議，只要收到狀態碼402回 應，就去解析付款需求，並利用錢包進行付款。

服務坊也可以非常簡單的建立付款回應

**AP2 & x402的關係：**

看完x402協議後我就有點困惑，那google為什麼還需要去設計一個AP2協議，既然都已經有這個現成的狀態碼了，且也正在發展。因此做了一些研究。

| 協議 | 關注範圍／目標 | 核心功能／特色 | 適用場景 | 與對方的關係 |
| AP2 | 為 AI 代理（以及相關機構、商家、支付方）建構一個可信、可互操作的支付協議框架。 (fintechwrapup.com) | – 授權機制（如「意圖授權 Intent Mandate」） (Cnblogs) – 購物車授權（Cart Mandate） (Cnblogs) – 支付授權／結算證明（Payment Mandate） (ap2lab.com) – 支持多種支付方式（卡片、銀行轉帳、數位資產／穩定幣） (Google Cloud) – 強調可追蹤、審計、信任、代理行為透明性。 | AI代理替使用者或系統執行購買、委託交易、自動化流程中涉及支付的場景（例如代理選貨、代理購買、代理代付） (tairoa.org.tw) | x402 是其中一種「可插入／可使用的支付鐵軌」之一。AP2 定義流程與框架，x402 提供特定實現（尤其是穩定幣＋鏈上微支付） |
| x402 | 作為一條“agent-to-agent”或“agent 支付服務”用的支付鐵軌／協議擴展，特別針對穩定幣／微支付／鏈上結算場景。 (Binance) | – 支援穩定幣（例如 USDC）結算，跨境、低手續費、即時。 (Coinbase) – 支援 agent 自行付款給其他 agent、或者 agent 代表使用者付款。 (Coinbase) – 結合鏈上技術與 HTTP/API 模式（如「基於 HTTP 402 狀態碼」的微支付概念） (arXiv) | Agent 生態中，尤其是 agent-to-agent 的微服務市場、微任務、市場平台、或者當代理需要向其他代理或服務支付的場景。 | 可被 AP2 採用作為其結算選項之一。在 AP2 架構中，若選用穩定幣或鏈上結算的路徑，x402 就是該路徑的技術支撐。 (ap2lab.com) |

AP2定義了Agent而設計的網路支付方式 / 協議。比如說代理者要代替人類在網路上購物 刷卡 賣賣，那AP2會是適用的協議。而如果場景縮小到瞄準是Agent to Agent的，Agent使用微服務的支付場景，並且使用穩定幣去做結算結帳，使用x402會是更適用的協議。

簡單說，AP2是一個大框架，定義了基礎的驗證授權細節，以及整體規則，x402是在這個框架下，縮小到特定場景下的一種使用穩定幣支付結算的支付方式，適用Agent to Agent / Agen to micor-service的使用場景。
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->

今日對A2A進行更深入的探討和研究
<!-- DAILY_CHECKIN_2025-10-19_END -->

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
