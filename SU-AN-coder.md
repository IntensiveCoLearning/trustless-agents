---
timezone: UTC+8
---

# AN SU

**GitHub ID:** SU-AN-coder

**Telegram:** @AN_SU

## Self-introduction

I am a college student currently studying, aiming to become a DePIN engineer. I have a strong interest in the Ethereum architecture. Fellow enthusiasts are welcome to connect with me! 😊

## Notes
<!-- Content_START -->
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
## **自主代理经济协议栈：A2A/AP2/x402协议解析**

### **1\. A2A协议：代理间身份与通信的信任基盘**

A2A协议的核心是为去中心化环境中的AI代理建立一个可互操作的身份、发现与安全通信层。它不依赖于任何中心化的控制机构。

-   **去中心化身份**
    
    -   **格式**：代理身份通常遵循W3C去中心化标识符规范或类似的基于公钥基础设施的方法。例如：`did:pkh:eip155:1:0x1a2b3c...`。该DID通过密码学方式与一个区块链账户（EOA或智能合约钱包）绑定。
        
    -   **解析**：身份解析器通过相应的DID方法，将DID解析为其对应的DID文档，其中包含用于验证的控制器的公钥、服务端点等信息。
        
-   **代理描述符**
    
    -   这是一个公开的JSON-LD文件，充当代理的“数字名片”和“服务清单”。
        
    -   **关键字段**:
        
        -   `@context`, `id`: 遵循JSON-LD标准，`id`即为代理的DID。
            
        -   `publicKey`: 用于验证请求签名。
            
        -   `service`: 定义代理提供的服务集合。每个服务应明确其`type`（如`A2AEndpoint`，`MarketDataService`）、`serviceEndpoint`（URL）和`capabilities`（描述输入输出格式、支付要求等）。
            
    -   **完整性**：描述符本身应由代理的私钥签名（例如使用`LinkedDataSignatures`），确保其内容在传输过程中未被篡改。
        
-   **安全握手流程**
    
    1.  **请求**：发起方代理（Alice）向目标代理（Bob）的`serviceEndpoint`发送一个结构化的HTTP请求。请求头应包含：
        
        -   `Authorization: Bearer <A2A-JWT>`
            
        -   JWT的Payload部分需包含Alice的DID、Bob的DID、请求的操作、随机数和时间戳。
            
    2.  **挑战**：Bob返回`401 Unauthorized`，并提供一个高强度的随机数。
        
    3.  **签名与重试**：Alice使用自己的私钥，按照EIP-712或类似标准，对包含原始请求参数和随机数的数据进行签名。她随后重试请求，并在头中附带签名（如`Signature: <EIP-712-signature>`）。
        
    4.  **验证与执行**：Bob使用从Alice的DID文档中获取的公钥验证签名。验证通过后，执行请求的操作。
        

**核心价值**：A2A建立了代理交互的**身份层和通信层**，实现了端到端的身份验证与消息完整性，是构建信任的基石。

* * *

### **2\. AP2协议：支付意图的标准化协调层**

AP2并非支付协议本身，而是一个在A2A建立的安全通道内，用于协商和确认支付意图的元协议。它定义了“支付什么”和“如何确认”，而非“如何支付”。

-   **支付请求对象**  
    这是一个高度结构化的数据负载，在A2A握手后，由服务方代理返回。
    
    json
    
    ```
    {
      "@context": "https://ap2.org/schemas/v1",
      "type": "PaymentRequest",
      "paymentRequestId": "pr_abc123", // 唯一标识此次支付请求
      "description": "Stock data query for AAPL",
      "amount": {
        "currency": "USDC",
        "value": "0.10"
      },
      "destination": "0xRecipientAddress",
      "chainId": 8453,
      "fulfillmentCondition": { // 关键：支付完成的条件
        "type": "onChainTransaction",
        "asset": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
        "method": "transfer",
        "minConfirmations": 1
      },
      "callback": {
        "url": "https://service.com/ap2/fulfill", // 支付证明提交地址
        "method": "POST"
      },
      "expiresAt": "2025-...", // 请求有效期
    }
    ```
    
    -   `fulfillmentCondition`字段是AP2的精髓，它明确定义了何种链上事件（如特定ERC-20的`transfer`函数调用）被视为支付完成。
        
    -   `callback`机制将支付执行与服务的最终解锁解耦。
        
