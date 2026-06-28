---
title: Sparse Tuning Enhances Plasticity in PTM-based Continual Learning
title_zh: 稀疏调优增强基于预训练模型的持续学习中的可塑性
authors: "Huan Zhang, Shenghua Fan, Shuyu Dong, Yujin Zheng, Dingwen Wang, Fan Lyu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40050/44011"
tags: ["query:continual"]
score: 8.0
evidence: 基于预训练模型的持续学习，解决遗忘
tldr: "基于预训练模型的持续学习方法通常冻结模型并使用适配器，限制了可塑性。本文提出互信息引导的稀疏调优方法MIST，基于互信息目标敏感度选择性地更新少于5%的模型参数，实现任务特定适应的同时保持泛化能力。实验表明，MIST在多个持续学习任务上优于现有方法，有效缓解了灾难性遗忘。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于预训练模型的持续学习方法冻结主干网络，导致模型可塑性不足且泛化能力受限。
method: "利用互信息目标选择性地稀疏更新预训练模型参数（<5%），保持旧知识的同时适应新任务。"
result: 在多个持续学习基准上，MIST在准确率和遗忘率上均优于现有方法。
conclusion: MIST通过稀疏调优平衡了可塑性与稳定性，提升了持续学习性能。
---

## Abstract
Continual Learning with Pre-trained Models holds great promise for efficient adaptation across sequential tasks. However, most existing approaches freeze PTMs and rely on auxiliary modules like prompts or adapters, limiting model plasticity and leading to suboptimal generalization when facing significant distribution shifts. While full fine-tuning can improve adaptability, it risks disrupting crucial pre-trained knowledge. In this paper, we propose Mutual Information-guided Sparse Tuning (MIST), a plug-and-play method that selectively updates a small subset of PTM parameters, less than 5%, based on sensitivity to mutual information objectives. MIST enables effective task-specific adaptation while preserving generalization. To further reduce interference, we introduce strong sparsity regularization by randomly dropping gradients during tuning, resulting in fewer than 0.5% of parameters being updated per step. Applied before standard freeze-based methods, MIST consistently boosts performance across diverse continual learning benchmarks. Experiments show that integrating our method into multiple baselines yields significant performance gains.

---

## 论文详细总结（自动生成）

好的，基于您提供的论文内容，以下是对该论文的结构化、深入且客观的中文总结。

---

### 论文核心问题与整体含义（研究动机和背景）

**1. 核心问题**

在基于预训练模型（PTM）的持续学习（CL）中，如何平衡“可塑性”（适应新任务的能力）与“稳定性”（保留旧知识和预训练泛化能力）是一个根本性挑战。

**2. 现有方法的局限性**

-   **基于冻结的方法（主流）：** 冻结PTM主干，仅训练额外的提示（Prompt）或适配器（Adapter）。虽然能保护预训练知识（高稳定性），但严重限制了模型适应大幅分布偏移的能力（低可塑性）。
-   **全微调方法：** 更新所有参数以提升对新任务的适应性（高可塑性），但极易破坏预训练模型的关键知识结构，导致灾难性遗忘和泛化能力下降。

**3. 本文动机**

现有方法未能有效兼顾可塑性与稳定性。作者旨在提出一种新的稀疏调优策略，仅更新对任务适应最关键且对预训练结构干扰最小的极少数参数，从而在两者之间达到最佳平衡。

### 论文提出的方法论：MIST

**1. 核心思想**

本文提出**互信息引导的稀疏调优（MIST）**，一个即插即用的预适应模块。其核心思想是：在每次增量任务开始前，基于**互信息（MI）目标**识别并稀疏地更新PTM中对新任务最敏感、同时对预训练结构干扰最小的一小部分参数，为后续的冻结式方法创造一个更好的特征空间。

**2. 关键技术细节**

