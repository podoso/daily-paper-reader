---
title: "UniRel-R1: RL-tuned LLM Reasoning for Knowledge Graph Relational Question Answering"
title_zh: "UniRel-R1: 强化学习调优的LLM推理用于知识图谱关系问答"
authors: "Yinxu Tang, Chengsong Huang, Jiaxin Huang, William Yeoh"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=LPhIQXgYmu"
tags: ["query:llm"]
score: 6.0
evidence: 强化学习调优LLM用于关系型知识图谱问答
tldr: 传统KGQA返回单一实体，但现实查询需要理解实体间关联。本文提出UniRel-R1，将子图选择、多阶段图剪枝与强化学习调优的LLM结合，聚焦关系为中心的问答。通过抑制平凡连接，在关系型KGQA任务上优于现有方法，展示了RL调优LLM在结构化推理中的潜力。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-lphiqxgymu/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1382, \"height\": 989, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lphiqxgymu/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1418, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lphiqxgymu/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1425, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lphiqxgymu/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 659, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lphiqxgymu/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 654, \"height\": 487, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1450, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1167, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1321, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1448, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 765, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1449, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lphiqxgymu/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1447, \"height\": 508, \"label\": \"Table\"}]"
motivation: 现有KGQA忽略关系型查询，且候选子图中平凡连接干扰结果。
method: 提出统一框架，结合子图选择、多阶段图剪枝和RL调优的LLM推理。
result: 在关系型KGQA任务上性能优于现有方法。
conclusion: RL调优的LLM能有效处理关系推理，提升KGQA质量。
---

## Abstract
Knowledge Graph Question Answering (KGQA) has traditionally focused on entity-centric queries that return a single answer entity. 
However, real-world queries are often relational, seeking to understand how entities are associated.
In this work, we introduce relation-centric KGQA, a complementary setting where the answer is a subgraph capturing the semantic connections among entities rather than an individual entity. 
The main challenge lies in the abundance of candidate subgraphs, where trivial or overly common connections often obscure the identification of unique and informative answers. 
To tackle this, we propose UniRel-R1, a unified framework that integrates subgraph selection, multi-stage graph pruning, and an LLM fine-tuned with reinforcement learning. The reward function is designed to encourage compact and specific subgraphs with more informative relations and lower-degree intermediate entities.
Extensive experiments show that UniRel-R1 achieves significant gains in connectivity and reward over Vanilla baselines and generalizes effectively to unseen entities and relations.

---

## 论文详细总结（自动生成）

# 论文总结：UniRel-R1: RL-tuned LLM Reasoning for Knowledge Graph Relational Question Answering

## 1. 论文的核心问题与整体含义（研究动机和背景）

传统知识图谱问答（KGQA）主要聚焦于**实体中心**的查询，即返回单个答案实体（例如“Meghan Markle的丈夫的祖母是谁？”回答“Queen Elizabeth II”）。然而，现实中的用户查询往往更关注**实体之间的关系**（例如“Meghan Markle和Queen Elizabeth II之间有什么关联？”），需要返回一个能够捕捉实体间语义连接的子图而非单个实体。这类**关系中心KGQA**在现有系统中尚未被充分探索。主要挑战在于：候选子图数量众多，其中平凡或过度常见的连接（如“性别”、“出生地”）往往掩盖了独特且富有信息量的答案。因此，论文旨在解决如何从海量候选子图中筛选出紧致、信息丰富的关系子图作为回答。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
提出**UniRel-R1**，一个统一框架，整合了**子图选择**、**多阶段图剪枝**和**强化学习调优的LLM**。通过设计奖励函数，鼓励生成紧致、特异性高（稀有关系和低度中间实体）的子图，压制平凡连接。

### 关键技术细节

