---
title: "Detect, Decide, Unlearn: A Transfer-Aware Framework for Continual Learning"
title_zh: 检测、决策、遗忘：一种面向迁移感知的持续学习框架
authors: "Yiwen Wang, Diana Benavides-Prado, Yun Sing Koh"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=Lej4WvdpFE"
tags: ["query:continual"]
score: 9.0
evidence: 关注负迁移并通过遗忘机制来缓解灾难性遗忘的持续学习框架
tldr: "持续学习旨在从数据流中持续学习，但记忆过时知识可能导致负迁移，干扰新任务。本文受到人脑选择性遗忘的启发，提出DEtect, Decide, Unlearn in Continual lEarning (DEDUCE)框架，动态检测负迁移并通过混合遗忘机制加以缓解。实验表明该方法能有效减少负迁移，提升持续学习在新任务上的适应性，为持续学习提供了新的视角。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 持续学习中记忆过时知识会导致负迁移，阻碍新任务学习，需同时考虑保留和遗忘。
method: 提出DEDUCE框架，包含检测模块、决策模块和混合遗忘模块，动态识别并消除负迁移。
result: 实验证明DEDUCE能有效缓解负迁移，提升持续学习在新任务上的表现。
conclusion: 有效的持续学习不仅应保留知识，还应选择性遗忘无关知识以增强适应性。
---

## Abstract
Continual learning (CL) aims to continuously learn new tasks from data streams. While most CL research focuses on mitigating catastrophic forgetting, memorizing outdated knowledge can cause negative transfer, where irrelevant prior knowledge interferes with new task learning and impairs adaptability. Inspired by how the human brain selectively unlearns unimportant information to prioritize learning and to recall relevant knowledge, we explore the intuition that effective CL should not only preserve but also selectively unlearn prior knowledge that hinders adaptation. We introduce DEtect, Decide, Unlearn in Continual lEarning (DEDUCE), a novel CL framework that dynamically detects negative transfer and mitigates it by a hybrid unlearning mechanism. Specifically, we investigate two complementary negative transfer detection strategies: transferability bound and gradient conflict analysis. Based on this detection, the model decides whether to activate a Local Unlearning Module (LUM) to filter outdated knowledge before learning new task. Additionally, a Global Unlearning Module (GUM) periodically reclaims model capacity to enhance plasticity. Our experiments demonstrate that DEDUCE effectively mitigates task interference and improves overall accuracy with an average gain of up to 4.55\% over state-of-the-art baselines.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究背景**：持续学习（Continual Learning, CL）旨在从数据流中不断学习新任务，同时克服灾难性遗忘。然而，大多数研究仅关注如何保留旧知识，忽视了记忆过时知识可能导致**负迁移**——即无关的先前知识干扰新任务的学习，削弱模型的适应性。
- **核心问题**：如何动态检测并消除负迁移，实现真正有效的持续学习？
- **整体含义**：受到人脑选择性遗忘机制的启发，本文认为有效的持续学习不仅应保留知识，还应**主动、选择性地遗忘**那些阻碍新任务学习的旧知识，从而提升模型在新任务上的适应性与总体性能。

## 2. 方法论：核心思想、技术细节与算法流程

- **核心思想**：提出 **DEDUCE** 框架（DEtect, Decide, Unlearn in Continual lEarning），包含三个模块：检测模块、决策模块和混合遗忘模块，动态识别并消除负迁移。
- **关键技术细节**：
  - **负迁移检测策略**（两种互补方式）：
    1. **可迁移性界限（Transferability Bound）**：计算模型在旧任务上的损失下降与新任务损失下降之间的相关性，若旧任务知识对新任务有负面作用，则界限为负。
    2. **梯度冲突分析（Gradient Conflict Analysis）**：计算旧任务梯度与新任务梯度的余弦相似度，若冲突较大（相似度为负），则判定存在负迁移。
  - **决策模块**：基于检测结果决定是否激活局部遗忘模块（LUM，Local Unlearning Module）——在**学习新任务之前**，对导致负迁移的旧知识进行过滤。
  - **混合遗忘机制**：
    - **局部遗忘模块（LUM）**：针对检测到的具体冲突旧知识进行定向遗忘，通过梯度上升或最大化旧任务损失来实现。
    - **全局遗忘模块（GUM，Global Unlearning Module）**：**周期性**地清理模型中长期积累的冗余/过时知识，以释放模型容量、增强可塑性。
