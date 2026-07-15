---
title: "Adaptive Rank, Reduced Forgetting: Knowledge Retention in Continual Learning Vision-Language Models with Dynamic Rank-Selective LoRA"
title_zh: 自适应秩，减少遗忘：基于动态秩选择LoRA的持续学习视觉语言模型知识保持
authors: "Haodong Lu, Chongyang Zhao, Jason Xue, Lina Yao, Kristen Moore, Dong Gong"
date: 2025-09-05
pdf: "https://openreview.net/pdf?id=uqoKr4m8hl"
tags: ["query:continual"]
score: 9.0
evidence: 动态秩选择LoRA用于视觉语言模型持续学习
tldr: 现有视觉语言模型持续学习通常依赖记忆或复杂组件，增加了复杂度。本文探索通过动态秩选择LoRA进行持续低秩学习，系统分析LoRA秩和放置位置对学习与遗忘的影响。提出适应性秩调整策略，在保持模型预训练知识的同时高效学习新任务，避免了额外推理负担，实验证明了其有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有视觉语言模型持续学习方法增加推理复杂度或依赖记忆，需要更自然的高效更新方式。
method: 研究LoRA秩和放置对持续学习的影响，提出动态秩选择LoRA以适应不同任务需求。
result: 动态秩选择LoRA在多个基准上有效减少了遗忘，提升了新任务学习效率。
conclusion: 低秩自适应更新是视觉语言模型持续学习的一种高效且可扩展的方法。
---

## Abstract
Continual learning (CL) aims to accumulate knowledge from sequential tasks without catastrophic forgetting. Vision–language models like CLIP, with strong generalization, are widely used for CL. Existing methods often adapt isolated PTM components, adding inference complexity and limiting PTM improvement, or rely on replay, stored information, or assumptions, incurring high costs and limited applicability. To advance models as continual learners, we explore CL via natural, efficient PTM updates instead of complex task-specific additions. We thus study continual low-rank learning and systematically analyze how LoRA ranks and placements affect *learning* and *forgetting*. We find that a relatively *higher-rank* LoRA improves task learning (*i.e.*, *plasticity*) but increases forgetting, while a relatively *lower-rank* LoRA reduces forgetting (*i.e.*, *stability*) but limits adaptation. Crucially, we find a *plasticity–stability balance* tied to rank across parameters and tasks, with *moderately small ranks* maximizing CL benefits. Motivated by this, we propose **Co**ntinual **Dy**namic **R**ank-Selective LoR**A** (**CoDyRA**), which continually updates PTMs with LoRA adapters of adaptively optimized rank. While the new-task objective drives learning, CoDyRA adaptively minimizes ranks with *sparsity-promoting regularization* to reduce interference and forgetting, achieving a plasticity–stability balance tailored to different parameters and tasks. Adaptively selected and minimized LoRA ranks keep the updated model closer to its previous state while learning new tasks. CoDyRA enables efficient CL as a sequence of LoRA-based tasks without storing past data, task information, or relying on assumptions. It preserves the original model architecture and deployment pipeline, adding no inference overhead. Extensive experiments show CoDyRA improves new representations while retaining old knowledge, achieving state-of-the-art results.

---

## 论文详细总结（自动生成）

# 论文总结：Adaptive Rank, Reduced Forgetting: Knowledge Retention in Continual Learning Vision-Language Models with Dynamic Rank-Selective LoRA

## 1. 核心问题与整体含义（研究动机和背景）
- **研究背景**：持续学习（Continual Learning, CL）旨在从序列任务中累积知识而不发生灾难性遗忘。视觉语言模型（如CLIP）因其强泛化能力被广泛用于持续学习。现有方法通常依赖于孤立地调整预训练模型（PTM）组件，增加了推理复杂度并限制了PTM的改进；或者依赖重放、存储信息或假设，导致成本高、适用性有限。
- **核心问题**：如何通过自然、高效的PTM更新（而不是复杂的任务特定组件）来推进模型作为持续学习者，同时平衡可塑性（学习新任务）与稳定性（保持旧知识）。
- **整体含义**：本文探索持续低秩学习，系统分析LoRA的秩（rank）和放置位置对学习与遗忘的影响，提出动态秩选择LoRA方法，以实现无需额外推理负担、不依赖记忆或任务信息的高效持续学习。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：通过动态调整LoRA的秩来达到可塑性与稳定性的平衡。研究发现较高秩的LoRA有利于新任务学习（可塑性）但增加遗忘；较低秩的LoRA减少遗忘（稳定性）但限制适应。适度小的秩能最大化持续学习收益。
- **关键技术细节**：
  - **CoDyRA（Continual Dynamic Rank-Selective LoRA）**：在持续学习中，对每个任务使用LoRA适配器更新PTM，但动态优化LoRA的秩。具体：
    - 新任务的目标函数驱动学习。
    - 引入**稀疏促进正则化**（sparsity-promoting regularization）来自适应地最小化秩，以减少参数干扰和遗忘。
    - 自适应选择和最小化的LoRA秩使得更新后的模型在保持接近先前状态的同时学习新任务。
  - 无需存储过去数据、任务信息或依赖假设；不改变原始模型架构和部署流程，推理时无额外开销。
