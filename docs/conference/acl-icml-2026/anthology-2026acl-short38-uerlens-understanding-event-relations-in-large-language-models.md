---
title: "UERLens: Understanding Event Relations in Large Language Models"
title_zh: UERLens：理解大语言模型中的事件关系
authors: "Yong Guan (关勇), Zhiyuan Li, Shaoru Guo (郭少茹)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-short.38.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 事件关系抽取可解释性
tldr: 针对大语言模型中事件关系内部表示不明确的问题，提出UERLens可解释性框架。构建包含因果、时序和子事件关系的反事实数据集UERBench，通过比较模型激活识别关系敏感特征，并通过模型操控验证其功能角色。
source: ACL-2026-Short
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.38/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 741, \"height\": 784, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.38/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1599, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.38/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1623, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.38/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 279, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.38/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 243, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-short/anthology-2026.acl-short.38/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1600, \"height\": 500, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.38/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 767, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.38/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 782, \"height\": 598, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-short/anthology-2026.acl-short.38/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 618, \"height\": 364, \"label\": \"Table\"}]"
motivation: 大语言模型在事件关系抽取上表现良好，但内部如何表示和利用事件关系尚不清楚。
method: 构建反事实数据集UERBench，通过激活比较和模型操控分析事件关系内部表示。
result: 识别出关系敏感的神经特征，并通过干预实验验证其因果作用。
conclusion: UERLens揭示了LLM中事件关系内部表示机制，提升了可解释性。
---

## Abstract
Events exhibit rich semantic relations that are essential for understanding the unfolding of real-world processes. Although large language models (LLMs) have achieved strong performance on event relation extraction, how event relations are internally represented and utilized remains unclear. In this paper, we present UERLens, an interpretability framework for understanding event relations in LLMs. Specifically, we first construct UERBench, a counterfactual dataset for event relation analysis that covers causal, temporal, and sub-event relations. Based on counterfactual pairs, we identify relation-sensitive internal features by comparing model activations. We then examine the functional role of these features through model manipulation, including model intervention and model training. Experimental results show that event relations are encoded through structured and layer-specific internal features. Disabling relation-sensitive features leads to performance drops of over 22%, while enhancing them yields improvements of up to 7%. Furthermore, leveraging these interpretable features to train a lightweight classifier significantly improves event relation extraction, achieving F1 gains of up to 24% for causal relations.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：尽管大语言模型（LLM）在事件关系抽取（如因果、时序、子事件关系）上表现优异，但**事件关系如何在模型内部被表示和利用仍是黑箱**。现有可解释性工作多关注事件提及或词元级特征，缺乏对结构化的**事件关系本身**进行内部表示分析的方法。
- **整体含义**：理解LLM编码事件关系的机制，有助于提升模型的可信度、可控性，并为细粒度模型诊断与改进提供依据。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：通过构造反事实句子对（有/无目标关系，其他语义尽可能一致），比较模型中间层激活差异，利用稀疏自编码器（SAE）分离出**关系敏感的神经特征**，再通过模型操控验证这些特征的功能因果性。
- **关键技术细节**：
  1. **反事实数据构造（UERBench）**：基于MAVEN-ERE的事件模式，对每一句源文本进行**最小编辑**（替换或移除关系触发词）得到反事实句，同时保持事件语义不变，形成配对样本 \((s^+, s^-)\)。
  2. **特征识别**：对LLM每层隐藏状态 \(f\)，用SAE得到稀疏激活向量 \(a\)。对每对样本计算每个基向量 \(k\) 的潜在效应 \(\tau_k(s)=a_k(s^+)-a_k(s^-)\)，再对全部N个样本求平均得到平均潜在效应 \(L_k = \frac{1}{N}\sum_i \tau_k(s_i)\)。按 \(L_k\) 排序选取Top基向量作为**关系敏感特征**。
  3. **模型操控**：
     - **模型干预**：在前向传播中，将选中特征的激活值置0（消融）或置为固定高值（增强），观察预测变化。
     - **模型训练**：提取Top-K敏感特征激活值拼接成向量，训练轻量分类器（SVM）进行事件关系分类，验证特征信息的判别力。

### 3. 实验设计

