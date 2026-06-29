---
title: "Cross-Modal Factor Reasoning with LLMs: Toward Semantic-Structured Generalization for Recommendation"
title_zh: 基于大语言模型的跨模态因子推理：面向推荐的语义结构化泛化
authors: "Wei Yang, Rui Zhong, Ze-Yu Song, Hengwei Ju, Yuecheng Li, Yiqun Chen, Ching Chang, Gengshuo Liu, Chi Lu, Peng Jiang"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Y6idSGOwfK"
tags: ["query:multimodal"]
score: 6.0
evidence: 利用LLM进行跨模态因子推理以实现推荐
tldr: 本文提出MARS框架，利用大语言模型进行跨模态因子推理，从多模态内容中提取结构化的语义关系（如功能、风格），而非浅层融合。该方法增强了推荐中的语义泛化能力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-y6idsgowfk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1449, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-y6idsgowfk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1440, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-y6idsgowfk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 700, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-y6idsgowfk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 703, \"height\": 298, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-y6idsgowfk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 696, \"height\": 265, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-y6idsgowfk/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 692, \"height\": 292, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-y6idsgowfk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-y6idsgowfk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1445, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-y6idsgowfk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 847, \"height\": 222, \"label\": \"Table\"}]"
motivation: 现有多模态推荐方法浅层融合多模态特征，缺乏结构化语义推理。
method: 引入LLM进行跨模态因子推理，构建结构化语义关系图以增强推荐。
result: 提升了推荐系统的个性化性能和语义泛化能力。
conclusion: MARS将LLM的推理能力有效应用于多模态推荐中的语义理解。
---

## Abstract
Multimodal recommendation aims to enhance personalization by leveraging content signals such as text and images. However, existing methods often treat modalities as shallow auxiliary inputs, fusing raw embeddings without reasoning about what semantics are useful or how they influence user preference. Content-based graphs typically rely on low-level similarity, lacking structured semantic relations such as functionality or style. Moreover, collaborative signals are used solely for ranking, without grounding content semantics. To address these limitations, we present MARS, a framework for Cross-Modal FActor Reasoning with LLMs, enabling Semantic-Structured Generalization in recommendation. MARS introduces a cognitively guided paradigm that prompts large language models (LLMs) to extract human-interpretable semantic factors (e.g., functionality, material and usage scenario) from raw visual and textual descriptions. These structured factors are used to build heterogeneous graphs that capture multi-aspect semantic relations among items. To integrate semantics into representation learning, we propose an auxiliary semantic prediction task that aligns collaborative embeddings with LLM-inferred factor knowledge. In addition, a cross-modal consistency loss encourages agreement across semantic views from different modalities. Extensive experiments show that MARS achieves superior accuracy and generalization compared to state-of-the-art multimodal baselines and LLM-based methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

现有多模态推荐方法通常将视觉、文本等模态特征作为浅层辅助信号，通过拼接、门控或注意力机制进行融合，缺乏对语义内容的结构化理解。具体问题包括：

- **语义浅层化**：模型只对特征向量进行融合，而不理解每个模态中哪些语义因素对用户偏好真正有用。
- **图构建依赖低层相似性**：基于多模态嵌入的item-item图仅能捕捉视觉或文本的低级相似度，无法表示功能、风格、使用场景等高阶语义关系。
- **协同信号流向单向**：协同信号仅用于排序，没有反向监督内容理解，导致语义鸿沟。

为此，论文提出**MARS**（Cross-Modal FActor Reasoning with LLMs）框架，借助大语言模型（LLM）对多模态内容进行高阶语义因子推理，构建结构化异构语义图，并通过辅助任务将语义知识注入协同表示，实现语义结构化的推荐泛化。

## 2. 方法论

### 核心思想
利用LLM从原始视觉和文本描述中提取人类可解释的语义因子（如功能、材料、使用场景），基于这些因子构建多视角异构图，并在图传播后通过语义预测任务和跨模态一致性约束使协同嵌入语义化。

### 关键技术细节

