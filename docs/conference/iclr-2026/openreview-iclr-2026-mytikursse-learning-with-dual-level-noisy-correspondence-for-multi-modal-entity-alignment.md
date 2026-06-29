---
title: Learning with Dual-level Noisy Correspondence for Multi-modal Entity Alignment
title_zh: 双级噪声对应下的多模态实体对齐学习
authors: "Haobin Li, Yijie Lin, Peng Hu, Mouxing Yang, Xi Peng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=mytIKuRsSE"
tags: ["query:multimodal"]
score: 6.0
evidence: 带噪声对应的多模态实体对齐
tldr: 多模态实体对齐中，现有方法假设对应关系完美，但实际存在实体-属性和图间双重噪声。本文揭示并解决该问题，提出RULE框架，通过鲁棒学习处理双重噪声。在多个MMEA基准上，RULE显著优于现有方法，展示了考虑噪声对应的重要性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1401, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1376, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1446, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 458, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1399, \"height\": 181, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1154, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1061, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 496, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 526, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1444, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 875, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1001, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1420, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1134, \"height\": 952, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1137, \"height\": 992, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1143, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1141, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-mytikursse/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1136, \"height\": 838, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1445, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1442, \"height\": 696, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 815, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1372, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1446, \"height\": 698, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1444, \"height\": 696, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 941, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1440, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 870, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1443, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 582, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1012, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1084, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1083, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 439, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1156, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 727, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-mytikursse/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 727, \"height\": 519, \"label\": \"Table\"}]"
motivation: 多模态实体对齐中实体-属性和图间对应存在双重噪声，现有方法忽略此问题。
method: 提出RULE框架，鲁棒处理双重噪声对应。
result: 在MMEA基准上取得最优结果。
conclusion: 建模噪声对应能有效提升多模态实体对齐的鲁棒性。
---

## Abstract
Multi-modal entity alignment (MMEA) aims to identify equivalent entities across heterogeneous multi-modal knowledge graphs (MMKGs), where each entity is described by attributes from various modalities. Existing methods typically assume that both intra-entity and inter-graph correspondences are faultless, which is often violated in real-world MMKGs due to the reliance on expert annotations. In this paper, we reveal and study a highly practical yet under-explored problem in MMEA, termed Dual-level Noisy Correspondence (DNC).
DNC refers to misalignments in both intra-entity (entity-attribute) and inter-graph (entity-entity and attribute-attribute) correspondences. To address the DNC problem, we propose a robust MMEA framework termed RULE. RULE first estimates the reliability of both intra-entity and inter-graph correspondences via a dedicated two-fold principle. Leveraging the estimated reliabilities, RULE mitigates the negative impact of intra-entity noise during attribute fusion and prevents overfitting to noisy inter-graph correspondences during inter-graph discrepancy elimination. Beyond the training-time designs, RULE further incorporates a correspondence reasoning module that uncovers the underlying attribute-attribute connection across graphs, guaranteeing more accurate equivalent entity identification. Extensive experiments on five benchmarks verify the effectiveness of our method against DNC compared with seven state-of-the-art methods. Code is available at https://github.com/XLearning-SCU/2026-ICLR-RULE.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：多模态实体对齐（MMEA）旨在对齐不同多模态知识图谱（MMKG）中的等价实体，现有方法通常假设实体-属性（intra-entity）和图间（inter-graph：entity-entity、attribute-attribute）对应关系完全准确。然而，实际构建的MMKG常因依赖专家标注而引入错误，导致双重噪声对应（Dual-level Noisy Correspondence，简称DNC）问题。
- **定义**：DNC包含两类噪声：
  - **实体-属性噪声**：实体与错误属性关联（如人物图像配错实体）；
  - **图间噪声**：实体对或属性对错误匹配（如电影实体与同名真实人物关联）。
- **影响**：DNC会破坏属内融合和图间对齐，使现有MMEA方法性能显著下降。
- **论文贡献**：首次揭示并系统研究MMEA中的DNC问题，提出鲁棒学习框架RULE，在训练和测试阶段同时应对双重噪声。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **整体框架（RULE）**：包含三个核心模块：
  1. **可靠性估计与对划分**：基于**不确定性**（通过Dempster-Shafer理论和Dirichlet分布量化）和**共识**（基于相似度与标注一致性）两重原则，计算每个图间对（entity-entity）的可靠性得分 \( w_i = (1-u_i)\gamma + c_i(1-\gamma) \)。根据可靠性和阈值，将图间对划分为三组：
     - \( S_C \)：干净对（低不确定度+高共识）
     - \( S_I \)：低共识对（低不确定度+低共识）
     - \( S_U \)：高不确定对（噪声）
  2. **鲁棒图间差异消除**：采用**证据深度学习方法**，对不同组采用不同策略：
     - 对 \( S_U \) 完全忽略；
     - 对 \( S_I \) 使用软标签（结合共识权重和softmax输出）；
     - 对 \( S_C \) 使用原始标签。
     - 损失函数由“双重鲁棒损失” \( L_{DR} \)（基于Dirichlet分布的MSE或CE）和KL正则项 \( L_{Reg} \) 组成，避免过拟合噪声对。
  3. **鲁棒属内融合**：将估计的可靠性作为权重，对各模态特征加权拼接，抑制不可靠属性。
  4. **测试时对应推理（TTR）**：利用多模态大语言模型（MLLM，如Qwen2.5-VL）结合Chain-of-Thought（CoT）进行逐步推理，挖掘属性对间的潜在语义关联，生成修正的相似度分数 \( \hat{s}_i \)，并与原始相似度联合用于最终匹配。

