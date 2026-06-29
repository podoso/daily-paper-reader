---
title: Structured Retrieval-Augmented Generation for Multi-Doc Multi-Entity Question Answering
title_zh: 结构化检索增强生成用于多文档多实体问答
authors: "Teng Lin, Yizhang Zhu, Zhengxuan Zhang, Yuyu Luo, Nan Tang"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=sMRzFxSg9W"
tags: ["query:llm"]
score: 6.0
evidence: 用于多实体问答的结构化RAG与LLM
tldr: 多文档多实体问答中，LLM和RAG难以构建跨文档证据链。本文提出结构化RAG，通过图结构整合实体关系网络，改进检索粒度，有效追踪实体间隐含逻辑。在MDMEQA基准上，该方法相比基线显著提升了答案准确率，展示了结构化检索对复杂推理的增益。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-smrzfxsg9w/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1548, \"height\": 887, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-smrzfxsg9w/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 982, \"height\": 1141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-smrzfxsg9w/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1491, \"height\": 1332, \"label\": \"Table\"}]"
motivation: 多文档多实体问答中LLM和RAG难以跨文档推理实体关系。
method: 提出结构化RAG，结合图结构检索与实体关系追踪，增强证据链构建。
result: 在MDMEQA基准上准确率显著提升。
conclusion: 结构化RAG能有效辅助LLM进行多实体跨文档推理。
---

## Abstract
Multi-document Multi-entity Question Answering (MDMEQA) fundamentally requires models to track and connect the implicit logic between multiple entities across documents, a task that reveals critical limitations of Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG) frameworks: they struggle to construct effective cross-document evidence chains and deduce entity relationships when faced with fragmented information. Although RAG improves answering capabilities through context injection, its coarse-grained retrieval strategy that relies on vector similarity often leads to the omission of critical facts. Meanwhile, graph-based RAG fails to efficiently integrate scattered complex relationship networks in multi-document scenarios, resulting in low efficiency in retrieving and reasoning MDMEQA. We propose Structured Retrieval-Augmented Generation (SRAG): a two-stage framework that first transforms unstructured text into semantically coherent relational tables via a SQL-driven Extraction-Retrieval module, then guides LLMs toward schema-aware relational reasoning over structured representations. This architectural breakthrough offers three key advantages: (1) SQL-powered indexing enables precise fact localization; (2) relational tables naturally support multi-hop entity join operations; (3) the structuring process mitigates the attention diffusion effect of LLMs. To verify the effectiveness of our proposed method, we evaluate SRAG on two multi-document QA benchmarks, MEBench and Loong. The results show that SRAG significantly outperforms the current state-of-the-art long-context LLMs and RAG systems, achieving 27.2% and 27% improvements in accuracy respectively. These results highlight the importance of structured data representation in enhancing complex reasoning and answer precision in multi-document multi-entity  question answering. The source code and data have been made available at https://anonymous.4open.science/r/SRAG-07A7.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：多文档多实体问答（MDMEQA）要求模型跨文档追踪和连接多个实体间的隐含逻辑，但大型语言模型（LLM）和传统检索增强生成（RAG）框架存在严重不足：
  - LLM 依赖参数化记忆，在处理分散信息时出现“注意力扩散”，且缺乏构建跨文档证据链的显式机制。
  - 传统 RAG 基于向量相似度的粗粒度检索常遗漏关键事实；图 RAG 在多文档场景下难以高效整合分散的复杂关系网络，导致检索与推理效率低下。
- **整体含义**：现有方法在检索精度与多实体推理能力之间存在断层，亟需一种能同时实现精确事实定位和跨文档关系推理的新范式。

## 2. 方法论
- **核心思想**：利用结构化关系表（而非非结构化文本块或稀疏图）作为推理核心，将检索与结构化构建统一。
- **两阶段框架 (SRAG)**：
  - **阶段一：SQL驱动的抽取-检索模块**
    - 将用户自然语言问题解析为 SQL 查询语句和目标表模式（Schema）。
    - 使用小规模语言模型（如 Mistral-7B）基于 Schema 进行多任务信息抽取（实体识别、属性抽取、关系链接）。
    - 执行 SQL 查询对抽取的原始信息进行过滤、连接和排序，生成干净、高相关的结构化关系表。
    - 优势：SQL 索引实现精确事实定位；关系表原生支持多跳实体连接；抽取过程高效且成本低。
  - **阶段二：Schema感知的 LLM 推理模块**
    - 将生成的关系表与原始问题一起注入 LLM 提示，强制 LLM 仅基于表格数据进行推理（结构化上下文注入）。
    - LLM 在表格上执行确定性推理（如按日期排序、跨行列关联），生成最终答案。
    - 优势：消除注意力扩散；补偿 LLM 在精确计算和逻辑操作上的弱点；答案可靠且可追溯。
