---
title: Towards Multimodal Continual Knowledge Embedding with Modality Forgetting Modulation
title_zh: 面向多模态持续知识嵌入的模态遗忘调制
authors: "Xiaowen Jiang, Jing Yang, ShunDong Yang, Yuan Gao, Xinfa Jiang, Laurence Tianruo Yang, Jieming Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38516/42478"
tags: ["query:continual"]
score: 9.0
evidence: 多模态持续知识嵌入缓解灾难性遗忘
tldr: 多模态知识图持续演化，但现有模型在增量学习时易发生灾难性遗忘。本文提出MoFot框架，通过模态遗忘调制技术缓解遗忘，无需从头训练。该方法在多模态知识嵌入任务上有效保持历史知识，适用于动态知识图谱场景。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有静态多模态知识图嵌入模型无法适应动态增长，增量微调导致灾难性遗忘。
method: 提出模态遗忘调制机制，在持续学习过程中选择性抑制遗忘，保留跨模态知识。
result: 在多模态知识图增量学习中显著缓解灾难性遗忘，优于静态重训练和微调方法。
conclusion: MoFot为持续知识嵌入提供有效方案，平衡稳定性与可塑性。
---

## Abstract
The continuous emergence of new entities, relations, triples, and multimodal information drives the dynamic evolution of multimodal knowledge graph (MMKG). However, existing MMKG embedding models follow a static setting, where training from scratch for growing MMKG wastes learned knowledge, while fine-tuning on new knowledge easily leads to catastrophic forgetting, severely limiting their applicability in real-world scenarios. To address this, we propose a multimodal continual representation learning framework (MoFot) for growing MMKG. Unlike existing static multimodal embedding methods, MoFot focuses on alleviating catastrophic forgetting rather than retraining to adapt to new knowledge. Specifically, MoFot effectively mitigates catastrophic forgetting caused by parameter updates and differing forgetting rates across modalities through a multimodal collaborative modulation mechanism. The mechanism ensures consistent retention of  previously learned multimodal knowledge across snapshots through multimodal weight modulation and multimodal feature modulation. MoFot outperforms existing MMKG embedding, KG continual learning, and MMKG inductive models.  Experimental results demonstrate that MoFot not only avoids forgetting but also enhances old knowledge by learning new knowledge, achieving adaptation to new knowledge while mitigating forgetting of old knowledge.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：多模态知识图谱（MMKG）在真实场景中持续演化，新实体、新关系、新三元组以及新多模态数据不断出现。然而，现有的 MMKG 嵌入模型（如 MKBE、MKGC、VBKGC、NativE、IMF、MoCi、AdaMF 等）均采用**静态设定**，无法有效处理动态增长。
- **核心问题**：若从头训练整个增长后的 MMKG，会浪费已学知识且时间成本极高；若仅在新数据上微调，则容易发生**灾难性遗忘**——模型在学习新知识时迅速遗忘旧知识。此外，不同模态（文本、图像、结构）在持续学习中的遗忘速率不同，导致模态间特征偏移，进一步加剧性能退化。
- **整体意义**：本文首次提出面向增长中 MMKG 的**多模态持续表示学习框架 MoFot**，旨在无需重训练的前提下，在适应新知识的同时有效缓解灾难性遗忘，为动态知识图谱的持续学习提供了新思路。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
MoFot 通过**多模态协同调制机制**（Multimodal Collaborative Modulation）同时解决两个遗忘来源：
- 参数更新导致的遗忘；
- 模态间遗忘速率不一致导致的遗忘。

该机制包含两个分支：**多模态权重调制**和**多模态特征调制**。

### 关键技术细节

#### (1) 关系驱动的路径传递（Relation‑Driven Path Passing）
- 使用 NBFNet 架构建模每个查询三元组 `(s, q, ?)` 的路径语义。通过关系聚合更新实体表示，捕获从头部实体到所有其他实体的完整路径信息。
- 路径表示 `z_{o|s,q}` 经多层传播得到，用于后续的特征调制。

#### (2) 历史路径保留（Historical Path Preservation，HPP）
- 定义查询关系 `x_q` 与所有关系 `x_r` 的拼接操作 `Ψ_q(x_r)`，并利用查询专属权重矩阵 `W_i^q` 和偏置 `b_i^q` 进行融合。
- 对新快照中新增的关系嵌入进行拼接初始化，同时对旧关系嵌入施加 L2 正则约束（公式 4），以保留先前快照中的路径语义。

#### (3) 路径引导的多模态特征调制（Path‑Guided Multimodal Feature Modulation，PGF）
- 将保留旧结构知识的路径表示作为注意力机制的 query/key，引导文本和视觉特征向路径语义对齐。
- 首先融合视觉、文本与路径特征得到 `Z_i^F`，然后采用线性复杂度的注意力机制（公式 6‑7）生成最终实体嵌入 `˜Z_{i}^{s,q}`，促进跨快照的多模态知识一致保留。

#### (4) 权重插值更新（Weight Interpolation Update，WIU）
- 对每个模态的独立权重（`W_i^V`、`W_i^T`、`W_i^q`）采用加权插值（公式 9）：`W_i^M = (1 - 1/i)W_{i-1}^M + (1/i) H(ΔW_i^M)`。
- 其中 `H(⋅)` 为统一缩放操作：先归一化新权重，再乘以一个可学习的缩放因子 σ（公式 10），实现方向和幅度的统一调制。
- 对多模态共享权重（`W_f, W_1, W_2`）则采用简化正则化（`ΔP2`）。

#### (5) 训练损失
- 使用负采样交叉熵损失，并加入路径保留正则项 `ΔP1` 和共享权重正则项 `ΔP2`（公式 11）。

## 3. 实验设计