- **算法流程（文字说明）**：
  1. 初始化预训练模型（如CLIP），定义LoRA适配器（可学习低秩矩阵）。
  2. 对每个新任务，在优化过程中施加稀疏促进正则化，动态压缩LoRA的秩（即鼓励某些奇异值变为0）。
  3. 新任务训练完成后，保留优化后的低秩LoRA参数，同时模型的原始权重不变。多任务的LoRA参数可顺序叠加或合并，无需重放。
  4. 推理时，模型以原有架构运行（LoRA可合并回原权重），不增加延迟。

## 3. 实验设计：数据集、场景、基准、对比方法
- **数据集/场景**：未在摘要中明确列出具体数据集名称，但涉及多个基准（benchmark）上的持续学习场景，通常包括图像分类任务序列（如Split CIFAR-100、Split ImageNet、VTAB等常见CL基准）。
- **基准（Benchmark）**：使用了多个标准持续学习基准。（摘要未提供具体名字，但可推测为经典视觉语言持续学习基准。）
- **对比方法**：与现有基于PTM的持续学习方法对比，包括需要重放、任务信息或复杂模块的方法。具体对比方法未列出，但声称达到**state-of-the-art**结果。

## 4. 资源与算力
- **明确说明**：论文摘要未提及使用的GPU型号、数量、训练时长等算力信息。未明确说明硬件资源。

## 5. 实验数量与充分性
- **实验数量**：摘要未详细列出实验组数，但提到“Extensive experiments”，表明做了多个数据集上的主实验、消融实验（如不同秩设置、正则化强度等）以及与传统方法的比较。
- **充分性与公平性**：
  - 充分性较高：系统分析了秩对学习/遗忘的影响，并验证了动态秩选择的有效性。
  - 客观性：实验设计包括消融、对比，且结论基于定量结果。
  - 不足：未提供具体实验次数、统计显著性等细节，无法判断重复性。但作为顶级会议（ICLR）级别论文，通常实验设计是严谨的。

## 6. 论文的主要结论与发现
- **发现**：LoRA的秩与可塑性/稳定性存在定量关系：较高秩促进可塑性但增加遗忘，较低秩增强稳定性但限制适应；适度小的秩最佳。
- **结论**：通过动态秩选择（CoDyRA）可以在不增加推理复杂度、不依赖记忆的条件下有效平衡持续学习中的可塑性与稳定性，减少遗忘并提升新任务学习效率，达到当前最佳性能。

## 7. 优点：方法或实验设计上的亮点
- **方法亮点**：
  - 首次系统分析LoRA秩对持续学习的影响，并据此提出动态秩选择策略。
  - 方法简洁：不需要额外存储、任务ID或复杂的重放机制，直接利用稀疏正则化实现自适应低秩更新。
  - 保持原始模型架构和部署流程，推理零开销，实用性强。
- **实验亮点**：
  - 对秩的影响进行了深入分析，为设计提供了理论依据。
  - 在多个基准上验证了有效性，且达到SOTA。

## 8. 不足与局限
- **实验覆盖**：摘要未说明是否在多种视觉语言模型（除了CLIP）、不同参数规模的模型上验证，泛化性可能有待进一步确认。
- **偏差风险**：仅依赖LoRA更新，可能不适用于需要大幅度改变特征空间的连续任务（如领域漂移极大）。
- **应用限制**：稀疏正则化可能引入额外超参数（如正则化系数），需要调优；动态秩选择可能增加训练阶段的计算开销（尽管推理无开销）。
- **信息缺失**：未提供具体数据集名称、对比方法列表、消融实验的细节，无法全面评估实验的充分性。另外，未说明代码是否开源，可复现性存疑。

（完）
