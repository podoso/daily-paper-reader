---
title: "ARTEM: Enhancing Large Language Model Agents with Spatial-Temporal Episodic Memory"
title_zh: ARTEM：利用时空情景记忆增强大语言模型智能体
authors: "Cassandra Hui-Ming Tan, Budhitama Subagdja, Ah-Hwee Tan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39773/43734"
tags: ["query:llm"]
score: 6.0
evidence: 利用时空情景记忆增强大语言模型智能体
tldr: 大语言模型在长期时间依赖的情景记忆任务中存在不足。本文提出ARTEM架构，将LLM与自组织时空情景记忆网络结合，实现时间感知的记忆编码、存储和检索。实验证明该方法在情景记忆任务上优于现有方法，为LLM长期记忆能力提供了新方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: LLM在编码、存储和检索时间依赖事件的能力严重不足。
method: 设计混合LLM智能体架构，集成自组织时空情景记忆网络以实现时间感知记忆。
result: 在情景记忆任务中显著优于上下文学习、RAG和微调等方法。
conclusion: 该方法为LLM提供了长效记忆机制，有助于处理依赖时间顺序的任务。
---

## Abstract
Current large language models (LLMs) exhibit significant deficiencies in episodic memory tasks including encoding, storing, and retrieving specific information from temporally dependent events over a long period of time. Recent approaches to handle memory tasks in LLMs, such as in-context learning, retrieval-augmented generation (RAG), and fine-tuning, may resolve the long-term retention issues, but are still inadequate to handle tasks requiring chronological awareness of the stored information. We introduce Agentic Retrieval with Temporal-Episodic Memory (ARTEM), a hybrid LLM-based agent architecture integrating LLMs with a self-organizing neural network named Spatial-Temporal Episodic Memory (STEM), designed to handle episodic memory tasks. Our approach employs LLMs for event extraction from the inputs to represent temporal, spatial, entitative, and semantic information that may facilitate future retrieval, aside from generating outputs or direct responses. The extracted events can then be encoded vectorially and stored in a fast and stable manner in the episodic memory through an instance-based incremental learning in STEM. STEM supports precise episodes retrieval and helps reduce computational overhead in generating the appropriate responses by LLMs. Evaluation on standardized episodic memory benchmarks across four tasks—partial cue retrieval, epistemic uncertainty detection, recent event identification, and chronological recall—demonstrates superior performance of ARTEM compared to in-context learning, RAG, and fine-tuning in various popular LLMs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

当前大语言模型（LLM）在情景记忆（episodic memory）任务上存在显著不足：它们难以编码、存储和长期检索具有时间依赖性的特定事件信息。现有解决方案（如上下文学习、检索增强生成 RAG、微调）虽然能部分缓解长期记忆问题，但在需要时间顺序意识（chronological awareness）的任务中表现仍然不佳。为此，论文提出一种混合架构 **ARTEM**（Agentic Retrieval with Temporal-Episodic Memory），将 LLM 与一个自组织神经网络 **STEM**（Spatial-Temporal Episodic Memory）结合，专门用于处理情景记忆任务。

## 2. 论文提出的方法论

### 核心思想
利用 LLM 作为事件提取和问答智能体，同时利用 STEM 作为结构化记忆存储和检索模块，实现时间感知的记忆编码与高效检索。

### 关键技术细节
- **事件提取**：LLM 从输入文本中提取时间、空间、实体、语义四类信息，并格式化为标准化 JSON 供 STEM 编码。
- **STEM 记忆网络**：
  - 四个编码通道：Channel 0（时间）、Channel 1（空间）、Channel 2（实体）、Channel 3（内容）。
  - 时间使用全局**最小-最大归一化**：$\tau_{\text{norm}} = \frac{\tau - \tau_{\min}}{\tau_{\max} - \tau_{\min}}$。
  - 语义通道（1-3）使用**每向量最小-最大归一化**：$v_{\text{norm}} = \frac{v - v_{\min}}{v_{\max} - v_{\min}}$。
  - 事件表示为 $e = (t, s, ent, c)$，各通道嵌入维度为 384（SentenceTransformer all-MiniLM-L6-v2）。
- **智能检索**：基于**警惕性（vigilance）** 参数 $\rho$ 控制检索精确度；匹配分数 $m_{kj} = \frac{|I_k \land w_{kj}|}{|I_k|}$（模糊交运算）。
- **三种时间访问策略**：
  - 完整访问（all）：返回所有匹配事件。
  - 最新访问（latest）：返回最晚事件。
  - 时间顺序访问（chronological）：按时间排序返回。
