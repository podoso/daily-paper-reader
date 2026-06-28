---
title: Expandable and Differentiable Dual Memories with Orthogonal Regularization for Exemplar-free Continual Learning
title_zh: 基于正交正则化的可扩展可微分双记忆无样本持续学习
authors: "Hyung-Jun Moon, Sung-Bae Cho"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39626/43587"
tags: ["query:continual"]
score: 9.0
evidence: 无需样本的持续学习，使用可扩展双记忆与正交正则化
tldr: 持续学习方法常要求隔离任务，忽视任务间关系导致重复学习。本文提出全可微分的可扩展双记忆方法：一个记忆学习跨任务共享特征，另一个学习样本独特特征，并辅以正交正则化。无需存储旧样本，在多个持续学习基准上显著缓解遗忘并提升泛化。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法迫使网络隔离处理任务，无法利用任务间关系导致重复或过度区分。
method: 设计两个互补记忆分别学习共享特征和判别特征，通过正交正则化增强区分性。
result: 在无样本持续学习设定下，有效缓解遗忘并实现任务间知识迁移。
conclusion: 双记忆架构为无样本持续学习提供了可扩展且高效方案。
---

## Abstract
Continual learning methods used to force neural networks to process sequential tasks in isolation, preventing them from leveraging useful inter-task relationships and causing them to repeatedly relearn similar features or overly differentiate them. To address this problem, we propose a fully differentiable, exemplar-free expandable method composed of two complementary memories: One learns common features that can be used across all tasks, and the other combines the shared features to learn discriminative characteristics unique to each sample. Both memories are differentiable so that the network can autonomously learn latent representations for each sample. For each task, the memory adjustment module adaptively prunes critical slots and minimally expands capacity to accommodate new concepts, and orthogonal regularization enforces geometric separation between preserved and newly learned memory components to prevent interference. Experiments on CIFAR-10, CIFAR-100, and Tiny-ImageNet show that the proposed method outperforms 14 state-of-the-art methods for class-incremental learning, achieving final accuracies of 55.13%, 37.24%, and 30.11%, respectively. Additional analysis confirms that, through effective integration and utilization of knowledge, the proposed method can increase average performance across sequential tasks, and it produces feature extraction results closest to the upper bound, thus establishing a new milestone in continual learning.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

持续学习旨在让模型按顺序学习多个任务，同时保持对旧任务的性能。然而，灾难性遗忘是核心难题，尤其在无样本（exemplar-free）设定下，因为没有旧样本可供回放，新训练会覆盖先前知识，或需要牺牲可塑性来保护稳定性。现有方法主要分为两类：

- **正则化方法**：通过对参数更新施加惩罚（如知识蒸馏）来防止干扰，但会过度限制模型的可塑性。
- **动态架构扩展/参数隔离方法**：为每个新任务分配专用神经元并冻结旧参数，但导致模型无节制增长，且忽略任务间关系，无法复用先前知识。

本文指出，这些方法将未来任务视为完全独立，阻碍了跨任务共享知识。因此，论文提出一种**可扩展、可微分的双记忆方法（EDD）**，通过将数据分解为子特征并存储在两个互补记忆中，实现知识复用和特征分离，在无样本条件下有效缓解遗忘并提升性能。

## 2. 论文提出的方法论

### 核心思想

受互补学习系统理论启发，EDD包含两个可微分记忆：

- **共享记忆（Mᵗ）**：编码所有任务通用的可迁移特征。
- **任务专用记忆（Mᵗ）**：基于共享特征，捕获每个样本的细粒度判别特征。

两个记忆均以键-值对形式存储，并通过余弦注意力机制读取。模型通过梯度下降端到端学习记忆参数。

### 关键技术细节

#### 2.1 可微分记忆读取
给定中间特征图 H，每个空间特征向量 h 作为查询，计算与所有键 kⱼ 的余弦相似度，得到注意力权重 wⱼ，输出为值向量的加权和：  
\[ \hat{h} = \sum_{j} w_j v_j \]  
记忆参数与编码器、分类器联合优化。

#### 2.2 记忆扩展与知识剪枝（Memory Adjustment）
在每个任务训练结束后，计算每个记忆槽的参数变化量 Δ，将变化最大的部分槽（即对该任务贡献最大的槽）冻结，并根据新任务类别数比例添加等量新槽。被冻结的旧槽保留知识且不再更新，新槽提供可塑性。这样既控制了模型增长，又防止了遗忘。

#### 2.3 正交正则化（Orthogonal Regularization）
仅在任务专用记忆 Mᵗ 上施加正交正则化，强制冻结槽的键/值与新激活槽的键/值之间正交，从而在几何上分离旧知识与新知识，减少干扰。损失函数为：  
\[ \mathcal{L}_{\text{orth}} = \|K^F (K^U)^\top\|_F^2 + \|V^F (V^U)^\top\|_F^2 \]

#### 2.4 记忆引导的表示对齐（Memory-Guided Representation Alignment）
为了保留旧任务的知识，将当前任务输入同时送入新模型和上一个任务的冻结模型，最小化两者在记忆上的注意力模式差异（余弦距离）：  
\[ \mathcal{L}_{\text{align}} = \sum_{\ell\in\{s,t\}} \mathbb{E}_{x\sim T_t} \left[ 1 - \cos(A^\ell_{\text{new}}(x), A^\ell_{\text{old}}(x)) \right] \]  
这相当于无样本的知识蒸馏，确保当前模型沿用之前的记忆激活模式。

