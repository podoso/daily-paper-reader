---
title: Structure-Aware Zero-Shot Relational Learning for Knowledge Graphs without External Knowledge
title_zh: 无外部知识的知识图谱结构感知零样本关系学习
authors: "Kuan Xu, Baoxin Zhang, Shuyue Fan, Ming Chen, Zhipeng Ke, Jian Yu (于剑), Xuezhong Zhou"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.941.pdf"
tags: ["query:ie"]
score: 7.0
evidence: 利用结构模式进行知识图谱零样本关系学习
tldr: 零样本关系学习通常依赖外部知识。本文提出SAZRL，仅利用KG内在结构模式为新关系构建条件查询图，并通过自适应关系更新模块生成表示。在多个KG补全基准上，无需外部知识即达到有监督竞争水平，拓展了零样本关系学习的实用性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.941/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.941/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.941/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.941/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1651, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.941/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 731, \"height\": 496, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.941/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.941/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1655, \"height\": 753, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.941/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 725, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.941/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1651, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.941/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 761, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.941/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1647, \"height\": 277, \"label\": \"Table\"}]"
motivation: 现有零样本关系学习依赖外部知识，代价高且泛化有限。
method: 利用KG内在结构模式，通过共享实体构建条件查询图并自适应更新关系表示。
result: 无需外部知识即在多个KG上达到与有监督方法可比的性能。
conclusion: 结构感知方法有效实现无外部知识的零样本关系学习。
---

## Abstract
Zero-shot Relational Learning (ZRL) aims to perform knowledge graph completion when dealing with newly emerging relations without instances of them. However, existing ZRL methods typically depend on external knowledge beyond Knowledge Graphs (KGs), resulting in increased annotation costs and limited practical applicability. To address this issue, we propose a new **S**tructure-**A**ware paradigm for **ZRL**, termed **SAZRL**, that performs ZRL without relying on external knowledge. SAZRL leverages intrinsic structural patterns in KGs to bridge semantic correlations for new relations with existing ones. It constructs structure-aware conditional query graphs based on shared entities and adaptive relation updating module to generate representations for new relations based on the query graphs. We conduct extensive experiments on three real-world benchmarks, **NELL-ZS**, **Wiki-ZS** and **FB15K-ZS**, demonstrating that SAZRL consistently surpasses state-of-the-art ZRL methods, achieving up to **10.66%** improvement in **MRR** while reducing annotation costs and enhancing practical applicability. **The code and data are provided in supplementary materials.**

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：知识图谱（KG）广泛用于药物重定位、推荐系统等任务，但现有KG往往不完整。知识图谱补全（KGC）旨在预测缺失实体，但现有方法难以处理**新出现的（未见过的）关系**。重新收集实例并重训练成本高昂，因此零样本关系学习（Zero-shot Relational Learning, ZRL）被提出，目标是在没有训练实例的情况下推断涉及新关系的事实。
- **现有ZRL的局限**：当前ZRL方法（如文本驱动、本体驱动、专家引导）均依赖外部知识（如文本描述、本体模式、专家标注），这些资源获取成本高，且在实际场景中常不可得。**核心问题**：能否仅利用KG自身的结构模式（而不依赖任何外部知识）来实现有效的零样本关系学习？
- **本文贡献**：提出**SAZRL**（Structure-Aware Zero-shot Relational Learning），首次在**无外部知识**的条件下实现了与有监督方法可比的零样本关系学习性能，显著降低了标注成本并增强了实用性。

## 2. 方法论：核心思想与技术细节

### 2.1 核心思想
- 语义上相关的关系往往共享相同的实体集合（聚类效应）。因此，可以通过KG中实体共享的模式来捕捉关系间的语义相关性，从而为未见关系生成合理的表示，无需外部辅助信息。

### 2.2 方法架构（三个模块）

1. **结构感知条件查询图（Conditional Query Graph, CQG）构建**  
   - 给定一个查询对（如 (h, r_unseen, ?) 或 (?, r_unseen, t)），从背景KG中提取以查询实体为中心的二跳邻居子图。  
   - 基于子图中实体与关系的共现频率，为每个查询关系构建一个**加权关系图**，节点为关系，边权为语义相似度（采用共现归一化，也可用Jaccard或PPMI）。  
   - 该图直接编码了未见关系与已知关系之间的邻近性。

2. **自适应关系更新（Adaptive Relation Updating, ARU）模块**  
   - 对每个关系（包含未见和可见）初始化特征向量。  
   - 通过多层GAT（图注意力网络）将未见关系的表示聚合其邻域中可见关系的表示。  
   - 注意力权重由两部分组成：  
     - 基于关系对隐藏特征的交互项（使用LeakyReLU激活和可学习参数）。  
     - 基于关系相似度排序的**全局偏差**项（将相似度离散化为B个桶，每个桶对应一个可学习的标量偏移），以捕捉图全局结构特征。  
   - 采用残差连接和投影矩阵得到最终关系嵌入。

3. **关系-实体交互建模**  
   - 使用基于对角矩阵的乘积评分函数：`f(e_i, r_k, e_j) = v_i^T diag(z_k) v_j`。  
   - 采用带自对抗负采样的对数似然损失函数优化模型，最大化正三元组的得分，最小化负三元组的得分。

