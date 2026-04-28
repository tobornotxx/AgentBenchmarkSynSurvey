# WebArena: A Realistic Web Environment for Building Autonomous Agents

> **作者**: Shuyan Zhou, Frank F. Xu, Hao Zhu, Xuhui Zhou, Robert Lo, Abishek Sridhar, Xianyi Cheng, Tianyue Ou, Yonatan Bisk, Daniel Fried, Uri Alon, Graham Neubig  
> **机构**: CMU, 普林斯顿大学  
> **发表**: ICLR 2024  
> **arXiv**: 2307.13854  
> **网站**: https://webarena.dev

---

## 研究问题

现有的Web Agent主要在简化的合成环境中创建和测试，与真实场景存在严重脱节。如何构建一个**高度逼真、可复现的Web环境**来评估语言引导Agent在真实Web任务中的表现？

## 困难点

1. **环境真实性**：现有benchmark使用模拟网站或静态网页，无法反映真实Web的复杂性和多样性。
2. **任务长程性**：真实Web任务通常需要多步操作和跨页面导航，对Agent的规划能力提出高要求。
3. **评估可靠性**：开放域任务的评估难以标准化，需要可靠的功能正确性验证方法。

## 解决方法

1. **真实Web环境**：构建了包含4个全功能网站的环境：
   - 电商网站（基于Magento）
   - 社交论坛（基于Reddit克隆）
   - 协作开发平台（基于GitLab）
   - 内容管理系统（基于维基）

2. **任务设计**：设计了812个多样化、长程的benchmark任务，模拟人类日常Web操作，如"找到价格在$50-$100之间的评价最高的蓝牙耳机"。

3. **评估方法**：基于功能正确性（functional correctness）的评估——检查任务执行后Web状态是否满足预期条件。

4. **辅助工具**：环境配备了地图工具和外部知识库（如用户手册），鼓励类人的任务解决方式。

## 主要结果

- GPT-4-based最佳Agent仅达到**14.41%**端到端任务成功率。
- 人类表现为**78.24%**。
- 巨大的人机差距揭示了当前LLM在复杂真实Web任务上的严重不足。
- 主要失败模式：操作错误、目标理解偏差、长程规划失败。

## 对本课题的启示

WebArena确立了**"真实环境+功能正确性评估"**的范式，但每个任务需要人工设计初始状态、任务描述和评估脚本，成本较高。后续工作（如AgentTrek、WebFactory）正是为了自动化这一过程。其任务模板和评估脚本框架为数据合成工作提供了参考。
