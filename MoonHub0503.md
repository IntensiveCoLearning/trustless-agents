---
timezone: UTC+8
---

# Joanna Ho

**GitHub ID:** MoonHub0503

**Telegram:** @MoonHub0503

## Self-introduction

Be a web3 builder~

## Notes
<!-- Content_START -->
# 2025-10-22
<!-- DAILY_CHECKIN_2025-10-22_START -->
**Agent2Agent (A2A) 协议：开启智能体互操作新时代**

**核心摘要：**

谷歌与50多家技术及服务伙伴联合推出开源协议**Agent2Agent**，旨在为不同框架和供应商开发的AI智能体建立统一通信标准，实现跨平台、跨系统的无缝协作，从而提升自动化水平、激发创新并降低长期成本。

* * *

**详细总结与翻译：**

**1\. 背景与愿景**

-   **机遇**：AI智能体能自主处理日常或复杂任务，极大提升生产力。企业正广泛部署智能体以优化流程（如设备订购、客服、供应链规划）。
    
-   **挑战与解决方案**：要最大化AI智能体的价值，关键在于让它们能在异构的数据系统和应用环境中动态协作。A2A协议应运而生，旨在**打破智能体之间的孤岛**，即使它们由不同厂商或不同框架构建，也能实现互操作，从而增强自主性、成倍提升效率并降低成本。
    
-   **共同愿景**：创造一个未来，无论AI智能体采用何种底层技术，都能无缝协作，自动化复杂的企业工作流，实现前所未有的效率和创新。
    

**2\. A2A协议是什么？**

-   一个**开放的、开源的**通信协议。
    
-   得到包括Atlassian、Box、Cohere、Intuit、Langchain、MongoDB、PayPal、Salesforce、SAP、ServiceNow、UKG、Workday等科技公司，以及埃森哲、BCG、凯捷、德勤、Infosys、毕马威、麦肯锡、普华永道、TCS、Wipro等领先服务提供商的支持。
    
-   与Anthropic的MCP协议互补，并借鉴了谷歌内部大规模智能体系统的经验。
    

**3\. A2A的核心设计原则**

-   **发挥智能体能力**：支持智能体以其自然的、非结构化的方式协作，不将其限制为单纯的“工具”。
    
-   **基于现有标准**：构建于HTTP、SSE、JSON-RPC等通用标准之上，易于与现有IT栈集成。
    
-   **默认安全**：支持企业级身份验证和授权。
    
-   **支持长时任务**：灵活支持从快速任务到可能耗时数小时甚至数天（含人工参与）的深度研究，并能提供实时反馈和状态更新。
    
-   **模态无关**：不仅支持文本，也支持音频、视频等多种模态。
    

**4\. A2A如何工作？**  
A2A协调“客户端”智能体与“远程”智能体之间的通信：

-   **能力发现**：智能体通过JSON格式的“智能体卡片”广告其能力，便于客户端智能体发现并调用最合适的智能体。
    
-   **任务管理**：通信围绕“任务”完成展开，任务具有生命周期，支持即时完成或长时运行，并能同步状态。任务输出称为“工件”。
    
-   **协作**：智能体可通过消息传递上下文、回复、工件或用户指令。
    
-   **用户体验协商**：消息中的“部分”包含格式化的内容（如图像），允许智能体协商所需的UI展示格式（如iframe、视频、网页表单等）。
    

**5\. 实际应用示例：候选人寻源**  
招聘经理可通过一个统一界面，指示自己的智能体寻找符合职位要求的候选人。该智能体随后通过A2A与其他专业智能体（如简历库搜索、面试安排）交互，汇总候选人建议，并可进一步安排面试、进行背景调查，极大地简化了招聘流程。

**6\. 合作伙伴反馈精选**  
合作伙伴普遍认为A2A是推动AI智能体互操作的关键一步，将：

-   打破数据和应用孤岛，实现安全、无缝的跨系统协作。
    
-   加速企业AI应用落地，释放自动化与智能化的巨大潜力。
    
-   通过开放标准，推动行业创新，构建更强大、更多元的智能体生态系统。
    
-   为企业提供跨平台、云环境管理智能体的标准化方法。
    

**7\. 未来与参与方式**

-   谷歌致力于与合作伙伴和社区共同建设该协议。
    
-   协议规范草案、代码示例和场景已发布在A2A网站上。
    
