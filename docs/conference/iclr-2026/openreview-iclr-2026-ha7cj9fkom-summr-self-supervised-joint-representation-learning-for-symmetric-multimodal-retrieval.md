---
title: "SUMMR: Self-supervised Joint Representation Learning for Symmetric Multimodal Retrieval"
title_zh: SUMMR：面向对称多模态检索的自监督联合表示学习
authors: "Yang Wenjie, Hang Yu, Yuyu Guo, Peng Di"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=ha7Cj9fKOM"
tags: ["query:multimodal"]
score: 7.0
evidence: 自监督联合表示学习用于多模态检索
tldr: 针对多模态检索中查询和上下文不对称的问题，本文提出SUMMR，一种两阶段自监督框架，利用无标签图像-文本对学习共享和独特表示，实现对称检索。该方法通过解耦共享和特有信息，对齐跨模态概念，在多个基准上表现优异。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1307, \"height\": 619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1450, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1457, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1178, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 322, \"height\": 185, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 327, \"height\": 185, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 324, \"height\": 223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 325, \"height\": 223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 159, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 241, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 323, \"height\": 220, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 293, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 261, \"height\": 262, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 324, \"height\": 248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 328, \"height\": 187, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 323, \"height\": 185, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 325, \"height\": 217, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 136, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 293, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 266, \"height\": 263, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1307, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1304, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1298, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1581, \"height\": 2248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1586, \"height\": 2322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 570, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1309, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1276, \"height\": 691, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1253, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1308, \"height\": 221, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ha7cj9fkom/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 643, \"height\": 412, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1459, \"height\": 505, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 670, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1384, \"height\": 1635, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1445, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1296, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1034, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1030, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1048, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1309, \"height\": 147, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 967, \"height\": 146, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1115, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ha7cj9fkom/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1421, \"height\": 125, \"label\": \"Table\"}]"
motivation: 现有多模态检索多为非对称，缺乏对称检索方法且依赖监督数据。
method: 提出两阶段自监督框架，先学习掩码分离共享与独特信息，再对齐共享概念。
result: 在多个多模态检索基准上取得最优结果，证明对称检索的有效性。
conclusion: 自监督对称多模态检索方法能有效利用无标签数据，提升检索性能。
---

