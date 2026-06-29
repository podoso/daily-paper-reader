---
title: Ground-Truth Subgraphs for Better Training and Evaluation of Knowledge Graph Augmented LLMs
title_zh: 使用真实子图改进知识图谱增强LLM的训练与评估
authors: "Alberto Cattaneo, Carlo Luschi, Daniel Justus"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Sp6znUhP1n"
tags: ["query:llm"]
score: 6.0
evidence: 用于训练LLM的合成知识图谱问答数据集生成
tldr: KG增强LLM的评估缺乏真实标注的数据集。SynthKGQA利用LLM从任意KG生成高质量合成问答数据集，并提供完整真实事实，可用于训练和评估KG检索器，在Wikidata上验证了有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1314, \"height\": 743, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1161, \"height\": 1157, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1437, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 857, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1433, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1224, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1445, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1070, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1228, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1292, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1433, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1304, \"height\": 1421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1582, \"height\": 1932, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1231, \"height\": 1991, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1305, \"height\": 1404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-sp6znuhp1n/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1440, \"height\": 415, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 926, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1442, \"height\": 685, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1449, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1585, \"height\": 2085, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1438, \"height\": 1127, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1548, \"height\": 2383, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1563, \"height\": 2391, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1552, \"height\": 640, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1218, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1442, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1227, \"height\": 398, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-sp6znuhp1n/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1230, \"height\": 377, \"label\": \"Table\"}]"
motivation: 知识图谱增强LLM的对比研究缺乏带有真实目标的问答数据集。
method: 提出SynthKGQA框架，利用LLM从任意知识图谱生成合成问答数据集，包含真实子图事实。
result: 在Wikidata上生成数据集，能训练更好的模型并实现更有信息量的基准测试。
conclusion: 合成数据生成框架有助于推动KG增强LLM的研究。
---

## Abstract
Retrieval of information from graph-structured knowledge bases represents a promising direction for improving the factuality of LLMs. While various solutions have been proposed, a comparison of methods is difficult due to the lack of challenging QA datasets with ground-truth targets for graph retrieval.
We present SynthKGQA, a LLM-powered framework for generating high-quality synthetic Knowledge Graph Question Answering datasets from any Knowledge Graph, providing the full set of ground-truth facts in the KG to reason over each question. We show how, in addition to enabling more informative benchmarking of KG retrievers, the data produced with SynthKGQA also allows us to train better models.
We apply SynthKGQA to Wikidata to generate GTSQA, a new dataset designed to test zero-shot generalization abilities of KG retrievers  with respect to unseen graph structures and relation types, and benchmark popular solutions for KG-augmented LLMs on it.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将根据您提供的论文内容，生成一份结构化、深入且客观的中文总结。

# 论文总结：Ground-Truth Subgraphs for Better Training and Evaluation of Knowledge Graph Augmented LLMs

## 1. 核心问题与研究动机

*   **核心问题：** 大型语言模型在提供事实信息时存在“幻觉”问题。检索增强生成是一种主流的解决方案，其中从知识图谱中检索信息被认为是提升事实准确性的重要方向。然而，当前知识图谱问答领域存在三个关键瓶颈：
    *   **缺乏高质量基准数据集：** 现有数据集中大量问题的事实正确性存疑（估计仅30-60%），且问题多为单跳或简单结构，已接近饱和，难以衡量模型在复杂场景下的真实能力。
    *   **缺乏真实子图标注：** 现有数据集只提供最终答案标签，不提供推理所必需的“真实答案子图”。这使得：
        *   **评估不准确：** 无法独立评估KG检索器的质量，只能进行端到端评估，导致不同模型间的比较充满噪声。
        *   **训练不充分：** 无法为需要监督信号的检索器提供准确训练目标，研究者不得不使用种子实体到答案节点间的“最短路径”作为近似，但这在复杂多跳问题上往往是糟糕的近似。
    *   **数据泄露与时效性问题：** 许多基准数据集基于已停更的Freebase KG，包含过时事实，且问题可能已被LLM在预训练阶段“看到”，导致评估结果虚高。

*   **研究动机：** 为了克服上述局限，需要一种能够自动生成高质量、多样化、带有完整真实子图标注的KGQA数据集的框架，以更好地训练和评估KG增强的LLM。

## 2. 方法论：SynthKGQA

