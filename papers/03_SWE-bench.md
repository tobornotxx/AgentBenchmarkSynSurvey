# SWE-bench: Can Language Models Resolve Real-World GitHub Issues?

> **作者**: Carlos E. Jimenez, John Yang, Alexander Wettig, Shunyu Yao, Kexin Pei, Ofir Press, Karthik Narasimhan  
> **机构**: 普林斯顿大学, 哥伦比亚大学  
> **发表**: ICLR 2024  
> **arXiv**: 2310.06770  
> **网站**: https://swe-bench.github.io

---

## 研究问题

如何在**真实软件工程场景**中评估语言模型的能力？具体地说，模型能否理解一个GitHub Issue描述，并在完整代码库中进行修改来解决该问题？

## 困难点

1. **任务复杂性**：解决真实Issue通常需要理解和协调多个函数、类甚至文件的修改，远超传统代码生成任务。
2. **上下文长度**：完整代码库远超模型上下文窗口，需要有效的信息检索和推理。
3. **评估标准**：需要确保修改不仅修复了目标Issue，还通过了相关测试用例。
4. **数据集构建可持续性**：如何从不断增长的开源项目中持续获取高质量评估数据。

## 解决方法

1. **数据来源**：从GitHub上12个流行Python仓库（如Django, scikit-learn, matplotlib等）自动提取Issue和对应的Pull Request。

2. **数据构建管线**：
   - 筛选有对应PR和测试的Issue
   - 提取任务实例（Issue描述 + 代码库快照 + 测试用例）
   - 共构建了**2,294个任务实例**

3. **评估框架**：
   - 给定代码库和Issue描述
   - 模型生成代码补丁
   - 通过执行测试用例验证修改正确性

4. **模型微调**：基于SWE-bench数据微调了SWE-Llama模型。

## 主要结果

- 最佳模型Claude 2仅解决了**1.96%**的Issue。
- 揭示了当前LLM在实际软件工程任务中的巨大局限。
- 该benchmark已成为评估代码Agent（如SWE-Agent, Devin等）的事实标准。

## 对本课题的启示

SWE-bench开创了**"从真实软件工件自动构建benchmark"**的范式——利用GitHub PR的天然结构（Issue → 代码修改 → 测试验证）自动生成评估数据。这是一种高效的**半自动数据合成方法**，可推广到其他具有自然评审流程的领域。其持续可更新的特性也为动态benchmark设计提供了启示。