## Abstract
Existing works on multimodality-to-multimodality (MM2MM) retrieval mainly focus on asymmetric retrieval, where text-image pairs in query and context serve distinct roles. In this work, we address the critical yet underexplored challenge of symmetric retrieval, where queries and contexts are interchangeable. We propose SUMMR, a novel two-stage self-supervised framework that leverages unlabeled web-scale image-text pairs, contrasting previous methods that heavily rely on costly supervised data. Based on the observation that both semantic alignment and discrepancies exist between the two modalities, we first learn a mask to disentangle shared and unique information within each image-text pair, allowing us to align the shared concepts while preserving modality-specific details. Then, we leverage this mask to automatically generate positive and negative samples for self-supervised contrastive learning of the final joint embedding. Complementing this framework, we introduce a novel benchmark featuring high-quality human-annotated positive and hard-negative pairs to evaluate symmetric MM2MM retrieval. On this benchmark, extensive experiments against ten SOTA methods show SUMMR surpasses the strongest supervised VLM by 3.42 points, with over 50x fewer model parameters and a 5x smaller embedding dimension. Code will be available upon publication.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有多模态检索（MM2MM）主要聚焦于**非对称检索**（如查询用文本+图像，候选用文本+图像但角色不同），而实际应用中大量场景需要**对称检索**——查询和候选在语义上等价且可互换（例如：电商中搜索T恤正面+背面描述，期望找到对应产品的背面+正面描述）。对称MM2MM检索的研究空白严重。同时，现有方法高度依赖昂贵的监督数据标注，这成为发展的瓶颈。
- **背景困境**：手工标注正/难负样本耗时费力，且数据量小；现有监督方法（如UniIR、VLM2Vec、MM-Embed等）需在人工标注数据上训练，泛化性差；而现代AI（CLIP、DINO、LLM等）在大规模无标注数据上训练效果更好。因此，论文旨在通过自监督方式突破数据瓶颈。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用无标注的网页级图像-文本对，通过学习一个“交集掩码”（intersection mask）来分离每一对中的**共享信息**（intersection）和**模态特有信息**（difference）。然后基于此掩码自动生成正样本（掩码共享信息，因为可从另一模态恢复）和负样本（掩码特有信息，导致不可逆信息丢失），用于对比学习。
- **两阶段框架 SUMMR**：
  - **Stage 1：解耦与对齐（Disentangle and Align）**
    - **组件**：视觉编码器 \(E_V\)、语言编码器 \(E_L\)、MLP适配器 \(A_V, A_L\)、视觉-语言编码器 \(E_{VL}\)（3层注意力）。
    - **关键模块**：
      - **全局到局部对齐（GLA）**：通过margin loss促使局部特征与伙伴模态的全局特征之间的相似度高于与负例的相似度，从而区分共享与独有特征。
      - **局部蒸馏（LD）**：使用强预训练单模态编码器（DINOv2、BGE-m3）作为教师，匹配学生局部特征的token间排序（Pearson相关），稳定训练。
      - **掩码生成（MaskGen）**：通过二次判别分析（QDA）自适应阈值 \(\tau\) 区分正/负分布，并采用**进化掩码**（从全1掩码逐渐过渡到硬掩码）保证训练稳定性。
      - **掩码图文对比学习（Masked ITC）**：仅对交集特征进行对比损失，对齐共享概念。
      - **全局蒸馏（GD）**：保留未掩码全局特征的结构，防止遗忘模-态特有信息。
  - **Stage 2：自监督多模态表示学习**
    - 利用Stage 1训练好的模型和阈值，自动构造正样本（掩码交集）和负样本（掩码差集）。对图像使用层次聚类生成语义段，再基于相似度确定段属于交集还是差集。
    - 训练使用对比损失，负样本包括：构造负例、批内负例、离线挖掘的难负例（来自4M LAION+多模型检索）。
  - **推理阶段**：所有掩码生成、分割、QDA均丢弃，模型只需一次前向，效率高。

## 3. 实验设计：数据集、Benchmark、对比方法

- **训练数据**：800,000张LAION-5B的随机子集（无标签）。
- **新Benchmark（sym-MM2MM）**：
  - 由人工辅助构建：利用VLM（GPT-4o）、LLM、SD 3.5生成候选，然后经人工严格审核、重写、替换，最终得到214个三元组（原始样本、正样本、难负样本）。近50%的候选正对被拒。
  - 评价指标：Recall@k（k=1,5,10）在包含1M LAION+benchmark的大池中计算；Precision（仅计算benchmark内正样本相似度高于负样本的比率）；最终平均Avg = (mR + Prec)/2。
- **对比方法**（10种SOTA通用多模态嵌入模型）：
  - 有监督编码器型：CLIP-SF、BGE-VL。
  - 有监督VLM型：MM-Embed、VLM2Vec、GME、Unite、LamRA、UniME、mmE5。
  - 无监督：CLIP-SF-ZS。
- **评估设置**：所有方法在相同池上测试，公平比较。注意：现有监督方法仅在非对称数据集上微调，因此测试其对对称任务的泛化能力。

## 4. 资源与算力

- **明确说明**：论文未给出具体的GPU型号、数量、训练总时长。但有提及：
  - SUMMR-B+D Stage 1每步训练时间0.79秒，Stage 2为0.53秒（batch_size=32）。
  - SUMMR-C Stage 1每步1.29秒，Stage 2为0.30秒。
  - 对比：VLM方法（Qwen2-VL-7B）每步7.12秒，Llama-3.2-11B每步10.83秒。
  - 训练步数：SUMMR-B+D Stage 1 8000步，Stage 2 200步；SUMMR-C Stage 1 2000步。
  - 因此总训练时间相对较短（约数小时至一天内），但未提及使用的GPU数量（推测为单机或多卡）。模型参数微小（0.20B~0.71B vs. 10.12B），算力需求远低于VLM。