-   **MI梯度优势的理论分析：**
    -   作者通过梯度分析指出，交叉熵（CE）损失的梯度包含`∂p(x; θ)/∂θi`项，这会直接改变PTM学到的输入数据分布`p(x)`，破坏其结构。
    -   相比之下，**互信息（MI）的梯度**由于概率归一化约束，天然消除了这一干扰项`∂p(x; θ)/∂θi`。因此，MI目标提供了一种更稳定的优化途径，能在适应新任务的同时最大限度地保留预训练特征空间的完整性。

-   **MIST算法流程（Algorithm 1）：**
    1.  **MI敏感性估计：** 对当前任务`Dt`，计算每个参数`θi`相对于MI目标的基于Fisher信息矩阵的敏感性分数`F’_MI`。为求效率，该矩阵通过多次小批量梯度平方的近似得到。
    2.  **稀疏选择：** 根据敏感性分数，选择排名前 **k%**（设为5%）的参数，构成更新子集`M`。
    3.  **预适应阶段（MI引导调优）：** 使用MI损失函数\( L_{MI} \)（基于监督对比学习InfoNCE损失变体）对`M`中的参数进行几个epoch的稀疏微调。为了进一步正则化更新路径并防止过拟合，引入了**梯度丢弃（Gradient Dropout）**，即在每个批次中随机丢弃`M`中d%的参数，最终每批次仅更新**0.5%** 的总参数。
    4.  **回归冻结方法：** 预适应阶段结束后，重新冻结PTM，然后恢复使用原始的冻结式持续学习方法（如L2P、DualPrompt等）来训练其提示或适配器。

-   **关键组件总结：**
    -   **MI基Fisher矩阵：** 用于识别对MI目标敏感的参数。
    -   **MI损失：** 用于在调优阶段最大化互信息，稳定地适应新任务。
    -   **梯度丢弃（Gradient Dropout）：** 用于正则化更新，防止对固定参数子集的过度依赖和过拟合。

### 实验设计

**1. 使用数据集与场景**

-   **基准数据集（共5个，每个随机分为10个不重叠的任务）：**
    -   CIFAR-100
    -   ImageNet-R
    -   ImageNet-A
    -   CUB-200
    -   Cars-196
-   **场景：** 标准的多任务类增量学习（Class-Incremental Learning）场景。

**2. 对比方法（Baselines）**

-   **主流的冻结式方法（6种，MIST作为插件融入其中）：**
    -   基于提示（Prompt）：L2P, DualPrompt
    -   基于适配器（Adapter）：RanPAC, EASE
    -   全微调变种：SLCA（降低学习率进行微调）
    -   无参数微调：SimpleCIL（直接训练分类器）
-   **其他对比方法：**
    -   传统持续学习方法：EWC
    -   基于互信息的持续学习方法：OCM
    -   其他近期方法：CODA-Prompt, SLCA++, APER

**3. 评价指标**

-   **平均准确率（Average Accuracy, \(\bar{A}\) 和 \(A_T\)）：** 这是持续学习最核心的评估指标，衡量模型在所有已学任务上的平均性能。

### 资源与算力

-   **文中提及：** 论文在效率分析部分（Table 3）提到训练单个批次的时间（Time）是在 **NVIDIA RTX 4090 GPU** 上测量的。
-   **未明确说明：** 论文**没有明确提供**训练所有实验所需的**总GPU数量**、**总训练时长**或**总计算开销（如GPU·小时）**。对于MIST的预适应阶段，仅提及训练了20个epoch，学习率为0.0001。

### 实验数量与充分性

**1. 实验数量**

论文设计了非常详尽的实验，包括：
-   **主实验（Table 1）：** 在5个数据集上，将MIST嵌入到6种基线方法中，形成了大量对比组（约30+个结果）。这是最核心的实验。
-   **性能分析图（Fig. 3, 4）：** 展示了新任务准确率和增量准确率随任务变化的情况，直观证明了MIST对可塑性的提升。
-   **消融实验（Table 2）：** 系统地对比了不同稀疏策略（随机、L2范数、梯度幅值）、不同损失函数（CE vs MI）以及有无梯度丢弃的效果，共3组（a, b, c）实验。
-   **效率分析（Table 3）：** 对比了MIST与其他方法的参数量、FLOPs和训练时间。