- **LLM 集成**：
  - 事件提取：温度 0.1 的确定性采样。
  - 答案生成：将 STEM 检索结果作为上下文给 LLM，强调事实准确性和时间连贯性。
  - 自动评估：采用“LLM-as-a-Judge”方法计算精确率、召回率和 F1。

## 3. 实验设计

- **数据集**：使用 **Episodic Memory Benchmark**（Huet, Houidi, Rossi 2025）中的合成长书数据集 “Synaptic Echoes”，包含 200 章、102,870 个 token。
- **基准任务**：四项标准情景记忆任务：
  - 局部线索检索（Partial Cue Retrieval）
  - 认知不确定性检测（Epistemic Uncertainty Detection）
  - 最新事件识别（Recent Event Identification）
  - 时间顺序回忆（Chronological Recall）
- **对比方法**：
  - 上下文学习（In-context）：GPT-4o-mini, GPT-4o, Claude-3-haiku, Claude-3.5-sonnet, o1-mini, Llama-3.1-405b
  - RAG：GPT-4o-mini, GPT-4o, Claude-3-haiku, Claude-3.5-sonnet
  - 微调：GPT-4o-mini
  - 基准模型（零样本）：Gemini-2-pro, Gemini-2-flash-thinking, DeepSeek-v3, etc.

## 4. 资源与算力

论文明确指出使用 **4 块 NVIDIA L40S GPU（每块 48GB 内存）** 进行大规模处理。未给出具体训练时长或推理步数。STEM 是一种快速增量学习方法，无需传统训练循环；LLM 调用为前向推理，整体算力需求相对较低。

## 5. 实验数量与充分性

- **主实验数量**：
  - STEM 模型：在 600 个查询上评估（表1）。
  - ARTEM 模型：在 548 个查询上评估（表2，52 个因 token 超限或解析失败被丢弃）。
  - 对比实验：表3 涵盖了 10 个不同基线模型在 5 个事件复杂度 bin 上的详细 F1 值。
  - 时间推理基准：表4 比较了 17 个模型在简单回忆和时间顺序任务上的 F1。
- **充分性评价**：实验设计较为全面，覆盖了四项核心任务、多种记忆架构和多种 LLM 规模。消融分析通过分开 STEM 和 ARTEM 进行，分析了 vigilance 参数、时间访问策略的影响。但实验仅基于单一合成数据集，缺乏真实场景验证，是主要局限。对比方法包括了主流 ICL、RAG 和微调，但未与 MemGPT 等更专门的记忆增强系统比较。

## 6. 论文的主要结论与发现

- **STEM 在认知不确定性检测上达到完美（F1=1.0）**，ARTEM 接近完美（F1=0.95），极大缓解了幻觉问题。
- **STEM 在时间顺序回忆任务上取得 SOTA（F1=0.644）**，ARTEM 为 0.585，而最强竞品 Gemini-2-pro 仅为 0.290，优势达 **2–19 倍**。
- ARTEM 通过 LLM 合成，在单事件检索上优于 STEM（F1 0.68 vs 0.55），但整体 F1 略低（0.691 vs 0.707），受限于 LLM token 限制和提取错误。
- 推理优化模型（如 o1、o3-mini）在时间顺序任务上表现极差（F1 0.052 和 0.044），说明通用推理能力不等于时间序列理解能力。

## 7. 优点

- **生物启发性**：基于自适应共振理论（ART）的 STEM 网络，具有明确的编码-检索机制，可解释性强。
- **抗幻觉能力强**：通过警惕性阈值控制，在信息不足时主动拒答，优于所有对比方法。
- **时间感知能力强**：明确的时间通道和归一化策略，使系统能精确维护事件顺序。
- **模块化混合架构**：LLM 与 STEM 解耦，可以灵活替换 LLM 或调整记忆参数。
- **计算效率高**：增量学习无需大量训练，检索复杂度低。

## 8. 不足与局限

- **依赖合成数据集**：仅使用 “Synaptic Echoes” 一个合成长书，缺乏真实世界场景验证，泛化性存疑。
- **LLM 依赖与误差传播**：事件提取和答案生成依赖 LLM 能力，提取错误或解析失败会导致性能下降（52 个查询被丢弃）。
- **警惕性参数敏感**：性能对 vigilance 参数的校准非常敏感，尤其单事件场景下窗口窄。
- **Token 限制**：ARTEM 因 LLM 上下文长度限制丢弃了部分复杂查询（3–5 bin 以上），可能引入选择偏差。
- **未与更先进的记忆系统比较**：如 MemGPT、MemoryBank 等基于长期记忆的专门架构缺少直接对比。
- **评估方法局限**：采用 LLM-as-a-Judge 可能存在偏差，评估标准依赖于另一个 LLM 的判断。

（完）
