---
title: Multi-modal Data Mixtures for Vision-Language Model Training
title_zh: 视觉-语言模型训练的多模态数据混合
authors: "Wanyun Xie, Francesco Tonin, Volkan Cevher"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=vk16mWMGXz"
tags: ["query:multimodal"]
score: 7.0
evidence: 自动确定视觉-语言模型训练数据混合比例
tldr: VLM训练依赖昂贵的手动数据混合调整。MMix提出基于模态感知对齐最大化的自动混合框架，通过模态间耦合变量推导对齐分数，能处理缺失模态域，并在0.5B和7B模型上提升精度，匹配专家调优性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-vk16mwmgxz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1450, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vk16mwmgxz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1403, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vk16mwmgxz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1418, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vk16mwmgxz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1419, \"height\": 649, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1465, \"height\": 709, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1466, \"height\": 708, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 553, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1466, \"height\": 867, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 552, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1386, \"height\": 597, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1466, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1390, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1444, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1286, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 753, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1361, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1459, \"height\": 672, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1460, \"height\": 671, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1030, \"height\": 673, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vk16mwmgxz/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 971, \"height\": 555, \"label\": \"Table\"}]"
motivation: 当前VLM训练依赖手动调优数据混合，成本高且不系统。
method: 提出MMix框架，将数据混合建模为模态感知对齐最大化问题，从对偶解导出对齐分数。
result: 在0.5B和7B VLM上提升多个基准精度，匹配专家调优。
conclusion: 自动数据混合方法高效且可扩展。
---

## Abstract
Vision-Language models (VLMs) are typically trained on a diverse set of multi-modal domains, yet current practices rely on costly manual tuning. This paper introduces MMix, a principled framework for automatically determining multi-modal data mixtures for VLM training. We formulate this task as a modality-aware alignment maximization over domains, deriving multi-modal alignment scores from the dual solution through inter-modal coupling variables. Our method is crucially designed to handle domains with missing modalities, allowing for the systematic integration of language-only domains. In experiments on both 0.5B and 7B VLMs, MMix boosts accuracies on diverse evaluation benchmarks with marginal computational cost. Remarkably, it matches the expert-tuned performance 1.28$\times$ faster in image-text tuning and extends to more complex multi-modal video scenarios outperforming uniform weights performance with only 33\% steps.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

视觉-语言模型（VLM）的训练数据通常来自多个多模态领域（如文档、数学、OCR、通用、语言等），当前主流实践依赖昂贵的手动调优或启发式规则来确定各领域的采样比例（如LLaVA-OneVision、Flamingo等）。这种人工策略成本高、不可扩展且可能次优。虽然大语言模型（LLM）中已有自动数据混合方法，但直接移植到VLM面临两大挑战：多模态特征异构性（图像、文本等）以及域中缺失模态的问题（如纯文本域没有图像数据）。因此，亟需一种专门针对VLM的、模态感知的自动数据混合框架。

## 2. 论文提出的方法论：核心思想、关键技术细节

**核心思想**：将数据混合问题建模为**模态感知的对齐最大化**问题。通过耦合多模态的潜在变量，从对偶解中导出每个域的对齐分数，分数越高表示该域与共享的鲁棒语义方向越一致，从而作为重采样权重的基础。

**关键技术细节**：
- 从预先训练的VLM中间层提取每个域的语义嵌入（对每个域内样本求平均），得到各模态的域嵌入 $\mathbf{x}_i^{[v]}$。
- 单模态情况下，引入岭回归形式的对齐最大化物：$\min_{\mathbf{w},\mathbf{e}} \frac{1}{2\lambda}\sum_i e_i^2 + \frac{1}{2}\|\mathbf{w}\|^2$，约束 $e_i = 1 - \mathbf{w}^\top \mathbf{x}_i$。
- 通过Fenchel-Young不等式引入潜在变量 $\alpha_i'$，得到下界 $J_{SM}$。
- 跨模态扩展：令每个模态共享相同的潜在变量 $\alpha$，构造联合目标 $\tilde{J}_{MM} = \sum_v J_{SM}^{(v)}(\mathbf{w}^{[v]}, \alpha)$，实现模态间的耦合。
- 处理缺失模态：对于缺失模态的域，将其嵌入设为 $\mathbf{0}_d$，并将对应的目标设为0。
- 求解后得到最优潜在变量 $\alpha = (K_{MM} + \lambda I)^{-1}\delta$，其中 $K_{MM} = \sum_v K^{[v]}$，$K^{[v]}_{ij}=(\mathbf{x}_i^{[v]})^\top \mathbf{x}_j^{[v]}$，$\delta_i = \sum_v \delta_i^{[v]}$（模态存在指示）。
- 每个模态的对齐分数 $S_i^{[v]} = [K^{[v]}(K_{MM}+\lambda I)^{-1}\delta]_i$。
- 最终的域权重 $p_i = \text{softmax}(\sum_v S_i^{[v]})$。