#### 2.5 训练流程
- 第一个任务：仅使用分类损失训练，不施加对齐和正交正则化。
- 后续任务：加载上一个冻结模型，先对其 Batch Normalization 层在新任务数据上做少量前向传递（无梯度）以校准分布；然后复制模型作为当前模型，在分类损失基础上加上对齐损失和正交正则化损失；训练结束后执行剪枝和扩展。

## 3. 实验设计

### 数据集与场景
- **CIFAR-10**：5 个任务，每个任务 2 类（S-CIFAR-10）
- **CIFAR-100**：10 个任务（每任务 10 类）和 20 个任务（每任务 5 类）
- **Tiny-ImageNet**：10 个任务（每任务 20 类）和 20 个任务（每任务 10 类）

所有实验均采用**无样本（exemplar-free）类增量学习（Class-IL）**设定，即模型不能使用任何旧样本。

### Benchmark 与对比方法
对比了 14 种最新方法，包括：
- 正则化/回放类：SI、o-EWC、LwF、A-GEM、HAL、GEM、FDR、LwF-MC
- 动态架构类：PNN、DualNet、LUCIR、RPC、GSS、PEC
- 也报告了联合训练（JT）和微调（FT）作为上下界。

### 关键实验结果
- 在所有设定下，EDD 均取得了最高准确率，例如 S-CIFAR-10 上 55.13%（第二名为 PEC 52.19%），S-CIFAR-100 10 任务 37.24%（第二名为 RPC 31.08%），S-Tiny-ImageNet 10 任务 30.11%（第二名为 LUCIR 25.84%）。
- 随着任务序列增长（从 10 任务到 20 任务），EDD 的相对提升幅度更大，尤其在 Tiny-ImageNet 上提升超过 26%。

## 4. 资源与算力

论文中未明确说明实验所使用的 GPU 型号、数量或训练时长。仅提及代码基于 PyTorch，使用 ResNet-18 骨干，Adam 优化器，批量大小 128，训练 50 个 epoch。具体的硬件配置没有披露。因此，无法评估其计算代价的绝对数值，仅能通过理论复杂度分析了解其相对效率。

## 5. 实验数量与充分性

论文进行了以下实验：
- **三个基准数据集上的类增量学习对比**：涵盖 CIFAR-10、CIFAR-100、Tiny-ImageNet，每个数据集有不同任务拆分，共 5 种设定。
- **消融实验**（表 2）：在 CIFAR-100 和 Tiny-ImageNet 的 10 任务设定下，依次加入对齐损失、正交正则化、批归一化适应，每个组件均有正贡献，累计提升显著。
- **遗忘动态分析**（图 4、图 5）：绘制了每个任务上的分类准确率曲线，显示 EDD 遗忘更慢且中间任务准确率不下降。
- **特征对齐分析**（图 6、图 7）：使用余弦相似度、KL 散度、Wasserstein 距离、特征距离等指标，比较各方法与联合学习的特征表示，EDD 最接近上界。
- **时间和空间复杂度分析**：给出了理论复杂度论述。

整体实验充分，覆盖了不同难度、不同任务长度，且消融实验清晰验证了各组件必要性。对比方法包含 14 种，涵盖主流方法，设置公平（均采用相同骨干和训练配置）。但论文未报告超参数敏感性分析或多次随机种子下的完整方差（表中只给出了均值±标准差，但多数仅一次？注意表中格式如“55.13 ± 0.21”，说明有多次运行），统计上较规范。

## 6. 论文的主要结论与发现

1. **EDD 在无样本类增量学习中显著优于所有对比方法**，包括需要缓冲的方法，例如 LUCIR、DualNet。
2. **双记忆系统能够有效分离共享特征和任务专用特征**，通过正交正则化进一步减少干扰，从而缓解灾难性遗忘。
3. **记忆扩展与剪枝机制实现了可控的增长**，避免了无限膨胀，同时保留了过去知识。
4. **EDD 学习到的特征表示与联合学习上界最为接近**，表明其能够有效整合和利用知识，而非简单地隔离任务。
5. **在长任务序列上，EDD 的相对优势更大**，证明了其在更复杂场景下的可扩展性和鲁棒性。

## 7. 优点

- **创新性地融合了可微分记忆、动态剪枝扩展、正交正则化和无样本蒸馏**，在无样本设定下实现了极佳的稳定-可塑性权衡。
- **无需存储任何旧样本**，符合隐私和存储受限的真实场景。
- **对照了 14 种方法**，包括经典和最新方法，对比全面且结果令人信服。
- **提供了深入的特征分析**，不仅报告准确率，还从特征空间角度验证表示质量。
- **理论与复杂度分析透明**，有利于后续研究。
- 代码已开源，可复现性强。

## 8. 不足与局限

- **未报告具体硬件与训练时间**，难以复现并评估实际计算开销。
- **内存管理开销随任务数线性增长**，尽管仍可控，但在极长任务序列（如数百个任务）下可能成为瓶颈。
- **在任务间共享结构极少的情况下**（如完全随机任务），共享记忆可能难以捕获通用特征，泛化性可能受限。
- **仅验证在 ResNet-18 骨干上**，未探索更大的模型（如 ResNet-50、ViT）或不同架构的适用性。
- **实验仅在三种图像分类基准上进行**，未涉及序列决策、自然语言处理等场景，通用性有待验证。
- **超参数 λ_mem 和 λ_orth 的选取**未提供敏感性分析，可能影响实际应用调参。
- **对批归一化校准的细节描述**不够，可能对长任务序列的分布漂移处理不够鲁棒。

（完）