-   **支付流程与状态机**
    
    1.  `payment_required`：服务方返回AP2支付请求。
        
    2.  `payment_pending`：客户端确认支付请求，并开始执行支付（例如，通过x402协议）。
        
    3.  `payment_verified`：客户端在链上完成支付后，将交易哈希作为支付证明，通过HTTPS POST请求发送到服务方的`callback.url`。
        
    4.  `fulfilled`：服务方监听链上事件，验证该交易确实符合`fulfillmentCondition`中定义的条件。验证通过后，服务状态转为完成，并（通常通过另一个A2A调用）交付服务结果。
        

**核心价值**：AP2是**协调层**。它提供了一个与底层支付方式（x402、闪电网络等）无关的、机器可读的支付协商标准，实现了支付流程的标准化与自动化。

* * *

### **3\. x402协议：HTTP原生支付的原子性执行**

x402协议将HTTP协议与区块链支付深度融合，为Web服务提供了一个极简的、按次付费的支付执行层。它专注于解决“如何支付”的问题。

-   **HTTP 402响应**  
    响应体必须遵循严格的规范，以便客户端SDK能自动处理。
    
    json
    
    ```
    {
      "error": {
        "code": 402,
        "message": "Payment Required"
      },
      "maxAmountRequired": "0.10",
      "paymentInfo": {
        "assetType": "ERC20",
        "assetAddress": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
        "paymentAddress": "0xMerchantAddress",
        "chainId": 8453,
        "expiresAt": "2025-...",
        "nonce": "unique_nonce_123" // 防止重放攻击
      }
    }
    ```
    
-   **支付授权**  
    客户端构造的签名负载必须包含所有关键信息，并遵循EIP-712结构化签名标准。这确保了签名在钱包中可以被清晰地解析和展示，用户明确知道自己在为什么签名。
    
    typescript
    
    ```
    const domain = {
      name: 'x402 Payment Proxy',
      version: '1',
      chainId: 8453,
      verifyingContract: '0x...', // 可选，一个代理合约地址
    };
    const types = {
      Payment: [
        { name: 'maxAmount', type: 'string' },
        { name: 'assetAddress', type: 'address' },
        { name: 'paymentAddress', type: 'address' },
        { name: 'chainId', type: 'uint256' },
        { name: 'nonce', type: 'string' },
        { name: 'expiresAt', type: 'uint256' },
      ],
    };
    const value = {
      // ... 从402响应中填充的值
    };
    const signature = await wallet.signTypedData(domain, types, value);
    ```
    
-   **服务端验证与结算**
    
    -   **验证**：服务端中间件使用`ecrecover`或类似逻辑，从签名中还原出签名者的地址，并验证其是否有权访问该资源。
        
    -   **结算策略**：
        
        -   **直接广播**：中间件将已签名的交易直接广播到内存池。优点是即时，但可能因 gas 费问题失败。
            
        -   **提交-揭示**：客户端先提交交易的哈希（承诺），服务端授予临时访问权限；客户端随后揭示完整交易。这可以防止前端跑路。
            
        -   **支付通道**：对于高频场景，双方可先开设支付通道，x402请求验证的是通道内的余额证明签名，而非链上交易。
            

**核心价值**：x402是**执行层**。它提供了将任意HTTP端点转化为原子性（支付与服务交付同时成功或失败）付费端面的最简方案。

* * *

### **4\. 总结：协议栈的协同关系**

这三个协议构成了一个层次分明、职责分离的**自主代理经济协议栈**。

-   **A2A是基础**：它解决了“你是谁”和“如何安全地跟你说话”的问题，建立了代理网络中最根本的信任层。所有高级交互都构建在A2A建立的安全通道之上。
    
-   **AP2是协调**：在A2A的安全通道内，AP2解决了“这项服务需要什么条件才能解锁”的问题。它将支付意图从具体的支付方式中抽象出来，使得代理可以使用同一套语言来协商支付，无论底层是用x402、闪电网络还是其他未来出现的支付协议。
    
-   **x402是执行**：当AP2协商好支付条件后，x402提供了一个标准化的、HTTP友好的方式来**具体执行**支付。它是实现AP2中`fulfillmentCondition`的一种强大而具体的工具。
    

**数据流关系图**：

