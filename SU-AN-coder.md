---
timezone: UTC+8
---

# AN SU

**GitHub ID:** SU-AN-coder

**Telegram:** @AN_SU

## Self-introduction

I am a college student currently studying, aiming to become a DePIN engineer. I have a strong interest in the Ethereum architecture. Fellow enthusiasts are welcome to connect with me! 😊

## Notes
<!-- Content_START -->
# 2025-10-21
<!-- DAILY_CHECKIN_2025-10-21_START -->
# **EIP-3009与x402协议的集成，是如何构建无Gas支付的AI代理服务？**

## **EIP-3009 核心机制分析**

### **技术架构原理**

![屏幕截图_21-10-2025_184640_.jpeg](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-21-1761043658153-_____21-10-2025_184640_.jpeg)

### **EIP-3009 无Gas支付实现**

solidity

```
// EIP-3009 核心接口
interface IEIP3009 {
    event AuthorizationUsed(address indexed authorizer, bytes32 indexed nonce);
    event TransferWithAuthorization(
        address indexed from,
        address indexed to,
        uint256 value,
        bytes32 indexed nonce,
        uint256 validAfter,
        uint256 validBefore
    );
    
    function transferWithAuthorization(
        address from,
        address to,
        uint256 value,
        uint256 validAfter,
        uint256 validBefore,
        bytes32 nonce,
        uint8 v,
        bytes32 r,
        bytes32 s
    ) external;
    
    function receiveWithAuthorization(
        address from,
        address to,
        uint256 value,
        uint256 validAfter,
        uint256 validBefore,
        bytes32 nonce,
        uint8 v,
        bytes32 r,
        bytes32 s
    ) external;
}
```

**关键优势：**

-   **Gas抽象**: 用户无需持有原生代币支付Gas费
    
-   **单步交易**: 无需先approve再transfer的两步操作
    
-   **批量处理**: 促进者可批量处理多个支付请求
    
-   **过期控制**: 通过validAfter/validBefore控制授权有效期
    

## **自动化结算系统设计**

### **支付授权流程**

javascript

```
class AutomatedPaymentSettlement {
    constructor(provider, tokenAddress, facilitator) {
        this.provider = provider;
        this.token = new ethers.Contract(tokenAddress, EIP3009_ABI, provider);
        this.facilitator = facilitator;
        this.paymentRegistry = new Map();
    }
    
    /**
     * 创建支付授权
     */
    async createPaymentAuthorization(params) {
        const {
            from,          // 支付方地址
            to,            // 收款方地址  
            value,         // 支付金额（wei）
            validDuration = 3600, // 授权有效期（秒）
            resourceId,    // 资源标识符
            metadata = {}  // 附加元数据
        } = params;
        
        // 生成唯一nonce
        const nonce = await this.generateNonce(from, resourceId);
        
        // 设置时间窗口
        const validAfter = Math.floor(Date.now() / 1000);
        const validBefore = validAfter + validDuration;
        
        // 构造类型化数据签名
        const domain = {
            name: await this.token.name(),
            version: await this.token.version(),
            chainId: await this.provider.getChainId(),
            verifyingContract: this.token.address
        };
        
        const types = {
            TransferWithAuthorization: [
                { name: 'from', type: 'address' },
                { name: 'to', type: 'address' },
                { name: 'value', type: 'uint256' },
                { name: 'validAfter', type: 'uint256' },
                { name: 'validBefore', type: 'uint256' },
                { name: 'nonce', type: 'bytes32' }
            ]
        };
        
        const message = {
            from,
            to, 
            value,
            validAfter,
            validBefore,
            nonce
        };
        
        return {
            domain,
            types,
            message,
            nonce,
            validAfter, 
            validBefore
        };
    }
    
    /**
     * 执行支付结算
     */
    async executePayment(authorization, signature) {
        try {
            const { domain, types, message } = authorization;
            const { v, r, s } = signature;
            
            // 验证签名有效性
            const recoveredAddress = ethers.utils.verifyTypedData(
                domain, types, message, { v, r, s }
            );
            
            if (recoveredAddress.toLowerCase() !== message.from.toLowerCase()) {
                throw new Error('Invalid signature');
            }
            
            // 通过促进者提交支付
            const txResponse = await this.facilitator.submitPayment({
                token: this.token.address,
                from: message.from,
                to: message.to,
                value: message.value,
                validAfter: message.validAfter,
                validBefore: message.validBefore,
                nonce: message.nonce,
                v, r, s
            });
            
            // 等待交易确认
            const receipt = await txResponse.wait();
            
            // 验证支付事件
            const transferEvent = receipt.events?.find(
                e => e.event === 'TransferWithAuthorization'
            );
            
            if (!transferEvent) {
                throw new Error('Payment event not found');
            }
            
            // 记录支付状态
            this.paymentRegistry.set(message.nonce, {
                status: 'completed',
                transactionHash: receipt.transactionHash,
                blockNumber: receipt.blockNumber,
                timestamp: Date.now()
            });
            
            return {
                success: true,
                paymentReference: message.nonce,
                transactionHash: receipt.transactionHash
            };
            
        } catch (error) {
            console.error('Payment execution failed:', error);
            return {
                success: false,
                error: error.message
            };
        }
    }
}
```

### **资源访问控制集成**

javascript

```
class ResourceAccessController {
    constructor(paymentVerifier, pricingEngine) {
        this.verifier = paymentVerifier;
        this.pricing = pricingEngine;
        this.accessGrants = new Map();
        this.resourcePolicies = new Map();
    }
    
    /**
     * 定义资源访问策略
     */
    defineResourcePolicy(resourceId, policy) {
        this.resourcePolicies.set(resourceId, {
            requiresPayment: policy.requiresPayment || false,
            price: policy.price || 0,
            currency: policy.currency || 'USDC',
            accessDuration: policy.accessDuration || 3600000, // 1小时
            maxUsage: policy.maxUsage || 1,
            ...policy
        });
    }
    
    /**
     * 检查并授权资源访问
     */
    async checkAndGrantAccess(resourceId, userAddress, paymentProof = null) {
        const policy = this.resourcePolicies.get(resourceId);
        
        if (!policy) {
            return { granted: true, reason: 'no_policy_defined' };
        }
        
        if (!policy.requiresPayment) {
            return { granted: true, reason: 'free_resource' };
        }
        
        // 检查现有访问授权
        const userAccessKey = `${userAddress}-${resourceId}`;
        const existingGrant = this.accessGrants.get(userAccessKey);
        
        if (existingGrant) {
            if (existingGrant.expiresAt > Date.now() && 
                existingGrant.usageCount < policy.maxUsage) {
                
                existingGrant.usageCount++;
                return { 
                    granted: true, 
                    reason: 'existing_grant',
                    grant: existingGrant
                };
            } else {
                // 授权已过期或达到使用上限
                this.accessGrants.delete(userAccessKey);
            }
        }
        
        // 需要支付验证
        if (paymentProof) {
            const verification = await this.verifier.verifyPaymentProof(
                paymentProof, 
                resourceId, 
                userAddress,
                policy.price
            );
            
            if (verification.valid) {
                const grant = this.grantAccess(
                    userAddress, 
                    resourceId, 
                    policy
                );
                
                return {
                    granted: true,
                    reason: 'payment_verified',
                    grant,
                    paymentDetails: verification
                };
            }
        }
        
        // 需要支付
        return {
            granted: false,
            reason: 'payment_required',
            paymentRequired: {
                resourceId,
                amount: policy.price,
                currency: policy.currency,
                accessDuration: policy.accessDuration,
                validAfter: Math.floor(Date.now() / 1000),
                validBefore: Math.floor(Date.now() / 1000) + 3600 // 1小时有效期
            }
        };
    }
    
    /**
     * 授予资源访问权限
     */
    grantAccess(userAddress, resourceId, policy) {
        const userAccessKey = `${userAddress}-${resourceId}`;
        
        const grant = {
            userAddress,
            resourceId,
            grantedAt: Date.now(),
            expiresAt: Date.now() + policy.accessDuration,
            usageCount: 1,
            maxUsage: policy.maxUsage,
            policy
        };
        
        this.accessGrants.set(userAccessKey, grant);
        
        // 设置自动过期清理
        setTimeout(() => {
            this.revokeAccess(userAddress, resourceId);
        }, policy.accessDuration);
        
        return grant;
    }
}
```

