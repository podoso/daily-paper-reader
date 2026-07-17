---
title: "SocraticKG: Knowledge Graph Construction via QA-Driven Fact Extraction"
title_zh: SocraticKG：通过问答驱动的事实抽取构建知识图谱
authors: "Sanghyeok Choi, Woosang Jeon, Kyuseok Yang, Taehyeong Kim"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1951.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 通过问答驱动的事实抽取构建知识图谱
tldr: 该论文提出SocraticKG方法，通过问答对作为结构化中间表示，逐步抽取文档级三元组来构建知识图谱。采用5W1H引导的问答扩展，有效捕捉上下文依赖和隐式关系链接，解决了现有方法中事实覆盖与关系碎片化的权衡问题。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1951/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1951/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 1008, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1951/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1640, \"height\": 500, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1664, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1661, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 817, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1665, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1663, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1663, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1951/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 813, \"height\": 306, \"label\": \"Table\"}]"
motivation: 现有基于LLM的知识图谱构建面临事实覆盖与关系碎片化的权衡。
method: 引入问答对作为中间表示，通过5W1H引导扩展进行事实抽取。
result: 在知识图谱构建质量上优于直接抽取方法。
conclusion: 问答驱动的中间表示能更好地保留文档级语义信息。
---

## Abstract
Constructing Knowledge Graphs (KGs) from unstructured text provides a structured framework for knowledge representation and reasoning, yet current LLM-based approaches struggle with a fundamental trade-off: factual coverage often leads to relational fragmentation, while premature consolidation causes information loss. To address this, we propose SocraticKG, an automated KG construction method that introduces question-answer pairs as a structured intermediate representation to systematically unfold document-level semantics prior to triple extraction. By employing 5W1H-guided QA expansion, SocraticKG captures contextual dependencies and implicit relational links typically lost in direct KG extraction pipelines, providing explicit grounding in the source document that helps mitigate implicit reasoning errors. Evaluation on the MINE benchmark demonstrates that our approach effectively addresses the coverage-connectivity trade-off, achieving superior factual retention while maintaining high structural cohesion even as extracted knowledge volume substantially expands. These results highlight that QA-mediated semantic scaffolding plays a critical role in structuring semantics prior to KG extraction, enabling more coherent and reliable graph construction in subsequent stages.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的详细中文总结，采用 Markdown 格式，并严格遵循了您要求的八个要点顺序。

### 论文核心问题与整体含义

*   **研究动机**：当前基于大语言模型（LLM）的知识图谱（KG）自动构建方法普遍面临一个根本性权衡：**事实覆盖度与结构连贯性难以兼得**。直接抽取方法（Direct Extraction）虽能保留较多事实，但往往导致图结构碎片化、语义连接弱；而优先进行实体识别和合并的整合策略（如GraphRAG、KGGen）虽能提升结构连贯性，却会因过早的“实体级瓶颈”而丢失大量潜在的上下文关系和隐含信息。
*   **整体含义**：为了突破这一权衡，论文认为问题根源在于缺乏有效的**中间语义表示**来组织文档级语义。因此，受人类通过主动提问来理解复杂信息的方式启发，提出一种新的范式：将问答对（QA pairs）作为一种结构化的语义支架，在抽取三元组之前，系统性地将文档的叙事逻辑展开并外显化，从而构建更完整、更连贯的知识图谱。

### 论文提出的方法论

*   **核心思想**：SocraticKG 方法的核心是 **QA 驱动的语义展开**。它不是直接从原始文本抽取三元组，而是先生成一系列与上下文无关、自包含的问答对，将这些问答对作为捕捉实体、关系和隐含依赖的中间表示，再从中抽取结构化的三元组。
*   **关键技术细节（三阶段流水线）**：
    1.  **5W1H 引导的 QA 生成**：
        *   利用`Who, What, When, Where, Why, How`框架，指导 LLM 系统地生成覆盖文档各个维度的详细问题。
        *   要求生成的答案必须**上下文无关**（Context-Independent），即替换所有代词为具体实体名，确保每个 QA 对是一个独立的语义单元，后续处理时不会丢失信息。
    2.  **从 QA 对中抽取三元组**：
        *   将每个 QA 对视为独立的抽取单元，遵循三个约束：**原子分解**（将复杂句分解为独立的三元组）、**实体清晰**（避免代词，确保每个实体是具体名词短语）、**化简关系**（将谓词精炼为简洁的动词短语）。
    3.  **图构建与标准化**：
        *   通过**嵌入聚类 + LLM 精炼**的标准化过程，将不同 QA 对中抽取的冗余或同义的实体和关系合并，最终形成连贯、一致的知识图谱。该过程独立处理实体和关系，通过 K-means 聚类缩小搜索空间，再结合稠密语义相似度（嵌入）与稀疏词汇重叠（BM25）找到候选匹配，最后用 LLM 解析同义词。

