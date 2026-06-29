---
title: "ALMEA: Active Learning-Enhanced Multimodal Entity Alignment with Semantic Modality Imputation"
title_zh: ALMEA：基于主动学习和语义模态补全的多模态实体对齐
authors: "Xizhe Zhang, Meng-Fen Chiang, Jingfeng Zhang"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=iitxXWqODX"
tags: ["query:joint-mer"]
score: 6.0
evidence: 多模态实体对齐与主动学习
tldr: 该论文提出ALMEA框架，针对多模态知识图谱中实体对齐任务，通过语义校准补偿缺失模态，并利用主动学习降低种子对需求。虽专注于实体对齐而非关系抽取，但方法在多模态实体处理方面与联合多模态实体关系抽取有较强关联。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1433, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1454, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1420, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1439, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1376, \"height\": 1090, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 943, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 947, \"height\": 461, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 943, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1331, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1442, \"height\": 1584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-iitxxwqodx/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1374, \"height\": 873, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1451, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 682, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1442, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1444, \"height\": 1717, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1501, \"height\": 2144, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 724, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1438, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1431, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1458, \"height\": 197, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1454, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 939, \"height\": 689, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 862, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1159, \"height\": 992, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 687, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 996, \"height\": 694, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-iitxxwqodx/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 579, \"height\": 292, \"label\": \"Table\"}]"
motivation: 多模态实体对齐面临模态缺失和语义不一致问题，且低资源场景下种子对有限。
method: 集成语义校准和主动学习，合成缺失模态的表示，并策略性选择最有信息量的样本进行标注。
result: 在实体对齐基准上提升了低资源下的鲁棒性，但未涉及关系抽取。
conclusion: 多模态对齐技术可迁移至联合抽取中的实体识别，但关系维度缺失。
---

## Abstract
Multimodal knowledge graphs (MMKGs) offer enriched knowledge representation by integrating structural, visual, and textual information from heterogeneous sources. However, existing multimodal entity alignment (MMEA) approaches face significant challenges due to missing modalities and semantic inconsistencies across sources. These limitations compromise alignment robustness, especially in low-resource scenarios with limited seed pairs (i.e., manually annotated aligned entities as supervision).

To bridge the gap, we propose **Active Learning for Multimodal Entity Alignment with Semantic Imputation (ALMEA)**, a MMEA framework that integrates semantic calibration and active learning to improve alignment. Specifically, ALMEA synthesizes embeddings for missing modalities and refines semantic representations to address inconsistencies across MMKGs. This approach iteratively selects optimal candidate pairs within the learnable budget through active learning strategies, thereby acquiring richer modal information in low-resource scenarios.

On the benchmark MMKG dataset, experimental results indicate that ALMEA consistently outperforms state-of-the-art baseline models under the low-resource scenario, achieving average improvements of **5.16% in Mean Reciprocal Rank (MRR)** and **5.57% in Hits at Top-1 (Hits@1)**.

