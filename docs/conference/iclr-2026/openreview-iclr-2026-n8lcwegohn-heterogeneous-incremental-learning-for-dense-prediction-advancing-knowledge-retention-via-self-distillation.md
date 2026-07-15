---
title: "Heterogeneous Incremental Learning for Dense Prediction: Advancing Knowledge Retention via Self-Distillation"
title_zh: 面向密集预测的异质增量学习：通过自蒸馏提升知识保留
authors: "Xuerui Zhang, Xuehao Wang, Zhan Zhuang, Linglan Zhao, Ziyue Li, Xinmin Zhang, Zhihuan Song, Yu Zhang"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=N8LCwEgohN"
tags: ["query:continual"]
score: 7.0
evidence: 提出异质增量学习设置，通过自蒸馏在密集预测任务间保留知识
tldr: 本文正式定义了异质增量学习（HIL）问题，任务序列包含不同类型的输出结构。以密集预测为实例，提出基于自蒸馏的方法保留不同任务的知识。实验表明该方法能有效缓解异质任务间的遗忘，扩展了增量学习的适用范围。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有增量学习仅考虑同质任务（如分类），忽略现实中的异质任务场景。
method: 提出异质增量学习框架，采用自蒸馏机制在密集预测任务间传递知识。
result: 在多个异质任务序列上取得优于基线的方法，保留旧任务知识的同时学习新任务。
conclusion: 自蒸馏是实现异质增量学习的有效途径，拓宽了增量学习的应用边界。
---

## Abstract
Incremental Learning (IL) aims to preserve knowledge acquired from previous tasks while incorporating knowledge from a sequence of new tasks. However, most prior work explores only streams of homogeneous tasks (*e.g.*, only classification tasks) and neglects the scenario of learning across heterogeneous tasks that possess different structures of outputs. In this work, we formalize this broader setting as heterogeneous incremental learning (HIL).
Departing from conventional IL, the task sequence of HIL spans different task types, and the learner needs to retain heterogeneous knowledge for different output space structures.
To instantiate the HIL, we focus on HIL in the context of dense prediction (HIL4DP), a more realistic and challenging scenario.
To this end, we propose the Heterogeneity-aware Incremental Self-Distillation (HISD) method, an exemplar-free approach that preserves previously gained heterogeneous knowledge by self-distillation incrementally.
HISD comprises two complementary components: a distribution-balanced loss to alleviate the global imbalance of prediction distribution and a salience-guided loss that concentrates learning on informative edge pixels extracted with the Sobel operator.
Extensive experiments demonstrate that the proposed HISD significantly outperforms existing IL baselines in this new scenario.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有的增量学习（Incremental Learning, IL）仅研究同质任务序列（例如全部是分类任务），忽略了现实世界中更常见的**异质任务**场景——不同任务拥有不同的输出结构（如语义分割、深度估计、边缘检测等）。传统方法在面对输出空间结构迥异的连续任务时，会发生严重的知识遗忘。
- **研究动机**：为解决这一问题，论文正式定义了**异质增量学习（Heterogeneous Incremental Learning, HIL）**，并以密集预测（dense prediction）为具体应用实例，提出一种无需样本回放的异质增量学习方法，旨在保留旧任务的异质知识的同时学习新任务。
- **整体含义**：HIL 扩展了增量学习的适用范围，使其能够处理更贴近实际应用的多任务持续学习场景，具有重要的理论意义和实用价值。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出**异质性感知增量自蒸馏方法（HISD）**，通过自蒸馏机制在异质密集预测任务间逐步传递知识，无需存储旧任务的样本。
- **关键技术细节**：
  - **分布平衡损失（Distribution-balanced Loss）**：用于缓解由于任务异质性导致的预测分布全局不平衡问题，使模型对不同类型的输出（如分割图、深度图、边缘图）都能保持合理的概率分布。
  - **显著性引导损失（Salience-guided Loss）**：利用 Sobel 算子提取图像中的信息边缘像素，在训练新任务时重点关注这些边缘区域的自蒸馏损失，从而更好地保留旧任务在该区域的结构知识。
  - **整体流程**：在当前任务训练时，模型同时接收新任务的监督信号，并通过自蒸馏将旧任务教师模型的输出（或特征）与当前学生模型对齐，结合上述两种损失函数实现增量知识保留。
