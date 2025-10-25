---
timezone: UTC+8
---

# Leo

**GitHub ID:** leopc999

**Telegram:** @elegant_5T

## Self-introduction

A web3 enthusiast in AI.

## Notes
<!-- Content_START -->
# 2025-10-25
<!-- DAILY_CHECKIN_2025-10-25_START -->
复习之前的学习内容
<!-- DAILY_CHECKIN_2025-10-25_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->

参加了 Workshop。

# Unibase 核心技术讲解

1\. **定位与愿景** - Unibase 是专为自主 AI 代理设计的高性能去中心化 AI 记忆层，核心目标是让任何人都能拥有“链上永久 AI 代理”。 - 这类 AI 代理需具备三大支柱：去中心化身份、自主交易钱包、永久记忆，三者共同构成“主权 AI”，可跨平台独立运行。

2\. **解决的行业痛点** - 缺乏持久记忆：当前多数 AI 代理是“无状态”的，无法记住过往交互，功能受限（类似“助理每天都忘记前一天的对话”）。 - 跨平台互操作性差：不同平台的 AI 代理孤立存在，形成数据孤岛，无法相互协作。 - 数据治理去中心化不足：用户数据分散在各平台，用户无法真正掌控自身数据。

3\. **技术架构与核心组件** - 三大核心组件： 1. Membase：以 RD 为核心的 AI 记忆层，存储代理的记忆与交互经验。 2. AIP 协议：AI 代理协作协议，支持不同平台的代理发现、交互。 3. Unibase DA 网络：高性能数据存储与可用性网络，保障数据安全存储与快速访问。

\- 四层架构： 1. 底层：DA 存储网络（基础支撑，保障数据可用性）。 2. 中间层：去中心化 AI 记忆层（含代理身份、指令、知识检索、智能模型四大模块）。 3. 适配层：支持 AI 16Z Virtuals、Bit Agent 等主流代理框架，降低开发者集成难度。 4. 应用层：覆盖 AI 助手、交易机器人等场景，支持代理部署、资产代币化、交易、跨代理通信四大功能。

# Unibase 与 ERC 8004 的整合逻辑

1\. **互补关系** - ERC 8004：定义区块链上 AI 代理的“身份、信誉、验证体系”，解决“谁是可信代理”的问题（即“Who”和“信任”层面）。 - Unibase：提供“数据基础设施与智能核心”，解决代理“知道什么”“如何学习”的问题（即“内容存储”和“能力进化”层面），二者结合可构建“可信、自主、持续学习”的AI代理生态。

2\. **Unibase 对 ERC 8004 的能力扩展** - 代理发现：通过向量嵌入实现语义搜索，用户可通过自然语言找到目标代理（而非仅浏览目录）。 - 任务执行与上下文管理：DA 层作为“工作内存”和代理执行容器，支持复杂多步骤任务。 - 长期自主进化：持久化存储代理的所有数据与交互日志，让 ERC 8004 代理从“简单身份载体”升级为“智能学习系统”。

# 三组现场演示

1\. **演示一：部署 ERC 8004 合规代理（基于 Bit Agent 平台）** - 操作流程：连接钱包（确认代理所有者身份）→上传代理头像（视觉身份）→填写代理信息（名称、代号、功能介绍）→点击“启动”→系统自动部署 ERC 8004 合约并初始化 Unibase 记忆模块（耗时仅数秒）。 - 代理功能页：包含“交易”（查看代理代币经济、买卖代币）和“聊天”（与代理交互、测试记忆功能）两个核心板块。

2\. **演示二：Unibase 记忆层的实际作用** - 交互记录：与已部署的代理聊天（如询问“BNB 相关信息”），所有提问与回答都会被 Unibase 的 Membase 捕获并存储为“语义记忆”（非简单日志）。 - 记忆层透明度：通过 Unibase 浏览器可查看代理的所有记忆条目，包含记忆 ID、文件哈希（用于验证完整性）、存储位置、创建时间，点击条目还能查看 JSON 格式的原始数据（含对话 ID、引用链接、时间戳，确保上下文可追溯）。

3\. **演示三：AI 数字孪生平台 Twinx** - 核心功能：连接用户 Twitter 账号，读取推文数据（分析用户写作风格、兴趣、知识领域），生成“数字孪生代理”，该代理可模仿用户的语言习惯与认知逻辑。 - 实际案例：平台已上线多位加密领域 KOL 的数字孪生（如币安 CZ、以太坊 Vitalik、OpenAI 山姆·奥特曼等），用户可 24 小时与这些“孪生代理”交互（如询问“区块链技术趋势”），代理会基于存储的 KOL 公开数据生成回答，并标注引用来源（如具体推文链接）。 - 扩展能力：数字孪生代理可链上部署，支持代币化，还能进入代理市场交易。

# 资源与后续活动

1\. **开发资源** - 开源与文档：所有演示代码、案例均开源，Unibase 官网提供完整技术文档。 - 工具支持：提供多语言 SDK 及快速示例（如 AIP 协议代码，可直接实现跨平台代理交互），降低开发者集成门槛。
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->


阅读了 Medium 文章 **“The Story Behind ERC-8004 & Next Steps”** 的总结与个人理解：

* * *

## 一、背景 & 初衷

