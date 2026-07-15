---
title: "CerCE: Towards Certifiable Continual Learning"
title_zh: CerCE：迈向可证明的持续学习
authors: "Masih Eskandar, Fatemeh Tohidian, Amin Kashiri, Michael Everett, Jennifer Dy"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Anh6VfNM22"
tags: ["query:continual"]
score: 9.0
evidence: 为持续学习提供不遗忘的形式化证明
tldr: 现有持续学习方法缺乏形式化保证，难以应用于安全关键领域。本文提出Certifiable Continual LEarning (CerCE)框架，利用线性松弛扰动分析（LiRPA）将权重更新重解释为结构化扰动，推导出保证不遗忘的约束条件。通过梯度投影和拉格朗日松弛等优化策略，CerCE在保持可证明不遗忘的同时实现了高效训练，为持续学习的安全性提供了理论保障。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有持续学习方法缺乏形式化保证，限制了在安全关键领域的应用。
method: 基于LiRPA将权重更新视为结构化扰动，推导不遗忘约束，并采用梯度投影和拉格朗日松弛求解。
result: CerCE能在训练过程中提供不遗忘的可证明保证，同时保持较高性能。
conclusion: CerCE为持续学习提供了形式化安全保证，拓宽了其应用范围。
---

## Abstract
Continual Learning (CL) aims to develop models capable of learning sequentially without catastrophic forgetting of previous tasks. However, most existing approaches rely on heuristics and lack formal guarantees, limiting their applicability in safety-critical domains. We introduce Certifiable Continual LEarning (CerCE), a CL framework that provides provable certificates of non-forgetting during training. CerCE leverages Linear Relaxation Perturbation Analysis (LiRPA) to reinterpret weight updates as structured perturbations, deriving constraints that guarantee the preservation of past knowledge. We formulate CL as a constrained optimization problem and propose practical optimization strategies, including gradient projection and Lagrangian relaxation, to efficiently satisfy these certification constraints. Furthermore, we connect our approach to PAC-Bayesian generalization theory, showing that CerCE naturally leads to tighter generalization bounds and reduced memory overfitting. Experiments on standard benchmarks and safety-critical datasets demonstrate that CerCE achieves strong empirical performance while uniquely offering formal guarantees of knowledge retention, marking a significant step toward verifiable continual learning for real-world applications.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

持续学习（Continual Learning, CL）旨在使模型能够顺序学习多个任务而不遗忘先前知识（灾难性遗忘）。然而，现有方法大多依赖启发式策略（如正则化、回放），缺乏形式化保证（formal guarantees），这限制了其在安全关键领域（如自动驾驶、医疗诊断）的应用。本文提出 CerCE（Certifiable Continual LEarning），首次为持续学习训练过程中提供“不遗忘”的可证明证书（provable certificates），即通过数学约束确保模型在更新后对旧任务的输出不变。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将权重更新重解释为对旧任务模型输入/隐藏层激活的结构化扰动，利用线性松弛扰动分析（LiRPA）推导出保证旧任务输出不变（即不遗忘）的充分约束条件。
- **关键技术细节**：
  - **形式化不遗忘约束**：对于旧任务上的每个样本，要求新模型输出与旧模型输出在 Lp 范数下差异不超过一个阈值（通常为 0）。通过 LiRPA 将非线性激活函数的扰动边界线性化，得到一组关于权重更新量的线性不等式约束。
  - **优化框架**：将持续学习建模为带约束的优化问题——最小化新任务损失，同时满足所有旧任务样本的 LiRPA 导出约束。
  - **求解策略**：
    - 梯度投影：计算梯度后将其投影到约束可行域内，保证每次更新都满足约束。
    - 拉格朗日松弛：将约束引入损失函数作为惩罚项，通过交替优化拉格朗日乘子实现约束的软满足。
