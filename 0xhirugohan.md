---
timezone: UTC+7
---

# hirugohan

**GitHub ID:** 0xhirugohan

**Telegram:** @hirugohan

## Self-introduction

a builder who currently learning and focusing on the research part

## Notes
<!-- Content_START -->
# 2025-10-28
<!-- DAILY_CHECKIN_2025-10-28_START -->
I guess it's the final day? honestly, nothing much compared to yesterday. I continue on the explorer page but no huge improvement. I rewrite it using React because somehow Astro is a bit weird on my end for pagination.

What's next? even if the Colearning for ERC-8004 is ended, I will still continue this project. An explorer to help myself to understand the landscape of "on-chain agents". I guess many people are working on it. But with many perspective working on different explorer, I expect that we could bring out some unique perspective that one day we could build a single explorer that represent all those perspectives and needs.

First, metadata is important, both for human and for agent. Those should be able to queried. Anyone (human and agent) should be able to find other agent based on their skills. And by using Reputation Registry, they should be able to filter the reputation based on certain parameters. Since I haven't dive deep into it, I still have no clue on what kind of reputation we can store both on-chain and off-chain, also how to retrieve them.

Of course x402 and Verification Registry are interesting but I am lacking a lot of time to research all of these stuff together. Because these are massive!

very amazing experience

here is my progress on the explorer. you can filter if the token URI is empty or not. I haven't stored the metadata from the tokenURI and from the A2A cards. also I included a statistics on like total agents, and the total agents with URI. and also unique owner address that I haven't done in the backend part.

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/0xhirugohan/images/2025-10-28-1761662970124-image.png)
<!-- DAILY_CHECKIN_2025-10-28_END -->

# 2025-10-27
<!-- DAILY_CHECKIN_2025-10-27_START -->

today I continue on the technical implementation part. I just finished an indexer for the identity registry because I want to list all the agent identities rather than like querying them one-by-one using tokenId (agent ID)  
  
when building it, I started to questioning like, how the agent supposed to use it? will the agent use on-chain directly to find another agent that could fulfill the task? but I don't think currently we can do that, because the only parameter accepted in the identity registry is through token id. which normally agent couldn't use it unless someone provide for this specific task use this agent id.

the identity registry contract is here [https://github.com/erc-8004/erc-8004-contracts/blob/master/contracts/IdentityRegistry.sol](https://github.com/erc-8004/erc-8004-contracts/blob/master/contracts/IdentityRegistry.sol)

that is one thing. the other thing is, the contract has onchain metadata storage with the name of `_metadata`. so, when do we have to store it in `_metadata`? and when do we have to store it in the tokenURI? what if there are same thing stored in these two places, but it has different value? which one we should trust or use?

now the last thing is, let's say that an agent is registered in 2 different chains. having a different agent id is not a problem. but what about the `_metadata` and the tokenURI? what if the `_metadata` is not the same across chains? what if the `tokenURI` is not referred to the same url?

this is honestly from the perspective of someone who just learnt about ERC-8004 and A2A. but I think making sure the data are same across "storage" and across "chains" is something that I think a bit concerning. I would love to see more use case, implementation, and more on what do people discover.

This is the interface I am working with. Someone shared an explorer already in the group but I can't find the link, so I decided to make my own. I want to make the explorer not only usable for human, but also for agent so they can utilize the A2A directly, and have the option to verify the metadata/tokenURI on-chain rather than relying only on my site.

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/0xhirugohan/images/2025-10-27-1761569736388-image.png)
<!-- DAILY_CHECKIN_2025-10-27_END -->

# 2025-10-26
<!-- DAILY_CHECKIN_2025-10-26_START -->


I took a day off yesterday, and I don't think I can take a day off again today, so I continue for a bit.

Not much changes, I focuses on the agent explorer and just finished decoding the metadata from the NFT. Next up I will spin up indexer so it can be dynamically listen to new agent entries and changes. idk how many day left, 2 days? 1 day? I'll focus on the agent explorer first, then interacting with them on-chain. Then making the A2A interactions between 2 agents or more. Then playing with the reputation registries. And finally playing with x402.  
  
I think verification registry need a dedicated research time since I have zero idea about any of the verification method.
<!-- DAILY_CHECKIN_2025-10-26_END -->

# 2025-10-24
<!-- DAILY_CHECKIN_2025-10-24_START -->



I finished reading whitepaper of x402 today, I got the concept and would love to try it directly. I want to focus more on the agentic use case of x402 rather than the human user one.