*   **核心思想：** 利用前沿LLM的强大能力，从任意知识图谱中自动生成合成问答数据，并辅以严格的验证流程，确保每个问题都附带了推理所需的完整真实子图（Ground-Truth Subgraphs）。这种方法消除了对人工标注的依赖，并能产生具有高多样性和可控复杂度的数据集。

*   **技术细节与流程（图1）：**
    1.  **种子子图采样：** 从知识图谱中随机采样一个包含约几十条边的连通子图Q作为上下文。
    2.  **候选生成（LLM驱动）：** 将子图Q输入给LLM（如GPT-4.1），通过**少样本提示**要求其生成：
        *   一个问题q，该问题需要从Q中特定的k条边进行推理。
        *   用于推理的真实子图G。
        *   问题的答案a及相关实体。
        *   问题中明确提到的种子实体集合S。
        *   对应自然语言问题的逻辑查询形式（SPARQL查询）。
    3.  **候选验证（SPARQL）：** 这是确保数据质量的关键步骤。将LLM生成的SPARQL查询在真实KG上执行，执行结果与LLM提供的答案进行比对，只有**完全匹配**的候选样本才被保留。这从程序上保证了事实的正确性。
    4.  **增强与分类：** 对验证通过的数据进行后处理：
        *   **释义：** 让另一个LLM对问题进行更自然的改写，增加多样性。
        *   **分类：** 根据真实子图G的**图同构类型**进行复杂度分类，并自动检测问题中的**冗余信息**（即是否存在部分种子实体足以回答问题），为评估提供更精细的维度。

*   **核心优势：** 通过SPARQL验证，从程序上保证了数据的事实准确性，解决了LLM生成数据时“幻觉”的核心问题。

## 3. 实验设计

*   **生成的数据集：GTSQA**
    *   **来源：** 使用SynthKGQA框架和GPT-4.1对Wikidata KG进行生成。
    *   **规模：** 训练集30,477个问题，测试集1,622个问题。
    *   **特性：** 覆盖27种图同构类型（高达5跳、5个种子实体）。训练/测试集刻意划分，专门用于测试模型的**零样本泛化能力**，即测试问题中包含训练中未见的图结构（8种新类型）和未见的关系类型（168种）。
    *   **验证：** 测试集中的问题都经过“可回答性”过滤（GPT-4o-mini在提供真实子图时能100%正确回答），确保其作为基准的可靠性。

*   **Benchmark & 对比方法：**
    *   **评估标准：** 除了最终答案的EM和Recall，更引入了对**检索子图质量**的评估（Recall, Precision, F1 of ground-truth triples）。
    *   **对比模型（分为四类）：**
        1.  **纯LLM基线：** GPT-4.1, GPT-4o-mini, Llama-3.1-8B等，不依赖外部检索。
        2.  **KG Agent（训练无关）：** Think-on-Graph, Plan-on-Graph。多步自主探索KG。
        3.  **路径检索器（需训练）：** SR (RoBERTa), RoG, GCR。预测从种子到答案的关系路径。
        4.  **全量检索器（需训练）：** SubgraphRAG。一次性为邻域内所有边打分。

## 4. 资源与算力

*   论文中**未明确说明**训练和评估所使用的具体GPU型号、数量及训练时长。虽然提到了使用了GPT-4.1等商业模型和可训练的LLaMA-2等开源模型，但关于硬件配置和计算量的具体细节缺失。

## 5. 实验数量与充分性

*   **实验丰富性：** 论文实验设计非常详尽，涵盖了多项核心分析：
    *   **全面基准测试（表2）：** 在GTSQA上比较了7种以上主流KG-RAG模型。
    *   **细粒度性能分析（图2）：** 将模型性能按**图同构类型**分解，精确揭示了模型在不同复杂度问题上的优劣，特别是多种子实体交集问题上的普遍失败。
    *   **零样本泛化分析（图3）：** 明确区分了在分布内、未见关系类型和未见图结构三种情况下的性能差异，提供了深刻的洞察。
    *   **训练信号对比实验（表3, 图C10）：** 这是论文最重要的实验之一。将“真实子图”与传统的“最短路径”作为训练信号，在SR、RoG和SubgraphRAG三种模型上进行对比，并报告了三个独立运行的平均结果和统计显著性p值。
    *   **规模影响分析（图C7）：** 探索了SubgraphRAG中检索子图大小和不同推理LLM对结果的影响。
    *   **相关性分析（图4, 图C6）：** 证明了“真实子图召回率”是比“答案节点召回率”更强的最终性能预测指标。

