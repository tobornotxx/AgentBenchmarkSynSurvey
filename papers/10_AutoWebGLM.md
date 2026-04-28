# AutoWebGLM: A Large Language Model-based Web Navigating Agent

> **作者**: Hanyu Lai, Xiao Liu, Iat Long Iong, Shuntian Yao, Yuxuan Chen, Pengbo Shen, Hao Yu, Hanchen Zhang, Xiaohan Zhang, Yuxiao Dong, Jie Tang  
> **机构**: 清华大学  
> **发表**: KDD 2024  
> **arXiv**: 2404.03648  
> **代码**: https://github.com/THUDM/AutoWebGLM

---

## 研究问题

如何构建一个**开源的、高性能的Web导航Agent**，使其在真实Web任务中超越GPT-4？关键挑战包括HTML数据的复杂性、网页操作的多样性以及开放域Web的任务难度。

## 困难点

1. **HTML数据复杂性**：原始HTML包含大量冗余信息，需要有效简化。
2. **操作空间多样性**：Web操作包括点击、输入、滚动等多种类型，组合空间巨大。
3. **开放域任务**：不同网站结构差异巨大，Agent需要泛化到未见网站。
4. **训练数据稀缺**：高质量Web Agent轨迹数据极其匮乏。

## 解决方法

### 1. HTML简化算法
设计了保留关键信息的HTML简化算法，模仿人类浏览模式，将冗余的网页数据压缩为简洁表示。

### 2. 人机混合数据构建（核心贡献）
采用**Hybrid Human-AI方法**构建Web浏览训练数据：
- **人工部分**：人工标注者提供高质量的关键操作示范
- **AI部分**：LLM自动扩展和补充训练数据
- **课程训练**：从简单到复杂的课程学习策略

### 3. 自举优化
- **强化学习（RL）**：通过环境反馈优化Agent策略
- **拒绝采样（Rejection Sampling）**：过滤低质量轨迹
- 进一步提升网页理解、浏览器操作和任务分解能力

### 4. AutoWebBench
建立了**双语（中英文）benchmark**用于真实Web导航任务评估。

## 主要结果

- AutoWebGLM基于ChatGLM3-6B，是较小的开源模型。
- 在多个Web导航benchmark上展现出与GPT-4相当甚至更好的表现。
- 在AutoWebBench上进行了全面评估。

## 对本课题的启示

AutoWebGLM的人机混合数据构建方法是连接"纯人工标注"和"纯自动合成"的重要中间路线。其"人工种子数据 → AI扩展 → RL/拒绝采样精炼"的管线为后续全自动化工作（如AgentTrek、WebFactory）奠定了基础。AutoWebBench的双语设计也提示了benchmark数据合成中的多语言维度。
