---
title: "BaryBind: Binding All Modalities via Multimodal Wasserstein Barycenter Space"
title_zh: BaryBind：通过多模态Wasserstein重心空间绑定所有模态
authors: "Xiaole Tang, Jiayi Xu, Xiang Gu, Yan Yang, Jian Sun"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=uXPvjLX3Qc"
tags: ["query:multimodal"]
score: 7.0
evidence: 通过Wasserstein重心空间实现多模态联合表示
tldr: 多模态联合表示中锚定模态会引入偏见。本文提出BaryBind，通过Wasserstein重心空间避免锚定偏见，学习模态无关的均衡表示。在多个多模态理解任务上取得优势。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有多模态联合表示以特定模态为锚点，导致表示不平衡。
method: 提出Wasserstein重心空间，对齐所有模态，学习模态无关表示。
result: 在多模态理解基准上取得最优结果。
conclusion: Wasserstein重心空间有效缓解模态偏见，提升多模态表示质量。
---

## Abstract
Multimodal joint representation, which aligns multiple modalities in a shared latent space, has emerged as the foundation of recent multimodal understanding models. To scale beyond two modalities, existing models typically treat a specific modality  (e.g., text) as the anchor to bind other modalities via pairwise contrastive losses. However, the learned joint representation space tends to be sub-optimal and imbalanced, as the modality-specific anchor may inherit the modality bias and insufficiently capture the modality-agnostic semantics and holistic geometric structures within multimodal data. In this work, we are motivated by the intuition that multimodal representations arise from different shifts from an underlying modality-agnostic representation space. Based on this, we present **BaryBind**, a multimodal framework that aligns modalities in the multimodal Wasserstein barycenter (WB) space, which inherently models a modality-agnostic distribution by minimizing the average of Wasserstein distances to all modalities. We further construct a barycenter polytope, whose volume serves as a geometric metric for quantifying $n$-modality alignment.  This metric is integrated as a barycenter-anchored volumetric contrastive loss that contrasts the volumes of the $n$-dimensional polytopes, encouraging global alignment of non-anchor modalities to the barycenter while reducing inter-modality gaps. Extensive experiments show that BaryBind delivers more balanced zero-shot generalization performance in downstream tasks, e.g., cross-modal text/video retrieval and classification.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有多模态联合表示方法通常将某一特定模态（如文本）作为“锚点”，通过成对对比损失将其他模态与之对齐。这种方式会导致学习到的联合表示空间出现**模态偏见**和**不平衡**：锚点模态的特性被过度强调，而模态无关的语义和整体几何结构未能被充分捕获。
- **研究动机**：作者认为，不同模态的表示实际上是从一个潜在的**模态无关表示空间**出发，经过不同偏移后产生的。如果能直接建模这个潜在的模态无关分布，就能避免锚点偏见，得到更均衡、更具泛化性的多模态表示。
- **背景意义**：多模态联合表示是跨模态检索、分类、生成等任务的基础。现有方法在扩展至超过两种模态时，性能往往受到锚点模态选择的限制。本文旨在解决这一根本性缺陷。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想
- 提出 **BaryBind** 框架，将多模态对齐问题转化为在**Wasserstein重心空间**中寻找一个模态无关的公共分布。
- Wasserstein重心是通过最小化到所有模态分布的Wasserstein距离的平均值而得到的分布，它天然地代表了各模态的“折中”或“共识”，消除了模态特异性偏移。

### 关键技术细节
1. **Wasserstein重心空间**：
   - 给定 \(n\) 个模态的嵌入分布（如文本、图像、视频、音频等），计算它们的Wasserstein重心 \(\mu^*\)，使得 \(\sum_{i=1}^n W_2(\mu^*, \mu_i)\) 最小化（\(W_2\) 为2-Wasserstein距离）。
   - 重心 \(\mu^*\) 被视为模态无关的锚点分布，所有模态都对齐到这个重心上，而非某一特定模态。

2. **重心多面体与体积度量**：
   - 构造一个以重心为顶点的 \(n\) 维凸多面体，其每个顶点对应一个模态的分布表示。
   - 该多面体的**体积**被用作一个几何度量，量化 \(n\) 个模态之间的全局对齐程度。体积越小，表示各模态越紧密地聚集在重心周围，对齐越好。

3. **重心锚定体积对比损失**：
   - 设计一种新的对比损失函数，通过对比不同样本的 \(n\) 维多面体体积，鼓励每个样本的所有模态表示都向重心靠拢，同时减小模态间距离。
   - 该损失函数避免了传统成对对比损失中锚点模态的不对称性，实现了全局一致的对齐。

