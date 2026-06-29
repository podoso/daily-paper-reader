---
title: "HYPER: A Foundation Model for Inductive Link Prediction with Knowledge Hypergraphs"
title_zh: HYPER：面向知识超图归纳链接预测的基础模型
authors: "Xingyue Huang, Mikhail Galkin, Michael M. Bronstein, Ismail Ilkan Ceylan"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=YLTQbMoAaX"
tags: ["query:ie"]
score: 4.0
evidence: 知识超图归纳链接预测，支持新实体和新关系
tldr: 现有归纳链接预测方法无法处理新关系类型。本文提出HYPER基础模型，通过编码实体角色和关系类型，泛化到任意知识超图，包括新实体和新关系。在多个数据集上超越现有方法。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 477, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 432, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 754, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1416, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 364, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-yltqbmoaax/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1433, \"height\": 377, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 744, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1450, \"height\": 824, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 712, \"height\": 1040, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 479, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1412, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1246, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 939, \"height\": 2310, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1377, \"height\": 777, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1220, \"height\": 776, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1308, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 637, \"height\": 653, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1455, \"height\": 634, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1427, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1386, \"height\": 717, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 878, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1427, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1443, \"height\": 812, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1464, \"height\": 798, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1449, \"height\": 1421, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1450, \"height\": 1421, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1391, \"height\": 981, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1124, \"height\": 1415, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yltqbmoaax/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1236, \"height\": 941, \"label\": \"Table\"}]"
motivation: 归纳链接预测需要泛化到新实体和新关系类型。
method: 提出HYPER基础模型，编码实体角色和关系类型实现跨关系泛化。
result: 在多个知识超图基准上取得最优性能。
conclusion: HYPER为知识超图归纳链接预测提供了基础模型解决方案。
---

## Abstract
Inductive link prediction with knowledge hypergraphs is the task of predicting missing hyperedges involving completely *novel entities* (i.e., nodes unseen during training). Existing methods for inductive link prediction with knowledge hypergraphs assume a fixed relational vocabulary and, as a result, cannot generalize to knowledge hypergraphs with *novel relation types* (i.e., relations unseen during training). Inspired by knowledge graph foundation models, we propose HYPER as a foundation model for link prediction, which can generalize to *any knowledge hypergraph*, including novel entities and novel relations. Importantly, HYPER can learn and transfer across different relation types of *varying arities*, by encoding the entities of each hyperedge along with their respective positions in the hyperedge. To evaluate HYPER, we construct 16 new inductive datasets from existing knowledge hypergraphs, covering a diverse range of relation types of varying arities. Empirically, HYPER consistently outperforms all existing methods in both node-only and node-and-relation inductive settings, showing strong generalization to unseen, higher-arity relational structures.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：知识超图（Knowledge Hypergraphs）能够表示任意元数的关系（如四元关系"Research(Bengio, ClimateAI, Montreal, CIFAR)"），这对链接预测提出了更高要求。现有归纳链接预测方法（如G-MPNN、HCNet）虽然能处理新实体（节点），但**假设关系词汇固定，无法泛化到训练中从未见过的新关系类型**。
- **核心问题**：如何设计一个基础模型，使其在测试时能同时处理**新实体和新关系**（包括不同元数的高阶关系），实现零样本迁移。
- **整体含义**：HYPER是首个面向知识超图的**基础模型**，可以在任意知识超图（包括新实体、新关系、任意元数）上进行零样本归纳链接预测，填补了该领域的空白。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：学习关系之间可迁移的**位置交互模式**，将关系泛化问题转化为对“关系图”的学习，利用关系间共享的结构信息（如实体在同一位置出现）进行迁移。
- **技术细节（三步流程）**：
  1. **构建关系图（Relation Graph）**：给定知识超图 \( G=(V,E,R) \)，构造关系图 \( G_{rel} \)，其中每个节点对应一个关系类型；若两个超边共享实体且分别出现在关系 \( r_1 \) 的位置 \( i \) 和关系 \( r_2 \) 的位置 \( j \)，则在 \( r_1 \) 和 \( r_2 \) 之间添加一条带标签 \( (i,j) \) 的边。该图捕获关系间的位置交互。
  2. **编码位置交互**：对每个位置对 \( (a,b) \)，使用**正弦位置编码 + 共享MLP** 计算嵌入 \( x_{a,b} = \text{MLP}([p_a \| p_b]) \)。该方法满足**外推性**（可泛化到未见位置对）和**单射性**（不同位置对映射到不同嵌入），且具有有界性和Lipschitz光滑性。
  3. **关系编码器与实体编码器**：关系编码器在 \( G_{rel} \) 上运行**条件消息传递（HCNet）**，以查询关系为条件更新所有关系表示；实体编码器在原始知识超图上运行另一个HCNet，利用关系编码器输出的关系嵌入进行消息聚合，最终通过解码器输出链接概率。
- **公式与算法**（文字说明）：
  - 关系编码器每一层：\( h^{(t+1)}_{r|q} = \text{UP}\big( h^{(t)}_{r|q}, \text{AGG}\{\text{MSG}_{(a,b)}(\cdot)\} \big) \)，其中消息由位置交互嵌入 \( x_{a,b} \) 调制。
  - 实体编码器类似，但消息中融入了关系嵌入（由关系编码器输出）和位置编码。
  - 训练采用自对抗负采样损失（self-adversarial negative sampling）。

## 3. 实验设计：数据集、基准场景、对比方法

