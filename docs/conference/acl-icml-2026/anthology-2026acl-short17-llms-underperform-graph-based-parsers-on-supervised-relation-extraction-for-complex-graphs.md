---
title: LLMs Underperform Graph-Based Parsers on Supervised Relation Extraction for Complex Graphs
title_zh: 大语言模型在复杂图监督关系抽取中表现不如图解析器
authors: "Paolo Gajo, Domenic Rosati, Hassan Sajjad, Alberto Barrón-Cedeño"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-short.17.pdf"
tags: ["query:ie"]
score: 7.0
evidence: 关系抽取中图解析器与LLM性能比较
tldr: 该论文在六个关系抽取数据集上比较了四种大语言模型与图解析器的性能，发现当文本语言图复杂度增加时，图解析器显著优于LLM，揭示了LLM在复杂关系抽取任务上的局限性。
source: ACL-2026-Short
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.17/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.17/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 1093, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.17/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1609, \"height\": 1183, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.17/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1070, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.17/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1661, \"height\": 1218, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.17/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.17/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.17/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1605, \"height\": 1060, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.17/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1506, \"height\": 836, \"label\": \"Table\"}]"
motivation: 探究大语言模型在复杂语言图关系抽取任务上的实际性能。
method: 在六个指标数据集上比较四种LLM与图解析器的关系抽取性能。
result: 图解析器在复杂文本上的关系抽取效果显著优于LLM。
conclusion: LLM在复杂关系抽取场景下仍有局限，图解析器仍是强有力选择。
---

## Abstract
Relation extraction represents a fundamental component in the process of creating knowledge graphs, among other applications. Large language models (LLMs) have been adopted as a promising tool for relation extraction, both in supervised and in-context learning settings. However, in this work we show that their performance still lags behind much smaller architectures when the linguistic graph underlying a text has great complexity. To demonstrate this, we evaluate four LLMs against a graph-based parser on six relation extraction datasets with sentence graphs of varying sizes and complexities. Our results show that the graph-based parser increasingly outperforms the LLMs, as the number of relations in the input documents increases. This makes the much lighter graph-based parser a superior choice in the presence of complex linguistic graphs.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：关系抽取（RE）是构建知识图谱等应用的基础任务。近年来，大型语言模型（LLM）因其强大的语言理解能力被广泛用于关系抽取（包括监督学习和上下文学习场景），但现有研究缺乏LLM与轻量级图解析器在监督设置下的直接比较。
- **核心问题**：随着文本语言图（linguistic graph）复杂度的增加（即文档中实体和关系的数量增多），LLM是否仍能保持优势？图解析器是否在复杂图上表现更优？
- **整体含义**：论文揭示了LLM在处理复杂语言图时的局限性，提示研究者和实践者：在涉及大量关系（例如超过约18条边）的文本时，轻量级图解析器可能是更合适的选择。

## 2. 论文提出的方法论

- **核心思想**：系统地比较LLM与图解析器在关系抽取任务上的性能，特别关注输入文档中关系数量（即图复杂度）对性能的影响。
- **关键技术细节**：
  - **图解析器**：基于Dozat & Manning (2017)的双仿射注意力解析器，并扩展了Bhatt等(2024)的架构。包含编码器（冻结的BERT，110M参数）、可选的词性标注器、可选的双向LSTM层（Lψ）和可选图注意力网络层（Lϕ），最后通过双仿射函数计算边分数和关系分数。解码阶段使用Chu-Liu/Edmonds最大生成树算法以保证生成有效的树结构。总共可学习参数最多14M，加上冻结BERT共124M参数。
  - **LLM**：使用4种不同规模的LLM：Mistral-7B-Instruct-v0.3（7B）、Qwen3-14B-Base（14B，未指令微调）、Qwen3-32B（32B）、Llama-3.3-70B-Instruct（70B）。微调采用LoRA（r=a=16），仅微调注意力层的key、query、value权重。
  - **提示设计**：包括四种提示变体：无描述（NoDesc）、有描述（Desc）、仅UUID代码、对抗性提示（要求模型不执行任务）。对比不同提示对微调性能的影响。
  - **训练策略**：图解析器训练3k步（k为训练样本数），每500步评估；LLM训练1个epoch或3k步；使用AdamW优化器；图解析器学习率1e-3，LLM学习率2e-4，batch size分别为8和1。
- **评估指标**：精确匹配的微F1（micro-F1），要求三元组实体和关系完全匹配。

## 3. 实验设计

- **数据集**：使用6个覆盖不同图复杂度的数据集：
  - **简单图**（多数样本关系数≤5）：CoNLL04（新闻文本，平均1.42关系）、ADE（药物不良反应报告，平均1.59）、SciERC（科学文献，平均2.38）
  - **中等图**：enEWT（英语网络树库，平均17.83关系）、SciDTB（科学摘要话语树库，平均23.41）
  - **复杂图**：ERFGC（烹饪食谱流图，平均49.19关系，最多167）