-   鼓励社区通过提交想法、完善文档等方式参与贡献，共同定义智能体互操作的未来。
    
-   预计**今年晚些时候**将发布生产就绪版本。
    

* * *

**总结要点：**

-   **目标**：解决AI智能体跨平台、跨框架协作的难题。
    
-   **性质**：开源、标准化通信协议。
    
-   **核心价值**：提升自动化、效率和创新，降低成本。
    
-   **关键特性**：安全、支持长时任务、多模态、易于集成。
    
-   **生态**：获得庞大合作伙伴生态系统的广泛支持。
    
-   **号召**：邀请开发者与社区共同参与，塑造未来。
<!-- DAILY_CHECKIN_2025-10-22_END -->

# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->


## **1\. A2A架构基础概念**

### **1.1 核心定义**

**Agent-to-Agent架构**是一个去中心化的智能体协作框架，其中：

-   每个智能体都是自主的决策实体
    
-   智能体通过标准化的协议进行通信
    
-   系统具备自组织和自适应能力
    

### **1.2 架构特点**

python

```
# A2A架构的核心特征
architecture_characteristics = {
    "decentralization": "无中心控制节点",
    "autonomy": "个体智能体自主决策",
    "interoperability": "跨平台、跨语言通信",
    "scalability": "动态扩展能力",
    "fault_tolerance": "局部故障不影响整体"
}
```

## **2\. 自主发现机制**

### **2.1 服务发现协议**

智能体通过以下方式发现彼此：

**2.1.1 注册发现模式**

yaml

```
# 服务注册发现流程
ServiceDiscovery:
  - 服务注册: Agent向注册中心发布能力描述
  - 服务查询: Agent通过注册中心查找所需服务
  - 心跳检测: 定期验证服务可用性
  - 动态更新: 服务状态实时更新
```

**2.1.2 对等发现模式**

python

```
class PeerDiscovery:
    def __init__(self):
        self.neighborhood_agents = []
        self.discovery_protocols = [
            "multicast_announcement",  # 组播宣告
            "gossip_protocol",         # 谣言传播协议
            "semantic_matching"        # 语义匹配发现
        ]
    
    def discover_peers(self, capability_requirements):
        """基于能力需求发现对等智能体"""
        matching_agents = []
        for agent in self.known_agents:
            if self.capability_match(agent.skills, capability_requirements):
                matching_agents.append(agent)
        return matching_agents
```

### **2.2 语义发现机制**

基于本体的智能体能力匹配：

python

```
class SemanticDiscovery:
    def __init__(self):
        self.ontology_base = AgentOntology()
    
    def semantic_match(self, requestor_needs, provider_capabilities):
        """语义级能力匹配"""
        # 基于本体推理进行智能匹配
        similarity_score = self.calculate_semantic_similarity(
            requestor_needs, 
            provider_capabilities
        )
        return similarity_score > MATCH_THRESHOLD
```

## **3\. 通信协议与模式**

### **3.1 通信原语**

基于FIPA ACL标准的通信原语：

python

```
class A2ACommunication:
    # 基本通信动作
    COMMUNICATIVE_ACTS = {
        "inform": "传递信息",
        "request": "请求行动",
        "query_ref": "查询信息",
        "propose": "提出建议",
        "accept_proposal": "接受提议",
        "reject_proposal": "拒绝提议",
        "cfp": "呼叫提案"
    }
    
    def send_message(self, receiver, performative, content, protocol):
        """发送标准化的A2A消息"""
        message = {
            "sender": self.agent_id,
            "receiver": receiver,
            "performative": performative,
            "content": content,
            "protocol": protocol,
            "language": "FIPA-SL",
            "ontology": "agent-communication",
            "timestamp": time.now()
        }
        return self.message_transport.send(message)
```

### **3.2 交互协议**

**3.2.1 合同网协议**

python

```
class ContractNetProtocol:
    def initiate_cfp(self, task_description, participants):
        """发起合同网协商"""
        # 1. 发布任务公告
        cfp_message = self.create_cfp_message(task_description)
        
        # 2. 收集投标
        proposals = self.collect_proposals(participants)
        
        # 3. 评估选择
        best_bidder = self.evaluate_proposals(proposals)
        
        # 4. 授予合同
        self.award_contract(best_bidder, task_description)
```

**3.2.2 协商协议**

python