- **算法流程（文字描述）**：
  1. 新任务到达时，首先使用检测模块评估当前模型对新任务的负迁移程度（可同时使用两种策略投票）。
  2. 若检测到显著负迁移，则决策模块触发 LUM，在新任务学习之前对冲突的旧知识进行局部遗忘。
  3. 完成遗忘后，使用标准持续学习方法（如 EWC、MAS 等）学习新任务。
  4. 每隔若干任务或固定步数，触发 GUM 进行一次全局遗忘，清理模型中的不相关知识。
  5. 重复以上步骤，直至所有任务结束。

## 3. 实验设计

- **数据集与场景**：
  - **基准场景**：Split CIFAR-10、Split CIFAR-100、Split Mini-ImageNet（均为常见的类增量持续学习场景）。
  - 每个场景将数据集划分为多个任务（如每任务5类或10类），任务顺序固定，模型依次学习。
- **基准方法（Baselines）**：
  - 经典持续学习方法：EWC、SI、MAS、GEM、AGS-CL、MER、ER-Reservoir。
  - 最新方法：如 DER++、FS-DGPM、PCL、OCD-Net 等（涵盖基于正则化、基于记忆回放和基于参数隔离的方法）。
  - 对比两个变体：DEDUCE 仅使用 LUM、仅使用 GUM、完整 DEDUCE。
- **对比指标**：平均准确率（Average Accuracy, AA）、遗忘度（Forgetting Measure, FM）、正向迁移率等。

## 4. 资源与算力

- **论文未明确说明**：文中未提及使用的 GPU 型号、数量、训练时长等具体算力信息。仅在实验中提到所有方法在相同硬件环境下运行以确保公平比较，但未披露硬件细节。

## 5. 实验数量与充分性

- **实验数量**：
  - 在3个主要数据集（CIFAR-10、CIFAR-100、Mini-ImageNet）上各执行了5个任务（CIFAR-10）或10个任务（CIFAR-100、Mini-ImageNet）的持续学习序列，每个实验重复3次取平均值。
  - 进行了全面的**消融实验**：比较完整 DEDUCE 与去掉 LUM 或 GUM 的变体，以及不同检测策略（可迁移性界限 vs. 梯度冲突 vs. 二者组合）的效果。
  - 进行了**超参数敏感性分析**（如遗忘强度、触发频率等）。
  - 与10种以上最新方法进行了对比。
- **充分性与公平性**：
  - 实验设计较为充分，覆盖了不同难度和规模的数据集，包括标准基准。
  - 对比方法为持续学习领域主流方法，且所有方法共用相同的实验设置（如任务顺序、数据划分、超参数搜索）。
  - 重复实验减小随机性，统计显著性检验未提及但通常做法足够。
  - 整体实验设计客观、公平，支持其结论。

## 6. 主要结论与发现

- DEDUCE 在三个基准数据集上平均准确率比最优基线提升 **高达 4.55%**。
- 混合遗忘机制（LUM+GUM）优于仅使用局部遗忘或仅使用全局遗忘，说明二者互补。
- 两种负迁移检测策略组合（可迁移性界限+梯度冲突）效果最好，单一策略也能有所提升。
- 选择性遗忘能够有效缓解任务间干扰，提高模型在新任务上的适应能力，同时保持旧任务性能。
- 全局遗忘模块周期性清理有助于释放模型容量，避免累积冗余。

## 7. 优点

- **创新性**：首次将选择性遗忘与负迁移检测明确结合到持续学习框架中，跳出了仅关注灾难性遗忘的思维定式。
- **方法完整性**：检测-决策-遗忘三阶段闭环设计，且提供了两种互补的检测策略和两种遗忘模块，可组合性强。
- **实验全面**：在多个标准数据集上与大量基线对比，消融实验和敏感性分析充分，支撑了设计决策的有效性。
- **科学启发**：借鉴人脑选择性遗忘机制，为持续学习提供了生物合理性启发。

## 8. 不足与局限

- **算力未报告**：未提供硬件配置和运行时间，不利于复现和效率评估。
- **数据集规模有限**：实验仅在中小型图像分类数据集（CIFAR、Mini-ImageNet）上进行，未在更大规模（如 ImageNet-1K）或更复杂场景（如任务序列长度>10）上验证，可能存在 scale 限制。
- **检测机制依赖任务标签/边界**：需要明确的任务划分（class-incremental），对于任务边界模糊的 stream 场景（如 task-free CL）适应性未知。
- **遗忘操作代价**：局部遗忘模块涉及梯度上升操作，可能增加每步训练时间，文中未分析计算开销。
- **超参数敏感**：遗忘触发频率、遗忘强度等需要调参，未提供自适应方案。

（完）
