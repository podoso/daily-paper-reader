---
title: Multi-Modal Fact Knowledge Generation for Imbalanced Cross-Source Entity Alignment
title_zh: 面向不平衡跨源实体对齐的多模态事实知识生成
authors: "Qian Li, Cheng Ji, Zhaoji Liang, Yuzheng Zhang, Zhuo Chen, Siyuan Liang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38999/42961"
tags: ["query:multimodal"]
score: 4.0
evidence: 多模态事实知识生成用于不平衡跨源实体对齐
tldr: 跨源多模态知识图谱中的模态不均衡导致实体对齐困难。本文提出多模态事实知识生成框架，通过生成缺失模态的事实知识来弥合信息差距。在多个基准上证明了其对不平衡场景下对齐性能的显著提升。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38999/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38999/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1846, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38999/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38999/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 854, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38999/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 851, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38999/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 867, \"height\": 522, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38999/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1824, \"height\": 661, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38999/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 870, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38999/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 382, \"label\": \"Table\"}]"
motivation: 多模态知识图谱中模态不均衡和缺失导致实体对齐性能下降。
method: 生成多模态事实知识来补充缺失信息，增强对齐表示。
result: 在不平衡跨源实体对齐任务上取得最好性能。
conclusion: 通过知识生成有效缓解模态不均衡问题，提升实体对齐鲁棒性。
---

## Abstract
Multi-modal imbalanced cross-source entity alignment aims to identify equivalent entity pairs across multi-modal knowledge graphs (MMKGs) that encompass diverse data sources with imbalanced modality, which poses significant challenges due to the non-uniform distribution of information across different modalities. Existing methods encounter major limitations in aligning entities across MMKGs, where missing data and modality-specific inconsistencies thus create information gaps. These gaps, stemming from disparities in neighborhood structure and attribute availability, result in reduced alignment performance. To address these challenges, we propose a novel multi-modal fact knowledge generation framework to advance imbalanced cross-source entity alignment. Utilizing large language models (LLMs) for comprehensive knowledge completion, our framework enriches MMKGs by synthesizing missing neighboring entities and relational attributes, enabling precise one-to-one similarity comparisons across all relations and attributes. Specifically, neighbor entity completion generates probable neighboring entities to fill structural gaps, while attribute completion synthesizes missing relational attributes to improve alignment. The facts evaluation module assesses generated triples, ensuring that only high-quality information supports the alignment. Extensive experiments on benchmark datasets demonstrate that our framework significantly outperforms strong competitors, achieving superior entity alignment performance.

---

## 论文详细总结（自动生成）

# 多模态事实知识生成用于不平衡跨源实体对齐（LLMEA）—— 论文详细总结

## 1. 论文的核心问题与整体含义
- **研究背景**：多模态知识图谱（MMKGs）广泛用于组织和表示结构化多模态信息，但由于真实世界数据的复杂性，MMKGs常存在信息缺失，不同模态间信息分布不均匀（模态不均衡），使得跨多个MMKG的实体对齐任务非常困难。
- **核心问题**：现有方法在处理多模态不平衡跨源实体对齐（MICEA）时，面临信息差距（information gap）问题。具体表现为：同⼀实体在不同KG中可能拥有不同数量的邻居实体、不同类型或数量的属性（文本、图像），导致结构信息和属性信息的非对应，削弱了实体对之间的相似性比较能力。
- **研究意义**：通过填补缺失信息来弥合模态不均衡带来的信息差距，提升跨源实体对齐的准确性和鲁棒性，对于知识融合、跨语言信息检索、问答系统、推荐系统等应用具有重要价值。

## 2. 论文提出的方法论
### 2.1 核心思想
提出 **LLMEA** 框架，利用大语言模型（LLM）的涌现知识能力生成缺失的邻居实体和关系属性，完成多模态知识图谱的知识补全，从而实现更精确的“一对一”相似度比较。同时设计事实评估模块过滤低质量生成结果，确保补全信息的可靠性。

### 2.2 关键技术细节
- **多模态位置编码（MPE）**：为实体、文本属性、图像属性、实体类型分别赋予独特位置编码，帮助模型区分不同模态。
- **结构位置编码（SPE）**：为邻居节点和关系赋予结构位置编码，保留图结构信息。
- **邻居实体生成**：设计提示词 `P_entity`，引导LLM基于已有邻居生成最可能缺失的邻居实体；再使用 `P_check` 验证生成关系是否存在。引入候选池机制和置信度过滤（阈值 τ_confidence）确保生成实体/关系在候选池内且置信度足够高。
- **属性生成**：类似地，通过 `P_attribute` 引导LLM生成缺失的关系属性，并用 `P_check_a` 筛选。
- **相似度计算**：利用Jaccard系数计算补全后实体之间属性和关系的相似度。
- **事实评估模块**：
  - **TransE评估**：使用TransE评分函数过滤非事实三元组（阈值 τ_a）。
  - **因果评估**：计算生成三元组与已有三元组的Jaccard得分（阈值 τ_c），衡量其对对齐的贡献。
  - **模型编辑评估**：确保生成关系在关系候选池内，并通过相似度函数筛选 top-k 最优三元组。