#### 2.1 LLM驱动的跨模态因子推理（两阶段）
- **阶段一：因子模式归纳**——提示LLM识别目标领域的关键语义因子集合 \( F = \{f_1, f_2, ..., f_K\} \)，每个因子对应一个有限属性空间。
- **阶段二：因子属性分配**——对每个物品，基于其多模态内容（文本描述、图像说明），让LLM推断每个因子的具体属性值，形成结构化档案 \( A_i = \{(f_k, a_k^{(i)})\} \)。

#### 2.2 异构图构建
- **因子级图**：对每个因子 \( f_k \)，若两个物品属性值相同则连边，得到二进制邻接矩阵 \( A_{f_k} \)，并做对称归一化。
- 所有因子级图构成异构语义图系统。

#### 2.3 多图增强的物品表示学习
- **骨干图编码**：拼接ID、视觉、文本特征后通过全连接映射得到统一表示 \( X \)，再基于全连接相似图（Top-K）做卷积得到结构增强嵌入 \( H_{struct} \)。
- **语义图传播**：在每个因子图 \( \hat{A}_{f_k} \) 上独立传播得到 \( H_{f_k} \)。
- **自适应融合**：通过可学习的门控权重 \( \alpha_i^{(k)} \) 动态融合各语义视图和结构视图，公式：
  \[
  H_i = \sum_{k=1}^K \alpha_i^{(k)} H_{f_k}^{(i)} + \alpha_i^{(struct)} H_{struct}^{(i)}
  \]
  权重由 \( [\alpha_i^{(struct)}, \alpha_i^{(1)}, ..., \alpha_i^{(K)}] = \text{softmax}(W_g \cdot X_i) \) 计算。

#### 2.4 语义因子预测辅助任务
- 设计多层标签分类器 \( \psi \)，从最终嵌入 \( H_i \) 预测所有因子属性的联合 multi-hot 向量 \( \hat{y}_i \)。
- 损失函数为多标签二元交叉熵 \( \mathcal{L}_{sem} \)。
- 信息论视角：该任务最大化 \( I(H_i; y_i) \) 并压缩无关噪声，遵循信息瓶颈原理。

#### 2.5 跨模态视图一致性正则化
- 对ID、视觉、文本三个视图的嵌入两两计算L2距离，作为一致性损失 \( \mathcal{L}_{view} \)。
- 促进多视图语义对齐，抑制模态特异噪声。

#### 2.6 多目标联合优化
- 主损失：BPR排序损失 \( \mathcal{L}_{rec} \)。
- 总损失：\( \mathcal{L} = \mathcal{L}_{rec} + \lambda \mathcal{L}_{sem} + \eta \mathcal{L}_{view} \)。
- \( \lambda \) 和 \( \eta \) 为超参数。

## 3. 实验设计

### 数据集
- **Amazon Review** 的三个子集：Baby、Sports and Outdoors、Clothing, Shoes and Jewelry。
- 采用5-core预处理，保留至少5次交互的用户与物品。
- 原始图像作为视觉模态，文本由标题、描述、品牌、类别拼接而成。

### 基准方法
- **传统协同过滤**：LightGCN
- **经典多模态**：MMGCN, GRCN, DualGNN, LATTICE, FREEDOM, DiffMM, MMIL, AlignRec, SMORE
- **基于LLM的方法**：RecFormer, TALLRec, A-LLMRec, UniMP

### 评价指标
- Recall@K 和 NDCG@K（K=10, 20），全排序评估（所有物品参与排名）。

### 实现细节
- 文本和视觉嵌入分别使用 Sentence-BERT 和 LLaVA-7B 初始化。
- 语义因子推理使用 GPT-4o，选取Top-10最频繁因子。
- 超参数 \( \lambda, \eta \) 从 {0.1, 0.01, 0.001, 0.0001} 调优。
- 代码基于 MMRec 框架，PyTorch实现。

## 4. 资源与算力

论文明确指出：
- **单个 NVIDIA A40 GPU（48GB）** 完成所有实验。
- **未报告具体训练时间或迭代轮次**，因此无法评估实际效率。

## 5. 实验数量与充分性

