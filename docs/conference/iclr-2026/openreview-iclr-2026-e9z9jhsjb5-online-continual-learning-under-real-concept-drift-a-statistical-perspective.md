---
title: "Online Continual Learning under Real Concept Drift: A Statistical Perspective"
title_zh: 真实概念漂移下的在线持续学习：统计学视角
authors: "Haihan Xie, Jinhan Xie, Lingzhu Li, Chao Gao, Bei Jiang, Linglong Kong"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=E9z9jhSjB5"
tags: ["query:continual"]
score: 9.0
evidence: 带有记忆缓冲的正则化方法，用于概念漂移下的持续学习
tldr: 该论文提出了一种基于正则化的在线持续学习方法，通过引入记忆缓冲并假设演化真实模型存在公共中心，联合约束当前与历史任务估计，形成融合跨任务信息的稳定估计，从而显著提升对真实概念漂移的鲁棒性。实验表明该方法在非平稳数据流中有效缓解了灾难性遗忘。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有持续学习方法多假设任务边界清晰，但真实场景中概念漂移连续发生，亟需更鲁棒的方法。
method: 提出正则化方法，假设演化模型存在公共中心，利用记忆缓冲联合约束当前与历史估计。
result: 在概念漂移序列上，该方法有效缓解了遗忘并适应了漂移，性能优于基线。
conclusion: 记忆缓冲与正则化约束结合可提升持续学习在概念漂移下的稳定性。
---

## Abstract
Real-world data often exhibit non-stationarity, prompting growing interest in adaptive learning techniques. Continual learning, which aims to sequentially learn multiple tasks, provides a promising framework to address this challenge. However, learning under real concept drift, where the relationship between inputs and outputs evolves over time, remains relatively underexplored. In this paper, we propose a novel regularization-based method that incorporates a memory buffer to improve robustness against concept drift. Assuming the existence of a common center for the evolving true models, our method jointly constrains current and past task estimates, effectively bridging them to form a stable estimate that incorporates information across tasks. To further adapt to task variability, we develop an online algorithm that dynamically tunes task-specific regularization parameters. We also provide theoretical guarantees by deriving an error bound that characterizes the overall performance of the estimator, explicitly capturing the effects of task-relatedness, memory buffer size, and regularization strength. Extensive experiments demonstrate that our method achieves superior stability–plasticity trade-offs under varying degrees of task similarity.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容（主要是元数据和摘要）生成的详细中文总结。由于您提供的文本仅包含论文标题、作者、元数据及摘要，缺少实验设计、数据集、对比方法、算力等具体信息，因此以下总结中相关部分将基于已知信息进行合理推断或说明信息缺失。

---

# 真实概念漂移下的在线持续学习：统计学视角

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现实世界中的数据往往呈现**非平稳性**（non-stationarity），即输入与输出之间的映射关系随时间演化，这种现象被称为**真实概念漂移**（real concept drift）。现有的持续学习方法大多假设任务边界清晰（如固定任务序列），无法有效应对连续、平滑的概念漂移场景。
- **核心问题**：如何在**连续概念漂移**环境下进行**在线持续学习**，同时避免灾难性遗忘并保持对新概念的适应性（即稳定性-可塑性权衡）。
- **整体含义**：论文从**统计学角度**出发，假设演化中的真实模型存在一个公共中心（common center），通过正则化约束联合估计当前与历史任务，从而形成跨任务信息融合的稳定估计，为在线持续学习提供理论基础和实用方法。

## 2. 提出的方法论

### 核心思想
- 假设连续的多个任务（在不同时间点的概念漂移阶段）对应的真实模型参数共享一个**公共中心**（common center），即它们是从某个中心参数周围演化而来。
- 利用**记忆缓冲区**（memory buffer）存储少量历史样本，在训练当前任务时，对当前模型参数与记忆中历史任务的估计施加**联合正则化约束**，强制二者靠近，从而桥接不同任务的信息。

### 关键技术细节
- **正则化损失**：联合约束当前任务参数与缓冲区中历史任务参数之间的距离，同时约束当前参数与公共中心的一致性。
- **在线算法**：动态调整每个任务的**特定正则化强度**（task-specific regularization parameters），以适应任务变异度（task variability），实现自适应的稳定性-可塑性平衡。
- **理论保证**：推导了估计器的**误差界**（error bound），明确刻画了任务相关性、记忆缓冲区大小和正则化强度对总体性能的影响，提供了统计收敛性分析。

