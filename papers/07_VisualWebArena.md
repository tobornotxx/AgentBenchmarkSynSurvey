# VisualWebArena: Evaluating Multimodal Agents on Realistic Visual Web Tasks

> **作者**: Jing Yu Koh, Robert Lo, Lawrence Jang, Vikram Duvvur, Ming Chong Lim, Po-Yu Huang, Graham Neubig, Shuyan Zhou, Ruslan Salakhutdinov, Daniel Fried  
> **机构**: CMU  
> **发表**: ACL 2024  
> **arXiv**: 2401.13649  
> **网站**: https://jykoh.com/vwa

---

## 研究问题

现有Web Agent benchmark主要面向纯文本Agent，忽略了许多需要**视觉信息**才能有效解决的自然任务。计算机界面天然为人类视觉感知设计，纯文本模型难以充分利用视觉信息。如何构建一个评估多模态Web Agent在**视觉定位任务**上能力的benchmark？

## 困难点

1. **视觉理解需求**：需要设计必须依赖图像理解才能完成的任务（如"找到与这张图片中相似的产品"）。
2. **多模态输入处理**：Agent需要同时处理图文输入，理解自然语言指令并在视觉丰富的网页上执行操作。
3. **任务多样性**：需要涵盖信息检索、比较、操作等多种视觉定位任务类型。

## 解决方法

1. **扩展WebArena环境**：在WebArena的基础上增加了需要视觉理解的任务类型。

2. **视觉定位任务设计**：
   - 图像匹配和比较
   - 视觉属性识别
   - 跨模态信息整合
   - 910个多样化的Web任务

3. **多模态评估框架**：
   - 同时支持纯文本和多模态Agent评估
   - 基于功能正确性的自动评估

## 主要结果

- 纯文本LLM Agent在视觉任务上表现显著受限。
- SOTA多模态模型仍存在明显能力缺陷。
- 定量和定性分析揭示了文本模型的局限性和多模态模型的能力差距。

## 对本课题的启示

VisualWebArena将Agent评估扩展到了多模态领域，其任务设计方法（在已有环境上叠加视觉需求）为**增量式benchmark构建**提供了范式。这也对数据合成提出了新挑战：合成数据需要同时包含视觉和文本模态的对齐信息。