```
class NegotiationProtocol:
    def automated_negotiation(self, initiator, responders, negotiation_topic):
        """自动化多轮协商"""
        current_offer = initiator.initial_offer
        rounds = 0
        
        while rounds < MAX_NEGOTIATION_ROUNDS:
            counter_offers = []
            for responder in responders:
                counter_offer = responder.evaluate_offer(current_offer)
                if counter_offer:
                    counter_offers.append(counter_offer)
            
            if self.reach_agreement(current_offer, counter_offers):
                return self.finalize_agreement()
            
            current_offer = self.generate_new_offer(counter_offers)
            rounds += 1
```

## **4\. 自主决策与协作**

### **4.1 分布式决策机制**

python

```
class AutonomousDecisionMaking:
    def collaborative_decision(self, context, available_agents):
        """协同决策过程"""
        # 1. 情境感知
        situation_assessment = self.assess_situation(context)
        
        # 2. 目标分解
        subgoals = self.decompose_goal(main_goal, available_agents)
        
        # 3. 角色分配
        role_assignment = self.dynamic_role_allocation(
            available_agents, 
            subgoals
        )
        
        # 4. 行动协调
        coordinated_plan = self.coordinate_actions(role_assignment)
        
        return coordinated_plan
```

### **4.2 信任与声誉管理**

python

```
class TrustManagement:
    def __init__(self):
        self.trust_network = {}
    
    def update_trust(self, agent_id, interaction_outcome):
        """基于交互结果更新信任值"""
        current_trust = self.trust_network.get(agent_id, INITIAL_TRUST)
        new_trust = self.calculate_new_trust(
            current_trust, 
            interaction_outcome
        )
        self.trust_network[agent_id] = new_trust
    
    def select_partner(self, capability_required):
        """基于信任和能力的伙伴选择"""
        candidates = self.discovery.find_agents(capability_required)
        ranked_candidates = self.rank_by_trust_and_capability(candidates)
        return ranked_candidates[0] if ranked_candidates else None
```

## **5\. 实现架构与模式**

### **5.1 微服务化A2A架构**

yaml

```
A2A_System_Architecture:
  Communication_Layer:
    - Message_Broker: "RabbitMQ/Kafka"
    - Serialization: "Protocol Buffers/JSON"
    - API_Gateway: "REST/gRPC endpoints"
  
  Discovery_Layer:
    - Service_Registry: "Consul/Etcd"
    - Health_Checking: "定期心跳检测"
    - Load_Balancer: "智能路由"
  
  Agent_Layer:
    - Specialized_Agents: "领域专用智能体"
    - Coordination_Agents: "协调智能体"
    - Interface_Agents: "人机交互智能体"
```

### **5.2 容错与恢复机制**

python

```
class FaultToleranceMechanism:
    def handle_agent_failure(self, failed_agent, ongoing_tasks):
        """处理智能体故障"""
        # 1. 检测故障
        if self.detect_failure(failed_agent):
            # 2. 任务重新分配
            backup_agents = self.find_backup_agents(failed_agent.capabilities)
            self.reassign_tasks(ongoing_tasks, backup_agents)
            
            # 3. 状态恢复
            self.recover_agent_state(failed_agent)
            
            # 4. 系统一致性维护
            self.maintain_system_consistency()
```

## **6\. 实际应用场景**

### **6.1 多智能体系统案例**

text

```
🤖 供应链优化系统
    ├── 供应商智能体：自主价格协商
    ├── 物流智能体：路径优化协调
    ├── 库存智能体：需求预测协作
    └── 销售智能体：市场响应协同

🎯 智能交通管理
    ├── 车辆智能体：路线规划
    ├── 信号灯智能体：流量优化
    ├── 停车场智能体：资源分配
    └── 调度中心智能体：全局协调
```

## **7\. 挑战与解决方案**

### **7.1 关键技术挑战**

python

```
challenges_and_solutions = {
    "语义互操作性": "建立共享本体和标准化通信语言",
    "安全与隐私": "实施加密通信和权限控制",
    "资源竞争": "设计公平的协商和分配机制",
    "系统复杂性": "采用模块化和分层设计",
    "扩展性限制": "使用分布式发现和通信协议"
}
```

## **总结**

A2A架构中的自主发现和通信是一个复杂但强大的范式，它通过：

1.  **标准化协议**实现智能体间的无缝交互
    
2.  **动态发现机制**支持系统的弹性扩展
    