## **增强型x402 MCP服务器**

### **系统架构**

![屏幕截图_21-10-2025_18472_.jpeg](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-21-1761043694988-_____21-10-2025_18472_.jpeg)

### **完整MCP服务器实现**

javascript

```
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { privateKeyToAccount } from "viem/accounts";
import { createWalletClient, http, parseUnits } from "viem";
import { baseSepolia } from "viem/chains";
import { withPaymentInterceptor } from "x402-axios";
import { ResourceAccessController } from './resource-access.js';
import { AutomatedPaymentSettlement } from './payment-settlement.js';

class EnhancedX402MCPServer {
    constructor(config) {
        this.config = config;
        this.initializeServer();
        this.initializePaymentSystem();
        this.setupTools();
        this.resourceCache = new Map();
    }
    
    initializeServer() {
        this.server = new McpServer({
            name: this.config.name || "x402-enhanced-mcp-server",
            version: this.config.version || "2.0.0",
            capabilities: {
                resources: {},
                tools: {}
            }
        });
        
        // 初始化钱包客户端
        this.wallet = createWalletClient({
            account: privateKeyToAccount(this.config.privateKey),
            chain: baseSepolia,
            transport: http(this.config.rpcUrl)
        });
        
        // 初始化HTTP客户端（集成x402拦截器）
        this.httpClient = withPaymentInterceptor(
            axios.create({
                timeout: 30000,
                maxRedirects: 0
            }), 
            this.wallet.account,
            {
                facilitatorUrl: this.config.facilitatorUrl,
                onPaymentRequired: this.handlePaymentRequired.bind(this),
                onPaymentCompleted: this.handlePaymentCompleted.bind(this)
            }
        );
    }
    
    initializePaymentSystem() {
        // 初始化支付结算系统
        this.paymentSettlement = new AutomatedPaymentSettlement(
            this.config.provider,
            this.config.usdcAddress,
            this.config.facilitator
        );
        
        // 初始化资源访问控制器
        this.accessController = new ResourceAccessController(
            this.paymentSettlement,
            this.config.pricingEngine
        );
        
        // 预定义资源策略
        this.defineResourcePolicies();
    }
    
    defineResourcePolicies() {
        // 定义各种资源的访问策略
        this.accessController.defineResourcePolicy('weather-api', {
            requiresPayment: true,
            price: parseUnits('0.01', 6), // 0.01 USDC
            currency: 'USDC',
            accessDuration: 3600000, // 1小时
            maxUsage: 10 // 最多使用10次
        });
        
        this.accessController.defineResourcePolicy('financial-data', {
            requiresPayment: true,
            price: parseUnits('0.05', 6), // 0.05 USDC
            currency: 'USDC', 
            accessDuration: 1800000, // 30分钟
            maxUsage: 5
        });
        
        this.accessController.defineResourcePolicy('ai-inference', {
            requiresPayment: true,
            price: parseUnits('0.10', 6), // 0.10 USDC
            currency: 'USDC',
            accessDuration: 7200000, // 2小时
            maxUsage: 3
        });
    }
    
    setupTools() {
        // 注册获取付费数据的工具
        this.server.tool(
            "fetch-paid-data",
            "从付费API获取数据，自动处理支付流程",
            {
                endpoint: {
                    type: "string", 
                    description: "API端点路径，例如 /weather 或 /financial"
                },
                params: {
                    type: "object",
                    description: "请求参数"
                },
                resourceType: {
                    type: "string",
                    description: "资源类型：weather-api, financial-data, ai-inference",
                    enum: ["weather-api", "financial-data", "ai-inference"]
                }
            },
            this.handlePaidDataRequest.bind(this)
        );
        
        // 注册支付状态查询工具
        this.server.tool(
            "check-payment-status", 
            "查询特定支付的链上状态",
            {
                paymentReference: {
                    type: "string",
                    description: "支付参考ID"
                }
            },
            this.checkPaymentStatus.bind(this)
        );
        
        // 注册可用API列表工具
        this.server.tool(
            "list-available-apis",
            "获取所有可用的付费API及其价格信息",
            {},
            this.listAvailableAPIs.bind(this)
        );
        
        // 注册资源访问状态工具
        this.server.tool(
            "check-access-status",
            "检查对特定资源的当前访问状态",
            {
                resourceType: {
                    type: "string", 
                    description: "资源类型"
                }
            },
            this.checkAccessStatus.bind(this)
        );
    }
    
    async handlePaidDataRequest({ endpoint, params, resourceType }) {
        try {
            const userAddress = this.wallet.account.address;
            
            // 1. 检查资源访问权限
            const accessCheck = await this.accessController.checkAndGrantAccess(
                resourceType, 
                userAddress
            );
            
            if (!accessCheck.granted) {
                // 需要支付 - 构建支付请求
                const paymentRequest = await this.buildPaymentRequest(
                    accessCheck.paymentRequired,
                    userAddress
                );
                
                return {
                    content: [{
                        type: "text",
                        text: `访问此资源需要支付。\n` +
                              `资源: ${resourceType}\n` +
                              `价格: ${ethers.utils.formatUnits(paymentRequest.amount, 6)} USDC\n` +
                              `支付参考: ${paymentRequest.paymentReference}\n\n` +
                              `请使用支付工具完成支付后重试。`
                    }],
                    isPaymentRequired: true,
                    paymentRequest
                };
            }
            
            // 2. 有访问权限 - 获取数据
            const cacheKey = this.generateCacheKey(endpoint, params, resourceType);
            const cachedData = this.getCachedData(cacheKey);
            
            if (cachedData) {
                return {
                    content: [{
                        type: "text", 
                        text: `缓存数据（${new Date(cachedData.timestamp).toLocaleString()}）:\n` +
                              JSON.stringify(cachedData.data, null, 2)
                    }]
                };
            }
            
            // 3. 发送API请求
            const response = await this.httpClient.get(endpoint, { params });
            
            // 4. 缓存响应数据
            this.cacheData(cacheKey, response.data);
            
            // 5. 更新使用统计
            await this.updateUsageStatistics(userAddress, resourceType);
            
            return {
                content: [{
                    type: "text",
                    text: `数据获取成功:\n${JSON.stringify(response.data, null, 2)}`
                }]
            };
            
        } catch (error) {
            return this.handleRequestError(error);
        }
    }
    
    async buildPaymentRequest(paymentRequired, userAddress) {
        const authorization = await this.paymentSettlement.createPaymentAuthorization({
            from: userAddress,
            to: this.config.merchantAddress,
            value: paymentRequired.amount,
            validDuration: 3600,
            resourceId: paymentRequired.resourceId,
            metadata: {
                resourceType: paymentRequired.resourceType,
                accessDuration: paymentRequired.accessDuration
            }
        });
        
        return {
            amount: paymentRequired.amount,
            currency: paymentRequired.currency,
            paymentReference: authorization.nonce,
            authorization,
            validUntil: authorization.validBefore
        };
    }
    
    async checkPaymentStatus({ paymentReference }) {
        try {
            const status = await this.paymentSettlement.getPaymentStatus(paymentReference);
            
            let statusText = '';
            if (status.status === 'completed') {
                statusText = `✅ 支付已完成\n交易哈希: ${status.transactionHash}\n区块: ${status.blockNumber}`;
            } else if (status.status === 'pending') {
                statusText = `⏳ 支付处理中\n请稍后查询`;
            } else {
                statusText = `❌ 支付未找到或已失败`;
            }
            
            return {
                content: [{
                    type: "text",
                    text: statusText
                }]
            };
        } catch (error) {
            return {
                content: [{
                    type: "text", 
                    text: `支付状态查询失败: ${error.message}`
                }]
            };
        }
    }
    
    async listAvailableAPIs() {
        const apis = [
            {
                name: "天气数据API",
                endpoint: "/weather",
                resourceType: "weather-api",
                description: "获取实时天气信息和预报",
                price: "0.01 USDC",
                accessDuration: "1小时",
                maxUsage: "10次"
            },
            {
                name: "金融数据API",
                endpoint: "/financial", 
                resourceType: "financial-data",
                description: "获取股票价格、市场数据",
                price: "0.05 USDC",
                accessDuration: "30分钟", 
                maxUsage: "5次"
            },
            {
                name: "AI模型推理",
                endpoint: "/inference",
                resourceType: "ai-inference",
                description: "运行大型语言模型推理",
                price: "0.10 USDC", 
                accessDuration: "2小时",
                maxUsage: "3次"
            }
        ];
        
        const apiList = apis.map(api => 
            `📊 ${api.name}\n` +
            `  描述: ${api.description}\n` +
            `  价格: ${api.price}\n` +
            `  访问时长: ${api.accessDuration}\n` +
            `  最大使用: ${api.maxUsage}\n` +
            `  资源类型: ${api.resourceType}\n`
        ).join('\n');
        
        return {
            content: [{
                type: "text",
                text: `可用的付费API:\n\n${apiList}`
            }]
        };
    }
    
    // 缓存管理方法
    generateCacheKey(endpoint, params, resourceType) {
        return `${resourceType}-${endpoint}-${JSON.stringify(params)}`;
    }
    
    getCachedData(cacheKey) {
        const cached = this.resourceCache.get(cacheKey);
        if (cached && Date.now() - cached.timestamp < 300000) { // 5分钟缓存
            return cached;
        }
        return null;
    }
    
    cacheData(cacheKey, data) {
        this.resourceCache.set(cacheKey, {
            data,
            timestamp: Date.now()
        });
    }
    
    async start() {
        const transport = new StdioServerTransport();
        await this.server.connect(transport);
        console.log('🚀 增强型 x402 MCP 服务器已启动');
    }
}
```

