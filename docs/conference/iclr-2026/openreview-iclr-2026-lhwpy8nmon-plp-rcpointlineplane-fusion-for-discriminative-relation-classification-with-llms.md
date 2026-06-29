---
title: "PLP-RC:Point–Line–Plane Fusion for Discriminative Relation Classification with LLMs"
title_zh: PLP-RC：基于点-线-面融合的LLM判别式关系分类
authors: "Pengjiu Xia, Wu Yuan, Yidian Huang, Wen Yuan, Wandong Zhang"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=LhwPy8NMoN"
tags: ["query:ie"]
score: 9.0
evidence: 使用LLM嵌入的点-线-面融合进行关系分类
tldr: 关系分类是NLP基础任务，LLM虽提供丰富知识但易产生幻觉。PLP-RC提出点-线-面融合框架：将实体跨度建模为局部点表示，序列结束标记为全局面表示，通过注意力对齐两者，实现判别式关系分类，无需生成文本，提高可靠性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-lhwpy8nmon/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1136, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lhwpy8nmon/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1320, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-lhwpy8nmon/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1446, \"height\": 508, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1202, \"height\": 839, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 566, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 668, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 551, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 993, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1065, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-lhwpy8nmon/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1454, \"height\": 895, \"label\": \"Table\"}]"
motivation: LLM生成式关系分类存在幻觉，且难以融合局部实体信息与全局上下文。
method: 提出点-线-面融合框架：实体跨度作为点，EOS作为面，注意力对齐作为线，结合LLM嵌入进行判别式分类。
result: 在关系分类基准上取得优异性能，减少幻觉。
conclusion: 判别式框架有效利用LLM知识，提高关系分类可靠性。
---

## Abstract
Relation classification is a fundamental NLP task that involves identifying the semantic relations between entity pairs in a given text. While pre-trained language models have advanced this area, effectively integrating local entity information with global context remains a key challenge. Large Language Models offer rich world knowledge, but their generative use often suffers from hallucinations, limiting reliability. To address these issues, we propose a Point–Line–Plane fusion framework for discriminative relation classification with LLM embeddings. Entity spans are modeled as local point representations, the end of sequence token provides a global plane representation, and an attention-based line representation aligns the two. This discriminative paradigm avoids hallucinations while fully exploiting LLM representations. Our method achieves new SOTA performance on TACRED, TACREV, and RE-TACRED benchmarks,  outperforming both discriminative and generative baselines. Ablation studies provide further evidence for the effectiveness of our design in achieving context-aware relation classification.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **任务**：关系分类（Relation Classification，RC）是自然语言处理的基础任务，旨在从文本中识别实体对之间的语义关系，对知识图谱构建、问答系统等下游应用至关重要。
- **现有挑战**：
  - 传统PLM（如BERT）虽能生成上下文表示，但在长距离依赖和跨句推理上能力有限；且其预训练目标（掩码语言模型）未显式优化实体间语义交互。
  - 大规模语言模型（LLM）提供丰富的世界知识，但生成式范式存在严重幻觉问题，且其在关系分类中难以有效融合局部实体信息与全局上下文。
- **本文目标**：提出判别式（discriminative）框架，利用LLM作为特征编码器，避免生成式幻觉，同时通过几何启发的“点-线-面”融合机制，整合实体局部信息、注意力对齐信息和全局上下文信息，实现可靠且高效的关系分类。

## 2. 论文提出的方法论

- **核心思想**：将几何类比映射到语言表示——token视为**点（Point）**，token间关系（注意力权重）视为**线（Line）**，完整上下文通过[EOS] token压缩为**面（Plane）**。三者融合得到增强的实体表示用于分类。
- **关键技术细节**：
  1. **Point表示**：实体的跨度（span）通过边界token嵌入（MLP_start和MLP_end分别投影）加上实体类型嵌入（e_type）得到，公式：\( e_{Point} = MLP_{start}(h_{start}) + MLP_{end}(h_{end}) + e_{type} \)。
  2. **Plane表示**：取[EOS] token的最终隐藏状态作为全局上下文压缩表示：\( e_{Plane} = h_{EOS} \)。
  3. **Line表示**：利用因果注意力的注意力分数，计算[EOS]与实体开始、实体结束以及实体跨度内所有token平均注意力分数，拼接后通过MLP_A投影到与Point相同维度：\( e_{Line} = Concat(A_{start}, A_{end}, \frac{1}{N_t}\sum_{i=head}^{end} A_i) \)，然后通过元素相加融入Point：\( e_{Entity} = e_{Point} + MLP_A(e_{Line}) \)。
  4. **最终融合**：将Plane、Subject实体嵌入、Object实体嵌入拼接：\( e_{Fused} = Concat(e_{Plane}, e_{Sub}, e_{Obj}) \)，输入线性分类器+softmax得到关系概率分布。
  5. **指令增强**：在输入序列末尾附加自然语言指令（如“Classify the relation between the two entities…”），增强[EOS]的任务感知语义，弥补预训练与关系分类任务间的语义鸿沟。
- **训练**：端到端全参数微调，优化交叉熵损失：\( \mathcal{L} = -\frac{1}{N}\sum_{i=1}^{N}\log p(r_i | e_{fused}^i) \)。

## 3. 实验设计

