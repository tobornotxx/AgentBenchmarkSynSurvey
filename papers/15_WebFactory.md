# WebFactory: Automated Compression of Foundational Language Intelligence into Grounded Web Agents

> **作者**: Sicheng Fan, Qingyun Shi, Shengze Xu, Shengbo Cai, Tieyong Zeng, Li Ling, Yanyi Shang, Dehan Kong  
> **机构**: CUHK, 字节跳动  
> **发表**: 2026（预印本）  
> **arXiv**: 2603.05044

---

## 研究问题

当前训练GUI Agent的范式受限于两种方式：(1) 不安全、不可复现的在线Web交互，(2) 昂贵稀缺的人工标注数据和环境。这些方法过度关注**数据量**，忽略了一个更关键的因素：如何高效地将LLM的潜在知识**压缩**为可操作的Agent行为？

## 困难点

1. **数据效率低**：现有方法需要大量数据才能训练出有效的Agent。
2. **环境不可控**：在真实网站上进行交互训练存在安全和复现性问题。
3. **知识浪费**：LLM已经编码了大量互联网知识，但这些知识未被有效转化为Agent能力。
4. **评估分离**：训练和评估通常使用不同的环境，可能产生偏差。

## 解决方法

### WebFactory管线

一个完全自动化的闭环强化学习（RL）管线：

### 1. 可扩展环境合成（Scalable Environment Synthesis）
- 自动合成用于训练的Web环境
- 无需依赖真实网站，避免安全和复现性问题

### 2. 知识感知任务生成（Knowledge-Aware Task Generation）
- 基于LLM已有知识生成任务
- 确保任务与LLM的知识分布对齐

### 3. LLM驱动轨迹收集（LLM-powered Trajectory Collection）
- 使用LLM在合成环境中执行任务
- 收集多样化的操作轨迹

### 4. 分解奖励RL训练（Decomposed Reward RL Training）
- 将奖励分解为多个子奖励
- 提供更精细的学习信号

### 5. 系统化Agent评估
- 内部离线和在线迁移benchmark
- 全面评估Agent的泛化能力

### 核心洞察："具身化潜力"（Embodiment Potential）
- 不同LLM基础模型具有不同的"具身化潜力"
- 提出了评估模型适合作为Agent基础的新维度

## 主要结果

- 仅在**10个合成网站**上训练，即可匹配在大量人工标注数据上训练的Agent
- 在内部离线和在线迁移benchmark上一致地超越基础模型
- 展示了卓越的数据效率
- 不同LLM基础模型的具身化潜力差异显著

## 对本课题的启示

WebFactory的核心贡献在于**知识压缩**视角：
1. **少量合成环境 ≈ 大量真实数据**——证明了合成数据的高效性
2. **端到端自动管线**——从环境合成到评估全部自动化
3. **RL与合成数据的结合**——分解奖励提供了精细监督
4. **具身化潜力**——为选择Agent基础模型提供了新标准

对于benchmark数据合成，WebFactory证明了**质量（知识对齐）比数量更重要**。
