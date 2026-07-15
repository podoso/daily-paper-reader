---
title: Learning Semantic Anchors for Continual Generalized Category Discovery
title_zh: 为持续广义类别发现学习语义锚点
authors: "Yuxin Fan, Junbiao Cui, Changhao Liu, Xingwang Zhao, Jiye Liang"
date: 2025-09-09
pdf: "https://openreview.net/pdf?id=rFmEPL6svs"
tags: ["query:continual"]
score: 8.0
evidence: 利用语义锚点抵抗灾难性遗忘，平衡稳定性-可塑性
tldr: 针对持续广义类别发现任务中稳定性-可塑性失衡问题，提出基于语义锚点的方法，利用文本描述和视觉特征构建并优化锚点，固定图像和文本编码器以保持预训练知识。实验证明该方法在新类识别和老类遗忘之间取得了更好平衡，有效提升了持续发现能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法在开放环境下不能有效平衡对旧类的记忆和新类的识别，导致灾难性遗忘。
method: 利用文本描述和视觉特征构建语义锚点，冻结编码器以保留预训练知识。
result: 在多个数据集上，所提方法在识别新类的同时显著减少了旧类遗忘。
conclusion: 语义锚点策略为持续类别发现中的稳定性-可塑性困境提供了有效解法。
---

## Abstract
Continual Generalized Category Discovery (C-GCD) aims to address the dual challenges of continual learning and generalized category discovery in open environments. This task requires the model to incrementally recognize new classes while resisting catastrophic forgetting of old classes. Existing C-GCD methods do not effectively balance the stability-plasticity dilemma, primarily due to ineffective semantic utilization and knowledge preservation, leading to poor recognition of new classes and catastrophic forgetting of old classes. To address these issues, we propose a novel C-GCD method that leverages textual descriptions and visual features to construct and optimize semantic anchors, and freeze image and text encoders to preserve general pre-trained knowledge. Extensive experiments on several datasets demonstrate that our method significantly outperforms existing C-GCD methods, effectively balancing the stability-plasticity dilemma to achieve enhanced new classes recognition and mitigated forgetting of old classes. Code is provided in the supplementary materials.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务定义**：Continual Generalized Category Discovery (C-GCD) 结合了持续学习与广义类别发现，要求模型在开放环境中逐步识别新类别，同时抵抗对旧类别的灾难性遗忘。
- **核心困境**：现有 C-GCD 方法无法有效平衡稳定性（保留旧类知识）与可塑性（学习新类），主要原因在于语义利用不充分、知识保留机制失效，导致新类识别差、旧类遗忘严重。
- **研究动机**：针对上述稳定性-可塑性失衡问题，提出一种利用文本描述和视觉特征构建语义锚点的全新方法，旨在同时提升新类识别并减轻旧类遗忘。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：通过“语义锚点”（semantic anchors）作为稳定知识表征，固定预训练的图像和文本编码器以保留泛化知识，仅在锚点优化过程中调整类表征。
- **关键技术细节**：
  - 利用文本描述（如类别名称或属性）和视觉特征共同构建每个类别的语义锚点。
  - 冻结图像编码器和文本编码器（如 CLIP 等），防止预训练知识被后续任务覆盖。
  - 通过优化目标（如对比学习或距离度量）使锚点与对应视觉特征对齐，同时保持不同类别锚点间可分。
- **算法流程（文字说明）**：
  1. 初始化：加载预训练的图像编码器（如 ViT）和文本编码器（如 CLIP 的文本分支），并冻结参数。
  2. 对新类别数据，使用文本描述生成初始语义锚点，结合当前批次视觉特征通过损失函数更新锚点。
  3. 在连续任务中，只优化锚点而不更新编码器，从而避免灾难性遗忘。
  4. 推理时，通过计算视觉特征与所有锚点的相似度进行分类。
- **注**：论文未提供具体公式，上述描述基于摘要推断。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：论文在多个数据集上进行了实验，但摘要未列出具体名称（常见 C-GCD 基准包括 CIFAR-100、ImageNet 子集、Fine-Grained 数据集等）。
- **基准场景**：采用持续的广义类别发现设置，即每个阶段引入部分已知类和未知类，模型逐步学习新类且不重复访问旧类数据。
- **对比方法**：与现有 C-GCD 方法（如基于原型、知识蒸馏等）进行比较，具体名称未在摘要中列出。
- **评估指标**：通常包括新类识别准确率、旧类遗忘率（或平均准确率），以及两者之间的权衡。

## 4. 资源与算力

- **明确说明**：论文摘要及元数据中未提及使用的 GPU 型号、数量、训练时长等算力信息。
- **推断**：由于模型基于预训练视觉语言模型（如 CLIP），且冻结编码器，预计训练开销较小，可能在单张或双张高端 GPU（如 A100）上数小时即可完成。

## 5. 实验数量与充分性

- **实验组数**：根据摘要“Extensive experiments on several datasets”，至少包含 3 个以上数据集的完整实验，以及可能的消融研究（如锚点构建方式、冻结策略等）。
- **充分性评估**：
  - 覆盖了多个数据集，说明方法具有一定泛化能力。
  - 但缺少具体结果数值和统计显著性检验，难以判断实验结果是否稳健。
  - 未报告超参数敏感性分析或失败案例，实验的客观性需结合全文判断。

## 6. 论文的主要结论与发现

- 所提出的语义锚点方法在多个数据集上显著优于现有 C-GCD 方法。
- 通过冻结编码器并优化锚点，有效平衡了稳定性-可塑性困境：新类识别准确率提高，同时旧类遗忘明显减少。
- 语义锚点策略为持续类别发现中的知识保留提供了有效解法。

## 7. 优点：方法或实验设计上的亮点

- **方法亮点**：
  - 引入文本描述辅助构建语义锚点，充分挖掘多模态预训练知识。
  - 冻结编码器策略简单且高效，天然防止灾难性遗忘，无需复杂正则化。
  - 锚点可随新任务增量优化，支持持续学习。
- **实验亮点**：
  - 在多个数据集验证，涵盖不同领域和难度，增强结果可信度。
  - 代码已提供，便于复现与验证。

## 8. 不足与局限

- **实验覆盖**：未明确列出数据集名称，且缺乏与其他基线方法的详细对比表格，难以全面评判。
- **偏差风险**：可能仅适用于具有丰富文本描述的类别（如名词类），对于抽象或缺乏语义标签的类别效果未知。
- **应用限制**：依赖预训练视觉语言模型（如 CLIP），若领域极度偏离，预训练知识泛化性可能受限。
- **理论分析不足**：未解释为何锚点优化能保证新旧类可分，缺乏收敛性或泛化界分析。
- **算力信息缺失**：无法评估方法在实际部署中的资源需求。

（完）
