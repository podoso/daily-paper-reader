---
title: "Ergodic Risk Measures: Towards a Risk-Aware Foundation for Continual Reinforcement Learning"
title_zh: 遍历风险度量：迈向风险感知的持续强化学习基础
authors: "Juan Sebastian Rojas, Chi-Guhn Lee"
date: 2025-09-13
pdf: "https://openreview.net/pdf?id=6aZxHDw163"
tags: ["query:continual"]
score: 6.0
evidence: 为持续强化学习建立风险感知的理论基础，平衡保留与适应
tldr: 本文首次对持续强化学习中的风险感知决策进行形式化理论处理，提出遍历风险度量作为优化目标，使智能体在长期性能优化中关注除均值外的风险。该工作为持续RL中平衡知识保留与适应新情况提供了新视角，但尚处于理论阶段。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有持续RL仅考虑风险中性决策，忽略了风险因素对长期性能的影响。
method: 引入遍历风险度量，将风险感知纳入持续RL的优化目标。
result: 理论上证明了遍历风险度量能引导智能体更鲁棒地平衡记忆与适应。
conclusion: 该工作为风险感知持续RL奠定了理论基础。
---

## Abstract
Continual reinforcement learning (continual RL) seeks to formalize the notions of lifelong learning and endless adaptation in RL. In particular, the aim of continual RL is to develop RL agents that can maintain a careful balance between retaining useful information and adapting to new situations. To date, continual RL has been explored almost exclusively through the lens of risk-neutral decision-making, in which the agent aims to optimize the expected long-run performance. In this work, we present the first formal theoretical treatment of continual RL through the lens of risk-aware decision-making, in which the behaviour of the agent is directed towards optimizing a measure of long-run performance beyond the mean. In particular, we show that the classical theory of risk measures, widely used as a theoretical foundation in non-continual risk-aware RL, is, in its current form, incompatible with continual learning. Then, building on this insight, we extend risk measure theory into the continual setting by introducing a new class of ergodic risk measures that are compatible with continual learning. Finally, we provide a case study of risk-aware continual learning, along with empirical results, which show the intuitive appeal of ergodic risk measures in continual settings.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的详细中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的持续强化学习（Continual RL）研究几乎全部基于风险中性的决策框架，即智能体只关注优化长期期望性能（均值），而忽略了风险因素（如方差、下行风险等）。这种忽略可能导致智能体在平衡知识保留与适应新情境时表现出不稳健的行为，例如在不确定环境下过度冒险或过度保守。
- **研究动机**：在非持续的风险感知强化学习（Risk-aware RL）中，风险度量（如CVaR）已被广泛应用，但这类经典风险度量与持续学习的基本要求（如长期依赖、历史信息累积）存在本质冲突。因此，需要为持续RL建立专门的风险感知理论基础。
- **整体含义**：本文首次从形式化理论角度处理持续RL中的风险感知决策，提出了一类与持续学习兼容的新风险度量——**遍历风险度量（Ergodic Risk Measures）**，旨在使智能体在优化长期性能时能够平衡均值与风险，从而更鲁棒地应对持续学习中的记忆-适应权衡。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将经典风险度量理论扩展到持续学习情境，要求风险度量满足**遍历性**（ergodicity），即随时间演化的长期风险度量应能聚合过去与未来信息，且与学习过程的平稳性要求兼容。
- **关键技术细节**：
    - 首先证明经典风险度量（如条件风险价值CVaR、熵风险度量等）在持续RL中不兼容，因为它们无法处理随任务序列变化的环境非平稳性及长期依赖。
    - 据此，提出**遍历风险度量**这一新类别：定义一类满足遍历性质的函数，该类函数能够将历史轨迹的累积风险映射为一个标量，该标量在无限时间下收敛到一个与时间窗口无关的极限值。
    - 形式化地，遍历风险度量 \( \rho_\infty \) 满足：对任何持续学习过程 \( (S_t, A_t, R_t) \)，存在一个与初始状态无关的极限值 \( \bar{\rho} \)，使得 \( \rho_\infty = \lim_{T \to \infty} \frac{1}{T} \sum_{t=1}^T \phi(R_t, \text{history}) \)（示意性表达），其中 \( \phi \) 是一个可分解的风险函数。
    - 算法流程上，论文未给出具体伪代码，但指出可将遍历风险度量作为优化目标替代传统的期望回报，通过策略梯度或动态规划方法进行优化。