**数值流程**（算法总结）：
1. 提取各域各模态的嵌入（若有缺失则置零）。
2. 构造各模态核矩阵并求和得到 $K_{MM}$。
3. 计算 $S_i^{[v]}$，加和后用softmax得到概率分布。
4. 按该分布重采样训练数据，进行VLM微调。

## 3. 实验设计：数据集、基准、对比方法

**数据集与模型**：基于LLaVA-OneVision的公开域结构数据，包括5个域（General、Doc/Chart/Screen、Math/Reasoning、General OCR、Language，其中Language为纯文本域）进行图像-文本指令微调；随后增加VideoQA域扩展为6个域3种模态（图像、文本、视频）训练。

**评估基准**：包含三类共10~12个基准：
- 图表/文档理解：AI2D, DocVQA, InfoVQA, OCRBench
- 感知与多学科推理：MMBench, MMStar, MMMU, MathVerse, ScienceQA
- 真实世界理解：RealworldQA；视频任务：Video-MMMU, MVBench

**对比方法**：
- UNIFORM（均匀权重）
- HUMAN（LLaVA-OneVision作者手动调优权重）
- AVG（单模态权重的平均）
- FUSED（VLM处理统一序列后取嵌入的融合权重）
- TEXT、IMAGE、VIDEO（仅用单模态嵌入求解）
- IMAGE†（修正语言域权重为HUMAN值）
- 正交分数（反对齐，用于消融）
- MMix（本文方法）

## 4. 资源与算力

- 嵌入提取：约0.58 H100 GPU小时（35分钟）
- 分数计算：约0.01小时（秒级）
- 总开销：0.59 H100小时
- 完整训练：0.5B模型90小时，7B模型620小时（使用H100 GPU，未说明具体GPU数量）
- 相比于训练总时长，MMix的额外开销几乎可以忽略。

## 5. 实验数量与充分性

共进行了以下多组实验：
- **主实验**：0.5B和7B两个规模，在图像-文本场景（5域）和视频-图像-文本场景（6域）下训练并评估12个基准。
- **消融实验**：
  - 正则化参数λ（1,10,100）影响小
  - 嵌入提取样本量（256,512,1024）稳定
  - 嵌入聚合方式（等权平均 vs 按数据集大小加权）结果相似
  - 模型规模（0.5B与7B）权重可迁移且稳定
  - 预训练模型训练步数（额外500/1000步）权重未变
  - 域数量（4域）验证鲁棒性
  - 正交分数对比，证实对齐分数更优
- **跨架构迁移**：将权重从LLaVA-0.5B迁移到Qwen2-VL-2B，表现同样优于基线。
- **训练效率**：绘制学习曲线，MMix仅用56%步数超越UNIFORM，78%步数超越HUMAN，视频场景下仅用33%步数即达标。

总体而言，实验设计充分覆盖了不同模型规模、不同模态组合、不同训练阶段和不同架构，消融实验齐全，对比基线客观，结论可信。

## 6. 论文的主要结论与发现

- MMix能**自动**生成优于均匀权重和手动调优权重的域权重，在0.5B模型上平均准确率提升1.24%，7B模型提升0.73%。
- 使用MMix训练速度更快：图像场景下**1.28×**快于手动调优，视频场景下**3×**快于均匀权重（仅需33%步数）。
- 方法**处理缺失模态**的能力有效（如纯语言域），且优于简单早期融合（FUSED）和单模态平均（AVG）。
- 域权重可**跨模型规模迁移**（0.5B→7B），跨架构（Qwen2-VL）同样有效。
- 下权重的域（如Math、OCR）并未导致对应能力下降，说明存在正向跨域迁移。

## 7. 优点

- **自动化**：无需人工调参或网格搜索，直接输出最优混合比例。
- **计算效率极高**：仅需一次快速推理和小矩阵求逆，总开销小于1 GPU小时。
- **模态感知**：通过共享潜在变量明确建模模态间的耦合与缺失模态，优于单模态或简单融合方法。
- **非侵入性**：不改变VLM训练算法，仅需调整采样权重，易于集成到现有流程。
- **实证验证充分**：在多种规模、多种模态组合、多种架构上验证了有效性和鲁棒性。

## 8. 不足与局限

- **依赖预定义的域结构**：方法要求数据已按技能或主题分好域，无法处理未分域的非结构化数据。
- **嵌入提取依赖预训练模型**：需要已训练好的VLM中间层表示，若模型尚未训练，则无法直接应用。
- **未考虑域内数据质量**：仅调整域间权重，假设域内数据纯净；数据噪声或域内不平衡可能影响性能。
- **跨任务泛化性待验证**：仅在LLaVA-OneVision和Qwen2-VL两类架构上测试，在更广泛VLM族中的表现未知。
- **多阶段训练中权重稳定性**：论文仅验证了微调阶段的权重，未讨论预训练不同阶段的动态混合需求。
- **理论分析深度有限**：虽给出对偶推导，但缺乏对收敛性和泛化误差的严格理论保证。

（完）
