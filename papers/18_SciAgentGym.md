# SciAgentGym: Benchmarking Multi-Step Scientific Tool-use in LLM Agents

> **作者**: Yujiong Shen, Yajie Yang, Zhiheng Xi, Binze Hu, Huayu Sha, Jiazheng Zhang, Qiyuan Peng, Junlin Shang, Jixuan Huang, Yutao Fan, Jingqi Tong, Shihan Dou, Ming Zhang, Lei Bai, Zhenfei Yin, Tao Gui, Xingjun Ma, Qi Zhang, Xuanjing Huang, Yu-Gang Jiang  
> **机构**: 复旦大学, 上海AI Lab  
> **发表**: 2026（预印本）  
> **arXiv**: 2602.12984

---

## 研究问题

科学推理本质上要求整合复杂工具包来导航领域特定知识。然而，现有benchmark大多忽略了**多步骤科学工具使用**这一关键能力。如何构建一个评估LLM Agent在科学领域中多步骤工具使用能力的benchmark？

## 困难点

1. **工具多样性**：科学研究使用的工具种类繁多（计算库、可视化工具、数据处理工具等）。
2. **多步骤推理**：科学任务通常需要多个工具的序列化使用，每步依赖前步结果。
3. **领域知识需求**：正确使用科学工具需要深厚的领域知识。
4. **评估复杂性**：科学任务的正确性评估比通用任务更复杂。

## 解决方法

### Benchmark设计

1. **多步骤科学任务**：设计需要Agent连续调用多个科学工具的任务
2. **工具集合**：涵盖数据分析、数值计算、可视化等多类科学工具
3. **领域覆盖**：跨多个科学领域
4. **评估框架**：支持自动化的多步骤评估

### 数据构建方法

- 从真实科学工作流中提取任务模式
- 结合科学知识库自动生成任务变体
- 人工验证确保科学正确性

## 主要结果

- 揭示了当前LLM在科学工具使用上的显著不足
- 多步骤任务的错误传播是主要挑战
- 为科学Agent的发展提供了量化评估标准

## 对本课题的启示

SciAgentGym展示了**领域特化benchmark构建**的方法论：
1. 从真实领域工作流提取任务模板
2. 利用领域知识库进行变体合成
3. 多步骤评估的设计模式
4. 工具调用序列的正确性验证方法