text

```
[ResearchAgent] --(A2A握手 & 服务请求)--> [ServiceAgent]
                                      |
                                      | (如需支付)
                                      V
[ResearchAgent] <--(AP2 PaymentRequest)-- [ServiceAgent]
                                      |
                                      | (切换至x402流程)
                                      V
[ResearchAgent] --(HTTP GET + 收到402)--> [ServiceAgent]
[ResearchAgent] --(HTTP GET + EIP-712签名)--> [ServiceAgent]
                                      |
                                      | (x402验证通过，执行服务)
                                      V
[ResearchAgent] <--(HTTP 200 + 服务数据)-- [ServiceAgent]
                                      |
                                      | (可选：声誉记录)
                                      V
                   [ERC-8004 Event Log on Blockchain]
```

简而言之，**A2A负责建立连接，AP2负责协商条件，x402负责完成支付**。三者协同工作，共同为实现真正自主、经济自足的AI代理经济体提供了完整的技术栈
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->

# **x402 开放支付标准笔记**

## **一、x402 是什么？**

-   定义：Coinbase 推出的**开放支付标准**，基于 HTTP 402 “Payment Required” 状态码，实现 AI 代理 / Web 服务的**自主支付**（无需人工干预）。
    
-   核心场景：API 访问、数据购买、AI 模型推理等，用 USDC 等稳定币结算，支持 “按使用付费”。
    
-   关键特点：无需 API 密钥、订阅或账户，纯 HTTP 原生集成，轻量化易开发。
    

## **二、为什么用 x402？**

传统支付（信用卡、PayPal、API 订阅）的问题：

1.  高成本：信用卡手续费 $0.30+2.9%，小额支付不划算；
    
2.  慢结算：ACH 需 1-3 天，信用卡授权后仍需数天到账；
    
3.  摩擦多：需注册账户、绑定支付方式、管理 API 密钥；
    
4.  不兼容 M2M：AI 代理无法自主完成支付，依赖人工干预；
    
5.  无小额支持：高手续费导致 $0.001 级微交易无法实现。
    

x402 的改进：

-   费用：近零（Base 链上约 $0.0001）；
    
-   结算：200ms 到账，即时确认；
    
-   无摩擦：无需账户 / API 密钥，AI 代理可自动处理；
    
-   支持微交易：最低 $0.001 付费。
    

## **三、核心工作流程**

1.  **客户端请求**：AI 代理 / 应用请求资源（如`GET /api/market-data`）；
    
2.  **服务器返回 402**：无有效支付时，返回 HTTP 402，附带支付详情（金额、收款地址、链网络）；
    
3.  **客户端重试（带支付）**：客户端生成签名支付（按 EIP-712 标准），重试请求时附加支付信息；
    
4.  **服务器验证并响应**：验证支付有效性→广播交易→返回请求的资源（如市场数据）。
    

## **四、核心代码示例**

### **1\. 服务器端：Node.js/Express 集成（关键是 x402 中间件）**

**javascript**

```javascript
// 1. 安装依赖：npm install @x402/express-middleware express
const express = require('express');
const { x402PaymentRequired } = require('@x402/express-middleware');

const app = express();

// 2. 配置x402中间件：保护需要付费的接口
app.get('/api/market-data', 
  x402PaymentRequired({
    amount: "0.10",          // 单次请求费用（单位：USDC）
    address: "0x1234...",    // 收款钱包地址
    assetAddress: "0xA0b86991C6218b36c1d19D4a2e9Eb0cE3606EB48", // USDC合约地址
    network: "base-mainnet"  // 区块链网络
  }), 
  // 3. 支付验证通过后，返回资源
  (req, res) => {
    res.json({
      marketData: { BTC: 50000, ETH: 2000 }, // 示例：付费后获取的实时数据
      timestamp: Date.now()
    });
  }
);

app.listen(3000, () => console.log("x402服务器运行在3000端口"));
```

### **2\. 402 响应的 JSON 格式（服务器返回给客户端的支付信息）**

**json**

