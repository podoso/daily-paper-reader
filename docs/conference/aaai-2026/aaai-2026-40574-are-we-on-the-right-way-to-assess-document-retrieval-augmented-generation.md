---
title: Are We on the Right Way to Assess Document Retrieval-Augmented Generation?
title_zh: 我们是否正走在评估文档检索增强生成的正路上？
authors: "Wenxuan Shen, Mingjia Wang, Yaochen Wang, Dongping Chen, Junjie Yang, Yao Wan, Weiwei Lin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40574/44535"
tags: ["query:multimodal"]
score: 4.0
evidence: 多模态大语言模型在文档RAG评估中的应用
tldr: 针对当前文档检索增强生成（RAG）系统评估基准存在的局限性，如聚焦于系统特定组件、使用合成数据且标签不完整等问题，本文提出了Double-Bench，一个大规模、多语言、多模态的评估系统，能够对文档RAG的每个组件进行细粒度评估。该基准包含3276份文档（72880页）和5168个跨6种语言和4种模态的单跳及多跳查询，为RAG评估提供了更真实全面的标杆。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有文档RAG系统评估基准无法反映真实世界的瓶颈和挑战，阻碍了系统发展。
method: 构建了一个包含多语言多模态文档和查询的大规模基准，支持对各组件细粒度评估。
result: Double-Bench包含3276份文档和5168个查询，覆盖6种语言和4种模态。
conclusion: 该评估系统为文档RAG提供了更全面真实的测试环境。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems using Multimodal Large Language Models (MLLMs) show great promise for complex document understanding, yet their development is critically hampered by inadequate evaluation. Current benchmarks often focus on specific part of document RAG system and use synthetic data with incomplete ground truth and evidence labels, therefore failing to reflect real-world bottlenecks and challenges. To overcome these limitations, we introduce Double-Bench: a new large-scale, multilingual, and multimodal evaluation system that is able to produce fine-grained assessment to each component within document RAG systems. It comprises 3,276 documents (72,880 pages) and 5,168 single- and multi-hop queries across 6 languages and 4 document types with streamlined dynamic update support for potential data contamination issues. Queries are grounded in exhaustively scanned evidence pages and verified by human experts to ensure maximum quality and completeness. Our comprehensive experiments across 9 state-of-the-art embedding models, 4 MLLMs and 4 end-to-end document RAG frameworks demonstrate the gap between text and visual embedding models is narrowing, highlighting the need in building stronger document retrieval models. Our findings also reveal the over-confidence dilemma within current document RAG frameworks that tend to provide answer even without evidence support. We hope our fully open-source Double-Bench provide a rigorous foundation for future research in advanced document RAG systems. We plan to retrieve timely corpus and release new benchmarks on an annual basis.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前文档检索增强生成（RAG）系统的评估基准存在严重缺陷，导致无法真实反映实际应用的瓶颈与挑战。
- **具体表现**：现有基准（如DocVQA、ViDoRe、MMLongBench-Doc等）存在四大局限：
  1. **评估范围有限**：仅聚焦于RAG系统的某个组件（如嵌入模型或VQA模型），缺乏对整体系统的细粒度分解评估。
  2. **不现实的先验知识假设**：许多VQA基准预设给定文档或页面位置，不适合评估真实场景中的全局检索。
  3. **模糊或非唯一证据**：合成查询常假设一对一的查询-证据映射，忽略了多页相关的情况。
  4. **未链接的多跳组合**：多跳查询常由松散连接的单跳组成，无法真正测试跨文档、跨模态的多跳推理能力。
- **整体含义**：为了推动文档RAG系统的发展，需要建立一个大规模、多语言、多模态、带人工验证的细粒度评估系统。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：构建一个三阶段流水线，自动合成高质量单跳和多跳查询，并通过人工精炼确保标签完整性，从而对RAG系统的检索、生成等各组件进行独立评估。
- **关键技术细节**：
  - **第一阶段：元数据收集与预处理**
    - 收集4类文档（PDF、扫描文档、幻灯片、HTML页面），覆盖6种语言（AR、ZH、EN、FR、JA、ES）。
    - **两阶段过滤**：粗粒度规则过滤（结构、语言要求） + 细粒度内容过滤（语义连贯性）。
    - **模态拆分**：使用Docling、MinerU将每页拆分为文本、表格、图片等模态。
  - **第二阶段：查询合成**
    - **单跳查询**：基于解析后的页面组件，利用GPT-4o根据4条原则（自包含、聚焦重要模态内容、禁止显式引用、多样自然性）生成初始查询。通过迭代清晰度优化：用Colqwen和Qwen3-Embedding检索top-10候选页，Qwen2.5-VL-32B验证证据页数量；若超过5个证据页，则添加区分细节后重新生成。
    - **多跳查询**：为每篇文档构建知识图谱（LightRAG），从高连接度节点开始，由LLM推理查询意图，沿图遍历选取邻居节点，逐步累积子问题形成连贯的多跳问题。确保每一步推理的必要性和唯一性。
  - **第三阶段：后处理**
    - **质量检查**：单跳查询检查清晰度等；多跳查询检查逻辑必要性、答案唯一性等。不合格者丢弃。
    - **证据标注**：人工逐页扫描文档，为单跳提供证据集标签，为多跳提供链式证据标签。
    - **人工精炼**：专业标注员修正8%的自动标注差异（96%一致性），保障数据质量。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：Double-Bench本身（3,276篇文档，72,880页，5,168个查询，6语言，4种文档类型）。查询包括单跳和多跳（2-hop、3-hop）。