3.  **自主决策算法**确保个体的智能行为
    
4.  **协作协调协议**实现集体智能涌现
    

这种架构为构建大规模、自适应、鲁棒的分布式人工智能系统提供了坚实的技术基础，正在成为下一代智能系统的重要发展方向。
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->



**背景**  
随着大语言模型（LLM）在推理和工具使用方面日益强大，由智能体框架、工具和LLM驱动的**智能体经济**正在兴起，对企业提升效率和自动化至关重要。然而，众多智能体和框架导致它们之间难以验证和交互。

**Google的A2A协议与其局限性**  
Google推出了**A2A协议**，旨在让集成了该协议的智能体能够轻松地通过"智能体卡片"相互识别和通信，从而跨框架和供应商执行任务。

然而，A2A协议**不符合Web3的抗审查和透明精神**，因为它假设了客户端智能体与服务端智能体之间已存在信任。相比之下，区块链通过密码学证明和链上不可变记录，能提供额外的透明度和信任层。

**以太坊的地位与ERC-8004的提出**  
以太坊目前主导着DeFi和现实世界资产市场，已成为**机构资本部署的首选层**。随着Web3智能体经济从社交和Meme币交易扩展到支持机构的链上战略，建立一个**无需信任、可验证且安全的智能体通信框架**变得至关重要。

为此，提出了**ERC-8004提案**，它作为A2A协议的扩展，旨在巩固以太坊作为AI协调基础层的地位。

**ERC-8004是什么？**  
ERC-8004是一个**信任层**，使利用A2A协议的链上智能体能够在**无需预先信任**的情况下进行交互。它引入了三个核心注册表：

1.  **身份注册表**：扩展A2A的"智能体卡片"，包含智能体的EVM地址，通过`(代理域, 代理地址)`来唯一标识智能体。
    
2.  **声誉注册表**：允许客户端智能体在任务完成后提供反馈。反馈通过`FeedbackDataURI`指向包含服务评级的JSON文件，支持多维评估。
    
3.  **验证注册表**：提供两种主要验证：
    
    -   **密码经济验证**：可由再质押AVS、可信中心化代理或可编程治理机制提供。
        
    -   **密码学验证**：可使用可信执行环境或零知识证明等技术。
        

**工作流程**

1.  智能体初始化并注册到身份注册表。
    
2.  客户端智能体发现服务端智能体，并协商任务输出。
    
3.  服务端接受任务，并承诺接受反馈。
    
4.  服务端执行任务，发布数据哈希，并请求验证。
    
5.  验证者智能体监视请求并进行验证。
    
6.  验证成功后，验证者响应。
    
7.  凭借验证响应，托管资金可以被释放以支付服务。
    
8.  客户端智能体发布包含关键信息的反馈证明，使结果可查询。
    

**优势**

-   **便携的发现与溯源**：通过身份注册表和智能体卡片实现。
    
-   **跨链互操作性**：智能体地址采用CAIP-10标准。
    
-   **可插拔的信任模型**：灵活支持TEE证明、zkTLS证明和密码经济安全。
    
-   **证明层中立性**。
    
-   **轻量级链上足迹**：平衡Gas费，同时在声誉算法、验证和存储协议上保持灵活。
    

**主要受益方**

-   **再质押服务**：验证注册表为再质押网络提供了中立的验证接口。
    
-   **TEE和证明系统**：协议明确支持基于TEE和ZK证明的密码学可验证信任模型。
    
-   **潜在用例**：加密领域深度研究智能体、AI加密对冲基金、链上信用评级、智能体评分服务、零工经济的有条件里程碑支付等。
    

**结论**  
ERC-8004通过建立在EVM网络上用于AI智能体协调的**无需信任层**，标志着智能体发展历程中的一个重要进展。就如同MCP为访问工具创建了通用框架，A2A为Web2智能体构建了通用通信层一样，ERC-8004作为一个蓝图，有潜力通过利用以太坊实现无需信任、可互操作的智能体间协调，来**解锁新的收入流并增强用户体验**。
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->




**ERC-8004 的诞生与愿景：为AI打造去中心化公共语言**

我们的“无需信任AI代理”提案在以太坊生态中引起了巨大反响。本文将讲述ERC-8004的诞生故事与下一步计划。