-   作者是 **Marco De Rossi**（MetaMask 的 AI 负责人）。他讲述了 ERC-8004 的诞生过程与愿景。
    
-   核心动机之一：在 AI / agent 生态中，已有许多项目自建协议 / schema 用于 agent 发现、通信、信任，但这些各自为政，不互通。如何让大家“说同一种语言”是个协调问题。
    
-   虽然 Google 将其 A2A（Agent2Agent）协议贡献给 Linux Foundation，作为中立标准，但在 Web3 / 信任最小假设场景下，A2A 本身忽略了 agent 发现和信任建立机制（即假设已有信任或组织内部使用）。作者意识到要扩展 A2A，使其适应无信任环境。
    
-   补充一点：标准设计者努力**不重复造轮子**。例如，在信任 / 验证模型方面，优先借鉴现有的模式（如 TEE attestation, staking / re-execution 验证、EigenLayer 等）。而在设计上保持“极简 / 模块化 / 插拔式”是优先考量。
    

* * *

## 二、文章中强调的特点 / 原则 / 理念

以下是作者特别强调、在撰写 ERC-8004 过程中的一些设计原则与理念：

| 原则 /理念 | 说明 |
| --- | --- |
| 极简（minimal） | 不把所有信任逻辑都写在标准里。标准只提供 最基础的注册、信任信号 + 可见性。复杂的规则（信誉策略、验证经济机制、评分算法等）交给生态自由设计。 |
| 链上可见性 / 数据入口点 | 区块链被用作一个逻辑中枢，用于注册 agent、列出验证请求、发出事件，让所有参与者在这个“中枢”上能看到公共信息。其他数据可放链下由专门协议处理。 |
| 分层 / 可插拔信任模型 | Agent 可以支持多种信任机制（声誉 / 验证 / 硬件证明等），不同场景可选不同模型。标准不强制一种信任方式。 |
| 社区驱动 / 构建为先（building-first） | 作者强调，标准最终的生命力在于被采纳、被真正构建出来。因此，他们愿 prioritise 那些愿意基于标准去构建项目的反馈和更改请求。 |
| 中立 / 无偏向 | 标准设计不偏向特定信任 / 验证模型，也不包含支付机制，以保持开放性、避免垄断 / 预设假设。 |

* * *

## 三、ERC-8004 的社会 / 社区反响 & 采用动向

-   作者提到，ERC-8004 在社区里“**异常爆炸性传播**”——被转发、讨论、用多种语言解读，还出现 meme、哲学讨论等。说明市场 /社区对 Agent 生态 / 去中心化信任层有强烈需求。
    
-   在文中，第一天就有参考实现被提交。说明设计者希望快速从标准走向落地样例。
    
-   作者也呼吁社区参与：欢迎读者在 Ethereum Magicians 论坛提交变更建议、讨论“未来方向”，但强调要以实用构建为导向。
    

* * *

## 四、文章提出的 “下一步 / 未来方向” 要点

作者列出了一些可能的未来方向 / 待解决的问题，以下是要点整理：

1.  **标准变更 / 反馈优先级由构建者驱动**  
    对于愿意基于标准构建项目的团队，其反馈 / 变更请求会被优先考虑。
    
2.  **继续保持标准的极简 & 模块化**  
    虽然未来可能增加功能（例如链上可组合性、复杂聚合、交叉链支持等），但核心设计仍要避免臃肿。
    
3.  **可视化 / 探索器 / agent 市场建设**  
    要让“发现 agent / 比较 agent / 选择 agent”这一用户体验流畅，需要社区搭建 agent 浏览器 / 市场 / 索引器工具。标准只提供基础数据与事件。
    
4.  **信任 / 评价 / 验证协议生态发展**  
    要有多个不同风格 / 模型的信誉 / 验证协议出现（staking 重运行、硬件证明、零知识证明、审计者网络等），构成一个丰富的生态。
    
5.  **跨链 / 跨网络 / 互操作**  
    Agent 不应被锁在单链 / 单网络。未来可能考虑多链注册 / 跨链信任机制。
    
6.  **与通信 / 合同 / 支付协议对接**  
    标准本身不包含支付 / 托管 / 合约执行逻辑，但需要与这些层（如 MCP / Agent 通信协议 / 支付协议）良好集成。
    

* * *

## 五、个人理解 & 展望建议

-   文章强化了 ERC-8004 不只是一个技术标准，更是 **理念驱动 / 社区协调** 的产物。作者把它看作对抗大型 AI 平台的基础设施工具，是基于去中心化 AI 理想的行动之一。
    
-   在落地阶段，一个挑战是：虽然标准极简，生态协议众多（评价系统、验证协议、市场、索引器等）必须形成协同。若生态支撑不足，再优秀的标准也难以广泛应用。
    
-   社区建设非常关键。标准必须得到早期项目 / 骨干团队采纳，才能验证可用性、调整缺陷、形成样板。
    
-   在未来版本或演进方向里，建议关注以下几个角度：
    
    1.  **链上可组合性增强**：尽管作者强调节省 gas，但若未来能支持某些自动化合约（例如“只有验证通过后才释放付款”）的可组合性，会极大提升实用性。
        
    2.  **跨链 / 跨域信任桥接**：随着 AI agent 生态在多个链 / 网络中发展，信任数据能否跨链访问 / 引用将是关键。
        
    3.  **隐私 / 合约可验证性保护**：Agent 的注册文件 / 反馈 / 验证报告有可能包含敏感信息，如何在保证可验证性的同时保护隐私，是协议中需要更多考虑的方向。
        
    4.  **渐进升级策略 / 兼容性**：未来如果要加入“更重 / 链上”特性（例如链上聚合评分 / 复杂验证状态机 / 支付集成等），如何在不破坏已有基础设施的前提下升级，是标准设计要考虑的向后兼容问题。
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->



