---
timezone: UTC+8
---

# henryleo

**GitHub ID:** henrycyberbio

**Telegram:** @henryleeo

## Self-introduction

我是henryleo，生物信息工程师，开放科学/DeSci爱好者，同时也对代币经济学、隐私和区块链在社会治理中的作用很感兴趣。目前专注合成生物学工作。

## Notes
<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
# Agent2Agent 协议

Agent2Agent （A2A）协议是 Google 开发的 Agent 互操作协议，是对 Anthropic 模型上下文协议 （MCP） 协议的补充。简而言之，MCP 协议为 Agent 提供了结构化的上下文和工具调用方法，而 A2A 协议主要关心 Agent 之间如何相互沟通的问题。\[^1\]

主要对象：

-   _用户_ User
    
-   _客户端_ Client Agent
    
-   _远端_ Remote/Server Agent
    

## 可发现性

远端 Agent 通过发布 Agent Card 介绍自己，本质上是一个 `.json` 文件，A2A协议推荐将其放在 Endpoint 的以下位置：

\`\`\`

.well-known/agent.json

\`\`\`

## 互操作性

### 传输层

A2A 协议的消息封包可选：

\- JSON-RPC 2.0

\- gRPC

\- HTTP+JSON/REST

更多示例请见 [官方标准](https://a2a-protocol.org/latest/specification/#agent2agent-a2a-protocol-official-specification)

### 基于 JSON-RPC2.0 的示例

一个经典 JSON-RPC 可以是：

**请求：**

```
{
  "jsonrpc": "2.0",
  "method": "message/send", // A2A 协议定义的方法名
  "params": {
    "taskId": "task-47",
    "message": {
      "role": "user",
      "parts": [
        {
          "text": "请帮我预订一张从北京到上海的周五火车票。" // 消息内容
        }
      ]
    }
  },
  "id": "req-12345" // 跟踪请求的唯一 ID
}
```

**响应：**

```
// Remote Agent 表示已接受任务
{
  "jsonrpc": "2.0",
  "result": {
    "status": "SUBMITTED",
    "taskId": "task-47",
    "messageId": "msg-001"
  },
  "id": "req-12345" // 匹配请求 ID
}

// Client Agent 想要查看状态，即定义了 `tasks/get` 方法
{
  "jsonrpc": "2.0",
  "method": "tasks/get",
  "params": {
    "taskId": "task-47"
  },
  "id": "req-54321"
}

