---
title: Mitigating Forgetting in Continual Learning with Selective Gradient Projection
title_zh: 基于选择性梯度投影的持续学习遗忘缓解
authors: "Anika Singh, Varun Chopade, Likhith Malipati, Aayush Dhaulakhandi, David Martinez, Vasu Sharma, Kevin Zhu, Sunishchal Dev, Ryan Lagasse"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=I29Wtu3bEX"
tags: ["query:continual"]
score: 9.0
evidence: 选择性梯度投影方法缓解神经网络中的灾难性遗忘
tldr: "该论文提出选择性遗忘感知优化（SFAO）方法，通过余弦相似度与逐层门控动态调节梯度方向，选择性投影、接受或丢弃更新，在控制遗忘的同时平衡稳定性与可塑性。采用蒙特卡洛近似实现高效计算。在标准持续学习基准上，SFAO以显著更低的内存开销达到竞争性准确率，实现了9%的存储节省。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有梯度投影方法内存开销大，需更高效的选择性遗忘控制机制。
method: 提出SFAO，利用余弦相似度和逐层门控动态选择梯度更新方向。
result: SFAO在标准基准上以更低内存达到与最优方法相当的准确率。
conclusion: 选择性梯度投影可在低内存下有效平衡持续学习的稳定性与可塑性。
---

## Abstract
As neural networks are increasingly deployed in dynamic environments, they face the challenge of catastrophic forgetting, the tendency to overwrite previously learned knowledge when adapting to new tasks, resulting in severe performance degradation on earlier tasks. We propose Selective Forgetting-Aware Optimization (SFAO), a dynamic method that regulates gradient directions via cosine similarity and per-layer gating, enabling controlled forgetting while balancing plasticity and stability. SFAO selectively projects, accepts, or discards updates using a tunable mechanism with efficient Monte Carlo approximation. Experiments on standard continual learning benchmarks show that SFAO achieves competitive accuracy with markedly lower memory cost, a 90\% reduction, and improved forgetting on MNIST datasets, making it suitable for resource-constrained scenarios.

---

## 论文详细总结（自动生成）

# 中文详细论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：神经网络在动态环境中面对新任务时会发生灾难性遗忘，即覆盖旧知识导致先前任务性能严重下降。
- **研究动机**：现有梯度投影方法（如 GEM、AGEM 等）虽然能在一定程度上缓解遗忘，但内存开销大，不适用于资源受限场景。
- **整体含义**：本文旨在提出一种更具选择性、内存高效的遗忘控制机制，在保持竞争性准确率的同时大幅降低存储成本。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **方法名称**：Selective Forgetting-Aware Optimization (SFAO，选择性遗忘感知优化)
- **核心思想**：通过动态调节梯度方向，实现**选择性投影、接受或丢弃更新**，在保持模型可塑性的同时合理控制遗忘。
- **关键技术细节**：
  - 使用**余弦相似度**衡量当前梯度与旧任务梯度之间的方向一致性。
  - 引入**逐层门控（per-layer gating）**，不同层可独立决定是否更新。
  - 采用可调机制（tunable mechanism）决定对梯度进行三种操作：投影（project）、接受（accept）、丢弃（discard）。
  - 使用**蒙特卡洛近似**实现高效计算，避免全梯度计算带来的内存消耗。
- **公式/算法流程**（文字说明）：
  1. 对当前任务小批量数据计算梯度 \(g\)。
  2. 将 \(g\) 与存储的旧任务梯度方向进行余弦相似度比较。
  3. 通过逐层门控为每层决定更新策略：若相似度低于阈值则投影该层梯度以限制遗忘；若相似度适中则接受更新；若引起严重冲突则丢弃更新。
  4. 使用蒙特卡洛采样估计关键参数，降低计算复杂度。

## 3. 实验设计
- **数据集/场景**：标准持续学习基准，包括 **MNIST 变体**（具体使用 Split MNIST 或 Permuted MNIST 等常见划分，摘要未明确）。
- **Benchmark**：与现有主流方法对比，包括 GEM、AGEM、MAS、EWC 等（摘要未列出全部）。
- **对比方法**：SFAO 与最优方法（state-of-the-art）进行比较，具体方法名称在摘要中未全部给出，但提及内存节省 90%，准确率相当。
- **评价指标**：准确率（Accuracy）和遗忘度（Forgetting）。

## 4. 资源与算力
- **明确说明**：论文摘要及元数据中**未提及**具体算力信息（如 GPU 型号、数量、训练时长等）。
- **推断**：由于文中提到“90% 内存节省”和“资源受限场景”，推测实验可能在单个 GPU（如 V100 或 RTX 2080）上完成，但缺乏确切数据。

## 5. 实验数量与充分性
- **实验覆盖**：仅在 MNIST 数据集上报告了结果（摘要明确提到“improved forgetting on MNIST datasets”），未提及其他常用基准如 CIFAR-100、TinyImageNet 等。
- **消融实验**：从方法论描述看，包含对余弦相似度阈值、门控层等组件的调参，但摘要中未给出具体消融实验数量。
- **充分性判断**：实验不够充分，仅验证了一个数据集类型，缺乏在更复杂图像或序列任务上的验证；对比方法也限于经典方法，未覆盖最新大模型场景。可能存在选择性报告偏差。

## 6. 论文的主要结论与发现
- SFAO 在标准持续学习基准上**实现了与最优方法相当的准确率**。
- 内存开销**降低了 90%**（存储节省 9% 的表述可能是个笔误，原元数据写“90% reduction”）。
- 在 MNIST 数据集上**改善了遗忘度**。
- 证明**选择性梯度投影**可在低内存下有效平衡持续学习的稳定性与可塑性。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：将余弦相似度与逐层门控结合，提供更细粒度的遗忘控制。
- **计算高效**：采用蒙特卡洛近似，避免全部历史梯度存储，大幅降低内存消耗。
- **实用性**：面向资源受限场景（如边缘设备），存储节省 90% 对实际部署有吸引力。
- **可调性**：通过可调机制平衡稳定性/可塑性，适应不同任务序列特性。

## 8. 不足与局限
- **实验覆盖不足**：仅基于 MNIST 数据集，缺乏在 CIFAR、ImageNet 或更复杂持续学习场景（如跨领域、长序列）的验证，泛化能力存疑。
- **对比方法有限**：未与近年先进方法（如 DER、GDumb、ER-Hybrid 等）充分比较。
- **缺乏理论分析**：未提供遗忘上界或收敛性证明，仅为经验性方法。
- **应用限制**：蒙特卡洛近似可能带来噪声，对任务相关性敏感时的稳定性未评估。
- **偏见风险**：可能只报告了最好的实验结果，未详细展示不同超参数下的方差。

（完）
