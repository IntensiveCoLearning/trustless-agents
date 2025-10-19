---
timezone: UTC+8
---

# Stephen

**GitHub ID:** kuove

**Telegram:** @stephkuove

## Self-introduction

努力转向web3的开发者

## Notes

<!-- Content_START -->
# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->
参考@点点

**三、实操：为 Agent 创建链上身份并实现简单链下声誉反馈机制**

**（一）前置准备**

NaN. **开发环境搭建**：

-   安装 Truffle 或 Hardhat 开发框架（本文以 Hardhat 为例），用于智能合约的编译、部署与测试；
    
-   配置以太坊测试网络（如 Goerli、Sepolia），获取测试 ETH（通过测试网水龙头），用于支付合约部署与交易 Gas 费；
    
-   安装 MetaMask 钱包，创建测试账户，用于作为 Agent 的关联地址。
    

NaN. **依赖资源准备**：

-   从 EIP-8004 官方标准（参考 “资源” 部分）获取 ERC-8004 智能合约接口代码（IERC8004Identity.sol、IERC8004Reputation.sol、IERC8004Verification.sol）；
    
-   准备 IPFS 节点或使用 Pinata 等 IPFS 服务，用于存储 Agent 身份元数据。
    

**（二）步骤 1：为 Agent 创建链上身份**

**1\. 编写 Agent 身份元数据**

Agent 的身份元数据需包含以下核心信息（以 JSON 格式为例）：

```
{
  "agentName": "TaskExecutorAgent",
  "agentType": "Service Agent",
  "description": "An Agent specialized in executing on-chain tasks such as data verification and asset transfer",
  "associatedAddresses": ["0x1234567890abcdef1234567890abcdef12345678"], // MetaMask测试账户地址
  "owner": "0xabcdef1234567890abcdef1234567890abcdef12", // Agent所有者地址
  "creationTime": "2024-XX-XXTXX:XX:XXZ"
}

```

将该 JSON 文件上传至 IPFS，获取元数据哈希（如`QmXf8dGp8z7y6Z9a5Y7b3c2d1e4f5g6h7j8k9l0m1n2o3p4`）。

**2\. 部署 ERC-8004 身份注册表合约**

-   在 Hardhat 项目中创建`ERC8004Identity.sol`合约，实现 IERC8004Identity 接口定义的`registerIdentity`、`updateIdentityMetadata`等核心函数（可参考 Vistara Apps 提供的 ERC-8004 示例代码，简化开发）；
    
-   编写部署脚本（deploy.js）：
    

```
const hre = require("hardhat");

async function main() {
  const identityContractAddress = "0x9876543210fedcba9876543210fedcba98765432";
  const identityContract = await hre.ethers.getContractAt("ERC8004Identity", identityContractAddress);
  const [deployer] = await hre.ethers.getSigners(); // 使用MetaMask测试账户（需配置Hardhat与MetaMask连接）

  const metadataHash = "QmXf8dGp8z7y6Z9a5Y7b3c2d1e4f5g6h7j8k9l0m1n2o3p4";
  const associatedAddresses = ["0x1234567890abcdef1234567890abcdef12345678"];

  const tx = await identityContract.connect(deployer).registerIdentity(metadataHash, associatedAddresses);
  await tx.wait();
  console.log("Agent identity registered successfully!");

  // 查询注册后的Identity ID（假设合约有getIdentityIdByAddress函数）
  const identityId = await identityContract.getIdentityIdByAddress(associatedAddresses[0]);
  console.log("Agent Identity ID:", identityId.toString());
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});

```

-   执行部署命令：`npx hardhat run scripts/deploy.js --network sepolia`，记录部署后的合约地址（如`0x9876543210fedcba9876543210fedcba98765432`）。
    

**3\. 调用合约注册 Agent 身份**

-   编写交互脚本（registerAgent.js），通过 MetaMask 测试账户调用`registerIdentity`函数：
    

```
const hre = require("hardhat");

async function main() {
  const identityContractAddress = "0x9876543210fedcba9876543210fedcba98765432";
  const identityContract = await hre.ethers.getContractAt("ERC8004Identity", identityContractAddress);
  const [deployer] = await hre.ethers.getSigners(); // 使用MetaMask测试账户（需配置Hardhat与MetaMask连接）

  const metadataHash = "QmXf8dGp8z7y6Z9a5Y7b3c2d1e4f5g6h7j8k9l0m1n2o3p4";
  const associatedAddresses = ["0x1234567890abcdef1234567890abcdef12345678"];

  const tx = await identityContract.connect(deployer).registerIdentity(metadataHash, associatedAddresses);
  await tx.wait();
  console.log("Agent identity registered successfully!");

  // 查询注册后的Identity ID（假设合约有getIdentityIdByAddress函数）
  const identityId = await identityContract.getIdentityIdByAddress(associatedAddresses[0]);
  console.log("Agent Identity ID:", identityId.toString());
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});

```

-   执行交互命令：`npx hardhat run scripts/registerAgent.js --network sepolia`，完成 Agent 链上身份注册，记录 Identity ID（如`123`）。
    

