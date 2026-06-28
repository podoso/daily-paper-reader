---
title: "TAdaRAG: Task Adaptive Retrieval-Augmented Generation via On-the-Fly Knowledge Graph Construction"
title_zh: TAdaRAG：通过即时知识图谱构建实现任务自适应检索增强生成
authors: "Jie Zhang, Bo Tang, Wanzi Shao, Wenqiang Wei, Jihao Zhao, Jianqing Zhu, Zhiyu Li, Wen Xi, Zehao Lin, Feiyu Xiong, Yanchao Tan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40774/44735"
tags: ["query:llm"]
score: 7.0
evidence: 任务自适应RAG与即时知识图谱构建
tldr: 针对传统RAG分块导致信息丢失和引入无关细节的问题，提出TAdaRAG框架，通过意图驱动路由和领域特定抽取模板，结合微调与强化学习实现即时任务自适应知识图谱构建，提升检索增强生成的质量。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 传统RAG分块导致信息丢失和推理链断裂，且检索非结构化知识引入无关细节。
method: 提出TAdaRAG，设计意图驱动路由、领域特定抽取模板，并通过监督微调和强化学习隐式抽取结构知识。
result: 在多个问答任务上，TAdaRAG优于基线，减少幻觉并提升推理准确性。
conclusion: 即时构建结构化知识图能有效增强RAG，为LLM应用提供更可靠的支持。
---

## Abstract
Retrieval-Augmented Generation (RAG) improves large language models by retrieving external knowledge, often truncated into smaller chunks due to the input context window, which leads to information loss, resulting in response hallucinations and broken reasoning chains.
Moreover, traditional RAG retrieves unstructured knowledge, introducing irrelevant details that hinder accurate reasoning.
To address these issues, we propose TAdaRAG, a novel RAG framework for on-the-fly task-adaptive knowledge graph construction from external sources. 
Specifically, we design an intent-driven routing mechanism to a domain-specific extraction template, followed by supervised fine-tuning and a reinforcement learning-based implicit extraction mechanism, ensuring concise, coherent, and non-redundant knowledge integration. 
Evaluations on six public benchmarks and a real-world business benchmark (NowNewsQA) across three backbone models demonstrate that TAdaRAG outperforms existing methods across diverse domains and long-text tasks, highlighting its strong generalization and practical effectiveness.

---

## 论文详细总结（自动生成）

# TAdaRAG：通过即时知识图谱构建实现任务自适应检索增强生成——详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统检索增强生成（RAG）方法在处理长文本时，由于输入上下文窗口限制，不得不将外部知识切割成小块（chunks），导致信息丢失，进而引发响应幻觉（hallucination）和推理链断裂。同时，传统RAG检索非结构化知识，容易引入无关细节，干扰准确推理。
- **研究背景**：大语言模型依赖内部参数知识易产生幻觉，引入外部知识可缓解此问题。但现有RAG方法面临三大缺陷：① 分块截断导致信息丢失（案例a）；② 离散块无法捕捉逻辑关系，破坏推理链（案例b）；③ 非结构化知识引入冗余细节（案例c）。近几年图增强RAG方法利用知识图谱结构信息，但依赖预构建KG，缺乏可扩展性和任务适应性。
- **整体含义**：论文提出TAdaRAG框架，将任务自适应知识图谱构建直接集成到推理过程中，而非检索阶段，旨在动态构建领域相关子图，解决分块幻觉、增强复杂推理、提高知识提取准确性。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将结构化知识图谱嵌入到生成推理过程，通过两阶段训练实现即时、任务自适应的KG构建与利用。
- **关键技术细节**：
  - **阶段一：监督知识抽取微调（Supervised Knowledge Extraction Fine-Tuning）**
    - ① 意图检测与模板路由：通过提示（prompt）对用户查询和外部知识进行意图检测，选择领域特定抽取模板，明确所需实体类型、描述规范和关系模式。
    - ② 高质量语料微调：基于模板构建指令集（查询+外部知识+模板），利用强LLM生成高质量KG三元组，构建约9,548个样本的训练数据集，使用LoRA对预训练LLM进行监督微调，使模型具备基础知识抽取能力。
  - **阶段二：任务自适应知识图谱构建（Task-Adaptive Knowledge Graph Construction）**
    - ① 并行构建：对每个输入指令采样p个候选子图（如p=3），使用特殊标记`<|startextraction|>`和`<|endextraction|>`实现隐式知识抽取。
    - ② 混合网络（Mixing Network）：设计图结构融合网络，分别计算无图和有图条件下的隐状态及对数似然，通过三层MLP计算每个token的权重，融合得到混合对数似然，用于生成和优化。
    - ③ 强化学习优化：基于REINFORCE算法设计奖励函数 $R_{i,k} = \max(0, L_{base}^i - L_{graph}^{i,k} - \bar{R}_i)$，奖励那些比平均表现更好的子图，并更新模型参数以鼓励生成高质量KG。总损失为 $L = \alpha L_{base} + (1-\alpha)L_{graph} + \beta L_{REINFORCE}$。

- **推理阶段**：输入查询和外部知识，模型动态构建任务自适应KG，并集成到生成过程，产生更准确、上下文相关的回答。

## 3. 实验设计：数据集/场景、benchmark、对比方法

