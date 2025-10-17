---
timezone: UTC+8
---

# Marvin

**GitHub ID:** Floydwish

**Telegram:** @Flashsky1235

## Self-introduction

我叫 Marvin (很喜欢银河系漫游指南中那个忧郁的机器人，名字由此而来)
做过 C++ 桌面应用程序的开发，目前正在学习 EVM 智能合约开发，关注 Web3 ，提升技能和认知中。

## Notes
<!-- Content_START -->

# 2025.10.15
<!-- DAILY_CHECKIN_2025-10-15_START -->

# ERC-8004：AI 代理的链上协作标准

ERC-8004（2025年8月提案）是以太坊上 AI 代理（autonomous agents）协作的基础设施标准，扩展 Google 的 A2A 协议，解决去中心化环境中的身份注册、信任验证和协作问题。

---

## 1. 核心特性

### 三个注册表

**Identity Registry（身份）**
- 管理 AgentID、域名、地址映射
- 防域名抢注（commit-reveal）
- 支持域名解析

**Reputation Registry（声誉）**
- 事件授权反馈机制
- 链下存储评分数据
- 低成本信任累积

**Validation Registry（验证）**
- 支持质押验证（EigenLayer）
- TEE/zkTLS 加密证明
- 多层次信任模型

### 分层信任模型

```
低风险：声誉反馈（~20k gas）
中风险：经济质押（EigenLayer 再质押）
高风险：加密证明（TEE/zk）
```

### 设计原则

- **轻量化**：链上存哈希承诺，链下执行复杂逻辑
- **事件驱动**：减少状态存储，降低 gas
- **多链兼容**：支持 CAIP-10 标准

---

## 2. Solidity 实现

### Identity Registry（身份注册）

```solidity
pragma solidity ^0.8.20;

contract IdentityRegistry {
    struct Agent {
        uint256 AgentID;
        string AgentDomain;
        address AgentAddress;
        uint256 registrationTime;
        bool isActive;
    }
    
    uint256 private _nextAgentID = 1;
    mapping(uint256 => Agent) public agents;
    mapping(string => uint256) public domainToAgentID;
    mapping(address => uint256) public addressToAgentID;

    event NewAgent(uint256 indexed AgentID, string AgentDomain, address AgentAddress);
    event UpdateAgent(uint256 indexed AgentID, string newDomain, address newAddress);

    function NewAgent(string calldata AgentDomain, address AgentAddress) external returns (uint256) {
        require(AgentAddress != address(0), "Invalid address");
        require(domainToAgentID[AgentDomain] == 0, "Domain taken");
        
        uint256 agentId = _nextAgentID++;
        agents[agentId] = Agent(agentId, AgentDomain, AgentAddress, block.timestamp, true);
        domainToAgentID[AgentDomain] = agentId;
        addressToAgentID[AgentAddress] = agentId;
        
        emit NewAgent(agentId, AgentDomain, AgentAddress);
        return agentId;
    }

    function Get(uint256 AgentID) external view returns (uint256, string memory, address) {
        Agent memory agent = agents[AgentID];
        require(agent.isActive, "Agent inactive");
        return (agent.AgentID, agent.AgentDomain, agent.AgentAddress);
    }
}
```

### Reputation Registry（声誉反馈）

```solidity
contract ReputationRegistry {
    event AuthFeedback(uint256 indexed ClientID, uint256 indexed ServerID, bytes32 FeedbackAuthID);

    function AcceptFeedback(uint256 ClientID, uint256 ServerID) external returns (bytes32) {
        bytes32 authID = keccak256(abi.encodePacked(ClientID, ServerID, block.timestamp, block.number));
        emit AuthFeedback(ClientID, ServerID, authID);
        return authID;  // 链下用此授权提交反馈
    }
}
```

### Validation Registry（验证请求）

