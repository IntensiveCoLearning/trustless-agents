---
timezone: UTC+8
---

# JoyWang

**GitHub ID:** JoyWQ

**Telegram:** @JoyWQQ

## Self-introduction

在一家传统物联网公司做数据预警平台的后端研发工作 主要是流式系统 工作中会用到一些数据挖掘或者自然语言学习的小模型 最近也在全力以赴的学习Web3相关的技术与知识和参加业余的黑客松 希望能通过此次活动更大幅度地提升自己 并结识到优秀、有意思的新朋友

## Notes
<!-- Content_START -->
# 2025-10-17
<!-- DAILY_CHECKIN_2025-10-17_START -->
## **一、了解声誉分析、ZK及TEE在EIP8004里的应用：**

```
原始数据
    ↓ [声誉分析层 - 量化信任]
声誉分数 + 元数据
    ↓ [TEE层 - 确保硬件层安全]  
可信计算结果 + SGX证明
    ↓ [ZK层 - 保护隐私]
零知识证明 + 选择性披露
    ↓ [链上验证]
可验证的信任声明
```

## **二、场景推演及伪代码**

### **阶段1：服务发现与资格验证**

**步骤1.1：客户B发布需求**

```
TaskRequirements {
    min_reputation: 800,
    tee_required: true,
    zk_proof_required: true
}
```

**步骤1.2：服务A提供基础证明**

```
# A只需要提供ZK证明，声誉分数是预计算的
def generate_simple_qualification():
    # 直接从声誉系统获取预计算的结果
    precomputed_reputation = get_precomputed_reputation()  # {score: 845, breaches: 0, ...}
    
    # 仅使用ZK层生成证明
    zk_proof = zk_circuit.prove(
        statement="reputation_score > 800 AND data_breaches == 0",
        witness=precomputed_reputation
    )
    
    return SimpleQualification(zk_proof, public_metadata)
```

**步骤1.3：验证C快速验证**

```
function quickVerify(SimpleQualification memory proof) public view returns (bool) {
    return zkVerifier.verify(proof.zk_proof);  // 快速验证
}
```

### **阶段2：安全任务执行**

**步骤2.1：数据在TEE中处理**

```
# 这才是TEE的主要应用场景
def secure_data_processing(encrypted_data):
    with tee_enclave():
        # 解密和分析
        raw_data = decrypt(encrypted_data)
        analysis_result = ai_analysis(raw_data)
        
        # 生成处理证明
        processing_proof = generate_processing_attestation(
            input_hash=hash(encrypted_data),
            output_hash=hash(analysis_result),
            code_integrity=AI_MODEL_HASH
        )
        
        return analysis_result, processing_proof
```

### **阶段3：结果交付与声誉更新**

**步骤3.1：结果交付**

```
result_package = {
    "insights": analysis_results,
    "processing_proof": processing_proof,  # TEE处理证明
    "privacy_proof": generate_privacy_proof()  # ZK隐私证明
}
```

**步骤3.2：声誉系统完整更新（这才是三层架构的正确位置）**

```
def complete_reputation_update(task_data, client_feedback, processing_proof):
    # 第一层：声誉分析（收集所有数据）
    performance_data = {
        "task_complexity": task_data.complexity,
        "processing_time": task_data.duration,
        "resource_usage": task_data.resources,
        "client_feedback": client_feedback,
        "tee_attestation": processing_proof  # 证明计算完整性
    }
    
    # 第二层：TEE安全计算新声誉分数
    with tee_enclave():
        # 在可信环境中重新计算声誉
        new_reputation = reputation_algorithm.calculate(
            current_score=845,
            new_performance=performance_data
        )
        
        # 生成计算完整性证明
        reputation_attestation = generate_sgx_attestation()
    
    # 第三层：ZK生成新的资格证明
    updated_zk_proof = zk_circuit.prove(
        statement=f"reputation_score > {new_reputation} AND recent_performance_positive",
        witness={
            "new_score": new_reputation,
            "performance_data": performance_data
        }
    )
    
    return UpdatedReputation(new_reputation, reputation_attestation, updated_zk_proof)
```
<!-- DAILY_CHECKIN_2025-10-17_END -->

# 2025-10-16
<!-- DAILY_CHECKIN_2025-10-16_START -->

1.  阅读erc-8004官方标准及hashkey的文章
    
2.  核心内容梳理：
    
    1.  智能体身份注册表：可使用erc721保证身份的唯一性
        
    2.  智能体声誉注册表：提供服务后授权评价并记录评价（链下分析评价数据，结果可回传至链上）
        
    3.  智能体验证注册表：申请并接收验证（链下验证，结果回传至链上）
        
3.  创建新项目，参考IdentityRegistry.sol进行简单重写
<!-- DAILY_CHECKIN_2025-10-16_END -->

# 2025-10-15
<!-- DAILY_CHECKIN_2025-10-15_START -->


1.  拉取erc-8004-example代码
    
2.  构建针对合约的简单测试样例
    
3.  使用Foundry和Anvil进行简单的本地部署和测试
<!-- DAILY_CHECKIN_2025-10-15_END -->
<!-- Content_END -->
