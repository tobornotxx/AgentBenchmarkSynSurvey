# DynaWeb: Model-Based Reinforcement Learning of Web Agents

> **作者**: Hang Ding, Peidong Liu, Junqiao Wang, Ziwei Ji, Meng Cao, Rongzhao Zhang, Lynn Ai, Eric Yang, Tianyu Shi, Lei Yu  
> **机构**: 未明确（预印本）  
> **发表**: 2026（预印本）  
> **arXiv**: 2601.22149

---

## 研究问题

训练Web Agent的强化学习面临一个根本矛盾：Agent需要与环境交互来学习，但与真实互联网交互**效率低、成本高、风险大**。模型驱动的强化学习（Model-Based RL, MBRL）通过学习环境模型来进行模拟交互是一个有前景的方向，但在Web领域尚未被充分探索。如何构建一个**Web世界模型**，让Agent在"想象"中学习？

## 困难点

1. **Web环境的复杂性**：网页内容多样、动态变化，难以建模。
2. **状态空间巨大**：HTML/DOM树的状态空间远大于传统RL环境。
3. **长程依赖**：Web任务通常需要多步操作，世界模型需要维持长距离的一致性。
4. **训练稳定性**：世界模型预测的误差会在rollout中累积（compounding error）。

## 解决方法

### DynaWeb 框架

DynaWeb是一个基于MBRL的Web Agent训练框架，核心思想是训练一个**Web World Model**来**生成合成轨迹**供Agent学习。

#### 1. Web World Model

- 训练一个神经网络模型**预测Web页面表示**
- 输入：当前页面状态 + Agent动作
- 输出：执行动作后的预测页面状态
- 使用**自然语言表示**而非原始HTML（降低建模复杂度）

#### 2. 合成轨迹生成（Dreaming）

- Agent在World Model中进行**梦境rollout**
- 从任意状态出发，Agent选择动作，World Model预测下一状态
- 生成**大量合成轨迹**用于策略学习
- 完全不需要与真实网站交互

#### 3. 混合训练策略

DynaWeb的训练结合两种数据源：
- **真实专家轨迹**：来自训练数据的高质量真实轨迹
- **合成轨迹（on-policy rollouts）**：Agent在World Model中生成的轨迹
- 两种轨迹在训练中**随机交错**（interleaving）
- 真实轨迹提供稳定信号，合成轨迹提供探索多样性

#### 4. 在线强化学习

- 在World Model生成的合成轨迹上进行在线RL
- 利用World Model的高效模拟降低了RL的样本复杂度
- 实轨迹的交错确保了训练稳定性

## 主要结果

- 在**WebArena**和**WebVoyager** benchmark上评估
- DynaWeb**一致且显著地提升**了SOTA开源Web Agent模型的性能
- 证明了Web Agent**可以通过"想象"来学习**
- 提供了一种可扩展且高效的Web Agent在线RL训练方式

## 核心贡献与技术细节

### 1. Web World Model的可行性
DynaWeb首次证明了为Web环境训练一个足够好的世界模型是可行的。尽管Web环境比传统MBRL场景（如游戏）复杂得多，但通过使用自然语言表示而非原始HTML，降低了建模难度。

### 2. "想象中学习"的范式
传统方法：Agent → 真实环境交互 → 收集轨迹 → 学习
DynaWeb：Agent → World Model中rollout → 收集合成轨迹 → 学习
这种范式的优势：
- **无限轨迹**：World Model可以生成任意多的轨迹
- **零成本交互**：不需要真实环境
- **零风险**：没有安全风险

### 3. 合成轨迹的质量
通过混合真实和合成轨迹的训练策略，DynaWeb有效解决了World Model预测误差累积的问题。这种混合策略可以视为一种**受控的合成数据使用方式**。

### 4. 与其他合成方法的互补性
DynaWeb生成的是**Agent当前策略下的on-policy轨迹**，而AgentTrek/Agent-as-Annotators生成的是**Expert轨迹**。这两种合成数据可以互补。

## 对本课题的启示

DynaWeb对benchmark数据合成的启示：
1. **World Model是一种特殊的环境合成**：不直接构建环境，而是学习环境的隐式表示
2. **合成轨迹+真实轨迹的混合**效果优于单独使用任何一种
3. **on-policy合成数据**（Agent当前策略下的轨迹）与expert合成数据有本质区别
4. MBRL为Agent训练数据合成提供了**新的技术路线**

### 方法论定位

| 方法 | 环境类型 | 轨迹来源 | 训练方式 |
|------|----------|----------|----------|
| AgentTrek | 真实环境 | Expert引导 | SFT |
| WebFactory | 合成网站 | LLM收集 | RL |
| VeriEnv | 克隆网站 | Agent自主探索 | RL |
| **DynaWeb** | **World Model** | **梦境rollout** | **MBRL** |
| EvoCUA | 合成沙箱 | 进化rollout | 进化RL |