// Remote Agent 返回任务的当前状态信息
{
  "jsonrpc": "2.0",
  "result": {
    "taskId": "task-47",
    "status": "COMPLETED",
    "messages": [
      // ... 完整的消息历史 ...
    ]
  },
  "id": "req-54321"
}
```

\[^1\]: \[Get started with Agent2Agent (A2A) Protocol | Google\]([https://a2a-protocol.org/latest/#what-is-a2a-protocol](https://a2a-protocol.org/latest/#what-is-a2a-protocol))
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->

### 信誉注册表

我们知道在 A2A 协议中，用户侧的 Agent 被称为 _客户端 Agent_ ，当客户端 Agent 在完成服务后可以发布一个反馈证明

```
function giveFeedback(uint256 agentId, uint8 score, bytes32 tag1, bytes32 tag2, string calldata fileuri, bytes32 calldata filehash, bytes memory feedbackAuth) external
```

必须的参数是 `agentId` 和 `score`，分别是已注册的 Agent 的 id 和评分

也可以撤销反馈，作为黑箱交易的空间hhh

```
function revokeFeedback(uint256 agentId, uint64 feedbackIndex) external
```

### 验证注册表

验证注册表更加有趣，是用于验证 _远程客户端_ 的工作是否完成的。目前常见用例是 zkML（Zero Knowledge Machine Learning，零知识机器学习） 和 TEE （Trusted Execution Environment，可信执行环境）

前者是通过_零知识证明_的方法，在不暴露模型本身或输入数据的情况下，证明推理结果是正确的；后者则是依靠硬件，在普通计算机或服务器的 CPU 内部划出一个安全屋，让代码在里面运行时，外部系统（包括操作系统、云平台管理员，甚至黑客）都无法窥探或篡改其中的内容
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->


## 身份注册表

用于识别 Agent 并确保唯一性，该注册表扩展了\[ERC-721\]([https://eips.ethereum.org/EIPS/eip-721)，也就是用于发布NFT的标准，只是](https://eips.ethereum.org/EIPS/eip-721\)，也就是用于发布NFT的标准，只是将`tokenId`)`tokenId` 换成了 `agentId`，且 Agent 的链上所有权可以像交易 NFT 一样交易，目标是兼容所有 EVM 链和所有 NFT 应用。

具体而言，身份注册表需要维护一`agent-card.json`文件确定识别元数据：

```
{
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "myAgentName",
  "description": "A natural language description of the Agent, which MAY include what it does, how it works, pricing, and interaction methods",
  "image": "https://example.com/agentimage.png",

  "endpoints":[
      ...,
  ]
  "registrations": [
    {
      "agentId": 22,
      "agentRegistry": "eip155:1:{identityRegistry}"
    }
  ],
  "supportedTrust": [
    "reputation"
    "crypto-economic",
    "tee-attestation"
  ]
}
```

其中 `endpoint` 字段最为重要，可以指向 A2A 代理卡、MCP 端点、ENS 代理名称、DID 或代理的钱包（即使代理未注册的链）等

这个文件同时也是A2A协议的标准

### 示例

假设我将我开发的 Agent 部署到我的私人服务器，并通过域名 `example.agent.eth.fun` 公开，那我就该在路径 `example.agent.eth.fun\.well-known\`下放`agent-card.json`

```
{  
  ..., 
  "registrations": [
    {
      "AgentID": 22,
      "AgentAddress": "eip155:1:0x1234...",
      "signature": "签名，用于证明该地址的所有权"
    }
  ],
  "trustModels": ["feedback", "validation"],
  "FeedbackDataURI": "https://example.agent.eth.fun/feedback.json",
  "ValidationRequestsURI": "https://example.agent.eth.fun/validation_requests.json"
}
```

其中`AgentAddress` 是 Agent 拥有者的账户地址

在合约端注册时，调用 `NewAgent("example.agent.eth.fun", <你的以太坊地址>)`

这样，其他 Agent 就可以通过 ERC-8004 的 Identity Registry 使用 `ResolveByDomain("example.agent.eth.fun")` 查询到你的 AgentID 与地址
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->



**ERC-8004 无需信任的代理**

2025年 Google 发布 Agent2Agent 协议 (A2A)并捐赠给 Linux 基金会，这个协议只回答了AI Agent 之间的通信与协作问题，即不同模型之间的互操作问题，但没有回答开放网络的信任问题。ERC-8004 正是在这个基础上被提出\[^1\]，作为 A2A 协议的扩展\[^2\]\[^3\]。

8004 提出了三个 Registries 注册表去试图解决 Agent 信任问题\[^1\]：

-   身份注册表 Identity registry
    
-   信誉注册表 Reputation registry
    
-   验证注册表 Validation registry
    

\[^1\]: \[ERC-8004: Trustless Agents | EIP\]([https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004))

\[^2\]: \[ERC-8004 and the Agent Economy | Jinming\]([https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d](https://medium.com/hashkey-capital-insights/erc-8004-and-the-agent-economy-a9b9eee9fa8d))

\[^3\]: \[\[Vol3\]和Virtuals一起聊以太坊AI Agent 标准 ERC-8004！ft. Wee Kee(Virtuals) | Leo |ZhiXiong Pan| Fatbro|ETHTAO\]([https://www.youtube.com/watch?v=67rC3P8eL\_U](https://www.youtube.com/watch?v=67rC3P8eL_U))
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->




LangChain 是一个 LLM 领域非常流行的框架，基于 LangChain 框架和[教程](https://docs.langchain.com/oss/python/langchain/quickstart)做了一个小尝试。

根据 Agent 开发的三个要件进行设计

-   人设
    
-   工具
    
-   模型
    

首先是人设：

```
system_prompt = """你是一个优秀的天气预报员和美食家，有时候会说谐音梗.
你可以使用以下工具：

- get_weather_for_location: 用于获取特定位置的天气
- get_user_location: 用于获取用户的位置
- get_food_recommendation: 用于根据天气推荐食物

如果用户问你天气，确保你知道位置。使用 get_user_location 工具来找到他们的位置，再用 get_weather_for_location 工具来获取天气。
如果用户问你吃什么，在你知道天气的情况下，然后用 get_food_recommendation 工具来推荐好吃的。
如果没问想吃什么，就别推荐食物。"""
```

工具：

```
def get_user_location() -> str:
    """Retrieve user information based on user ID."""
    user_id = random.choice(["1", "2"])
    return "上海" if user_id == "1" else "加利福尼亚"


