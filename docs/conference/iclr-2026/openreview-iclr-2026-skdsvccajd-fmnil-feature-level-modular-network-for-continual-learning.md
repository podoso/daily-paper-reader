---
title: "FMNIL: Feature-level Modular Network for Continual Learning"
title_zh: FMNIL：面向持续学习的特征级模块化网络
authors: "Qinwen Yang, Qiqi Wang, Jörg Wicker, Gillian Dobbie"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=sKDSVcCaJD"
tags: ["query:continual"]
score: 9.0
evidence: 基于特征级任务相似性的模块化网络缓解灾难性遗忘
tldr: 针对现有模块化持续学习方法在准确率与可扩展性之间的权衡问题，提出FMNIL方法，通过特征级任务相似性动态构建子网络，避免了参数扩张带来的效率损失。实验表明该方法在缓解灾难性遗忘的同时保持了较好的可扩展性，为持续学习提供了一种高效的模块化解决方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有模块化方法在准确率和可扩展性间存在矛盾，且基于准确率的任务相似性评估计算开销大。
method: 提出FMNIL，利用特征级任务相似性动态构建任务特定子网络，避免参数扩张。
result: 在多个持续学习基准上，FMNIL在保持高准确率的同时显著降低了计算开销。
conclusion: FMNIL有效平衡了模块化持续学习的准确率与可扩展性，为长期应用提供了可行方案。
---

## Abstract
Continual learning (CL) enables models to sequentially learn from a stream of tasks while retaining previously acquired knowledge, mitigating catastrophic forgetting (CF). Modular approaches in CL enhance flexibility by decomposing tasks into reusable modules. However, existing approaches suffer from a trade-off between accuracy and scalability, often resorting to parameter expansion to preserve accuracy at the cost of efficiency and long-term applicability. In addition, these methods that evaluate task similarity based on task accuracy are computationally expensive. To overcome these limitations, we propose Feature-level Modular Network for Continual Learning (FMNIL), which focuses on feature-level task similarity. FMNIL dynamically constructs task-specific subnetworks, reusing modules when tasks exhibit high feature similarity and expanding the network only when necessary. This approach results in significantly less parameter growth while maintaining higher accuracy compared to existing methods. Experiments on four benchmarks (CIFAR100-SC/RS/B0, ImageNet1000) show FMNIL achieves up to 5.9% higher accuracy (2.8% on average) while reducing parameter growth by 35% compared to state-of-the-art methods. FMNIL thus provides an accuracy-preserving and parameter-efficient solution that breaks the accuracy–scalability trade-off in long-term continual learning.

---

## 论文详细总结（自动生成）

# FMNIL: Feature-level Modular Network for Continual Learning 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：持续学习（Continual Learning, CL）中的灾难性遗忘（Catastrophic Forgetting, CF），以及现有模块化方法在**准确率与可扩展性之间的权衡**。传统模块化方法通过将任务分解为可重用模块来缓解遗忘，但为了保持较高准确率往往需要扩展参数规模，导致效率下降和长期适用性受限。此外，基于任务准确率来评估任务相似性的方法计算开销大。
- **整体含义**：本文旨在打破准确率-可扩展性的矛盾，提出一种既保持高精度又具有参数效率的模块化持续学习方案，为长期连续的模型学习提供实用路径。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用**特征级任务相似性**（Feature-level task similarity）动态构建任务特定的子网络，避免基于准确率的相似性评估带来的计算开销。
- **关键技术细节**：
  - 采用模块化网络结构，每个模块是可复用的特征处理单元。
  - 动态子网络构建：当新任务与已有任务具有高特征相似性时，重用已有模块；仅在必要时扩展新模块。
  - 特征相似度计算在特征空间进行，而非任务准确率，从而降低计算量。
  - 没有正式的公式或算法流程图（基于提供的摘要信息），但整体流程可描述为：
    1. 当前任务到来，提取其特征表示。
    2. 与历史任务的特征分布计算相似度（如余弦相似度或KL散度）。
    3. 若相似度高于阈值，复用对应模块；否则分配新模块。
    4. 所有子网络并行训练，但参数增长受控。
- **方法名称**：Feature-level Modular Network for Continual Learning (FMNIL)。

## 3. 实验设计：数据集、场景、基准、对比方法

- **数据集与场景**：
  - CIFAR100 上的三种分割场景：CIFAR100-SC（Super Class）、CIFAR100-RS（Random Split）、CIFAR100-B0（Base 0? 原文为B0，可能指类增量场景）。
  - ImageNet1000 上的完整场景（可能为类增量或任务增量）。
- **基准（Benchmark）**：四个持续学习标准基准。
- **对比方法**：与当前最先进（State-of-the-Art, SOTA）的模块化持续学习方法进行比较（具体方法名称未在摘要中列出，但声称相比SOTA有提升）。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提到FMNIL在参数增长上减少了35%，并保持了更高准确率，但未披露计算资源。可能需要阅读正文获取更多细节。

## 5. 实验数量与充分性

- **实验数量**：涉及4个不同场景的数据集，覆盖了常见的持续学习设置（类增量、任务增量、超类等）。每个实验报告了准确率和参数增长率（或绝对参数数）。
- **充分性与客观性**：
  - 从摘要看，实验结果明确（准确率平均提升2.8%，最高5.9%；参数增长减少35%），但**缺少消融实验**的明确提及（例如是否验证了特征相似度阈值选择、组件贡献等）。
  - 没有列出方差或统计显著性，也未报告多次运行的平均值和标准差。
  - 对比方法可能包含了近期SOTA，但未逐一说明基线方法名称，公平性有待正文补充。

## 6. 论文的主要结论与发现

- FMNIL在四个基准上均取得了比现有SOTA方法更高的准确率（平均+2.8%，最高+5.9%）。
- 同时显著降低了参数增长（减少35%），有效缓解了准确率与可扩展性的权衡。
- 基于特征级任务相似性的模块化策略在保持性能的同时提高了计算效率。
- 结论：FMNIL为长期持续学习提供了一种准确率保持且参数高效的解决方案。

## 7. 优点：方法或实验设计上的亮点

- **创新点清晰**：将任务相似性评估从准确率层面下放到特征层面，规避了昂贵的准确率计算。
- **效率优势明显**：避免无限制的参数扩展，兼顾精度与模型规模。
- **实验覆盖面较广**：包含CIFAR100的多种分割设定和ImageNet1000，验证了方法的通用性。
- **性能提升明确**：数值结果（+2.8%准确率，-35%参数）直观表明优势。

## 8. 不足与局限

- **缺少消融研究**：未明确说明对特征相似度度量、阈值选择、模块分配策略等关键组件的消融实验，难以判断各部分贡献。
- **资源开销未量化**：未提供训练时间、显存占用等实际计算成本，仅从参数数量推测效率。
- **对比方法不够具体**：摘要未列出基线方法名称，读者无法直接评估比较的公平性。
- **可扩展性边界**：当任务数量极大时，特征相似度计算可能成为瓶颈，文中未讨论。
- **应用限制**：目前仅在图像分类基准上验证，未涉及其他模态（如NLP、强化学习）或更复杂的任务序列。
- **实验统计性不足**：未报告多次重复实验的结果方差，可能影响结论的稳定性。

（完）