### **配置与部署示例**

javascript

```
// 服务器配置
const serverConfig = {
    name: "AI-Assistant-X402-Server",
    version: "2.1.0",
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL || "https://base-sepolia.g.alchemy.com/v2/your-key",
    facilitatorUrl: "https://x402.org/facilitator",
    usdcAddress: "0x036CbD53842c5426634e7929541eC2318f3dCF7e", // Base Sepolia USDC
    merchantAddress: "0xYourMerchantAddress",
    
    // 资源定价配置
    pricingEngine: {
        baseCurrency: 'USDC',
        defaultAccessDuration: 3600000, // 1小时
        dynamicPricing: true
    },
    
    // 缓存配置
    cache: {
        enabled: true,
        ttl: 300000, // 5分钟
        maxSize: 1000
    },
    
    // 监控配置
    monitoring: {
        enabled: true,
        logLevel: 'info',
        metrics: true
    }
};

// Claude Desktop MCP 配置
const claudeConfig = {
    "mcpServers": {
        "x402-enhanced": {
            "command": "node",
            "args": ["dist/server.js"],
            "env": {
                "PRIVATE_KEY": "0xYourPrivateKey",
                "RPC_URL": "https://base-sepolia.g.alchemy.com/v2/your-key",
                "FACILITATOR_URL": "https://x402.org/facilitator"
            }
        }
    }
};
```

## **核心工作流程**

### **完整支付与访问流程**

![屏幕截图_21-10-2025_184717_.jpeg](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-21-1761043715854-_____21-10-2025_184717_.jpeg)

## **技术优势总结**

1.  **无缝支付体验**: EIP-3009实现真正的无Gas支付，用户只需签名授权
    
2.  **自动化结算**: 支付成功后自动授权资源访问，无需人工干预
    
3.  **灵活定价**: 支持按次付费、时段授权、用量限制等多种模式
    
4.  **状态持久化**: 完整的支付状态跟踪和访问授权管理
    
5.  **缓存优化**: 智能缓存减少重复支付，提升用户体验
    
6.  **错误恢复**: 完善的错误处理和重试机制
    
7.  **多网络支持**: 通过促进者抽象支持多链环境
<!-- DAILY_CHECKIN_2025-10-21_END -->

# 2025-10-20
<!-- DAILY_CHECKIN_2025-10-20_START -->

## **去中心化AI模型市场演示代理**

### **核心概念**

构建一个允许AI代理发布、发现和付费使用机器学习模型的市场，集成A2A发现、AP2支付和x402 API支付墙

### **1\. 项目架构**

solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

// 自定义模型市场合约
contract ModelMarketplace {
    event ModelPublished(
        uint256 indexed agentId,
        string modelId,
        string modelType,
        uint256 price,
        string endpoint,
        string description
    );
    
    event ModelPurchased(
        uint256 indexed buyerAgentId,
        uint256 indexed sellerAgentId,
        string modelId,
        uint256 price,
        bytes32 paymentReference
    );
    
    struct ModelListing {
        uint256 agentId;
        string modelId;
        string modelType; // "llama2", "whisper", "stable-diffusion"
        uint256 price;
        string endpoint;
        bool active;
    }
    
    mapping(string => ModelListing) public models;
    string[] public modelIds;
    
    IReputationRegistry public reputationRegistry;
    
    constructor(address _reputationRegistry) {
        reputationRegistry = IReputationRegistry(_reputationRegistry);
    }
    
    function publishModel(
        string memory modelId,
        string memory modelType,
        uint256 price,
        string memory endpoint,
        string memory description
    ) external {
        // 获取调用者代理ID（简化实现）
        uint256 agentId = getCallerAgentId();
        
        models[modelId] = ModelListing({
            agentId: agentId,
            modelId: modelId,
            modelType: modelType,
            price: price,
            endpoint: endpoint,
            active: true
        });
        
        modelIds.push(modelId);
        
        emit ModelPublished(agentId, modelId, modelType, price, endpoint, description);
    }
}
```

### **2\. 自定义代理元数据配置**

json

```
{
  "name": "AI-Model-Marketplace-Agent",
  "description": "Decentralized marketplace for AI model inference services",
  "version": "1.0.0",
  "endpoints": {
    "modelDiscovery": "https://marketplace-agent.com/api/models",
    "inference": "https://marketplace-agent.com/api/inference",
    "payment": "https://marketplace-agent.com/api/payment"
  },
  "supportedModels": ["llama2-7b", "whisper-large", "stable-diffusion-xl"],
  "pricing": "dynamic",
  "agentWallet": "0x742d35Cc6634C0532925a3b8D...",
  "metadata": {
    "serviceLevel": "99.9%",
    "maxConcurrentRequests": 100,
    "avgResponseTime": "2.5s"
  }
}
```

### **3\. x402 支付墙集成**

javascript

```
// 模型推理API - 集成x402支付
const express = require('express');
const app = express();