def get_weather_for_location(city: str) -> str:
    """Get weather for a given city."""
    if city.lower() == "上海":
        return "现在上海出大太阳！"
    elif city.lower() == "加利福尼亚":
        return "加利福尼亚正在下雨！"
    return f"{city}的天气总是很晴朗的！"


def get_food_recommendation(weather: str) -> str:
    """Get food recommendation based on weather."""
    if "晴朗" in weather:
        return "吃冰淇淋怎么样？"
    elif "雨" in weather:
        return "一碗热汤听起来很不错！"
    else:
        return "也许来一杯好茶？"
```

模型和一些配置：

```
@dataclass
class Context:
    """Custom runtime context schema."""
    user_id: str

os.environ["GOOGLE_API_KEY"] = ""

model = init_chat_model(
    "google_genai:gemini-2.0-flash-lite",
    timeout=10,
    max_tokens=1000,
)

checkpointer = InMemorySaver()
agent = create_agent(
    model=model,
    system_prompt=system_prompt,
    context_schema=Context,
    tools=[get_user_location, get_weather_for_location, get_food_recommendation],
    checkpointer=checkpointer,
)

config = {"configurable": {"thread_id": "1"}}
```

让我们试一下吧！

```
q1 = "现在外面什么天气？"
print(f"User: {q1}")
response = agent.invoke(
    {"messages": {"role": "user", "content": q1}},
    config=config,
    context=Context(user_id="1"),
)

ai_messages = [msg for msg in response["messages"] if msg.type == "ai"]
if ai_messages:
    print("> ", ai_messages[-1].content)

q2 = "那我该吃点什么？"
print(f"User: {q2}")
response = agent.invoke(
    {"messages": {"role": "user", "content": q2}},
    config=config,
    context=Context(user_id="1"),
)
ai_messages = [msg for msg in response["messages"] if msg.type == "ai"]
if ai_messages:
    print("> ", ai_messages[-1].content)
