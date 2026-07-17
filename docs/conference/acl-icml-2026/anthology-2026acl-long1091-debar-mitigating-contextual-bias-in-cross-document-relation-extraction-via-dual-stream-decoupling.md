---
title: "DEBAR: Mitigating Contextual Bias in Cross-Document Relation Extraction via Dual-Stream Decoupling"
title_zh: DEBAR：通过双流解耦缓解跨文档关系抽取中的上下文偏差
authors: "Zhixuan Yang, Fu Zhang, Huangming Xu, Jingwei Cheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1091.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 跨文档关系抽取中的偏见缓解
tldr: 跨文档关系抽取中现有方法融合目标实体与桥梁实体导致片面关系转移偏差。本文提出DEBAR，通过双流解耦分别建模目标实体和桥梁实体，并引入自适应阈值策略，有效缓解偏差并增强推理链完整性。实验证明DEBAR在跨文档关系抽取任务上性能显著提升。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 820, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 785, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1091/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 797, \"height\": 593, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 726, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 782, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 637, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1091/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 811, \"height\": 872, \"label\": \"Table\"}]"
motivation: 现有方法在跨文档关系抽取中因融合表示导致片面关系转移偏差。
method: 提出双流解耦框架，分别建模目标实体流和桥梁实体流，并采用自适应阈值。
result: 在跨文档关系抽取数据集上取得最优性能，有效缓解偏差。
conclusion: 双流解耦策略是提升跨文档关系抽取推理完整性的有效方法。
---

## Abstract
Cross-document Relation Extraction (CodRE) requires reasoning over scattered evidence to identify relations between target entities across multiple documents. Existing methods indiscriminately fuse target entities and the intermediate bridge entities that link them into a unified representation. This leads to intermediate evidence that often aligns with only one side of the entity pair, resulting in one-sided relation transfer contextual bias and incomplete reasoning chains. Moreover, these methods typically employ a global threshold to determine relation existence for all entity pairs, limiting the model’s reasoning performance.To address these issues, we propose **DEBAR** (Dual-stream Entity Bias Reduction), a framework designed to explicitly decouple and preserve bidirectional bridge evidence, combined with a novel dynamic loss optimization objective. Specifically, DEBAR employs a **bridge-aware input construction** strategy and a **dual-stream graph reasoning network** to separately encode head and tail contexts, preventing semantic interference while capturing global dependencies through iterative message passing. Furthermore, we introduce a **curriculum-aware ranking optimization objective** that progressively tightens classification constraints to stabilize training and enforce discriminative decision boundaries. Experiments on the CodRE benchmarks show that DEBAR achieves state-of-the-art performance while effectively mitigating cross-document contextual bias. Moreover, extensive experiments on our proposed loss across backbones confirm its generalization, suggesting it as a reliable replacement for existing CodRE losses. Code is available at https://github.com/newyuyou/DEBAR.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

跨文档关系抽取（Cross-document Relation Extraction, CodRE）旨在从多个分散的文档中整合推理证据，识别目标实体对之间的语义关系。现有方法的一个关键缺陷是：它们将目标实体（头实体、尾实体）与连接它们的中间桥梁实体（bridge entity）不加区分地融合到一个统一表示空间中。这种融合导致中间证据往往只与实体对中的一侧对齐（例如偏袒头实体而忽略尾实体），从而产生**片面关系转移上下文偏差**（one-sided relation transfer contextual bias），使得推理链不完整。此外，现有方法对所有实体对使用一个固定的全局阈值（global threshold）来判断关系是否存在，这无法保证正样本得分始终高于负样本，限制了模型判别能力。本文针对这两个问题提出解决框架。

## 2. 方法论

- **核心思想**：显式解耦和保留双向桥梁证据，通过双流架构独立编码头实体和尾实体的上下文，再通过图迭代推理合成全局关系；同时引入动态训练目标替代固定阈值。
- **关键技术组件**：
  - **桥梁感知输入构建（Bridge-aware Input Construction, BIC）**：首先计算每个桥梁实体与头实体和尾实体在不同粒度（句子、段落、文档）上的共现频次加权得分（公式1，权重α>β>γ）；然后使用几何平均综合两方向得分（公式5）以惩罚单侧连接；最后将桥实体得分传播到句子级别（公式6），选取得分最高的句子分别构建头实体和尾实体的两个独立输入流。
  - **双流图推理网络（Dual-Stream Graph Reasoning Network, DSGN）**：使用预训练语言模型分别对两个输入流编码（公式7），提取头、尾及桥梁实体的独立表示；构建全局实体图，初始化节点状态和全局状态；通过图循环网络（GRN）迭代L步，每步进行门控聚合、局部状态更新（公式8）和全局状态更新（公式9），交替传递消息以融合解耦后的信息。
  - **关系预测与课程感知排序优化（Curriculum-aware Ranking Optimization, CAO）**：路径级表示经MLP和跨路径自注意力得到袋级得分（公式10）。CAO损失包含两部分：
    - *课程式分类损失*：动态调整上界m_n和下界m_p，从宽松逐步收紧（m_start → m_end），迫使正负样本分离（公式11）；
    - *加权成对排序损失*：对每个正-负样本对施加惩罚，使用sigmoid加权确保正样本得分高于负样本（公式12-13）。
  - 最终损失：L_CAO = L_CL + λ L_rank。