app.post('/api/inference/:modelId', async (req, res) => {
    const { modelId } = req.params;
    const { input } = req.body;
    
    // 获取模型定价
    const modelPrice = await getModelPrice(modelId);
    const paymentRef = generatePaymentReference();
    
    // 检查支付状态
    const isPaid = await checkPaymentStatus(paymentRef);
    
    if (!isPaid) {
        // 返回402支付要求
        return res.status(402).set({
            'Pay': `AP2; address="${process.env.AGENT_WALLET}"; value="${modelPrice}"; chain-id=1; ref="${paymentRef}"`,
            'Pay-Link': `<https://${req.hostname}/api/pay/${paymentRef}>; rel="payment"`,
            'Model-Id': modelId,
            'Price-Wei': modelPrice.toString()
        }).json({
            error: "Payment required",
            modelId,
            price: modelPrice,
            paymentReference: paymentRef
        });
    }
    
    // 执行模型推理
    try {
        const result = await runModelInference(modelId, input);
        res.json({
            success: true,
            modelId,
            result,
            usage: { tokens: result.usage }
        });
    } catch (error) {
        res.status(500).json({ error: "Inference failed" });
    }
});
```

### **4\. 增强信誉事件系统**

solidity

```
// 增强的信誉事件发射器
contract ModelMarketReputation {
    event ModelQualityFeedback(
        uint256 indexed agentId,
        address indexed rater,
        string modelId,
        uint8 inferenceQuality,
        uint8 responseTime,
        uint8 accuracy,
        string feedbackUri,
        uint256 timestamp
    );
    
    event ServiceLevelViolation(
        uint256 indexed agentId,
        string modelId,
        uint256 expectedResponseTime,
        uint256 actualResponseTime,
        uint256 blockNumber
    );
    
    function submitModelFeedback(
        uint256 agentId,
        string memory modelId,
        uint8 inferenceQuality,
        uint8 responseTime,
        uint8 accuracy,
        string memory feedbackUri
    ) external {
        // 提交到标准信誉注册表
        reputationRegistry.giveFeedback(
            agentId,
            calculateOverallScore(inferenceQuality, responseTime, accuracy),
            "model:quality",
            "model:performance",
            feedbackUri,
            keccak256(abi.encodePacked(modelId))
        );
        
        // 发射自定义模型质量事件
        emit ModelQualityFeedback(
            agentId,
            msg.sender,
            modelId,
            inferenceQuality,
            responseTime,
            accuracy,
            feedbackUri,
            block.timestamp
        );
    }
    
    function reportSlowResponse(
        uint256 agentId,
        string memory modelId,
        uint256 expectedMs,
        uint256 actualMs
    ) external {
        emit ServiceLevelViolation(
            agentId,
            modelId,
            expectedMs,
            actualMs,
            block.number
        );
    }
    
    function calculateOverallScore(
        uint8 quality,
        uint8 responseTime,
        uint8 accuracy
    ) internal pure returns (uint8) {
        return (quality + responseTime + accuracy) / 3;
    }
}
```

### **5\. 模型发现与验证工作流**

javascript

```
// 模型发现API
app.get('/api/models', async (req, res) => {
    const { type, minReputation, maxPrice } = req.query;
    
    // 从链上获取可用模型
    const availableModels = await getAvailableModelsFromChain();
    
    // 过滤基于查询参数
    const filteredModels = await Promise.all(
        availableModels.map(async model => {
            const reputation = await getAgentReputation(model.agentId);
            const meetsReputation = !minReputation || reputation >= minReputation;
            const meetsPrice = !maxPrice || model.price <= maxPrice;
            const meetsType = !type || model.modelType === type;
            
            return meetsReputation && meetsPrice && meetsType ? model : null;
        })
    );
    
    const result = filteredModels.filter(Boolean);
    
    res.json({
        models: result,
        count: result.length,
        query: { type, minReputation, maxPrice }
    });
});

// 验证工作流集成
async function verifyModelProvider(agentId) {
    // 调用验证注册表
    const verification = await verificationRegistry.verify(
        agentId,
        "tee", // TEE证明验证
        "0x" // 验证数据
    );
    
    if (ververified) {
        // 增强信誉评分
        await reputationRegistry.giveFeedback(
            agentId,
            95, // 验证奖励分数
            "capability:verified",
            "security:tee",
            "ipfs://QmVerificationProof",
            keccak256(abi.encodePacked("tee-verified"))
        );
    }
    
    return verification.verified;
}
```

### **6\. 部署和测试脚本**

javascript

```
// scripts/deploy-marketplace.js
async function main() {
    // 部署基础注册表
    const agentRegistry = await deployAgentRegistry();
    const reputationRegistry = await deployReputationRegistry();
    
    // 部署自定义市场合约
    const marketplace = await deployModelMarketplace(reputationRegistry.address);
    
    // 注册演示代理
    await registerDemoAgents(agentRegistry);
    
    // 发布测试模型
    await publishDemoModels(marketplace);
    
    console.log("🎯 模型市场部署完成");
    console.log("Agent Registry:", agentRegistry.address);
    console.log("Marketplace:", marketplace.address);
    
    return { marketplace, agentRegistry, reputationRegistry };
}