*   **充分性与客观性：**
    *   **优点：** 实验设计非常系统，逻辑链条完整，从宏观性能到微观原因（泛化、训练信号）都有深入剖析。对比实验设置了统一的推理LLM（GPT-4o-mini），确保了比较的公平性。
    *   **不足：** 算力资源的缺失是一个信息点不足。实验结论对GTSQA这一个生成数据集的有效性非常依赖，虽然文中进行了数据质量验证，但对合成数据本身的普遍性和潜在偏差探讨不足。

## 6. 主要结论与发现

1.  **GTSQA极具挑战性：** 即使是SOTA的KG-RAG模型，在GTSQA上的表现也远未饱和，其多样化的复杂问题能有效揭示现有方法的弱点。
2.  **多种子实体问题是共同瓶颈：** 几乎所有模型都在需要从3个或更多种子实体进行推理相交的任务上表现极差，揭示了对多个信息源进行协调搜索的普遍不足。
3.  **推理LLM能力影响巨大：** 使用更强的LLM（如GPT-5-mini）进行最终推理，能显著提升最终答案的准确性，尤其是在处理大容量、低精度的检索结果时，强LLM能更好地过滤噪声。
4.  **全量检索器优于路径检索器：** SubgraphRAG这类一次性为所有相关边打分的模型在整体上优于路径预测模型（RoG, SR等），尤其是在召回真实子图方面表现突出。
5.  **模型在零样本泛化上的差异：**
    *   **SubgraphRAG** 对未见关系类型泛化能力强，但对未见图结构泛化能力差。
    *   **RoG** 对未见图结构泛化能力强，但对未见关系类型泛化能力差。
    *   **GCR** 对未见关系类型泛化相对更鲁棒。
6.  **使用“真实子图”进行训练至关重要：** 明确证明了用真实子图替代传统的“最短路径”进行训练，能带来**5%到20%**的EM提升。这种优势在多跳问题上尤为显著，因为“最短路径”极易产生“捷径”或“平行路径”等噪声信号。

## 7. 优点

1.  **方法论创新：** 提出了一个实用且可扩展的合成数据生成框架（SynthKGQA），有效解决了KG增强LLM领域长期存在的数据质量、标注缺失和评估噪声问题。
2.  **实验设计严谨：** 实验系统性极强，从多个维度（图结构、关系类型、泛化能力、训练信号）深入剖析问题，且对比公平（统一推理LLM）、结论有强统计支撑。
3.  **贡献巨大：** 不仅提供了一个高质量、有针对性的新基准数据集GTSQA，更重要的是证明了**提供高质量训练信号（真实子图）比提供部分近似信号（最短路径）对于训练更好的检索模型有实质性帮助**，这一发现对领域发展有重要指导意义。
4.  **评估指标先进：** 引入并强调了子图检索质量（GT triple recall/precision/F1）作为评估指标，比仅看最终答案命中率提供了更具诊断性的信息。

## 8. 不足与局限

1.  **依赖LLM质量：** SynthKGQA的生成质量高度依赖于所用的LLM（本文为GPT-4.1），若LLM能力不足，生成的问题质量和多样性可能受限。
2.  **验证逻辑的完备性：** SPARQL验证能确保数据事实正确，但无法保证问题表述的自然性和合理性。文中虽然通过“释义”步骤进行了改善，但“自然”的标准仍可能存疑。
3.  **基准数据集的局限性：** GTSQA的测试集虽然难度大，但规模较小（仅1622个问题），且完全依赖合成数据。这与其他基于人工或真实用户查询构建的基准（如WebQSP）在“真实性”上存在差异。
4.  **泛化能力的定义：** 零样本泛化的测试（未见图结构、未见关系类型）是基于一个特定、静态的KG和特定模型初次训练时的知识。模型的泛化能力是否会随着在更大型、不同分布的合成数据上训练而改变，文中没有探讨。
5.  **对其他KG的验证不足：** 框架虽然声称可用于“任意KG”，但所有实验仅基于Wikidata（或其子集ogbl-wikikg2），其在其他知识库上的有效性和通用性尚待证明。
6.  **计算成本：** 生成数据集需要反复调用大型LLM（如GPT-4.1）和查询真实KG，成本较高。训练GCR等依赖KG Trie索引的模型也面临不小的时空开销。

（完）
