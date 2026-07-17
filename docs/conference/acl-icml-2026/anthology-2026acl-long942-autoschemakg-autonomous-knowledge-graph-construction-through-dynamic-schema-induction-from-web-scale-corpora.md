---
title: "AutoSchemaKG: Autonomous Knowledge Graph Construction through Dynamic Schema Induction from Web-Scale Corpora"
title_zh: AutoSchemaKG：通过大规模语料库动态模式归纳实现自主知识图谱构建
authors: "Jiaxin Bai, Wei Fan, Qi Hu, Qing Zong, Chunyang Li, Hong Ting Tsang, Hongyu Luo, Yauwai Yim, Haoyu Huang, Xiao Zhou, Feng Qin, Tianshi Zheng, Xi Peng, Xin Yao, Huiwen Yang, Leijie Wu, JI Yi, Gong Zhang, Renhai Chen, Yangqiu Song"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.942.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 自主知识图谱构建，同时抽取三元组并归纳模式
tldr: "现有知识图谱构建依赖预定义模式，限制了扩展性。本文提出AutoSchemaKG，利用大语言模型从海量文本中同时抽取知识三元组并动态归纳模式，构建包含5.9B边的大规模知识图谱ATLAS。实验表明，该方案在多跳问答和LLM事实性提升上超越已有基准，模式归纳准确率达92%。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.942/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.942/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 768, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.942/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 643, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.942/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 772, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.942/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1199, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.942/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1331, \"height\": 508, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1560, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 801, \"height\": 772, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 680, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 912, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 804, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 508, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 801, \"height\": 1463, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 766, \"height\": 813, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1563, \"height\": 1095, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 796, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 797, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1609, \"height\": 1019, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1649, \"height\": 749, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1662, \"height\": 1050, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.942/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1654, \"height\": 1025, \"label\": \"Table\"}]"
motivation: 消除知识图谱构建对预定义模式的依赖，实现全自动模式归纳。
method: 利用大语言模型同时抽取实体和事件三元组，并通过概念化组织实例诱导模式。
result: "处理50M文档，构建90亿节点、59亿边的知识图谱ATLAS，多跳问答超越基线，模式归纳准确率92%。"
conclusion: 证明了大规模自动化模式归纳与知识图谱构建的有效性，提升了下游任务性能。
---

## Abstract
We present AutoSchemaKG, a framework for fully autonomous knowledge graph construction that eliminates the need for predefined schemas. Our system leverages large language models to simultaneously extract knowledge triples and induce comprehensive schemas directly from text, modeling both entities and events while employing conceptualization to organize instances into semantic categories. Processing over 50 million documents, we construct ATLAS (Automated Triple Linking And Schema induction), a family of knowledge graphs with 900+ million nodes and 5.9 billion edges. This approach outperforms state-of-the-art baselines on multi-hop QA tasks and enhances LLM factuality. Notably, our schema induction achieves 92% semantic alignment with human-crafted schemas with zero manual intervention, demonstrating that billion-scale knowledge graphs with dynamically induced schemas can effectively complement parametric knowledge in large language models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前知识图谱（KG）构建严重依赖领域专家预先定义的模式（schema），这从根本上限制了构建的可扩展性和领域覆盖率。如何让KG构建过程摆脱人工预定义模式的束缚，实现全自动、大规模的知识获取，是人工智能面临的一项重大挑战。
- **整体含义**：本文提出AutoSchemaKG，通过利用大语言模型（LLMs）同时从非结构化文本中抽取知识三元组（实体-实体、实体-事件、事件-事件）并动态归纳抽象模式（conceptualization），构建了包含超过9亿节点和59亿边的大规模知识图谱家族ATLAS。实验证明，这种带有自动归纳模式的知识图谱能够有效增强LLM在事实性和多跳推理任务上的表现，验证了大规模自动构建KG的价值。

## 2. 论文提出的方法论

- **核心思想**：以实体、事件和概念（concept）为核心要素，通过LLM驱动的多阶段流水线实现三元组抽取和模式归纳，最终构成带概念化模式的知识图谱`G = (V, E, C, φ, ψ)`，其中`V`为实体和事件节点，`E`为边（关系），`C`为概念集合，`φ`和`ψ`分别将节点和关系映射到概念子集。
- **关键技术细节**：
  - **三元组抽取**：对文档进行语言过滤、分块（不超过`C_max` token）和批次处理。分三个阶段：
    - 阶段1：用提示`P_EE`抽取实体-实体关系，输出`(e1, r, e2)`。
    - 阶段2：用提示`P_EV`抽取实体-事件关系，输出`(e, r, v)`或`(v, r, e)`。
    - 阶段3：用提示`P_VV`抽取事件-事件关系（时间/因果），输出`(v1, r, v2)`。
    - 所有输出以JSON格式解析，异常时返回空列表保持流水线连续。
  - **模式归纳（Schema Induction）**：对已抽取的实体、事件和关系分别用LLM生成至少3个抽象短语（1-2词），作为其类型或相关概念的表示。对实体，还通过采样邻居节点（最多`N_ctx`个）提供上下文以增强抽象准确性。生成结果构成概念集`C`和映射`φ`、`ψ`。
- **算法流程（文字说明）**：1）输入文档→过滤→分块→分批；2）批次送入LLM依次执行EE、EV、VV三段抽取，解析得到三元组列表；3）基于三元组构建图结构，然后对图中每个元素（实体、事件、关系）用LLM和上下文（实体时）生成抽象短语；4）将抽象短语作为概念节点连接原节点，完成带概念模式的KG构建。

