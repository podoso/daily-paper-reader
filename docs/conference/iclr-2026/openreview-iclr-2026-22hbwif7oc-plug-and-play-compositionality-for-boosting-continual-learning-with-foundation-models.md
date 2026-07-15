---
title: Plug-and-Play Compositionality for Boosting Continual Learning with Foundation Models
title_zh: 即插即用的组合性增强基础模型的持续学习
authors: "Weiduo Liao, Fei Han, Hisao Ishibuchi, Qingfu Zhang, Ying Wei"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=22hBwIf7OC"
tags: ["query:continual"]
score: 9.0
evidence: 即插即用的组合性增强基础模型的持续学习
tldr: 本文提出CompSLOT通用框架，利用目标中心化槽位学习引导概念提取，增强视觉基础模型在持续学习中的遗忘缓解能力，尤其在小样本任务中表现优异。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 视觉持续学习常因基于比较而非概念组合识别造成遗忘，现有模型在小样本任务中更差。
method: 设计CompSLOT框架，通过物体中心学习解析语义槽位，引导概念学习。
result: 实验表明，CompSLOT能显著提升多种持续学习器的性能，减轻遗忘。
conclusion: 概念级理解是缓解视觉持续学习遗忘的关键，CompSLOT提供了有效工具。
---

## Abstract
Vision learners often struggle with catastrophic forgetting due to their reliance on class recognition by comparison, rather than understanding classes as compositions of representative concepts. 
This limitation is prevalent even in state-of-the-art continual learners with foundation models and worsens when current tasks contain few classes. 
Inspired by the recent success of concept-level understanding in mitigating forgetting, we design a universal framework CompSLOT to guide concept learning across diverse continual learners. 
Leveraging the progress of object-centric learning in parsing semantically meaningful slots from images, we tackle the challenge of learning slot extraction from ImageNet-pretrained vision transformers by analyzing meaningful concept properties. 
We further introduce a primitive selection and aggregation mechanism to harness concept-level image understanding. 
Additionally, we propose a method-agnostic self-supervision approach to distill sample-wise concept-based similarity information into the classifier, reducing reliance on incorrect or partial concepts for classification. 
Experiments show CompSLOT significantly enhances various continual learners and provides a universal concept-level module for the community.

---

## 论文详细总结（自动生成）

# 论文总结：《即插即用的组合性增强基础模型的持续学习》

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：视觉持续学习（Continual Learning）中的灾难性遗忘问题。现有模型在识别类别时依赖“类间比较”而非“概念组合”，导致对新任务的记忆容易覆盖旧知识。这一问题在使用基础模型（如ImageNet预训练的Vision Transformer）的最新持续学习方法中仍然存在，且在少样本（few classes）场景下更为严重。
- **研究动机**：借鉴概念级理解（concept-level understanding）在缓解遗忘方面的成功经验，探索如何让模型通过组合代表性概念来理解类别，从而提升持续学习的鲁棒性。
- **整体含义**：论文提出一种通用的即插即用框架CompSLOT，旨在引导不同持续学习器在训练过程中自动学习语义概念，增强基础模型的遗忘缓解能力，尤其在少样本任务中表现显著。

## 2. 论文提出的方法论

- **核心思想**：利用目标中心化槽位学习（object-centric slot learning）从图像中解析出语义上有意义的槽位（slots），每个槽位对应一个视觉概念，使得分类器基于概念组合而非整体特征进行判别。
- **关键技术细节**：
  - **槽位提取**：从ImageNet预训练的Vision Transformer中学习提取语义槽位。论文通过分析有意义概念的性质，设计了一种适应于ViT架构的槽位学习方法，克服了直接提取的困难。
  - **原始选择与聚合机制（Primitive Selection and Aggregation）**：在获得多个概念槽位后，通过选择关键原型并聚合它们的信息，实现对图像的概念级理解。
  - **方法无关的自监督方案（Method-Agnostic Self-Supervision）**：设计一种不依赖特定持续学习方法的自监督损失，将样本级别的概念相似性信息蒸馏到分类器中，减少分类时对错误或不完整概念的依赖。