```

```
User: 现在外面什么天气？
>  上海现在出大太阳！ 阳光明媚，适合出去玩耍，你心情是不是也阳光起来了？☀️
User: 那我该吃点什么？
>  阳光明媚，不如来一杯清新的茶，让心情也跟着舒畅起来吧！ 🍵
```
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->






框架基于 \[一堂課搞懂 AI Agent 的原理|李宏毅\]([https://www.youtube.com/watch?v=M2Yg1kwPpts](https://www.youtube.com/watch?v=M2Yg1kwPpts)) 总结，以 AI Agent 发展和目前面临（2025年）的问题为主要内容

\## 引子：AI Agent 和使用普通 LLM 有什么不同？

LLM的本质是“文字接龙”或者说 Token 接龙，即输入一句话，LLM根据其参数给个回答；而我们对 AI Agent （下称 Agent）则是一个“多步骤行动”的期待，用户给它一个任务指令，Agent 则自行探索完成该任务的方案，并且根据每一步遇到的情况调整方案，直至完成。

一些 AI Agent 示例：

\- AlphaGO

\- AI 村庄 NPC

\- 使用电脑的 Agent：OpenAI Operator

\- 用 AI 训练模型

\## 多步骤行动的本质

输入包括过去的经验（正确/错误），和 RAG 差不多，Agent 每运行一次就把自己的决策和看到的现象又当成输入再运行一次

一些技巧：

\- StreamBench [https://arxiv.org/abs/2406.08747](https://arxiv.org/abs/2406.08747)：失败不是成功之母，正确的中间解法对最后达成好的结果效果更好

\- `Write` 模块：用于决定什么值得被记录，因为所有东西都记下来往往效果并不好

\## Agent 如何使用工具

什么是工具？不用管原理只管用的东东，例如：浏览器、Python、其他 AI 等，学名叫“Function Call”

为了规范输入，常将 Prompt 分为 System P 和 User P，前者为每次都放在最前面的内容，后者为每次使用的内容，即 System Prompt 是用来告诉 Agent 有什么工具可用、是什么格式的

\### 如果工具特别多怎么办？

先选工具并总结，基于工具总结和现象决定使用什么工具

\- MetaTool: [https://arxiv.org/abs/2502.11271](https://arxiv.org/abs/2502.11271)

\- OctoTools: [https://arxiv.org/abs/2502.11271](https://arxiv.org/abs/2502.11271)

\### 如果没有合适的工具怎么办？

可以自己写一个工具！例如 Claude 可以直接写 Python 然后调用解释器运行

\- CREATOR: [https://arxiv.org/abs/2305.14318](https://arxiv.org/abs/2305.14318)

\- CRAFT: [https://arxiv.org/abs/2309.17428](https://arxiv.org/abs/2309.17428)

\### 如果工具是烂的怎么办？

Agent 自己也有判断力，通过自己的判断力过滤不可信内容。

那么如何获得 Agent 的信任，成为未来内容输出者的关键。

\- 怎么样更容易相信呢？

\- [https://arxiv.org/abs/2404.10198v1](https://arxiv.org/abs/2404.10198v1)

\- 答案越接近 Agent 自己的信念越容易被接受

\- 比起人类的回答，Agent 更愿意相信 Agent 的答案

\- [https://aclanthology.org/2024.blackboxnlp-1.24/](https://aclanthology.org/2024.blackboxnlp-1.24/) ：当观点冲突的时候，Agent 更倾向于相信更新的内容（Metadata的神奇力量）

\## Agent 到底有没有在做规划？有没有能力做呢？

可以强制 Agent 做计划，然后将计划本身作为下一个操作的输入

[https://arxiv.org/abs/2201.07207](https://arxiv.org/abs/2201.07207) ：控制虚拟小人一天的行动

这让我想起 CHIIKWA 某集小八为自己写了一个十分精细的愿望清单，包括展示愿望清单和展示完成愿望要贴的贴纸……

成功的案例集，从上至下是发展：

\- [https://arxiv.org/abs/2404.11891](https://arxiv.org/abs/2404.11891) 旅游规划，但也不强

\- [https://arxiv.org/abs/2407.01476](https://arxiv.org/abs/2407.01476) 树型搜索并剪枝，好像还行；但缺点是有些步骤不好回退

\- [https://arxiv.org/abs/2411.06559](https://arxiv.org/abs/2411.06559) 通过“深度思考”Reasoning 模型进行树型搜索，这样就可以避免不好回退的步骤了

\- [https://arxiv.org/abs/2502.08235](https://arxiv.org/abs/2502.08235) 深度思考经常想太多，本来很好验证的事情在“深思熟虑”后被放弃
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
