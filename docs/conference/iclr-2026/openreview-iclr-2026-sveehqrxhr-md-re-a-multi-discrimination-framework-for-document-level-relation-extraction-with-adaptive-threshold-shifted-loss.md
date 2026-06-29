---
title: "MD-RE: A Multi-Discrimination Framework for Document-Level Relation Extraction with Adaptive Threshold Shifted Loss"
title_zh: "MD-RE: 具有自适应阈值偏移损失的多判别文档级关系抽取框架"
authors: "Huangming Xu, Fu Zhang, Lu Zhang, Zhixuan Yang, Jingwei Cheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=SveEhQrxhR"
tags: ["query:joint-mer"]
score: 9.0
evidence: 文档级关系抽取方法
tldr: 文档级关系抽取面临噪声和类别不平衡问题。本文提出MD-RE，采用多判别框架和自适应阈值偏移损失，有效缓解了噪声引入和阈值过高导致的无关系预测。在DocRE基准上，该方法显著提升了关系抽取的F1值，尤其对稀有关系更加鲁棒。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-sveehqrxhr/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 752, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sveehqrxhr/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1153, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sveehqrxhr/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1101, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sveehqrxhr/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1420, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sveehqrxhr/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1104, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sveehqrxhr/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1398, \"height\": 494, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1226, \"height\": 758, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 623, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 713, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1432, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 693, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 719, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 715, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 700, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 711, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 697, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1011, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 862, \"height\": 621, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1287, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 726, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 656, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 719, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 712, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1459, \"height\": 781, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1436, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sveehqrxhr/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1447, \"height\": 962, \"label\": \"Table\"}]"
motivation: 文档级关系抽取中全文档编码引入噪声，证据提取依赖质量，类别不平衡导致高阈值。
method: 提出多判别框架，使用自适应阈值偏移损失同时处理噪声和类别不平衡。
result: 在DocRE基准上取得显著性能提升，特别是对稀有关系。
conclusion: 自适应阈值和多判别机制能有效提升文档级关系抽取精度。
---

## Abstract
Document-level relation extraction (DocRE) aims to identify relations for an entity pair within a document. Existing methods can be broadly classified into two categories: direct encoding of the entire document or enhancement using extracted evidence sentences. However, the former often introduces noise unrelated to relations, while the latter is heavily dependent on the quality of evidence extraction. Moreover, these DocRE models typically use an adaptive threshold to predict all potential relations for an entity pair. As a result, class imbalance in DocRE often leads the model to learn a high throshold for an entity pair, which in turn causes the model to frequently predict that the entity pair has no relation. To address these issues, we propose a **M**ulti-**D**iscrimination framework (**MD-RE**) that does not rely on evidence sentences. MD-RE employs three discriminators with dynamically adjusted thresholds to independently predict relations, and aggregates their outputs via a weighted fusion strategy. Furthermore, we propose an **A**daptive **T**hreshold **S**hifted **L**oss (**ATSL**), which encourages lower threshold to alleviate the high false negative rate resulting from class imbalance. Experiments on three datasets demonstrate that our MD-RE framework with ATSL achieves new state-of-the-art results. Moreover, ATSL significantly improves the performance of various existing DocRE models. In addition, combining other losses with MD-RE also yields competitive results. Our code is available at https://anonymous.4open.science/r/MD-RE.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：文档级关系抽取（DocRE）旨在从文档中识别实体对之间的关系。现有方法主要分为两类：直接编码整个文档，或利用提取的证据句子增强。前者容易引入与关系无关的噪声，后者高度依赖证据抽取的质量。此外，DocRE 中普遍存在的类别不平衡（负样本远多于正样本）导致模型为实体对学得较高的阈值，从而频繁预测“无关系”，增大了假阴性率。
- **整体含义**：针对噪声和类别不平衡问题，本文提出不依赖证据句的多判别框架 MD-RE 和自适应阈值偏移损失 ATSL，以提升 DocRE 的性能和鲁棒性。