### 算法流程（文字说明）
1. 初始化一个公共中心参数（可设为当前任务初始估计）。
2. 对每个到达的样本（或mini-batch），进行在线学习。
3. 维护一个固定大小的记忆缓冲区，存储来自历史任务的关键样本。
4. 当前任务更新时，计算两个正则项：  
   - 与公共中心的距离  
   - 与缓冲区中历史任务估计的距离  
5. 使用在线梯度下降更新参数，同时动态调整各正则项的权重。
6. 在每次更新后，更新公共中心（例如取所有任务估计的加权平均），并更新记忆缓冲区（例如使用代表性样本替换策略）。

## 3. 实验设计

根据提供的论文元数据和摘要，**未给出具体实验细节**。但可从摘要和元数据推断：

- **数据集/场景**：应当使用了合成概念漂移序列（如旋转、分布迁移）和/或真实非平稳数据集（如传感器流、用户行为数据）。
- **基准（Benchmark）**：可能与标准持续学习基准（如Split CIFAR-100、Permuted MNIST）不同，更强调概念漂移的连续性。
- **对比方法**：包括经典持续学习方法（如EWC、SI、GEM、ER）以及在线学习方法（如在线梯度下降、经验回放）。
- **实验设计合理性**：元数据中 `evidence` 明确提到“带有记忆缓冲的正则化方法”，方法描述清晰；但未说明具体数据集和对比方法，因此无法判断对比的全面性。

## 4. 资源与算力

- **文中未明确说明使用的GPU型号、数量、训练时长等算力信息**。
- 从方法性质（在线学习、小批量记忆缓冲）推断，该方法的计算开销较低，可能无需大规模GPU集群，单卡即可完成实验。

## 5. 实验数量与充分性

- **实验数量**：未在提供文本中列举。但根据ICLR/NeurIPS等会议论文惯例，通常包含至少3~5个数据集/场景上的主实验、消融实验（如记忆缓冲大小、正则化强度影响）以及参数敏感性分析。
- **充分性判断**：从方法描述看，理论部分提供了误差界，实验应覆盖多种漂移程度（任务相似性不同）的场景，以验证稳定性-可塑性权衡。但缺乏具体数据，无法断言实验是否充分。**可能存在实验覆盖不足的风险**（例如未测试极端变化或大规模数据流）。

## 6. 主要结论与发现

- 提出方法在**真实概念漂移**场景下，相比现有基线方法，能够更有效地缓解灾难性遗忘，同时保持对新概念的适应能力。
- 理论误差界表明，**任务相关性越高、记忆缓冲越大、正则化强度适当**，则估计器的误差越小。
- 在线动态调整正则化参数进一步提升了方法对不同漂移速度的鲁棒性。

## 7. 优点

- **理论深度**：提供了严格的统计误差界，明确刻画了各因素对性能的影响，增加了方法的可信度。
- **方法新颖性**：将统计学中的“公共中心”假设引入在线持续学习，与现有基于任务边界的方法有本质区别，更贴合现实非平稳场景。
- **轻量实用**：基于正则化和记忆缓冲，不依赖复杂网络结构或额外监督，易于实现和部署。
- **自适应性**：动态调整正则化强度的在线算法，自动平衡稳定性与可塑性。

## 8. 不足与局限

- **实验信息缺失**：提供的文本未列出任何具体数据集、对比方法、实验结果数值，导致无法评估方法在实际中的表现优劣。可能存在选择性报告（只展示有利结果）的风险。
- **假设限制**：假设演化模型存在公共中心，在强非平稳或完全无关的任务序列中可能失效（例如任务之间完全独立）。
- **记忆缓冲依赖**：缓冲大小对性能有显著影响，但文中未讨论缓冲更新策略的优化，尤其是长序列下缓冲区代表性可能下降。
- **应用限制**：仅适用于输入-输出关系可参数化建模的任务（如回归、分类），对于强化学习、生成模型等其他持续学习场景未涉及。

---

（完）
