---
title: "LexRel: Benchmarking Legal Relation Extraction for Chinese Civil Cases"
title_zh: LexRel：面向中文民事案件的法律关系抽取基准
authors: "Yida Cai, Ranjuexiao Hu, Huiyuan Xie, Chenyang Li (李晨阳), Yun Liu, Yuxiao Ye, Zhenghao Liu (刘正皓), Weixing Shen, Zhiyuan Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.980.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 法律关系抽取基准
tldr: 针对中文民事案件法律关系抽取缺乏基准的问题，提出LexRel基准，包含层次化模式和论元定义。评估了多种大语言模型，发现当前模型在法律关系抽取上存在显著局限性，为后续研究提供参考。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.980/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 764, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.980/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.980/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.980/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 480, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 614, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 597, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 1273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1647, \"height\": 2384, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1641, \"height\": 2321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1640, \"height\": 2264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.980/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1646, \"height\": 2135, \"label\": \"Table\"}]"
motivation: 中文民事案件法律关系抽取缺少综合模式和基准数据集。
method: 构建层次化法律关系模式并标注LexRel基准数据集。
result: 评估多种LLM，发现它们在法律关系抽取上表现有限。
conclusion: LexRel为法律AI领域提供了标准化评估资源。
---

## Abstract
Legal relations serve as an important analytical framework for dispute resolution in civil cases. However, legal relations in Chinese civil cases remain underexplored in the field of legal AI, largely due to the absence of comprehensive schemas. In this work, we first introduce a comprehensive schema for legal relations in civil cases, which contains a hierarchical taxonomy and definitions of arguments. Based on this schema, we formulate a legal relation extraction task and present **LexRel**, an expert-annotated benchmark for legal relation extraction in the Chinese civil law domain. We use **LexRel** to evaluate state-of-the-art large language models (LLMs) on legal relation extraction, showing that current LLMs exhibit significant limitations in accurately identifying civil legal relations. Furthermore, we demonstrate that explicitly incorporating information about legal relations leads to promising performance gains on other downstream legal AI tasks.

---

## 论文详细总结（自动生成）

## 论文总结：LexRel: Benchmarking Legal Relation Extraction for Chinese Civil Cases

### 1. 核心问题与整体含义（研究动机和背景）
- **法律关系的核心地位**：在中文民事案件中，法律关系（legal relations）是纠纷解决的底层分析单元，法官借助法律关系确定主体、客体和权利义务（内容），进行案件定性、法律适用和结果预测。
- **现有法律AI的不足**：
  - 当前法律信息抽取多聚焦于**事实实体**（如人、物、合同）或**一般社会关系**（如雇佣、所有权），而忽略了基于法律规范和法律理论定义的法律关系。
  - 已存在的法律关系模式多为粗粒度（如“民事权利义务关系”），缺乏结构化、细粒度的分类体系和明确的论元定义。
  - 法律关系的识别需要法律专业知识，仅依赖大规模法律文本预训练的模型难以准确捕获。
- **本文目标**：构建第一个全面的中文民事法律关系模式（scheme），包含层次化分类和论元定义，并据此构建了人工标注基准**LexRel**，用于评估和推动法律AI在法律关系抽取任务上的能力。

### 2. 方法论
#### 核心思想
- 将法律关系定义为**（主体、客体、内容）** 的三元组，并针对不同大类（如物权关系、合同关系、侵权关系等）分别设计了详细的论元定义。
- 将法律关系抽取分解为两个子任务：
  1. **类型抽取（Type Extraction）**：从案件事实文本中识别出存在的法律关系类型（共265种，属9大域）。
  2. **论元抽取（Argument Extraction）**：给定事实文本和关系类型，抽取对应的**主体（Subject）**、**客体（Object）** 和**内容（Content）**。
- 整体采用**先自动标注、后专家修正**的流水线方式构建基准。

