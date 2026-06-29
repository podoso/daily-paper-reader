---
title: Polysemic Semantic Instance Network for Cross-Modal Hashing
title_zh: 跨模态哈希的多义语义实例网络
authors: "Shuo Han, Qibing Qin, Kezhen Xie, Wenfeng Zhang, Lei Huang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/42459/46420"
tags: ["query:multimodal"]
score: 7.0
evidence: 跨模态哈希中的多义语义实例嵌入用于多模态检索
tldr: 针对跨模态哈希中语义歧义（多义词、多目标图像等）导致对齐不准确的问题，提出深度多义语义实例哈希方法。该方法通过多样语义实例嵌入模块，结合多头自注意力和残差学习，捕获局部和全局特征，生成多义语义哈希码。实验表明，在跨模态检索任务上显著提升了检索精度，有效处理了语义歧义。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1836, \"height\": 797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1817, \"height\": 828, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 862, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 731, \"height\": 251, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42459/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 736, \"height\": 435, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42459/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1597, \"height\": 810, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42459/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 878, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42459/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 889, \"height\": 368, \"label\": \"Table\"}]"
motivation: 跨模态哈希中语义歧义（多义词、多目标）导致检索精度下降。
method: 设计多样语义实例嵌入模块，融合多头注意力和残差学习生成多义语义哈希码。
result: 在跨模态检索基准上取得更优的检索精度。
conclusion: 多义语义建模有效缓解了跨模态检索中的语义歧义问题。
---

## Abstract
Hashing techniques are widely adopted in large-scale cross-modal retrieval due to their efficiency and low storage cost. However, semantic ambiguities, including polysemy, multi-object images, and missing semantic descriptions, significantly degrade the accuracy of alignment and retrieval performance. Most existing methods rely on one-to-one mappings that preserve only global average semantics, which fail to capture the intrinsic polysemous structures embedded within individual samples. To address this issue, we propose a novel Deep Polysemic Semantic Instance Hashing (DPSIH) method and design a Diverse Semantic Instance Embedding (DSIE) module. This module integrates local and global features through multi-head self-attention and residual learning, generating multiple diverse embeddings per sample to effectively capture fine-grained and polysemous semantic structures. Furthermore, we design a multi-embedding semantic correlation constraint that relaxes strict alignment restrictions to improve robustness under partial alignment, and introduce Maximum Mean Discrepancy (MMD) regularization to alleviate cross-modal distribution shifts. Additionally, an embedding diversity mechanism is proposed to prevent all embeddings from collapsing into a central or averaged representation, thereby enhancing semantic diversity. Extensive experiments on four benchmark datasets demonstrate that DPSIH significantly outperforms state-of-the-art methods and effectively improves the modeling of semantic ambiguity in cross-modal retrieval tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：跨模态哈希检索中，样本常存在语义歧义，包括图片中的多义词语、多目标场景、文本描述缺失或不完整，导致传统的“一对一”嵌入（每个样本仅映射为一个全局平均向量）无法捕捉细粒度、多义的语义结构，严重影响对齐精度和检索性能。
- **背景**：现有方法大多基于一对一映射，仅保留全局平均语义，忽略样本内在的多义结构。例如，一张图片包含“人、马、天空、山、田野”等多个语义，但对应文本只描述“人、马、田野”，单一嵌入会压缩信息，无法处理部分对齐情况。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：提出深度多义语义实例哈希（DPSIH），为每个样本生成**多个多样化嵌入**，每个嵌入捕获一个语义分量，从而实现细粒度跨模态对齐。
- **关键技术**：
  - **多样语义实例嵌入模块（DSIE）**：使用CLIP Transformer提取图像（50个token）和文本（33个token）特征，分离全局特征（class token/max pooling）和局部特征（patch tokens/end-of-text）。通过多头自注意力生成η个注意力图，重新组合局部特征得到η个表示；再通过残差学习（全局+局部）融合，经全连接层和tanh输出η个二值化嵌入。
  - **多嵌入语义相关性约束**：对正样本对，假设至少有一对嵌入匹配；对负样本对，所有嵌入对都不匹配。使用最小余弦距离的合页损失，允许模型自动选择最佳对齐的嵌入对，增强部分对齐鲁棒性。
  - **分布一致性策略（MMD）**：引入最大均值差异（MMD）正则化，减少两个模态整体嵌入分布之间的差异。
  - **嵌入多样性机制**：对局部特征计算Gram矩阵，惩罚非对角元素（除单位矩阵外），迫使不同局部特征正交，避免嵌入坍塌为单一中心表示。