**（三）步骤 2：实现简单链下声誉反馈机制**

由于链上存储成本较高，对于高频、轻量级的声誉反馈（如用户对 Agent 服务的评分、简短评价），可采用 “链下存储 + 链上哈希存证” 的方式实现，兼顾成本与可信度。

**1\. 设计链下声誉反馈数据结构**

每个声誉反馈记录包含以下信息（JSON 格式）：

```
{
  "feedbackId": "fb-123456", // 反馈唯一标识
  "agentIdentityId": "123", // 被反馈Agent的Identity ID
  "feedbackProvider": "0xabc123def456abc123def456abc123def456abc1", // 反馈发起方地址
  "score": 4, // 评分（1-5分）
  "comment": "The Agent completed the task quickly, but the result had a small error", // 评价内容
  "feedbackTime": "2024-XX-XXTXX:XX:XXZ",
  "signature": "0x...", // 反馈发起方对该反馈记录的签名，用于验证真实性
  "metadataHash": "QmY7a9b8c7d6e5f4g3h2j1k0l9m8n7o6p5q4r3s2t1u0v" // 反馈记录的IPFS哈希
}

```

**2\. 搭建链下声誉反馈系统（简易版）**

-   **前端界面**：使用 HTML+JavaScript 搭建简单页面，提供 “输入 Agent Identity ID”“选择评分（1-5 分）”“填写评价内容” 的表单，用户提交后调用 MetaMask 签名该反馈记录；
    
-   **后端服务**：使用 Node.js+Express 搭建后端，接收前端提交的签名后反馈记录，验证签名真实性（通过 ethers.js 的`verifyMessage`函数），验证通过后将反馈记录上传至 IPFS，获取 metadataHash；
    
-   **链上存证**：后端调用 ERC-8004 声誉注册表合约的`recordReputation`函数，将 “评分转化的分数变更”（如 4 分对应 + 4 分，2 分对应 - 1 分）、反馈记录的 metadataHash 作为 reason 参数，完成声誉分数的链上更新与反馈记录的哈希存证。
    

**3\. 声誉反馈查询与展示**

-   用户可在前端输入 Agent 的 Identity ID，前端调用后端接口查询该 Agent 的所有链下声誉反馈记录（从 IPFS 获取），同时调用链上合约查询当前声誉分数，综合展示 Agent 的声誉情况（如 “当前分数：108 分，共收到 5 条反馈，平均评分 4.2 分”）。
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->

参考@点点

**Module 1：信任基础 ——ERC-8004 身份与声誉层学习笔记**

**一、ERC-8004 标准整体认知**

ERC-8004 作为以太坊生态中聚焦 “身份与声誉” 的关键标准，核心目标是为链上主体（尤其是 Agent 智能体）构建一套可信赖的信任基础设施。在当前 Web3 与 Agent 经济快速发展的背景下，传统链上交互仅依赖地址标识，缺乏对主体身份真实性、行为可信度的有效评估维度，而 ERC-8004 通过定义统一的身份注册、声誉记录与验证机制，填补了这一空白，为 Agent 间协作、资源交互、风险控制提供了标准化的信任依据，是推动 Agent 经济规模化落地的重要技术基石。

**二、ERC-8004 标准核心组成深度解析**

**（一）身份注册表（Identity Registry）：链上身份的 “数字身份证”**

**1\. 核心定位与价值**

身份注册表是 ERC-8004 的基础模块，负责将链下或链上的主体（如个人、机构、Agent 智能体）与唯一的链上身份标识绑定，形成不可篡改的 “数字身份证”。其核心价值在于解决 “链上地址匿名性” 与 “主体身份真实性” 的矛盾 —— 通过标准化的身份注册流程，让每个参与链上活动的主体都有可追溯、可验证的身份标识，避免匿名地址带来的欺诈、恶意攻击等风险。

**2\. 关键数据结构与功能**

-   **身份标识（Identity ID）**：每个注册主体的唯一标识符，通常由智能合约根据主体提交的基础信息（如公钥、链下认证凭证哈希等）生成，具备不可重复性与唯一性。
    
-   **身份元数据（Identity Metadata）**：存储主体的核心信息，包括但不限于：主体类型（个人 / 机构 / Agent）、基础信息哈希（如个人姓名与身份证号的哈希、机构名称与营业执照号的哈希）、关联地址列表（该身份绑定的所有以太坊地址）、身份状态（激活 / 冻结 / 注销）等。元数据通常以 IPFS 哈希形式存储在链上，既保证数据不可篡改，又避免链上存储成本过高。
    
-   **核心功能函数**：
    
-   `registerIdentity(bytes calldata metadataHash, address[] calldata associatedAddresses)`：主体提交身份元数据哈希与关联地址，发起身份注册请求；智能合约会验证请求的合法性（如关联地址签名授权），通过后生成 Identity ID 并记录身份信息。
    
-   `updateIdentityMetadata(bytes calldata newMetadataHash)`：当主体身份信息发生变更（如新增关联地址、更新基础信息）时，可提交新的元数据哈希，更新链上记录，同时保留历史元数据哈希，实现身份信息的可追溯。
    
