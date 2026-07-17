---
title: "Chain-of-Relations: Faithful and Efficient LLM Reasoning over Knowledge Graphs via Relation-Centric Exploration"
title_zh: 关系链：通过以关系为中心的探索实现知识图谱上的忠实高效LLM推理
authors: "Chenhui Liu, Jianpeng Zhou, Jiahai Wang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2138.pdf"
tags: ["query:llm"]
score: 7.0
evidence: 大语言模型在知识图谱上的关系中心探索推理
tldr: 现有基于知识图谱的问答方法采用实体中心探索，面临实体不完整和过早剪枝问题。本文提出Chain-of-Relations，一种以关系为中心的探索方法，通过优先考虑关系路径而非实体来增强推理的忠实性和效率。在多个KGQA基准上，该方法优于现有实体中心方法。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2138/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 696, \"height\": 1092, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2138/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1612, \"height\": 878, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2138/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 799, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2138/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1625, \"height\": 692, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2138/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 589, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2138/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 584, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2138/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 750, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2138/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1636, \"height\": 537, \"label\": \"Table\"}]"
motivation: 实体中心探索在知识图谱问答中易受实体不完整和过早剪枝影响。
method: 提出以关系为中心的探索策略，优先扩展关系路径而非实体节点。
result: 在多个KGQA数据集上取得更优的推理准确率和效率。
conclusion: 关系中心探索可提升LLM在知识图谱上的推理可靠性。
---

## Abstract
Knowledge graph question answering (KGQA) serves as an essential benchmark for KG-enhanced large language models. Among various approaches, agent-based methods have emerged as an effective solution.Existing methods adopt entity-centric exploration that incrementally constructs reasoning paths by selecting and connecting intermediate entities. However, they face two critical limitations. (1) Entity incompleteness vulnerability arises when some intermediate entities lack semantic information beyond opaque IDs, preventing relevance evaluation and leading to discarding valid reasoning paths.(2) Premature entity pruning occurs because beam search retains only top-ranked entities at each step, eliminating candidates before their relevance can be verified.To address these challenges, this paper proposes Chain-of-Relations (CoR) with relation-centric exploration and global entity filtering, reducing dependence on entity completeness and ensuring complete candidate retrieval before constraint validation.Experiments on three benchmark datasets show that CoR consistently outperforms strong baselines in both F1 score and KG-grounded Rate.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLM）在复杂推理任务中表现出色，但存在知识过时、幻觉和缺乏可解释性等根本局限。知识图谱（KG）通过结构化、可验证的知识表示可弥补这些不足。知识图谱问答（KGQA）成为评估KG增强LLM的关键基准。

- **现有方法**：基于智能体的方法（如ToG、PoG）采用实体中心探索（entity-centric exploration），逐步通过选择中间实体来构建推理路径。但面临两个严重缺陷：
  - **实体不完整漏洞（Entity incompleteness vulnerability）**：当中间实体仅由不透明ID（如 m.0f4vbz）标识时，缺乏语义信息，导致LLM无法评估其相关性，从而丢弃有效路径。
  - **过早实体剪枝（Premature entity pruning）**：束搜索（beam search）每步只保留top-k实体，许多潜在有效实体在后续约束验证前就被剪掉，导致召回率大幅下降。

- **动机**：解决上述问题，提升KGQA的准确性、忠实性和效率。

### 2. 方法论：核心思想、关键技术细节

- **核心思想**：从实体中心探索转变为关系中心探索（Relation-Centric Exploration），将关系作为多跳推理的基本单元，而非实体。同时采用全局实体过滤（Global Entity Filtering），推迟约束验证直至完整关系链构建完成。

- **关键组件**：
  - **关系中心探索**：
    - 操作空间从实体空间（百万级）缩小到关系空间（10³~10⁴），降低计算成本。
    - 每一步：①**关系搜索**：基于当前关系链查询KG，获取所有可扩展的关系候选；②**关系剪枝**：LLM根据语义对齐、逻辑一致性和目标接近度对候选关系评分，保留top-k（k=3）；③**记忆更新**：将候选关系链推入记忆栈，优先探索高分路径，支持回溯；④**推理**：LLM通过两个层次的问题决定下一步动作（停止/前进/回溯/过滤）。
    - 引入关系级回溯机制，遇到死胡同时可自动回退到替代关系路径。
  - **全局实体过滤**：
    - 关系链构建完成后，一次性执行实体检索，获取所有可达候选实体。
    - LLM识别问题中的全部约束（如 nationality=American），同时对候选实体进行过滤，选出最终答案。避免每步剪枝造成的信息丢失。

- **新评估指标**：KG-grounded Rate (KGR) 衡量通过显式KG推理路径获得答案的问题比例，用于区分答案来自KG还是LLM记忆，评估推理忠实性。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**（三个KGQA基准）：
  - **WebQSP**（Freebase）：1,639个测试问题，平均1-2跳推理，约束简单。
  - **ComplexWebQuestions (CWQ)**（Freebase）：3,531个测试问题，2-4跳推理，多约束。
  - **QALD10-EN**（Wikidata）：333个测试问题，强调组合推理和多种约束类型。

