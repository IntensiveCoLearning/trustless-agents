---
timezone: UTC+8
---

# Swift Evo

**GitHub ID:** Swiftevo

**Telegram:** @Swiftevo

## Self-introduction

Swift Evo

## Notes
<!-- Content_START -->
# 2025-10-26
<!-- DAILY_CHECKIN_2025-10-26_START -->
[https://aurracloud.com/showcase/6b4c844b-4976-4183-9889-c684a1a30b70](https://aurracloud.com/showcase/6b4c844b-4976-4183-9889-c684a1a30b70)  
  
A Telegram bot to record and evaluate decentralized science project achievements and store them on Google Drive or IPFS. Future plans include rewards distribution and DeSci agent registration in Asia.
<!-- DAILY_CHECKIN_2025-10-26_END -->

# 2025-10-25
<!-- DAILY_CHECKIN_2025-10-25_START -->

在建立aurracloud AI前，先要想好實際的應用場景。而不是為做而做。

[https://aurracloud.com/dashboard/agents/create/wizard](https://aurracloud.com/dashboard/agents/create/wizard)
<!-- DAILY_CHECKIN_2025-10-25_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->


今天開始手動嘗試 Aurracloud 看能否無痛建立一個AI agent 再結合 x402  
  
[https://aurracloud.com/dashboard](https://aurracloud.com/dashboard)
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->



[https://www.youtube.com/watch?v=pL5LxhZ8iCY](https://www.youtube.com/watch?v=pL5LxhZ8iCY)  
  
繼續學習 x402 coinbase
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->




[https://www.youtube.com/watch?v=pL5LxhZ8iCY](https://www.youtube.com/watch?v=pL5LxhZ8iCY)  
  
學習 coinbase 發表關於 x402 的分享
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->





Chat with AI for understanding about 8004 and the twitter post about x402 as well

https://x.com/tinyxiong\_eth/status/1980542373018103863?t=DtscjHYs\_BQzH9Gc5ZIOzw&s=19
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->






由於新手，在看到不同的佈署編碼時，我都帶有資訊透露的風險。今天查問了以下的問題，為本地模擬以及鏈上佈署做好準備。  
  
[https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68f27943-1578-8330-9759-8e76a6c21a51](https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68f27943-1578-8330-9759-8e76a6c21a51)  
  

* * *

## 🧠 問題 1：

> 「在本地模擬執行，是指在自己電腦上模擬。但並不連接網絡，也不連接區塊鏈？」

✅ **完全正確！**  
在區塊鏈開發裡，「本地模擬執行」通常是指：

> 在你的電腦上開啟一條「模擬以太坊網絡」的私有鏈，  
> 它只存在於你的電腦記憶體中，不連接到真實的區塊鏈。

* * *

### 💻 常見模擬工具

| 工具 | 用途 |
| --- | --- |
| Hardhat Network | Hardhat 內建的模擬以太坊網路（本地鏈） |
| Ganache | 另一個圖形介面的本地以太坊模擬器 |
| Anvil (Foundry) | 超快的 Rust 實作版本 |

* * *

### 🔍 模擬時的特性

-   一切交易都在你電腦內執行
    
-   不需要網路、也不花任何真實 ETH
    
-   交易與區塊是即時生成的
    
-   你可以隨時重啟鏈、重設狀態
    

換句話說：

> 它就像是一個「虛擬區塊鏈實驗室」。

* * *

## 🧱 問題 2：

> 「部署區塊鏈時，會透露了自己電腦的哪些資訊？」

這個問題非常關鍵 👀  
我們要分成兩種情境：

* * *

### 🧩 (1) 在「本地模擬鏈」上部署

-   不會連線網路
    
-   不會傳出任何資料
    
-   不會洩漏 IP、帳號或電腦名稱  
    ✅ 所有交易都留在你電腦裡
    

* * *

### 🌐 (2) 在「真實網路」上部署（例如 Ethereum testnet 或 mainnet）

這時候你會：

-   連線到節點（RPC provider，如 Infura、Alchemy）
    
-   使用錢包簽署交易
    
-   把交易送上區塊鏈
    

區塊鏈節點（或 RPC 提供者）看到的只有：

| 可見資訊 | 說明 |
| --- | --- |
| 你的錢包地址（公鑰） | 例如 0x1234...abcd |
| 交易內容（合約部署的 bytecode） | 智能合約的編譯結果 |
| gas 費用與 nonce | 區塊鏈交易參數 |
| IP（只有 RPC 節點看到，不會上鏈） | 例如 Infura 伺服器可能看到來源 IP，用於防濫用保護 |

🧡 **不會洩漏的東西：**

-   你的電腦名稱
    
-   系統登入帳號
    
-   本地資料
    
-   任何私密檔案
    

* * *

### ⚠️ 提醒：

如果你使用 **Infura / Alchemy / QuickNode** 這類 RPC 服務，  
它們會記錄：

-   你的請求次數
    
-   來源 IP（僅在伺服器端，用於安全與流量分析）  
    但這些資訊不會上鏈，也不會與你的合約公開關聯。
    

* * *

## 🔐 問題 3：

> 「編碼中需要輸入 AI agent 的 private key，透露了 private key 不會造成 agent 錢包被 hack 嗎？」

💀 非常好的警覺，這是 **最常見的新手陷阱之一！**

* * *

### 🧩 Private Key（私鑰）是什麼？

它是你的「區塊鏈身份密碼」  
👉 只要別人拿到這把鑰匙，就可以完全控制你的錢包。  
無論是人還是 AI agent，原理都一樣。

* * *

### 🚫 千萬不要：

-   在程式碼中**直接寫出私鑰**（例如 `PRIVATE_KEY="0xabc..."`）
    
-   上傳含有私鑰的檔案到 GitHub
    
-   把 `.env` 檔案公開分享
    
-   在聊天室或測試代碼裡貼出私鑰
    

* * *

### ✅ 正確做法：

1️⃣ **使用環境變數 (**`.env`**) 儲存私鑰**

```bash
# .env
PRIVATE_KEY=0x1234567890abcdef...
```

2️⃣ **在程式中引用但不顯示**

```javascript
require("dotenv").config();
const PRIVATE_KEY = process.env.PRIVATE_KEY;
```

3️⃣ **把** `.env` **加入** `.gitignore`  
確保這個檔案永遠不會上傳：

```
# .gitignore
.env
```

4️⃣ **用專門錢包做測試**

-   建立一個新的測試錢包（不放真錢）
    
-   在 **Sepolia testnet** 上領取測試用 ETH（免費）
    

5️⃣ **永遠不要用你主錢包的私鑰做開發！**

* * *

### 🧠 額外安全建議

-   **硬體錢包**：部署正式合約時用 Ledger 或 Trezor
    
-   **多簽合約**：重要資金放多簽帳戶
    
-   **離線簽署 (offline signing)**：在安全環境簽好交易，再送出
    

* * *

## ✅ 總結

| 問題 | 答案 |
| --- | --- |
| 1️⃣ 本地模擬鏈會連網嗎？ | 不會，一切在你電腦內執行 |
| 2️⃣ 部署時會洩漏電腦資訊嗎？ | 不會，只有錢包地址與交易內容會公開；RPC 節點可能看到你的 IP，但不上鏈 |
| 3️⃣ 輸入 private key 會有風險嗎？ | 會！請務必放在 .env 檔案並保密，不要上傳或分享 |

* * *
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->







[https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68f27943-1578-8330-9759-8e76a6c21a51](https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68f27943-1578-8330-9759-8e76a6c21a51)

繼續和AI對話，學習 8004 的 coding ；同時嘗試了解 MCP, A2A 與 ADK 的分別  
  
[https://codelabs.developers.google.com/codelabs/currency-agent?hl=zh\_tw#0](https://codelabs.developers.google.com/codelabs/currency-agent?hl=zh_tw#0)
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->








[https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68f27943-1578-8330-9759-8e76a6c21a51](https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68f27943-1578-8330-9759-8e76a6c21a51)

透過 bot 學習整個佈署的流程，了解當中不明白的專業名語及工具，一一拆解以下兩部份。明天繼續下一步部份的學習。

第1部安裝 hardhat  
bash npm install --save-dev hardhat npx hardhat init

第2部建立專案結構 lua my-agent-project/ ├─ contracts/ │ └─ IdentityRegistry.sol ├─ scripts/ │ └─ deploy.js ├─ test/ │ └─ test\_identity.js ├─ hardhat.config.js └─ package.json  
  
學習了 A2A 的基本概念, 這8分鐘的講解很精彩！  
[https://youtu.be/Fbr\_Solax1w](https://youtu.be/Fbr_Solax1w)
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->










參加了 workshop ，對於 ERC 8004 的整理流程有了進一步理解，也提出了關於注冊的相關問題
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->











一無所知的第一天  
  
靠著AI和翻譯，大概知道了三個功能︰注冊、聲譽系統以及審核。其他的功能和細節，可能隨著更多知識的累積才回來再看。  
[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)  
  
看慬了這個ERC 8004 背後的原因，終於來了。一個去中心化方式去管理AI。  
[https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879](https://medium.com/survival-tech/the-story-behind-erc-8004-next-steps-ec46c18d1879)  
  
很好地解釋了整個 AI 的流程和經濟，當中的 How it works 清晰而容易理解  
[https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d](https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d)  
  
同時透過 ChapGBT 了解了VAS, TEEs ，感受到學習的樂趣。有了 AI 的幫助下，學習的行政成本大大減低。求知的慾望一個接一個出現  
[https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68ef8ae4-61fc-8330-8942-162d29db5dbe](https://chatgpt.com/g/g-68da14310f6c81918d088bd729edefce-erc-8004-qa/c/68ef8ae4-61fc-8330-8942-162d29db5dbe)
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
