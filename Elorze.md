---
timezone: UTC+8
---

# 云展

**GitHub ID:** Elorze

**Telegram:** @Elorze

## Self-introduction

一个爱学习的人

## Notes
<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
[https://www.youtube.com/watch?v=8lsJ7zLa2Pk：](https://www.youtube.com/watch?v=8lsJ7zLa2Pk：)

更详细地介绍了三种AI AGENT FRAMEWORK：

AUTOGEN:

中心化分布式，异步消息传递框架。邮箱式，消息流形式，每个agent内部都有收到什么信息要怎么回答。这里的agent是一个完整的人物，不可拆分为更小的单元；这些agent内部由不同的逻辑单元构成，有点类似于LANGRAPH的node，但它是封装在agent的程序控制流与消息循环里的，是隐藏的、不可见的。

LANGRAPH:

可编程图。一个agent由多个负责不同功能的node构成，这些node之间构成图一样的结构。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->

[https://www.youtube.com/watch?v=VChRPFUzJGA](https://www.youtube.com/watch?v=VChRPFUzJGA):

MCP 是一种让 AI 能安全访问外部工具和数据的开放协议，相当于 AI 的通用接口。

MCP使用场景：

让 AI 模型安全、高效地调用外部工具或数据时，比如访问数据库、执行代码、查询 API、读取文件或控制业务系统等。

使用建议：

**MCP 要与后端 API 配合使用，而不是替代它** —— MCP 是让 AI 更高效地使用现有 API 的接口层，而不是新的通用 API 标准。

**不要试图用一个 MCP 服务器做所有事情** —— 只做你独特的部分，让客户端同时连接多个 MCP 服务器协同完成任务。

**保持 MCP 服务器的抽象层级尽可能高** —— 不要让 AI 直接访问底层数据库，而是提供简化的高层工具接口以提高安全性和效率。

[https://www.youtube.com/watch?v=voaKr\_JHvF4](https://www.youtube.com/watch?v=voaKr_JHvF4):

A2A（Agent-to-Agent Protocol）:

是 Google 提出的一个开放通信协议，用于让不同 AI 代理（agents）之间能够互相发现、交流和协作。它规定了统一的消息格式、任务流程和安全机制，使来自不同平台或厂商的智能体可以像互联网网站一样互通，从而构建出多代理协作的生态系统。

A2A和MCP：

🧩 MCP 让一个 Agent 能更聪明地用工具，

🔗 A2A 让多个 Agent 能更聪明地协作。

A2A目前的问题：

⚙️ **标准尚未完善** —— A2A 目前只是 Google 提出的初步规范，不同实现之间还缺乏统一的约定，很多细节（如任务生命周期、权限模型）仍在变化。

🔐 **安全与信任机制不足** —— Agent 之间通信涉及身份认证、权限控制、数据隐私等问题，但目前还没有成熟、通用的安全框架。

🔄 **互操作性不稳定** —— 各家 Agent 框架（如 OpenAI、Anthropic、Hugging Face 等）尚未全面支持 A2A，跨平台协作容易出现兼容性问题。

🧱 **生态系统稀缺** —— 还缺少足够多的公共 Agent、工具和示例，导致开发者难以体验到多 Agent 协作的真正价值。

🚧 **开发者门槛较高** —— 实现 A2A 通信目前需要自建服务、配置复杂的元数据（如 .well-known/agent.json），对普通开发者来说还不够友好。

[https://www.youtube.com/watch?v=mFkw3p5qSuA&t=13s：](https://www.youtube.com/watch?v=mFkw3p5qSuA&t=13s：)

这个视频是A2A更全面的介绍，指导如何搭建自己的A2A项目。

A2A的缺点：有些大语言模型可能并不靠谱，但是只要套了一个代理，它就会被无条件信任。所以需要额外的质量保证机制来补充身份认证的不足。

[https://www.youtube.com/watch?v=8HqeY5v0ohM：](https://www.youtube.com/watch?v=8HqeY5v0ohM：)

介绍了三种AI Agent Framework：AutoGen CrewAI LangGraph。

AutoGen难用，LangGraph依赖生态。看起来CrewAI最好上手。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