**核心理念**  
为了抵御中心化AI的垄断，我们需要分布式的代理经济体。而实现这一目标的关键，在于建立一套**共享的公共语言**，让代理能够相互发现、建立信任并进行通信。我们不需要新的底层区块链，**以太坊L1/L2 + 链下数据** 已是最佳选择，因其拥有最可信的去中心化特性和最繁荣的开发者生态。

**问题起源：协调的困境**  
在探索去中心化AI时，我发现许多项目都创建了自己的语言和架构，这带来了经典的协调问题：如何让所有人都说同一种语言？

当谷歌将其**Agent2Agent协议**捐赠给Linux基金会时，我最初感到振奋。但深入研究后，我发现该协议忽略了Web3和无需信任的使用场景，其设计仍局限于组织内部的信任假设。

**解决方案：ERC-8004的诞生**  
在以太坊基金会的支持下，我们开始着手解决这个问题。ERC-8004的设计遵循两大原则：

1.  **不重复造轮子**：协议不仅扩展了A2A，并且将其信任机制建立在现有构建者已熟悉的概念上（如基于质押的验证参考EigenLayer，TEE证明参考Phala等）。
    
2.  **保持极简**：协议极其轻量，仅利用区块链作为**逻辑上的中央入口**，提供可见性（哪些代理已注册、存在哪些验证请求）和数据承诺。所有其他复杂功能（如声誉计算）都交由链下或其他特定协议去实现。
    

**本质上是解决了一个协调问题**：ERC-8004为所有人提供平等的数据和可见性以创建代理经济体，同时将具体的规则和信任阈值交给生态自身决定。

**社区反响：“终于来了！”**  
协议发布后，社区的反响远超预期，被翻译成十多种语言并被广泛讨论。这表明生态内部对于将我们关心的**Web3原则（无需许可、去中心化、抗审查、隐私保护）应用于AI** 有着巨大的潜在需求。人们的本能反应是“终于等到你了！”，因为我们已经空谈“AI运行在区块链上”两年了，而ERC-8004终于提供了具体的实现路径。

**下一步计划：构建优先**  
我们将采用“**构建优先**”的方式来管理此ERC的讨论。协议最终成功在于采用。我们将优先考虑那些承诺基于此标准进行构建的团队的反馈和变更请求，并始终保持标准的最小化和中立性。

**共同目标：让以太坊成为我们AI未来的可信基础设施。**
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->





**ERC-8004：自主AI代理的基础设施**

**核心概述**  
ERC-8004是一个为自主AI代理网络奠定基础的技术标准。它通过引入基于区块链的信任机制，扩展了谷歌的Agent-to-Agent协议，旨在实现无需信任的协调和去中心化的基础设施，推动"代理经济体"的发展。

**核心组件**  
该标准定义了三个核心链上注册表，作为跨组织代理交互的信任骨干，采用混合架构：

1.  **身份注册表**：
    
    -   为每个代理提供便携、抗审查的唯一标识符。
        
    -   将`AgentID`与代理的域名和以太坊地址绑定，创建全局命名空间。
        
    -   代理需在其域名下托管一个`Agent Card`文件，包含区块链相关信息。
        
2.  **声誉注册表**：
    
    -   采用轻量级设计，仅在链上处理代理间的"反馈授权"事件。
        
    -   实际的声誉数据和复杂的评分算法置于链下，兼顾灵活性与成本。
        
3.  **验证注册表**：
    
    -   提供通用钩子，用于请求和记录独立验证。
        
    -   支持多种验证协议，包括经济质押和可信执行环境认证。
        

**解决的问题**

-   **信任鸿沟**：解决了谷歌A2A协议在跨组织、无需信任环境中无法验证代理身份和声誉的问题。
    
-   **市场失灵**：解决了代理在开放经济中面临的**发现**、**质量保证**、**声誉可移植性**和**验证可扩展性**等核心问题。
    

**工作原理**  
通过三个互联的智能合约实现信任基础设施：

-   **身份注册表**：管理代理的全局身份映射（ID、域名、地址）。
    
-   **声誉注册表**：仅发射授权事件，链下存储具体反馈数据。
    
-   **验证注册表**：管理验证请求和响应，支持经济抵押等机制。
    

**分层信任模型**  
ERC-8004采用与风险匹配的分层安全架构：

1.  **声誉信任**：适用于低风险任务，依赖累积的链下反馈。
    
2.  **加密经济验证**：适用于中等风险任务，验证者需质押资产，作恶将被罚没。
    