- **数据集**：三个广泛使用的关系分类基准：
  - TACRED（42种关系，68,124训练/15,509测试/22,631验证）
  - TACREV（TACED修正版，数据规模相同）
  - RE-TACRED（重新标注版，40种关系，58,465训练/13,418测试/19,584验证）
- **基准方法**：分为两类：
  - 传统判别式模型：PA-LSTM、C-GCN、SpanBert、KnowBERT、LUKE、Roberta+Typed、GAP等。
  - LLM生成式方法：DeepStruct、RAGRE、RAGRE+Finetune（基于Flan-T5-XL、LLaMA2-7B、Mistral-7B）。
- **评价指标**：Micro-F1，这是关系分类的通用指标。
- **对比结果**：本文方法（PLP-RC）在不同参数规模的Qwen3模型（0.6B、1.7B、4B）上均取得最优或持平结果，小模型（0.6B）即超越所有生成式基线。

## 4. 资源与算力

- **硬件**：单张NVIDIA H100 80GB GPU（文中明确说明“All experiments can be conducted on a single NVIDIA H100 GPU 80GB.”）。
- **训练时长**：针对1.7B模型在TACRED上，完整PLP-RC每epoch约25.5分钟（见表2）；去除Line和Plane约16.0分钟；去除Line约24.2分钟。总训练epoch数为10，因此完整训练耗时约4.25小时。
- **模型规模**：使用Qwen3系列模型（参数范围0.6B、1.7B、4B），采用全参数微调。
- **超参数**：学习率3×10⁻⁵，batch size 24，weight decay 0.01，warmup steps 1000，优化器AdamW，随机种子42。

## 5. 实验数量与充分性

- **主实验**：在三个数据集（TACRED、TACREV、RE-TACRED）上与11个基线对比，完整展示于表1。
- **组件消融**：图3a，逐步去除Line、Line+Plane、Instruction，验证各组件贡献。
- **参数规模消融**：图3b，使用Qwen2.5-0.5B、Qwen3-0.6B/1.7B/4B观察规模缩放规律。
- **计算效率消融**：表2，记录每epoch分钟数。
- **指令位置消融**：表3，比较前缀（prefix）与后缀（suffix）效果。
- **生成式对比消融**：表4，在同一LLM（Qwen3-1.7B/4B）上采用零样本和SFT生成式方法，验证判别式框架优势。
- **类别级性能分析**：表7，对RE-TACRED各关系类型分别计算F1，识别因数据不平衡导致的低分类别。
- **充分性与公平性**：实验覆盖多种对比方法（判别式与生成式），消融全面，包括指令设计、注意力来源、模型规模等维度，且基线方法使用官方报告结果或复现，实验设计客观公平。

## 6. 论文的主要结论与发现

- **性能领先**：PLP-RC在所有三个数据集上达到新SOTA（判别式方法），小模型（0.6B）即可超越甚至2-7B的生成式模型。
- **组件有效性**：Plane（全局上下文）和Instruction贡献最大；Line提供补充增益；去除指令导致最大性能下降。
- **规模递减**：增大模型参数（0.5B→4B）带来非线性的有限提升，纯生成能力不能直接转化为判别式下游性能。
- **判别式 vs 生成式**：判别式范式避免幻觉，计算效率高，相比SFT生成式方法（仅45.6/57.9 Micro-F1）性能显著更好。
- **指令位置不敏感**：前缀或后缀指令效果接近，不影响性能。

## 7. 优点

- **方法创新**：提出“点-线-面”几何类比的融合方式，新颖且直觉性强，有效整合多粒度语义（局部实体、全局上下文、注意力关联）。
- **避免幻觉**：采用判别式范式（基于LLM embedding分类而非生成）从原理上消除生成式模型的幻觉问题。
- **高效实用**：即便使用0.6B小参数模型，性能已经优于传统大生成模型；训练成本可控（单卡H100，数小时）。
- **实验设计严谨**：
  - 包括三种主流数据集和多个基线，对比公平；
  - 消融实验覆盖组件、规模、效率、指令设计、生成式直接对比，全面揭示贡献。
  - 公开代码和预处理数据，可复现性好。
- **分析深入**：针对每个关系类型计算F1，指出数据不平衡影响，为后续改进提供方向。

## 8. 不足与局限

- **依赖预训练模型能力**：性能增益主要来自PLP-RC方法，但仍受限于底层LLM（Qwen3）的表示能力，若改用更优基础模型可能进一步提升。
- **计算效率有提升空间**：完整PLP-RC（含Line）相比基线（去除Line和Plane）增加约59%的每epoch时间（16.0→25.5分钟），尽管增量不大，但仍可优化。
- **评估局限于句子级**：所有基准数据集均为句子级别，无法充分验证跨句子关系推理能力。论文承认“systematic evaluation of cross-sentence cases is not currently available”。
- **数据不平衡风险**：某些低频关系（如per:country of birth为0条测试样本，org:dissolved仅5条）导致对应F1极低（0.00或0.13），模型对长尾关系处理能力有限，存在偏差风险。
- **未涉及多语言场景**：实验仅使用英语数据集，泛化性需进一步验证。
- **审稿状态**：论文目前为“under review as a conference paper at ICLR 2026”，且元数据标注为“ICLR-2026-Rejected-Public”，表明已被拒稿，可能存在未被完全解决的缺陷。

（完）