- **对比方法**：
  - 四种LLM（Mistral-7B、Qwen3-14B、Qwen3-32B、Llama-3.3-70B）在不同提示和ICL设置下评估。
  - 图解析器（多种BiLSTM层数和GAT层数配置，共4×4=16种组合，表6）。
  - LLM基线：未微调的零样本/少样本性能。
- **基准**：各数据集的标准测试划分，精确匹配F1。

## 4. 资源与算力

- **GPU型号**：LLM微调使用NVIDIA L40s和H100s；LLM推理使用相同GPU（需3-6小时）；图解析器训练使用NVIDIA P100s和Tesla V100s。
- **训练时长**：LLM微调每个模型/数据集组合耗时30分钟至18小时；图解析器每个训练运行约10分钟。
- **资源说明**：论文未明确GPU数量，但提到“computational constraints”导致对更大模型使用更少种子实验和部分数据集采样（如Qwen3-14B和Qwen3-32B在enEWT和SciDTB上只评估100样本，Llama-3.3-70B在所有数据集上只评估100样本）。

## 5. 实验数量与充分性

- **实验数量**：
  - 图解析器：16种架构配置（BiLSTM层数0-3 × GAT层数0-3），每种5个种子，在6个数据集上训练评估。
  - LLM：4种模型，多种提示和ICL变体，部分模型多个种子（Mistral-7B: 5种子；Qwen3-14B: 4种子；Qwen3-32B: 3种子；Llama-3.3-70B: 1或5种子），微调1 epoch或3k步。
  - 总计数十组实验。
- **充分性与公平性**：
  - 优点：覆盖了从简单到极复杂的图结构；使用相同评估指标（精确匹配F1）；控制训练步数（部分LLM也训练3k步）；报告了方差（表4显示方差很低）。
  - 不足：由于计算限制，部分LLM在大数据集上只评估子集（100样本），可能引入采样偏差；只使用了一种图解析器架构；未进行定性错误分析；LLM训练步数未完全对齐（图解析器3k步 vs LLM 1 epoch,但部分LLM也做了3k步）。

## 6. 论文的主要结论与发现

- **核心发现**：在简单图（关系数≤5）上，LLM可匹配或超越图解析器；但当图复杂度增加（平均关系数>18），图解析器显著优于所有LLM，且优势随复杂度扩大（ERFGC上，最佳LLM F1=0.606 vs 图解析器F1=0.713，差距13.2点）。
- **LLM性能与图复杂度负相关**：表3显示Qwen3-14B-Base的F1与关系数呈强负相关（ERFGC: r=-0.639），而图解析器相关性较弱（ERFGC: r=-0.206）。
- **提示设计影响微弱**：在微调时，提示内容（描述、ICL、UUID、甚至对抗性指令）对性能无明显影响，说明微调后LLM主要依赖训练数据而非提示。
- **模型规模非决定性因素**：更大模型（70B）未必性能更好，甚至14B的Qwen3-14B-Base（未指令微调）平均表现优于指令微调后的更大模型，推测指令微调可能引入偏差。
- **轻量级图解析器的优势**：仅14M可学习参数（总124M）就显著优于数十亿参数的LLM，且在推理效率上优势巨大（需一次前向传播，LLM需数千次生成）。

## 7. 优点

- **空白填补**：首次系统比较LLM与图解析器在监督关系抽取中的性能，明确指出了LLM在复杂图上的局限性。
- **实验设计细致**：控制图复杂度（6个数据集，关系数从1到167）、多种提示变体、多种模型规模、消融实验（图解析器不同层配置）、报告方差。
- **公平性考量**：使用相同评估指标；部分LLM也训练相同步数（3k）以对齐计算量；使用精确匹配（不依赖标签）消除数据集差异。
- **发现具有实用性**：结论直接指导实际应用，提示在复杂图场景下选择轻量图解析器更优。

## 8. 不足与局限

- **图解析器单一**：只采用了一种图解析器架构（Dozat & Manning双仿射解析器），未对比其他SOTA图解析器（如基于GCN、GAT的不同变体）。
- **计算受限导致部分实验采样**：对最大模型和最大数据集仅评估100样本子集，可能引入偏差，影响结论的泛化性。
- **缺少定性分析**：未通过注意力可视化或错误类型分析深入解释LLM为何在复杂图上失败（作者在局限中也承认这一点）。
- **训练步数不完全对齐**：虽然部分LLM也训练3k步，但整体上LLM与图解析器的训练步数、学习率调度等超参数未完全一致，可能影响比较公平性。
- **未探索缓解策略**：论文呈现负面结果，但未尝试如何改进LLM（例如通过提示压缩、结构化生成等）以克服局限。
- **应用限制**：结论可能不适用于其他类型的关系抽取（如开放域、跨句子等），或更先进的LLM/训练范式（如RLHF、思维链）。

（完）