// 测试支付流程
async function testModelPurchase() {
    const modelId = "llama2-7b-chat";
    const input = "Explain blockchain to a beginner";
    
    // 1. 发现模型
    const models = await fetch('/api/models?type=llama2').then(r => r.json());
    
    // 2. 请求推理（应该收到402）
    const response = await fetch(`/api/inference/${modelId}`, {
        method: 'POST',
        body: JSON.stringify({ input })
    });
    
    if (response.status === 402) {
        const payHeader = response.headers.get('Pay');
        const paymentParams = parsePayHeader(payHeader);
        
        // 3. 支付
        const tx = await makeAP2Payment(paymentParams);
        
        // 4. 重新请求（带支付证明）
        const finalResponse = await fetch(`/api/inference/${modelId}`, {
            method: 'POST',
            headers: { 'Payment-Proof': paymentParams.ref },
            body: JSON.stringify({ input })
        });
        
        const result = await finalResponse.json();
        console.log("推理结果:", result);
        
        // 5. 提交反馈
        await submitFeedback(modelId, 95, 90, 92);
    }
}
```

### **7\. 检查清单**

**基础设置**

-   克隆并配置ERC-8004示例仓库
    
-   启动本地Anvil链并部署注册表
    
-   配置自定义代理元数据
    

**核心功能**

-   实现模型市场智能合约
    
-   集成x402支付墙到推理API
    
-   部署自定义信誉事件系统
    
-   实现模型发现服务
    

**高级特性**

-   TEE验证集成
    
-   服务质量监控
    
-   动态信誉评分
    
-   支付证明验证
    

**测试验证**

-   模型发布和发现流程
    
-   x402支付完整流程
    
-   信誉反馈系统
    
-   区块链审计跟踪生成
<!-- DAILY_CHECKIN_2025-10-20_END -->

# 2025-10-19
<!-- DAILY_CHECKIN_2025-10-19_START -->


## **自主代理经济协议栈：A2A/AP2/x402协议解析**

### **1\. A2A协议：代理间身份与通信的信任基盘**

A2A协议的核心是为去中心化环境中的AI代理建立一个可互操作的身份、发现与安全通信层。它不依赖于任何中心化的控制机构。

-   **去中心化身份**
    
    -   **格式**：代理身份通常遵循W3C去中心化标识符规范或类似的基于公钥基础设施的方法。例如：`did:pkh:eip155:1:0x1a2b3c...`。该DID通过密码学方式与一个区块链账户（EOA或智能合约钱包）绑定。
        
    -   **解析**：身份解析器通过相应的DID方法，将DID解析为其对应的DID文档，其中包含用于验证的控制器的公钥、服务端点等信息。
        
-   **代理描述符**
    
    -   这是一个公开的JSON-LD文件，充当代理的“数字名片”和“服务清单”。
        
    -   **关键字段**:
        
        -   `@context`, `id`: 遵循JSON-LD标准，`id`即为代理的DID。
            
        -   `publicKey`: 用于验证请求签名。
            
        -   `service`: 定义代理提供的服务集合。每个服务应明确其`type`（如`A2AEndpoint`，`MarketDataService`）、`serviceEndpoint`（URL）和`capabilities`（描述输入输出格式、支付要求等）。
            
    -   **完整性**：描述符本身应由代理的私钥签名（例如使用`LinkedDataSignatures`），确保其内容在传输过程中未被篡改。
        
-   **安全握手流程**
    
    1.  **请求**：发起方代理（Alice）向目标代理（Bob）的`serviceEndpoint`发送一个结构化的HTTP请求。请求头应包含：
        
        -   `Authorization: Bearer <A2A-JWT>`
            
        -   JWT的Payload部分需包含Alice的DID、Bob的DID、请求的操作、随机数和时间戳。
            
    2.  **挑战**：Bob返回`401 Unauthorized`，并提供一个高强度的随机数。
        
    3.  **签名与重试**：Alice使用自己的私钥，按照EIP-712或类似标准，对包含原始请求参数和随机数的数据进行签名。她随后重试请求，并在头中附带签名（如`Signature: <EIP-712-signature>`）。
        
    4.  **验证与执行**：Bob使用从Alice的DID文档中获取的公钥验证签名。验证通过后，执行请求的操作。
        

**核心价值**：A2A建立了代理交互的**身份层和通信层**，实现了端到端的身份验证与消息完整性，是构建信任的基石。

* * *

### **2\. AP2协议：支付意图的标准化协调层**

AP2并非支付协议本身，而是一个在A2A建立的安全通道内，用于协商和确认支付意图的元协议。它定义了“支付什么”和“如何确认”，而非“如何支付”。

-   **支付请求对象**  
    这是一个高度结构化的数据负载，在A2A握手后，由服务方代理返回。
    
    json
    
    ```
    {
      "@context": "https://ap2.org/schemas/v1",
      "type": "PaymentRequest",
      "paymentRequestId": "pr_abc123", // 唯一标识此次支付请求
      "description": "Stock data query for AAPL",
      "amount": {
        "currency": "USDC",
        "value": "0.10"
      },
      "destination": "0xRecipientAddress",
      "chainId": 8453,
      "fulfillmentCondition": { // 关键：支付完成的条件
        "type": "onChainTransaction",
        "asset": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
        "method": "transfer",
        "minConfirmations": 1
      },
      "callback": {
        "url": "https://service.com/ap2/fulfill", // 支付证明提交地址
        "method": "POST"
      },
      "expiresAt": "2025-...", // 请求有效期
    }
    ```
    
    -   `fulfillmentCondition`字段是AP2的精髓，它明确定义了何种链上事件（如特定ERC-20的`transfer`函数调用）被视为支付完成。
        
    -   `callback`机制将支付执行与服务的最终解锁解耦。
        
-   **支付流程与状态机**
    
    1.  `payment_required`：服务方返回AP2支付请求。
        
    2.  `payment_pending`：客户端确认支付请求，并开始执行支付（例如，通过x402协议）。
        
    3.  `payment_verified`：客户端在链上完成支付后，将交易哈希作为支付证明，通过HTTPS POST请求发送到服务方的`callback.url`。
        
    4.  `fulfilled`：服务方监听链上事件，验证该交易确实符合`fulfillmentCondition`中定义的条件。验证通过后，服务状态转为完成，并（通常通过另一个A2A调用）交付服务结果。
        

**核心价值**：AP2是**协调层**。它提供了一个与底层支付方式（x402、闪电网络等）无关的、机器可读的支付协商标准，实现了支付流程的标准化与自动化。

* * *

### **3\. x402协议：HTTP原生支付的原子性执行**

x402协议将HTTP协议与区块链支付深度融合，为Web服务提供了一个极简的、按次付费的支付执行层。它专注于解决“如何支付”的问题。

-   **HTTP 402响应**  
    响应体必须遵循严格的规范，以便客户端SDK能自动处理。
    
    json
    
    ```
    {
      "error": {
        "code": 402,
        "message": "Payment Required"
      },
      "maxAmountRequired": "0.10",
      "paymentInfo": {
        "assetType": "ERC20",
        "assetAddress": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
        "paymentAddress": "0xMerchantAddress",
        "chainId": 8453,
        "expiresAt": "2025-...",
        "nonce": "unique_nonce_123" // 防止重放攻击
      }
    }
    ```
    
-   **支付授权**  
    客户端构造的签名负载必须包含所有关键信息，并遵循EIP-712结构化签名标准。这确保了签名在钱包中可以被清晰地解析和展示，用户明确知道自己在为什么签名。
    
    typescript
    
    ```
    const domain = {
      name: 'x402 Payment Proxy',
      version: '1',
      chainId: 8453,
      verifyingContract: '0x...', // 可选，一个代理合约地址
    };
    const types = {
      Payment: [
        { name: 'maxAmount', type: 'string' },
        { name: 'assetAddress', type: 'address' },
        { name: 'paymentAddress', type: 'address' },
        { name: 'chainId', type: 'uint256' },
        { name: 'nonce', type: 'string' },
        { name: 'expiresAt', type: 'uint256' },
      ],
    };
    const value = {
      // ... 从402响应中填充的值
    };
    const signature = await wallet.signTypedData(domain, types, value);
    ```
    
-   **服务端验证与结算**
    
    -   **验证**：服务端中间件使用`ecrecover`或类似逻辑，从签名中还原出签名者的地址，并验证其是否有权访问该资源。
        
    -   **结算策略**：
        
        -   **直接广播**：中间件将已签名的交易直接广播到内存池。优点是即时，但可能因 gas 费问题失败。
            
        -   **提交-揭示**：客户端先提交交易的哈希（承诺），服务端授予临时访问权限；客户端随后揭示完整交易。这可以防止前端跑路。
            
        -   **支付通道**：对于高频场景，双方可先开设支付通道，x402请求验证的是通道内的余额证明签名，而非链上交易。
            

**核心价值**：x402是**执行层**。它提供了将任意HTTP端点转化为原子性（支付与服务交付同时成功或失败）付费端面的最简方案。

* * *

### **4\. 总结：协议栈的协同关系**

这三个协议构成了一个层次分明、职责分离的**自主代理经济协议栈**。

-   **A2A是基础**：它解决了“你是谁”和“如何安全地跟你说话”的问题，建立了代理网络中最根本的信任层。所有高级交互都构建在A2A建立的安全通道之上。
    
-   **AP2是协调**：在A2A的安全通道内，AP2解决了“这项服务需要什么条件才能解锁”的问题。它将支付意图从具体的支付方式中抽象出来，使得代理可以使用同一套语言来协商支付，无论底层是用x402、闪电网络还是其他未来出现的支付协议。
    
-   **x402是执行**：当AP2协商好支付条件后，x402提供了一个标准化的、HTTP友好的方式来**具体执行**支付。它是实现AP2中`fulfillmentCondition`的一种强大而具体的工具。
    

**数据流关系图**：

text

```
[ResearchAgent] --(A2A握手 & 服务请求)--> [ServiceAgent]
                                      |
                                      | (如需支付)
                                      V