#### 关键技术细节
- **层次化分类体系构建**：
  - 初始分类：通过关键词匹配从中国裁判文书网提取关系表述语，再结合法律术语词典（如《中国法律大辞典》）过滤，形成6大类123种候选关系。
  - 专家精炼：由两位资深法学学者新增3个域（票据关系、信用证关系、独立保函关系），最终得到9大域、265种关系类型。
  - 其中“债的关系”包含最多子类型（200种），对应实际民事案件中合同纠纷和侵权纠纷的高发特征。
- **论元定义**：针对8个主要域及债权关系下的4个子域（合同、侵权、无因管理、不当得利），分别给出了主体、客体、内容的精确法律定义（表1展示了物权关系示例）。
- **基准构建流程**：
  1. 使用**DeepSeek-V3**（提示词见表2）从裁判文书完整文本中抽取候选关系类型和论元，同时抽取“法院认定事实”部分作为输入文本。
  2. 6位法律专业标注员逐一验证并修正1160个样本，最终剔除60个无明确关系的样本，得到1140个有效样本，包含1863个完全标注的法律关系三元组。
- **评价方法**：
  - 类型抽取：直接匹配预测类型与黄金标签。
  - 论元抽取：使用**LLM-as-a-Judge**策略，利用DeepSeek-V3判断预测论元与黄金论元是否语义等价。并经过人工校验（193对样本），确认DeepSeek-V3的评估准确率：主体0.954、客体0.969、内容0.810，验证了自动评估的可靠性。
- **实验设置**：
  - **零样本基线**：直接使用提示词（同表2）让模型抽取。
  - **关系增强（Relation-Enhanced, RE）基线**：将完整的判决书文本（而非仅事实部分）输入给GPT-4o和DeepSeek-R1生成训练数据（5500个合成样本），然后对小型开源模型进行SFT，再用LexRel评估。

### 3. 实验设计
#### 数据集 / 场景
- **主评估**：LexRel基准（1140个样本，1863条关系，覆盖全部9大域）。
- **长尾分析**：依赖中国裁判文书网公开的2660万份民事判决书的案由数据作为近似分布。
- **下游任务**：LawBench中的三个任务——Case Analysis、Consultation、Criminal Damages Calculation。

#### 基准与对比方法
- **零样本基线**：
  - 闭源：GPT-4o、o3-mini、Claude-Sonnet-4
  - 开源：DeepSeek-V3、DeepSeek-R1（API调用）、Llama3.1-8B-Instruct、Llama3.1-70B-Instruct、InternLM3-8B-Instruct、MiniCPM4-8B、Qwen3-8B/14B/32B
- **关系增强基线（SFT）**：仅对8B和14B开源模型（InternLM3-8B、MiniCPM4-8B、Qwen3-8B/14B）进行微调，训练数据来自GPT-4o或DeepSeek-R1生成的5500条合成数据。
- **下游任务**：GPT-4o、DeepSeek-V3、MiniCPM4-8B、Qwen3-8B，对比有无注入法律关系信息的性能。

#### 评估指标
- 类型抽取和论元抽取均使用：精确率（Precision）、召回率（Recall）、micro-F1、macro-F1。
- 论元抽取使用LLM-as-a-Judge（DeepSeek-V3）逐项判断主体、客体、内容是否匹配。

### 4. 资源与算力
- **计算资源**：所有实验在**4×A800 GPU**（每卡40GB显存）上进行。
- **训练细节**：未明确说明训练时长和具体超参数（如学习率、epoch数等）。文中提到由于计算成本限制，仅对参数量8B和14B的模型进行了SFT。

### 5. 实验数量与充分性
- **实验数量**：
  - 零样本评估：涵盖11个LLM（闭源+开源），每个模型报告了类型抽取和论元抽取的4项指标（P/R/micro-F1/macro-F1），共约88个结果。
  - 关系增强评估：4个小型模型（8B/14B）分别使用两种数据源（GPT-4o、DeepSeek-R1），同样报告4项指标，共约64个结果。
  - 长尾分析：包含χ²检验、Cramér's V、Pareto分布图，验证了LexRel的长尾分布与真实案件分布的一致性。
  - 下游任务：4个模型×3个任务×2种设置（有无法律关系），共24个结果。
  - 误差分析：详细讨论了混淆错误（法律 vs 社会关系）、长尾稀疏性、客体误判、内容缺失等典型错误案例。
