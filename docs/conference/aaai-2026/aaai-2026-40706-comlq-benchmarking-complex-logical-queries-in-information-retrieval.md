---
title: "ComLQ: Benchmarking Complex Logical Queries in Information Retrieval"
title_zh: ComLQ：信息检索中复杂逻辑查询的基准测试
authors: "Ganlin Xu, Zhitao Yin, Linghao Zhang, Jiaqing Liang, Weijia Lu, Xiaodong Zhang, Zhifei Yang, Sihang Jiang, Deqing Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40706/44667"
tags: ["query:llm"]
score: 4.0
evidence: 使用大语言模型构建信息检索复杂逻辑查询数据集
tldr: 信息检索系统在真实场景中需处理复杂逻辑查询，但现有基准仅覆盖简单查询。本文利用大语言模型构建新数据集ComLQ，包含2909个查询和11251个候选段落，涵盖合取、析取和否定操作。该工作弥补了基准缺失，但更侧重于信息检索而非信息抽取。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有信息检索基准只关注简单查询，无法充分评估模型在真实场景中的复杂逻辑查询性能。
method: 利用大语言模型自动化生成包含合取、析取和否定的复杂逻辑查询及其候选段落。
result: 构建了包含2909个查询和11251个候选段落的数据集ComLQ。
conclusion: ComLQ为评估复杂逻辑查询性能提供了新基准，但主要贡献在信息检索领域。
---

## Abstract
Information retrieval (IR) systems play a critical role in navigating information overload across various applications. Existing IR benchmarks primarily focus on simple queries that are semantically analogous to single- and multi-hop relations, overlooking complex logical queries involving first-order logic operations such as conjunction (∧), disjunction (∨), and negation (¬). 
Thus, these benchmarks can not be used to sufficiently evaluate the performance of IR models on complex queries in real-world scenarios. To address this problem, we propose a novel method leveraging large language models (LLMs) to construct a new IR dataset ComLQ for Complex Logical Queries, which comprises 2,909 queries and 11,251 candidate passages. A key challenge in constructing the dataset lies in capturing the underlying logical structures within unstructured text. Therefore, by designing the subgraph-guided prompt with the subgraph indicator, an LLM (such as GPT-4o) is guided to generate queries with specific logical structures based on selected passages. All query-passage pairs in ComLQ are ensured structure conformity and evidence distribution through expert annotation. To better evaluate whether retrievers can handle queries with negation, we further propose a new evaluation metric, Log-Scaled Negation Consistency (LSNC@K). As a supplement to standard relevance-based metrics (such as nDCG and mAP), LSNC@K measures whether top-K retrieved passages violate negation conditions in queries. Our experimental results under zero-shot settings demonstrate existing retrieval models' limited performance on complex logical queries, especially on queries with negation, exposing their inferior capabilities of modeling exclusion. In summary, our ComLQ offers a comprehensive and fine-grained exploration, paving the way for future research on complex logical queries in IR.

---

## 论文详细总结（自动生成）

# ComLQ：信息检索中复杂逻辑查询的基准测试 — 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有信息检索（IR）基准（如 MS-MARCO、TREC、BEIR）主要关注语义简单的查询（单跳或多跳关系），忽略了包含一阶逻辑操作（合取 ∧、析取 ∨、否定 ¬）的复杂逻辑查询。而真实用户查询常涉及复合逻辑推理，因此现有基准无法充分评估 IR 模型在现实场景中的性能。
- **整体含义**：引入首个聚焦复杂逻辑查询的 IR 数据集 ComLQ，填补了该领域的空白，旨在推动 IR 系统对逻辑结构理解和排除能力（negation modeling）的研究。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：利用大语言模型（LLM）自动生成符合特定逻辑结构（如 1p、2i、pin 等 14 种类型）的查询，并通过人工审核确保质量，从而构建高质量基准数据集。
- **关键技术细节**：
  1. **子图引导提示（Subgraph-Guided Prompt）**：设计包含三个部分的提示：
     - **查询定义**：自然语言描述该查询类型的定义。
     - **子图指示器（Subgraph Indicator）**：以符号逻辑形式（如 `{?z | (?x, R1, ?y) ∧ (?y, R2, ?z)} ∩ {?z | ¬(?w, R3, ?z)}`）表示查询的 FOL 结构，帮助 LLM 理解模式。
     - **演示示例**：提供现成的查询-答案对。
     - 基于选定的若干段落，要求 LLM 生成符合指定逻辑结构的查询。
  2. **数据合成流程**：
     - **段落选择**：从 Wikipedia dump（20M 段落）中选取同一主题的一个或多个段落。
     - **查询生成**：使用 GPT-4o，将段落和提示输入，生成查询及其对应的三元组表示。
     - **专家验证**：三名标注员依据两个标准审核每一对查询-段落：
       - **结构符合性**：查询是否严格按照目标逻辑结构（通过辅助三元组判断）。
       - **证据分布**：对于多段落查询，确认支持证据确实分布在所选段落中。
     - **添加干扰段落**：增加与查询主题完全无关的段落，以测试模型忽略无关信息的能力。
