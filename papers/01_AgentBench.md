# AgentBench: Evaluating LLMs as Agents

> **作者**: Xiao Liu, Hao Yu, Hanchen Zhang, Yifan Xu, Xuanyu Lei, Hanyu Lai, Yu Gu, Hangliang Ding, Kaiwen Men, et al.  
> **机构**: 清华大学  
> **发表**: ICLR 2024  
> **arXiv**: 2308.03688  
> **代码**: https://github.com/THUDM/AgentBench

---

## 研究问题

随着LLM作为自主Agent的潜力被广泛认可，如何**系统性、定量地评估LLM作为Agent在复杂交互环境中的推理和决策能力**，是一个亟待解决的问题。现有的评估主要集中在静态NLP任务上，缺乏对Agent在动态环境中多步交互能力的全面评估。

## 困难点

1. **评估维度多样性**：Agent能力涵盖代码执行、Web浏览、游戏策略、知识推理等多个维度，单一benchmark难以全面覆盖。
2. **环境构建复杂**：每个评估环境需要独立的交互接口和评判机制。
3. **开源与闭源模型的差距**：如何建立统一标准，同时揭示模型间的实质性差异。

## 解决方法

提出AgentBench，一个**多维度综合benchmark**，包含8个不同的交互环境：

| 环境 | 描述 |
|------|------|
| Operating System (OS) | 在Linux终端执行命令完成任务 |
| Database (DB) | SQL数据库查询和操作 |
| Knowledge Graph (KG) | 知识图谱推理 |
| Digital Card Game (DCG) | 数字卡牌游戏策略 |
| Lateral Thinking Puzzles (LTP) | 横向思维谜题 |
| Household (HH) | 家务场景任务（ALFWorld） |
| Web Browsing (WB) | 网页浏览任务 |
| Web Shopping (WS) | 网络购物任务 |

每个环境都提供标准化的交互接口，支持多轮对话式评估。

## 主要结果

- 评估了27个API-based和开源LLM。
- **顶级商业模型**（如GPT-4）在多环境中展现出较强的Agent能力。
- 开源模型（≤70B参数）与商业模型之间存在**显著差距**。
- 失败原因分析：**长程推理能力差**、**决策能力不足**、**指令遵循能力弱**是主要障碍。
- 发现：在高质量多轮对齐数据上训练可以改善Agent表现；代码训练对不同Agent任务的影响不一致。

## 对本课题的启示

AgentBench建立了Agent评估的标准范式——多环境、多维度、交互式评估。但其数据**主要依靠人工设计**，可扩展性受限，为后续自动化数据合成工作指明了方向。
