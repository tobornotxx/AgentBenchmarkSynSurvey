# Agent-as-Annotators: Structured Distillation of Web Agent Capabilities Enables Generalization

> **作者**: Xing Han Lù, Siva Reddy  
> **机构**: McGill University, Mila  
> **发表**: 2026（预印本）  
> **arXiv**: 2604.07776  
> **项目**: https://agent-as-annotators.github.io/

---

## 研究问题

前沿LLM（如Gemini 3 Pro, Claude 4等）可以导航复杂网站，但其**高成本和对第三方API的依赖**使得本地部署不切实际。如何将前沿模型的Web Agent能力**蒸馏到小型开源模型**中？核心挑战是如何**结构化地生成高质量合成轨迹**。

## 困难点

1. **轨迹质量不均**：前沿模型生成的轨迹并非都是高质量的，需要有效过滤。
2. **任务覆盖不足**：随机生成任务可能导致分布偏斜。
3. **知识蒸馏效率**：如何用最少的合成数据获得最大的性能提升。
4. **跨环境泛化**：在特定网站上训练的Agent需要能泛化到未见网站。

## 解决方法

### Agent-as-Annotators 框架

核心创新：将合成轨迹生成过程**类比于人工标注流程**，用模块化的LLM组件替代人工标注的三个角色。

#### 1. 三角色分工

| 角色 | 人工标注中 | Agent-as-Annotators中 | 功能 |
|------|-----------|---------------------|------|
| **Task Designer** | 任务设计师 | LLM任务生成器 | 设计多样化的Web任务 |
| **Annotator** | 标注员 | Teacher Agent（Gemini 3 Pro） | 在Web环境中执行任务，记录轨迹 |
| **Supervisor** | 质检员 | LLM Judge | 评估轨迹质量，过滤低质量数据 |

#### 2. 任务生成（Task Designer）

- 分析目标网站的功能和页面结构
- 生成覆盖不同功能和复杂度的任务集合
- 加入**评估提示（evaluation hints）**，帮助Judge更准确地评估
- 确保任务分布的多样性

#### 3. 轨迹收集（Annotator）

- 使用Gemini 3 Pro作为Teacher Agent
- 在6个Web环境中执行生成的任务
- 记录完整轨迹：截图、HTML、动作序列、推理链
- 跨6个环境共生成**3,000条轨迹**

#### 4. 质量过滤（Supervisor）

- LLM Judge评估每条轨迹的正确性
- 利用评估提示提高判断准确度
- 过滤通过率约**77.4%**（2,322/3,000条通过）
- 仅保留高质量轨迹用于训练

#### 5. 推理链蒸馏

- 不仅蒸馏动作序列，还蒸馏**推理过程（reasoning traces）**
- Student模型学习Teacher的思考过程
- 这一设计贡献了显著的性能增益

### 训练配置

- Student模型：9B参数
- 训练方式：纯监督学习（SFT）
- 训练数据：2,322条通过质量过滤的轨迹
- 跨6个Web环境

## 主要结果

- **WebArena上41.5%成功率**，超越：
  - Claude 3.5 Sonnet (36.0%)
  - GPT-4o (31.5%)
  - 此前最佳开源结果Go-Browse (21.7%)——提升近一倍
- **WorkArena L1**（从未见过的企业平台）上**+18.2百分点**
- 在另外3个benchmark上也有一致提升
- 仅用2,322条合成轨迹训练的9B模型即可超越大型闭源模型

### 消融实验（关键细节）

- **Judge过滤**贡献了显著性能增益
- **评估提示（Evaluation Hints）**提升了过滤质量
- **推理链（Reasoning Traces）**蒸馏贡献了可测量的增益
- 每个管线组件都有独立可验证的贡献

## 核心贡献与技术细节

### 1. 标注流程的结构化分解
将"LLM生成轨迹"这个黑盒过程分解为Task Designer → Annotator → Supervisor的结构化流程，每个环节可独立优化和评估。这与EigenData的DatabaseAgent → CodingAgent → DataAgent分工有异曲同工之妙。

### 2. 数据效率惊人
仅2,322条轨迹（单个Teacher模型），就让9B Student在WebArena上超越GPT-4o。这进一步证实了WebFactory的发现：**数据质量远比数据数量重要**。

### 3. 跨环境泛化
在WorkArena L1（训练时从未见过的企业级平台）上的大幅提升，证明了结构化蒸馏方法产生的不是模式记忆，而是**可迁移的Web导航能力**。

### 4. 推理链蒸馏的价值
不只蒸馏"做什么"（actions），还蒸馏"为什么这样做"（reasoning）。这为Agent数据合成指出了一个重要维度——**轨迹数据应包含推理过程**。

## 对本课题的启示

Agent-as-Annotators对benchmark数据合成的启示：
1. **结构化分工**大幅提升合成数据质量
2. **少量高质量数据 > 大量低质量数据**（2K条即超越闭源模型）
3. **推理链蒸馏**是合成数据中被低估的维度
4. **质量过滤**（Judge机制）是必不可少的环节
5. 提供了一种**低成本、高效果**的Agent能力迁移方法