- **数据集与场景**：
  - **公共基准**（6个）：开放域QA（Health, Biology, Legal）、多跳QA（HotpotQA, 2WikiMQA）、摘要（GovReport）。
  - **真实业务场景**：构建NowNewsQA（中文时事新闻多文档QA，3,150个样本，其中3,000训练/150测试），源自鑫语AI搜索的实际用户查询。
- **评估指标**：F1分数（QA任务）和ROUGE-L（摘要任务）；业务场景采用9维多面评估（相关性、数值精确性、简洁性、事实性、时效性、全面性、清晰性、连贯性、洞察力），分别由人类专家和GPT-4o评分。
- **对比方法**：包括NaïveRAG、BGE-M3、RQ-RAG、GraphRAG、HippoRAG、MEMORAG、PathRAG。同时还与三种长上下文机制（Self-Extend, H2O+THINK, SnapKV+THINK）比较。
- **骨干模型**：Mistral-7B-Instruct、Qwen2.5-7B-Instruct、Qwen2.5-14B-Instruct。

## 4. 资源与算力

- **训练硬件**：8块 NVIDIA A100（80 GB）GPU。
- **训练时长**：总共约16小时（阶段一约4小时，阶段二约12小时）。
- **训练配置**：阶段一训练5个epoch，最大输入长度20,480 tokens，batch size=1，梯度累积8步，余弦学习率5e-5；阶段二使用ZeRO stage-2优化，AdamW优化器，batch size=1 per GPU，bfloat16精度，训练3个epoch，学习率5e-7。采样温度T=0.6，贪婪解码用于评估。

## 5. 实验数量与充分性

- **实验数量**：
  - 6个公共数据集 + 1个业务数据集，共7组实验。
  - 在Mistral-7B和Qwen2.5-7B上报告全量结果，在Qwen2.5-14B上报告部分结果。
  - 消融实验：比较w/ graph（仅提示）、w/ sft（监督微调）、w/ reinforce（完整TAdaRAG）三阶段。
  - 超参数分析：测试并行子图数量（p=2,3,4,5）对性能的影响。
  - 长上下文任务对比实验。
  - 人类评分一致性验证（3位专家，Pearson相关系数）。
  - LLM评分与人类评分相关性分析（Pearson，9维度）。
- **充分性与客观性**：
  - 覆盖了多种任务类型（事实问答、多跳推理、长文本摘要、真实业务问答）。
  - 对比了7种代表性RAG方法，包括最新SOTA（MEMORAG, PathRAG）。
  - 消融实验验证各模块贡献，超参数分析证明设计选择的合理性。
  - 统计显著性检验（p<0.01）支持结果可靠性。
  - 人类评估与LLM评估高度一致，说明评价体系稳定。
  - 整体实验设计较为充分、客观、公平，但业务场景仅有一个数据集，泛化性需进一步验证。

## 6. 论文的主要结论与发现

- **性能优势**：TAdaRAG在所有6个公共基准和业务基准上均优于现有SOTA RAG方法，特别是在事实性（Health/Biology/Legal）、多跳推理（HotpotQA/2WikiMQA）和长文本摘要（GovReport）上提升显著。
- **幻觉缓解**：通过即时知识图谱构建有效减少分块信息丢失带来的幻觉。
- **推理增强**：动态组织知识层次提升了复杂推理链的完整性。
- **任务导向性**：通过意图检测和强化学习优化，提取的知识更简洁、相关、无冗余。
- **通用性**：在三种不同骨干模型上保持一致性能，说明方法具备良好泛化能力。
- **业务可行性**：在NowNewsQA上多维度评分领先，显示实际应用价值。

## 7. 优点

- 方法创新：提出动态、任务自适应的KG构建，而非依赖预构建KG，解决了现有图增强RAG缺乏灵活性和可扩展性的问题。
- 两阶段训练设计合理：监督微调提供冷启动能力，强化学习优化实现自适应，二者互补。
- 混合网络巧妙：可学习的加权融合机制使模型能自主衡量KG重要性。
- 实验全面：覆盖多领域、多任务、多模型，消融和超参数分析到位，验证了每个设计选择的有效性。
- 业务验证：构建真实业务数据集NowNewsQA并进行了人类专家评估，增强了实际应用说服力。
- 开源代码和提供试用账户，促进可复现性和社区应用。

## 8. 不足与局限

- **计算开销**：动态KG构建和多阶段训练增加了整体计算成本，可能限制在资源受限场景下的部署。
- **模板依赖**：部分依赖手动设计的领域模板，在完全未见过的新领域可能需要人工干预，影响自动化程度。
- **业务场景单一**：仅用一个真实业务数据集（新闻QA）验证，更多行业（如金融、医疗、法律等）的泛化性有待验证。
- **长上下文实验对比有限**：长上下文机制对比仅使用了Mistral-7B一个模型，且未与更多先进长上下文方法（如LongLoRA, YaRN等）对比。
- **强化学习奖励函数简单**：基于平均损失差的奖励设计可能不足以捕捉细微的质量差异，更复杂的奖励建模可能进一步提升。
- **未讨论垂直领域微调**：论文未探索在特定领域继续微调（如法律、医疗）是否能进一步提升性能，仅使用通用模板和训练。

（完）