### 2. 论文提出的方法论
- **核心思想**：通过多个具有不同判别标准（不同召回率/阈值）的判别器，从多角度筛选候选关系，并通过加权融合整合各判别器输出，在不引入证据句的情况下减少噪声。同时，设计 ATSL 损失，引入阈值偏置以降低阈值，缓解类别不平衡导致的假阴性。
- **关键技术细节**：
  - **文档编码模块**：使用 Transformer（BERT/RoBERTa）获取 token 隐藏状态和注意力，通过局部上下文池化（localized context pooling）获取实体对的上下文表示，再经双线性分类器得到关系 logits。
  - **多判别框架（MD-RE）**：
    - **Recall 判别器**：采用较低阈值（高 λ），追求高召回，保留更多候选关系。
    - **Coarse 判别器**：采用中等阈值，在 Recall 输出基础上进一步粗粒度筛选。
    - **Fine 判别器**：采用较高阈值，进行精细筛选，提高精确率。
  - **Loss-aware Negative Selection（LNS）**：在每个 batch 中保留所有正样本，选取 loss 最高的 top-k 负样本（k = ρ · |Spos|），减少易分负样本的影响，使后续判别器关注更难的样本，并与 ATSL 协同调整阈值。
  - **自适应阈值偏移损失（ATSL）**：
    - 在原始自适应阈值损失（ATL）的 L1 和 L2 部分分别加入偏置 β 和 λ（β=0 时简化），使得正类 logit 与阈值 logit 的边界缩小，阈值相对降低，从而提升召回，降低假阴性。
    - 公式：L'1 = -Σ_{r∈PT} log(exp(logit_r) / (exp(logit_TH+β) + Σ_{r'∈PT} exp(logit_{r'}))); L'2 = -log(exp(logit_TH+λ) / (exp(logit_TH+λ) + Σ_{r'∈NT} exp(logit_{r'}))); LATSL = L'1 + L'2。
    - 理论分析表明 ATSL 是凸损失，并能实现贝叶斯一致性。
  - **加权融合策略**：在推理时，若 Recall 判别器预测 NA 则直接接受；否则若三个均预测存在则直接接受；否则计算融合 logit（三个判别器 logit 之和）和融合阈值（α·logit_TH_recall + logit_TH_coarse + logit_TH_fine），当融合 logit > 融合阈值时判断关系存在。

### 3. 实验设计
- **数据集**：DocRED（含不完整标注）、Re-DocRED（DocRED 修订版）、DWIE。
- **基准（Benchmark）**：使用标准 F1 和 Ign-F1（排除训练集与开发/测试集共享的已知事实）。
- **对比方法**：ATLOP、DocuNet、KD-DocRE、DREEAM、CAST、ABRE、VaeDiff-DocRE、TTM-RE、AA、P3M、SSR-PU 等。部分实验还比较了不同损失函数（ATL、Balanced-Softmax、AML、AFL、HingeABL、CMM 等）。
- **消融实验**：移除 ATSL、LNS、不同融合策略、移除各个判别器等。
- **资源效率**：对比了内存占用和训练时间（表9）。
- **其他分析**：类别不平衡分析（FN/FP/AUC）、长文档性能、判别器数量影响、超参数 λ 和 α 的影响。

### 4. 资源与算力
- 论文在资源效率部分（表9）给出了使用 BERT base 编码器、batch size=4 时，MD-RE 在 Re-DocRED 上的内存占用为 **17.63 GiB**，训练时长为 **81.80 分钟**。
- **未明确说明 GPU 型号和数量**，仅报告了内存和训练时间，但未提及具体硬件（如 Tesla V100 或 A100）及使用的 GPU 数量。

### 5. 实验数量与充分性
- **实验数量丰富**：在三个数据集（DocRED、Re-DocRED、DWIE）上进行了主实验；在 Re-DocRED 上进行了详细的消融实验（至少 8 组消融配置）；对比了 5 种以上不同损失函数；测试了 ATSL 在 5 种不同基线模型上的提升效果；进行了长文档分析、判别器数量影响、超参数扫描（λ 和 α）等。
- **充分性与客观性**：实验设计覆盖了常见的 DocRE 基线、不同损失函数、不同大小的编码器（BERT base / RoBERTa large），并报告了多次运行的平均值和标准差（如 MD-RE 结果报告 ±0.xx），确保了结果的可靠性。消融实验逐一验证了各组件的贡献，分析全面。不过，缺少在其他领域（如生物医学）数据集的验证，通用性需进一步验证。

### 6. 论文的主要结论与发现
- MD-RE 框架结合 ATSL 损失在三个数据集上均达到新 SOTA。例如，Re-DocRED 上 BERT base 达到 77.80 F1，RoBERTa large 达到 81.49 F1。
- ATSL 损失具有通用性：将其应用于多种现有 DocRE 模型（ATLOP、DocuNet、KD-DocRE、DREEAM、TTM-RE）平均提升 +2.52 F1（BERT base 测试集）。
- ATSL 有效缓解了类别不平衡：大幅降低假阴性（FN）和 FN/(FN+FP) 比值，并提升 AUC（平均 +4.53）。
- MD-RE 框架本身有效，即使只用 ATL 损失，也比基线 ATLOP 提升 +3.04 F1。
- 加权融合策略优于管道融合、加法融合等简单策略。
- 三个判别器互补，其中 Recall 判别器贡献高召回，Fine 判别器贡献高精度，Coarse 判别器起到平衡作用。

### 7. 优点
- **方法创新**：提出多判别框架，从不同视角（不同阈值）筛选关系，无需依赖证据句，自然减少文档噪声；ATSL 损失简洁有效，通过阈值偏置直接缓解类别不平衡，且理论性质良好（凸性、贝叶斯一致性）。
- **通用性与互补性**：MD-RE 和 ATSL 独立且互补，可分别用于不同模型或框架，实验证明两者结合效果最佳。
- **实验充分**：在三个数据集上进行，对比众多 SOTA，消融实验全面，资源效率分析详尽，从多个角度（F1、FN/FP、AUC、长文档、判别器数量）验证了方法的有效性。
- **公平性**：报告了多次运行的平均值和标准差，并采用公开数据集和标准指标。

### 8. 不足与局限
- **长尾关系性能仍待提升**：实验显示在低频关系（如 replaced by、replaces）上 F1 较低（22.22%、12.50%），虽然 MD-RE 提高了长尾关系 F1，但绝对值仍然不高。
- **计算开销**：相比单一判别器（如 ATLOP），MD-RE 使用三个编码器副本，内存和训练时间增加（17.63 GiB vs 10.37 GiB，81.8 min vs 55.8 min），资源消耗较高。
- **超参数依赖**：ATSL 需要调节 λ（每个判别器不同）、融合权重 α，且最优值在不同数据集和模型下有差异，调参成本较高。
- **假阳性增加**：虽然 ATSL 大幅降低假阴性，但在高频率关系上假阳性有所增加（表19），导致精确率可能下降。
- **领域泛化**：仅在新闻/百科类数据集（Wikipedia-based DocRED、DWIE）上验证，未在生物医学、金融等专业领域评估，方法的领域适应性尚不明确。
- **未说明 GPU 细节**：未能提供所用 GPU 型号、数量、分布式训练等信息，影响可重复性评估。

（完）