3.  **加密学验证**：适用于高风险任务，使用TEE等提供计算完整性和保密性的密码学证明。
    

**安全考量**  
标准识别并提出了针对以下攻击的缓解措施：

-   域名抢注
    
-   未经授权的反馈
    
-   存储膨胀和拒绝服务攻击
    
-   女巫攻击
    

**结论**  
ERC-8004通过将区块链的无需信任基础设施与AI的自主潜力相结合，为实现"代理经济体"迈出了变革性的一步。它通过轻量级、可扩展的注册表解决了跨组织代理交互中的关键信任缺口，有望释放万亿美元级别的市场潜力。确保其底层智能合约的安全审计对于实现可持续、可靠的自主经济协作至关重要。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->






（ERC-8004）为以太坊的智能代理（Agent）间协议引入了**去中心化信任层**，使不同组织间的代理能够**在没有预先建立信任的情况下**进行发现、选择和交互。它通过三个**轻量级链上注册表（身份、声誉、验证）** 实现信任锚定，而将具体的应用逻辑留给**链下组件**处理。

在公开讨论中，有开发者提出关键改进建议：**当前标准过于侧重链下读取，而忽略了链上可组合性的巨大价值**。建议增强链上智能合约对注册表数据（如验证结果、声誉分数）的读取能力，以实现更复杂的链上权限逻辑和模块化执行（例如罚没机制）。

此外，社区建议**声誉注册表**应支持**聚合多个提供方的评分**，以形成一个更全面、抗偏见和共谋的累积声誉指标，供链上与链下消费者共同使用。

* * *

**详细翻译与要点解析：**

1.  **标准概述:**
    
    -   **原文:** "This standard extends the Agent-to-Agent (A2A) protocol with a trust layer..."
        
    -   **翻译与解析:** 该标准通过一个**信任层**扩展了代理到代理协议，使得参与者能够在**没有预先信任**的情况下，跨组织边界发现、选择并与代理进行交互。
        
2.  **技术架构:**
    
    -   **原文:** "It introduces three lightweight, on-chain registries—Identity, Reputation, and Validation—and leaves application-specific logic to off-chain components."
        
    -   **翻译与解析:** 它引入了三个轻量级的**链上注册表——身份、声誉和验证**，并将**应用特定逻辑留给链下组件**处理。
        
3.  **社区反馈与改进建议:**
    
    -   **核心批评:**
        
        -   **原文:** "...this standard prioritizes offchain reads... over onchain reads... I think this is a big miss."
            
        -   **翻译与解析:** 有观点认为，该标准**优先考虑链下读取而非链上读取**，这是一个重大不足。因为代理创造的许多价值涉及**需要链上权限的操作**，因此为**链上可组合性**创建基础组件非常有价值。
            
        -   **具体建议:** 标准应允许任意智能合约读取验证结果等数据，从而将**验证与执行解耦**，让其他协议能基于验证结果模块化地创新（如实施罚没逻辑）。
            
    -   **对声誉系统的建议:**
        
        -   **原文:** "...the Reputation registry could use functions for multiple Reputation scores from one or multiple providers..."
            
        -   **翻译与解析:** **声誉注册表**应具备处理来自一个或多个提供方的**多个声誉评分**的功能。这可以作为一个代理和提供方的**累积感知声誉的快照/证明**。
            
        -   **优势:** 使该注册表成为**链上和链下消费者的统一入口**，并利用**多个提供方的评分**来降低偏见、共谋等风险。
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->







ERC-8004 旨在创建一个**无需信任、可发现且能建立信任的开放代理经济体系**。它通过在区块链上部署三个轻量级的注册表来实现这一目标，使代理（AI Agent）能够被跨组织发现，并通过声誉和验证机制来建立信任，而无需预先存在的信任关系。

* * *

### **详细翻译与总结**

**1\. 基本概况**

-   **标题**: ERC-8004: 无需信任的代理
    
-   **核心目标**: 通过声誉和验证来发现代理并建立信任。
    
-   **状态**: 正在同行评审中（创建于2025-08-13）。
    
-   **核心方案**: 提出三个核心的链上注册表。
    

**2\. 摘要**

该协议提出利用区块链来**跨组织边界**地**发现、选择和交互**代理，而无需预先存在的信任，从而构建开放的代理经济。