- **数据集**：
  - **UERBench**（自建）：源自MAVEN-ERE的反事实数据集，包含因果、时序、子事件三类主关系及8个子关系（Cause, Precondition, Subevent, Begins-on, Ends-on, Contains, Before, Overlap, Simultaneous），共约42,000个关系实例（文档数约3,000+）。
  - **基准（Baseline）**：
    - 对比不同特征选择策略：随机选取特征（RFB） vs. 关系敏感特征（RSFT）。
    - 对比方法：ICL（上下文学习）、RFB（随机特征SVM）、RSFT（敏感特征SVM）。
- **评估指标**：
  - 特征敏感性：**PS**（充分性概率）、**PN**（必要性概率）、**FRC**（调和平均）。
  - 分类性能：精确率（P）、召回率（R）、F1值。
- **实验配置**：
  - 骨干模型：LLaMA‑3.1‑8B（主要）、Qwen‑1.7B（跨模型泛化验证）。
  - SAE：使用OpenSAE预训练检查点（32层全部）。
  - 特征选择层：选取0、6、8、15、24、30共6层，每层选Top‑20（共120个）特征用于干预和训练。

### 4. 资源与算力

- **论文未明确说明**GPU型号、数量、训练总时长等具体算力信息。只提到使用OpenSAE的公开检查点以及LLaMA‑3.1‑8B/Qwen‑1.7B模型。反事实数据的生成依赖GPT‑5（也未提具体调用次数或成本）。因此算力资源细节缺失。

### 5. 实验数量与充分性

- **实验类型丰富**：
  - 特征分析实验：层间FRC/PS/PN分布、跨关系重叠分析（C‑S、C‑T、S‑T）。
  - 模型干预实验：消融/增强对目标关系预测的影响（图4），以及非目标关系控制实验（附录C）。
  - 模型训练实验：对比RFB和RSFT的SVM分类性能（表2）。
  - 跨模型泛化实验：Qwen上重复特征识别（表3）。
- **充分性评价**：实验设计较全面，考虑了**正向（增强）、负向（消融）、控制（非目标特征）**三种操纵，且重复多次取平均；跨模型验证增强了结论稳健性。不足之处：仅涵盖两种模型（8B和1.7B），且反事实数据仅基于单一源数据集MAVEN‑ERE，可能多样性有限。

### 6. 论文的主要结论与发现

- **事件关系在中高层编码为关系敏感的神经特征**（FRC在6~15层最高），而非仅词元层面。
- **这些特征具有功能因果性**：消融导致目标关系预测准确率下降>22%，增强提升高达7%（以准确性为指标）。
- **利用敏感特征训练轻量分类器（SVM）**，在因果关系上F1提升24%（67.40→72.05 vs. 47.65），子事件和时序分别提升18.63和13.06。
- **特征结构呈现“共享-分化-部分整合”的层次模式**：低层特征重叠高，中间层分化显著，高层（尤及时序）部分重聚。
- **跨模型泛化一致**：Qwen上也观察到类似的特征分布趋势。

### 7. 优点

- **方法新颖**：首次从**事件关系本身**出发进行内部表示的可解释性分析，而非仅关注词元或实体。
- **反事实设计严谨**：遵循最小编辑、语义保持、逻辑合理三原则，使得激活差异可归因于关系。
- **双重验证（干预+训练）**：既通过因果关系验证（消融/增强直接影响预测），又通过判别力验证（敏感特征可使简单分类器显著提升），证据链完整。
- **开源代码和数据集**：GitHub提供复现资源，有助于后续研究。

### 8. 不足与局限

- **实验覆盖有限**：仅分析了三类基本事件关系，未涉及更细粒度（如对比、条件）或复杂多事件链；未覆盖事件检测、参数抽取等任务。
- **模型规模偏小**：主要实验在8B模型上，而当前LLM常用70B+；跨模型泛化仅用了1.7B的Qwen，未在更大规模上验证。
- **反事实构造依赖外部LLM（GPT‑5）**，可能引入生成偏差，且缺乏人工验证的质量保证。
- **资源消耗未报告**：缺少训练/推理时间、GPU规格等，不利于复现成本评估。
- **仅限于文本模态**，未考虑多模态场景下事件关系的内部表示。

（完）
