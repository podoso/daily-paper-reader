---
title: Multimodal Classification via Total Correlation Maximization
title_zh: 通过总相关最大化进行多模态分类
authors: "Feng Yu, Xiangyu Wu, Yang Yang, Jianfeng Lu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=MbQhdzAhSl"
tags: ["query:multimodal"]
score: 7.0
evidence: 通过总相关最大化进行多模态分类
tldr: 多模态学习常过拟合某些模态而忽略其他。本文从信息论角度分析模态竞争，提出通过最大化多模态特征间的总相关来进行分类，缓解模态退化，在多个数据集上优于联合和单模态方法。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-mbqhdzahsl/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 529, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mbqhdzahsl/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1305, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mbqhdzahsl/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 764, \"height\": 317, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mbqhdzahsl/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 609, \"height\": 581, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-mbqhdzahsl/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1393, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mbqhdzahsl/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1443, \"height\": 503, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mbqhdzahsl/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 710, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mbqhdzahsl/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 673, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mbqhdzahsl/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1448, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mbqhdzahsl/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1197, \"height\": 263, \"label\": \"Table\"}]"
motivation: 多模态联合学习常忽略弱模态，性能不如单模态。
method: 从信息论分析模态竞争，提出最大化多模态特征总相关的分类方法。
result: 在多个数据集上优于联合和单模态学习方法。
conclusion: 总相关最大化有效平衡模态贡献。
---

## Abstract
Multimodal learning integrates data from diverse sensors to effectively harness information from different modalities. However, recent studies reveal that joint learning often overfits certain modalities while neglecting others, leading to performance inferior to that of unimodal learning. Although previous efforts have sought to balance modal contributions or combine joint and unimodal learning—thereby mitigating the degradation of weaker modalities with promising outcomes—few have examined the relationship between joint and unimodal learning from an information-theoretic perspective.
    In this paper, we theoretically analyze modality competition and propose a method for multimodal classification by maximizing the total correlation between multimodal features and labels. By maximizing this objective, our approach alleviates modality competition while capturing inter-modal interactions via feature alignment. Building on Mutual Information Neural Estimation (MINE), we introduce **T**otal **C**orrelation **N**eural **E**stimation (**TCNE**) to derive a lower bound for total correlation. Subsequently, we present TCMax, a hyperparameter-free loss function that maximizes total correlation through variational bound optimization. Extensive experiments demonstrate that TCMax outperforms state-of-the-art joint and unimodal learning approaches. Our code is available at https://anonymous.4open.science/r/TCMax_Experiments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

多模态学习中，联合学习（joint learning）常导致模态不平衡：某些模态（强模态）被充分拟合，而弱模态被忽略，最终使得多模态模型性能甚至不如单模态模型。现有方法尝试通过梯度调制或引入单模态损失来平衡模态贡献，但鲜有从信息论角度深入分析模态竞争的本质。本文旨在填补这一空白，并从信息论视角提出一种新的学习目标——最大化多模态特征与标签之间的**总相关（Total Correlation, TC）**，以同时利用联合学习、单模态学习和模态对齐的优势，解决模态退化问题。

### 2. 论文提出的方法论

- **核心思想**：将模态竞争归因于联合学习目标（最大化互信息 I(y; Z)）的分解特性。以两个模态为例，I(y; Z)=I(y; z^a) + I(y; z^v|z^a)，当音频模态信息充足时，条件互信息项的上界很小，导致视觉模态难以学习。而单模态学习（最大化 I(y; z^a) + I(y; z^v)）可避免竞争但无法捕捉跨模态交互。总相关 TC(z^a, z^v, y) 同时包含联合学习项 I(y; z^a, z^v)、模态对齐项 I(z^a; z^v) 以及单模态学习项 I(y; z^a) + I(y; z^v) + I(z^a; z^v|y)（见公式6）。因此，最大化 TC 可融合三者优势。

- **关键技术与细节**：
  - 基于 MINE 提出 **Total Correlation Neural Estimation (TCNE)**，给出 TC 的下界估计器（公式10）。
  - 设计 **TCMax 损失函数**（公式11）：L_TCMax = -E_{P_Z,Y}[f_θ] + log(E_{P_Z×P_Y}[e^{f_θ}])，其中 f_θ 为多模态模型的预测头输出 logits。该损失无需额外超参数。
  - 理论上证明（命题1-3）：最小化 L_TCMax 等价于提高 TC 的下界；当模型最优时，其输出可精确估计联合分布 P(x^(1),...,x^(M), y)，且预测时与联合学习无异（直接 softmax）。
  - 计算优化：对线性融合（f_θ(z^a, z^v)=f^a_θa(z^a)+f^v_θv(z^v)），损失可分解为两个独立的和，只需 |B| 次前向传播（公式16），大幅降低开销。