- **训练目标**：联合实体对齐损失（LEA）和属性相似性损失（Lattr），平衡对齐与属性一致性。

## 3. 实验设计
### 3.1 数据集与场景
- **单语MMEA**：FB15K-DB15K（12,846个对齐种子）、FB15K-YAGO15K（11,199个对齐种子）
- **双语MMEA**：DBP15K ZH-EN、JA-EN、FR-EN（各约15,000个对齐种子）
- **场景**：不同比例的训练种子（20%、50%、80%）下评估模型性能，模拟少样本和完整训练设置。

### 3.2 对比方法
- **单语**：TransE、GCN-align、AttrGNN、BERT、ViT、CLIP、PoE、Chen et al.、HEA、EVA、MSNEA、ACK-MMEA、MoAlign、MEAformer、DESAlign
- **双语**：SBootEA、NAEA、EVA*、MSNEA*、MCLEA*、MMEA-cat、UMAEA、MoAlign、PMF

### 3.3 评估指标
MRR（平均倒数排名）、Hits@1、Hits@10

## 4. 资源与算力
- 文中明确提及：“all the experiments on a server equipped with one Tesla V100 GPU”
- **未明确说明**：训练时长、总GPU小时数、批量大小等具体算力消耗。仅提到训练轮次设为200，但实际耗时未给出。

## 5. 实验数量与充分性
- **主要实验**：6个数据集 × 3个训练比例下的3个指标 = 大量结果（表1、表2），全面对比了多种基线。
- **消融实验**：完整模型 vs. 移除LLM知识补全（LKC）、邻居实体补全（NEC）、属性补全（RAC）、属性损失（AL）、文本属性（TA）、图像属性（IA）——共6组，验证各模块贡献（表3）。
- **属性影响分析**：删除图像/文本/全部属性后MRR变化（图3）。
- **属性数量差距影响**：按属性数量差距分组（0-24），考察MRR变化（图4）。
- **干扰数据实验**：随机替换部分邻居/属性，考察鲁棒性（图5）。
- **可视化**：t-SNE嵌入可视化（图6a-6f），展示对齐效果和多模态属性聚类效果。
- **充分性评价**：实验覆盖了不同模态组合、不同缺失程度、不同训练规模、干扰场景，消融设计合理，对比方法全面，结果统计指标标准。结论客观可信。

## 6. 论文的主要结论与发现
- LLMEA在所有数据集和训练比例下均显著优于所有对比方法，尤其在少样本（20%种子）场景下提升幅度更大，表明知识生成机制有效弥补了信息差距。
- 邻居实体补全和属性补全都是关键模块，缺失任一模块都会导致性能下降。
- 多模态属性（文本+图像）对对齐均有贡献，但图像属性的贡献略小于文本。
- 模型对属性数量差距具有更强的鲁棒性，性能下降更平缓（图4）。
- 对于干扰数据，LLMEA表现出更好的容错能力（图5）。
- 嵌入可视化显示对齐实体对在LLMEA的嵌入空间中更接近，非对齐实体分离更明显。

## 7. 优点
- **创新性**：首次系统性地利用LLM的生成能力来解决多模态知识图谱中因模态不均衡引起的“信息缺口”问题，而非仅依赖已有信息进行表示学习。
- **方法完备性**：包含生成、验证、过滤、训练四个阶段，提示设计、候选池控制、多重评估机制保证了生成质量。
- **实验充分**：在单语和双语多个数据集上进行了全面的定量与定性评估，消融实验覆盖所有关键组件，可视化直观展示优势。
- **结果显著**：在六个基准数据集上均达到SOTA，特别是在少样本训练条件下提升幅度较大，具有实际应用价值。

## 8. 不足与局限
- **算力开销未量化**：未报告训练时间、推理成本，难以评估实际部署的计算需求。
- **生成质量依赖LLM**：LLM生成可能存在幻觉或遗漏，虽有过滤机制但仍可能引入错误信息；不同LLM效果好，论文未提供对不同LLM（如GPT-4、Llama）的对比实验。
- **评估指标有限**：仅使用MRR、Hits@1、Hits@10，未使用更细粒度的对齐准确率或检索任务评测。
- **应用场景限制**：方法要求两个KG使用相同的实体/关系候选池，且假设LLM的通用知识可以覆盖缺失信息，对于高度领域特异性的知识图谱（如医疗、金融）可能效果有限。
- **公平性考虑**：对比方法中部分未公开代码，运行结果可能因复现差异而略有偏差；论文未提供开源代码，可复现性待验证。

（完）