- **评估指标**：
  - 检索准确率：hit@1、hit@3、hit@5。
  - 回答准确率：LLM-as-a-judge（GPT-4o评分0-10），>=7为正确，<=3为错误，其余为部分正确。
- **对比方法**：
  - **文本嵌入模型**：bge-m3、gte-Qwen2-7B-instruct、NV-Embed-v2、Qwen3-Embedding-4B（4个）。
  - **视觉/多模态嵌入模型**：colpali-v1.3、colqwen2.5-3b-multilingual、gme-Qwen2-VL-7B-Instruct、vdr-2b-multi、jina-embeddings-v4（5个）。
  - **MLLMs（无RAG和Oracle设置）**：Qwen3-32B text-only、Qwen2.5-VL-7B/32B、GPT-4o、Llama4 Maverick（5个）。
  - **文档RAG框架**：M3DocRAG、MDocAgent、ViDoRAG、Colqwen-gen（将最强嵌入Colqwen与GPT-4o直接配对，作为参考）。此外，还评估了Oracle设定（直接提供所有证据页）作为上界。

## 4. 资源与算力
- **未明确说明**：论文未报告训练/推理所用的GPU型号、数量、时长等具体信息。实验使用了多个商业API（如GPT-4o）和开源模型，但未提供硬件细节。因此无法总结算力消耗。

## 5. 实验数量与充分性
- **实验数量**：大量对比实验，包括：
  - 9个嵌入模型在单跳、2-hop、3-hop上的hit@1/3/5（共27组检索指标）。
  - 5个MLLM在无RAG和Oracle设定下的回答准确率（两种设置各5组）。
  - 4个RAG框架的检索+回答准确率（共4组，含多跳分解）。
  - 深入分析：过置信行为分解、时间效率、推理模式（附录）。
- **充分性判断**：
  - **公平性**：各模型采用标准配置，基准开源，超参数固定；检索与生成组件独立评估，对比合理。
  - **充分性**：覆盖了主流嵌入模型、MLLM和完整RAG框架，且对多跳难度进行了分层分析；但缺乏对更大规模框架（如基于不同LLM的变体）的测试。总体而言，实验设计系统、客观，能够验证基准的有效性和当前系统的局限性。

## 6. 论文的主要结论与发现
- **检索层面**：
  - 文本与视觉嵌入模型差距缩小，Colqwen2.5-3b最强（平均hit@5=0.795）。
  - 高资源语言（如英语）检索性能优于低资源语言（如阿拉伯语、法语）。
  - 结构化文档（PDF、HTML）检索更容易。
- **回答层面**：
  - 无RAG时，MLLM仅有50-70%部分正确；提供Oracle证据页后，完全正确率提升3-5倍。
  - 多跳查询对当前RAG框架极具挑战，即使提供所有证据页，准确率也仅0.655。
- **框架行为**：
  - 现有RAG框架存在**过置信困境**：当检索失败时，框架仍倾向于给出答案，而非拒绝回答。简单框架（M3DocRAG）更保守，复杂框架（MDocAgent、ViDoRAG）更过度自信。
  - **检索精度与回答精度强相关**：优化检索阶段比设计复杂推理流程更关键。Colqwen-gen（仅单次MLLM传递）在多跳查询上甚至部分优于MDocAgent。
- **推理模式**：MLLM处理多跳查询时并非按步推理，而是先收集各跳中的“签名信息”，再通过包含/排除快速得出答案。仅增加跳数不一定增加难度。

## 7. 优点：方法或实验设计上的亮点
- **基准质量高**：大规模（3276文档、5168查询）、多语言（6种）、多模态（4种文档类型）；人工验证证据标签，确保完整性和低歧义。
- **细粒度评估**：支持对RAG系统每个组件（检索、生成、框架策略）独立评估，揭示组件交互瓶颈。
- **发现关键问题**：揭示过置信困境和检索瓶颈，为后续研究指明方向。
- **开源与可扩展**：提供自动化流水线，支持动态更新以避免数据污染，社区可持续贡献。
- **实验设计严谨**：分别评估无RAG、Oracle、真实RAG三种设定，并使用LLM-as-a-judge进行多级评分（正确/部分/错误），避免二元判断的粗糙性。

## 8. 不足与局限
- **合成数据依赖**：尽管经过人工精炼，但查询仍由LLM生成，可能引入模型偏好或特定模式，不完全代表真实用户自然查询分布。
- **文档覆盖有限**：仅包括4种类型和6种语言，未覆盖手写文档、表单、复杂学术PDF等；低资源语言样本较少。
- **框架评估不完全**：仅测试4个RAG框架，未包含其他流行方法（如CRAG、Self-RAG、自适应RAG等）；且所有框架均使用默认配置，未进行超参数调优。
- **算力开销未报告**：未提供计算资源消耗，不利于可复现性评估。
- **评分方法争议**：使用GPT-4o作为评判标准，可能对自身产物有偏见，且对部分正确情况的分界（7/10）可能欠鲁棒。
- **多跳查询难度层次**：虽然设计了知识图谱遍历，但部分多跳查询仍可能被模型通过强先验知识直接回答，削弱评估有效性。
- **未测试实时效率**：实验未关注推理延迟、资源占用等实际部署指标。

（完）