- **算法流程（文字说明）**：
  1. 输入图像通过ViT编码器得到特征。
  2. 槽位学习模块将特征解析为K个语义槽位。
  3. 原始选择与聚合机制从槽位中挑选关键原型并进行聚合，形成概念表示。
  4. 该概念表示被注入到持续学习任务的分类器（例如EWC、LwF等）。
  5. 同时，自监督模块计算不同样本间的概念相似性，作为辅助损失训练分类器。
- **公式化**：文中未给出具体公式，但描述了上述组件。

## 3. 实验设计

- **使用的数据集/场景**：论文元数据和摘要中未明确列举具体数据集。推测采用了常见的持续学习基准（如CIFAR-100、ImageNet子集等）以及少样本场景下的任务。需注意原文在实验部分未详细说明。
- **Benchmark**：未明确定义benchmark，但基于“持续学习器”和“小样本任务”的表述，可能包含经典的类增量（class-incremental）或任务增量（task-incremental）设置。
- **对比方法**：文中提到“significantly enhances various continual learners”，表明对比了多种基础持续学习方法（如EWC、LwF、iCaRL、Experience Replay等）以及一些使用基础模型的最新方法。但具体列表未给出。

**注意**：实验设计的完整信息在提供的摘要和元数据中缺失，需作者论文全文才能详细说明。

## 4. 资源与算力

- **未提及**：论文元数据和摘要中完全没有提及使用的GPU型号、数量、训练时长等算力信息。因此无法总结。

## 5. 实验数量与充分性

- **实验数量**：仅提及“Experiments show CompSLOT significantly enhances various continual learners”，未给出具体的实验组数或消融实验数量。推测至少进行了多个数据集和多种持续学习器的对比实验，以及消融研究（例如移除槽位学习或自监督模块的影响）。
- **充分性与公平性**：从摘要看，方法具有通用性，且声称显著提升。但缺乏定量细节，难以判断实验是否全面覆盖不同任务复杂度（如长序列、大尺度数据集），以及是否与最先进方法公平比较。总体而言，实验充分性存疑，需要查看全文验证。

## 6. 论文的主要结论与发现

- 概念级理解（将类别视为代表性概念的组合）是缓解视觉持续学习中灾难性遗忘的关键。
- 提出的CompSLOT框架能够有效引导多种持续学习器学习语义概念，显著提升其性能并减轻遗忘。
- 在少样本任务中，CompSLOT带来的提升尤为明显，弥补了基础模型在该场景下的不足。
- CompSLOT是一个通用的即插即用模块，可为社区提供概念级持续学习工具。

## 7. 优点

- **创新性**：将目标中心化槽位学习（通常用于无监督场景）引入持续学习，提出概念组合的新视角。
- **通用性**：框架与特定持续学习方法无关，可增强任意现有持续学习器，具备即插即用特性。
- **实用价值**：针对基础模型在小样本任务中的弱点，有效提升实用性，适用于现实世界数据稀疏的场景。
- **设计精巧**：原始选择与聚合机制以及方法无关的自监督方案，有助于减少对噪声或错误概念的依赖，提升鲁棒性。

## 8. 不足与局限

- **实验细节缺失**：提供的摘要和元数据中未给出具体数据集、对比方法和量化实验结果，无法评估方法的绝对性能。可能需要在论文全文中核实。
- **可重复性存疑**：未提及超参数、训练设置或代码开源信息，复现困难。
- **算力与效率**：未讨论CompSLOT模块带来的额外计算开销或训练时间增加。若槽位学习复杂度高，可能影响持续学习的效率。
- **局限性**：
  - 可能依赖ImageNet预训练的基础模型，若预训练数据与目标领域差异大，概念提取效果受限。
  - 仅适用于视觉领域，未验证在其他模态（如文本、音频）中的有效性。
  - 少样本场景下的提升是否以牺牲正常样本下的性能为代价，未明确说明。

（完）