```json
{
  "resource": "/api/market-data",       // 请求的资源路径
  "description": "实时市场数据访问需付费", // 可选：支付说明
  "maxAmountRequired": "0.10",          // 所需支付金额（USDC）
  "payTo": "0x1234...",                 // 收款地址
  "asset": "0xA0b86991C6218b36c1d19D4a2e9Eb0cE3606EB48", // 支付资产（USDC）合约地址
  "network": "base-mainnet",            // 区块链网络
  "nonce": "abc123",                    // 防重放攻击的唯一标识
  "expiresAt": 1717248000              // 支付请求过期时间戳
}
```

### **3\. 客户端代码：AI 代理处理 402 并重试支付**

**javascript**

```javascript
// 1. 安装依赖：npm install @x402/client your-wallet-connector
import { x402Client } from '@x402/client';
import { connectWallet } from 'your-wallet-connector'; // 连接钱包（如MetaMask）

async function getPaidResource() {
  // 2. 初始化客户端并连接钱包
  const client = new x402Client();
  const wallet = await connectWallet(); // 获取用户/代理的钱包（如USDC钱包）
  client.setWallet(wallet);

  try {
    // 3. 请求付费资源：客户端自动处理402重试
    const data = await client.fetch('https://api.example.com/api/market-data');
    console.log("获取到付费资源：", data);
    return data;
  } catch (error) {
    console.error("支付失败：", error.message);
  }
}

// 调用函数：AI代理自主获取付费数据
getPaidResource();
```

## **五、x402 关键优势**

1.  **低成本**：Base 链上交易费≈$0.0001，支持$0.001 级微交易；
    
2.  **快结算**：200ms 到账，无延迟，且支付不可撤销（无拒付风险）；
    
3.  **零摩擦**：无需注册账户、管理 API 密钥或订阅，AI 代理可全自动支付；
    
4.  **兼容性强**：HTTP 原生，支持任何区块链（EVM/SVM）和稳定币，适配现有 Web 服务；
    
5.  **安全**：支付签名遵循 EIP-712 标准，无需 PCI 合规（除非直接收信用卡）。
    

## **六、适用人群及其核心用例**

### **1\. 适用人群**

-   **卖家**：API 提供商、数字内容平台（如新闻 / 论文）、AI 模型服务商、云资源商；
    
-   **买家**：AI 代理（自主采购数据 / 算力）、开发者（快速访问付费 API）、普通用户（按次购买内容，如单篇论文）。
    

### **2\. 核心用例**

-   按请求付费 API：AI 代理查实时股市数据（$0.02 / 次）；
    
-   AI 模型推理：图像识别 API（$0.005 / 次分类）；
    
-   云资源支付：AI 代理购买 GPU 算力（$0.50/GPU 分钟）；
    
-   内容付费：用户按篇买新闻（$0.25 / 篇），无需订阅。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->


# A2A协议与组件（核心概念）

## **一、核心参与者：谁在参与 A2A 交互？**

| 参与者 | 角色说明 |
| --- | --- |
| 用户（User） | 发起请求的人 / 自动服务（如 “要订酒店的用户”） |
| A2A 客户端（Client Agent） | 代表用户做事的程序 / 代理（如 “酒店预订代理”，用 A2A 协议发请求） |
| A2A 服务器（Remote Agent） | 提供服务的代理（如 “货币换算代理”，暴露 HTTP 端点，处理任务、返回结果） |

-   关键特点：A2A 服务器对客户端是 “黑匣子”，不暴露内部逻辑 / 工具。
    

## **二、核心通信元素：交互的 “基本零件”**

| 元素 | 作用说明 | 代码示例（简化） |
| --- | --- | --- |
| 代理卡 | JSON 格式 “数字名片”，含代理地址、认证要求、功能（客户端靠它发现代理） | json { "url": "https://currency-agent/a2a", "securitySchemes": ["openIdConnect"], "capabilities": ["convertCurrency"] } |
| 任务（Task） | 有状态的工作单元（唯一 ID + 生命周期，如 “300 美元换人民币” 任务） | python class Task(BaseModel): task_id: str status: Literal["submitted", "working", "completed"] request_data: dict |
| 消息（Message） | 单轮通信内容（含角色 “user/agent”+ 唯一 ID + 内容部件） | json { "message_id": "msg-123", "role": "user", "parts": [{"type": "TextPart", "content": "换300美元"}] } |
| 部件（Part） | 内容容器（TextPart 文本 / FilePart 文件 / DataPart 结构化数据） | python class TextPart(BaseModel): type: Literal["TextPart"] content: str class DataPart(BaseModel): type: Literal["DataPart"] data: dict |
| 工件（Artifact） | 代理生成的有形结果（如换算结果文档，含唯一 ID + 部件） | json { "artifact_id": "art-456", "name": "换算结果", "parts": [{"type": "DataPart", "data": {"amount": 300, "result": 2180}}] } |

