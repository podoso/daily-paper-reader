---
title: "DecAlign: Hierarchical Cross-Modal Alignment for Decoupled Multimodal Representation Learning"
title_zh: DecAlign：用于解耦多模态表示的层次交叉对齐
authors: "Chengxuan Qian, Shuo Xing, Li Li, Yue Zhao, Zhengzhong Tu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=LasUPe2UxG"
tags: ["query:multimodal"]
score: 7.0
evidence: 解耦多模态表示的层次交叉对齐
tldr: 多模态表示面临模态异质性挑战。DecAlign通过层次交叉对齐框架，利用高斯混合建模和多边缘最优传输策略，将表示解耦为模态独有和模态共有特征，有效缓解分布差异。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-lasupe2uxg/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1449, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lasupe2uxg/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1237, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lasupe2uxg/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1447, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lasupe2uxg/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1444, \"height\": 781, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lasupe2uxg/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 381, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1440, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1151, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1437, \"height\": 527, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1316, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1310, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lasupe2uxg/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1311, \"height\": 689, \"label\": \"Table\"}]"
motivation: 多模态数据的异质性使得跨模态协作困难。
method: 提出层次交叉对齐框架，使用原型引导的最优传输对齐策略解耦表示。
result: 在多个多模态任务上提升了表示质量。
conclusion: 解耦表示能更好地处理模态异质性。
---

## Abstract
Multimodal representation learning aims to capture both shared and complementary semantic information across multiple modalities. However, the intrinsic heterogeneity of diverse modalities presents substantial challenges to achieve effective cross-modal collaboration and integration. To address this, we introduce DecAlign, a novel hierarchical cross-modal alignment framework designed to decouple multimodal representations into modality-unique (heterogeneous) and modality-common (homogeneous) features. For handling heterogeneity, we employ a prototype-guided optimal transport alignment strategy leveraging gaussian mixture modeling and multi-marginal transport plans, thus mitigating distribution discrepancies while preserving modality-unique characteristics. To reinforce homogeneity, we ensure semantic consistency across modalities by aligning latent distribution matching with Maximum Mean Discrepancy regularization. Furthermore, we incorporate a multimodal transformer to enhance high-level semantic feature fusion, thereby further reducing cross-modal inconsistencies. Our extensive experiments on four widely used multimodal benchmarks demonstrate that DecAlign consistently outperforms existing state-of-the-art methods across five metrics. These results highlight the efficacy of DecAlign in enhancing superior cross-modal alignment and semantic consistency while preserving modality-unique features, marking a significant advancement in multimodal representation learning scenarios.

---

## 论文详细总结（自动生成）

# DecAlign：解耦多模态表示的层次交叉对齐框架——论文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态表示学习面临**模态异质性**（heterogeneity）带来的根本性挑战——不同模态（如视觉、语言、音频）在数据分布、尺度、语义粒度上存在显著差异，直接融合（如拼接或线性变换）常导致模态独有特征与共有特征的纠缠，引发语义干扰（semantic interference）。
- **研究动机**：现有方法（如MISA、DMD）虽然尝试解耦模态不变/独有特征，但多从全局视角建模，忽略**局部token级**的不一致性，且易导致**过度对齐**而丢失模态独有信息。
- **整体含义**：提出**DecAlign**，一种层次化交叉对齐框架，通过显式解耦模态异质特征（heterogeneous）和同质特征（homogeneous），并分别采用定制化的对齐策略，在保持模态独有特性的同时强化跨模态语义一致性，从而显著提升多模态表示的质量。

## 2. 方法论
- **核心思想**：先解耦后对齐——将多模态特征解耦为模态独有（heterogeneous）和模态共有（homogeneous）两部分，分别进行层次化对齐。
- **关键技术细节**：
  - **模态特征解耦**（多模态特征解耦, MFD）：通过模态独有编码器 \(E^{(m)}_{uni}\) 和共享编码器 \(E_{com}\) 提取异质特征 \(F^{(m)}_{uni}\) 和同质特征 \(F^{(m)}_{com}\)；利用余弦相似度损失 \(L_{dec}\) 最小化两者重叠。
  - **异质性对齐**（Hete alignment）：针对模态独有特征的分布差异，提出**原型引导的多边缘最优传输**（Prototype-guided Multi-marginal Optimal Transport）。
    - 原型生成：对每种模态的独有特征拟合高斯混合模型（GMM），得到K个高斯分量（\(K\)=类别数），每个分量由均值\(\mu\)和协方差\(\Sigma\)表示。
    - 最优传输：构建多边际运输计划，最小化跨模态原型匹配成本（含Wasserstein-2距离和熵正则化），同时结合样本-原型校准项（\(L_{proto}\)），实现全局与局部联合对齐。
  - **同质性对齐**（Homo alignment）：针对模态共有特征，进行**潜在空间语义对齐**和**分布匹配**。
    - 语义对齐：将模态共有特征参数化为高斯分布（含均值、协方差、偏度），最小化模态间统计量差异（\(L_{sem}\)）。
    - 分布匹配：通过概率分布编码器（PDE）将特征映射到再生核希尔伯特空间（RKHS），使用最大均值差异（MMD）度量分布距离（\(L_{MMD}\)）。
  - **多模态融合**：异质特征经过跨模态Transformer（per-modality）增强后，与同质特征拼接，经全连接层进行下游预测。
  - **总损失**：\(L_{total} = L_{task} + L_{dec} + \alpha L_{hete} + \beta L_{homo}\)，\(\alpha,\beta\)为超参数。