### 实验设计

*   **数据集与基准 (Benchmark)**：
    1.  **MINE (Measure of Information in Nodes and Edges) 基准**：包含 100 篇不同文章，每篇配有 15 个已验证的原子事实，总计 1500 个事实实例，用于评估 KG 对源信息的保留能力（事实保留率 Factual Retention Score）。
    2.  **HotpotQA 下游任务**：使用 800 个“Hard Bridge”样本进行评估，这些样本需要跨多个证据进行多跳推理，用于评估 KG 在下游推理任务中的实用性。
*   **对比方法**：
    *   **Direct Extraction**：直接从原始文本抽取三元组。
    *   **GraphRAG**：基于实体索引和层次化社区摘要的方法。
    *   **KGGen**：实体优先的抽取与结构整合方法。
    *   **SoKG (w/o 5W1H)**：无5W1H引导的变体，用于消融实验。
    *   **SoKG (Ours)**：完整方法。

### 资源与算力

论文正文和附录**并未明确提及所使用的具体 GPU 型号、数量和训练时长**。附录 D 提供了一个计算效率分析表，报告了各方法的总Token消耗量 (Ttotal) 和生成的三元组数量 (Ntri)，但未涉及硬件资源。这表明作者将分析重点放在了方法的计算成本（Token消耗）而非具体的硬件配置上。

### 实验数量与充分性

*   **实验数量**：实验较为充分。核心实验包括：在不同 LLM 骨干（GPT-4o, GPT-4o-mini, Gemini-2.5, Qwen-2.5, Claude-4）上对比事实保留率、图拓扑特征（节点/边数、平均度）、碎片化指数（NFI）、信息量（三元组总数）。另有 HotpotQA 的多跳推理准确率实验。附录中还包括消融实验（对比不同 Prompt 原型、对比实体优先策略）、计算成本分析、三元组质量分析（独特性、粒度、事实精确度）以及失败案例分析。
*   **公平性与客观性**：实验设计相对公平。对比方法均为当前主流且开源的 LLM 方法，并在相同条件下评估。使用了统一的标准化过程，并通过 LLM-as-Judge 和人工评估进行验证，降低了主观偏差。实验对比了 5 个不同规模和系列的 LLM，覆盖了弱模型到强模型，增强了结论的普适性。

### 论文的主要结论与发现

1.  **QA 中间表示有效**：在几乎所有被评估的 LLM 上，SocraticKG 都取得了最高的事实保留率（最高达 96.3%），优于直接抽取和整合策略。
2.  **平衡了覆盖与连贯性**：SocraticKG 在显著扩大知识图谱规模和事实数量的同时，**降低了图的碎片化程度**（NFI值更低），并**保持了更高的平均度**（更好的局部连接性），有效解决了覆盖度-连接性之间的权衡。
3.  **下游推理性能提升**：在 HotpotQA 的多跳推理任务中，SocraticKG 在所有设置下均优于基于文本块的 Naive RAG 和其他 KG 构建方法，证明了结构优势能转化为实际的推理增益。
4.  **5W1H 引导至关重要**：消融实验表明，5W1H 框架能提高事实保留率，并增强图的结构凝聚力，其作用是普适的，不依赖于特定的提示词风格。

### 优点

*   **方法创新性强**：巧妙的将人类学习过程中的“提问”机制引入 KG 构建，将 QA 对作为核心的语义组织单元，思路新颖且有效。
*   **普适性强**：在不同规模、不同家族的多个 LLM 上均表现出一致的性能提升，证明了方法的鲁棒性和泛化能力。
*   **实验设计严谨**：不仅评估了事实保留率，还深入分析了图的拓扑结构指标（度、碎片化指数），并将结构优势关联到下游推理任务，实验逻辑完整。
*   **分析深入**：附录中对失败案例进行了详细分析，揭示了主要瓶颈在 QA 生成阶段（“What”类问题易流于表面），为未来改进指明了方向。

### 不足与局限

*   **计算成本较高**：多阶段流水线（QA生成 + 逐对三元组抽取）比单次直接抽取消耗更多 Token。虽然论文认为投入与产出成正比，但并未讨论如何优化其效率。
*   **依赖 LLM 推理能力**：QA 生成的质量直接受限于底层 LLM 的推理深度和提问能力，在需要高度专业化领域知识的场景下可能表现不稳定。
*   **三元组表示的限制**：当前使用二元组（Subject-Relation-Object），可能简化了包含时空等限定词的复杂关系（n-ary 关系），存在信息丢失风险。
*   **评估范围有限**：主要聚焦于事实可恢复性和下游推理，对知识图谱的其他重要维度，如**模式对齐**（Schema Alignment）和**关系类型保真度**（Relation-Type Fidelity）未作评估。

（完）
