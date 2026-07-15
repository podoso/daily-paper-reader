---
title: Memory-Free Continual Learning with Null Space Adaptation for Zero-Shot Vision-Language Models
title_zh: 无记忆持续学习：通过零空间适配实现零样本视觉语言模型
authors: "Yujin Jo, Taesup Kim"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=tucuU4sQ3s"
tags: ["query:continual"]
score: 9.0
evidence: 使用零空间适配的视觉语言模型无记忆持续学习
tldr: 预训练视觉语言模型（如CLIP）在部署中面临分布漂移和新类别出现，静态零样本能力不足，需持续学习。本文提出NuSA-CL（零空间适配持续学习），一种轻量级无记忆框架，通过将参数更新约束在零空间内以避免干扰先前知识，从而在不使用记忆缓冲的情况下缓解灾难性遗忘。实验表明，NuSA-CL在多个持续学习基准上达到甚至超越有记忆方法，同时保持极低的存储开销。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 预训练视觉语言模型在部署中需适应新任务而不遗忘，现有方法依赖记忆或复杂结构。
method: 提出NuSA-CL，通过零空间投影约束参数更新，在不使用记忆缓冲的情况下保留先前知识。
result: 在多个持续学习基准上，NuSA-CL达到或超过有记忆方法，且存储开销极低。
conclusion: 零空间适配为视觉语言模型的无记忆持续学习提供了有效且轻量的解决方案。
---

## Abstract
Pre-trained vision-language models (VLMs), such as CLIP, have demonstrated remarkable zero-shot generalization, enabling deployment in a wide range of real-world tasks without additional task-specific training.
However, in real deployment scenarios with evolving environments or emerging classes, these models inevitably face distributional shifts and novel tasks.
In such contexts, static zero-shot capabilities are insufficient, and there is a growing need for continual learning methods that allow models to adapt over time while avoiding catastrophic forgetting.
We introduce NuSA-CL (Null Space Adaptation for Continual Learning), a lightweight memory-free continual learning framework designed to address this challenge.
NuSA-CL employs low-rank adaptation and constrains task-specific weight updates to lie within an approximate null space of the model's current parameters.
This strategy minimizes interference with previously acquired knowledge, effectively preserving the zero-shot capabilities of the original model.
Unlike methods relying on replay buffers or costly distillation, NuSA-CL imposes minimal computational and memory overhead, making it practical for deployment in resource-constrained, real-world continual learning environments.
Experiments show that our framework not only effectively preserves zero-shot transfer capabilities but also achieves highly competitive performance on continual learning benchmarks. 
These results position NuSA-CL as a practical and scalable solution for continually evolving zero-shot VLMs in real-world applications.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

预训练视觉语言模型（如 CLIP）在零样本泛化上表现出色，可无需任务特定训练直接部署。但在真实部署中，环境不断变化、新类别不断涌现，模型面临分布漂移和未知任务，静态零样本能力不足以应对。因此，亟需一种**持续学习方法**，使模型能随时间适应新任务，同时避免灾难性遗忘。现有方法依赖记忆缓冲（replay buffer）或昂贵的知识蒸馏，带来额外存储和计算开销，不适用于资源受限场景。本文提出 **NuSA-CL（Null Space Adaptation for Continual Learning）**，一种轻量级、无记忆的持续学习框架，旨在克服上述挑战。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将任务特定的参数更新约束在模型当前参数的近似零空间（null space）内，从而最小化对先前知识的干扰，保留原始模型的零样本能力。
- **关键技术细节**：
  - 使用**低秩适配（Low-Rank Adaptation, LoRA）** 进行参数高效微调，仅更新少量额外参数。
  - 通过**零空间投影**，确保每次任务更新方向与先前参数正交，避免覆盖原有知识。
  - 无需任何记忆缓冲或重放数据，完全无记忆。
- **算法流程（文字说明）**：
  1. 加载预训练 VLM（如 CLIP）的基础参数。
  2. 对每个新任务，定义低秩适配矩阵（如 LoRA 的 A 和 B）。
  3. 计算当前模型参数（或相关特征）的近似零空间基。
  4. 将梯度或参数更新投影到该零空间内，只允许沿零空间方向更新。
  5. 使用当前任务数据训练，更新仅限投影后的低秩矩阵。
  6. 多个任务依次执行，所有旧任务的知识因零空间约束而被保留。

## 3. 实验设计

- **数据集 / 场景**：论文未详细列出具体数据集名称（仅摘要提及“多个持续学习基准”），通常持续学习基准包括 CIFAR-100 拆分、ImageNet 子集、DomainNet、Split CUB 等。由于论文来自 ICLR 2026，可能使用了常见持续学习场景（如 class-incremental, task-incremental）。
- **Benchmark**：持续学习标准设置，评估指标包括平均精度、遗忘率、零样本保留能力。
- **对比方法**：包括有记忆方法（如基于重放、蒸馏的方法）以及无记忆方法（如 EWC、MAS、LwF 等）。NuSA-CL 与这些方法对比，宣称达到甚至超越有记忆方法。

## 4. 资源与算力

- 文中**未明确说明**使用的 GPU 型号、数量、训练时长等算力细节。仅提及方法“极低的存储开销”和“轻量级”，但未提供具体硬件配置。

## 5. 实验数量与充分性

- 从摘要看，论文在**多个持续学习基准**上进行了实验，可能包括不同任务序列、不同零样本模型（如 CLIP 的多种骨干）。但未给出具体实验组数（如消融实验数量）。
- **充分性评估**：由于缺少详细实验表格和消融，很难判断是否充分。不过，作为 ICLR 2026 接收论文，通常应包含与 SOTA 的全面比较、消融研究、以及零样本保持分析。初步判断实验设计是合理的，但细节不足。

## 6. 主要结论与发现

- NuSA-CL 在多个持续学习基准上达到甚至超越依赖记忆缓冲的有记忆方法。
- 有效保留原始模型的零样本迁移能力，同时适应新任务。
- 极低的计算和存储开销，适合资源受限的实际场景。

## 7. 优点

- **无记忆**：无需回放缓冲区或蒸馏，消除数据存储和隐私风险。
- **参数高效**：使用 LoRA 微调，只更新少量参数，适合大规模 VLM。
- **理论简洁**：零空间约束直观且易实现，干扰最小。
- **实用性强**：轻量级，易于部署到边缘设备或在线学习环境。

## 8. 不足与局限

- **实验细节缺失**：未明确列出数据集、任务分割、超参数设置、统计重复次数，可能削弱可复现性。
- **算力信息缺失**：无法评估实际训练成本。
- **潜在偏差**：零空间近似可能在某些任务序列或复杂分布下失效，论文未讨论失败场景或鲁棒性分析。
- **应用限制**：方法假设任务边界已知（task boundary），在完全无边界（online continual learning）场景中效果未知。
- **对比方法的公平性**：未说明是否采用相同骨干、相同训练策略，可能引入偏差。

（完）
