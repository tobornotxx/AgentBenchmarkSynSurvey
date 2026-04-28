# ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs

> **作者**: Yujia Qin, Shihao Liang, Yining Ye, Kunlun Zhu, Lan Yan, Yaxi Lu, Yankai Lin, Xin Cong, Xiangru Tang, et al.  
> **机构**: 清华大学, 耶鲁大学  
> **发表**: NeurIPS 2023  
> **arXiv**: 2307.16789  
> **代码**: https://github.com/OpenBMB/ToolBench

---

## 研究问题

开源LLM在工具使用（tool-use）能力上与闭源模型（如ChatGPT）存在显著差距。如何构建一个**通用的工具使用框架**，涵盖数据构建、模型训练和评估的全流程，以提升开源LLM的工具调用能力？

## 困难点

1. **API规模与多样性**：现实中API种类繁多，如何覆盖大量真实API场景。
2. **指令多样性**：需要生成涵盖单工具和多工具场景的多样化指令。
3. **解决路径标注**：每条指令的正确API调用序列（解决路径）标注成本极高。
4. **评估标准化**：工具使用的正确性难以用简单指标衡量。

## 解决方法

### 数据构建（ToolBench）

三阶段自动构建：

1. **API收集**：从RapidAPI Hub收集**16,464个真实RESTful API**，横跨49个类别。
2. **指令生成**：使用ChatGPT围绕这些API生成多样化的用户指令，涵盖：
   - 单工具场景（Single-tool）
   - 多工具场景（Multi-tool）
3. **解决路径标注**：使用ChatGPT搜索有效的解决路径（API调用链）。

### 决策增强

提出**基于深度优先搜索（DFS）的决策树算法**，使LLM能够评估多条推理链路并扩展搜索空间，提升复杂指令的解决能力。

### 自动评估（ToolEval）

开发了自动评估器ToolEval，评估工具调用的功能正确性。

### 模型训练

基于ToolBench微调LLaMA得到ToolLLaMA，并配备神经API检索器推荐合适的API。

## 主要结果

- ToolLLaMA展现了执行复杂指令和泛化到未见API的显著能力。
- 与ChatGPT表现相当。
- 在分布外数据集APIBench上展现了强零样本泛化能力。

## 对本课题的启示

ToolLLM是**LLM驱动的benchmark数据合成**的先驱性工作。其"收集真实API → LLM生成指令 → LLM标注路径"的管线直接启发了后续的数据合成框架（如EigenData）。DFS决策树搜索也影响了Agent-R等使用树搜索构建训练数据的工作。