- **关键公式**：
  - 可靠性：\( w_i = (1-u_i)\gamma + c_i(1-\gamma) \)
  - 不确定性：\( u_i = \tilde{N} / Q_i \)，其中 \( Q_i = \sum_j (e_{ij}+1) \)，\( e_{ij} = \exp(\tanh(s_{ij}/\tau)) \)
  - 共识：\( c_i = \max(0, s_i \cdot y_i) \)
  - 双鲁棒损失（MSE形式）：\( L_{DR} = \mathbb{I}(i \notin S_U) \int \|\hat{y}_i - p_i\|^2 D(p_i|\alpha_i) dp_i \)

### 3. 实验设计

- **数据集**：五个主流MMEA基准：
  - ICEWS-WIKI、ICEWS-YAGO、DBP15K ZH-EN、DBP15K JA-EN、DBP15K FR-EN。
- **评估协议**：
  - **Non-name**：排除名称属性；**All-attributes**：使用所有模态（名称、结构、图像、文本等）。
  - **噪声设置**：人工注入0%、20%、50%的双重噪声（同时污染E-E、E-A、A-A对）。
- **对比方法**：7种SOTA方法：EVA、MCLEA、XGEA、MEAformer、UMAEA、PMF、HHEA。
- **评价指标**：Hit@1、Hit@5、MRR。
- **公平性**：所有方法使用相同的特征提取骨干（CLIP ViT-L/14），部分实验还额外使用SigLIP、BLIP验证迁移性。

### 4. 资源与算力

- **GPU**：实验使用NVIDIA RTX 3090（24GB显存），多卡并行。
- **MLLM推理**：测试时TTR模块使用不同规模模型，较大模型（如Qwen2.5-VL 72B）需8张GPU、每张约20GB显存；轻量版（3B/7B）可在单卡运行。训练阶段未明确报告总时长，但附录G.8给出了时间成本（Non-name设置下不加TTR约103秒，加72B模型约10043秒）。
- **说明**：论文未给出完整训练所需的GPU小时数，仅提供了推理阶段的时间参考。

### 5. 实验数量与充分性

- **实验数量相当丰富**：
  - **主实验**：5个数据集 × 2种协议 × 3种噪声水平 = 30组对比（表1-2）。
  - **单独噪声类型**：E-E、E-A、A-A各50%噪声（表5-6）。
  - **消融实验**：训练阶段（w/o DRL、w/o DRF、仅不确定性/仅共识）；测试阶段（w/o TTR、w/o DRF、MLLM增强对比）等（表3）。
  - **参数分析**：λ、τ、β的敏感性（图7）。
  - **可靠性可视化**：图3、4、5展示分布和权重。
  - **多种MLLM**：Qwen2.5-VL 3B/7B/72B、LLaVA-1.6 34B对比（表12）。
  - **不同骨干**：SigLIP和BLIP（表16）。
  - **额外数据集**：FB15K-DB15K和FB15K-YAGO15K（表17-18）。
  - **推理时分析**：时间复杂度与内存消耗（附录G.8）。
- **充分性评估**：实验设计系统、覆盖全面，消融清晰，对比公平（统一骨干、相同噪声注入方式），结论可信。

### 6. 论文的主要结论与发现

- 现有MMEA方法在DNC下性能剧烈下降，而RULE在所有设置（0%-50%噪声）下显著超越所有对比方法，平均Hit@1提升5-20个百分点。
- 双重可靠性估计（不确定性+共识）能有效区分干净对和噪声对。
- 鲁棒融合和差异消除模块能抑制噪声影响，测试时对应推理（TTR）进一步挖掘潜在连接，提升匹配准确率。
- 即使在无额外噪声的“Inherent DNC”场景（实际数据集自带噪声）中，RULE也能取得最佳结果，表明其泛化性。

### 7. 优点

- **问题新颖**：首次定义并解决MMEA中的DNC问题，填补了该领域对双重噪声对应研究的空白。
- **方法论完善**：同时处理训练和测试两个阶段的噪声，结合证据学习、软标签、加权融合和MLLM推理，框架完整且实用。
- **可靠性估计巧妙**：不确定性（基于Dirichlet分布）和共识（基于相似度一致性）两重原则互补，可自适应确定划分阈值。
- **测试时推理创新**：利用MLLM + CoT进行逐步推理，挖掘属性对间的隐含语义关联，显著提升鲁棒性。
- **实验严谨**：大量实验覆盖多种噪声类型、多种骨干、多种MLLM，消融和参数分析充分，结果客观。

### 8. 不足与局限

- **计算开销**：测试时MLLM推理较为昂贵（尤其72B模型），在资源受限场景下可能不实用。论文虽提供了轻量版选项，但性能略降。
- **MLLM依赖**：TTR模块的推理质量受限于MLLM的知识覆盖和推理能力，存在失败案例（如缩写实体的识别），可能引入新类型的误判。
- **噪声类型假设**：论文假设噪声以纯随机方式注入，但真实世界的噪声可能是系统性的（如特定属性类型易出错），未深入探讨。
- **未验证大规模图谱**：实验限于中等规模数据集（约1.5万-2万实体对），未在真实大规模KG（如全量Wikidata）上评估，可扩展性待验证。
- **可解释性**：虽然可视化了可靠性权重，但对如何自动确定阈值（β_u、β_c）的机制说明较少，依赖最大最小值的自适应策略可能对异常值敏感。
- **未与其他噪声处理范式对比**：如主动学习、跨模态去噪等，未直接与文献中其他噪声处理方法比较（论文附录G.13仅作简要讨论，未实验对比）。

（完）