[ResearchAgent] <--(AP2 PaymentRequest)-- [ServiceAgent]
                                      |
                                      | (切换至x402流程)
                                      V
[ResearchAgent] --(HTTP GET + 收到402)--> [ServiceAgent]
[ResearchAgent] --(HTTP GET + EIP-712签名)--> [ServiceAgent]
                                      |
                                      | (x402验证通过，执行服务)
                                      V
[ResearchAgent] <--(HTTP 200 + 服务数据)-- [ServiceAgent]
                                      |
                                      | (可选：声誉记录)
                                      V
                   [ERC-8004 Event Log on Blockchain]
```

简而言之，**A2A负责建立连接，AP2负责协商条件，x402负责完成支付**。三者协同工作，共同为实现真正自主、经济自足的AI代理经济体提供了完整的技术栈
<!-- DAILY_CHECKIN_2025-10-19_END -->

# 2025-10-18
<!-- DAILY_CHECKIN_2025-10-18_START -->



# **x402 开放支付标准笔记**

## **一、x402 是什么？**

-   定义：Coinbase 推出的**开放支付标准**，基于 HTTP 402 “Payment Required” 状态码，实现 AI 代理 / Web 服务的**自主支付**（无需人工干预）。
    
-   核心场景：API 访问、数据购买、AI 模型推理等，用 USDC 等稳定币结算，支持 “按使用付费”。
    
-   关键特点：无需 API 密钥、订阅或账户，纯 HTTP 原生集成，轻量化易开发。
    

## **二、为什么用 x402？**

传统支付（信用卡、PayPal、API 订阅）的问题：

1.  高成本：信用卡手续费 $0.30+2.9%，小额支付不划算；
    
2.  慢结算：ACH 需 1-3 天，信用卡授权后仍需数天到账；
    
3.  摩擦多：需注册账户、绑定支付方式、管理 API 密钥；
    
4.  不兼容 M2M：AI 代理无法自主完成支付，依赖人工干预；
    
5.  无小额支持：高手续费导致 $0.001 级微交易无法实现。
    

x402 的改进：

-   费用：近零（Base 链上约 $0.0001）；
    
-   结算：200ms 到账，即时确认；
    
-   无摩擦：无需账户 / API 密钥，AI 代理可自动处理；
    
-   支持微交易：最低 $0.001 付费。
    

## **三、核心工作流程**

1.  **客户端请求**：AI 代理 / 应用请求资源（如`GET /api/market-data`）；
    
2.  **服务器返回 402**：无有效支付时，返回 HTTP 402，附带支付详情（金额、收款地址、链网络）；
    
3.  **客户端重试（带支付）**：客户端生成签名支付（按 EIP-712 标准），重试请求时附加支付信息；
    
4.  **服务器验证并响应**：验证支付有效性→广播交易→返回请求的资源（如市场数据）。
    

## **四、核心代码示例**

### **1\. 服务器端：Node.js/Express 集成（关键是 x402 中间件）**

**javascript**

```javascript
// 1. 安装依赖：npm install @x402/express-middleware express
const express = require('express');
const { x402PaymentRequired } = require('@x402/express-middleware');

const app = express();

// 2. 配置x402中间件：保护需要付费的接口
app.get('/api/market-data', 
  x402PaymentRequired({
    amount: "0.10",          // 单次请求费用（单位：USDC）
    address: "0x1234...",    // 收款钱包地址
    assetAddress: "0xA0b86991C6218b36c1d19D4a2e9Eb0cE3606EB48", // USDC合约地址
    network: "base-mainnet"  // 区块链网络
  }), 
  // 3. 支付验证通过后，返回资源
  (req, res) => {
    res.json({
      marketData: { BTC: 50000, ETH: 2000 }, // 示例：付费后获取的实时数据
      timestamp: Date.now()
    });
  }
);

app.listen(3000, () => console.log("x402服务器运行在3000端口"));
```

### **2\. 402 响应的 JSON 格式（服务器返回给客户端的支付信息）**

**json**

```json
{
  "resource": "/api/market-data",       // 请求的资源路径
  "description": "实时市场数据访问需付费", // 可选：支付说明
  "maxAmountRequired": "0.10",          // 所需支付金额（USDC）
  "payTo": "0x1234...",                 // 收款地址
  "asset": "0xA0b86991C6218b36c1d19D4a2e9Eb0cE3606EB48", // 支付资产（USDC）合约地址
  "network": "base-mainnet",            // 区块链网络
  "nonce": "abc123",                    // 防重放攻击的唯一标识
  "expiresAt": 1717248000              // 支付请求过期时间戳
}
```

### **3\. 客户端代码：AI 代理处理 402 并重试支付**

**javascript**

```javascript
// 1. 安装依赖：npm install @x402/client your-wallet-connector
import { x402Client } from '@x402/client';
import { connectWallet } from 'your-wallet-connector'; // 连接钱包（如MetaMask）

async function getPaidResource() {
  // 2. 初始化客户端并连接钱包
  const client = new x402Client();
  const wallet = await connectWallet(); // 获取用户/代理的钱包（如USDC钱包）
  client.setWallet(wallet);

  try {
    // 3. 请求付费资源：客户端自动处理402重试
    const data = await client.fetch('https://api.example.com/api/market-data');
    console.log("获取到付费资源：", data);
    return data;
  } catch (error) {
    console.error("支付失败：", error.message);
  }
}