## **三、交互机制：代理怎么 “聊天”？**

3 种模式适配不同场景，核心是 “高效传数据”：

1.  **请求 / 响应（轮询）**
    
    -   逻辑：客户端发请求→服务器马上回，长任务需客户端反复问 “结果好了吗”。
        
    -   代码（客户端轮询）：
        
        python
        
        ```python
        def poll_task(task_id):
            while True:
                resp = requests.get(f"https://agent/a2a/task/{task_id}")
                if resp.json()["status"] == "completed":
                    return resp.json()["artifact"]
                time.sleep(5)  # 每5秒问一次
        ```
        
2.  **SSE 流式传输**
    
    -   逻辑：客户端连服务器后不断开，服务器有更新就主动推（如 “任务处理中→结果生成”）。
        
    -   代码（客户端收流）：
        
        python
        
        ```python
        from sseclient import SSEClient
        messages = SSEClient(f"https://agent/a2a/stream?task_id=123")
        for msg in messages:
            if msg.event == "TaskStatusUpdate":
                print(f"状态：{msg.data}")
            if msg.event == "ArtifactUpdate":
                print(f"结果：{json.loads(msg.data)}")
        ```
        
3.  **推送通知（Webhook）**
    
    -   逻辑：长任务 / 断连场景，服务器用客户端提供的 Webhook 地址，有更新就主动发请求。
        
    -   代码（服务器推通知）：
        
        python
        
        ```python
        def send_webhook(webhook_url, task_data):
            requests.post(webhook_url, json={"task_id": "123", "status": "completed", "artifact": ...})
        ```
        

## **四、核心架构与工作流程：A2A 怎么跑起来？**

### **1\. 3 步核心流程**

1.  **发现（Discovery）**：客户端找代理卡（如访问`/.well-known/agent-card.json`），确定 “和谁聊、怎么聊”。
    
2.  **认证（Authentication）**：按代理卡要求拿 “通行证”（如 JWT 令牌），证明 “我是可信的”。
    
3.  **通信（Communication）**：客户端发任务→服务器处理→返回结果 / 推更新。
    

### **2\. 代码实现：用 FastA2A 搭 A2A 服务器（Python）**

-   前提：先装库 `pip install fasta2a pydantic`
    
-   代码（货币换算代理服务器）：
    
    python
    
    ```python
    from fastapi import FastAPI
    from pydantic import BaseModel
    from fasta2a import A2AServer, Task
    
    app = FastAPI()
    # 初始化A2A服务器，绑定代理卡
    a2a_server = A2AServer(
        agent_card={
            "url": "http://localhost:8000/a2a",
            "capabilities": ["convertCurrency"],
            "securitySchemes": []  # 简化：不设认证
        }
    )
    
    # 定义换算请求数据结构
    class ConvertRequest(BaseModel):
        amount: float
        from_currency: str
        to_currency: str
    
    # 处理换算任务
    @a2a_server.task_handler("convertCurrency")
    async def handle_convert(task: Task, request: ConvertRequest):
        # 模拟换算逻辑（1USD=7.27CNY）
        rate = 7.27 if request.to_currency == "CNY" else 1/7.27
        result = request.amount * rate
        # 返回工件（结果）
        return {
            "artifact": {
                "name": "CurrencyConversionResult",
                "parts": [{"type": "DataPart", "data": {"result": result}}]
            }
        }
    
    # 挂载A2A路由
    app.include_router(a2a_server.router, prefix="/a2a")
    
    # 运行：uvicorn main:app --port 8000
    ```
    

总结思维图

![exported_image (1).png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-17-1760712730430-exported_image__1_.png)
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->



-   **A2A协议**(基础)
    

_1.为何采用它_

Agent协作之间没有统一的规则，A2A协议提供AI代理之间“开放沟通标准”，使得不同框架（如 TensorFlow、PyTorch）、不同公司开发的 AI 代理，能无缝通信、一起协作

eg：A 代理负责数据分析，B 代理负责生成报告，二者通过 A2A 高效配合

