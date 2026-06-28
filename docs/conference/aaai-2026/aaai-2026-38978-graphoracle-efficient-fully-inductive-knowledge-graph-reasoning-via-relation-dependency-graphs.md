---
title: "GraphOracle: Efficient Fully-Inductive Knowledge Graph Reasoning via Relation-Dependency Graphs"
title_zh: GraphOracle：通过关系依赖图实现高效全归纳知识图谱推理
authors: "Enjun Du, Siyi Liu, Yongqi Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38978/42940"
tags: ["query:ie"]
score: 5.0
evidence: 关注知识图谱中的关系抽取推理
tldr: 本文提出GraphOracle框架，将知识图谱转换为关系依赖图，通过多头注意力机制学习关系嵌入，实现全归纳设置下的关系推理。该方法能处理训练时未见过的实体和关系，显著提升关系抽取的泛化能力。实验证明GraphOracle在多个推理基准上达到最优性能，为关系抽取和知识图谱推理提供了新范式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 全归纳知识图谱推理中关系与实体均未见，现有方法难以捕捉关系间的组合模式。
method: 将知识图谱转换为关系依赖图，利用多头注意力学习关系感知嵌入并指导消息传递。
result: 在多个全归纳推理数据集上取得最优结果，且推理效率高。
conclusion: 为处理开放世界中的关系抽取提供了可扩展的归纳推理方法。
---

## Abstract
Knowledge graph reasoning in the fully-inductive setting—where both entities and relations at test time are unseen during training—remains an open challenge. In this work, we introduce GraphOracle, a novel framework that achieves robust fully-inductive reasoning by transforming each knowledge graph into a Relation-Dependency Graph (RDG). The RDG encodes directed precedence links between relations, capturing essential compositional patterns while drastically reducing graph density. Conditioned on a query relation, a multi-head attention mechanism propagates information over the RDG to produce context-aware relation embeddings. These embeddings then guide a second GNN to perform inductive message passing over the original knowledge graph, enabling prediction on entirely new entities and relations. Comprehensive experiments on 60 benchmarks demonstrate that GraphOracle outperforms prior methods by up to 25% in fully-inductive and 28% in cross-domain scenarios. Our analysis further confirms that the compact RDG structure and attention-based propagation are key to efficient and accurate generalization

---

## 论文详细总结（自动生成）

# 中文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：知识图谱（KG）推理的核心是链接预测，而最困难的场景是**全归纳（fully-inductive）设置**——测试时实体和关系均未在训练中出现。现有方法（如INGRAM、ULTRA）通过构建关系图来捕获关系依赖，但存在两个局限：
  - 依赖共现统计导致关系图稠密（边数达 |R|²），计算成本高且引入噪声，缺乏方向性。
  - 每个关系只用一个固定嵌入，无法适应不同查询上下文（例如“associated with”在不同领域语义不同）。
- **整体含义**：需要一种既高效又能捕捉关系间有向组合模式、且能为每个查询动态生成关系嵌入的框架，从而实现跨知识图谱的零样本泛化。

## 2. 方法论

- **核心思想**：将知识图谱转换为**关系依赖图（Relation-Dependency Graph, RDG）**，通过有向优先边编码关系间的组合模式，再基于查询关系用多头注意力机制在RDG上传播信息，获得上下文感知的关系嵌入，最后用这些嵌入指导原始KG上的GNN消息传递进行预测。
- **关键技术细节**：
  - **RDG构建**：提取KG中所有两跳路径 (e, r_i, e') 和 (e', r_j, e'') 得到关系对 (r_i, r_j)，作为有向边。通过拓扑排序定义部分顺序函数 τ，使得关系图中的边从低τ指向高τ，形成有向无环结构。每个关系r_v的过去邻居集合 N_past(r_v) 只包含τ更小的关系。
  - **关系表示学习**：对查询关系r_q，初始化指示向量。使用多头注意力在RDG上迭代传播（公式4），注意力权重由源节点和目标节点表示拼接后经线性层和softmax计算。经过L_r层后得到每个关系的最终表示 h^{L_r}_{r|r_q}。
  - **实体表示学习**：在原始KG上，用得到的上下文关系嵌入代替固定关系嵌入，按公式(1)进行GNN消息传递，注意力权重同时考虑源节点、关系嵌入和查询关系嵌入。最终打分计算。
