---
title: Decoupling Shared and Modality-Specific Subspaces in Multimodal Learning via Low-Rank Representation Fine-Tuning
title_zh: 通过低秩表示微调解耦多模态学习中的共享和模态特定子空间
authors: "Sana Tonekaboni, Viktoria Schuster, Caroline Uhler"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=aiJtxcNbqB"
tags: ["query:multimodal"]
score: 8.0
evidence: 通过低秩微调解耦多模态子空间
tldr: 本文提出MultiLoReFT框架，将低秩表示微调扩展到多模态学习。通过学习可解释的投影子空间，解耦共享和模态特定信息，同时自适应调整子空间秩。该方法提升了多模态模型的解释性和训练效率，在多模态任务上具有实用性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-aijtxcnbqb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1451, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-aijtxcnbqb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1435, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-aijtxcnbqb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1438, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-aijtxcnbqb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 743, \"height\": 469, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1461, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1557, \"height\": 657, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 698, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1448, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 444, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1296, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1488, \"height\": 930, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-aijtxcnbqb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 891, \"height\": 440, \"label\": \"Table\"}]"
motivation: 多模态模型训练计算昂贵且缺乏解释性，现有方法无法有效分离共享和模态特定信息。
method: 提出MultiLoReFT，利用低秩表示微调学习可解释的子空间，自适应调整秩以解耦信息。
result: 在多个多模态任务上验证了方法的有效性和效率，提升了模型的可解释性。
conclusion: MultiLoReFT为多模态模型的解释性和高效训练提供了新途径。
---

## Abstract
Multimodal data in machine learning promises to improve generalization and performance on complex tasks. However, training multimodal models requires extensive paired datasets, can be computationally expensive, and lacks transparency by entangling shared and modality-specific signals in ways that hinder interpretability and control. In this work, we introduce MultiLoReFT: a low-rank representation fine-tuning framework for multimodal learning using pretrained unimodal models. Our approach extends low-rank representation finetuning to the multimodal setting and learns interpretable projection subspaces that decouple shared and modality-specific information. MultiLoReFT adaptively learns the rank of each subspace to best capture complementary contributions of each modality with minimal trainable parameters.  Our method offers an efficient and scalable solution to adapting pretrained representations for multimodal reasoning, enabling interpretable fine-tuning across both synthetic and real-world benchmarks.

---

## 论文详细总结（自动生成）

# 论文结构化中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：多模态机器学习（如图像-文本对、视频-音频等）在实际应用中面临三大挑战：①需要大量对齐的配对数据，获取成本高；②从头训练多模态模型计算开销大；③共享信息与模态特有信息纠缠在一起，导致模型缺乏可解释性和可控性。
- **背景**：现有方法多采用预训练的单模态编码器（如BERT、ViT）进行微调，但全参数微调仍效率低下，且未能显式分离共享与特有信息。参数高效微调（PEFT）方法如LoRA、LoReFT虽然降低了参数量，但尚未在多模态场景下实现信息解耦。
- **整体含义**：该论文旨在提出一种低秩表示微调框架，在冻结预训练单模态编码器的同时，学习可解释的投影子空间，将共享信息和各模态特有信息解耦，从而提升效率、可解释性和跨模态泛化能力。

## 2. 论文提出的方法论：核心思想与关键技术细节

### 核心思想
- 将低秩表示微调（LoReFT）扩展至多模态场景，为每个模态学习两个投影子空间：一个共享子空间（捕获跨模态共有信息）、两个模态特有子空间（分别捕获各模态独有信息）。
- 通过低秩投影矩阵（R_s, R_m1, R_m2）将原始表示映射到子空间，并在子空间内学习轻量变换（f_s, f_m），然后投影回原始空间得到微调后的表示。
- 引入自适应秩剪枝机制，动态调整每个子空间的秩，避免过参数化或信息冗余。

### 关键技术细节
- **表示编辑公式**：对于模态i，微调表示为：
  Φ_i = h_i + R_s^T (f_s(h_i) - R_s h_i) + R_{mi}^T (f_{mi}(h_i) - R_{mi} h_i)
  其中h_i为冻结编码器输出，R_s、R_{mi}为低秩投影矩阵，f_s、f_{mi}为子空间内变换（如MLP）。
- **损失函数**：包含三个部分：
  - **独立性损失**（Lindep）：使用HSIC（希尔伯特-施密特独立性准则）强制共享与模态特有成分之间、以及两个模态特有成分之间统计独立。
  - **正交性损失**（Lorth）：最小化共享子空间与模态特有子空间投影矩阵的Frobenius内积，确保几何上正交。
  - **互信息损失**（LMI）：采用InfoNCE对比损失，保证微调后的投影保留原始表示的信息。
- **多阶段训练策略**：
  - Stage 1：仅优化共享子空间，使用LMI。
  - Stage 2：仅优化模态特有子空间，使用Lorth+Lindep+LMI。
  - Stage 3：联合优化全部参数，并启动自适应秩剪枝。
- **自适应秩剪枝**：对每个投影矩阵进行SVD，剪除低于阈值ϵ的奇异值对应的维度，更新矩阵为低秩形式，并调整关联变换层的输出维度。
- **超参数自适应**：使用Gradient Normalization自动平衡多损失项权重。

### 算法流程（文字说明）
1. 输入多模态数据，通过预训练编码器得到表示h1, h2。
2. 分阶段训练：先共享，后私有，最后联合。
3. 每次前向计算微调表示Φ1, Φ2，并提取子空间投影zs, zm1, zm2。
4. 计算LMI、Lindep、Lorth，通过梯度归一化聚合。
5. 联合阶段每轮验证后，若收敛则触发秩剪枝（Alg. 2）。
6. 循环直至所有阶段收敛。