- **对比方法**：
  - LLM-only方法：IO Prompting，Chain-of-Thought (CoT) Prompting。
  - 基于智能体的方法：ToG（实体中心探索+束搜索）、PoG（自适应计划+自纠正），均为训练免费方法。

- **LLM骨干**：gpt-4.1-mini（闭源、快速）和 DeepSeek-V3.1（开源、优化推理），温度0.01。

- **实现细节**：top-k=3，最大推理深度WebQSP/QALD10为3跳，CWQ为4跳；使用官方Freebase快照和Wikidata SPARQL端点。

### 4. 资源与算力

- **未明确说明**：论文未提及使用的GPU型号、数量、训练时长或推理集群配置。仅提到使用两种LLM模型（GPT-4.1-mini和DeepSeek-V3.1）通过API调用，未涉及自定义模型训练，因此算力消耗主要来自LLM推理调用。
- 文中提供了总token用量（表4），可作为计算资源消耗的间接参考。

### 5. 实验数量与充分性

- **实验组数**：
  - 主实验：三个数据集 × 两种LLM × 四种方法（IO、CoT、ToG、PoG、CoR），共30组结果（表1）。
  - 消融实验：在CWQ上移除关系级回溯（RB）和全局实体过滤（GEF），共3组（表3）。
  - 推理深度影响实验：CWQ上深度3/4/5，3组（表2）。
  - 效率分析：LLM调用次数分布（图3）、总token用量（表4）。
  - 案例研究：一个具体问题“Who inspired Obama?”的对比（表5）。

- **充分性与公平性**：
  - 对比方法均使用官方开源代码实现，同一KG、同一LLM骨干、相同超参数（束宽、深度），控制变量严格。
  - 消融实验验证各组件贡献，深度实验探索最佳设置。
  - 评估指标包括Hits@1、Precision、Recall、F1和KGR，覆盖正确性和忠实性。
  - 实验设计较为充分、客观、公平。

### 6. 主要结论与发现

- **CoR在准确性和忠实性上均优于实体中心方法**：在WebQSP和CWQ上，CoR在Hits@1、F1和KGR指标上显著领先ToG和PoG；在QALD10上，CoR同样具有竞争力（KGR在GPT-4.1-mini下最高）。
- **效率优势显著**：CoR在三个数据集上均比ToG和PoG使用更少的总token和更低的平均LLM调用次数（WebQSP 4.03次，CWQ 11.21次，QALD10 4.78次），主要因关系空间更紧凑、无需逐实体评分。
- **全局实体过滤贡献最大**：消融实验表明，移除GEF后性能下降最明显（CWQ F1从52.0降至42.8），说明推迟约束验证对保留候选实体至关重要。
- **关系级回溯有助于恢复错误路径**：移除RB后性能小幅下降（F1从52.0降至50.0）。
- **最佳推理深度为4跳**：CWQ上深度4达到最佳平衡，深度3覆盖不足，深度5引入噪声。

### 7. 优点

- **方法创新性**：首次提出关系中心探索范式，将问题从实体空间转移到关系空间，有效规避实体不完整问题，设计简洁且通用。
- **高效性**：通过减少API调用和token消耗，大幅降低推理成本，同时保持或提升性能。
- **可解释性**：关系链作为明确的推理路径，易于理解和验证；新指标KGR提供忠实性量化，超越单纯正确性评估。
- **实验全面性**：涵盖三个不同KG、两种主流LLM、多项消融和效率分析，结果稳健。
- **实用性**：训练免费，可直接应用于现有KG，无需额外微调。

### 8. 不足与局限

- **仍依赖LLM的约束识别能力**：全局实体过滤阶段，LLM需要从问题中识别约束并应用于候选实体，若LLM产生幻觉或错误理解约束（如识别错误nationality约束），可能引入错误。
- **关系空间限制**：对关系稀疏的KG（某些领域关系少）可能效果有限；对需要实体属性值比较（如数值排序）的查询，关系链无法直接表达，需依赖LLM后处理。
- **通用性待验证**：当前仅在Freebase和Wikidata上评估，未在更多领域KG（如生物医学、金融等）上测试，泛化能力未知。
- **实时应用挑战**：虽效率提升，但仍需多次LLM调用（CWQ平均11.21次），对延迟敏感场景可能不足。
- **未讨论错误传播**：关系链中某一步选择错误关系可能导致后续全部无效，尽管回溯机制可缓解，但无法完全消除。
- **实验未覆盖所有最新方法**：仅对比ToG和PoG，未与更多基于检索或图神经网络的方法（如GNN-RAG）比较，但论文解释ToG和PoG是代表性训练免费实体中心方法。

（完）