**2. 充分性与公平性**

-   **充分性：** 实验覆盖了不同类型的基线（提示、适配器、全微调）、多个难度不同的数据集、以及详尽的消融研究，证明了MIST的通用性和有效性。实验结论扎实。
-   **公平性：** 作者声明遵循了先前工作的实现（如ViT-B/16骨干、优化器选择等），这保证了对比的公平性。MIST作为插件的设计，使其能以最小的改动公平地与所有基线方法进行比较。

### 论文主要结论与发现

1.  **MIST持续提升性能：** 将MIST作为插件应用于6种冻结式持续学习方法，在所有5个数据集上均取得了**一致且显著的平均准确率提升**。例如，在Cars-196数据集上，SimpleCIL+MIST的最终准确率提升了15.7%。
2.  **有效提升可塑性：** MIST显著提升了模型在学习新任务时的准确率（Fig. 3），表明其有效增强了模型的可塑性。
3.  **稀疏策略的优越性：** 基于互信息的稀疏选择（MS）远优于传统的基于梯度幅值或参数范数的选择策略。
4.  **组件协同增益：** MI基稀疏选择、MI损失和梯度丢弃三个组件缺一不可，协同作用才能达到最佳效果。
5.  **低计算代价：** 作为一种稀疏调优方法，MIST引入的计算开销极低，更新参数仅为总参数的0.5%，易于嵌入其他框架。

### 优点：方法与实验设计的亮点

1.  **创新性的理论分析：** 从信息论（互信息）和梯度分析的角度，深刻揭示了现有冻结式方法可塑性不足和全微调方法结构破坏的根本原因，为稀疏调优策略提供了坚实的理论依据。
2.  **即插即用的设计：** MIST设计为一种预适应插件，能与绝大多数现有冻结式方法无缝集成，通用性强，实用价值高。
3.  **极低的参数量更新：** 每批次仅更新0.5%的参数，不仅计算高效，也极大地降低了对预训练知识的干扰风险，是“四两拨千斤”的典范。
4.  **详尽的消融实验：** 通过精心设计的消融实验（Table 2），清晰地分离并验证了方法中各组件（稀疏策略、损失函数、梯度丢弃）的贡献，逻辑严谨。
5.  **梯段丢弃机制（Gradient Dropout）：** 这是一个简单但有效的正则化技巧，能够避免对固定参数子集过度更新，提升了训练的稳定性。

### 不足与局限

1.  **Fisher矩阵近似的可靠性：** 论文明确指出其局限性在于对MI Fisher矩阵的近似计算。当任务内部数据分布不均（存在显著分布差异）时，这种基于小批量的近似可能会不准确，从而影响参数敏感性估计的效果，降低MIST的性能。
2.  **计算开销的隐忧：** 虽然更新参数少，但计算MI损失（\( L_{MI} \)）需要生成每个样本的增广视图（augmented view），这增加了每次迭代的计算开销。这在某些对延迟极其敏感的场景可能是个问题，但相较于全微调，总体开销仍然较低。
3.  **实验覆盖的局限：** 论文主要基于ViT-B/16这一个预训练模型架构。虽然实验结果具有很强的说服力，但未测试在其他PTM（如ResNet, Swin Transformer等）上的表现，其跨架构的普适性有待进一步验证。
4.  **基线方法的覆盖：** 虽然覆盖了多种代表性方法，但消融实验主要是在RanPAC这一个较强的基线上进行的（Table 2）。如果在其他不同类型的基线上进行更多消融，结论会更坚实。
5.  **超参数敏感性：** 方法引入了两个关键超参数（选择率k%和丢弃率d%），论文中固定了其值（5%, 90%），但未充分讨论它们对性能的敏感性。在不同任务或数据集上，这些超参数可能需要调整。

（完）