- **目标函数**：\( \mathcal{L} = \mathcal{L}_{msc} + \alpha_1 \mathcal{L}_{dc} + \alpha_2 \mathcal{L}_{ed} \)，其中α1和α2均为0.01。

### 3. 实验设计：数据集、基准、对比方法
- **数据集**：四个公开数据集：MIRFLICKR-25K（24,581对，24类）、NUS-WIDE（195,834对，21类）、MS COCO（80概念，训练+验证）、IAPR TC-12（20,000样本，291类）。标准划分：10,000训练、5,000查询、其余检索库。
- **对比方法**：8种代表性深度跨模态哈希方法：DCMH、SSAH、DCHMT、MIAN、DNPH、DHaPH、BiLGSEH、DDBH。
- **评估指标**：平均精度均值（mAP）和海明半径2下的精度（P@H≤2），任务包括图像检索文本（I2T）和文本检索图像（T2I）。

### 4. 资源与算力
- 文中仅提及“基于PyTorch框架，在NVIDIA RTX 4090 GPU上训练”。**未明确说明使用的GPU数量、训练总时长或具体算力需求**。因此，无法量化资源开销。

### 5. 实验数量与充分性
- **实验数量**：共进行以下多组实验：
  - 主表（Tab.1）：4个数据集 × 3种哈希长度（32/64/128 bits）× 2种任务，报告mAP。
  - P@H≤2柱状图（Fig.3）：同上设置。
  - 参数分析（Fig.4）：η从1到10，α1和α2在0.001~0.1范围内变化。
  - 消融实验（Tab.2）：4种变体（去除DSIE、用三元组替换Lmsc、去除Ldc、去除Led）在2个数据集上3种编码长度。
  - 鲁棒性实验（Tab.3）：在20%/50%/80%标签噪声下，对比5种方法3种编码长度。
  - 效率分析（Fig.5）：训练和编码时间比较。
  - 可视化（Fig.6-7）：词语分布、注意力图。
- **充分性与公平性**：实验覆盖多种数据集、编码长度、消融、噪声场景，对比方法均为近年代表性工作，采用官方代码和推荐参数。**较为充分且公平**。但未提供多次重复实验的统计方差（如置信区间），也未进行显著性检验。

### 6. 论文的主要结论与发现
- DPSIH在所有四个数据集、所有编码长度下均显著优于对比方法（如MIRFLICKR-25K 32bits I2T mAP达0.8703，比最佳基线DDBH高约1.7%）。
- 多嵌入策略（η=4最佳）能有效缓解语义歧义，尤其在标签噪声场景下表现突出（80%噪声时仍保持0.8455平均mAP）。
- 消融实验证实每个组件（DSIE、多嵌入约束、MMD、多样性机制）均贡献显著；去除任一组件均导致性能下降。

### 7. 优点
- **创新性**：首次在跨模态哈希中系统性地使用多嵌入建模多义语义，并通过残差融合和多样性约束避免坍塌，设计巧妙。
- **鲁棒性**：通过放宽对齐约束（最小配对）和MMD正则化，有效处理部分对齐和分布偏移；标签噪声实验证明了强鲁棒性。
- **实验全面**：主表、消融、参数敏感性、鲁棒性、效率、可视化都做齐，对比方法覆盖主流baselines，结果可信度高。
- **代码开源**：提供GitHub仓库，便于复现。

### 8. 不足与局限
- **资源细节缺失**：未报告训练总时间、GPU数量或显存需求，不利于评估部署成本。
- **统计严谨性不足**：未报告多次运行的标准差或进行显著性检验，难以判断方法间差异是否偶然。
- **应用限制**：仅考虑图像-文本两种模态，未扩展到视频、音频等；未来工作提到零样本/少样本场景，但当前未验证。
- **超参数依赖性**：虽然做了敏感性分析，但α1、α2、η的默认值可能在其他数据集上需要重新调整，文中未讨论调参策略。
- **多样性机制仅作用于局部特征**：作者明确指出对全局嵌入直接加正交约束会失效，但该设计是否最优？可进一步讨论。

（完）