- **公式/算法流程文字说明**：整体流程为：输入多模态数据 → 1D卷积对齐时间维度 → 解耦为异质/同质特征 → 异质对齐（GMM原型+多边缘OT+样本校准）→ 同质对齐（语义统计量匹配+MMD分布匹配）→ 跨模态Transformer融合 → 拼接后分类/回归。

## 3. 实验设计
- **数据集**：四个多模态情感分析/情绪识别数据集：
  - CMU-MOSI（英文，2/7类情感强度）
  - CMU-MOSEI（英文，大规模，2/7类）
  - CH-SIMS（中文，3类）
  - IEMOCAP（英文，六类情绪：愤怒、开心、悲伤、中性、兴奋、沮丧）
- **Benchmark**：使用标准划分（train/test），评估指标包括MAE、Corr、Acc-2、Acc-7、F1 Score、Weighted Accuracy (WAcc)、Weighted F1 (WAF1)等。
- **对比方法**：13种SOTA方法：MFM、MulT、PMR、CubeMLP、MUTA-Net、MISA、CENet、Self-MM、FDMER、AOBERT、DMD、ReconBoost、CGGM。均在统一实验环境和数据拆分下复现。

## 4. 资源与算力
- **GPU型号**：NVIDIA A6000（单卡）
- **训练参数**：50 epoch，batch size 32，Adam优化器，学习率5e-5（MOSI/CH-SIMS）或1e-4（MOSEI/IEMOCAP）。
- **说明**：论文未明确报告总训练时长，但基于单卡A6000和50 epoch，推测训练时间在数小时内（具体取决于数据集规模）。模型复杂度适中，但在资源消耗上缺乏详尽数据。

## 5. 实验数量与充分性
- **实验数量**：包含：
  - **主要对比实验**（表1）：在4个数据集上对比13种方法，报告5个指标（部分数据集指标不同）。
  - **消融实验**（表2）：两大组消融——(a) 关键组件（MFD、Hete、Homo）;(b) 具体策略（Proto-OT、CT、Sem、MMD），分别在MOSI和MOSEI上报告MAE和F1。
  - **混淆矩阵分析**（图3）：MOSI上对比MulT、MISA、DMD和DecAlign的混淆矩阵。
  - **模态间隔可视化**（图4(e)-(h)）：t-SNE展示语言-视觉特征距离。
  - **参数敏感性分析**（图5）：\(\alpha,\beta\)的网格搜索热力图。
  - **附录**中还包含更多数据集（CH-SIMS、IEMOCAP）的详细结果和全指标对比。
- **充分性与公平性**：实验较为充分。采用统一实验环境、固定随机种子（5次平均）、标准数据拆分、与原文/官方复现一致的基准方法，确保了公平性。消融实验覆盖了每个关键模块和策略，验证了各组件贡献。参数敏感性分析揭示了超参数影响范围。不足在于未涉及真实世界缺失模态场景、未在更多任务（如推荐、自动驾驶）上验证泛化性。

## 6. 主要结论与发现
- **全面SOTA**：DecAlign在四个数据集上所有指标均显著超越对比方法。例如MOSI上Acc-2达到85.75（+2.5%）、F1 Score 85.82（+2.3%），MOSEI上Acc-2 86.48（+2.3%），CH-SIMS上F1 81.85（+1.7%），IEMOCAP上WAcc 73.35（+1.1%）。
- **层次对齐的必要性**：消融表明，同时去除Hete和Homo导致严重退化；单独去除Hete对MAE影响更大，去除Homo对F1影响更大，两者互补。
- **原型OT和对比训练是关键**：在策略消融中，去除Proto-OT或CT是性能下降最大的两个操作，说明结构对齐和判别性监督不可或缺。
- **模态间隔显著缩小**：可视化显示完整DecAlign能紧密对齐语言-视觉特征簇，而缺少任一模块则存在残余偏移。

## 7. 优点
- **方法创新性**：首次将原型引导的多边缘最优传输应用于多模态异质对齐，同时结合语义统计量匹配和MMD处理同质性，形成层次化解耦-对齐范式。
- **实验设计严谨**：统一环境、多次平均、全面消融、参数敏感度分析，结果可信度高。
- **通用性**：在英文/中文、不同任务（回归/分类）和不同规模数据集上均表现优异，证明方法具有良好泛化性。
- **可重复性**：论文附录提供了详细超参数（表4）、特征提取细节、随机种子等，并承诺开源代码。
- **性能提升显著**：尤其在回归指标MAE和精细分类（Acc-7/Acc-3）上提升幅度较大，反映出对连续值和离散值均有更好建模能力。

## 8. 不足与局限
- **实验覆盖有限**：仅在情感分析/情绪识别任务上验证，未涉及更广泛的多模态任务（如VQA、图文检索、自动驾驶感知等），通用性暂未充分证明。
- **模态缺失场景未探讨**：现实应用中常出现模态缺失（如音频损坏），论文未设计相关实验。
- **计算资源开销**：虽然训练时间可控，但GMM拟合、最优传输计算可能增加单次迭代负担，论文未提供详细的运行时间或复杂度分析。
- **超参数依赖性**：\(\alpha,\beta\)需要网格搜索调节（图5），最优值对不同数据集可能敏感，增加了应用成本。
- **特征提取依赖**：实验采用预训练好的BERT/OpenFace/COVAREP特征，并未端到端联合训练，可能限制了模型端到端优化的潜力。
- **仅回归/分类任务**：未在生成任务或多模态推理上验证，对语义对齐的深层效果尚需进一步验证。

（完）