```solidity
contract ValidationRegistry {
    struct Request {
        uint256 ValidatorID;
        uint256 ServerID;
        uint256 timestamp;
        bool active;
    }
    mapping(bytes32 => Request) public requests;

    event ValidationRequest(bytes32 indexed DataHash, uint256 indexed ValidatorID, uint256 indexed ServerID);
    event ValidationResponse(bytes32 indexed RequestID, bool isValid, bytes proof);

    function ValidationRequest(bytes32 DataHash, uint256 ValidatorID, uint256 ServerID) external {
        require(DataHash != bytes32(0), "Invalid hash");
        requests[DataHash] = Request(ValidatorID, ServerID, block.timestamp, true);
        emit ValidationRequest(DataHash, ValidatorID, ServerID);
    }

    function ValidationResponse(bytes32 DataHash, bool isValid, bytes calldata proof) external {
        Request storage req = requests[DataHash];
        require(req.active, "Inactive request");
        emit ValidationResponse(DataHash, isValid, proof);
        req.active = false;
    }
}
```

**Gas 预估**：
- 注册代理：~50k gas
- 授权反馈：~20k gas
- 验证请求：~30k gas

---

## 3. 与 A2A 协议集成

### 工作流程

```
1. 链下：A2A Agent Card 发现能力
2. 链上：ERC-8004 验证身份
3. 链下：A2A 协商任务（JSON-RPC）
4. 链上：提交 DataHash 承诺
5. 链下：执行任务
6. 链上：验证结果 + 反馈
```

### 技术集成

- **身份映射**：A2A Agent Card 扩展 EVM 地址
- **信任桥接**：链上注册表 + 链下通信
- **跨链支持**：CAIP-10（多链代理协作）
- **证明系统**：集成 EAS、TEE、zkTLS

---

## 4. 应用场景

### DeFi 策略代理
```
场景：自动化套利机器人
- 代理注册身份 → Identity Registry
- 协商策略 → A2A 链下
- 质押保证金 → Validation Registry
- 执行套利 → 链上验证
```

### DAO 决策代理
```
场景：多代理投票治理
- 各代理注册 → 验证投票权
- 链下讨论提案 → A2A
- 链上提交投票 → 可验证
- 声誉累积 → Reputation Registry
```

### 审计工具代理
```
场景：代码安全审计
- 审计代理注册
- 提交审计任务
- zk 证明审计结果
- 链上验证 + 反馈
```

---

## 5. 技术挑战

### 安全问题
- **域名抢注**：使用 commit-reveal 机制
- **Sybil 攻击**：要求质押 bond
- **DoS 攻击**：请求限额 + 过期机制

### Gas 优化
- 使用事件而非存储（节省 ~80% gas）
- L2 部署（高频交互）
- 批量操作

### 信任模型
- 灵活设计（unopinionated）
- 需要自定义验证逻辑
- 平衡安全与成本

---

## 6. 开发建议

### 快速开始

```bash
# 使用 Foundry 测试参考实现
forge init erc8004-agent
cd erc8004-agent

# 安装依赖
forge install OpenZeppelin/openzeppelin-contracts

# 编写合约（参考上面代码）
# 编写测试
forge test
```

### 集成要点

1. **模块化接口**：IIdentityRegistry、IReputationRegistry
2. **事件监听**：链下服务监听链上事件
3. **EAS 集成**：使用 Ethereum Attestation Service
4. **Oracle 集成**：链上验证链下数据

### 安全审计

- 防止未授权反馈
- 验证 DataHash 唯一性
- 保护质押资金
- 防止重入攻击

---

## 总结

**ERC-8004 = AI 代理的链上身份与信任层**

- **技术**：Solidity 注册表 + 事件驱动
- **优势**：低 gas（~20-50k）+ 去中心化
- **挑战**：安全审计 + 信任模型设计
- **未来**：与 EigenLayer、zkTLS 结合，推动代理经济

**参考资源**：
- 提案讨论：https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098
- Google A2A：https://github.com/google/a2a
- 预计主网：2026年

---

**适用场景**：DeFi 自动化、DAO 治理、审计工具、RWA 管理

<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