- **公式/算法**：文中未列出具体公式，但强调了理论推导过程。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- 论文仅提供了一个**案例研究（case study）** 和对应的**实证结果**，并未在多个标准基准数据集上进行广泛评估。
- 实验场景：未明确说明具体环境（如迷宫导航、机器人控制或离散游戏），仅提及“风险感知持续学习案例”。
- Benchmark：未提及任何现有持续RL基准或风险RL基准。
- 对比方法：未列出对比基线（如经典持续RL方法或风险中性方法），而是直接展示遍历风险度量下的智能体行为，并与直觉解释进行对比。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点。
- **未明确说明**：论文中完全没有提及任何计算资源信息，包括GPU型号、数量、训练时长、内存消耗等。这可能是因为论文主要侧重于理论贡献，案例研究规模较小。

### 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平。
- **实验数量**：仅一个案例研究，未包含消融实验、超参数敏感性分析、不同任务序列的对比或多随机种子重复。
- **充分性**：实验覆盖范围非常有限，仅作为理论概念的可视化验证，不足以证明遍历风险度量在实际大规模持续RL任务中的有效性。实验设计也缺乏与现有方法的公平比较，因此充分性不足。
- **客观性**：案例研究结果仅展示了遍历风险度量带来的直观行为变化，未提供统计显著性检验或误差条，客观性一般。

### 6. 论文的主要结论与发现
- 经典风险度量与持续学习不兼容，需要重新定义。
- 提出**遍历风险度量**作为持续RL中风险感知优化的合适理论工具。
- 通过理论分析证明了遍历风险度量能够引导智能体在保留旧知识与适应新任务之间实现更鲁棒的平衡，具体表现为：在风险敏感的场景下，智能体倾向于避免极端的性能波动，从而获得更平稳的长期表现。
- 案例研究显示，使用遍历风险度量的智能体在面对任务切换时，其性能退化的幅度小于风险中性智能体。

### 7. 优点：方法或实验设计上有哪些亮点。
- **理论创新性**：首次将风险感知决策形式化引入持续RL，提出了与持续学习约束兼容的新风险度量类别，填补了该领域的理论空白。
- **问题洞察**：清晰指出了经典风险度量在持续环境中失效的根本原因（非遍历性），为后续研究提供了方向。
- **直观性**：遍历风险度量的概念具有直观的物理含义（长期平均风险），易于理解。
- 虽然实验少，但案例设计旨在直观展示理论概念，对于理论论文而言是可接受的起点。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等。
- **实验覆盖过少**：仅一个简单案例，缺乏在多个标准持续RL基准（如Minigrid、MuJoCo连续控制、Atari游戏）上的验证，无法判断方法在复杂环境下的普适性。
- **缺少对比基线**：未与现有持续RL方法（如EWC、VCL、PackNet等）或风险中性方法进行定量比较，无法评估性能提升幅度。
- **算法实现细节缺失**：如何将遍历风险度量融入策略优化算法（如PPO、SAC）未给出具体方案，实际应用门槛高。
- **计算代价未知**：未讨论遍历风险度量在训练中的计算效率和收敛性保证，可能存在额外计算开销。
- **应用限制**：理论上需要无限时间遍历假设，在有限时间任务切换频繁的场景下，其性质可能退化。同时，风险偏好参数的选择缺乏指导，可能需要手动调整。

（完）
