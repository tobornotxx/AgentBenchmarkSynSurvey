# OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments

> **作者**: Tianbao Xie, Danyang Zhang, Jixuan Chen, Xiaochuan Li, Siheng Zhao, Ruisheng Cao, Toh Jing Hua, Zhoujun Cheng, et al.  
> **机构**: HKU, 上海交通大学  
> **发表**: NeurIPS 2024  
> **arXiv**: 2404.07972  
> **网站**: https://os-world.github.io

---

## 研究问题

现有Agent benchmark要么缺乏交互环境，要么局限于特定应用或领域（如仅Web浏览），无法反映真实计算机使用的多样性和复杂性。如何构建一个**可扩展的、真实的操作系统级计算机环境**来评估多模态Agent在开放式任务中的表现？

## 困难点

1. **环境真实性**：需要完整的操作系统，支持任意应用程序的安装和运行。
2. **跨平台支持**：真实用户使用不同的操作系统（Linux, Windows, macOS）。
3. **任务多样性**：需要覆盖Web浏览、桌面应用、文件操作、跨应用工作流等。
4. **评估可靠性**：开放式任务的评估需要可靠的基于执行结果的验证方法。

## 解决方法

1. **真实计算机环境**：
   - 支持Ubuntu, Windows, macOS三大操作系统
   - 基于虚拟机，可完全复现
   - 支持任意应用安装和交互

2. **任务构建**：
   - 369个源自真实计算机使用场景的任务
   - 涵盖Web应用、桌面应用、OS文件I/O、跨应用工作流
   - 每个任务包含详细的初始状态配置和自定义执行评估脚本

3. **评估方法**：
   - 基于执行结果的评估（execution-based evaluation）
   - 比较任务执行后的系统状态与期望状态

4. **统一接口**：
   - 支持任务设置、执行评估、交互学习的统一框架

## 主要结果

- 人类成功率：**72.36%**
- 最佳模型成功率：**12.24%**
- 主要瓶颈：GUI定位（grounding）和操作知识（operational knowledge）不足。
- 为多模态通用Agent的开发提供了此前不可能的深入分析。

## 对本课题的启示

OSWorld展示了高保真度环境的价值，但其369个任务（每个需人工编写初始化和评估脚本）的构建成本极高。这直接激发了EvoCUA等工作中的**自动化任务和验证器合成**方法。OSWorld也成为了合成数据方法的重要下游评估平台。
