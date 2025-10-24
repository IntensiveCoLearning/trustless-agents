---
timezone: UTC+12
---

# Neo Sun

**GitHub ID:** sunhuachuang

**Telegram:** @sunhuachuang

## Self-introduction

An idealist, programmer, cryptographer. Hacking for Freedom!

## Notes
<!-- Content_START -->
# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->
今天开始调试将x402的 payment service 通过 8004 注册到 onchain 中。

首先完成注册：

Agent: 303

IPFS : ipfs://bafkreibecca2m7txyqcrwssij6ccnbv7p26eiqmzf6chq2dunx46ic2wme

Tx   : [0x7529b115dc2e8dad68da7b3d3843505afa91a4e5b3af5b272ab4a16bfc474c54](https://sepolia.etherscan.io/tx/0x7529b115dc2e8dad68da7b3d3843505afa91a4e5b3af5b272ab4a16bfc474c54)

在 Reputation 中，我们需要 x402 协议的 payment service 能够进行 x402 签名动作，用作 client 去进行 feedback。这点是个有异于标准 x402 的点，需要主动实现并提供一个方式，我个人的实现，会在 settle response 的时候，加上这个 签名信息。
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->


今天继续在实现 8004 的 SDK，目前 关于 Metadata, Feedback 等 off-chain 数据的定义都非常丰富，因为想要在 简洁+自定义 之间找到一个 平衡，默认配置极度简单，但是又可以让开发者自定义其中的各个部分。

在 Identity 中，可以上传特殊的 key-value 结构作为 onchain 的 metadata，但是有了 off-chain 的之后，这个地方需要存放什么，还有待考虑。在 x402 协议的情况下，我更希望让 payment agent 把支付的 支付方式 上传上去，因为它可能会有变动，如果直接存储在 off-chain 的 ipfs 中的话，有可能导致需要经常更新 ipfs，然后再更新 onchain 的 uri，当然如果 uri 指向 https 也不错，但是可能造成 subgraph 之类的无法访问。

特别是针对 Reputation 的方法，默认链上的参数，都挺复杂的，那么这就要求开发者能够把复杂的东西都封装起来，只保留最简洁的接口给使用者。

在 Reputation 里面，我发现一个 很 tricky 的东西，就是 feedback index，它在 new 的返回值和 event 中都没有出现，但是 revoke 和 append 都要求它，当然它可以通过 getLast 来拿到，但是这个就要求实现的时候，必须统一，否则就对不齐了，有些反直觉，这个东西必须封装起来，否则没人会去懂，这个 index 是哪里来的。
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->




今天在实现 [https://github.com/zpaynow/8004](https://github.com/zpaynow/8004) 8004 rust sdk，使用的是 chaoschain 他们的 abi，目前已经完成了基本的架构和合约解析，接下来会把实现过程中遇到的一些想法记录下来。

第一点：x402 payment agent 可以有 identity 和 reputation 部分，是否值得有 validation，因为它的验证（重现）的意义不大。
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->





正在基于 8004 协议的 abi，源自 chaoschain 的实现，来构建一个 rust sdk，用于与 8004 合约进行交互，目前分两个部分，一个是 sdk，第二个会有一个 bianry，用于命令行交互，代码会开源在：[https://github.com/ZeroPayDev/8004](https://github.com/ZeroPayDev/8004)，接下来就是对 8004 进行深度的研究和代码编写了。
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->






完成了 x402 rust 代码的实现，并合并到我的支付系统中了：[https://github.com/ZeroPayDev/ZeroPay/pull/8](https://github.com/ZeroPayDev/ZeroPay/pull/8)

下一步就是使用社区提供的 agent contracts 注册该 payment agent 服务，并思考其中对应的 3 种角色，是否需要。
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->







今天时间不多，继续在实现了一小会 x402 协议
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->








今天在继续实现 x402 协议，学习内容不多。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->









今天继续在实现 x402 协议，[https://github.com/ZeroPayDev/ZeroPay/pull/8](https://github.com/ZeroPayDev/ZeroPay/pull/8) 准备先只实现 evm，不实现 sol 生态。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->










明白 8004 协议之后，就得开始寻找具体的 agent 领域，除非是想做通用型的 agent exchange platform。目前结合自身，我开始学习 x402 -> A2A 这条路线，毕竟 payment 是最熟悉的。今天先学习 x402，并开始编码，尝试在我的开源项目中，实现一个，支持它。

更新：已经初步完成了 x402 协议的基本框架。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->












本质上是构建了一套 agent 发现和评价的标准体系。让 所有的 agent 都可以在 “某个” 地方被找到，并且通过相同的协议 去解析和了解它，当然因为它定义了这个 标准，所以可能会存在 **很多** 的 agent 市场，按照不同的类型。但是这些市场使用了同一套基础的解析模版。我能想象，未来肯定会出现 许多 agent 交易市场，针对不同类型的 agent 列表。是否会催生 第二个 opensea 呢？
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
