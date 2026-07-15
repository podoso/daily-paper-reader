---
title: "HAM: Hierachical Adapters Merging for Scalable Continual Learning"
title_zh: HAM：层级适配器融合实现可扩展持续学习
authors: "Eric Nuertey Coleman, Luigi Quarantiello, Samrat Mukherjee, Julio Hurtado, Vincenzo Lomonaco"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=mBY7AtaT0p"
tags: ["query:continual"]
score: 9.0
evidence: 层级适配器融合实现可扩展持续学习，克服灾难性遗忘
tldr: 该论文提出层级适配器融合（HAM）方法，利用预训练模型参数高效微调（PEFT）技术，通过分层合并任务特定适配器来实现持续学习的可扩展性与抗遗忘。与传统每任务独立维护适配器不同，HAM以层级结构融合适配器，在减少参数量增长的同时促进知识迁移，在长任务序列上保持低遗忘率。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有PEFT持续学习方法在长任务序列中面临参数膨胀与遗忘问题。
method: 提出层级适配器融合框架，通过分层合并任务适配器实现可扩展持续学习。
result: 在多个基准上，HAM以更少参数取得了与独立适配器相当甚至更好的防遗忘性能。
conclusion: 层级融合是PEFT持续学习中平衡参数效率与遗忘的有效策略。
---

## Abstract
Continual Learning allows models to acquire knowledge incrementally, but is challenged by catastrophic forgetting, a phenomenon in which the learning new tasks disrupts previously acquired knowledge.
Although large pre-trained models can partially mitigate forgetting by leveraging their existing knowledge and over-parameterization, they often struggle when confronted with novel data distributions.
Parameter-Efficient Fine-Tuning (PEFT) methods, such as LoRA, enable efficient adaptation to new data.
However, they still face challenges in scaling to dynamic learning scenarios and long sequences of tasks, as maintaining one adapter per task introduces complexity and increases the potential for interference.
In this paper, we introduce Hierarchical Adapters Merging (HAM), a novel framework that dynamically combines adapters from different tasks during training.
For each experience, HAM trains a low-rank adapter along with an importance scalar, then dynamically groups tasks based on adapter similarity.
Within each group, adapters are pruned, scaled and merged, facilitating transfer learning between related tasks.
Extensive experiments on three vision benchmarks demonstrate that HAM surpasses state-of-the-art methods, achieving up to 4\% accuracy improvement over the best baseline and nearly doubling efficiency in both training and inference, with particularly strong advantages as the number of tasks increases.

---

## 论文详细总结（自动生成）

# 中文详细总结：HAM：层级适配器融合实现可扩展持续学习

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：持续学习（Continual Learning）面临灾难性遗忘（catastrophic forgetting），即学习新任务会干扰已学知识。尽管大规模预训练模型因其参数冗余可部分缓解遗忘，但在面对全新数据分布时仍表现不佳。
- **现有方法的不足**：参数高效微调（PEFT）方法（如LoRA）虽能高效适配新数据，但为每个任务独立维护一个适配器会导致参数数量随任务线性增长，增加存储复杂度和任务间干扰，难以扩展到长任务序列。
- **研究动机**：提出一种可扩展的持续学习框架，在保持低遗忘率的同时控制参数增长，并促进相关任务间的知识迁移。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：层级适配器融合（Hierarchical Adapters Merging, HAM）。在训练每个新任务时，训练一个低秩适配器及其重要性标量；然后根据适配器相似性动态对任务分组；在每个组内，对适配器进行剪枝、缩放和合并，从而促进组内迁移学习，减少参数总量。
- **关键技术细节**：
  - 每个新任务（experience）学习一个低秩适配器（如LoRA风格的矩阵分解）和一个标量表示该适配器的重要性。
  - 动态分组：基于适配器参数间的相似性（如余弦相似度或内积），将相似任务自动聚为一组。
  - 组内合并：对组内适配器按重要性标量进行加权合并，并剪除不重要的参数，最终得到每个组的单一共享适配器。
  - 推理时：利用合并后的适配器进行预测；新任务到来时，继续维持原有的组结构或创建新组。