// 调用函数：AI代理自主获取付费数据
getPaidResource();
```

## **五、x402 关键优势**

1.  **低成本**：Base 链上交易费≈$0.0001，支持$0.001 级微交易；
    
2.  **快结算**：200ms 到账，无延迟，且支付不可撤销（无拒付风险）；
    
3.  **零摩擦**：无需注册账户、管理 API 密钥或订阅，AI 代理可全自动支付；
    
4.  **兼容性强**：HTTP 原生，支持任何区块链（EVM/SVM）和稳定币，适配现有 Web 服务；
    
5.  **安全**：支付签名遵循 EIP-712 标准，无需 PCI 合规（除非直接收信用卡）。
    

## **六、适用人群及其核心用例**

### **1\. 适用人群**

-   **卖家**：API 提供商、数字内容平台（如新闻 / 论文）、AI 模型服务商、云资源商；
    
-   **买家**：AI 代理（自主采购数据 / 算力）、开发者（快速访问付费 API）、普通用户（按次购买内容，如单篇论文）。
    

### **2\. 核心用例**

-   按请求付费 API：AI 代理查实时股市数据（$0.02 / 次）；
    
-   AI 模型推理：图像识别 API（$0.005 / 次分类）；
    
-   云资源支付：AI 代理购买 GPU 算力（$0.50/GPU 分钟）；
    
-   内容付费：用户按篇买新闻（$0.25 / 篇），无需订阅。
<!-- DAILY_CHECKIN_2025-10-18_END -->

# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->




# A2A协议与组件（核心概念）

## **一、核心参与者：谁在参与 A2A 交互？**

| 参与者 | 角色说明 |
| --- | --- |
| 用户（User） | 发起请求的人 / 自动服务（如 “要订酒店的用户”） |
| A2A 客户端（Client Agent） | 代表用户做事的程序 / 代理（如 “酒店预订代理”，用 A2A 协议发请求） |
| A2A 服务器（Remote Agent） | 提供服务的代理（如 “货币换算代理”，暴露 HTTP 端点，处理任务、返回结果） |

-   关键特点：A2A 服务器对客户端是 “黑匣子”，不暴露内部逻辑 / 工具。
    

## **二、核心通信元素：交互的 “基本零件”**

| 元素 | 作用说明 | 代码示例（简化） |
| --- | --- | --- |
| 代理卡 | JSON 格式 “数字名片”，含代理地址、认证要求、功能（客户端靠它发现代理） | json { "url": "https://currency-agent/a2a", "securitySchemes": ["openIdConnect"], "capabilities": ["convertCurrency"] } |
| 任务（Task） | 有状态的工作单元（唯一 ID + 生命周期，如 “300 美元换人民币” 任务） | python class Task(BaseModel): task_id: str status: Literal["submitted", "working", "completed"] request_data: dict |
| 消息（Message） | 单轮通信内容（含角色 “user/agent”+ 唯一 ID + 内容部件） | json { "message_id": "msg-123", "role": "user", "parts": [{"type": "TextPart", "content": "换300美元"}] } |
| 部件（Part） | 内容容器（TextPart 文本 / FilePart 文件 / DataPart 结构化数据） | python class TextPart(BaseModel): type: Literal["TextPart"] content: str class DataPart(BaseModel): type: Literal["DataPart"] data: dict |
| 工件（Artifact） | 代理生成的有形结果（如换算结果文档，含唯一 ID + 部件） | json { "artifact_id": "art-456", "name": "换算结果", "parts": [{"type": "DataPart", "data": {"amount": 300, "result": 2180}}] } |

## **三、交互机制：代理怎么 “聊天”？**

3 种模式适配不同场景，核心是 “高效传数据”：

1.  **请求 / 响应（轮询）**
    
    -   逻辑：客户端发请求→服务器马上回，长任务需客户端反复问 “结果好了吗”。
        
    -   代码（客户端轮询）：
        
        python
        
        ```python
        def poll_task(task_id):
            while True:
                resp = requests.get(f"https://agent/a2a/task/{task_id}")
                if resp.json()["status"] == "completed":
                    return resp.json()["artifact"]
                time.sleep(5)  # 每5秒问一次
        ```
        
2.  **SSE 流式传输**
    
    -   逻辑：客户端连服务器后不断开，服务器有更新就主动推（如 “任务处理中→结果生成”）。
        
    -   代码（客户端收流）：
        
        python
        
        ```python
        from sseclient import SSEClient
        messages = SSEClient(f"https://agent/a2a/stream?task_id=123")
        for msg in messages:
            if msg.event == "TaskStatusUpdate":
                print(f"状态：{msg.data}")
            if msg.event == "ArtifactUpdate":
                print(f"结果：{json.loads(msg.data)}")
        ```
        
3.  **推送通知（Webhook）**
    
    -   逻辑：长任务 / 断连场景，服务器用客户端提供的 Webhook 地址，有更新就主动发请求。
        
    -   代码（服务器推通知）：
        
        python
        
        ```python
        def send_webhook(webhook_url, task_data):
            requests.post(webhook_url, json={"task_id": "123", "status": "completed", "artifact": ...})
        ```
        

## **四、核心架构与工作流程：A2A 怎么跑起来？**

### **1\. 3 步核心流程**

1.  **发现（Discovery）**：客户端找代理卡（如访问`/.well-known/agent-card.json`），确定 “和谁聊、怎么聊”。
    
2.  **认证（Authentication）**：按代理卡要求拿 “通行证”（如 JWT 令牌），证明 “我是可信的”。
    
3.  **通信（Communication）**：客户端发任务→服务器处理→返回结果 / 推更新。
    

### **2\. 代码实现：用 FastA2A 搭 A2A 服务器（Python）**

-   前提：先装库 `pip install fasta2a pydantic`
    
-   代码（货币换算代理服务器）：
    
    python
    
    ```python
    from fastapi import FastAPI
    from pydantic import BaseModel
    from fasta2a import A2AServer, Task
    
    app = FastAPI()
    # 初始化A2A服务器，绑定代理卡
    a2a_server = A2AServer(
        agent_card={
            "url": "http://localhost:8000/a2a",
            "capabilities": ["convertCurrency"],
            "securitySchemes": []  # 简化：不设认证
        }
    )
    
    # 定义换算请求数据结构
    class ConvertRequest(BaseModel):
        amount: float
        from_currency: str
        to_currency: str
    
    # 处理换算任务
    @a2a_server.task_handler("convertCurrency")
    async def handle_convert(task: Task, request: ConvertRequest):
        # 模拟换算逻辑（1USD=7.27CNY）
        rate = 7.27 if request.to_currency == "CNY" else 1/7.27
        result = request.amount * rate
        # 返回工件（结果）
        return {
            "artifact": {
                "name": "CurrencyConversionResult",
                "parts": [{"type": "DataPart", "data": {"result": result}}]
            }
        }
    
    # 挂载A2A路由
    app.include_router(a2a_server.router, prefix="/a2a")
    
    # 运行：uvicorn main:app --port 8000
    ```
    

总结思维图

![exported_image (1).png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-17-1760712730430-exported_image__1_.png)
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->





-   **A2A协议**(基础)
    

_1.为何采用它_

Agent协作之间没有统一的规则，A2A协议提供AI代理之间“开放沟通标准”，使得不同框架（如 TensorFlow、PyTorch）、不同公司开发的 AI 代理，能无缝通信、一起协作

eg：A 代理负责数据分析，B 代理负责生成报告，二者通过 A2A 高效配合

_2.解决问题场景示例_

用户使用AI Agent来货币换算服务

```
        +-----------+        +--------------------+        +----------------------+
        |   User    | -----> |    AI Assistant    | -----> | Currency Conversion  |
        | (Request) |        |    (Identifies      |        |      Agent           |
        |           |        |    Conversion Task) |        | (Converts Currency)  |
        +-----------+        +--------------------+        +----------------------+
                                                       |
                                                (Returns Conversion Result)
                                                       |
                                                    +--------------------+
                                                    |  AI Assistant      |
                                                    |  (Final Result)    |
                                                    +--------------------+
                                                       |
                                                    +-----------+
                                                    |   User    |
                                                    | (Receives |
                                                    |   Result) |
                                                    +-----------+