- **数据集**：
  - **新构建的16个节点-关系归纳数据集**：来自 JF17K、WikiPeople (WP)、M-FB15K (MFB)、WD50K（超关系KG转换而来）。每个源数据集按**不同比例（25%、50%、75%、100%）**包含测试元组中未见关系的比例。
  - **已有3个节点归纳数据集**：JF-IND、WP-IND、MFB-IND。
  - **补充实验**：标准知识图谱基准（如FB15k-237、WN18RR、GraIL、INDIGO、ILPC等），用于评估HYPER在二元关系上的性能。
- **基准场景**：
  - **端到端训练**（在目标训练集上训练）。
  - **零样本推理**（预训练后直接在测试超图上评估，未见任何训练数据）。
  - **微调推理**（先预训练，再在目标训练集上微调）。
- **对比方法**：
  - **知识超图方法**：G-MPNN、RD-MPNN、HCNet、HyperGCN等（端到端）。
  - **知识图谱基础模型（KGFM）**：ULTRA（训练于3/4/50个KG）、KG-ICL；通过**实体化（reification）**将超图转为KG后应用。
  - **HYPER变种**：HYPER(3KG/4KG/50KG/4HG/3KG+2HG)，分别在不同预训练混合数据上训练（混合KG和超图）。
- **评估指标**：过滤排名协议下的MRR、Hits@K。

## 4. 资源与算力

- 论文明确说明了计算资源：
  - **预训练**：单张NVIDIA H100 80GB，耗时约4天。
  - **其余实验（微调、端到端训练）**：单张NVIDIA A10 24GB，耗时一般少于3小时。
  - 实现基于PyTorch和PyTorch Geometric，核心超图消息传递使用**自定义Triton内核**优化，将内存复杂度从 \( O(k|E|) \) 降至 \( O(|V|) \)，训练时间减半，内存节省约5倍。
- 总体算力需求属于中等水平，在单GPU上可完成。

## 5. 实验数量与充分性

- **实验数量**：
  - 节点-关系归纳：16个数据集（4个源×4种比例）×多种模型变种 → 大量比较。
  - 节点归纳：3个标准数据集。
  - 知识图谱归纳：23个数据集（13个节点-关系 + 12个节点仅）。
  - 消融实验：位置交互编码器的不同方案（全一、随机、幅值、正弦）；位置扰动弹窗实验（50%超边随机排列位置）。
  - 超参数敏感性：报告了学习率、层数等（附录G.4-G.5）。
- **充分性与客观性**：
  - 对比了当前最强的方法，包括监督的（HyperGCN、G-MPNN、HCNet）和零样本的（ULTRA、KG-ICL）。
  - 公平性：对ULTRA等KGFM在实体化超图上进行了相同预训练混合的对比（ULTRA†, ULTRA‡两种实体化方式），同时进行了微调对比。
  - 报告了多次运行的平均值和标准差（部分表如Table 19-21中有 ± 值）。
  - 覆盖了多种比例未见关系，系统性评估难度递增。
  - 不足：没有与更多超图基础模型（如Hyper-FM、IHP）对比，但这些模型不适用于链接预测任务；实验仅在英文数据集上，未考虑跨语言或带文本属性的超图。

## 6. 论文的主要结论与发现

- HYPER在所有节点-关系归纳超图数据集上**显著优于**现有端到端方法和KGFM（ULTRA）。
- 在节点归纳设置中，HYPER（零样本/微调）也**超越**HCNet等最强基线。
- 当测试集中未见关系比例增高时，现有方法性能急剧下降，而HYPER**保持稳定强性能**。
- **位置交互编码器的选择至关重要**：正弦编码（单射+有界+外推）远优于全一、随机、幅值编码。
- **预训练混合多样性增强泛化**：混合KG和超图（3KG+2HG）优于仅KG或仅超图预训练。
- 实体化KGFM（ULTRA）在超图上表现不佳，因为实体化破坏了结构（三部分图、辅助节点增加跳数），HYPER直接处理超图结构更优。
- 在标准知识图谱任务上，HYPER性能与ULTRA相当（略低），证明其设计可同时适应二元和高阶关系。

## 7. 优点（方法或实验设计亮点）

- **首次实现**知识超图上完全泛化（新实体+新关系+任意元数）的基础模型。
- **巧妙的泛化机制**：通过关系图编码关系间的位置交互模式，将关系级泛化转化为图结构学习，避免了为每个关系分配独立嵌入。
- **位置交互编码器的理论保证**：单射性、有界性、Lipschitz光滑性，确保对不同元数的外推。
- **全面的实验设计**：构建16个不同比例的新数据集，系统评估难度；引入实体化和不同预训练混合对比，消融彻底。
- **高效实现**：使用Triton内核优化消息传递，大幅降低内存和加速。
- **指标和结果可信**：报告标准差，多次运行。

## 8. 不足与局限

- **计算复杂度**：位置交互数量随关系元数平方增长（\( O(k^2) \)），对于极高元数（如WD50K出现22元）可能成为瓶颈。论文本身提到这是主要局限。
- **在标准知识图谱上性能略逊于ULTRA**：虽然HYPER能处理超图，但在纯二元关系任务上不如专门优化的KGFM，未来需要弥合差距。
- **依赖关系图构建**：关系图的质量依赖于超图中实体共享的丰富性，若测试超图与训练超图的结构差异极大（例如所有关系之间无任何共享实体），泛化可能受限。
- **实验覆盖不足**：未在文本属性超图或含噪声的真实世界超图上测试；未与基于语言模型的方法（如HyperBERT）比较（因任务不同）。
- **潜在偏差风险**：知识超图本身可能包含社会偏见，模型可能学习到不公平的连接模式，但论文伦理声明中已提及这一点。
- **应用限制**：当前框架需要将超图视为完全结构化的，对动态变化或流式超图适应能力未研究。

（完）