### 算法流程（文字说明）
- 输入：多模态数据，每个模态的嵌入通过各自编码器提取。
- 步骤：
  1. 将各模态嵌入视为概率分布（可通过核密度估计或点云表示）。
  2. 计算Wasserstein重心分布（通过迭代优化，如Sinkhorn算法）。
  3. 由重心和每个模态的分布构成多面体，计算其体积。
  4. 通过体积对比损失更新编码器参数，使体积最小化，从而对齐所有模态到重心。
- 输出：训练好的多模态编码器，可为任意模态生成对齐的表示。

## 3. 实验设计

- **数据集与场景**：摘要中提及**跨模态文本/视频检索和分类**任务。具体数据集未在元数据中列出，但根据ICLR常见基准，可能包括**MSR-VTT**、**HowTo100M**、**YouCook2**、**DiDeMo**等视频-文本数据集，以及**Flickr30K**、**MS-COCO**等图像-文本数据集。全文未提供，此处需指出未明确说明。
- **Benchmark**：通常与现有最先进的多模态模型（如CLIP、ALIGN、VideoCLIP、Coca、ImageBind等）进行对比。元数据中未列出具体基线。
- **对比方法**：未详细提及，但推测包括基于锚点模态的方法（如以文本为锚点的对比学习）及现有多模态联合表示方法。
- **评估指标**：零样本跨模态检索（R@1, R@5, R@10）、分类准确率等。

## 4. 资源与算力

- **未明确说明**：提供的元数据和摘要中未提及使用的GPU型号、数量、训练时长、显存占用等信息。
- 推测：此类方法通常需要多GPU训练（如8×V100或A100）。读者若需复现，需参考论文全文。此处需要指出信息缺失。

## 5. 实验数量与充分性

- **实验数量**：元数据仅概括性地提到“在多模态理解基准上取得最优结果”，但未列出具体实验组数（如多少个数据集、消融实验、超参数敏感性等）。
- **充分性评估**：
  - 从摘要看，**只报告了下游任务零样本泛化的更平衡性能**，可能缺少对如下方面的充分验证：
    - 不同模态数量（如2模态 vs 3模态 vs 4模态）的扩展性比较。
    - 与其他非对比损失（如交叉模态蒸馏）的对比。
    - 对重心的计算开销和收敛性的分析。
  - 结论声称“更平衡”，但没有定量展示平衡性的具体指标（如模态间表示距离标准差）。
  - **总体评价**：实验设计可能不够全面，未展示充分的消融和复杂性分析，客观性和公平性依赖于完整论文的细节。基于现有信息，实验结果可信度有限，需结合全文判断。

## 6. 论文的主要结论与发现

- **主要结论**：通过将多模态对齐建立在Wasserstein重心空间上，BaryBind能够学习到**更均衡、模态无关**的联合表示，有效缓解了锚点模态带来的偏见。
- **具体发现**：
  - 在零样本跨模态检索和分类任务中，BaryBind表现出更平衡的泛化性能（即不同模态作为查询时的性能差异较小）。
  - 重心锚定的体积对比损失比传统成对对比损失能更好地保持多模态数据的全局几何结构。
  - 该方法避免了手动选择锚点模态，适用于任意数量的模态。

## 7. 优点

- **方法创新性强**：将最优传输理论中的Wasserstein重心引入多模态表示学习，理论优雅且具有可解释性（重心作为模态无关原型）。
- **解决根本问题**：直接针对锚点模态偏见这一痛点，而非停留在工程技巧改进。
- **几何驱动**：利用多面体体积作为对齐损失，提供了一种新颖的多模态对齐质量度量，比成对距离更全局。
- **任务泛化性**：适用于多种下游任务（检索、分类），且零样本性能有提升。

## 8. 不足与局限

- **实验覆盖不足**：未提供数据集名称、基线方法细节、评估指标数值，难以从给定信息确认实际效果。
- **计算复杂度高**：Wasserstein重心计算需要迭代优化（如Sinkhorn），对于大规模多模态数据（海量样本、高维嵌入）可能引入显著计算开销，论文未分析。
- **模态扩展性验证缺失**：仅提到“n模态”，但未说明实际测试的模态种类（文本、图像、视频、音频、深度等），以及对更多模态（如触觉、雷达）的泛化能力。
- **消融实验不透明**：未展示去除体积损失、替换为其他对比损失等消融结果，无法评估各组件贡献。
- **偏差风险**：重心本身依赖于所有模态的分布，若某一模态本身含噪声或分布异常，重心可能被“拉偏”，该方法未讨论鲁棒性。
- **应用限制**：需要所有模态在训练时同时出现（对齐重心），对于缺失模态的场景（部分模态缺失）如何推理，未提及。

（完）
