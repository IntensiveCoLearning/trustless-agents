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
# 2025.10.15
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
