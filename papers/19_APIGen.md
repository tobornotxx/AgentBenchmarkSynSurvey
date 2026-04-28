# APIGen: Automated Pipeline for Generating Verifiable and Diverse Function-Calling Datasets

> **作者**: Zuxin Liu, Thai Hoang, Jianguo Zhang, Ming Zhu, Tian Lan, Shirley Kokane, Juntao Tan, Weiran Yao, Zhiwei Liu, Yihao Feng, Rithesh Murthy, Liangwei Yang, Silvio Savarese, Juan Carlos Niebles, Huan Wang, Shelby Heinecke, Caiming Xiong  
> **机构**: Salesforce AI Research  
> **发表**: 2024（预印本）  
> **arXiv**: 2406.18518  
> **项目**: https://apigen-pipeline.github.io/  
> **数据集**: https://huggingface.co/datasets/Salesforce/xlam-function-calling-60k

---

## 研究问题

函数调用（function-calling）Agent模型的发展需要多样、可靠、高质量的训练数据集。现有数据集要么规模太小、要么质量不可控、要么缺乏可验证性。如何设计一条**自动化、可验证、可扩展**的数据合成管线来生成函数调用数据集？

## 困难点

1. **数据质量保证**：LLM生成的函数调用数据可能包含格式错误、参数错误、语义错误等多种问题。
2. **多样性不足**：单一生成策略容易导致数据分布集中在少数模式上。
3. **可验证性缺失**：大部分已有数据集缺少对函数调用正确性的验证，仅靠LLM判断，幻觉问题严重。
4. **API覆盖率**：需要涵盖足够广泛的API类别和使用场景。

## 解决方法

### APIGen 管线设计

#### 第一步：API收集与规范化
- 从21个不同类别收集了**3,673个可执行API**
- 每个API都有完整的函数签名（schema）、参数定义和可执行实现
- 确保API集合的多样性和真实性

#### 第二步：多样化数据生成
- 使用多个强LLM（如GPT-4等）生成用户查询（query）和对应的函数调用序列
- 通过**种子prompt多样化**和**采样温度调节**确保生成数据的多样性
- 支持单函数和多函数调用场景

#### 第三步：三层级验证（核心创新）

APIGen的最大亮点是其**三层级质量验证机制**：

| 验证层级 | 内容 | 作用 |
|----------|------|------|
| **格式检查** | JSON格式、参数类型、必需参数 | 过滤语法错误 |
| **实际执行** | 在真实环境中执行函数调用 | 验证可执行性 |
| **语义验证** | LLM评估结果是否满足用户意图 | 确保功能正确性 |

三层验证逐步过滤，最终只保留通过所有检查的高质量数据。

### 数据统计

- 最终生成**60,000条高质量数据**
- 涵盖21个类别
- 包含单工具和多工具调用场景
- 所有数据都经过三层验证

## 主要结果

- 使用APIGen数据微调的**7B参数模型**在Berkeley Function-Calling Benchmark上达到了**SOTA**，超越了多个GPT-4版本
- **1B参数模型**即超越GPT-3.5-Turbo和Claude-3 Haiku
- 证明了高质量合成数据能让小模型在特定任务上超越大模型
- 数据效率极高：60K数据即可获得顶级性能

## 核心贡献与技术细节

### 1. 可执行验证 vs LLM判断
APIGen的核心洞察是：**不信任LLM的自我判断，而是通过实际执行来验证**。这与EigenData的结果感知评估、EvoCUA的可执行验证器形成了一致的技术趋势。

### 2. 数据过滤率
三层验证的过滤率约为40-60%，即一半以上的LLM生成数据在某一层级被过滤掉。这说明：
- 即使用强LLM生成，数据质量仍无法保证
- 自动验证机制是必要的

### 3. 小模型超越大模型
APIGen数据训练的7B模型超越GPT-4，说明**数据质量 > 模型规模**在函数调用场景中的重要性。

## 对本课题的启示

APIGen是**函数调用数据合成**领域的开创性工作：
1. **三层验证范式**为后续所有数据合成工作建立了质量保证的标杆
2. **可执行验证**成为合成数据质量控制的黄金标准
3. 证明了合成数据可以让小模型达到大模型水平
4. 直接启发了EigenData等后续全生命周期数据平台

### 与其他工作的关系

| 对比维度 | APIGen | ToolLLM | EigenData |
|----------|--------|---------|-----------|
| 数据范围 | 函数调用 | API工具使用 | 函数调用全生命周期 |
| 验证方法 | 三层级（格式+执行+语义） | ToolEval自动评估 | 结果感知评估 |
| 环境生成 | 手动收集API | 从RapidAPI收集 | 自动生成环境 |
| 数据规模 | 60K | 12K+ | 自适应 |
| 时间 | 2024 | 2023 | 2026 |
