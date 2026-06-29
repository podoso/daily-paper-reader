---
title: Multimodal Representation Learning Conditioned on Semantic Relations
title_zh: 基于语义关系的多模态表示学习
authors: "Yang Qiao, Yuntong Hu, Liang Zhao"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=zAtrBcGsyf"
tags: ["query:multimodal"]
score: 7.0
evidence: 基于语义关系的多模态表示学习
tldr: 现有多模态对比模型如CLIP只关注图像-文本对，忽略跨对的语义关系。RCML提出基于自然语言关系描述的条件多模态学习，构建多对多训练对，引导特征提取和对齐，从而更好地捕捉语义关联。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1438, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 659, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 696, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 640, \"height\": 704, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 695, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1431, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-zatrbcgsyf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1439, \"height\": 760, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1477, \"height\": 1006, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 918, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1381, \"height\": 1218, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1378, \"height\": 878, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1380, \"height\": 1319, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1379, \"height\": 1288, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1380, \"height\": 849, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1375, \"height\": 1866, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1375, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1377, \"height\": 2345, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1378, \"height\": 2180, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1376, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1377, \"height\": 1784, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1379, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1378, \"height\": 1678, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1380, \"height\": 779, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-zatrbcgsyf/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1379, \"height\": 900, \"label\": \"Table\"}]"
motivation: 对比模型如CLIP未充分利用跨图像-文本对的语义关系，且全局对齐缺乏上下文。
method: 提出Relation-Conditioned Multimodal Learning (RCML)，用自然语言关系描述指导表示学习和对齐。
result: 方法在多个多模态基准上提升了表示质量。
conclusion: 条件多模态学习能更有效地捕捉语义关系。
---

## Abstract
Multimodal representation learning has advanced rapidly with contrastive models such as CLIP, which align image-text pairs in a shared embedding space. However, these models face the limitations: (1) they typically focus on image-text pairs, underutilizing the semantic relations across different pairs. (2) they directly match global embeddings without contextualization, overlooking the need for semantic alignment along specific subspaces or relational dimensions. To address these issues, we propose Relation-Conditioned Multimodal Learning (RCML), a framework that learns multimodal representations under natural-language relation descriptions to guide both feature extraction and alignment. Our approach constructs many-to-many training pairs linked by semantic relations and introduces a relation-guided cross-attention mechanism that modulates multimodal representations under each relation context. The training objective combines cross-modal and intra-modal contrastive losses, encouraging consistency across both modalities and semantically related samples. Experiments on different datasets show that RCML,consistently outperforms strong baselines on both retrieval and classification tasks, highlighting the effectiveness of leveraging semantic relations to guide multimodal representation learning.

---

## 论文详细总结（自动生成）

# 论文总结：基于语义关系的多模态表示学习 (RCML)

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **现有问题**：当前主流的对比学习模型（如 CLIP）仅利用图像-文本对进行对齐，忽略了跨样本间丰富的语义关系（如功能互补、共同购买意图等）。此外，它们直接匹配全局嵌入，缺乏上下文，无法沿特定语义维度进行对齐。
- **研究动机**：在许多现实场景（如商品推荐、科学文献关联、社交媒体）中，不同样本在特定语义关系下紧密相关，但现有模型无法捕获这种关系层面的相似性。
- **目标**：提出一种能够利用自然语言描述的关系来指导多模态表示学习的框架，实现基于语义关系的多对多对齐。

## 2. 论文提出的方法论
- **核心思想**：将样本间的关系（用自然语言描述）作为条件信号，在特征提取和对比学习过程中引导表示生成，从而获得上下文感知的关系化嵌入。
- **关键技术细节**：
  1. **关系引导的注意机制**：对每个样本对 (Vi, Vj) 及其关系描述 eij，利用关系嵌入作为查询（Query），对文本/图像 token 进行加权聚合，得到关系条件化的特征 z<sub>i</sub><sup>x</sup>(e<sub>ij</sub>)。公式中 β 控制关系引导与全局池化的平衡。
  2. **多对多训练对构建**：包括内样本关系（同一产品的文本-图像对）和跨样本关系（不同产品间由用户行为定义的语义关系）。
  3. **损失函数**：统一损失包含四个对比项：文本到图像、图像到文本、文本到文本、图像到图像，分别计算交叉模态和模态内一致性。损失形式为温度缩放的交叉熵（公式 1-2）。