## 3. 实验设计

- **数据集**：使用 CodRED 标准基准，源自 Wikipedia 和 Wikidata，包含 276 种关系类型，文档平均长度约 4939 tokens。训练/开发/测试集信息见表1。
- **实验场景**：
  - **封闭设置**（Closed Setting）：预提供有效文本路径。
  - **开放设置**（Open Setting）：需自行从语料库检索路径。
  - 额外设置：移除单文档子集，仅保留严格跨文档实例（表4）。
- **对比方法**：Pipeline、End-to-end、ECRIM、MR.COD、LGCR、NEPD，以及GPT-3.5-turbo、InstructUIE等大语言模型。
- **评价指标**：AUC、F1、P@500、P@1000。与LLM对比时使用Micro-F1。

## 4. 资源与算力

论文未明确说明使用的GPU型号和数量（如V100、A100等）。仅在表6中报告了训练时间效率：End-to-end 6.5小时/epoch，ECRIM 9.7小时/epoch，DEBAR 10.2小时/epoch。对于具体硬件规格，文中未提及。

## 5. 实验数量与充分性

论文进行了全面丰富的实验，包括：
- 主实验结果：表2（BERT-base，封闭+开放）、表3（RoBERTa-large，封闭）、表4（仅跨文档子集）。
- 消融实验（表5）：逐个移除BIC、双流编码器、GRN、CAO等组件，均导致显著性能下降，验证各模块必要性。
- 效率对比（表6）。
- CAO泛化实验（表7）：将CAO损失应用于End-to-end和ECRIM基线，F1均有提升。
- 与LLM对比实验（表8）。
- 桥梁实体数量影响分析（图3a, 3b）。
- 得分分布可视化（图4）。
- 案例研究（表9）：定性分析偏差缓解效果。
- 超参数分析（附录A）：考察α,β,γ、λ、δ等参数敏感性。

所有实验均在同一基准、相同评价指标下进行，对比方法涵盖多种主流基线，消融设计与分析完整。结论客观，实验充分。

## 6. 主要结论与发现

- DEBAR在封闭和开放设置下均取得最优（SOTA）结果，显著优于此前最佳方法（例如在BERT-base上，封闭开发集F1提升0.95，AUC提升0.42）。
- 使用RoBERTa-large时优势更为明显（AUC提升1.55，F1提升2.06）。
- 仅使用跨文档子集时，DEBAR仍领先NEPD和ECRIM（F1提升1.10以上）。
- 消融实验证实每个组件（BIC、双流编码、GRN、CAO）均有贡献，特别地BIC贡献最大（F1下降5.74）。
- 所提出的CAO损失具有良好泛化性，可替换现有CodRE损失提升其他模型性能。
- 案例研究直观展示了DEBAR如何通过桥梁感知筛选避免噪声，构建完整证据链。

## 7. 优点

- **创新性**：首次明确提出CodRE中的片面关系转移偏差，并设计双流解耦结构针对性缓解。
- **方法有效**：BIC模块通过联合共现权重确保双向连接，GRN迭代融合全局依赖，CAO动态阈值与排序损失共同提升判别力。
- **实验扎实**：在多个设置下验证，消融完整，与LLM对比说明专用架构的优势。
- **泛化性强**：所提损失可应用于其他框架并带来提升。
- **可复现**：开源代码（GitHub）。

## 8. 不足与局限

- **额外计算开销**：双流独立编码需要分别处理头尾输入，相比单流融合方法引入了约5%的训练时间延迟（从9.7小时/epoch到10.2小时/epoch）。
- **对桥梁实体的依赖**：方法显式依赖桥梁实体构建证据路径，在桥梁实体稀疏或缺失的场景下可能不适用。作者在局限中承认，未来可考虑引入隐式推理机制和非桥梁实体的辅助上下文。
- **未报告GPU型号与数量**：影响了硬件资源消耗的可比性。
- **仅在CodRED单一数据集上验证**：虽然该数据集是标准基准，但更广泛数据集上的泛化性尚未验证。

（完）