共包含以下实验组：
- **主表对比**（Table 1）：在3个数据集上比较12种以上基线方法，报告Recall和NDCG各2个指标，共3×4=12组对比，结果全面。
- **冷启动实验**（Table 2）：针对用户只有5个交互的冷启动场景，在3个数据集上对比6个代表性基线，同样4个指标，共12组结果。
- **消融实验**（Figure 2）：移除了语义预测、一致性损失、多模态、语义图等核心组件，并在3个数据集上对比Recall@20和NDCG@20，共6组对比。
- **超参数敏感性**（Figure 3-4）：考察 \( \lambda \)、\( \eta \) 和嵌入维度 \( d \) 的影响，涉及3个数据集。
- **表示散度分析**（Figure 5）：比较有无视图一致性损失时的跨模态表示距离分布。
- **t-SNE可视化**（Figure 6）：对比基线（FREEDOM）与MARS在“Target Age”属性上的语义聚类效果。

**充分性评估**：实验覆盖了主流对比、冷启动、消融、超参调优、可视化以及定量分析，设计较为全面；但缺乏对模型复杂度（训练/推理时间）的量化对比，也没有跨领域（如视频、音乐）的验证，公平性方面所有实验基于同一代码库，超参数采用最优配置，可认为是客观公平的。

## 6. 主要结论与发现

- MARS在所有数据集和指标上**显著优于**最先进的基线和LLM方法，例如在Sports数据集上比SMORE高5.6% Recall@10。
- **冷启动场景**下优势更加突出，说明语义结构化表示对稀疏交互具有强泛化能力。
- **消融实验**证实：
  - 语义预测任务（w/o FP）最为关键；
  - 语义图结构（w/o SG）比单纯标签监督更重要；
  - LLM推理的高质量因子（对比r/p SF）不可或缺；
  - 跨模态一致性损失（w/o CL）和原始多模态（w/o MM）均有贡献。
- **超参数敏感度**：\( \lambda=0.001 \)、\( \eta=0.01 \) 效果最好，过大或过小都会损伤性能；嵌入维度128为最佳选择。
- **表示散度和语义聚类**可视化表明，MARS有效降低了跨模态表示差异并形成了更清晰、符合语义的簇结构。

## 7. 优点

1. **创新性突出**：首次将LLM的语义推理能力与多模态推荐的图结构学习深度融合，提出“语义因子→异构语义图→语义预测辅助任务”全套流程，思想清晰。
2. **可解释性强**：提取的因子（如功能、材料）是人类可理解的，通过辅助任务将协同嵌入与符号语义对齐，模型更具透明性。
3. **实验全面**：涵盖主流多模态、LLM基线，包含冷启动、消融、超参、可视化等，结果一致支持方法有效性。
4. **理论支撑**：从信息瓶颈角度对语义预测任务进行理论分析，增强了方法的可信度。
5. **设计简洁有效**：多图自适应融合、轻量级一致性损失，不增加过多复杂度。

## 8. 不足与局限

1. **LLM推理成本**：使用GPT-4o进行因子提取，虽未公开推理时间和API成本，但实际部署中可能带来较大开销，且依赖商业化API，可复现性受限。
2. **物品端仅语义**：方法仅从物品内容提取语义因子，未探索用户侧的语义图（如用户偏好因子），未来工作提及但未实现。
3. **数据集单一**：仅在Amazon三个子集上验证，均为电商场景，缺少视频、音乐、新闻等其他类型多模态推荐评估，外推性待检验。
4. **未报告训练效率**：没有提供训练时间、参数数量、显存占用等效率指标，不利于与其他方法公平比较计算开销。
5. **因子数量固定**：取Top-10最频繁因子，未分析不同因子数量对效果的影响，可能忽略稀有但重要的因子。
6. **超参数调优未深入**：λ和η的候选集较粗（4个值），且未跨数据集独立最优报告，可能存在过拟合风险。
7. **缺少与更多LLM方法的比较**：最新LLM推荐方法如LLaRA、RecMind等未被纳入对比。
8. **可视化为定性分析**：t-SNE仅展示单语义属性，缺乏定量聚类指标（如NMI、ARI）支撑。

（完）