_2.解决问题场景示例_

用户使用AI Agent来货币换算服务

```
        +-----------+        +--------------------+        +----------------------+
        |   User    | -----> |    AI Assistant    | -----> | Currency Conversion  |
        | (Request) |        |    (Identifies      |        |      Agent           |
        |           |        |    Conversion Task) |        | (Converts Currency)  |
        +-----------+        +--------------------+        +----------------------+
                                                       |
                                                (Returns Conversion Result)
                                                       |
                                                    +--------------------+
                                                    |  AI Assistant      |
                                                    |  (Final Result)    |
                                                    +--------------------+
                                                       |
                                                    +-----------+
                                                    |   User    |
                                                    | (Receives |
                                                    |   Result) |
                                                    +-----------+
```

Currency Conversion Agent：专注于执行 “不同货币间的汇率查询与换算”，是 A2A 协议中的 “功能型代理”，和AI Assistant之间通过A2A协议进行通信。

Request和Result：代表用户与 AI 助手、AI 助手与代理之间的 “数据交互”，A2A 协议会规定这些交互的标准格式，确保不同代理能顺畅沟通。

ps: A2A带来的优势：靠 HTTPS 实现安全协作（代理互不可见）、打破Agent代理孤岛实现互作、保留代理自主权、标准化沟通降低集成复杂度、支持长时间运行协作与流式处理。

_3.A2A位于的代理堆栈_

代理堆栈是构建 AI 代理的 “技术组合”，从底层基础到上层通信，分为四层，每层负责不同功能：

a.模型（最底层）：AI 代理的 “大脑”，用 LLM（如 GPT、Gemini）提供推理能力，是代理思考、决策的基础

b.框架（中间层）：构建代理的 “工具包”，比如 Google 的 ADK、LangGraph、Crew AI，提供代码模板、部署工具，帮开发者快速搭代理

c.MCP（中间层）：模型与外部资源的 “连接器”，专注把模型和数据、工具（如计算器、数据库查询）对接，降低连接复杂度（工具通常无状态，只做固定功能）

d.A2A（最上层**）**：代理之间的 “通信标准”，解决不同组织、不同框架开发的代理的协作问题，让代理能以 “自主身份” 多轮交互（如谈判、任务委派）

![屏幕截图_16-10-2025_22151_a2a-protocol.org.jpeg](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-16-1760624245446-_____16-10-2025_22151_a2a-protocol.org.jpeg)

A2A和MCP的区别

|   | A2A | MCP |
| --- | --- | --- |
| 定位 | 代理间的 “通信协议” | 模型与工具和数据的 “连接协议” |
| 对象 | 两个或以上 AI 代理 | 模型 ↔ 外部工具 / 数据 |
| 能力 | 多轮复杂交互（谈判） | 简化工具调用（如查数据库） |
| 价值 | 代理怎么合作 | 模型怎么用工具 |

ps:A2A和ADK------->协议和开发协议的工具包

_4.A2A 请求生命周期_

![exported_image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-16-1760625532237-exported_image.png)
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->





-   **ERC8004**（相关概念基础分析）
    

总目录：抽象，赋予动机（身份注册表，信誉注册表，验证注册表），规范，理由

_1.抽象_

区块链跨**组织边界发现、选择代理并与代理交互**，而无需预先存在的信任，从而**实现开放式代理经济**。

根据安全需求选择三种不同信任模型：使用客户端反馈的声誉系统、通过权益安全重新执行进行验证、zkML 证明或 TEE 预言机

eg：A 公司找 B 物流企业代理运输：

不知道有哪些潜在代理（发现难）;不确定代理的资质和可信度（选择难）；协作中数据易篡改、责任难追溯（交互难）。

_2.赋予动机（身份注册表，信誉注册表，验证注册表）_

现有协议的局限：MCP（服务器提供）+A2A（代理身份验证 技能通告等等）可支撑代理基础通信，但**不涵盖代理发现与信任**，无法满足跨组织需求

ERC方案目标：在不受信任环境中，通过 3 个轻量级注册表（每链单例部署，支持 L2 / 主网），构建开放跨组织代理经济

a.身份注册表：基于 ERC-721+URIStorage，提供可移植、抗审查的代理标识符（URI 解析注册文件）