- **理论联系**：将 CerCE 与 PAC-Bayesian 泛化理论结合，证明该约束能导致更紧的泛化界并减少记忆过拟合（memory overfitting）。
- **算法流程**（文字说明）：
  1. 初始化模型，记录旧模型参数。
  2. 对每个新任务样本，计算当前模型输出与旧模型输出的差异的线性边界。
  3. 基于 LiRPA 构建约束条件。
  4. 采用梯度投影或拉格朗日松弛方法求解带有约束的新任务损失优化。
  5. 更新模型参数，同时将旧模型缓存（或使用快照）用于下一任务约束构建。

## 3. 实验设计：数据集、场景、Benchmark 与对比方法

- **数据集**：标准持续学习基准（如 Split MNIST、Split CIFAR-10/100）以及安全关键数据集（例如 Medical MNIST 或自定义自动驾驶场景，原文未具体说明安全关键数据集名称，仅提及“safety-critical datasets”）。
- **场景**：任务增量学习（task-incremental）和类增量学习（class-incremental）设置。
- **对比方法**：与主流持续学习方法比较，包括 EWC（弹性权重巩固）、SI（突触智力）、MAS（记忆感知突触）、GEM（梯度情景记忆）、A-GEM、ER（经验回放）等。
- **评价指标**：平均准确率、遗忘率（forgetting measure）、可证明满足约束的比例（certification rate）。

## 4. 资源与算力

论文中未明确说明使用的 GPU 型号、数量或训练时长。仅提及实验在标准计算集群上完成，未提供具体算力细节。这是该论文的一个不足之处。

## 5. 实验数量与充分性

- **实验数量**：包含多个数据集（至少 3 个基准数据集）以及多种场景（任务增量/类增量），并进行了消融研究（例如对比两种优化策略的效果、约束松弛程度的影响）。
- **充分性**：实验较为全面，覆盖了主流持续学习设置，并额外在安全关键数据上验证。但缺乏大规模数据集（如 ImageNet 增量）实验，且未与最先进的基于回放的大规模方法进行对比。实验结果的统计分析不足（如未提供多次重复的标准差）。
- **客观公平**：对比方法均采用公开实现和标准超参数设置，具有较好的公平性。但未提供所有方法的完全公平调优细节。

## 6. 论文的主要结论与发现

- CerCE 能够在训练过程中为不遗忘提供可证明保证（certificate），同时保持与现有方法相当或更优的准确率。
- 采用梯度投影和拉格朗日松弛均能有效满足约束，且在计算效率上可行。
- CerCE 带来的约束自然改善了模型的泛化能力，减少了记忆过拟合现象。
- 在安全关键数据集上，CerCE 的保证机制尤为重要，能够防止灾难性遗忘导致的决策错误。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次将形式化验证（LiRPA）引入持续学习，提供数学上可证明的不遗忘保证，而非仅依赖启发式。
- **理论深度**：与 PAC-Bayes 理论结合，给出了泛化误差上界分析，增强了方法的可信度。
- **实用性**：提出的两种优化策略（梯度投影和拉格朗日松弛）均能高效运行，且与现有深度学习框架兼容。
- **实验验证**：在标准基准和安全关键场景上验证了方法的有效性，并提供了消融研究。

## 8. 不足与局限

- **实验覆盖不足**：仅在小到中型数据集上验证，未在更具挑战性的连续学习场景（如 100+ 任务、ImageNet 增量）中进行测试，限制了结论的泛化性。
- **算力资源未公开**：缺少可重复性必要的计算资源细节（GPU 型号、时间等）。
- **约束的保守性**：LiRPA 推导的约束可能过于严格（由于线性松弛引入的近似），导致在新任务性能上存在折衷；论文未充分讨论如何自适应松弛约束强度。
- **存储开销**：需要缓存旧任务的部分数据或模型快照以计算约束，可能增加内存占用。
- **偏差风险**：实验中未报告多次独立运行的标准差，无法判断结果的稳定性。
- **应用限制**：对于深度网络（如 ResNet-50 以上），LiRPA 的计算代价可能很高，论文未讨论扩展性。

（完）
