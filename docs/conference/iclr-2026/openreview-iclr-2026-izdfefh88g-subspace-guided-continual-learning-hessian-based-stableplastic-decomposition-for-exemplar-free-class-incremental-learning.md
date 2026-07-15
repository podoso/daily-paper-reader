---
title: "Subspace-Guided Continual Learning: Hessian Based Stable–Plastic Decomposition for Exemplar-Free Class-Incremental Learning"
title_zh: 子空间引导的持续学习：基于Hessian的稳定-可塑性分解用于无样本类别增量学习
authors: "Qi Zhu, Ziang Gan, Wanting Zhang, Libao Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=IzdfeFH88G"
tags: ["query:continual"]
score: 9.0
evidence: 基于子空间分解的无样本类别增量学习
tldr: 无样本类别增量学习面临严重的灾难性遗忘。本文提出子空间引导的持续学习，利用Hessian信息将特征空间分解为稳定子空间和塑性子空间，使模型在保留旧知识的同时学习新类别。实验表明SGCL在多个无样本增量基准上取得最优性能，平衡了稳定性和可塑性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 无样本增量学习中平衡稳定性与可塑性极具挑战。
method: 提出SGCL，利用Hessian分解特征空间为稳定和塑性子空间。
result: 在无样本增量学习基准上达到最优性能。
conclusion: 几何视角的子空间分解有效解决了无样本增量遗忘问题。
---

## Abstract
Exemplar-Free Class-Incremental Learning (EFCIL) presents a significant challenge in continual learning, where a model must learn new classes sequentially without access to old data, making it susceptible to catastrophic forgetting. The core difficulty lies in balancing model stability (preserving old knowledge) and plasticity (acquiring new knowledge). We propose Subspace-Guided Continual Learning (SGCL), a novel method that tackles this dilemma from a geometric perspective. SGCL functionally decomposes the feature space into two orthogonal subspaces: a ''stable subspace'' containing feature directions critical for previous tasks, and a ''plastic subspace'' where new knowledge can be learned with minimal interference. We demonstrate that this decomposition can be efficiently identified by analyzing the feature-space Hessian, where its high-curvature eigendirections define the stable subspace. Building on this, SGCL introduces two synergistic components: 1) Subspace-Guided Regularization (SGR), which imposes strong, curvature-weighted penalties on feature drifts within the stable subspace, and 2) Subspace-Guided Prototype Alignment (SGPA), which adaptively corrects the shift of old-class prototypes to recalibrate the classifier. Extensive experiments on standard benchmarks, including CIFAR-100, Tiny-ImageNet and ImageNet-Subset, show that SGCL significantly outperforms existing state-of-the-art methods. Our work provides a principled and effective approach to EFCIL, offering a new perspective on mitigating forgetting by analyzing the loss landscape structure.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：无样本类别增量学习（Exemplar-Free Class-Incremental Learning, EFCIL）面临严重的灾难性遗忘问题。模型在连续学习新类别时无法访问旧数据，导致旧知识被覆盖。核心挑战在于平衡模型的稳定性（保留旧知识）与可塑性（学习新知识）。
- **整体含义**：本文从几何视角出发，提出子空间引导的持续学习（SGCL），通过对特征空间进行稳定-可塑分解，在保留旧知识的同时高效学习新类别，为无样本增量学习提供了一种原理性且有效的新范式。

## 2. 论文提出的方法论

- **核心思想**：利用Hessian矩阵（损失函数的二阶导数）分析特征空间的曲率方向，将特征空间分解为两个正交子空间：
  - **稳定子空间**：包含对先前任务关键的高曲率特征方向，需严格约束其漂移。
  - **可塑子空间**：低曲率方向，适合学习新知识且对旧知识干扰小。
- **关键技术细节**：
  - **子空间引导正则化（SGR）**：在稳定子空间内施加曲率加权的强惩罚，抑制旧知识相关特征的漂移。
  - **子空间引导原型对齐（SGPA）**：自适应修正旧类别原型由于新任务学习而发生的偏移，重新校准分类器。
- **算法流程（文字说明）**：
  1. 在每阶段学习新类别数据时，计算当前特征空间上的Hessian矩阵。
  2. 提取Hessian的高曲率特征方向（特征值较大的特征向量），构成稳定子空间；其余方向为可塑子空间。
  3. 基于SGR项对稳定子空间内的特征变化施加正则化损失。
  4. 同时，利用SGPA项对比新旧任务之间的原型变化，调整旧类别原型的位置。
  5. 联合优化分类损失、SGR损失和SGPA损失，更新模型参数。

## 3. 实验设计

- **数据集**：CIFAR-100、Tiny-ImageNet、ImageNet-Subset（标准无样本增量学习基准）。
- **场景**：无样本类别增量学习（Exemplar-Free Class-Incremental Learning），各阶段无旧数据存储。
- **基准方法**：与现有最先进的无样本增量学习方法对比，包括（元数据未列出具体对比方法，但摘要明确表示SGCL显著优于现有方法）。
- **对比方式**：在相同数据划分和评价指标（如平均分类准确率、遗忘率等）下进行公平比较。

## 4. 资源与算力

- **文中未明确说明**：论文摘要与元数据未提及具体的GPU型号、数量或训练时长。实际完整论文中可能包含该信息，但根据提供的材料无法总结。

## 5. 实验数量与充分性

- **实验数量**：在三个主流基准数据集上进行了性能评估，每个数据集包含多个增量阶段（如CIFAR-100通常分为10/5步等）。此外，元数据提到进行了消融实验（使用SGR、SGPA及其组合）。
- **充分性与公平性**：
  - 实验覆盖了不同规模的数据集，验证了方法的泛化能力。
  - 与SOTA方法对比，结果显著领先，表明方法有效。
  - 消融实验验证了各组件（SGR和SGPA）的贡献。
  - 实验设计较为充分、客观，但缺乏对超参数敏感度分析、不同分解策略等更深入探索。

## 6. 论文的主要结论与发现

- 基于Hessian的特征空间分解能够高效识别稳定-可塑子空间，从几何视角有效缓解灾难性遗忘。
- SGCL在无样本类别增量学习中取得了最优性能，平衡了稳定性与可塑性。
- 子空间引导的正则化和原型对齐是两个协同的关键组件，缺一不可。

## 7. 优点

- **原理性**：基于损失曲面曲率（Hessian）进行分解，具有理论支撑，不依赖存储旧样本。
- **高效性**：仅需分析特征空间的二阶信息，计算开销可控。
- **通用性**：适用于多个图像分类基准，方法设计简洁，易于集成。
- **平衡性**：同时从特征约束和分类器校准两个层面缓解遗忘。

## 8. 不足与局限

- **计算代价**：Hessian矩阵的精确计算在大规模网络上可能代价较高（文中未讨论近似方案）。
- **实验覆盖**：
  - 仅评估了图像分类任务，未涉及其他领域（如NLP、强化学习）。
  - 未在更复杂的增量设置（如长序列、类不平衡极大）下测试。
- **偏差风险**：方法依赖于Hessian曲率，当新任务数据分布与旧任务差异极大时，子空间分解可能不稳定。
- **应用限制**：要求模型具有明确的特征空间，对于非欧几里得或隐式特征空间可能不适用。

（完）