- **训练范式**：多数据集顺序预训练（NELL-995, CoDEx-Medium, FB15k-237）→ 微调（仅1~2个epoch）。零样本推理可直接应用预训练模型。

## 3. 实验设计

- **数据集与场景**：
  - **归纳和直推基准**：使用与ULTRA、TRIX、KG-ICL相同的设置，共57个数据集（16个直推、18个实体归纳、23个全归纳）。
  - **跨域数据集**：
    - 生物医学：PrimeKG（蛋白质-疾病、药物-适应症等）。
    - 推荐：Amazon-book转化为KG推理格式。
    - 地理：GeoNames。
- **Benchmark与对比方法**：
  - 对比大量基线，包括：
    - 直推：ConvE, QuatE, DuASE, BioBRIDGE。
    - 实体归纳：MINERVA, DRUM, AnyBURL, RNNLogic, RLogic, GraphRulRL, CompGCN, NBFNet, RED-GNN, A*Net, Adaprop, one-shot-subgraph。
    - 全归纳：INGRAM, ULTRA, TRIX, KG-ICL。
  - 采用标准指标：MRR, H@1, H@10。

## 4. 资源与算力

- **预训练**：在单个A6000（48GB）GPU上运行，150,000步，batch size 32，使用AdamW优化器，耗时约**36小时**。
- **微调**：仅1~2个epoch，耗时**15~60分钟**（取决于目标数据集大小）。
- 论文未明确说明总共消耗的GPU数量，但所有实验应在单卡或少数卡上完成。

## 5. 实验数量与充分性

- **数量**：共60个不同知识图谱（57个标准归纳/直推+3个跨域专用数据集），涵盖多种规模和领域。
- **充分性**：实验设计较充分，包括：
  - 主实验对比4种设置下的SOTA（表2）。
  - 消融实验（表3）分析RDG、多头注意力、以及替换为INGRAM/ULTRA的图构建和消息传递的影响。
  - 扰动分析（图2）验证RDG中注意权重高的边的重要性。
  - 预训练数据数量影响分析（图3）。
  - 外部信息增强实验（图4）。
- **公平性**：对比方法结果来自原始论文或官方代码复现，设置一致；评估指标标准。但在跨域场景中仅测试了三个领域，可能不足以证明在所有跨域任务上的普适性。

## 6. 主要结论与发现

- GraphOracle在所有60个数据集上均一致超越SOTA，全归纳设置下MRR提升25%，H@1提升25.36%。
- RDG的有向优先结构和多头注意力是性能提升的关键；去掉RDG或注意力均导致显著下降。
- 零样本性能在预训练3个多样数据集后饱和，增加更多数据集无显著收益。
- 外部信息（如基础模型嵌入）可进一步提升性能（GraphOracle+），在PrimeKG上MRR提升最高15%。

## 7. 优点

- **方法创新性**：首次提出有向关系依赖图，捕获关系间的组合模式而非共现统计，边数大大减少且方向明确。
- **动态关系嵌入**：根据查询关系生成上下文感知的关系表示，解决固定嵌入无法适应多语义的问题。
- **高效性**：RDG紧凑（|E_R| 远小于 |R|²），预训练后仅需极短微调即可适应新域。
- **实验全面性**：在60个基准上验证，涵盖直推、归纳、全归纳、跨域多种设置，消融和扰动分析有力支撑设计有效性。

## 8. 不足与局限

- **RDG构建依赖拓扑排序**：若KG中存在循环依赖或关系层次不清晰，可能无法正确建立有向边，影响性能。
- **实验覆盖有限**：跨域仅测试了生物医学、推荐、地理三个领域，未能检验在更多领域（如金融、法律）的泛化能力。
- **偏差风险**：预训练数据只有三个通用KG，可能偏向这些图的分布，在分布差异极大的新KG上零样本表现可能下降。
- **算力资源**：预训练需36小时，尽管微调快，但对资源有限的研究者仍有一定门槛。
- **未比较与LLM结合的方法**：论文未讨论与当前大语言模型增强的知识图谱推理方法（如KG-ICL虽作为基线，但未深入分析）的优劣。

（完）