- **与 CLIP 的关系**：当 β=1 且仅使用交叉模态自对比时，RCML 退化为 CLIP。

## 3. 实验设计
- **数据集**：
  - **Amazon 产品数据集**：7 个领域（Electronics, Automotive, Office Products, Baby, Pet Supplies, Musical Instruments, Sports）。
  - **Goodreads 数据集**：书籍，作为域外评估集（OOD）。
- **基准方法**：CLIP, DeCLIP, UniCL, SigLIP, ImageBind（均为官方或公开检查点）。
- **评估任务**：
  1. **关系引导检索**：给定源物品和关系类型，从 21 选 1 候选中检索目标物品，指标 Hit@5。使用五种相似度（TT, II, TI, IT, AVG）。
  2. **关系类型预测**：给定物品对，从多个候选关系中选出正确的关系类型（10/8 类），指标 Top-3 准确率。
  3. **关系有效性预测**：二分类，预测给定物品对是否具有某关系，训练线性分类器，指标准确率。
- **消融实验**：移除跨样本关系、移除模态内损失、移除关系描述、冻结 CLIP 编码器。
- **敏感性分析**：变化注意力平衡系数 β ∈ [0,1]。
- **可视化**：t-SNE 和典型案例展示。

## 4. 资源与算力
- **硬件**：单块 NVIDIA RTX A6000（48GB 显存）。
- **训练配置**：批次大小 512，AdamW 优化器，学习率 5e-5（余弦衰减），训练 3 个 epoch 内收敛（早停）。模型参数量 152.33M（略高于 CLIP 的 151.28M）。
- **推理时间**：14.32 ms/样本。

## 5. 实验数量与充分性
- **实验数量**：主表（Table 1）覆盖 8 个数据集 × 5 种相似度 × 6 个方法，共 240 个指标；还有关系类型预测（图2）、有效性预测（图3）、消融（图4）、敏感性（图5）、可视化（图6）、案例（图7），总计 10 组以上实验。
- **充分性与公平性**：比较全面，消融覆盖各组件，baseline 使用相同关系文本输入。多次运行（3 次）取平均。但仅在两个数据集（Amazon 和 Goodreads）上评估，未在更大规模或更多模态上验证。总体实验设计客观、公平。

## 6. 论文的主要结论与发现
- RCML 在所有任务上持续超越强 baseline（CLIP 提升约 30.79% Hit@5），尤其在关系引导检索上优势显著。
- 跨样本关系是最大贡献因素（消融去除后降 38.68%），其次是关系描述（降 11.60%）和模态内损失（降 8.5%）。
- 对 β 值鲁棒（0.0-0.6 性能稳定），β=1（纯 CLIP）时性能骤降。
- 模型在域外 Goodreads 上表现良好，说明关系条件化可跨域泛化。
- t-SNE 显示 RCML 能按关系语义形成更紧凑的聚类。

## 7. 优点
- **创新性**：首次将自然语言关系作为条件变量融入多模态对比学习，实现多对多对齐，超越了传统对偶视角。
- **架构简洁有效**：在 CLIP 基础上加入轻量注意机制，不增加大量参数（仅 1.05M 额外），推理高效。
- **损失函数统一**：同时优化交叉模态和模态内一致性，理论清晰。
- **实验详实**：多个任务、多种相似度、全面消融和敏感性分析，证明各组件必要。

## 8. 不足与局限
- **关系描述依赖外部知识**：关系描述需通过用户行为聚类生成（或人工定义），自动获取高质量关系描述仍是瓶颈。
- **领域覆盖有限**：仅在商品和书籍数据上验证，未在通用图文预训练（如 CC12M）或更多模态（音频、视频）上测试。
- **未探索端到端大规模预训练**：模型基于 CLIP 进行微调，未从头训练关系感知编码器，可能限制上限。
- **计算开销略高于 CLIP**：推理时间增加约 56%，但仍远低于 ImageBind。

（完）