## 5. 实验数量与充分性

- **实验数量充足**：
  - 主表（Table 1）：对比10种方法在两个变体（SUMMR-B+D, SUMMR-C）上的Recall、Precision、Avg。
  - Stage 1消融（Table 2）：9种设置（去除各损失、进化掩码、投影头等），并报告Stage 1后和Stage 2后结果。
  - Stage 2消融（Table 3）：7种设置（去除构造负例、替换正例构建策略、去除分割、用SAM等）。
  - 敏感性分析（图11、Table 8）：margin δ和损失权重。
  - 离线硬负例消融（Table 7）：6种设置。
  - CLIP backbone消融（Table 9）：单独Stage 1 vs. Stage 2 vs. 完整。
  - 分割方法比较（Table 10）：与SAM对比。
  - 额外实验：在MBEIR子集、RefCOCO上的辅助验证（App H）。
  - 训练时间比较（Table 13）。
- **充分性与客观性**：
  - 消融实验覆盖了几乎所有关键组件，验证了各部分的必要性。
  - 对比基线全面，包括最新VLM方法，且指标多样（R@1, R@5, R@10, Precision, Avg），避免单一指标偏见。
  - 注：监督基线仅在非对称数据集上训练，因此结果可能反映了任务特异性的差异，但论文明确说明了这点，评价为公平。

## 6. 论文的主要结论与发现

- SUMMR在sym-MM2MM benchmark上以绝对优势超越所有基线：最佳变体SUMMR-C平均87.69，比最强VLM mmE5高3.42点，但参数量仅为其1/50，嵌入维度1/5。
- 自监督范式有效：无需人工标注即可达到甚至超越大规模监督模型。
- Stage 1的解耦能力是关键：通过进化掩码、QDA、多损失协同，模型学会区分共享与特有信息。Stage 2进一步利用该能力进行对比学习，显著提升（+4.3点）。
- 进化掩码、投影头、局部蒸馏、全局蒸馏等设计均必不可少，缺少任何一个都会导致性能下降。
- 构造正负样本的策略（掩码交集/差集）优于随机掩码或普通数据增强。
- 模型对几何变换稳健，对颜色变化敏感，说明学到了有意义的语义属性。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次系统研究对称MM2MM检索，提出自监督两阶段框架，克服数据标注瓶颈。
- **自监督数据生成**：利用模态对的内在结构（交集/差集）自动构造正/负样本，方法巧妙。
- **进化掩码+QDA**：从全1掩码逐步过渡到预测掩码，避免初期噪声；QDA自适应阈值，无需手动设定。
- **轻量高效**：参数量小（0.2B-0.7B），推理速度快（FPS 520-922），远胜VLM方法（FPS 4-19）。
- **全面消融**：从损失项、掩码策略、投影头、分割方法、硬负例挖掘等多个维度论证设计选择，实验设计严谨。
- **高质量Benchmark**：人工审核构建的214个三元组虽然量小但质量高，且提供了多样类别和大规模检索池。

## 8. 不足与局限

- **训练数据规模有限**：仅使用80万LAION对，且来源单一，可能限制泛化；更大规模（>1000万）训练能否提升未知。
- **构造样本类型单一**：主要模拟信息删除，未涉及内容修改或添加；依赖离线硬负例补偿，但并非最优。
- **Benchmark规模小**：仅214个三元组，可能统计不够稳健；且全部由人工标注，成本高，难以扩展。
- **未公开代码与数据**：论文声称代码将在发表后公开，但当前无法复现。
- **仅限图像-文本模态**：未拓展到音频-文本、视频-文本等其他模态；方法中聚类分割依赖于视觉特征，对音频/视频需调整。
- **局限性讨论**：论文在Limitations部分承认构造样本仅模拟删除，离线硬负例是必要补充；未来工作可探索完全自举生成修改/增加的样本。

（完）
