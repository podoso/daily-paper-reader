---
title: "R$^2$AG: Rethinking Retrieval-Augmented Generation via Multimodal Coherence Understanding"
title_zh: R$^2$AG：通过多模态连贯性理解重新思考检索增强生成
authors: "Jing Tang, Weizhi Du, Siyuan Yuan, Jiechao Gao"
date: 2025-09-10
pdf: "https://openreview.net/pdf?id=KQL9UuQv6k"
tags: ["query:multimodal"]
score: 7.0
evidence: 通过属性图理解多模态连贯性的多模态检索增强生成
tldr: 多模态检索增强生成难以捕捉文本和视觉元素间的复杂结构关系。R$^2$AG将多模态内容表示为属性图中的节点和边，通过隐式思维链处理图复杂度，显著提升多模态连贯性理解。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-kql9uuqv6k/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1360, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-kql9uuqv6k/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1316, \"height\": 1114, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1348, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1383, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1270, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1475, \"height\": 878, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1493, \"height\": 877, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1443, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1423, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1558, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1346, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1387, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1418, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1498, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kql9uuqv6k/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1567, \"height\": 313, \"label\": \"Table\"}]"
motivation: 现有MRAG难以准确捕捉多模态内容间的复杂结构关系。
method: 将多模态内容表示为属性图，使用隐式思维链高效推理多级关系。
result: 显著提升多模态连贯性理解。
conclusion: 图表示与思维链结合有效改进MRAG。
---