```

Currency Conversion Agent：专注于执行 “不同货币间的汇率查询与换算”，是 A2A 协议中的 “功能型代理”，和AI Assistant之间通过A2A协议进行通信。

Request和Result：代表用户与 AI 助手、AI 助手与代理之间的 “数据交互”，A2A 协议会规定这些交互的标准格式，确保不同代理能顺畅沟通。

ps: A2A带来的优势：靠 HTTPS 实现安全协作（代理互不可见）、打破Agent代理孤岛实现互作、保留代理自主权、标准化沟通降低集成复杂度、支持长时间运行协作与流式处理。

_3.A2A位于的代理堆栈_

代理堆栈是构建 AI 代理的 “技术组合”，从底层基础到上层通信，分为四层，每层负责不同功能：

a.模型（最底层）：AI 代理的 “大脑”，用 LLM（如 GPT、Gemini）提供推理能力，是代理思考、决策的基础

b.框架（中间层）：构建代理的 “工具包”，比如 Google 的 ADK、LangGraph、Crew AI，提供代码模板、部署工具，帮开发者快速搭代理

c.MCP（中间层）：模型与外部资源的 “连接器”，专注把模型和数据、工具（如计算器、数据库查询）对接，降低连接复杂度（工具通常无状态，只做固定功能）

d.A2A（最上层**）**：代理之间的 “通信标准”，解决不同组织、不同框架开发的代理的协作问题，让代理能以 “自主身份” 多轮交互（如谈判、任务委派）

![屏幕截图_16-10-2025_22151_a2a-protocol.org.jpeg](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-16-1760624245446-_____16-10-2025_22151_a2a-protocol.org.jpeg)

A2A和MCP的区别

|   | A2A | MCP |
| --- | --- | --- |
| 定位 | 代理间的 “通信协议” | 模型与工具和数据的 “连接协议” |
| 对象 | 两个或以上 AI 代理 | 模型 ↔ 外部工具 / 数据 |
| 能力 | 多轮复杂交互（谈判） | 简化工具调用（如查数据库） |
| 价值 | 代理怎么合作 | 模型怎么用工具 |

ps:A2A和ADK------->协议和开发协议的工具包

_4.A2A 请求生命周期_

![exported_image.png](https://raw.githubusercontent.com/IntensiveCoLearning/trustless-agents/main/assets/SU-AN-coder/images/2025-10-16-1760625532237-exported_image.png)
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->







-   **ERC8004**（相关概念基础分析）
    

总目录：抽象，赋予动机（身份注册表，信誉注册表，验证注册表），规范，理由

_1.抽象_

区块链跨**组织边界发现、选择代理并与代理交互**，而无需预先存在的信任，从而**实现开放式代理经济**。

根据安全需求选择三种不同信任模型：使用客户端反馈的声誉系统、通过权益安全重新执行进行验证、zkML 证明或 TEE 预言机

eg：A 公司找 B 物流企业代理运输：

不知道有哪些潜在代理（发现难）;不确定代理的资质和可信度（选择难）；协作中数据易篡改、责任难追溯（交互难）。

_2.赋予动机（身份注册表，信誉注册表，验证注册表）_

现有协议的局限：MCP（服务器提供）+A2A（代理身份验证 技能通告等等）可支撑代理基础通信，但**不涵盖代理发现与信任**，无法满足跨组织需求

ERC方案目标：在不受信任环境中，通过 3 个轻量级注册表（每链单例部署，支持 L2 / 主网），构建开放跨组织代理经济

a.身份注册表：基于 ERC-721+URIStorage，提供可移植、抗审查的代理标识符（URI 解析注册文件）

b.信誉注册表：标准反馈接口，链上（保障可组合性）+ 链下（复杂算法）评分聚合，支撑专业服务生态

c.验证注册表：通用钩子，支持独立验证者（质押者、zkML 验证者等）检查与记录

ps：身份注册表相当于给代理发“唯一身份证”，信誉注册表相当于给代理“打分记评价”，验证注册表相当于给代理“做质检”

_3.规范_

按照 [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) 和 [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174) 中的说明进行解释

_4.理由_

a.适配多协议：MCP、A2A 常用，还可能有新协议，所以用灵活注册文件，能加各种接口，同时兼容 AI 功能和 Web3 信息（钱包、域名等）

b.反馈易上手：用 A2A、MCP 已有的说法（如 “任务”“工具”），反馈格式还能自己定，不用学新规则

c.反馈低门槛：给反馈不用先注册，还能让别人帮付 Gas 费，提交顺畅

d.数据易查找：反馈核心存在链上，完整数据建议存 IPFS，用工具能快速查到

e.部署易用：每条链只装一个注册表，代理在 A 链注册，也能去其他链干活，多链注册也支持

-   **身份注册表、信誉注册表和验证注册表**
    

核心关系图如下

```
┌────────────────────────┐
│     Identity Registry   │
│   (ERC-721 Agent NFTs)  │
│    ↓ 唯一身份与URI       │
└────────────┬───────────┘
             │ agentId
             │
┌────────────▼───────────┐
│   Reputation Registry   │
│   链上评分与反馈记录     │
│   （信任信号层）        │
└────────────┬───────────┘
             │ 验证/引用
┌────────────▼───────────┐
│   Validation Registry   │
│   验证结果与证明层       │
└────────────────────────┘
```

_1.身份注册表_

a.将每个 Agent 注册为一个 **ERC-721 NFT**

b.agentId = tokenId

c.NFT的所有权即代表代理的控制权

d.`tokenURI` 指向代理的链下注册文件（JSON 结构，描述代理能力、端点、信任模型等等）

| 项目 | 内容 |
| --- | --- |
| 标准扩展 | ERC-721 + ERC721URIStorage |
| 唯一标识 | eip155:chainId:registryAddress:agentId |
| 注册文件（JSON） | 含代理名称、描述、端点（A2A/MCP/DID）、支持的信任模式等 |
| 链上函数 | register(), setMetadata(), getMetadata() |
| 链下数据 | tokenURI 指向的 JSON 文件（可在 IPFS/HTTPS 等存储） |
| 事件 | Registered, MetadataSet |
| 可组合性 | 因为是 ERC-721，Agent 可与 NFT 市场、钱包等生态直接兼容 |

_2.信誉注册表_

a.提供一个了链上反馈与授权系统

b.用户或代理可为某个`agentId` 提供评分（0~100分）

c.反馈可附带链下文件 URI（如 IPFS）（透明度更高 审计性更强）

d.允许撤销与追加响应，实现声誉的治理与修正

| 项目 | 内容 |
| --- | --- |
| 依赖 | IdentityRegistry（确保 agentId 有效） |
| 反馈结构 | score, tag1, tag2, fileURI, fileHash |
| 反馈签名 | feedbackAuth（EIP-191 / ERC-1271）授权机制 |
| 事件 | NewFeedback, FeedbackRevoked, ResponseAppended |
| 撤销功能 | 用户可撤销旧反馈（防止垃圾和错误评价） |
| 扩展性 | feedback 文件中可加入 x402 支付凭证、上下文、任务信息等 |

_3.验证注册表_

a.代理可以请求验证任务结果

b.Validator可基于 zkML、TEE、或质押机制提供链上验证结果

c.通过事件与记录建立可追踪的验证链

| 项目 | 内容 |
| --- | --- |
| 验证请求 | validationRequest(validatorAddress, agentId, requestUri, requestHash) |
| 验证响应 | validationResponse(requestHash, response, responseUri, responseHash, tag) |
| 响应值 | 0–100（可二值/多级） |
| 链下数据 | requestUri / responseUri（例如 IPFS 审计报告） |
| 事件 | ValidationRequest, ValidationResponse |
| 查询函数 | getValidationStatus(), getSummary() |
| 可组合性 | 任何验证器协议（TEE、zk、质押）都能接入 |
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