Our anonymized code is available at [github.com/RTX4090123/ALMEA](https://github.com/RTX4090123/ALMEA).

---

## 论文详细总结（自动生成）

# 论文总结：ALMEA – 基于主动学习和语义模态补全的多模态实体对齐

## 1. 核心问题与整体含义（研究动机与背景）

多模态知识图谱（MMKG）融合了结构、视觉和文本信息，但现有的大多数多模态实体对齐（MMEA）方法面临两个关键挑战：
- **模态缺失与语义不一致**：不同知识图谱间实体可能缺失视觉、属性等模态，且跨图谱的语义分布存在差异，导致对齐失效。
- **低资源场景下种子对不足**：实际应用中人工标注的对齐实体对（种子对）非常有限，传统方法在监督稀疏时性能急剧下降。

该论文旨在通过**主动学习**和**语义校准**来提升MMEA在低资源条件下的鲁棒性和准确性。

## 2. 方法论：核心思想与技术细节

论文提出了 **ALMEA** 框架，包含三个核心模块：

### 2.1 潜在语义学习（LSL）
- 使用**变分自编码器（VAE）** 对缺失模态进行隐空间重建。
- 引入二进制掩码矩阵 \(B\)，模拟模态缺失，通过编码器得到隐变量 \(z_m\)，再通过重参数化采样生成潜在表示。
- 损失函数包括：分布匹配损失（DML，KL正则化）、单模态重建损失（URL，MSE）、跨模态校准损失（SCL，双向KL散度）和联合对齐损失（JAL，MSE）。

### 2.2 潜在语义校准（LSC）
- 对不同模态的潜在嵌入进行线性变换+Tanh激活，得到校准后的嵌入。
- 通过MLP计算模态权重，加权融合得到联合潜在表示。
- 使用双向KL散度最小化源与目标MMKG之间缺失模态对应的语义分布差异。

### 2.3 主动候选选择（ACS）
- 基于**互近邻（mutual NN）** 构建候选池 \(Q\)。
- 构建相异度矩阵 \(A\) 和多样性矩阵 \(C\)，引入多样性得分 \(D\)。
- 将选择问题形式化为**稀疏子集选择（DS3）** 优化问题，通过ADMM求解，在标记预算内选出代表性和多样性兼具的候选对。
- 迭代地将高质量候选对从无标签池提升到有标签池，增强训练信号。

算法流程总结：模型先在有标签集上训练，每间隔一定轮次运行ACS挑选新候选对加入训练，重复多轮。

## 3. 实验设计

### 3.1 数据集与基准
- **FB15K-DB15K** 和 **FB15K-YAGO15K**，包含关系、视觉、属性、邻居等多种模态。
- 种子对划分比例：20%、50%、80%（模拟不同资源水平）。

### 3.2 对比方法
- 经典方法：TransE、GCN-Align、SEA
- 多模态方法：MMEA、EVA、MSNEA、MCLEA、GEEA、MEAformer、OTMEA、SimDiff
- 对比指标：MRR、Hits@1、Hits@10

### 3.3 消融实验与敏感性分析
- 移除LSL、LSC、各损失项、各模态
- 移除ACS中的候选池、多样性得分
- 不同稀疏因子 \(\alpha\) 的敏感性
- 不同主动学习预算（5% Base + 1%×15、10% Base + 1%×10、15% Base + 1%×5）的比较
- 统计显著性检验（配对t检验）

## 4. 资源与算力

- 文中明确提到使用 **Tesla A100 GPU** 进行实验。
- 具体GPU数量未说明。
- 总训练轮数 \(T_{total}=750\)，其中基训练 \(T_{base}=500\)，主动学习轮 \(T_r=5\)，间隔 \(T_{inter}=50\)。
- 批大小3500，学习率0.001，Adam优化器。
- 模型参数量约14.34M（ALMEA），训练速度约1.05 iter/s（含ACS）。

## 5. 实验数量与充分性

- 主要对比实验在**两个数据集** × **三个种子比例**（共6组）上报告了平均值和标准差（各5次运行）。
- 消融实验覆盖**10种以上变体**，包括移除模块、损失函数、模态、主动学习组件等。
- 额外进行了：
  - 模态移除分析
  - 稀疏因子 \(\alpha\) 敏感性（每组约10个点）
  - 低资源预算对比（3种设置，每个设置15轮）
  - 统计显著性检验（t值、p值）
  - 效率与复杂度分析
  - 定性案例分析（含热力图）
- **实验设计全面**，覆盖了方法各组件的影响、超参数敏感性、统计可信度，对比方法均为近年SOTA，且多数复现运行。
- **公平性**：报告多次运行的平均值和标准差，进行统计检验，超参数通过网格搜索确定。

## 6. 主要结论与发现

- ALMEA在所有种子比例下（20%、50%、80%）均**超越所有基线**，尤其在低资源（20%）下增益最大（平均MRR提升5.16%，Hits@1提升5.57%）。
- 在缺失视觉模态较多的FB15K-YAGO15K上，提升幅度（4.19%）高于FB15K-DB15K（1.25%），说明ALMEA对模态缺失更鲁棒。
- 语义校准（LSC）比语义学习（LSL）贡献更大，移除LSC下降明显。
- 主动学习（ACS）在低资源下显著提升性能，且多样性得分D对选择质量至关重要。
- 非主动学习的变体（ALMEA w/o ACS）也优于大多数基线，但加入ACS后进一步扩大优势。

## 7. 优点

- **创新性**：首次将主动学习与语义校准结合，系统解决MMEA中模态缺失和低资源两大难题。
- **技术完整性**：构建了从缺失模态生成、语义分布对齐到主动样本选择的完整流程，各模块设计有理论支撑（VAE、KL散度、DS3优化）。
- **实验充分**：覆盖多数据集、多资源水平、大量消融和敏感分析，并进行了统计显著性检验，结果可信。
- **效率尚可**：尽管模型参数量略高于部分基线，但训练速度在可接受范围内（1.05 iter/s）。
- **可复现性**：提供匿名代码和超参数设置。

## 8. 不足与局限

- **主动学习仍为模拟**：实验采用“模拟主动学习”，即从已有标注数据中隐藏标签，未涉及真实人类标注成本或反馈，可能高估方法在实际应用中的效益。
- **数据集规模有限**：仅在两个中等规模MMKG（约1.5万实体）上评估，在更大规模、更复杂场景（如多语言、开放域）下的泛化性未验证。
- **超参数敏感**：稀疏因子 \(\alpha\)、温度 \(\tau\)、ADMM参数等需针对不同数据集调优，可能影响实用便捷性。
- **无关系抽取维度**：论文完全聚焦于实体对齐，未处理关系层级语义，无法直接用于联合多模态实体关系抽取任务。
- **偏差风险**：虽然未提及，但视觉或文本模态的预训练表示可能携带社会偏见，对齐过程可能放大，文中未讨论偏差审计。
- **计算资源**：虽未明确GPU数量，但A100单卡训练750 epoch可能耗时数小时，对资源受限场景不友好。

（完）