- **充分性与公平性**：
  - 覆盖了主流的闭源和开源LLM，评价标准统一（同一提示、同一自动裁判器）。
  - 验证了自动裁判器与人工的一致性，确保论元评估的可靠性。
  - 消融实验：通过关系增强设置，间接对比了有无SFT的效果；通过下游任务，对比了有无法律关系的效果。
  - **不足**：未对不同的模式设计（如仅用类型 vs 完整三元组）进行消融；未对比传统的分类或序列标注方法（如基于BERT的模型）；未详细分析不同关系类型间的难度差异；SFT数据完全来自DeepSeek-R1和GPT-4o，未尝试其他生成模型。

### 6. 主要结论与发现
1. **当前LLM在法律关系抽取上表现有限**：
   - 零样本类型抽取：最佳为o3-mini（micro-F1=0.762），其次DeepSeek-R1（0.693）。开源模型Qwen3系列最好（32B为0.583）。
   - 零样本论元抽取：非常困难，最佳o3-mini也仅0.382，多数开源模型低于0.2。
2. **推理型LLM更优**：o3-mini和DeepSeek-R1展现更强能力，说明推理能力有助于法律关系理解。
3. **SFT显著提升**：通过蒸馏DeepSeek-R1到Qwen3-14B，类型抽取micro-F1达到0.733，接近零样本最佳；论元抽取从0.102提升至0.381（InternLM3-8B从0.048到0.323）。
4. **长尾分布吻合现实**：LexRel中关系类型的频率分布与真实民事案件案由分布高度一致（Cramér's V=0.528），说明基准具有较好的代表性。
5. **法律关系对下游任务有帮助**：在Case Analysis、Consultation、Criminal Damages Calculation上，引入关系信息普遍提升模型性能（如MiniCPM4-8B的Case Analysis从32.0升至45.0）。

### 7. 优点
- **首创性**：首次系统定义并结构化中文民事法律关系模式，涵盖9大域265种关系及精细的论元定义，为法律AI提供基础资源。
- **数据质量高**：专家标注（6位法律专业+资深专家监督），并进行一致性检验（Cohen's Kappa=0.706，substantial agreement），保证基准可靠性。
- **评估全面且谨慎**：评估了多种闭源/开源LLM，指标覆盖微观和宏观；自动裁判器经过人工验证，避免主观偏差。
- **实用性验证**：通过下游任务证明法律关系信息的附加价值，呼应“法律AI需要结构化知识”的论点。
- **长尾分析严谨**：用大规模真实判决书案由数据验证基准分布，增强外部有效性。

### 8. 不足与局限
- **领域限制**：模式针对中国民法，对英美法系或其他大陆法系国家的直接迁移性不强，需本地化适配。
- **模型族耦合风险**：数据生成（DeepSeek-V3）、SFT数据源（DeepSeek-R1）、评估裁判器（DeepSeek-V3）均来自DeepSeek系列，可能存在风格/偏见耦合，尽管作者声称采取了缓解措施（如指令对不同模型的提示保持一致）。
- **基准规模有限**：仅1140个样本，虽然覆盖265种关系，但每种关系出现频次差异大，长尾关系评估信度可能不足。
- **任务定义简化**：将法律关系抽取视为独立的类型+论元抽取，未考虑关系之间的层次性与交互（如多个关系共存、关系演化等）；论元内容抽取为自然语言段落，评估依赖自动裁判器（尽管已校验，但仍有误差，content准确率0.810）。
- **缺乏传统方法对比**：未与基于BERT的序列标注或阅读理解模型对比，无法判断LLM在法律关系抽取上是否显著优于传统方法。
- **消融实验不够丰富**：未对模式的不同组件（如去掉论元定义、仅使用类型等）进行消融；未分析不同提示模板的影响。
- **SFT实验细节缺失**：未报告训练epoch、学习率、batch size等，复现难度大。

（完）