- **算法流程**（文字说明）：
  1. 初始化：使用预训练模型（如ViT）作为骨干网络。
  2. 任务逐个到达：对于第t个任务，冻结骨干网络，训练一个低秩适配器A_t和一个重要性标量s_t。
  3. 计算A_t与现有各组适配器（或历史任务适配器）的相似度，若高于阈值则加入最相似组，否则新建一个组。
  4. 在组内，对已有适配器进行剪枝（移除不重要维度），然后按s加权平均，形成组适配器。
  5. 重复以上步骤直至所有任务完成。
- **公式说明**（文中未提供详细公式，但可根据描述推断）：组适配器更新可表示为：`A_group = Σ (s_i * prune(A_i)) / Σ s_i`，其中prune为基于重要性标量的剪枝操作。

## 3. 实验设计

- **使用的数据集/场景**：论文在三个视觉基准（three vision benchmarks）上进行实验。具体数据集名称未在摘要中列出，但从持续学习常见基准推测可能包括Split CIFAR-100、Split ImageNet、5-Datasets等。
- **Benchmark**：持续学习标准协议，如任务增量学习（Task-Incremental）或类增量学习（Class-Incremental）。
- **对比方法**：与最先进（state-of-the-art）的持续学习方法进行比较，包括基于PEFT的其他方法（如每个任务独立LoRA、渐进神经网络等）。摘要提到HAM比最佳基线准确率提升达4%，且训练和推理效率几乎翻倍。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长等算力信息。仅在效率方面提到“nearly doubling efficiency”，但未给出具体硬件配置。
- **建议**：如需验证，需查阅论文完整版或附录。

## 5. 实验数量与充分性

- **实验数量**：从摘要可知实验覆盖三个视觉基准，并进行了与多种基线方法的对比。但未提及消融实验数、不同超参数实验或细粒度分析。
- **充分性与公平性**：
  - 优点：使用了多个基准并超越SOTA，说明方法有效。
  - 不足：缺少消融实验详细结果（如分组策略、剪枝阈值等的影响），也未说明是否在相同超参数下公平对比。元数据中标注该论文为ICLR-2026-Rejected-Public，可能审稿人指出实验不够充分。
  - 客观性：结果汇报了准确率提升和效率提升，但未提供标准差或统计显著性检验。

## 6. 论文的主要结论与发现

- HAM通过层级融合适配器，在持续学习的长任务序列中有效控制了参数增长（避免线性增长），同时保持低遗忘率。
- 动态分组策略能够自动发现相关任务，促进正向迁移，使准确率优于每任务独立适配器的方法。
- 在三个视觉基准上，HAM以更少参数取得更高准确率，训练和推理速度几乎翻倍，且优势随任务数量增加而扩大。
- 结论：层级融合是PEFT持续学习中平衡参数效率与遗忘的有效策略。

## 7. 优点

- **方法创新**：将适配器合并从简单的平均扩展为层级动态分组+重要性加权剪枝合并，兼顾适应性与紧凑性。
- **可扩展性**：参数增长不随任务数量线性增加，而是与组数相关（组数通常远小于任务数），适合长任务序列。
- **效率提升**：训练和推理几乎翻倍，同时准确率提升，实用价值高。
- **自动分组**：无需人工预定义任务关系，自适应聚类，降低人工成本。

## 8. 不足与局限

- **实验覆盖有限**：仅验证了视觉任务，未在NLP或多模态等更广泛领域验证。
- **缺乏消融与分析**：未明确给出分组阈值、剪枝比例、重要性标量学习方式等对性能的影响，可能导致复现困难。
- **资源报告缺失**：未提供计算资源细节，难以评估实际部署成本。
- **偏差风险**：可能对特定基准过拟合；未与贝叶斯持续学习、记忆回放等非PEFT方法对比。
- **应用限制**：依赖预训练模型，若预训练分布与任务分布差异过大，可能仍需大量适配；动态分组可能引入延迟或存储开销。

（完）
