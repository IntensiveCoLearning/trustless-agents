---
timezone: UTC+8
---

# k66

**GitHub ID:** k66inthesky

**Telegram:** @thekidk66

## Self-introduction

感謝Bruce, ETHPanda, LXDAO舉辦這活動! 之前參加過ETHPanda x LXDAO約三次殘酷共學，這次想再參加與大家一同學習進步!

我預計的學習方式：根據[readme](https://github.com/IntensiveCoLearning/trustless-agents)順序學習，有不懂的再延伸查詢並將筆記紀錄於此。
期待自己能完成coding challenge。

## Notes
<!-- Content_START -->
# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->
> 閱讀 [https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)  
> **目標**：讓 AI 代理能在不同組織之間安全協作，不需要事先信任任何對方，支持自動發現、選擇與互動，推進去中心化的 agent 經濟。

## **三大核心鏈上註冊表**

> `Identity` 、`Reputation` 、`Validation`

## **信任模型**

> 多種模式如: 聲譽驅動、經濟質押、密碼學驗證（零知識、TEE），根據需求選擇。

## SDK

> \[erc-8004-contracts\]([https://github.com/erc-8004/erc-8004-contracts](https://github.com/erc-8004/erc-8004-contracts))  
> \[ChaosChain\]([https://github.com/ChaosChain/chaoschain-genesis-studio](https://github.com/ChaosChain/chaoschain-genesis-studio))

### 參與ERC-8004會議心得  

### 實作介紹

-   上述兩SDK
    
    -   執行前: 有npm, hardhad即可。
        
    -   執行時: 使用就npm run deploy 或 npm run test 某隻ts即可。
        
-   已佈署在sepolia測試網上。
    
-   使用提供的SDK與身分註冊表、反饋註冊表和驗證註冊表進行交互。
    

###   
Q&A

-   驗證機制不指定具體實現方式，而是提供標準化接口。
    
-   數據隱私保護取決於所驗證方法:
    
    -   使用ZKML時可以保護隱私，因為只有ZKP的公共輸入是公開的。
        
    -   使用stake-secure interface時輸入和計算是可以公開的。
        
    -   使用TEE時可以有不同的實現方式，既可以公開也可以私有。
        
-   關於驗證請求URL架構
    
    -   目前支持IPFS和HTTP URL，但可以添加其他架構。這是一個string，只要有標準化方式解析它即可。未來計畫支持更多內容可尋址的方式如ARE(?)。
        
-   關於多管理員支持
    
    -   NFT所有者可以使用 `operators` 來添加操作者。操作者可執行所有者能做的所有操作，這解決多人管理單個代理的問題。
        
-   關於註冊問題
    
    -   ERC-8004的目標是每條鏈上都有一個單例(singleton)註冊表，但技術上無法阻止有人佈署自己的註冊表。
        
    -   Leonard他們希望每條鏈都會指向一個規範的、眾所周知的單例註冊表。  
        \> 隨著時間推移，聚合器可能優先考慮最知名、最廣泛使用的註冊表。
        
    -   Macro提到IFPS創建者Protocol Labs正為ERC-8004社區提供免費的IFPS託管服務。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
## 名詞摘要(ERC-8004, AP2, A2A, x402, DecentralizedAI, AgentEconomy, Trustless Agents, AI Agents):
```
  + ERC-8004: EIP-8004旨在AI agents間的通訊協議。
  + AP2: Agent Protocol 2
  + A2A: Agent-to-Agent
  + x402: Web3和AI的通訊協議，強調隱私保障與分布式身份驗證。
  + DecentralizedAI: 去中心化人工智慧，表示AI模型、訓練、運算和決策分散在多個節點或平台上，不依賴單一集中式伺服器。
  + AgentEconomy: 代理經濟，指的是由大量AI代理參與的經濟生態，這些代理可自主執行任務、達成交易並創造價值。
  + Trustless Agents:無需信任的代理，是指在設計安全協議和加密驗證後，彼此互動時無需建立傳統信任關係的AI代理。
  + AI Agents: 人工智慧代理。
```
先寫這樣晚點再補

<!-- DAILY_CHECKIN_2025-10-15_START -->
<!-- Content_END -->
