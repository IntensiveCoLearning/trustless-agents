---
timezone: UTC+8
---

# pzx

**GitHub ID:** liwnldutng

**Telegram:** @looken awayry

## Self-introduction

大家好，我是一名工科生。目前工作与工程与实验相关，我对ai与web3充满好奇，也在不断学习中，期待收获更多。

## Notes
<!-- Content_START -->
# 2025-10-25
<!-- DAILY_CHECKIN_2025-10-25_START -->
#ERC\\-8004

基于以太坊\\（Ethereum\\）的新标准，用于为\*\*AI 智能体\\（Agent\\）\*\* 建立一个\*\*去信任的协调层\\（trustless coordination layer\\）\*\*。它在Google 提出的\*\*Agent-to-Agent\\（A2A\\）\*\* 协议基础上进行了扩展，引入了 **链上身份注册、信誉注册与验证注册机制**，从而使自主智能体能够在没有预先信任关系的情况下，跨组织安全、可验证地进行交互与协作。 

**身份注册表\\（Identity Registry\\）   
为每个智能体分配唯一、抗审查的 AgentID，并将其以太坊地址和域名映射到一个**AgentCard\*\*\\（JSON 文件\\），其中描述智能体的技能、能力与信任模型。 

\*\*信誉注册表\\（Reputation Registry\\）   
负责授权智能体之间的反馈；反馈数据本身保存在链下，从而允许灵活的信誉评分与见证系统。

**验证注册表\\（Validation Registry\\）   
用于记录与验证任务执行情况，可支持** 经济质押验证**\*\***（验证者抵押代币以获得经济激励）或\*\*加密验证\*\*\\（如可信执行环境 TEE 或零知识证明 zk-Proof\\）

**TEE\\(Trusted Execution Environment,可信执行环境\\)**是一种硬件级安全技术，用于确保计算在一个受保护的、不可篡改的环境中执行。它常见于 CPU 芯片中。在 ERC-8004 中的作用：TEE 用于实现\*\*高安全等级的验证模型\*\*\\（High-Stake Validation\\）。  
当一个 AI 智能体执行关键任务\\（如医疗诊断或金融操作\\）时，它可以：

1.在 TEE 内运行；