#### （1）子图选择
- 从查询中提取种子实体集 \(E_q\)。
- 对每个种子实体进行k跳扩展，合并得到候选子图 \(G'\)（包括节点、边和关系类型）。

#### （2）多阶段图剪枝（Multi-Step Graph Pruning）
定义**中心惩罚（Hub Penalty）**：\( \text{HubPenalty}(e) = \log(1 + \deg(e)) \)，度数高的实体（如"male"）惩罚高，稀有实体惩罚低。

- **Stage 1: Local Pruning**：对每个扩展集，根据阈值 \(\rho\) 移除中心惩罚过高的非种子实体及其关联边，再移除孤立节点。
- **Stage 2: Connectivity Guarantee**：检查剪枝后各种子实体邻域是否连通；若不连通，则逐步放松阈值 \(\rho\) 并重复Stage1，直到连通。
- **Stage 3: Leaf Entity Pruning**：迭代移除邻居数仅为1的非种子实体及其边，直到无法再移除。
- **Stage 4: Compactness Control**：若子图仍太大，利用种子实体邻域的非空交集，选择中心惩罚最低的m个实体，再通过k跳扩展保留子图，进一步精简。
- **Stage 5: Iterative Reduction**：若子图仍大于目标尺寸，减小参数m并重复Stage4。

#### （3）关系答案生成 via RL-tuned LLM
- **RL算法**：使用**Group Relative Policy Optimization (GRPO)**，基于组内相对表现计算优势，用裁剪代理损失和KL散度正则项优化策略。
- **奖励设计（复合奖励，共四部分）**：
  - **格式奖励** \(R_{fmt}\)：输出格式正确为1，否则-1。
  - **连通性奖励** \(R_{con}\)：根据种子实体连通程度给出离散值（-⌊|Eq|/2⌋ 到 ⌈|Eq|/2⌉-1）。
  - **实体信息量奖励** \(R_{ent}\)：基于负的归一化中心惩罚，鼓励低度实体。
  - **关系信息量奖励** \(R_{rel}\)：基于负的归一化逆文档频率（IDF），鼓励稀有关系。
  - **总奖励**：\( R(a) = R_{fmt} + R_{con} + \frac{1}{2}(R_{ent}/x + R_{rel}/y) \)，其中x,y为归一化常数（实验设定x=7, y=6）。

#### 流程总结
查询 → 种子实体提取 → k跳子图选择 → 多阶段剪枝（包含连通性保证）→ 剪枝后子图文本化 → RL-tuned LLM根据查询和子图生成答案 → 奖励信号反馈训练。

## 3. 实验设计

### 数据集
使用7个基准KG数据集，涵盖百科、生物医学、常识等领域：
- Freebase13, FB15k-237, MetaQA, DBpedia50, DBpedia500, YAGO3-10, UMLS。

### 查询构造
- 每个数据集构建2500个关系中心查询（2000训练/500测试），主要是**双实体查询**（种子实体距离≤4）。
- 为评估可扩展性，在DBpedia50上额外构建**三实体和四实体查询**。

### 对比方法
- **Vanilla baseline**：使用相同LLM但未经RL调优的原始模型（直接基于提示生成）。
- **Optimal Reward**：通过穷举搜索得到的最优子图奖励上界。

### 模型
- Qwen-2.5系列：3B、7B、14B-Instruct
- Llama-3.2-3B-Instruct、Llama-3.1-8B-Instruct

### 评估指标
- **主要指标**：
  - **连通率（Connectivity Ratio, C）**：生成子图连接所有种子实体的查询比例。
  - **平均奖励（Average Reward, \(\bar{R}\)）**：综合奖励均值。
- **辅助指标**：格式正确率、实体信息量平均分、关系信息量平均分。

## 4. 资源与算力

论文**未明确说明**使用的GPU型号、数量及训练时长。仅在附录中列出了超参数（如全局batch size=64，学习率1e-6，20个epochs（双实体）、40个epochs（多实体）等），但未提及具体硬件配置。因此，无法评估计算成本。

## 5. 实验数量与充分性

### 实验数量
- **主实验**：5个模型 × 7个数据集 × 2种方法（Vanilla vs UniRel-R1） = 70组对比结果，每个结果报告(C, \(\bar{R}\))。
- **泛化实验**：模型在DBpedia500上训练后，直接测试在其余6个数据集上（包括原始和“修改版”——实体/关系替换为随机标识符），共 5模型 × 6数据集 × 2变体 = 60组结果。
- **渐进修改实验**：在MetaQA上以25%、50%、75%、100%比例替换实体/关系为随机标识符，观察性能变化，5模型，4比例，共20组。
- **可扩展性实验**：DBpedia50上三实体和四实体查询，5模型 × 2方法 = 10组（含详细连通级别）。

### 充分性与公平性
- **充分性**：跨越7个不同规模、领域的KG，覆盖两大模型家族、多种参数规模，并设计多实体场景验证可扩展性。消融方面（如无剪枝、无RL等）未明确报告，但通过对比Vanilla和Optimal Reward，间接体现了各组件贡献。
- **公平性**：超参数（x,y）在DBpedia500上固定后统一应用于所有实验，避免了过拟合。Vanilla与UniRel-R1使用相同提示模板，仅训练方式不同。但未与已有关系问答方法（如路径查询）直接比较，因为论文声称该任务是全新的，故缺乏外部对比基线。

## 6. 论文的主要结论与发现

1. **主要效果**：UniRel-R1在所有数据集上**一致优于Vanilla**，连通率至少提升35%，平均奖励至少提升245%。
2. **模型规模影响**：更大的模型（Qwen-14B、Llama-8B）在Vanilla和UniRel-R1下均表现更好，RL进一步放大了容量优势。
3. **泛化能力**：在DBpedia500上训练的模型能有效迁移到其他数据集（未见过的实体/关系），跨域泛化能力强。
4. **语义依赖差异性**：Qwen模型对语义信息高度敏感，移除语义（替换为随机标识符）导致性能大幅下降；Llama模型更多依赖结构连通性，受影响较小。
5. **可扩展性**：框架能自然扩展到三实体、四实体查询，Llama模型在多实体场景下表现更优。
6. **格式遵守**：RL训练后，几乎所有模型都达到100%格式正确率，而Vanilla中Llama模型格式正确率极低（<5%）。

## 7. 优点

- **问题新颖**：正式定义了“关系中心KGQA”这一被忽视但实际重要的任务。
- **方法设计精巧**：多阶段剪枝结合中心惩罚和连通性保证，有效筛选出信息量高的子图；复合奖励函数平衡了格式、连通、实体和关系信息量。
- **实验全面**：覆盖7个KG、2个模型家族、多种参数规模、跨域泛化、多实体扩展，结论稳健。
- **分析深入**：揭示了Qwen和Llama在依赖语义 vs. 结构上的本质差异，对模型选择有指导意义。
- **可复现**：提供了详细的超参数、提示模板、采样算法和数据集统计，附录清晰。

## 8. 不足与局限

- **缺乏外部基准对比**：由于任务新定义，未与任何已有方法（如基于路径搜索的KGQA、GNN+LLM方法）直接比较，仅对比了Vanilla，说服力受限。
- **算力信息缺失**：未报告GPU型号、数量、训练时间，社区难以评估成本与可复现性。
- **消融实验不完整**：未单独分析剪枝各阶段或奖励各分量的贡献，仅通过完整框架与Vanilla对比，组件贡献无法量化。
- **实验设置局限**：查询距离限制在≤4跳，未探索更远距离；仅测试了文本化子图输入，未对比其他输入形式（如纯文本描述）。
- **泛化实验偏差**：泛化测试中“修改版”数据集只能消除语义，但结构仍与原始相同，可能低估了语义依赖差异的实际影响。
- **应用限制**：依赖预定义的KG和种子实体提取（论文未深入探讨实体链接），实际应用中实体提取会引入额外误差。

（完）