## 3. 实验设计

### 数据集
- **合成数据集 Simulation I & II**：具有已知生成结构的双模态数据，提供共享标签、模态1特有标签、模态2特有标签，用于验证解耦正确性。Simulation I中隐变量独立；Simulation II引入跨模态依赖。
- **Flickr30K-Multi**：图像-多语言文本数据，选取英语和法语，语言类别作为模态特有标签。
- **Crema-D**：视频-音频情感表达数据集，标注了句子ID、种族、性别、情感等，用于评估下游任务和解耦。

### 对比方法
- **通用融合方法**：Late fusion（串联）、Cross attention、Multiplicative Interactions (MI)、Contrastive learning。
- **解耦方法**：APOLLO（基于潜变量优化的自编码器）、DRIM-U（基于重建和对抗正则化的自监督解耦）。
- 所有方法均使用相同的预训练编码器输出作为输入，仅适配器结构不同。

### 评估指标
- 解耦评估：训练逻辑回归模型用各子空间表示预测对应标签，报告准确率（分类）或MSE（回归），重点考察正确成分与错误成分的性能差距（Δ）。
- 跨模态学习评估：用融合表示预测联合标签（如情感），比较微调前后单模态表示的性能提升。

## 4. 资源与算力

- 论文中**未明确说明**所使用的GPU型号、数量及具体训练时长。
- 仅提到方法参数量少（投影矩阵+小变换函数），且训练流程（多阶段和剪枝）在标准硬件上可运行，但无量化数据。

## 5. 实验数量与充分性

### 实验数量
- 在**两个合成数据集**上做了完整的解耦评估（表1、图2）。
- 在**两个真实数据集**（Flickr30K、Crema-D）上做了解耦评估（表2）和融合预测（表3a）。
- 包含了**消融实验**（附录A.2.2）：分别移除剪枝、移除多阶段训练、移除各损失项，以及使用固定损失权重。
- 对**秩剪枝效果**做了补充实验（表4、表7），展示了初始和收敛秩。
- 对**单模态编码器强度的影响**做了附加实验（表8）。
- 实验合计约8个主要表格+3个主要图，外加附录中多个表格。

### 充分性与公平性
- **解耦评估**：通过预测已知标签，直接验证信息是否落在正确子空间，设计直接有效。
- **公平性**：对比方法均使用相同预训练编码器输出，基准方法的子空间维度设为MultiLoReFT剪枝后的最终维数（提供了优势），但仍被全面超越；如果使用固定大维度，基准性能下降（表4），说明剪枝的必要性。
- **统计性**：多次随机种子运行并报告均值±标准差，结果稳健。
- **不足**：所有实验均为2模态场景，未扩展至3模态以上；真实数据集标签可能并非完全对应于“特有”或“共享”，需依赖任务假设。

## 6. 论文的主要结论与发现

1. **MultiLoReFT能够有效解耦共享和模态特有信息**：在合成和真实数据上，相应子空间对对应标签预测性能最高，其他子空间性能接近随机，且性能差距Δ显著大于对比方法。
2. **自适应秩剪枝提升了效率和鲁棒性**：模型自动将高维初始子空间剪枝为低维稳定表示（如Crema-D上共享子空间从700→30），且不同种子间一致。
3. **微调同时提升下游任务表现**：融合后的表示在情感分类等任务上优于全连接融合、注意力融合、对比学习及现有解耦方法；且较弱模态受益更大（跨模态信息迁移）。
4. **高容量单模态编码器可进一步提升多模态性能**：使用更强编码器，所有方法提升，但MultiLoReFT提升幅度更明显，且方法排名稳定。

## 7. 优点

- **参数高效**：仅需学习低秩投影矩阵和小型变换函数，参数量远小于全参数微调。
- **可解释性强**：显式将表示分解为共享、模态1特有、模态2特有三个成分，可单独分析各成分对下游任务的贡献。
- **自适应秩剪枝**：无需手动设定子空间维度，自动从数据中学习合适秩，消除对超参数的敏感度。
- **多阶段训练策略**：逐步优化不同子空间，避免联合训练早期的竞争，稳定收敛。
- **损失设计合理**：HSIC保证统计独立性，正交性保证几何分离，InfoNCE保留信息完整性，三者互补。
- **实验设计严谨**：使用已知标签的合成数据作为“ground truth”验证解耦，真实数据集做多任务评估，消融实验全面。

## 8. 不足与局限

- **仅支持2模态**：论文聚焦双模态场景，虽理论上可扩展至更多模态，但会引入“部分共享”复杂性和可解释性降低的问题，未在实验中验证。
- **依赖预训练编码器质量**：如果单模态编码器本身无法捕获该模态相关信息（如低质量情况下），微调提升有限。附录虽验证了更强编码器的优势，但未讨论编码器失效的边界条件。
- **未报告算力消耗**：缺少GPU型号、训练时间等具体信息，难以评估实际部署成本。
- **无真实标签的共享/特有验证**：在真实数据上，标签（如句子ID、种族）是否真正属于“模态特有”或“共享”需基于先验假设，可能与其他因素混淆。例如，Crema-D中句子ID主要通过音频体现，但视频也可能包含微弱唇动信息。
- **未与其他最新的多模态解耦方法（如FactorCL、Triple Disentanglement）对比**：实验中仅对比了APOLLO和DRIM-U，未包含同样声称解耦的FactorCL等更近方法（尽管可能因篇幅限制）。
- **可解释性在真实场景中的实用性未深入探讨**：虽展示了子空间可视化，但未分析解耦后的成分如何被用于下游可解释AI（如归因、反事实推理）。

（完）
