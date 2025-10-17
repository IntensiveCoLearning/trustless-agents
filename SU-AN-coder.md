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
