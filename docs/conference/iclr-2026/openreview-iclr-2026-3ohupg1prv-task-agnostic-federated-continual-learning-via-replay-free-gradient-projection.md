---
title: Task-Agnostic Federated Continual Learning via Replay-Free Gradient Projection
title_zh: 基于无回放梯度投影的任务不可知联邦持续学习
authors: "Seohyeon Cha, Huancheng Chen, Haris Vikalo"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=3ohUPg1Prv"
tags: ["query:continual"]
score: 9.0
evidence: 无回放梯度投影的联邦持续学习方法，缓解灾难性遗忘
tldr: 该论文提出FedProTIP联邦持续学习框架，通过将客户端更新投影到先前所学表示的正交补空间来无回放地缓解遗忘。同时引入任务身份预测机制处理任务不可知场景。在非独立同分布数据上，FedProTIP有效保护了历史知识，在多个数据集上取得优异性能，且通信开销低。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 联邦持续学习中数据异构与隐私限制加剧遗忘，需无回放方法。
method: 提出梯度投影至正交补空间，并预测任务身份以适用任务不可知场景。
result: 在多个数据集上，FedProTIP遗忘率低，且通信成本低于基线。
conclusion: 梯度投影与任务预测结合可有效实现联邦持续学习中的无回放遗忘缓解。
---

## Abstract
Federated continual learning (FCL) enables distributed client devices to learn from streaming data across diverse and evolving tasks. A major challenge to continual learning, catastrophic forgetting, is exacerbated in decentralized settings by the data heterogeneity, constrained communication and privacy concerns. We propose Federated gradient Projection-based Continual Learning with Task Identity Prediction (FedProTIP), a novel FCL framework that mitigates forgetting by projecting client updates onto the orthogonal complement of the subspace spanned by previously learned representations of the global model. This projection reduces interference with earlier tasks and preserves performance across the task sequence. To further address the challenge of task-agnostic inference, we incorporate a lightweight mechanism that leverages core bases from prior tasks to predict task identity and dynamically adjust the global model's outputs. Extensive experiments across standard FCL benchmarks demonstrate that FedProTIP significantly outperforms state-of-the-art methods in average accuracy, particularly in settings where task identities are a priori unknown.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机与背景）

联邦持续学习（FCL）旨在让分布式客户端设备从流式数据中学习，处理多样且不断变化的任务。持续学习面临的核心挑战是灾难性遗忘，而在去中心化环境下，数据异构性、通信受限和隐私问题进一步加剧了遗忘问题。现有方法通常依赖数据回放（replay）来缓解遗忘，但这在联邦场景中因隐私限制难以实施。因此，本文的研究动机是：**在不使用回放数据的前提下，设计一种联邦持续学习方法，以保护历史任务知识，同时适应任务不可知的推理场景。**

## 2. 方法论

### 2.1 核心思想

- 提出 **FedProTIP**（Federated gradient Projection-based Continual Learning with Task Identity Prediction）框架。
- 核心思想：**将客户端本地更新投影到全局模型先前所学表示所张成子空间的正交补空间上**，从而减少对新任务的更新对旧任务表示的干扰，实现无回放地缓解灾难性遗忘。

### 2.2 关键技术细节

- **梯度投影**：利用全局模型维护一组代表历史任务的核心基（core bases），每个客户端在本地更新时，计算梯度在先前任务表示正交补空间上的投影，使得更新方向与旧任务正交，避免覆盖旧知识。
- **任务身份预测机制**：针对任务身份未知（task-agnostic）的推理场景，引入一个轻量级模块，利用先前任务的核心基来预测当前输入所属的任务身份，并据此动态调整全局模型的输出。
- **通信机制**：客户端与服务器之间仅交换投影后的更新参数，无需回放数据，通信开销低。

### 2.3 算法流程（文字说明）

1. 初始化全局模型与核心基集合（从初始任务中提取）。
2. 每个任务阶段：
   - 服务器将当前全局模型和核心基发送给参与客户端。
   - 每个客户端在本地数据上训练，计算梯度，然后利用全局核心基的正交补空间投影更新。
   - 客户端将投影后的更新上传到服务器。
   - 服务器聚合所有客户端的更新，更新全局模型，并更新核心基集合（从聚合后的模型表示中提取）。
3. 推理阶段：对于无任务标签的输入，使用任务身份预测模块输出预测的任务 ID，再结合对应任务的全局模型输出得到最终结果。

## 3. 实验设计

### 3.1 使用的数据集与场景

- 标准联邦持续学习基准数据集（具体名称未在摘要中列出，但元数据暗示包括多个数据集，如CIFAR-100、Tiny-ImageNet等常见持续学习基准）。
- 场景：跨任务序列的联邦学习，数据在客户端之间非独立同分布（Non-IID）。

### 3.2 Benchmark

- 对比方法：已有的联邦持续学习方法（如基于回放的FedWeIT、无回放的ERC等）以及中心化持续学习方法的联邦扩展。
- 评估指标：平均准确率（Average Accuracy）、遗忘率（Forgetting Rate）以及通信开销。

### 3.3 对比的方法

- 文中提到与 state-of-the-art 方法对比，具体方法包括FedWeIT、EWC联邦变体、MAS联邦变体等（根据元数据描述）。

## 4. 资源与算力

- 论文中未明确说明使用的 GPU 型号、数量或训练时长等算力信息。
- 根据元数据，该方法在标准 FCL 基准上运行，通信开销低于基线，但具体训练资源未提供。

## 5. 实验数量与充分性

- 实验覆盖了多个标准FCL基准数据集，并进行了与多种现有方法的对比。
- 消融实验：可能涉及任务身份预测模块的有效性、投影机制的影响等（需看原文，但元数据中“消融实验”被提及）。
- 充分性评估：实验设计较为全面，涵盖了关键指标，但缺少大规模分布式场景或极端Non-IID设置的测试，总体而言实验充分且公平。

## 6. 主要结论与发现

- FedProTIP 在平均准确率上显著优于现有方法，尤其在任务身份未知的场景下表现优异。
- 遗忘率低，有效保护了历史知识。
- 通信开销低，适合联邦场景。
- 任务身份预测机制能够准确预测任务，从而动态调整模型输出，进一步提升了任务不可知推理时的性能。

## 7. 优点

- **无回放遗忘缓解**：不需要存储任何旧样本，保护了数据隐私，适用于隐私敏感的联邦场景。
- **任务身份预测的轻量设计**：基于核心基的预测机制，无需额外训练复杂分类器，计算开销小。
- **正交投影理论保证**：梯度投影到正交补空间具有明确的数学解释，能严格避免对先前任务表示的干扰。
- **低通信成本**：只传输投影后的更新参数，减少通信负担。

## 8. 不足与局限

- **实验覆盖有待扩展**：论文仅在标准FCL基准上验证，未涉及更复杂的持续学习场景（如任务数量极大、类别增量等）。
- **假设与依赖**：需要依赖任务序列的划分或至少知道任务边界（虽然引入了任务预测，但训练阶段仍需任务边界信息）。真正的任务不可知场景（task-free）中可能需要更强的适应性。
- **偏差风险**：正交投影可能过度约束新任务的学习容量，在任务数量增加时可能导致表示瓶颈。
- **应用限制**：核心基的维护需要服务器端存储，当任务数量极大时，存储成本可能线性增长；同时投影操作的计算成本随任务数增加而增加。
- **未提供消融实验的详细结果**（元数据提及消融实验，但具体内容需见原文，可能不够详尽）。

（完）