今天继续复习之前的内容，体会其中的机制。
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->




# x402 本地测试

**目标**：在本地暴露一个付费保护的 endpoint（Seller），用 Buyer 触发 **402 → 完成支付 → 返回真实响应**，并在服务端看到成功日志（`402 → success logs`）。

* * *

## 快速步骤

1.  安装依赖
    

```bash
npm install x402-express x402-fetch @coinbase/cdp-sdk dotenv
```

2.  Seller（简化 Express）
    

```js
// server.js
import express from "express";
import { paymentMiddleware } from "x402-express";

const app = express();
app.use(paymentMiddleware("0xReceiverAddr", {
  "GET /weather": { price: "$0.001", network: "base-sepolia" }
}, { url: "https://x402.org/facilitator" }));

app.get("/weather", (req,res) => {
  console.log("payment verified — serving resource");
  res.json({ weather: "sunny", temp: 70 });
});
app.listen(4021, ()=>console.log("http://localhost:4021"));
```

3.  启动服务并验证初次响应（应返回 402）：
    

```bash
node server.js
curl -i http://localhost:4021/weather   # expect HTTP/1.1 402 Payment Required
```

4.  Buyer（自动付费并重试）
    

```js
// buyer.js
import { wrapFetchWithPayment } from "x402-fetch";
import { CdpClient } from "@coinbase/cdp-sdk";

const cdp = new CdpClient();
const acct = await cdp.evm.createAccount();
const fetchWithPayment = wrapFetchWithPayment(fetch, acct);
const res = await fetchWithPayment("http://localhost:4021/weather");
console.log(await res.json()); // paid response
```

5.  Check-in 期待结果：
    

-   第一次 `curl` 返回 **402**（payment instructions）。
    
-   运行 Buyer 脚本后，服务端日志显示 `payment verified — serving resource`，Buyer 收到真实 JSON 响应（完成：**402 → success logs**）。
    

* * *

## 快速故障排查

-   若 `curl` 返回 200：确认中间件挂载位置与路由路径一致。
    
-   Buyer 无法付费：确认 wallet/account 可签名并有测试资产，或使用 CDP Server Wallet。
    
-   Facilitator 验证失败：检查中间件 facilitator URL（测试环境使用 `https://x402.org/facilitator`）。
    

* * *

## Checklist（最小）

-   安装依赖
    
-   启动 seller，curl 得到 402
    
-   运行 buyer，拿到真实响应并在 server 看到成功日志
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->





# **A2A → AP2** 协议内容学习