- **最终数据集**：包含 2,909 个查询和 11,251 个候选段落，覆盖 14 种查询类型（9 种无否定，5 种有否定）。

## 3. 实验设计

- **使用的数据集 / 场景**：ComLQ 数据集本身（14 种查询类型），零样本（zero-shot）设置。
- **Benchmark**：与现有 IR 基准不同，本文直接以 ComLQ 为测试基准。
- **对比的方法**：
  - **稀疏检索器**：BM25
  - **稠密检索器**：BGE、Contriever
  - **基于 LLM 的检索模型**：HyDE、InteR、LameR、AGR、PromptReps
- **实现细节**：
  - 对于 HyDE、LameR、AGR、InteR，统一使用 `bge-small-en-v1.5` 作为嵌入模型，GPT-4o（温度 0.5）作为底层 LLM。
  - PromptReps 使用 LLaMA3-70B-Instruct。
- **评价指标**：
  - **nDCG@10**：用于衡量整体相关性（原标准指标）。
  - **LSNC@K（Log-Scaled Negation Consistency）**：新指标，专门衡量 Top-K 检索结果中违反查询否定条件的程度。公式：`LSNC@K = -log((∑d∈D_k V(d)+1)/(K+1)) / log(K+1)`，其中 V(d) 为 1 表示违反否定条件。得分越高越好。

## 4. 资源与算力

- **明确说明**：所有实验在三块 NVIDIA A800 80GB GPU 上进行。
- **其他算力信息（如训练时长、总计算量）**：文中未提及具体训练时长或 GPU 小时数。

## 5. 实验数量与充分性

- **实验数量**：
  - 对 10 种检索模型在 14 种查询类型上进行了 nDCG@10 评估（表 3）。
  - 对包含否定的 5 种查询类型进行了 LSNC@100 评估（表 4）。
  - 分析逻辑操作顺序影响（pi vs ip 可视化，图 4）。
  - 分析证据分布影响（不同支持段落数 #1/#2/#3，图 5）。
  - 消融实验：有无子图指示器对生成查询结构符合性的影响（图 6）。
  - 案例研究：改写查询（表 5）。
- **充分性与客观性**：
  - 覆盖了多种主流检索方法（稀疏、稠密、LLM-based）。
  - 提供了全面的误差分析和可视化，实验设计较为充分。
  - 但仅使用了 ComLQ 一个数据集，未与其他复杂逻辑查询基准（如 NegConstraint、HotpotQA）直接对比，存在一定局限性。

## 6. 论文的主要结论与发现

1. **性能不足**：所有检索模型在复杂逻辑查询上表现有限，没有任何模型能在所有查询类型上一致最优。
2. **复杂度影响**：随着查询复杂度增加（如 1p→2p→3p），性能显著下降；包含否定的查询（2in/3in/inp/pin/pni）性能远低于无否定查询。
3. **操作顺序影响**：投影-交集查询（pi、pin、pni）性能差于交集-投影查询（ip、inp），原因是前者语义组合更复杂。
4. **否定处理失败**：所有模型在 LSNC@100 上得分很低，表明它们难以正确处理否定条件，倾向于检索包含否定关键词的文档而非真正排除。
5. **稀疏检索器竞争力**：BM25 在某些类型上甚至优于稠密检索器（如 BGE、HyDE），挑战了稠密检索普遍更优的假设。
6. **子图指示器有效性**：消融实验表明，移除子图指示器会导致生成查询的结构符合性明显下降，尤其对复杂查询类型。

## 7. 优点：方法或实验设计上的亮点

- **创新数据集**：首个系统覆盖 14 种一阶逻辑操作组合的 IR 基准，填补了领域空白。
- **高质量生成流程**：结合符号子图指示器与 LLM 生成，并通过人工双重验证（结构符合 + 证据分布），保证了数据质量。
- **新评价指标**：LSNC 专门针对否定查询，弥补了传统相关性指标无法捕捉排除能力的不足。
- **详尽分析**：实验不仅报告整体分数，还深入分析了操作顺序、证据分布、否定影响等微观因素，提供了有价值的洞察。
- **可复现性**：公开代码和数据集。

## 8. 不足与局限

- **数据集规模小**：仅 2,909 个查询和 11,251 个段落，可能不足以覆盖所有领域的复杂逻辑查询模式。
- **域限定**：仅基于 Wikipedia，未扩展到其他领域（如科学文献、法律），泛化性未知。
- **LLM 依赖**：数据生成依赖 GPT-4o，可能存在 LLM 自身的偏见或偏移，尽管有人工审核，但审核本身也有主观性。
- **零样本评估局限性**：实验仅在零样本设置下进行，未探索微调或 prompt-tuning 对提升复杂逻辑查询性能的效果。
- **缺乏与现有复杂性基准的对比**：虽然论文提及 NegConstraint 仅关注否定、HotpotQA 仅关注多跳，但未在 ComLQ 上复现这些基准方法或直接比较，削弱了基准的差异化优势论证。
- **计算资源有限**：仅使用单种嵌入模型（bge-small）和一种 LLM（GPT-4o），不同嵌入/LLM 的影响未探索。

（完）