### 2.3 训练与推理流程
- 训练阶段：将可见关系三元组随机划分为训练集（模拟未见）和背景KG，为每个模拟未见关系构建CQG，通过ARU生成其表示，并利用交互损失训练参数。  
- 推理阶段：仅使用查询实体和背景KG构建CQG，生成未见关系表示，然后对候选实体进行排序。

## 3. 实验设计

### 3.1 数据集与基准
- **三个公开数据集**：  
  - **NELL-ZS**：65,567实体，139种可见关系+32种测试未见关系。  
  - **Wiki-ZS**：605,812实体，469种可见关系+48种测试未见关系。  
  - **FB15K-ZS**（新构建）：10,399实体，191种可见关系+21种测试未见关系，**无任何外部知识**。  
- **评估指标**：MRR、Hits@1、Hits@5、Hits@10。

### 3.2 对比方法
- 经典KGE的ZRL变体：ZS-TransE、ZS-DistMult、ZS-ComplEx。  
- 文本方法：ZSGAN、CZRL。  
- 本体方法：OntoZSL、DOZSL（含4种变体）。  
- 专家引导方法：FZR（含TransE和DistMult两种预训练变体）。  
- 其他GNN方法：RGAT、DisenE、DisenKGAT（与GAN或GCN组合）。  
- **共18种以上基线方法**。

### 3.3 实验结果
- 在NELL-ZS上：SAZRL MRR=0.270，相比最优基线提升**10.66%**。  
- 在Wiki-ZS上：MRR=0.217，提升**4.33%**。  
- 在FB15K-ZS上：SAZRL显著优于所有基线（因其他方法无法运行或性能极低），MRR=0.152，提升**360%**。  
- **消融实验**：验证了每个组件（CQG、子图扩展、全局偏差、注意力聚合）的必要性。  
- **稀疏性分析**：固定共享实体数量或邻居关系数量，观察性能变化，验证了聚类效应假设。  
- **案例研究**：通过t-SNE可视化及语义分析，展示了SAZRL能正确找到与未见关系最相似的已知关系（如“Wife of”关联到“Has spouse”“Mother of person”等）。

## 4. 资源与算力
- 原文明确说明：所有实验在配备**NVIDIA RTX 3090 GPU（24GB RAM）** 的Linux服务器上进行。  
- **未明确说明**：训练总时长、具体使用了几块GPU、批大小等细节，仅提及每个epoch随机抽取500/3000个负样本等超参数配置。

## 5. 实验数量与充分性
- **实验数量充足**：覆盖三个数据集，对比了18种以上基线，每个基线条目均报告四个指标。  
- **消融实验全面**：分别去掉CQG、子图扩展、全局偏差、替换为求和/平均聚合，共5种消融设置。  
- **额外分析充分**：包括结构稀疏性实验（变化共享实体数、邻居关系数）、不同相似度度量对比（CS、JS、PPMI）以及案例分析+可视化。  
- **公平性**：对基线方法使用了其最优超参数（如FZR的调参），并统一在相同环境下重跑；代码与数据公开。  
- **总体评价**：实验设计严谨、充分，验证了方法各组件贡献及鲁棒性。

## 6. 主要结论与发现
- 仅利用KG结构模式（实体共享）即可有效实现零样本关系学习，完全摆脱对外部知识的依赖。  
- 条件查询图能够捕捉关系间的局部语义相关性，自适应注意力机制能有效聚合邻域信息。  
- 共享实体数量即使较少（如1个）也能获得较好性能，体现了关系聚类的强先验。  
- 方法在多个数据集上均显著优于现有依赖外部知识的ZRL方法，特别是在无外部知识场景（FB15K-ZS）下优势巨大。

## 7. 优点
- **首创性**：首次提出无需任何外部知识（文本、本体、专家标注）的ZRL范式，拓宽了方法适用范围。  
- **结构精巧**：CQG+ARU设计充分利用了KG固有结构，既简单又高效，可解释性强（案例分析清晰）。  
- **实验充分公正**：涵盖流行基线、多种消融、稀疏性分析、多种相似度量对比，代码开源，可复现。  
- **实用性强**：降低实际部署成本，尤其适用于缺乏丰富注释的工业KG。

## 8. 不足与局限
- **数据稀疏性**：若未见关系与任何可见关系没有共享实体（例如孤立关系），则CQG无法捕捉可靠相关性，性能会显著下降。  
- **对KG质量的依赖**：KG中可能含有噪音（假阳性或假阴性事实），结构模式可能被扭曲，影响推理准确性。  
- **未考虑未见实体**：当前工作在封闭实体假设下进行（所有实体在背景KG中已出现），未扩展到同时包含未见实体的更复杂场景。  
- **训练细节缺失**：论文未报告完整的训练时间、GPU数量、收敛速度等，可能影响在更大规模KG上的可扩展性评估。  
- **通用性局限**：仅测试了三个数据集（NELL、Wiki、FB15K-237），未涉及医疗、金融等特殊领域KG。

（完）