-   **可插拔的信任模型**: 开发者可以根据任务的风险等级（从订购披萨到医疗诊断）选择三种信任模型：
    
    1.  **声誉系统**: 基于客户反馈。
        
    2.  **验证系统**: 通过质押担保的重新执行、零知识机器学习证明或可信执行环境预言机。
        
    3.  **TEE证明**。
        

**3\. 动机**

现有的代理通信协议（如MCP和A2A）本身不涵盖**代理发现和信任**。为了培育开放的代理经济，需要一种在不可信环境中发现和信任代理的机制。ERC-8004通过三个注册表解决了这一需求。

**4\. 核心规范（三个注册表）**

**a. 身份注册表**

-   **功能**: 为每个代理提供一个**全局唯一的、可移植的、抗审查的身份标识**。
    
-   **技术实现**: 基于ERC-721（NFT）标准。每个代理被铸造为一个NFT。
    
-   **注册文件**: 每个代理的 `tokenURI` 指向一个包含其详细信息的JSON文件，包括：
    
    -   名称、描述、图像。
        
    -   **端点**: 列出代理支持的各种协议和服务地址（如A2A、MCP、ENS、钱包地址等）。
        
    -   **支持的信任模型**: 声明代理支持哪种信任建立方式（声誉、加密经济、TEE证明等）。
        

**b. 声誉注册表**

-   **功能**: 提供一个标准接口，供客户（人或代理）对代理的服务提供**反馈和评分**。
    
-   **核心机制**:
    
    -   **预授权**: 代理在接受任务前，需要预先签署一个授权，允许特定客户为其提供反馈。
        
    -   **反馈内容**: 包括分数（0-100）、自定义标签、以及一个指向更详细反馈文件的URI。
        
    -   **链上+链下结合**: 分数和标签存储在链上以便组合使用，详细反馈存储在链下（如IPFS）以实现复杂分析。
        
-   **主要操作**:
    
    -   `giveFeedback`: 提交反馈。
        
    -   `revokeFeedback`: 撤销反馈。
        
    -   `appendResponse`: 对反馈追加回应（如代理辩解或数据聚合商标记垃圾信息）。
        

**c. 验证注册表**

-   **功能**: 为代理提供一个标准接口来**请求对其工作进行独立验证**。
    
-   **工作流程**:
    
    1.  **验证请求**: 代理提交一个验证请求，指向包含其工作输入/输出的链下数据。
        
    2.  **验证响应**: 指定的验证者（如zkML验证器、TEE预言机）检查工作并返回一个响应（0-100分），并可选地提供证明。
        
-   **用途**: 适用于需要高保证的任务，通过密码学或经济抵押来证明工作的正确性。
    

**5\. 设计原理**

-   **灵活性**: 支持现有的（MCP, A2A）和未来可能出现的代理通信协议。
    
-   **组合性**: 链上存储的核心信号（如声誉分数）可以被其他智能合约读取和使用。
    
-   **用户体验**: 利用如EIP-7702等标准，可以实现无需用户持有代币即可支付Gas费，提供无缝体验。
    
-   **部署**: 预计在每个链上以单例模式部署。一个代理可以在一条链上注册和积累声誉，同时在多条链上运作。
    

**6\. 安全考虑**

-   **女巫攻击**: 协议本身不能完全防止通过创建大量虚假身份（Sybil攻击）来刷高声誉。它的价值在于**使所有信号公开化**，从而激励第三方构建更复杂的声誉聚合和反垃圾系统。
    
-   **审计轨迹**: 链上的指针和哈希一旦创建就无法删除，保证了数据的可审计性。
    
-   **功能保证**: 该协议能**密码学地保证**注册文件与链上代理身份的对应关系，但**无法保证**代理广告的功能是正常且无恶意的。这正是三种信任模型要解决的问题。
    
-   **验证者激励**: 验证者本身的激励和惩罚机制由它们各自的特定协议管理，不在本ERC范围内。
    

### **总结**

**ERC-8004 旨在成为开放AI代理经济的基石协议。** 它通过：

1.  **身份NFT** 解决“代理是谁”和“如何连接”的问题。
    
2.  **声誉系统** 解决“这个代理做得好不好”的问题，依赖于社区众包评价。
    
3.  **验证系统** 解决“这个代理的工作结果是否可信”的问题，依赖于密码学或经济抵押验证。
    

最终，它为实现一个充满活力、竞争且可互操作的AI代理市场提供了必要的底层基础设施。
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