- **关键技术细节**：使用 GPT-4o 作为解析器和推理模型，Mistral-7B 作为信息抽取小模型；通过指令控制减少输出 token 大小，优化成本。

## 3. 实验设计
- **数据集**：
  - **MEBench**：包含 4780 个精心设计的问题，涵盖比较、统计、关系三类，并按实体数量分为 ≤10、11–100、>100 三个子集。
  - **Loong**：包含四个推理任务（Spotlight Locating、Comparison、Clustering、Chain of Reasoning），文档长度横跨 10K–250K tokens 四个区间。
- **基准方法**：
  - 无检索：GPT-4o
  - 传统 RAG：GPT-4o + RAG (使用向量检索)
  - 结构增强方法：GraphRAG（知识图谱）、StructRAG（动态结构表示）
  - 本文方法：SRAG
- **评估指标**：
  - MEBench：准确率（Accuracy）
  - Loong：LLM 判分（0–100 平均分）和精确匹配率（Perfect Rate, 0–1）

## 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。
- 实验使用了 GPT-4o（云 API）和 Mistral-7B（开源模型），未提及训练或微调，仅涉及推理阶段，因此算力要求相对较低。

## 5. 实验数量与充分性
- **实验数量**：
  - MEBench：报告了整体准确率及三个子集（按实体数量）的准确率，每种方法在三个问题类别上的结果。
  - Loong：报告了四个任务在四个 token 长度区间的平均分和精确匹配率，共 4×4 = 16 个子结果。
  - 隐含消融：通过对比 SRAG 与 GPT-4o（无检索）、传统 RAG、GraphRAG、StructRAG，实际上评估了每个模块的贡献（组件替换比较）。
- **充分性与公平性**：
  - 覆盖多种推理类型和文档规模，具有较好的泛化性。
  - 所有基线均为 SOTA 方法，实现细节（如使用相同的基础 LLM GPT-4o）保证了公平比较。
  - 缺乏显式消融实验（如仅替换抽取模块或仅使用结构化推理），但作者声称对比设计已隐含消融逻辑，可接受。
- **总体评价**：实验设计较为充分，结果客观。

## 6. 论文的主要结论与发现
- **性能大幅领先**：SRAG 在 MEBench 上整体准确率 89.2%，比最佳基线（GPT-4o+RAG 62.0%）提高 27.2 个百分点；在 Loong 上平均分 68.29，精确匹配率 0.53，远超其他方法（最好基线为 GPT-4o 的 0.26）。
- **鲁棒性极强**：随着实体数量增加（MEBench Set3 >100 实体）或文档长度增加（Loong 200K–250K tokens），SRAG 性能下降最小，而基线方法衰减严重。
- **任务适用广泛**：在比较、统计、关系、精确定位、链式推理等各类任务中均表现最佳。
- **核心发现**：结构化数据表示（关系表）是解决多文档多实体推理中检索不精确和推理效率低下的关键。

## 7. 优点
- **方法创新性**：将 SQL 驱动的结构化抽取与 Schema 感知推理有机结合，突破了传统 RAG 和图 RAG 在 MDMEQA 中的瓶颈。
- **设计优势**：
  - SQL 索引实现精确事实定位，避免向量相似度的噪声。
  - 关系表天然支持多跳实体连接，简化跨文档推理。
  - 结构化过程抑制 LLM 的注意力扩散，提升推理可靠性。
- **实验扎实**：在两个难度不同的基准上进行了全面的多维度评估，结果稳健且提升幅度显著。
- **实用性强**：使用小型模型进行抽取，大型模型仅用于推理及解析，成本和速度平衡较好。

## 8. 不足与局限
- **实验覆盖的局限**：
  - 未在更多样化的文档类型（如表格、图像、PDF 中的非连续文本）上验证。
  - 未涉及低资源领域（如医学、法律）的特定术语适应。
- **模型依赖**：高度依赖于 GPT-4o 的解析和推理能力，若使用较弱 LLM 可能性能下降；Mistral-7B 的抽取质量也需进一步验证。
- **可扩展性挑战**：对于超大规模语料，SQL 驱动检索的延迟可能较高，文中未详述优化策略。
- **隐含消融的不足**：虽然有对比设计，但缺少显式消融（如仅使用结构化抽取但不使用 SQL 过滤、或使用其他小模型）来分离每个因素的具体贡献。
- **未讨论偏见与公平性**：未对 LLM 本身或源文档中的潜在偏见进行敏感性分析。
- **应用限制**：需要预定义或动态生成表 Schema，对于问题高度开放或概念模糊的场景可能存在适配困难。

（完）