> 阅读了 A2A 官方文档（[https://a2a-protocol.org/](https://a2a-protocol.org/)）、Google AP2 发布博客（[https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol)）、Cloud Security Alliance 对 AP2 的安全分析（[https://cloudsecurityalliance.org/blog/2025/10/06/secure-use-of-the-agent-payments-protocol-ap2-a-framework-for-trustworthy-ai-driven-transactions](https://cloudsecurityalliance.org/blog/2025/10/06/secure-use-of-the-agent-payments-protocol-ap2-a-framework-for-trustworthy-ai-driven-transactions)）。进行如下总结。

* * *

## 一、概览

-   **A2A**（Agent2Agent）是用于不同 AI agent 之间互通、发现、协调与任务委派的通信 / 协作规范；**AP2**（Agent Payments Protocol）是对 A2A 的支付扩展，专注于让 agent 安全、可审计、可互操作地发起与接受付款（包括人与 agent、agent-to-agent 的交易），并使用可验证凭证（VC / Mandates）与现有支付生态（卡、银行、稳定币、钱包）对接来建立“agentic commerce”信任链。
    

* * *

## 二、A2A 的关键能力

-   **互操作的 agent 通信层**：标准消息格式、Agent Card、技能/能力描述、API / endpoint 描述，便于跨平台 agent 协作与委派。
    
-   **发现与能力协商**：Agent 能被发现并通过其声明（Agent Card / metadata）被选用。
    
-   **安全与隔离**：支持在不暴露内部记忆或私有工具的情况下交换任务信息（隐私 / 隔离设计）。
    
-   **与 MCP 等协议协同**：A2A 与 MCP（Model Context Protocol）互补，后者负责 agent ↔ tool 的交互，A2A 负责 agent ↔ agent 间的通信。
    

* * *

## 三、AP2 的关键能力

-   **Mandates（意向 / 授权凭证）— 基于可验证凭证（VC）**：AP2 引入签名的 Mandates（VC 形式）来表达用户对 agent 的支付授权与意图（scope、TTL、限额、风控参数等），使授权具有**不可否认性**与机器可验证性。
    
-   **角色化交易流**：定义 human-present 与 human-not-present 两类交易/交互模式，并区分 agent、merchant、payment provider、credential provider 等角色与接口。
    
-   **可插拔支付后端**：AP2 设计为可与传统支付网关、卡网络、银行 rails 以及链上 stablecoin/crypto rails（如 x402）整合，允许 agent 在多种 rails 上发起或接收款项。
    
-   **身份与证明链**：强调硬件/软件密钥证明（硬件 key attestation / TPM / Android key attestation）、数字签名与 DIDs/VCs，以防止伪造/代签问题。
    
-   **参考实现与生态支持**：已有行业参与者（支付厂商、钱包、云厂商等）与参考 SDK / 示例，实现互操作性与落地。
    

* * *

## 四、**A2A → AP2** 能力对照映射表

| A2A 能力（什么） | AP2 对应/新增能力（怎么扩展/补强） | 说明 / 设计意图 |
| --- | --- | --- |
| Agent Discovery / Agent Card（能力声明） | Credential-aware Agent Cards / Mandate hooks | Agent Card 扩展包含支付相关的 capability 字段（可接受哪类支付、所需 credential types、supported trust 等），让支付方能在选择 agent 时考虑支付合规/风控。 |
| Task delegation & result exchange | Payment lifecycle integrated into task flow | 在 task lifecycle 中嵌入 payment intent → mandate issuance → payment execution → receipt/validation 的步骤（即把付款当成 task 的一个子流程）。 |
| Secure, opaque tool access (隐私/隔离) | Non-repudiable mandates + attested keys | 为了在不暴露用户凭据的情况下授予 agent 支付权，AP2 使用签名 Mandates 与硬件/attestation 证书来绑定 agent 的执行环境。 |
| Protocol messages / events | Payment events, disputes, TTLs, intents | AP2 在消息模型中加入 payment-specific events（intent_created, mandate_signed, payment_requested, payment_executed, dispute_requested）以支持审计与纠纷处理。 |
| Integration with MCP for tools | MCP + AP2 choreography | MCP 提供数据/工具上下文（比如商家 API 访问），AP2 在 MCP 的上下文里注入支付授权与结算步骤；二者合作实现端到端 agentic commerce。 |
| Agent authentication (基本签名) | VCs / DIDs + hardware attestation + SCA alignment | AP2 要求更强的身份 binding（例如 verifiable credentials、DID、以及硬件密钥 attestation），并在需要时结合 Strong Customer Authentication（SCA）流程。 |
| Asynchronous / streaming tasks | Asynchronous payment reconciliation / streaming settlement support | AP2 设计考虑了 agent 的异步工作流，允许 later authorization、delayed settlement，及与 streaming/real-time settlement 后端的整合（例如 stablecoin rails）。 |

* * *

## 五、典型交易流程

1.  **发现 & 评估（A2A）**
    
    -   客户端发现 Agent，读取其 Agent Card（包含 AP2 支付能力字段）。
        
2.  **创建 Intent / Mandate 请求（AP2）**
    
    -   Agent 向用户或用户代理请求签发 Mandate（包含 scope、限额、TTL、可用支付方式）。Mandate 以 VC 签名形式颁发。
        
3.  **授权 & 验证**
    
    -   Mandate 签发后，可由 credential provider / attestor 验证（硬件 key attestation、DID、签名检验）。必要时触发 SCA。
        
4.  **发起支付 / 路由**
    
    -   Agent 用 Mandate 向支付提供者（card gateway / PSP / stablecoin rail）提交付款请求，支付路由器选择最合适的 rails（传统或链上）。
        
5.  **执行 & 记录**
    
    -   完成支付并在 A2A/AP2 的事件流中记录 payment\_executed、收据与可证明的执行证据。必要时保留证据用于争议。
        
6.  **纠纷 / 撤销 / TTL 到期**
    
    -   AP2 规定 dispute 流程、Mandate TTL 以及撤销/回滚机制（human-present 通常更严格）。CSA 对这些环节提出了许多安全建议（见下节）。
        

* * *

## 六、安全与风险（CSA 的分析要点）

-   **Mandate spoofing / fake authorizations**：攻击者伪造或重放 Mandates → 需要硬件-backed keys、签名校验与去中心化 allowlists 来减轻风险。
    
-   **Agent coercion / credential theft**：agent 的凭证若被窃取，可被滥用；建议采用 TPM / key attestation、短 TTL、可撤销的凭证模型。
    
-   **Human-present vs Human-not-present 风险差异**：对高价值/敏感交易应强制 human-present（实时用户确认 / SCA）；自动化任务可在低风险限额内运行并附加审计链。
    
-   **Replay / front-running / domain squatting**：提交与注册流程需考虑 commit-reveal、nonce、时间窗等反滥用手段。
    
-   **合规与隐私**：AP2 要与现行支付合规（如 PSD2 SCA）与隐私法规对齐；实现需兼顾最小数据暴露与可审计。
    

* * *

## 七、实现与工程注意点（实践建议）

-   在 **Agent Card / A2A schema** 中加入 AP2 必需字段（supported\_payment\_types、mandate\_endpoint、min\_human\_threshold 等）。
    
-   Mandate/VC 的设计要支持 **短 TTL、独立撤销/查验接口（CRL 或 OCSP-like）**。
    
-   对接多个支付后端时，设计一层 **routing/orchestration**（选择最优 rails、回退策略、手续费与失败重试逻辑）。AP2 生态已有多家支付与钱包厂商表达支持。
    
-   为关键操作引入 **attestation & hardware-backed keys**（Android/iOS key attestation、TPM）并在 Agent Card 中指明受信任根或证书来源。
    
-   定义清晰的 **dispute & liability model**（谁对错误付款负责、如何退款、如何移送证据），并将其映射到 A2A 的事件与日志。
    

* * *

## 八、Key takeaways（要点速记）

-   **AP2 是 A2A 的支付扩展**：把“支付”变成 agent 协作流的一个原生步骤（intent → mandate → execute → audit）。
    
-   **安全是核心设计约束**：Mandate（VC）、hardware attestation、SCA 对齐是防护基石；CSA 提供了实用的风险缓解清单。
    
-   **可插拔支付后端与生态合作**：AP2 允许传统及链上 rails 共存，已获得支付厂商、钱包与云厂商多方支持（有助于早期落地）。
    
-   **实现需跨层工程协调**：需要在 A2A agent card、MCP tool access、支付网关、credential provider、以及合规策略间做端到端设计与测试。
    

* * *

## 九、参考 / 延伸阅读（原文）

-   A2A Protocol — Agent2Agent 官方文档（规范、Agent Card、示例 SDK）。([a2a-protocol.org](http://a2a-protocol.org))
    
-   Google Blog — Announcing Agent Payments Protocol (AP2)。([Google Cloud](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol))
    
-   Cloud Security Alliance — “Secure Use of the Agent Payments Protocol (AP2)”（安全分析、具体威胁与缓解建议，2025-10-06）。([cloudsecurityalliance.org](http://cloudsecurityalliance.org))
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->






今天阅读了 QuillAudits 文章《ERC-8004: Infrastructure for Autonomous AI Agents》。

* * *

## 一、QuillAudits 视角：ERC-8004 的定位与价值

### 1\. 从 A2A 协议到区块链信任层的演进

-   QuillAudits 提到，Google 的 Agent-to-Agent (A2A) 协议（Agent Cards, JSON-RPC 通信, 能力协商等）确实在组织内部发挥了作用，但它默认假设通信方之间已有信任关系。QuillAudits 认为，这在跨组织、链上 / 跨平台的 Agent 生态中无法成立。
    
-   ERC-8004 的提出，则正是为了填补 “Agent 通信协议 + 信任机制”之间的空白：让 Agent 之间在没有预先信任的情况下也能进行合作。
    
-   从 QuillAudits 的表述看，他们强调的是：ERC-8004 不是单纯的 token / 能力协议，而是“信任基础设施”（trust backbone / trust layer）。
    

### 2\. 轻量链上 + 重量链下 = 混合设计（Hybrid Architecture）

-   QuillAudits 特别指出 ERC-8004 在设计上的**轻量链上**取向：链上只存储关键的授权 / 索引 / 校验逻辑，而把大多数声誉数据 / 验证细节 / Agent Card / 反馈文件都放在链下（通过 URI 引用）
    
-   这种设计有两个好处：
    
    1.  **减少 gas 成本 / 链上负担**
        
    2.  **更灵活 / 可扩展**：链下系统可以随意使用复杂的评分算法或验证逻辑，而不被链上效率约束
        
-   在 QuillAudits 的解读里，Reputation Registry 本身不保存实际评分数据，而只负责“**反馈授权（feedback authorization）**”的链上记录。真实的声誉计算留给链下系统。
    
-   类似地，Validation Registry 是一个通用钩子（hook），允许对某个数据 / 任务请求发出验证请求 / 记录响应。它不限定验证协议细节，而允许多种验证机制共存（staking 重运行、TEE attestation、密码学证明等）。
    

### 3\. 分层信任模型（Tiered Trust Models）

QuillAudits 引入一个“信任分层”概念，强调对不同风险 / 任务价值要用不同信任级别：

| 风险 / 任务价值级别 | 建议信任机制 |
| --- | --- |
| 低风险 / 日常任务 | 基于 Reputation（评价 / 反馈） 即可 |
| 中风险 / 涉及价值 / 资金 | 加入 Crypto-Economic 验证机制：验证者需抵押 / 被惩罚以保证诚实性 |
| 高风险 / 关键任务 | 使用 可信执行环境 (TEE) 证明 / 硬件证明 / 加密证明，以提供更强的保证 |

这种方式强调：信任机制应该与任务价值成正比，不要总用最严苛的方法，也不要总用最宽松的方法。

* * *

## 二、QuillAudits 补充的风险 / 安全考量 & 攻击向量

QuillAudits 在文章末尾列了几个他们认为设计者必须特别注意 / 防范的攻击 / 安全风险点。整理如下，并适当补充我的理解。

| 风险 | 描述 | 缓解 / 对策 |
| --- | --- | --- |
| Domain 抢注 / 前置（Front-Running） | 在 AgentDomain 注册时，有人可能监测到交易池，然后抢在你之前注册同一个域名（domain squatting） | 使用 commit–reveal 机制 或隐藏提交（即先提交哈希、稍后公开）来防止抢注 |
| 反馈授权滥用 | 如果 AcceptFeedback(agentClient, agentServer) 没有权限检查，任何地址都能调用这个接口，生成假的 AuthFeedback 记录，污染反馈授权体系 | 在合约里加入权限校验，比如仅 msg.sender == serverAgentAddress 才能生成授权，确保只有被评价的 Agent 本身或其授权方可以发授权 |
| 存储膨胀 / DoS 攻击 | 如果 ValidationRequest 被大量调用，则请求记录会在链上长期占用存储（直到超时 /清除），可能导致未来 gas / 存储成本变高或恶意阻塞 | 设计超时清除（expire）机制、限制每个 AgentServerID 可挂起请求数、对提交请求收取保证金 / bond 并在完成后返还 |
| Sybil 身份滥用 | 恶意方可批量注册 Agent 身份（Domain + 地址）来操纵声誉系统 / 做协调攻击 | 要求注册时最低保证金 / 销毁 /锁定 / probation 期后返还；或者通过零知识证明 / 唯一性签名机制限制一个经济实体能控制的身份数量 |

QuillAudits 的这些补充是非常实用的“落地建议 /安全提醒”，很值得在真是部署实现时一一考虑。

* * *

## 三、QuillAudits 解读的新增视角总结

1.  **定位侧重点：信任基础设施，而非能力 / 通信协议**
    
    -   强调 ERC-8004 是为 Agent 生态提供信任层，构建信誉、验证机制基础。
        
    -   它与 A2A / 能力协议 / 任务调度协议并不冲突，而是互补。
        
2.  **链上 ↔ 链下 混合架构是关键设计权衡**
    
    -   链上尽可能简洁，只做授权 / 索引 / 事件记录
        
    -   链下承担复杂评分 / 反馈 / 验证细节
        
    -   这样能在保持透明 / 可组合性的基础上，提高效率、扩展性、灵活性。
        
3.  **信任模型按业务价值分层**
    
    -   不是所有任务都要求最高级验证机制
        
    -   低风险任务只依赖评价，重要任务依赖 staking / 硬件证明
        
    -   这种分层信任设计让系统更实用、成本更可控
        
4.  **现实风险 / 攻击场景不可忽略**
    
    -   抢注、授权滥用、存储 bloat、Sybil 等都是现实攻击路径
        
    -   在实现时，不仅要遵照 ERC-8004 的接口规范，也要在合约层、经济机制层做防护设计
        
5.  **实现示例 / 伪代码**
    
    -   文章里给出了 Identity Registry / Reputation Registry / Validation Registry 的伪代码示例（简化版）
        
    -   特别在 Reputation Registry 部分，只做 `AcceptFeedback`，而不直接存评分数据，是一种“授权记录 + 反馈在链下”的轻量化方案
        
    -   在 Validation Registry 中，用 mapping 存 request，再在验证回应时做清除、emit event 等。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->







# 构建无信任代理（Trustless Agents）：ERC-8004 Workshop

本次会议围绕“无信任代理（Trustless Agents）”相关的 ERC-8004 标准展开，涵盖标准背景、核心功能、技术实现及后续规划，我参会后，对核心内容进行了总结。

## 一、ERC-8004 标准核心价值与背景

1\. **解决的核心问题**：随着 AI 在经济活动中（如供需匹配、信息交互）的作用增强，需建立类似“物理世界”的去中心化系统——让 AI 代理能自主发现、交互，避免依赖中心化中介（如应用商店）。

2\. **标准定位**：通过区块链智能合约构建“中性信息基础设施”，为 AI 代理提供身份、声誉、验证三大核心能力，支撑开放的“代理经济”。

## 二、ERC-8004 三大核心结构

### 1\. 身份注册表（Identity Registry）

\- **功能**：为 AI 代理提供“全球通讯录”，支持代理注册、信息展示与发现。

\- **技术实现**：基于 NFT（ERC-721）标准，注册时需提供指向链下 JSON 文件的 URI（含代理名称、技能、通信端点等信息），生成唯一“代理 ID”（即 NFT 的 Token ID）。

\- **灵活操作**：支持代理转移、指定“操作员”（代维护代理信息），且兼容现有 NFT 生态（如市场、浏览器可直接展示代理信息）。

### 2\. 声誉注册表（Reputation Registry）

\- **功能**：收集用户对代理的反馈，形成可验证的声誉数据。

\- **反馈规则**：用户无需注册即可提交反馈，但需提供代理签署的“反馈授权凭证”（避免未交互就评分的垃圾反馈）；反馈含“0 - 100 分”、可选标签及链下详细信息链接。

\- **数据使用**：可在链上直接查询代理声誉（如筛选特定用户、特定标签的评分），也支持基于此构建上层应用（如游戏中代理组队信任判断）。

### 3\. 验证注册表（Validation Registry）

\- **功能**：为代理的“工作成果”提供验证通道，适用于需证明真实性的场景（如 AI 任务执行结果）。

\- **操作流程**：代理完成任务后，向指定智能合约提交“验证请求”（含任务数据链接，支持 IPFS 或中心化存储）；仅指定的“验证者”可提交“验证响应”（0 - 100分，支持“失败/通过”二元判断）。

\- **兼容方案**：支持零知识证明（zkML）、质押安全推理（Stake Secure Inference）、可信执行环境（TEE）等多种验证技术，兼顾隐私与公开验证需求。

### 四、技术落地与使用细节

1\. **当前进展**：已发布参考实现代码（开源），并部署至 Sepolia 测试网；提供 SDK（社区也在开发适配工具），支持通过 Hardhat 本地运行测试（`npm run local` 启动节点 `npm test` 运行测试用例）。

2\. **用户体验优化**：支持 EIP-1271 标准，可实现“无 Gas 费交互”（智能合约钱包签名），降低开发者使用门槛。

### 五、关键规划与问题解答

1\. 主网部署与治理

\- **时间线**：最坏情况 10 月底部署以太坊主网，具体取决于社区反馈；

\- **治理机制**：采用多签钱包（Multisig）分布式治理，以太坊基金会协调部署，避免单一主体控制；初期保留合约升级灵活性，后续可能转为不可变合约。

2\. 常见问题回应

\- **数据隐私**：验证数据隐私性取决于技术方案——zkML 可隐藏私有输入，质押安全推理需公开数据，TEE 可通过加密实现隐私；

\- **恶意评分过滤**：支持通过规则筛选恶意反馈，但暂无法实现“完全防攻击”，需依赖上层应用优化；

\- **链上/链下数据**：核心信息（如代理 ID、评分）链上存储，详细信息（如任务描述）链下存储（IPFS 为主）；计划通过 The Graph等工具实现多链数据索引。

### 六、后续行动

\- 社区持续收集反馈，优化标准与实现；

\- 近期将召开会议讨论“链上 TEE 验证数据标准化”，欢迎开发者参与；

\- 建议开发者加入社区（已超 750 人），获取最新 SDK 与部署动态。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->








\# ERC-8004 学习笔记：Trustless Agents 标准

\> 标准链接：[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

\> 目标：为 **去中心化 Agent（含 AI agents）** 提供\*\*信任基础设施\*\*，实现 **身份注册 + 声誉反馈 + 结果验证**。

\---

\## ✨ 一、为什么需要 ERC-8004？

在去中心化 Agent 生态中，Agent 之间要协作或交易，但存在三个核心问题：

| 问题 | 描述 | 需要的能力 |

|------|------|------------|

| 我如何找到一个 Agent？ | 缺乏全局标准身份 | **身份注册** |

| 我能信任它吗？ | 无法评估质量可靠性 | **声誉系统** |

| 它给的结果是真的吗？ | 结果可能被操控或出错 | **结果验证机制** |

✅ ERC-8004 提出解决方案：三个链上注册表（Registry）构成的\*\*可组合信任层\*\*。

\---

\## 🧱 二、核心组成（3 大 Registry）

\### 1. **Identity Registry（身份注册表）**

为每个 Agent 分配一个链上身份`agentId`（基于 ERC-721）

| 功能 | 说明 |

|------|------|

| 注册 Agent | 每个 Agent 拥有唯一 ID |

| 关联元数据 | tokenURI 指向 Agent JSON 描述文件 |

| 支持扩展 | 可存额外 metadata |

✅ 解决的问题：\*Agent 可发现、可识别、有公开接口描述\*

\---

\### 2. **Reputation Registry（声誉反馈注册表）**

记录用户/客户端对 Agent 的服务评分与反馈

| 支持的内容 | 说明 |

|------------|------|

| 评分（0–100） | 质量分 |

| 标签（tag1, tag2） | 用于分类或评价维度 |

| feedback URI + hash | 指向详细反馈的链下文件 |

| 撤销反馈 | 支持撤回 |

| 反馈可回应 | Agent 可回应用户评论 |

✅ 解决的问题：\*让 Agent 有“链上信用历史”\*

\---

\### 3. **Validation Registry（验证注册表）**

允许验证者对 Agent 的执行结果进行验证登记（验证可信性）

| 功能 | 描述 |

|------|------|

| 提交验证请求 | Agent 或用户提交验证任务 |

| 验证者回应 | 给出 response 分数 + URI 证明 |

| 多次验证 | 支持软/硬最终性验证 |

| 可过滤统计 | 按 agent / validator / tag 查询验证情况 |

✅ 解决的问题：\*结果可验证，信任不是嘴上说说\*

\---

\## 🔧 三、支持的信任模型（可组合）

Agent 可声明支持哪些信任方式：

\- ✅ Reputation Trust（声誉信任）

\- ✅ Crypto-economic Trust（质押+验证）

\- ✅ Hardware Attestation（TEE）

\- ✅ zkML / Proof-based Trust

\- ✅ 甚至未来扩展其他模型

📌 这些在 Agent 注册文件 `tokenURI JSON`) 中的 `supportedTrust` 字段声明。

\---

\## 🔄 四、工作流程示意

\`\`\`mermaid

sequenceDiagram

participant U as 用户

participant IR as Identity Registry

participant RR as Reputation

participant VR as Validation

participant A as Agent

A->>IR: 注册 agentId

U->>A: 调用任务

U->>RR: 提交评分/反馈

U->>VR: (可选) 请求验证

VR->>U: 返回验证记录


# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->
\# ERC-8004 学习笔记：Trustless Agents 标准

\> 标准链接：[https://eips.ethereum.org/EIPS/eip-8004](https://eips.ethereum.org/EIPS/eip-8004)

\> 目标：为 **去中心化 Agent（含 AI agents）** 提供\*\*信任基础设施\*\*，实现 **身份注册 + 声誉反馈 + 结果验证**。

\---

\## ✨ 一、为什么需要 ERC-8004？

在去中心化 Agent 生态中，Agent 之间要协作或交易，但存在三个核心问题：

| 问题 | 描述 | 需要的能力 |

|------|------|------------|

| 我如何找到一个 Agent？ | 缺乏全局标准身份 | **身份注册** |

| 我能信任它吗？ | 无法评估质量可靠性 | **声誉系统** |

| 它给的结果是真的吗？ | 结果可能被操控或出错 | **结果验证机制** |

✅ ERC-8004 提出解决方案：三个链上注册表（Registry）构成的\*\*可组合信任层\*\*。

\---

\## 🧱 二、核心组成（3 大 Registry）

\### 1. **Identity Registry（身份注册表）**

为每个 Agent 分配一个链上身份`agentId`（基于 ERC-721）

| 功能 | 说明 |

|------|------|

| 注册 Agent | 每个 Agent 拥有唯一 ID |

| 关联元数据 | tokenURI 指向 Agent JSON 描述文件 |

| 支持扩展 | 可存额外 metadata |

✅ 解决的问题：\*Agent 可发现、可识别、有公开接口描述\*

\---

\### 2. **Reputation Registry（声誉反馈注册表）**

记录用户/客户端对 Agent 的服务评分与反馈

| 支持的内容 | 说明 |

|------------|------|

| 评分（0–100） | 质量分 |

| 标签（tag1, tag2） | 用于分类或评价维度 |

| feedback URI + hash | 指向详细反馈的链下文件 |

| 撤销反馈 | 支持撤回 |

| 反馈可回应 | Agent 可回应用户评论 |

✅ 解决的问题：\*让 Agent 有“链上信用历史”\*

\---

\### 3. **Validation Registry（验证注册表）**

允许验证者对 Agent 的执行结果进行验证登记（验证可信性）

| 功能 | 描述 |

|------|------|

| 提交验证请求 | Agent 或用户提交验证任务 |

| 验证者回应 | 给出 response 分数 + URI 证明 |

| 多次验证 | 支持软/硬最终性验证 |

| 可过滤统计 | 按 agent / validator / tag 查询验证情况 |

✅ 解决的问题：\*结果可验证，信任不是嘴上说说\*

\---

\## 🔧 三、支持的信任模型（可组合）

Agent 可声明支持哪些信任方式：

\- ✅ Reputation Trust（声誉信任）

\- ✅ Crypto-economic Trust（质押+验证）

\- ✅ Hardware Attestation（TEE）

\- ✅ zkML / Proof-based Trust

\- ✅ 甚至未来扩展其他模型

📌 这些在 Agent 注册文件 `tokenURI JSON`) 中的 `supportedTrust` 字段声明。

\---

\## 🔄 四、工作流程示意

\`\`\`mermaid

sequenceDiagram

participant U as 用户

participant IR as Identity Registry

participant RR as Reputation

participant VR as Validation

participant A as Agent

A->>IR: 注册 agentId

U->>A: 调用任务

U->>RR: 提交评分/反馈

U->>VR: (可选) 请求验证

VR->>U: 返回验证记录

## 五、优点

| 优点 | 描述 |
| --- | --- |
| 模块化 | 身份/声誉/验证分层设计 |
| 可组合 | 任意协议可基于它扩展 |
| 链上可信 | 数据可审计、可追溯 |
| 去中心化 Agent 基础设施 | 与 MCP、A2A 互补 |

## 六、风险与挑战

| 风险 | 说明 |
| --- | --- |
| Sybil 攻击 | 恶意刷声誉 |
| 验证经济未定义 | Slashing/Staking 需外部标准补充 |
| 结果依赖链下 URI | 需要可靠存储如 IPFS |
| 数据量扩展 | 声誉写入可能昂贵 |

## 七、小结

-   ERC-8004 是 **Agent 信任层基础设施**。
    
-   通过三个 Registry 建立 **身份 + 声誉 + 验证**。
    
-   使 **链上 Agent 市场 & AI Agent Economy 成为可能**。
    
-   与通信协议（如 MCP/A2A）互补，而非竞争。
    
-   下一步生态重点将围绕：  
    ✅ 信任模型扩展  
    ✅ 验证协议  
    ✅ Agent Marketplace 搭建
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
## 五、优点

| 优点 | 描述 |
| --- | --- |
| 模块化 | 身份/声誉/验证分层设计 |
| 可组合 | 任意协议可基于它扩展 |
| 链上可信 | 数据可审计、可追溯 |
| 去中心化 Agent 基础设施 | 与 MCP、A2A 互补 |

## 六、风险与挑战

| 风险 | 说明 |
| --- | --- |
| Sybil 攻击 | 恶意刷声誉 |
| 验证经济未定义 | Slashing/Staking 需外部标准补充 |
| 结果依赖链下 URI | 需要可靠存储如 IPFS |
| 数据量扩展 | 声誉写入可能昂贵 |

## 七、小结

-   ERC-8004 是 **Agent 信任层基础设施**。
    
-   通过三个 Registry 建立 **身份 + 声誉 + 验证**。
    
-   使 **链上 Agent 市场 & AI Agent Economy 成为可能**。
    
-   与通信协议（如 MCP/A2A）互补，而非竞争。
    
-   下一步生态重点将围绕：  
    ✅ 信任模型扩展  
    ✅ 验证协议  
    ✅ Agent Marketplace 搭建
<!-- DAILY_CHECKIN_2025-10-15_END -->



<!-- Content_END -->
