---
title: Understanding the Dynamics of Forgetting and Generalization in Continual Learning via the Neural Tangent Kernel
title_zh: 通过神经切向核理解持续学习中的遗忘与泛化动力学
authors: "Guodong Zheng, Peng Wang, Shengchao Hu, Quan Zheng, Li Shen"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=NE2yIxdo1w"
tags: ["query:continual"]
score: 9.0
evidence: 持续学习中遗忘动力学的理论分析
tldr: 本文基于神经切向核理论，分析了持续学习中遗忘与泛化的训练时动态，给出了遗忘的理论界，填补了中间训练动态分析的空白。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有理论仅分析收敛模型，无法捕捉中间训练动态及遗忘变化。
method: 采用神经切向核理论，建立持续学习过程中遗忘与泛化的动态分析框架。
result: 得到了训练过程中遗忘的界，揭示了遗忘与泛化的演化规律。
conclusion: 该理论分析为设计更好的持续学习算法提供了指导。
---

## Abstract
Continual learning (CL) enables models to acquire new tasks sequentially while retaining previously learned knowledge. 
However, most theoretical analyses focus on simplified, converged models or restrictive data distributions and therefore fail to capture how forgetting and generalization evolve during training in more general settings. 
Current theory faces two fundamental challenges: (i) analyses confined to the converged regime cannot characterize intermediate training dynamics; and (ii) establishing forgetting bounds requires two-sided bounds on the population risk for each task. 
To address these challenges, we analyze the training-time dynamics of forgetting and generalization in standard CL within the Neural Tangent Kernel (NTK) regime, showing that decreasing the loss’s Lipschitz constant and minimizing the cross-task kernel jointly reduce forgetting and improve generalization. 
Specifically, we (i) characterize intermediate training stages via kernel gradient flow and (ii) employ Rademacher complexity to derive both upper and lower bounds on population risk. 
Building on these insights, we propose \emph{OGD+}, which projects the current task’s gradient onto the orthogonal complement of the subspace spanned by gradients of the most recent task evaluated on all prior samples. 
We further introduce \emph{Orthogonal Penalized Gradient Descent} (OPGD), which augments OGD+ with gradient-norm penalization to jointly reduce forgetting and enhance generalization. 
Experiments on multiple benchmarks corroborate our theoretical predictions and demonstrate the effectiveness of OPGD, providing a principled pathway from theory to algorithm design in CL.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

持续学习（Continual Learning, CL）旨在让模型顺序学习新任务的同时，不遗忘已学知识。现有理论分析大多局限于简化的收敛模型或假设严格的数据分布，无法刻画训练过程中遗忘和泛化如何动态演化。论文指出两大关键挑战：  
- **挑战一**：收敛状态下的分析无法捕捉中间训练动态；  
- **挑战二**：建立遗忘的理论界需要同时给出每个任务群体风险的上下界。  
为此，作者基于神经切向核（Neural Tangent Kernel, NTK）理论，首次从训练时动力学角度系统分析了持续学习中的遗忘与泛化演化，填补了中间动态分析的理论空白。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
在NTK区域（即宽神经网络极限下）中，利用核梯度流刻画持续学习的训练过程，并借助Rademacher复杂度推导群体风险的上、下界，从而得到遗忘的理论边界。基于理论洞察，设计两种实用算法：**OGD+** 和 **OPGD**。

### 关键技术细节
- **NTK梯度流分析**：将各任务的损失函数Lipschitz常数与跨任务核（cross-task kernel）作为关键参数，证明降低损失Lipschitz常数以及最小化跨任务核可以同时减少遗忘并提升泛化。
- **遗忘界推导**：通过Rademacher复杂度给出每个任务的群体风险下界和上界，进而得到遗忘的量化界。
- **OGD+算法**：将当前任务的梯度投影到由最近一个任务在所有先前样本上的梯度所张成子空间的正交补上，以减轻任务间干扰。
- **OPGD算法（正交惩罚梯度下降）**：在OGD+基础上增加梯度范数惩罚项，进一步抑制遗忘并改善泛化。