after finally finished reading ERC-8004, A2A, and x402. I decided to start a repository where I put everything there [https://github.com/0xhirugohan/all-about-erc-8004](https://github.com/0xhirugohan/all-about-erc-8004)

and now I am starting to developing. I was planning to working on the onchain of identity and reputation registry. But then I think like, what if I pulled back a bit. So I want to have a list of all identities and reputations. That way, when I registered a new identity and a new reputation, I can see it directly from the web view. It will takes a lot of time but I feel its more enjoyable if I have the explorer or visual interface to do it.
<!-- DAILY_CHECKIN_2025-10-24_END -->

# 2025-10-23
<!-- DAILY_CHECKIN_2025-10-23_START -->




I am definitely falling behind, but here is my note for today.

I finished the A2A today through reading the release blog by Google, the video introduction by Google Cloud, and also one from IBM. I started to understand what is A2A, and how A2A complies with MCP. So both MCP, A2A, and ERC-8004 are connected to each other.

Also previously I don't really have any image of how does A2A works. But now I understand that its kinda work like how actual human as a user interact with LLM. It communicates in a "human" way rather than machinery way.

In the A2A web/docs, there is a step-by-step tutorial. I haven't tried it. But definitely is going to read them and maybe implement it using different programming language rather than using Python.

And definitely if possible for the "capstone project" or "hackathon", or literally anything, I don't want to build my own MCP or Agent. I just want to use existing one and focus more on the ERC-8004 infrastructure. Or literally helping what's needed to be build around that part. So maybe it's pretty similar with other, I need more agent to be registered on the singleton so that I can utilize, test them out, and build something on top of it.

Tomorrow I will continue reading on the x402. Honestly I feel like out of the "line" here, like, I am not sure what is the end goal of the colearning. But I have my own goal, from the technical perspective, I want to try running end-to-end so I can understand how does it works. Maybe not playing much on the Verification Registry since it's pretty "complex" and advanced for me.
<!-- DAILY_CHECKIN_2025-10-23_END -->

# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->





I continue finishing blog posts from yesterday. I now kinda get that ERC-8004 was initially the extension of A2A. A2A has a "problem" that it requires "trust" within the system which ERC-8004 is trying to solve through a trustless networks.  
  
The goal is making the discovery and "reputation" and also "verification" to be on-chain (not all), so that it can become public and transparent. So there will be many tradeoffs in the process like what to put onchain vs offchain. And also making the ERC-8004 to be very minimal so that people can easily register. And the process later can be improved by protocols or dapps.  
  
I feel like running out of the time here. So maybe I won't read much about A2A and the x402. I will just see the overview and get dirty with the code for the remaining days.
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->






this note is a diary rather than a informational note, for personal progress and note.  
  
I just finished reading all the discussion in ethereum magicians for ERC-8004, and I can't summarize things because I feel like the whole discussion is going left and right without any proper way to manage the flow of discussion. Unless I ignore most of the discussions, I can see the focus more on the on-chain data part (I can't go depth into it since I can't understand much).  
  
I am kinda not on the track, so I will see if I could finish the ERC-8004 resources by tomorrow. And then, jump into A2A and x402. I'm planning to make a proper plan for week 2 so I can have more time in the technical part. Because I feel like it will take a lot of time because it's totally new to me.  
  
My technical plan if possible is use any existing agent and play with the on-chain and off-chain interactions rather than developing the agent myself. Then I would love to see how both on-chain data and off-chain data can be used. And thinking of what can I improve or contribute to this ERC in the infra part.
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->







almost done with the EIP discussion, few takeaways:  
\- it's a singleton (I just realized what does it mean), its literally one contract on each chain. so no need to deploy it multiple times  
\- I can understand some of the concern, but I also can understand the tradeoff and the scope focus  
  
ps, this is my first time reading almost everything from the ethereum magician discussions, and I can see the variety of people when discussing about this ERC.  
  
hopefully can finish it by tomorrow and then continue on the blog posts and VoD
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->








slow progress on weekend, will go full on Monday. I just finished 25% of the ERC-8004 discussion. In overview, I could see the concern being discussed like what to put on-chain vs off-chain. also about scoring/reputation modularity. I don't really know much the detail but I think I can keep it up later.  
  
I would love to see the scoring or reputation in action.
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->









I just finished reading the EIP-8004 but this note is not summary about it yet. It makes sense that the ERC-8004 uses existing standards/protocols such as MCP and A2A. And also it's pretty flexible and extendable into any other upcoming protocol as well.  
  
The Identity Registry is very simple and easy to understand. For the reputation registry, it's easy enough to understand but it's a bit unimaginable how it actually works in real-world case scenario on my end. It mentions about like the possibly of sybill attack etc which is possible and it lets the other protocol or dapp to handle it rather than ERC-8004 is the one who handling the rules about it.  
  
As for the Verification Registry, it's understandable but hard to imagine. I would love to see it in the real-world or even a very simple simulation on how it works for the "stake" and the other methods.  
  
Planning to continue on the EIP discussion, that is pretty long. And then on the VoD and blog posts.
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->










I've listed all the resources I need for the upcoming 2 weeks but mostly it's from this page.  
  
Today I plan to mainly finish the EIP and read the discussion part. Hopefully can manage into the blog posts.

Also attended the sharing session, so glad to attend because I can see it directly how does it works
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->











for today, I am planning to arrange the resources I will consume for this week. making sure that it's synced with the timeline from intensive co-learning. I'm focusing more on the theories, papers, and docs rather than building it myself.
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