2.生成一份加密证明\\(attestation\\），证明任务在可信硬件中执行；

3.其他智能体或验证者通过该证明确认任务结果的真实性。 

**zk-Proof\\（零知识证明，Zero-Knowledge Proof\\）**是一种密码学方法，用来在不泄露原始数据内容的情况下，证明某个声明是真实的。在 ERC-8004 中的作用：用于实现加密验证模型\\（Cryptographic Validation\\）。例如：一个智能体在链下完成某个任务（比如模型推理），然后生成一个零知识证明，提交到链上；其他智能体或验证者无需重算整个任务，就能确认该任务确实被正确执行。就像比特币上用私钥签名公钥解密。
<!-- DAILY_CHECKIN_2025-10-25_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->

**#A2A 协议**

**A2A\\（Agent-to-Agent Protocol\\）** 是一个开放标准，用于让不同来源、不同框架的 AI 智能体可以彼此发现、通信、协作与执行任务。

  
\*\*A2A = 智能体之间的\\“HTTP 标准 + JSON-RPC 通信协议\\”\*\*

##A2A 协议的核心组成

| 模块 | 功能说明 |
| Agent Card（智能体卡片） | JSON 文件，描述智能体的能力、接口、安全机制等（相当于“数字名片”）。 |
| Discovery（发现机制） | 通过访问 https://{agent_domain}/.well-known/agent-card 来发现 Agent。 |
| Authentication（身份认证） | 采用 OpenID Connect 或 JWT 令牌机制。 |
| sendMessage / sendMessageStream | 标准 API，用于发送任务或流式请求（支持异步任务与长连接）。 |
| Artifacts（产物） | 任务执行后生成的结果对象，如文档、图片、数据流等。 |
| Context ID | 用于维持多轮对话或任务上下文的标识符。 |
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->


#ERC\\-8004

基于以太坊\\（Ethereum\\）的新标准，用于为\*\*AI 智能体\\（Agent\\）\*\* 建立一个\*\*去信任的协调层\\（trustless coordination layer\\）\*\*。它在Google 提出的\*\*Agent-to-Agent\\（A2A\\）\*\* 协议基础上进行了扩展，引入了 **链上身份注册、信誉注册与验证注册机制**，从而使自主智能体能够在没有预先信任关系的情况下，跨组织安全、可验证地进行交互与协作。 

**身份注册表\\（Identity Registry\\）   
为每个智能体分配唯一、抗审查的 AgentID，并将其以太坊地址和域名映射到一个**AgentCard\*\*\\（JSON 文件\\），其中描述智能体的技能、能力与信任模型。 

\*\*信誉注册表\\（Reputation Registry\\）   
负责授权智能体之间的反馈；反馈数据本身保存在链下，从而允许灵活的信誉评分与见证系统。

**验证注册表\\（Validation Registry\\）   
用于记录与验证任务执行情况，可支持** 经济质押验证**\*\***（验证者抵押代币以获得经济激励）或\*\*加密验证\*\*\\（如可信执行环境 TEE 或零知识证明 zk-Proof\\）

**TEE\\(Trusted Execution Environment,可信执行环境\\)**是一种硬件级安全技术，用于确保计算在一个受保护的、不可篡改的环境中执行。它常见于 CPU 芯片中。在 ERC-8004 中的作用：TEE 用于实现\*\*高安全等级的验证模型\*\*\\（High-Stake Validation\\）。  
当一个 AI 智能体执行关键任务\\（如医疗诊断或金融操作\\）时，它可以：

1.在 TEE 内运行；

2.生成一份加密证明\\(attestation\\），证明任务在可信硬件中执行；

3.其他智能体或验证者通过该证明确认任务结果的真实性。 

**zk-Proof\\（零知识证明，Zero-Knowledge Proof\\）**是一种密码学方法，用来在不泄露原始数据内容的情况下，证明某个声明是真实的。在 ERC-8004 中的作用：用于实现加密验证模型\\（Cryptographic Validation\\）。例如：一个智能体在链下完成某个任务（比如模型推理），然后生成一个零知识证明，提交到链上；其他智能体或验证者无需重算整个任务，就能确认该任务确实被正确执行。就像比特币上用私钥签名公钥解密。

**#A2A 协议**

**A2A\\（Agent-to-Agent Protocol\\）** 是一个开放标准，用于让不同来源、不同框架的 AI 智能体可以彼此发现、通信、协作与执行任务。

  
\*\*A2A = 智能体之间的\\“HTTP 标准 + JSON-RPC 通信协议\\”\*\*

##A2A 协议的核心组成

| 模块 | 功能说明 |
| Agent Card（智能体卡片） | JSON 文件，描述智能体的能力、接口、安全机制等（相当于“数字名片”）。 |
| Discovery（发现机制） | 通过访问 https://{agent_domain}/.well-known/agent-card 来发现 Agent。 |
| Authentication（身份认证） | 采用 OpenID Connect 或 JWT 令牌机制。 |
| sendMessage / sendMessageStream | 标准 API，用于发送任务或流式请求（支持异步任务与长连接）。 |
| Artifacts（产物） | 任务执行后生成的结果对象，如文档、图片、数据流等。 |
| Context ID | 用于维持多轮对话或任务上下文的标识符。 |
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->



**#A2A 协议**

**A2A\\（Agent-to-Agent Protocol\\）** 是一个开放标准，用于让不同来源、不同框架的 AI 智能体可以彼此发现、通信、协作与执行任务。

  
\*\*A2A = 智能体之间的\\“HTTP 标准 + JSON-RPC 通信协议\\”\*\*

##A2A 协议的核心组成

| 模块 | 功能说明 |
| Agent Card（智能体卡片） | JSON 文件，描述智能体的能力、接口、安全机制等（相当于“数字名片”）。 |
| Discovery（发现机制） | 通过访问 https://{agent_domain}/.well-known/agent-card 来发现 Agent。 |
| Authentication（身份认证） | 采用 OpenID Connect 或 JWT 令牌机制。 |
| sendMessage / sendMessageStream | 标准 API，用于发送任务或流式请求（支持异步任务与长连接）。 |
| Artifacts（产物） | 任务执行后生成的结果对象，如文档、图片、数据流等。 |
| Context ID | 用于维持多轮对话或任务上下文的标识符。 |
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->




#ERC\\-8004

基于以太坊\\（Ethereum\\）的新标准，用于为\*\*AI 智能体\\（Agent\\）\*\* 建立一个\*\*去信任的协调层\\（trustless coordination layer\\）\*\*。它在Google 提出的\*\*Agent-to-Agent\\（A2A\\）\*\* 协议基础上进行了扩展，引入了 **链上身份注册、信誉注册与验证注册机制**，从而使自主智能体能够在没有预先信任关系的情况下，跨组织安全、可验证地进行交互与协作。 

**身份注册表\\（Identity Registry\\）   
为每个智能体分配唯一、抗审查的 AgentID，并将其以太坊地址和域名映射到一个**AgentCard\*\*\\（JSON 文件\\），其中描述智能体的技能、能力与信任模型。 

\*\*信誉注册表\\（Reputation Registry\\）   
负责授权智能体之间的反馈；反馈数据本身保存在链下，从而允许灵活的信誉评分与见证系统。

**验证注册表\\（Validation Registry\\）   
用于记录与验证任务执行情况，可支持** 经济质押验证**\*\***（验证者抵押代币以获得经济激励）或\*\*加密验证\*\*\\（如可信执行环境 TEE 或零知识证明 zk-Proof\\）

**TEE\\(Trusted Execution Environment,可信执行环境\\)**是一种硬件级安全技术，用于确保计算在一个受保护的、不可篡改的环境中执行。它常见于 CPU 芯片中。在 ERC-8004 中的作用：TEE 用于实现\*\*高安全等级的验证模型\*\*\\（High-Stake Validation\\）。  
当一个 AI 智能体执行关键任务\\（如医疗诊断或金融操作\\）时，它可以：

1.在 TEE 内运行；

2.生成一份加密证明\\(attestation\\），证明任务在可信硬件中执行；

3.其他智能体或验证者通过该证明确认任务结果的真实性。 

**zk-Proof\\（零知识证明，Zero-Knowledge Proof\\）**是一种密码学方法，用来在不泄露原始数据内容的情况下，证明某个声明是真实的。在 ERC-8004 中的作用：用于实现加密验证模型\\（Cryptographic Validation\\）。例如：一个智能体在链下完成某个任务（比如模型推理），然后生成一个零知识证明，提交到链上；其他智能体或验证者无需重算整个任务，就能确认该任务确实被正确执行。就像比特币上用私钥签名公钥解密。
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->





#ERC\\-8004

基于以太坊\\（Ethereum\\）的新标准，用于为\*\*AI 智能体\\（Agent\\）\*\* 建立一个\*\*去信任的协调层\\（trustless coordination layer\\）\*\*。它在Google 提出的\*\*Agent-to-Agent\\（A2A\\）\*\* 协议基础上进行了扩展，引入了 **链上身份注册、信誉注册与验证注册机制**，从而使自主智能体能够在没有预先信任关系的情况下，跨组织安全、可验证地进行交互与协作。 

**身份注册表\\（Identity Registry\\）   
为每个智能体分配唯一、抗审查的 AgentID，并将其以太坊地址和域名映射到一个**AgentCard\*\*\\（JSON 文件\\），其中描述智能体的技能、能力与信任模型。 

\*\*信誉注册表\\（Reputation Registry\\）   
负责授权智能体之间的反馈；反馈数据本身保存在链下，从而允许灵活的信誉评分与见证系统。

**验证注册表\\（Validation Registry\\）   
用于记录与验证任务执行情况，可支持** 经济质押验证**\*\***（验证者抵押代币以获得经济激励）或\*\*加密验证\*\*\\（如可信执行环境 TEE 或零知识证明 zk-Proof\\）

**TEE\\(Trusted Execution Environment,可信执行环境\\)**是一种硬件级安全技术，用于确保计算在一个受保护的、不可篡改的环境中执行。它常见于 CPU 芯片中。在 ERC-8004 中的作用：TEE 用于实现\*\*高安全等级的验证模型\*\*\\（High-Stake Validation\\）。  
当一个 AI 智能体执行关键任务\\（如医疗诊断或金融操作\\）时，它可以：

1.在 TEE 内运行；

2.生成一份加密证明\\(attestation\\），证明任务在可信硬件中执行；

3.其他智能体或验证者通过该证明确认任务结果的真实性。 

**zk-Proof\\（零知识证明，Zero-Knowledge Proof\\）**是一种密码学方法，用来在不泄露原始数据内容的情况下，证明某个声明是真实的。在 ERC-8004 中的作用：用于实现加密验证模型\\（Cryptographic Validation\\）。例如：一个智能体在链下完成某个任务（比如模型推理），然后生成一个零知识证明，提交到链上；其他智能体或验证者无需重算整个任务，就能确认该任务确实被正确执行。就像比特币上用私钥签名公钥解密。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->






#ERC\\-8004

基于以太坊\\（Ethereum\\）的新标准，用于为\*\*AI 智能体\\（Agent\\）\*\* 建立一个\*\*去信任的协调层\\（trustless coordination layer\\）\*\*。它在Google 提出的\*\*Agent-to-Agent\\（A2A\\）\*\* 协议基础上进行了扩展，引入了 **链上身份注册、信誉注册与验证注册机制**，从而使自主智能体能够在没有预先信任关系的情况下，跨组织安全、可验证地进行交互与协作。 

**身份注册表\\（Identity Registry\\）   
为每个智能体分配唯一、抗审查的 AgentID，并将其以太坊地址和域名映射到一个**AgentCard\*\*\\（JSON 文件\\），其中描述智能体的技能、能力与信任模型。 

\*\*信誉注册表\\（Reputation Registry\\）   
负责授权智能体之间的反馈；反馈数据本身保存在链下，从而允许灵活的信誉评分与见证系统。

**验证注册表\\（Validation Registry\\）   
用于记录与验证任务执行情况，可支持** 经济质押验证**\*\***（验证者抵押代币以获得经济激励）或\*\*加密验证\*\*\\（如可信执行环境 TEE 或零知识证明 zk-Proof\\）

**TEE\\(Trusted Execution Environment,可信执行环境\\)**是一种硬件级安全技术，用于确保计算在一个受保护的、不可篡改的环境中执行。它常见于 CPU 芯片中。在 ERC-8004 中的作用：TEE 用于实现\*\*高安全等级的验证模型\*\*\\（High-Stake Validation\\）。  
当一个 AI 智能体执行关键任务\\（如医疗诊断或金融操作\\）时，它可以：

1.在 TEE 内运行；

2.生成一份加密证明\\(attestation\\），证明任务在可信硬件中执行；

3.其他智能体或验证者通过该证明确认任务结果的真实性。 

**zk-Proof\\（零知识证明，Zero-Knowledge Proof\\）**是一种密码学方法，用来在不泄露原始数据内容的情况下，证明某个声明是真实的。在 ERC-8004 中的作用：用于实现加密验证模型\\（Cryptographic Validation\\）。例如：一个智能体在链下完成某个任务（比如模型推理），然后生成一个零知识证明，提交到链上；其他智能体或验证者无需重算整个任务，就能确认该任务确实被正确执行。就像比特币上用私钥签名公钥解密。

**#A2A 协议**

**A2A\\（Agent-to-Agent Protocol\\）** 是一个开放标准，用于让不同来源、不同框架的 AI 智能体可以彼此发现、通信、协作与执行任务。

  
\*\*A2A = 智能体之间的\\“HTTP 标准 + JSON-RPC 通信协议\\”\*\*

##A2A 协议的核心组成

| 模块 | 功能说明 |
| Agent Card（智能体卡片） | JSON 文件，描述智能体的能力、接口、安全机制等（相当于“数字名片”）。 |
| Discovery（发现机制） | 通过访问 https://{agent_domain}/.well-known/agent-card 来发现 Agent。 |
| Authentication（身份认证） | 采用 OpenID Connect 或 JWT 令牌机制。 |
| sendMessage / sendMessageStream | 标准 API，用于发送任务或流式请求（支持异步任务与长连接）。 |
| Artifacts（产物） | 任务执行后生成的结果对象，如文档、图片、数据流等。 |
| Context ID | 用于维持多轮对话或任务上下文的标识符。 |
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->







**#A2A 协议**

**A2A\\（Agent-to-Agent Protocol\\）** 是一个开放标准，用于让不同来源、不同框架的 AI 智能体可以彼此发现、通信、协作与执行任务。

  
\*\*A2A = 智能体之间的\\“HTTP 标准 + JSON-RPC 通信协议\\”\*\*

##A2A 协议的核心组成

| 模块 | 功能说明 |
| Agent Card（智能体卡片） | JSON 文件，描述智能体的能力、接口、安全机制等（相当于“数字名片”）。 |
| Discovery（发现机制） | 通过访问 https://{agent_domain}/.well-known/agent-card 来发现 Agent。 |
| Authentication（身份认证） | 采用 OpenID Connect 或 JWT 令牌机制。 |
| sendMessage / sendMessageStream | 标准 API，用于发送任务或流式请求（支持异步任务与长连接）。 |
| Artifacts（产物） | 任务执行后生成的结果对象，如文档、图片、数据流等。 |
| Context ID | 用于维持多轮对话或任务上下文的标识符。 |
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->








#ERC\\-8004

基于以太坊\\（Ethereum\\）的新标准，用于为\*\*AI 智能体\\（Agent\\）\*\* 建立一个\*\*去信任的协调层\\（trustless coordination layer\\）\*\*。它在Google 提出的\*\*Agent-to-Agent\\（A2A\\）\*\* 协议基础上进行了扩展，引入了 **链上身份注册、信誉注册与验证注册机制**，从而使自主智能体能够在没有预先信任关系的情况下，跨组织安全、可验证地进行交互与协作。 

**身份注册表\\（Identity Registry\\）   
为每个智能体分配唯一、抗审查的 AgentID，并将其以太坊地址和域名映射到一个**AgentCard\*\*\\（JSON 文件\\），其中描述智能体的技能、能力与信任模型。 

\*\*信誉注册表\\（Reputation Registry\\）   
负责授权智能体之间的反馈；反馈数据本身保存在链下，从而允许灵活的信誉评分与见证系统。

**验证注册表\\（Validation Registry\\）   
用于记录与验证任务执行情况，可支持** 经济质押验证**\*\***（验证者抵押代币以获得经济激励）或\*\*加密验证\*\*\\（如可信执行环境 TEE 或零知识证明 zk-Proof\\）

**TEE\\(Trusted Execution Environment,可信执行环境\\)**是一种硬件级安全技术，用于确保计算在一个受保护的、不可篡改的环境中执行。它常见于 CPU 芯片中。在 ERC-8004 中的作用：TEE 用于实现\*\*高安全等级的验证模型\*\*\\（High-Stake Validation\\）。  
当一个 AI 智能体执行关键任务\\（如医疗诊断或金融操作\\）时，它可以：

1.在 TEE 内运行；

2.生成一份加密证明\\(attestation\\），证明任务在可信硬件中执行；

3.其他智能体或验证者通过该证明确认任务结果的真实性。 

**zk-Proof\\（零知识证明，Zero-Knowledge Proof\\）**是一种密码学方法，用来在不泄露原始数据内容的情况下，证明某个声明是真实的。在 ERC-8004 中的作用：用于实现加密验证模型\\（Cryptographic Validation\\）。例如：一个智能体在链下完成某个任务（比如模型推理），然后生成一个零知识证明，提交到链上；其他智能体或验证者无需重算整个任务，就能确认该任务确实被正确执行。就像比特币上用私钥签名公钥解密。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
