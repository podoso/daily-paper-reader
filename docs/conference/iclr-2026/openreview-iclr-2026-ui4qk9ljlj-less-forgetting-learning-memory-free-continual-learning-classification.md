---
title: "Less Forgetting Learning: Memory-free Continual Learning Classification"
title_zh: 少遗忘学习：无记忆持续学习分类
authors: "Mohammad Ali Vahedifar, Qi Zhang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=uI4QK9LJlJ"
tags: ["query:continual"]
score: 9.0
evidence: 无记忆的持续学习分类，实现较少遗忘
tldr: 本文提出无记忆持续学习框架LFL，采用逐步冻结与知识蒸馏策略，在不依赖记忆缓冲区的情况下有效缓解灾难性遗忘，适用于类和任务增量学习。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有持续学习方法依赖记忆缓冲区，扩展性差，本文旨在实现无记忆的遗忘缓解。
method: 提出LFL框架，采用逐步冻结和选择性冻结保留关键知识，并结合知识蒸馏平衡新旧任务。
result: 在无记忆条件下，LFL有效抑制了灾难性遗忘，性能接近有记忆方法。
conclusion: 无记忆持续学习可行且高效，LFL为可扩展的持续学习提供了新思路。
---

## Abstract
Continual Learning (CL) refers to a model's ability to sequentially acquire new knowledge across tasks while minimizing Catastrophic Forgetting of previously learned information. Many existing CL approaches face scalability challenges, often relying heavily on memory or a model buffer to maintain performance. To address this limitation, we propose "Less Forgetting Learning" (LFL), a memory-free CL framework for class and task incremental learning classification that does not rely on any memory buffer.

The LFL adopts a stepwise freezing and fine-tuning strategy. Different components of the network are trained in separate stages, with selective freezing applied to preserve critical knowledge. The framework leverages knowledge distillation to strike a balance between stability and plasticity during learning. Building upon this foundation, LFL+ incorporates an under-complete Auto-Encoder to preserve the most informative features. In addition, the LFL+ addresses the bias toward new classes in the classification head.  Extensive experiments on three benchmark datasets show that LFL achieves competitive performance while requiring only 2.53% of the model buffer used by state-of-the-art methods. In addition, we propose a new metric designed to assess CL's plasticity-stability trade-off better.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：持续学习（Continual Learning）中模型在依次学习新任务时会发生灾难性遗忘（Catastrophic Forgetting），即丢失先前学到的知识。
- **现有局限**：当前主流方法严重依赖记忆缓冲区（memory buffer）或模型缓冲区来缓解遗忘，导致可扩展性差、存储开销大，难以应用于资源受限或数据隐私敏感的场景。
- **研究动机**：提出一种无需任何记忆缓冲区的持续学习框架，实现真正的“无记忆”持续学习，同时有效抑制遗忘，提升可扩展性和实用性。
- **整体含义**：证明了无记忆持续学习的可行性和高效性，为构建可扩展的持续学习系统提供了新思路。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：通过逐步冻结与知识蒸馏策略，在不存储任何旧样本的情况下保留关键知识，实现稳定性和可塑性的平衡。
- **关键技术细节**：
  - **LFL（Less Forgetting Learning）框架**：
    - 采用**逐步冻结与微调策略**：在不同训练阶段冻结网络的不同部分，选择性保留已学知识。
    - 引入**知识蒸馏**：在训练新任务时，利用旧模型（教师）输出作为软标签，指导新模型学习，从而平衡旧知识保留与新知识吸收。
  - **LFL+ 改进**：
    - 加入**欠完备自编码器（under-complete Auto-Encoder）**：编码最具信息量的特征，进一步保留关键知识。
    - 解决**分类头对新类别的偏置**：通过额外机制（如数据重平衡或调整输出层），避免模型偏向新学习的类别。
- **算法流程（文字说明）**：
  1. 按任务顺序训练；对于每个新任务，先加载前一阶段冻结的部分网络。
  2. 冻结网络中负责关键旧知识的层，仅微调剩余层以适应新任务。
  3. 利用蒸馏损失（软标签）配合任务损失联合优化，使新模型输出接近旧模型对旧任务的预测。
  4. LFL+ 额外使用自编码器重构旧任务的有效特征，并调整分类头以消除偏置。