### 数据集
- 基于五个基准 KG 持续学习数据集构造了五个多模态版本：**M-ENTITY**、**M-RELATION**、**M-FACT**、**M-HYBRID**、**M-GraphEqual**。每个数据集包含 5 个时间快照，分别由实体、关系、三元组或混合方式驱动增长。
- 文本和视觉特征分别使用 BERT 和 VGG16 提取。

### 基准方法
- **单模态持续学习模型**：PNN、EWC、SI、LKGE、IncDE。
- **静态 MMKG 模型**：MoCi、IMF（通过微调或重训练适应新数据）。
- **归纳式多模态模型**：IndMKG（仅在第一个快照训练，泛化到后续快照）。
- **多模态变体**：将 LKGE、IncDE 与三种多模态融合策略（双线性池化、自适应融合、MLP）结合得到 LKGE-M、IncDE-M。

### 评估指标
- **链接预测**：MRR、Hits@1、Hits@3、Hits@10。
- **知识保留与迁移**：后向迁移（BWT，负值表示遗忘，正值表示增强旧知识）、前向迁移（FWT）。

## 4. 资源与算力

- 文中未明确说明使用的 GPU 型号、数量及训练时长等具体算力信息。
- 仅在 **图 7** 中展示了训练时间对比：MoFot 的训练时间远低于 IMF 和 MoCi 的重训练模式，且与微调模式相比也更具优势（在 M-ENTITY 数据集上五轮快照总时间约 2000–3000 秒，而重训练超过 12000 秒）。但未提供硬件环境细节。

## 5. 实验数量与充分性

### 实验组数
- **主表（Table 1）**：在 5 个数据集上，与 10+ 个基线方法对比，报告了 MRR、Hits@1/3/10 等 4 项指标，共计约 200+ 个数值。
- **图 4**：展示了在 5 个数据集上每个单独快照的性能。
- **图 5**：展示了 MoFot 在三个数据集上对历史快照的保留性能（模型 M_i 在快照 1..i 上的测试结果）。
- **Table 2**：报告了三个数据集的 BWT 和 FWT 分数。
- **消融实验**（Table 3、Table 4）：分别移除 HPP、PGF、WIU 三个模块，在多模态和单模态设定下进行性能与 BWT 对比。
- **图 6**：模态消融，分别去除文本/视觉模态，以及去除特征调制和权重更新模块。
- **图 7**：训练效率对比。

### 充分性与客观性
- 实验覆盖了多种增长场景（实体、关系、三元组、混合），对比了最先进的持续学习模型和静态/归纳式多模态模型，基线丰富。
- 消融实验验证了各模块必要性，BWT/FWT 分析充分说明了遗忘缓解和知识迁移能力。
- 但未与更多最新多模态持续学习模型（如 Continual Multimodal KG Construction, Chen et al. 2024）进行直接对比（该工作仅在参考文献中提及）。
- 数据集由作者构建，缺乏使用广泛公开的 MMKG 持续学习基准（如 DBpedia、Wikidata 的动态版本），可能影响泛化性。

## 6. 主要结论与发现

1. **MoFot 在所有五个数据集上显著优于所有基线**，在 MRR、Hits@1/10 等指标上提升明显（例如 M-ENTITY 上 MRR 0.413 vs 第二名 IndMKG 0.372）。
2. **MoFot 实现了正的后向迁移（BWT 均为正或极小的负值）**，表明模型不仅不遗忘旧知识，反而通过学习新知识增强了旧知识。
3. **前向迁移能力（FWT）远高于其他方法**（M-ENTITY 上 0.387 vs 次优 LKGE 0.097），说明学到的知识可以有效帮助未来任务。
4. **多模态融合若不加以调制会加剧遗忘**，而 MoFot 的多模态协同调制机制有效地解决了模态间遗忘速率不一致的问题。
5. **权重插值更新和路径引导特征调制各自对缓解遗忘均有贡献**，且两者结合效果最佳。
6. **训练效率高**：MoFot 的累计训练时间远低于重训练方法，甚至优于微调方法，同时保持更好的长期性能。

## 7. 优点

- **首创性**：首次提出针对增长 MMKG 的多模态持续表示学习框架，填补了该领域空白。
- **方法设计巧妙**：同时从权重空间和特征空间两个层面针对遗忘根源进行调制，尤其关注模态间遗忘速率差异这一关键挑战。
- **实验全面**：涵盖多种增长模式、充分对比当前最优模型，并提供 BWT/FWT 分析客观量化遗忘程度。
- **结果惊艳**：不仅缓解遗忘，还能增强旧知识（正 BWT），兼顾稳定性和可塑性。
- **代码开源**：提供了 GitHub 仓库，可复现性良好。

## 8. 不足与局限

- **算力信息缺失**：未报告 GPU 型号、显存、训练周期等硬件细节，不利于其他研究者复现成本评估。
- **数据集自定义**：实验所用数据集是由作者在已有 KG 持续学习数据集基础上添加多模态特征构建的，并非广泛使用的公开 MMKG 标准持续学习基准，可能引入偏差，且未在真实大规模动态 MMKG（如 Wikidata 带时间戳版本）上验证。
- **与最新多模态持续学习相关工作对比不足**：虽然引用了 Chen et al. 2024（Continual Multimodal KG Construction），但未将其作为基线比较，可能遗漏竞争对手。
- **跨快照数量有限**：仅 5 个快照，可能不足以完全验证长期持续学习（如 10+ 快照）下的遗忘行为。
- **模态种类有限**：仅使用了文本和图像两种模态，未涉及视频、音频等多模态数据，实际 MMKG 可能更丰富。
- **未讨论模型容量随快照增长的可扩展性**：权重插值需要额外存储旧快照的权重，且共享权重正则化可能限制模型表达。

（完）