-   `freezeIdentity(uint256 identityId)`：当身份存在异常（如关联地址被盗、身份信息造假被举报）时，经授权的管理员或主体自身可调用该函数冻结身份，冻结期间该身份无法参与需要身份验证的链上活动，保障系统安全。
    

**（二）声誉注册表（Reputation Registry）：主体可信度的 “量化标尺”**

**1\. 核心定位与价值**

声誉注册表是基于身份注册表的延伸模块，负责记录主体在链上活动中的行为表现，并将其转化为可量化、可比较的声誉分数或等级，成为评估主体可信度的 “量化标尺”。在 Agent 经济中，Agent 间的协作、任务分配、资源交易等场景均需依赖对方的声誉 —— 例如，一个声誉分数高的 Agent 更易获得任务委托，而声誉分数低的 Agent 可能被限制参与高价值活动，因此声誉注册表是构建 Agent 间信任协作体系的核心支撑。

**2\. 声誉维度与计算逻辑**

-   **声誉维度设计**：ERC-8004 并未强制规定具体的声誉维度，而是提供了标准化的框架供开发者扩展，常见的声誉维度包括：
    
-   履约维度：如 Agent 接受任务后是否按时完成、完成质量是否达标（可通过任务发起方的反馈或链上结果验证记录）；
    
-   合规维度：是否存在违反链上规则的行为（如恶意取消任务、提交虚假结果）；
    
-   协作维度：与其他 Agent 协作时的响应速度、沟通效率、合作成功率等。
    
-   **声誉计算逻辑**：
    
-   基础分数初始值：主体完成身份注册后，通常会获得一个基础声誉分数（如 100 分），作为声誉积累的起点；
    
-   行为影响因子：不同行为对声誉分数的影响不同，例如 “成功完成高价值任务” 可能增加 10-20 分，“恶意违约” 可能扣除 30-50 分，具体影响因子可由社区治理或应用方根据场景定义；
    
-   时间衰减机制：为保证声誉的时效性，声誉分数会随时间自然衰减（如每月衰减 5%），鼓励主体持续保持良好行为以维持高声誉；
    
-   链上记录与不可篡改性：每次声誉变更（加分 / 扣分）都会记录在链上，包括变更原因、操作主体（如任务发起方、系统管理员）、变更时间等信息，确保声誉记录可追溯、不可篡改。
    

**3\. 核心功能函数**

-   `recordReputation(uint256 identityId, int256 scoreChange, string calldata reason, address operator)`：授权主体（如任务发起方、系统）为特定 Identity ID 记录声誉分数变更，需提交分数变更值（正数为加分，负数为扣分）、变更原因（如 “完成 XX 任务”“恶意违约 XX 任务”）与操作主体地址，智能合约验证授权后更新声誉分数并记录变更日志。
    
-   `getReputationScore(uint256 identityId)`：查询特定 Identity ID 的当前声誉分数，返回分数值与最近一次更新时间，方便其他主体快速评估可信度。
    
-   `getReputationHistory(uint256 identityId, uint256 startIndex, uint256 endIndex)`：查询特定 Identity ID 的声誉变更历史，支持按索引范围筛选，便于深入了解主体的行为记录。
    

**（三）验证注册表（Verification Registry）：身份与声誉的 “信任背书”**

**1\. 核心定位与价值**

验证注册表是为身份信息与声誉记录提供 “信任背书” 的模块，负责记录第三方验证机构（如认证服务商、监管机构、知名企业）对主体身份真实性、声誉事件真实性的验证结果。其核心价值在于提升身份与声誉的可信度 —— 当主体的身份信息或声誉事件经过权威第三方验证后，其他主体会更信任该信息，减少信息造假带来的风险，尤其在金融、医疗等对可信度要求极高的场景中至关重要。

**2\. 验证类型与验证流程**

-   **验证类型**：
    
-   身份验证：验证主体提交的身份元数据是否真实（如验证个人身份证信息、机构营业执照信息）；
    
-   声誉事件验证：验证声誉注册表中记录的行为事件是否真实（如验证 Agent 是否确实完成了某任务、是否存在违约行为）。
    
-   **验证流程**：
    

NaN. 主体或系统发起验证请求：提交待验证的 Identity ID、待验证信息类型（身份 / 声誉事件）、相关证明材料哈希（如身份证扫描件哈希、任务完成凭证哈希）；

NaN. 第三方验证机构接收请求：验证机构通过链下渠道核对证明材料的真实性（如与官方数据库比对身份证信息、查看任务链上执行记录）；

NaN. 验证结果上链：验证机构完成验证后，调用智能合约将验证结果（通过 / 不通过）、验证机构地址、验证时间、验证备注等信息记录在链上；

NaN. 验证结果查询：其他主体可查询特定 Identity ID 的验证记录，作为信任评估的重要参考。
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->


参加了第一次课程会议

了解ERC-8004基本概念，尝试使用
<!-- DAILY_CHECKIN_2025-10-16_END -->
<!-- Content_END -->