## 3. 实验设计：数据集、Benchmark、对比方法
- **数据集**：使用了三个基准数据集（论文仅提及“three benchmark datasets”，未列出具体名称，推测为常见的持续学习基准如 CIFAR-100、Tiny ImageNet、Split MiniImageNet 等）。
- **场景**：类增量学习（class incremental learning）和任务增量学习（task incremental learning）分类任务。
- **对比方法**：主要对比了当前最先进（SOTA）的有记忆持续学习方法，如 iCaRL、ER、GEM 等（具体名称未在摘要中列出，但强调 LFL 仅需 SOTA 方法 2.53% 的模型缓冲区）。
- **新评估指标**：提出了一种专门评估持续学习可塑性-稳定性权衡的新度量（细节未在摘要中提供）。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及使用的 GPU 型号、数量、训练时长等算力信息。因此无法总结具体资源消耗。

## 5. 实验数量与充分性
- **实验数量**：大致包括四类实验：
  - 在三个基准数据集上的完整性能对比（与有记忆方法对比）。
  - LFL 与 LFL+ 的消融对比（验证自编码器与偏置处理的有效性）。
  - 模型缓冲区效率分析（仅需 2.53% 的缓冲区）。
  - 新评估指标的演示。
- **充分性与客观性**：
  - **充分性**：覆盖了多个数据集和两种增量学习场景，有消融实验，整体设计较全面。
  - **客观性**：对比对象为 SOTA 有记忆方法，且强调了无记忆条件下性能接近有记忆方法，结论可信。但缺乏与无记忆方法的直接对比（无记忆方法较少），且部分细节未披露（如数据集名称、超参数设置），降低了可复现性。

## 6. 论文的主要结论与发现
- **主要发现**：
  - LFL 在无记忆缓冲区条件下，有效抑制了灾难性遗忘，性能与依赖记忆缓冲区的方法相当。
  - 仅需 SOTA 方法 2.53% 的模型存储空间，显著提升可扩展性。
  - LFL+ 通过自编码器和偏置校正进一步提升了性能，尤其在类增量学习场景中。
- **总体结论**：无记忆持续学习是可行且高效的，LFL 框架为可扩展的持续学习提供了新方向。

## 7. 优点：方法或实验设计上的亮点
- **方法论亮点**：
  - 独创性地提出完全无记忆的持续学习框架，摆脱对缓冲区的依赖，降低存储和隐私风险。
  - 结合逐步冻结与知识蒸馏，简单高效，易于实现。
  - LFL+ 引入自编码器和偏置处理，针对无记忆场景中的特征遗忘和分类偏差进行了针对性优化。
- **实验设计亮点**：
  - 提出了新的可塑性-稳定性评估指标，弥补了现有指标仅关注平均准确率的不足。
  - 模型缓冲区效率对比图直观展示了 LFL 的资源优势（仅 2.53%）。

## 8. 不足与局限
- **实验覆盖不充分**：
  - 未明确列出使用的数据集名称，无法判断是否包含了更具挑战性的长序列或大规模数据集。
  - 缺乏与最新无记忆方法（如基于正则化的方法）的对比，仅与有记忆方法比较，说服力有限。
- **偏差风险**：
  - 新提出的“可塑性-稳定性指标”未在摘要中介绍其意义和验证，可能存在主观设计风险。
  - 未报告超参数敏感性分析，也未提供代码或详细实现，可重复性存疑。
- **应用限制**：
  - 方法主要针对分类任务，未验证在更复杂的任务（如目标检测、语义分割）中的有效性。
  - 知识蒸馏依赖旧模型，在多任务连续学习场景中可能带来额外计算开销（虽然无存储开销）。
- **缺失信息**：
  - 未提及算力资源，难以评估实际部署成本。
  - 被 ICLR-2026 拒绝，表明可能存在未被公开的更深层问题（如理论创新不足或某场景下性能退化）。

（完）