## Abstract
While Multimodal Retrieval-Augmented Generation (MRAG) has shown promise in enhancing large language models, existing approaches are difficult to accurately capture the complex structural relationships between text and visual elements. This paper introduces R$^2$AG  (Rethinking Retrieval-Augmented Generation), a novel framework that extends MRAG to multimodal multi-level property graphs, significantly improving multimodal coherence understanding. Our approach represents multimodal content as interconnected nodes and edges in a property graph, capturing semantically rich relationships beyond conventional embedding distances. To address the exponential growth of graph complexity with additional hops, we propose an Implicit Chain-of-Thought (Implicit-CoT) technique that efficiently partitions and analyzes local subgraphs while deriving comprehensive features from both node semantics and structural properties. Additionally, we develop an improved graph matching algorithm that not only considers feature consistency but also recognizes semantic approximations and prioritizes rare entities, enhancing matching accuracy and robustness. Extensive experiments on public datasets demonstrate that R$^2$AG outperforms state-of-the-art methods in multiple tasks requiring deep multimodal coherence understanding. Our code is available at \url{https://anonymous.4open.science/r/R2AG-4F58/}.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有多模态检索增强生成（MRAG）方法主要依赖单模态统一表示进行特征空间嵌入距离计算，难以准确捕捉文本和视觉元素之间复杂的**结构关系**（如多层属性图关系），导致多模态连贯性理解不足，且容易产生多模态幻觉。
- **核心问题**：如何将多模态内容组织成结构化图（多模态多级属性图），并利用图结构信息来提升大语言模型在多模态任务中的生成质量和连贯性。
- **整体含义**：提出 R²AG 框架，通过引入属性图表示、隐式思维链推理和改进的图匹配算法，显著增强了多模态内容的检索与生成能力，填补了传统 RAG 在多模态结构化理解方面的空白。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将多模态内容（文本、图像）表示为多模态多级属性图（MMPG）中的节点和边，利用图拓扑结构捕捉超越嵌入距离的语义关系；通过隐式思维链（Implicit-CoT）高效处理图复杂增长；通过改进的图匹配算法——软加权多模态 Jaccard 相似度（Soft-Weighted Multimodal Jaccard Similarity, SWMJS）实现更精确的检索。

- **关键技术与流程**：
  1. **提取 MMPG**：
     - 文本清洗（NLP 管道、TF-IDF 过滤、Levenshtein 校正等）；图像处理（小波去噪、直方图均衡、双三次插值等）。
     - 对用户查询 Q 进行初步检索得到文档集合 D；通过多编码器架构（文本+视觉）生成节点嵌入，建立异构图，其中节点为语义单元，边为跨模态关系。
  2. **多模态连贯性理解**：
     - **隐式思维链（Implicit-CoT）**：
       - Step 1: 隐式关系抽取——基于上下文和显式关系集，让 LLM 发现隐藏的连接，生成高阶关系三元组，如式 (1): \(E_i' = \bigcup_{i,j \in V} \{(v_i, v_j, e_k)\}\)。
       - Step 2: 关系验证——利用 LLM 自验证能力对每个三元组分配置信度 \(V(i,j,k)\)，过滤低于阈值 \(v_{th}\) 的关系，如式 (2): \(E_i = \bigcup_{i,j \in V, V(i,j,k) \ge v_{th}} \{(v_i, v_j, e_k)\}\)。
       - Step 3: 优化 MMPG 构建——整合显式与隐式关系，求解条件概率最大化，如式 (3): \(G = \arg\max_{G_i} P(G_i | V, E = [E_e, E_i], I, T, Q)\)。
     - **改进的图匹配算法（SWMJS）**：
       - 算法核心：对文本实体集 T 和图像实体集 I，计算每个实体与另一集合中相似度超过阈值 τ 的最大相似度，并用 IDF 权值加权，最终计算加权交集除以并集（详见附录 A.6 的 Algorithm 1）。该算法能处理同义词、复数、拼写差异，并给稀有实体更高权重。
  3. **多模态生成**（三阶段）：
     - 语义内容初始化：基于检索文档生成初始文本 \(T_0\)。
     - 视觉嵌入决策：将文本分段，通过 MLLM 确定图像嵌入位置。
     - 内容融合优化：将视觉元素与文本融合，优化每个段落，生成结构化图标记（Graph tokens），最后输入 MLLM 生成最终多模态输出 \(O_m\)。

## 3. 实验设计：数据集、场景、benchmarks、对比方法

- **数据集**：使用 M2RAG 论文中的数据，并抽象为五个经典任务：视觉问答（Visual Question Answering）、多模态理解（Multimodal Understanding）、多模态生成（Multimodal Generation）、跨模态检索（Cross-modal Retrieval）、多模态对话（Multimodal Dialogue）。最终整理出 1200 条测试数据。
- **基准模型**：基于 Qwen（Wang et al., 2024a）实现。
- **对比方法**：MuRAR、EchoSight、M2RAG（均为 SOTA 方法）。
- **评估指标**：
  - 主观指标（文本维度）：流畅度（Flu.）、相关性（Rel.）、上下文精度（CP.）、忠实度（Faith.），由 GPT-4 和人类评估者打分（满分 100）。
  - 主观指标（视觉维度）：连贯性（Coher.）、有帮助性（Help.）、参考质量（Ref.）、召回率（Recall），同样由 GPT-4 和人类评估。
  - 客观指标：FVD（越低越好，评估真实性）、CLIP Score（越高越好，评估图文对齐）、DOVER（越高越好，评估内容忠实度和描述连贯性）。

## 4. 资源与算力

- **未明确说明**：论文中未提及 GPU 型号、数量、训练时长等算力资源信息。仅说明代码已公开，未提供硬件配置。

## 5. 实验数量与充分性

- **实验数量**：
  - 主观文本指标：在 5 个任务上分别报告 M2RAG 和 R²AG 的 GPT-4 及人类评分（表 4）。
  - 主观视觉指标：类似地，5 个任务上分别报告（表 5）。
  - 客观指标：5 个任务上分别报告 FVD、CLIP Score、DOVER（表 6）。
  - 对比不同架构能力（表 7）：多级检索、多主体推理、知识集成。
  - 对比 MMKG 与多级 MMKG（表 8）。
  - 消融实验：
    - 消融 ICoT 和 SWMJS 组件（表 9、表 10）。
    - 消融图像 token（表 11）。
  - 不同基础模型对比：Llama-3.1-8B-Instruct、Qwen2-VL-7B-Instruct、Qwen2.5-VL-7B-Instruct（表 12、表 13）。
- **充分性评价**：
  - **较充分**：覆盖多个任务、多种指标，同时使用了自动评估和人工评估；进行了消融研究和基础模型泛化实验。
  - **待改进**：
    - 未说明数据集的具体名称，可能影响可复现性。
    - 未报告重复实验次数或统计显著性检验（如 p 值、置信区间）。
    - 主观评估中 GPT-4 评分普遍高于人类，可能存在系统性偏差，但作者指出趋势一致。

## 6. 论文的主要结论与发现

- R²AG 在所有主观和客观指标上**全面超越** SOTA 方法 MuRAR、EchoSight 和 M2RAG。
- 在文本维度：R²AG 的流畅度和相关性显著提升（GPT-4 评分分别达 88.2/100 和 89.2/100 vs M2RAG 的 80.6 和 79.4）。
- 在视觉维度：R²AG 的连贯性和有帮助性均优于对比方法。
- 客观指标：R²AG 的 FVD 大幅降低（12.45 vs M2RAG 18.02），CLIP Score 和 DOVER 均有显著提升。
- 消融实验证实 ICoT 和 SWMJS 组件均为性能提升的关键。
- 不同基础模型（Llama-3.1、Qwen2-VL、Qwen2.5-VL）下 R²AG 均能取得一致改进，证明了框架的模型无关性。

## 7. 优点

- **方法创新**：将多模态 RAG 拓展到多级属性图，引入隐式思维链处理图结构复杂增长，提出软加权多模态 Jaccard 相似度改进图匹配，具有理论新颖性和实用性。
- **实验设计全面**：覆盖 5 种经典多模态任务，使用 GPT-4 和人类双重评估，主客观指标结合，消融实验完整，并验证了模型无关性。
- **可复现性**：提供了开源代码。
- **缓解幻觉**：通过显式结构化关系和单跳验证，有效减少了多模态幻觉。

## 8. 不足与局限

- **数据集不明确**：未给出公开数据集的具体名称，仅说明来自 M2RAG 论文，可能影响他人复现和对比。
- **算力信息缺失**：未报告训练/推理所需 GPU 型号、数量、时间，不利于评估资源需求。
- **统计显著性缺失**：未进行多次重复实验或显著性检验，结果稳定性存疑。
- **主观评估偏差**：GPT-4 的评分系统与人类评分存在系统差异（GPT-4 普遍给更高分），虽然趋势一致，但绝对分数可能不可靠。
- **语言局限**：实验仅针对英文数据，未讨论多语言或跨文化场景。
- **图复杂度处理**：ICoT 虽能缓解指数增长，但理论上对极大规模图仍可能面临效率瓶颈，论文未讨论扩展性。
- **应用限制**：方法依赖 LLM 的推理和验证能力，对较弱基础模型可能效果受限；且需要构建属性图，预处理成本较高。

（完）