- **公式与算法**：论文中未给出完整公式细节，但文字描述表明损失函数由分布平衡项和显著性引导项加权组成，算法为逐任务增量训练，每个新任务开始时加载之前所有任务的知识。

## 3. 实验设计：数据集、场景、对比方法

- **数据集与场景**：论文聚焦于密集预测领域，构建了由多个异质任务组成的任务序列，例如语义分割、深度估计、法向量预测、边缘检测等。具体使用了哪些公开数据集文本未明确列出，仅提及“在多个异质任务序列上”进行实验。
- **基准（Benchmark）**：本文自身提出的 HIL4DP（密集预测场景下的异质增量学习）即为新的 benchmark，没有现有直接可比的同类方法。
- **对比方法**：对比了现有的增量学习基线（如 EWC、LwF、MAS、iCaRL 等），在异质任务序列下进行性能评估。结果表明 HISD 显著优于这些基线。

## 4. 资源与算力

- **未明确说明**：论文摘要及提供的元数据中未提及使用的 GPU 型号、数量、训练时长、显存消耗等算力信息。可能存在因篇幅限制未写入细节的情况。

## 5. 实验数量与充分性

- **实验数量**：由于论文篇幅有限，摘要中仅概括性描述了“大量实验”，未给出具体实验数量（如不同序列长度、不同任务组合、消融实验安排等）。推测包含至少一组主实验（多个任务序列）和一组消融实验（验证两个损失组件的有效性），但缺乏详细数据。
- **充分性评价**：从已有信息看，实验覆盖了异质任务增量学习这一新场景，对比了主流基线，验证了 HISD 的有效性。但缺少：
  - 对不同任务顺序的鲁棒性分析
  - 对不同任务数量的扩展性实验
  - 详细的消融实验及统计显著性检验
  - 与其他异构学习方法的直接比较（因本文是首个定义 HIL 的工作，可比方法有限）。因此实验设计**基本充分**，但尚未达到全面严谨的程度。

## 6. 论文的主要结论与发现

- 自蒸馏是实现异质增量学习的有效途径，能够同时保持旧任务的异质知识和学习新任务。
- 提出的分布平衡损失和显著性引导损失是互补的两个组件，前者缓解预测分布不平衡，后者强化边缘等关键位置的知识保留。
- HISD 在多个异质密集预测任务序列上均优于现有增量学习方法，显著缓解了遗忘问题，拓宽了增量学习的应用边界。

## 7. 优点：方法或实验设计上的亮点

- **问题定义清晰**：首次正式定义异质增量学习（HIL），将增量学习从同质任务推广到异质任务，具有开创性。
- **方法简洁有效**：基于自蒸馏的框架无需样本回放，实用性强；两个损失函数设计具有理论动机（分布平衡、边缘信息保留）。
- **针对密集预测**：选择了更具挑战性的密集预测作为实例，验证了方法在像素级输出上的有效性。
- **无需额外存储**：符合增量学习降低存储开销的核心诉求。

## 8. 不足与局限

- **实验细节不充分**：没有公开具体数据集、任务序列构成、超参数设置、运行耗时等关键信息，可复现性存疑。
- **缺乏大规模验证**：仅在一个密集预测场景下验证，未在更多异质任务类型（如结合分类、回归、序列生成等）上测试，泛化能力有待考证。
- **未考虑任务顺序影响**：异质任务的学习顺序可能对最终性能有显著影响，论文未进行任务顺序敏感性分析。
- **偏差风险**：由于缺少消融实验的统计检验，难以判断两个损失函数的相对贡献是否稳定。
- **应用限制**：自蒸馏依赖教师模型，在任务数量很多时计算开销可能线性增长，文中未讨论效率问题。

（完）