### 3. 实验设计

- **数据集**：
  - 音频-视觉分类：CREMA-D（情感，6类，7442样本）、Kinetics-Sounds（KS，31类，19000样本）、AVE（28类，4143样本）、VGGSound（309类，152638训练+13294测试）、UCF101（101类，13320样本，RGB+光流）。
  - 文本-图像情感分析：MVSA（MVSA-Single）。

- **Benchmark**：对比基线方法包括 Concat、Share Head、Unimodal Ensemble，以及近期方法：FiLM、BiGated、OGM-GE、AGM、QMF、OPM、MLA、MMPareto 等。

- **实验设置**：所有音频-视觉数据集使用 ResNet-18 从零训练，音频输入为频谱或fbank，视觉为采样帧。优化器 SGD（momentum=0.9, weight decay=1e-4），学习率、batch size、epochs 因数据集而异（详见原文表1下方）。MVSA 使用冻结的 CLIP 编码器（RN50 和 ViT-B/32），仅训练分类头。

### 4. 资源与算力

文中明确说明所有实验均在同一张 **NVIDIA Tesla V100 GPU** 上进行，未提及训练总时长或 GPU 数量。由于从零训练 ResNet-18 并设置 200-400 epoch，推理资源消耗较大，但作者未提供具体耗时。

### 5. 实验数量与充分性

- **充分性**：实验覆盖 6 个多模态分类数据集，包括音频-视觉（5个）和文本-图像（1个）；对比了 10 余种最新方法；在音频-视觉任务上报告了单模态和多模态准确率（表1）、JS散度（表2）、熵分析（表3）、训练曲线（图4）、负采样数量影响（图3）、预训练编码器实验（表4）。此外，附录还扩展了回归任务（CMU-MOSI/MOSEI）的初步结果。
- **公平性**：所有对比方法在相同骨干网络和训练设置下复现，结果取三个随机种子平均；MVSA 上报告了 10 次随机种子及 95% 置信区间（附录表5），较好控制了随机性。实验设计较客观公正。

### 6. 论文的主要结论与发现

- 从信息论角度揭示了模态竞争的根源：联合学习下弱模态的学习上限受强模态影响。
- 提出最大化总相关可兼顾联合学习、单模态学习和模态对齐，且无需额外超参数或结构修改。
- TCMax 在多个数据集上取得了最高的多模态准确率，同时单模态性能不丢（表1）；JS散度最小，说明跨模态预测更一致（表2）。
- 训练过程中损失更高，有效防止过拟合（图4）；熵比率更接近，模态贡献更平衡（表3）。
- 在预训练编码器场景（MVSA）下，TCMax 同样优于联合学习和单模态学习（表4）。

### 7. 优点

- **理论创新**：首次使用总相关作为多模态分类的学习目标，并给出了神经估计器（TCNE）和严格的理论证明。
- **实用简洁**：TCMax 损失无额外超参数，训练时仅替换交叉熵损失，预测时无需任何改动；且支持计算优化（线性融合时开销几乎无增加）。
- **实验全面**：在多种数据规模、多种模态组合（音-视、RGB-光流、文本-图像）上验证，涵盖从零训练和预训练场景，并与主流方法充分对比。
- **分析深入**：通过熵、JS散度、训练曲线等指标深入解释模态平衡和过拟合抑制机制。

### 8. 不足与局限

- **任务覆盖**：主要针对分类任务，未直接扩展到目标检测、生成等任务。附录虽尝试回归，但仅初步验证，缺乏系统性消融。
- **计算开销**：当模态数量多或 batch 大且不使用线性融合时，TCNE 需对预测头进行 O(|B|^M) 次前向传播（如公式14），即使采样仍可能增加负担。
- **模型架构依赖**：方法本身不依赖特定架构，但作者指出其最佳性能可能需要针对该框架专门设计的模型，而非简单套用现有骨干。
- **偏差风险**：实验均基于可控视频数据集（如情感、动作），未涉及噪声场景或模态缺失等实际挑战。
- **可重复性**：代码已开源，但未提供详细超参数搜索过程，部分数据集（如 UCF101）学习率和 epoch 选择理由不明确。

（完）