b.信誉注册表：标准反馈接口，链上（保障可组合性）+ 链下（复杂算法）评分聚合，支撑专业服务生态

c.验证注册表：通用钩子，支持独立验证者（质押者、zkML 验证者等）检查与记录

ps：身份注册表相当于给代理发“唯一身份证”，信誉注册表相当于给代理“打分记评价”，验证注册表相当于给代理“做质检”

_3.规范_

按照 [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) 和 [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174) 中的说明进行解释

_4.理由_

a.适配多协议：MCP、A2A 常用，还可能有新协议，所以用灵活注册文件，能加各种接口，同时兼容 AI 功能和 Web3 信息（钱包、域名等）

b.反馈易上手：用 A2A、MCP 已有的说法（如 “任务”“工具”），反馈格式还能自己定，不用学新规则

c.反馈低门槛：给反馈不用先注册，还能让别人帮付 Gas 费，提交顺畅

d.数据易查找：反馈核心存在链上，完整数据建议存 IPFS，用工具能快速查到

e.部署易用：每条链只装一个注册表，代理在 A 链注册，也能去其他链干活，多链注册也支持

-   **身份注册表、信誉注册表和验证注册表**
    

核心关系图如下

```
┌────────────────────────┐
│     Identity Registry   │
│   (ERC-721 Agent NFTs)  │
│    ↓ 唯一身份与URI       │
└────────────┬───────────┘
             │ agentId
             │
┌────────────▼───────────┐
│   Reputation Registry   │
│   链上评分与反馈记录     │
│   （信任信号层）        │
└────────────┬───────────┘
             │ 验证/引用
┌────────────▼───────────┐
│   Validation Registry   │
│   验证结果与证明层       │
└────────────────────────┘
```

_1.身份注册表_

a.将每个 Agent 注册为一个 **ERC-721 NFT**

b.agentId = tokenId

c.NFT的所有权即代表代理的控制权

d.`tokenURI` 指向代理的链下注册文件（JSON 结构，描述代理能力、端点、信任模型等等）

| 项目 | 内容 |
| --- | --- |
| 标准扩展 | ERC-721 + ERC721URIStorage |
| 唯一标识 | eip155:chainId:registryAddress:agentId |
| 注册文件（JSON） | 含代理名称、描述、端点（A2A/MCP/DID）、支持的信任模式等 |
| 链上函数 | register(), setMetadata(), getMetadata() |
| 链下数据 | tokenURI 指向的 JSON 文件（可在 IPFS/HTTPS 等存储） |
| 事件 | Registered, MetadataSet |
| 可组合性 | 因为是 ERC-721，Agent 可与 NFT 市场、钱包等生态直接兼容 |

_2.信誉注册表_

a.提供一个了链上反馈与授权系统

b.用户或代理可为某个`agentId` 提供评分（0~100分）

c.反馈可附带链下文件 URI（如 IPFS）（透明度更高 审计性更强）

d.允许撤销与追加响应，实现声誉的治理与修正

| 项目 | 内容 |
| --- | --- |
| 依赖 | IdentityRegistry（确保 agentId 有效） |
| 反馈结构 | score, tag1, tag2, fileURI, fileHash |
| 反馈签名 | feedbackAuth（EIP-191 / ERC-1271）授权机制 |
| 事件 | NewFeedback, FeedbackRevoked, ResponseAppended |
| 撤销功能 | 用户可撤销旧反馈（防止垃圾和错误评价） |
| 扩展性 | feedback 文件中可加入 x402 支付凭证、上下文、任务信息等 |

_3.验证注册表_

a.代理可以请求验证任务结果

b.Validator可基于 zkML、TEE、或质押机制提供链上验证结果

c.通过事件与记录建立可追踪的验证链

| 项目 | 内容 |
| --- | --- |
| 验证请求 | validationRequest(validatorAddress, agentId, requestUri, requestHash) |
| 验证响应 | validationResponse(requestHash, response, responseUri, responseHash, tag) |
| 响应值 | 0–100（可二值/多级） |
| 链下数据 | requestUri / responseUri（例如 IPFS 审计报告） |
| 事件 | ValidationRequest, ValidationResponse |
| 查询函数 | getValidationStatus(), getSummary() |
| 可组合性 | 任何验证器协议（TEE、zk、质押）都能接入 |
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