## 3. 实验设计

- **使用的数据集/场景**：
  - **预训练语料**：Dolma 1.7（包含Wikipedia & Wikibooks、Semantic Scholar摘要、Common Crawl的3%），分别构建ATLAS-Wiki、ATLAS-Pes2o、ATLAS-CC。
  - **多跳QA基准**：MuSiQue、HotpotQA、2WikiMultihopQA（各随机1000题）。
  - **事实性基准**：FELM（847样本，4,425细粒度片段，覆盖世界知识、科学/技术、写作/推荐等域）。
  - **通用领域知识**：MMLU（按14个主题分组，重点分析知识密集型领域）。
- **对比的方法**：
  - **三元组抽取基线**：OpenIE 6、Stanford OIE。
  - **模式归纳基线**：Txt2onto。
  - **QA/RAG基线**：BM25+LLM、Contriever、RAPTOR、GraphRAG、LightRAG、MiniRAG、HippoRAG、HippoRAG2，以及传统OpenIE+ HippoRAG组合。
  - **消融设置**：Entity-KG vs Entity-Event-KG vs Full-KG（含概念）；不同LLM架构（DeepSeek、LLaMA、Qwen）和参数量（1B-70B）。
- **评价指标**：三元组抽取用精确率、召回率、F1；信息保留用MCQ准确率；模式质量用BS-R和BS-C（基于BERTScore）；QA用Exact Match和F1；事实性用平衡准确率和F1。

## 4. 资源与算力

- 论文在D节“Implementation Details”中明确说明了计算成本：
  - **硬件**：80GB GPU（1,513 TFLOPS FP16），运行Llama-3-8B-Instruct，启用Flash Attention 2。
  - **耗时**：总计约**78,400 GPU小时**，其中En-Wiki 14,300小时，Pes2o-Abstract 11,800小时，Common Crawl 52,300小时。
  - 未明确GPU具体型号（推测为A100或H100），但给出了浮点算力指标。

## 5. 实验数量与充分性

- **实验数量**：本文进行了大量实验：
  - 三元组抽取准确率（3个语料 × 3类三元组 + 与2个基线对比）。
  - 信息保留（MCQ，3个语料 × 多个LLM × 多种表示）。
  - 模式质量（4个实体/事件/关系数据集，与Txt2onto对比，跨7种LLM）。
  - 多跳QA（3个数据集 × 15+种基线方法 × 3种KG配置）。
  - 事实性（FELM，3个域 × 多种检索方法）。
  - MMLU（14个主题 × 多种检索方法 × 3种语料 × 2种RAG方式）。
  - 消融研究（实体/事件/概念逐步添加）和跨LLM架构/规模比较。
- **充分性与公平性**：覆盖了从组件到完整系统的多层次评估，对比方法全面且包含最新SOTA（如HippoRAG2）。使用了标准指标，并进行了跨验证（多judge验证三元组质量）。实验设计客观、公平，足以支撑结论。

## 6. 论文的主要结论与发现

- **三元组抽取质量高**：AutoSchemaKG在三个语料上均达到>95%的精确率，召回率和F1超过OpenIE 6和Stanford OIE。
- **事件保留更丰富信息**：仅使用事件三元组的MCQ性能显著优于仅实体，保留超95%原文信息。
- **模式归纳准确**：自动归纳模式与人工归纳的语义对齐率达92%（BS-R/C），远优于传统Txt2onto方法。
- **多跳QA显著提升**：Full-KG（含概念）配合HippoRAG2在多跳QA上取得12-18%绝对提升（EM/F1）。
- **LLM事实性增强**：在FELM上，ATLAS-Wiki和ATLAS-CC的知识图谱检索对LLM事实性提升1-9%。
- **领域知识增强**：在MMLU知识密集型领域（法律、历史、社会等）持续改进，但数学/逻辑类受益有限。
- **不同语料各有特长**：ATLAS-Pes2o（学术摘要）在医学、宗教、社会等领域表现更强，ATLAS-CC（通用网络）在法律和历史上更好。

## 7. 优点

- **全自动无人工干预**：完全消除对预定义模式的依赖，实现端到端自动化KG构建。
- **事件和概念的unique建模**：同时建模事件和概念，保留更丰富的语义信息，并提供跨越不连通子图的替代检索路径。
- **规模巨大**：构建了迄今为止最大的自动构建KG和最大Graph RAG数据集（9亿节点、59亿边）。
- **泛化性良好**：框架与多种LLM架构和参数规模兼容，且在不同语料和下游任务上均有效。
- **实验设计严谨**：多层次评估（组件+系统）、多judge验证、与大量SOTA基线公平比较，消融清晰。

## 8. 不足与局限

- **LLM偏差与局限性**：框架继承了所用LLM的偏差和知识缺口，在专业领域可能因LLM知识不足而表现欠佳。
- **技术领域局限**：在MMLU的数学、逻辑等依赖程序性知识的领域，知识图谱检索反而可能干扰LLM性能。
- **可能存在不一致**：尽管规模巨大，但自动抽取可能引入矛盾或信息缺失，尤其在稀疏知识区域。
- **计算成本高**：构建大规模KG需要数万GPU小时，对资源要求较高，可能限制小型团队的复现和应用。
- **未深入探讨**：论文未详细讨论对不同语言或非英语语料的适应性；也未讨论对短期更新（时序）的处理机制。

（完）