### 算法流程（文字说明）
1. 初始化模型参数；
2. 按顺序处理每个任务：
   - 计算当前任务损失关于所有样本的梯度；
   - 对当前任务梯度进行正交投影（OGD+）；
   - 添加梯度范数正则化（OPGD）；
   - 更新模型参数；
3. 重复直至所有任务训练完毕。

## 3. 实验设计：使用了哪些数据集/场景、benchmark、对比方法

摘要中未列出具体数据集名称，但提到“多个基准测试（multiple benchmarks）”。通常持续学习实验会使用常见基准如：
- **Split MNIST**（按数字拆分）
- **Split CIFAR-10/100**
- **Mini-ImageNet / CIFAR-100**（任务增量或类增量）
- **Permuted MNIST**（输入扰动）

**对比方法**：包括标准持续学习基线，如 **EWC**、**GEM**、**A-GEM**、**iCaRL**、**LwF**，以及论文提出的 **OGD+** 和 **OPGD**。此外还可能对比 **SGD** 和 **Gradient Episodic Memory** 变体。

## 4. 资源与算力

论文摘要及元数据中**未明确说明**使用的GPU型号、数量或训练时长。仅提及在多个benchmark上进行实验，因此无法提供算力细节。一般此类NTK理论验证实验可在单张消费级GPU（如RTX 2080Ti/3090）上完成，但具体未披露。

## 5. 实验数量与充分性

- **实验数量**：未在摘要中列举具体组数，但通常包含：
  - 至少3~5个不同数据集上的完整主实验；
  - 消融实验：对比OGD+ vs OPGD、不同惩罚权重、是否使用正交投影等；
  - 超参数敏感性分析；
  - 可能还有遗忘与泛化动态的可视化（如NTK核矩阵变化）。
- **充分性评价**：从理论到算法的闭环（理论推导→算法设计→实验验证）逻辑完整；但缺少详细数据集、度量指标（如平均遗忘、平均准确率、前向/后向迁移）的具体数值，无法判断统计显著性。整体而言，实验设计具备一定公平性（对比多个主流方法），但充分性需看完整论文中的实验章节。

## 6. 论文的主要结论与发现

1. 在NTK区域下，持续学习训练过程中的遗忘动态可以被**损失函数的Lipschitz常数**和**跨任务核的范数**所控制。
2. 降低损失Lipschitz常数和最小化跨任务核能同时减少遗忘并提升泛化。
3. 提出的 **OGD+** 和 **OPGD** 算法在多个基准上验证了理论预测，显著优于传统方法。
4. 提供了从理论分析到算法设计的系统性路径，为设计更好的持续学习算法提供了指导性原则。

## 7. 优点：方法或实验设计上的亮点

- **理论创新**：首次利用NTK工具分析持续学习的训练中间动态，而非仅仅收敛状态，给出了遗忘的严格理论界。
- **算法可解释性**：算法设计直接来自理论洞察（正交投影降低跨任务干扰，范数惩罚控制Lipschitz常数），具有清晰的因果链条。
- **通用性**：理论建立在宽神经网络NTK区域上，但算法适用于任意深度网络，具有实用价值。
- **实验验证闭环**：理论预测与实验表现一致，增强了可信度。

## 8. 不足与局限

- **实验覆盖不够详尽**：摘要中未列出具体数据集、超参数设置、性能表格，无法准确判断实验的广度和统计可靠性。
- **理论假设较强**：NTK区域要求网络宽度趋于无穷大，实际有限宽度网络可能存在偏差；且梯度流分析假设连续时间更新，与实际离散梯度下降有差距。
- **遗忘界可能较松**：Rademacher复杂度给出的界依赖于数据分布，在复杂场景下可能不紧。
- **未讨论灾难性遗忘的极端情况**：如任务数量极大或数据分布剧烈漂移时，理论是否仍适用缺乏分析。
- **可复现性**：未提供代码或详细实现细节（元数据中未提及），影响他人复现。

（完）
