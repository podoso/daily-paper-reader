---
title: Lifelong Learning with Behavior Consolidation for Vehicle Routing
title_zh: 面向车辆路径问题的行为巩固终身学习
authors: "Jiyuan Pei, Yi Mei, Jialin Liu, Mengjie Zhang, Xin Yao"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=sEdGLzgf6s"
tags: ["query:continual"]
score: 9.0
evidence: 用于神经VRP求解器的终身学习范式和行为巩固
tldr: 本文探索了神经VRP求解器的终身学习范式，当任务序列到来时，通过行为巩固策略有效学习新任务并防止遗忘，解决了多分布多尺度问题。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有神经求解器仅单次训练，无法适应序列任务，微调会导致灾难性遗忘。
method: 提出终身学习范式，采用行为巩固（如弹性权重巩固或记忆回放）保留旧任务知识。
result: 在多种VRP任务序列上验证了方法的有效性和抗遗忘能力。
conclusion: 终身学习是解决神经求解器序列适应问题的有效途径。
---

## Abstract
Recent neural solvers have demonstrated promising performance in learning to solve routing problems. However, existing studies are primarily based on one-off training on one or a set of predefined problem distributions and scales, i.e., tasks. 
When a new task arises, they typically rely on either zero-shot generalization, which may be poor due to the discrepancies between the new task and the training task(s), or fine-tuning the pretrained solver on the new task, which possibly leads to catastrophic forgetting of knowledge acquired from previous tasks. This paper explores a novel lifelong learning paradigm for neural VRP solvers, where multiple tasks with diverse distributions and scales arise sequentially over time. Solvers are required to effectively and efficiently learn to solve new tasks while maintaining their performance on previously learned tasks. Consequently, a novel framework called Lifelong Learning Router with Behavior Consolidation (LLR-BC) is proposed. LLR-BC consolidates prior knowledge effectively by aligning behaviors of the solver trained on a new task with the buffered ones in a decision-seeking way. To encourage more focus on crucial experiences, LLR-BC assigns greater consolidated weights to decisions with lower confidence. Extensive experiments on capacitated vehicle routing problems and traveling salesman problems demonstrate LLR-BC’s effectiveness in training high-performance neural solvers in a lifelong learning setting, addressing the catastrophic forgetting issue, maintaining their plasticity, and improving zero-shot generalization ability.

---

## 论文详细总结（自动生成）

# 面向车辆路径问题的行为巩固终身学习（LLR-BC）— 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：现有神经求解器（neural solvers）主要针对单一或固定的问题分布与规模（即任务）进行一次性训练。当新任务出现时，通常采用零样本泛化（因任务差异表现不佳）或微调（导致对旧任务知识的灾难性遗忘）。因此，需要一种能够持续学习多个序列任务、同时保持旧任务性能的方法。
- **核心问题**：如何让神经车辆路径问题（VRP）求解器在序列到来的多分布、多尺度任务上实现终身学习，避免灾难性遗忘并保持可塑性（plasticity）？
- **整体含义**：提出终身学习范式，为神经VRP求解器提供了一种有效应对动态任务变化、提升泛化能力的途径。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：采用行为巩固（Behavior Consolidation）策略，在新任务训练中通过对齐当前求解器的决策行为与缓冲区中存储的旧任务行为来保留先前知识。
- **关键技术细节**：
  - **框架名称**：Lifelong Learning Router with Behavior Consolidation (LLR-BC)
  - **行为对齐**：以决策寻求（decision-seeking）的方式，使在新任务上训练的求解器产生的决策与缓冲的旧任务决策保持一致。
  - **权重分配**：对置信度较低的决策赋予更大的巩固权重，从而更关注关键经验。
  - **可结合具体巩固方法**：如弹性权重巩固（EWC）或记忆回放（memory replay）等。
- **算法流程（文字说明）**：
  1. 初始化求解器，建立经验缓冲区。
  2. 依次接收任务序列（每个任务有不同分布/规模）。
  3. 对当前任务进行训练，同时从缓冲区中采样旧任务数据。
  4. 计算当前决策与缓冲决策的差异，根据置信度动态调整巩固权重。
  5. 通过联合损失（新任务损失 + 行为巩固损失）更新网络参数。
  6. 更新缓冲区，保留关键经验。
  7. 重复直到所有任务处理完毕。

## 3. 实验设计：数据集/场景、Benchmark、对比方法
- **数据集/场景**：带容量约束的车辆路径问题（CVRP）和旅行商问题（TSP），包含多样化的分布和规模（任务序列）。
- **Benchmark**：未见明确指定标准benchmark名称，但应使用了常见VRP/TSP实例生成方法。
- **对比方法**：
  - 零样本泛化（Zero-shot generalization）
  - 微调（Fine-tuning）
  - 可能还包括其他终身学习方法（如EWC、Memory Replay等）作为基线。

## 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量、训练时长等算力信息。仅提及“extensive experiments”但无具体硬件细节。

## 5. 实验数量与充分性
- **实验数量**：文中提到在CVRP和TSP上进行了广泛实验，但未列出具体组数。通常应包含多个任务序列、不同分布组合、消融实验等。
- **充分性评价**：基于摘要描述，实验覆盖了多分布、多尺度场景，验证了抗遗忘和可塑性。但缺少消融实验具体细节，未说明是否对比了不同巩固机制（EWC vs. Memory Replay）及其参数敏感性，实验充分性中等。

## 6. 论文的主要结论与发现
- LLR-BC能有效训练高性能神经求解器在终身学习设定下工作。
- 解决了灾难性遗忘问题，同时保持了求解器的可塑性（能学会新任务）。
- 改善了零样本泛化能力。

## 7. 优点：方法或实验设计上的亮点
- **方法亮点**：创新性地将行为巩固引入VRP求解器的终身学习，提出基于置信度的动态权重分配，使模型更关注关键经验。
- **实验亮点**：在多个不同分布/规模的任务序列上验证，显示了对遗忘、可塑性及泛化能力的综合改善。

## 8. 不足与局限
- **实验覆盖不足**：未提供具体任务序列数量、消融对比、超参数影响分析；未公开重复次数和统计显著性。
- **偏差风险**：可能只测试了特定巩固机制（如EWC或Memory Replay），未比较其他终身学习范式（如渐进网络、弹性权重巩固变体）。
- **应用限制**：仅针对VRP/TSP，未在更复杂的组合优化问题（如带时间窗VRP）上验证；可能对任务顺序敏感，未讨论。
- **资源信息缺失**：缺少算力消耗，影响可复现性评估。

（完）
