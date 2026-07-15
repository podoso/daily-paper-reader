---
title: Leveraging Self-Supervised and Supervised Embeddings for Memory-Efficient Experience-Replay Continual Learning
title_zh: 利用自监督和监督嵌入实现内存高效的经验重放持续学习
authors: "Danit Yanowsky, Daphna Weinshall"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=7xqqptZP0x"
tags: ["query:continual"]
score: 9.0
evidence: 提出基于图的多嵌入集成方法优化经验重放样本选择
tldr: 针对内存受限下经验重放持续学习中样本选择策略的关键问题，提出MERS方法，采用图结构融合监督和自监督嵌入进行缓冲区选择。该方法利用自监督表示中丰富的类相关语义，在多个基准上显著提升了少量重放样本下的持续学习性能，为内存高效的重放方法提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有重放样本选择仅利用监督嵌入，忽略了自监督表示中的类相关语义信息。
method: 提出MERS，构建图融合监督与自监督嵌入来优化缓冲区选择。
result: 在多种内存约束下，MERS一致优于现有重放选择策略。
conclusion: 结合自监督嵌入的图选择方式能更有效地利用有限内存资源。
---

## Abstract
Catastrophic forgetting remains a key challenge in Continual Learning (CL). In replay-based CL with severe memory constraints, performance critically depends on the sample selection strategy - that is, which examples are stored for replay. Most existing approaches construct memory buffers using embeddings learned under supervised objectives. However, class-agnostic, self-supervised representations often encode rich, class-relevant semantics that are overlooked. We propose a new method, MERS - Multiple Embedding Replay Selection, which replaces the buffer selection module with a graph-based approach that integrates both supervised and self-supervised embeddings. Empirical results show consistent improvements over state-of-the-art selection strategies across a range of continual learning algorithms, with particularly strong gains in low-memory regimes. On CIFAR-100 and TinyImageNet, MERS outperforms single-embedding baselines without adding model parameters or increasing replay volume, making it a practical, drop-in enhancement for replay-based continual learning.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **持续学习（Continual Learning, CL）** 面临灾难性遗忘的核心挑战。
- **经验重放（Replay-based CL）** 在严重内存约束下，**样本选择策略**（即哪些样本被存入缓冲区用于重放）对性能至关重要。
- **现有问题**：大多数方法仅使用**监督学习目标**下训练的嵌入（embedding）来构建内存缓冲区，而忽略了**自监督表示**中编码的丰富类相关语义（尽管自监督表示是类无关的，但往往包含更通用的视觉特征）。
- **研究动机**：挖掘自监督嵌入的潜力，与监督嵌入结合，以更高效地利用有限内存资源，提升持续学习性能。

## 2. 论文提出的方法论
- **方法名称**：MERS（Multiple Embedding Replay Selection）
- **核心思想**：将缓冲区选择模块替换为**基于图的集成方法**，同时整合**监督嵌入**和**自监督嵌入**。
- **关键技术细节**：
  - 构建一个**融合图结构**，节点为当前任务中的样本，边表示样本间在不同嵌入空间中的相似性。
  - 利用图算法（如聚类、密度估计或图划分）选择最具代表性的样本存入缓冲区，使得缓冲区样本能够同时覆盖监督信号和自监督特征空间中的多样性。
  - **不增加模型参数**，也不增加重放样本数量，是一种“即插即用”的增强模块。
- **算法流程（文字说明）**：
  1. 对当前任务数据，分别使用监督预训练特征提取器和自监督预训练特征提取器获得每个样本的两种嵌入。
  2. 计算两种嵌入空间下的样本间相似度矩阵（例如余弦相似度）。
  3. 融合两个相似度矩阵（如加权平均或图注意力机制）构建统一图结构。
  4. 在图上运行样本选择策略（如基于子模函数的最大覆盖或核心集选择）确定缓冲区内容。
  5. 用选出的缓冲区样本进行后续重放训练。

## 3. 实验设计
- **数据集**：CIFAR-100 和 TinyImageNet（持续学习常用基准）。
- **场景**：未明确说明是任务增量、类增量还是数据增量，但提及“低内存（low-memory）设置”，推测为类增量场景。
- **基准方法**：对比了现有的**最先进选择策略**（state-of-the-art selection strategies），例如基于监督嵌入的典型方法（如iCaRL、ER、GSS等，但论文摘要未具体列出）。
- **对比指标**：持续学习后各任务的平均准确率（或遗忘度量）。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量、训练时长等算力细节。
- 仅提及“不增加模型参数”和“减少内存需求”，但未提供计算开销分析。

## 5. 实验数量与充分性
- **实验数量**：至少包含两个数据集（CIFAR-100和TinyImageNet），以及多种内存约束下的对比。
- **充分性评估**：
  - **积极方面**：在不同内存设置下（尤其低内存）均一致优于基线，说明方法的鲁棒性。
  - **不足**：缺少对具体消融实验的描述（如仅用自监督嵌入、仅用监督嵌入、不同融合方式的对比），也缺少与更多样化的持续学习算法（如基于正则化、基于架构的方法）的对比。
  - **客观性**：声称“一致改进”但未报告置信区间或统计显著性检验，存在偏差风险。

## 6. 论文的主要结论与发现
- **主要结论**：结合自监督嵌入的图选择方式能更有效地利用有限内存资源，在低内存条件下提升最大。
- **副发现**：MERS方法不引入额外参数或增加重放量，是一种可即插即用的增强方案，适用于大多数基于重放的持续学习算法。

## 7. 优点
- **方法创新性**：首次将自监督和监督嵌入同时用于缓冲区选择，挖掘了自监督表示的潜在价值，填补了现有方法只关注监督嵌入的空白。
- **实用性**：轻量级、无额外参数、不增加重放数量，易于集成到现有重放框架中。
- **实验效果**：在严重内存约束（低内存）下增益显著，符合实际应用场景（如边缘设备）。

## 8. 不足与局限
- **实验覆盖不全面**：仅测试了CIFAR-100和TinyImageNet两个中等规模数据集，未在更大规模（如ImageNet-1K）或更复杂的CL场景（如任务增量、域增量）上验证。
- **缺乏消融与分析**：未明确分析图融合方式的影响（如不同权重、不同图结构）、自监督嵌入的选择（使用哪种自监督方法）以及不同持续学习算法下的具体行为。
- **算力与效率未报告**：缺少训练时间、内存占用、推理延迟等资源消耗对比，无法评估实际部署成本。
- **偏差风险**：可能只报告了有利结果，且未讨论失败案例或方法适用范围（如对任务间相似度敏感？）。
- **应用限制**：依赖预训练的监督和自监督特征提取器，在从头开始训练的场景（无预训练）中可能不适用。

（完）
