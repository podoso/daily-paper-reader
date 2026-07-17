---
title: Combining Distantly Supervised Models with In Context Learning for Monolingual and Cross-Lingual Relation Extraction
title_zh: 结合远程监督模型与上下文学习进行单语和跨语言关系抽取
authors: "Vipul Kumar Rathore, Malik Hammad Faisal, Parag Singla, Mausam ."
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2109.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 远程监督关系抽取结合上下文学习
tldr: 远程监督关系抽取面临噪声标注挑战。本文提出HYDRE框架，先由DSRE模型预测候选关系，再通过动态示例检索和上下文学习纠正偏差。在单语和跨语言设定下，HYDRE显著提升句子级关系抽取准确性，且无需额外标注。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2109/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 732, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2109/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 735, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2109/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1670, \"height\": 1976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2109/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1668, \"height\": 1925, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2109/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1625, \"height\": 619, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 857, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1351, \"height\": 1493, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1323, \"height\": 410, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1627, \"height\": 613, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1567, \"height\": 675, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 865, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1559, \"height\": 604, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 745, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 624, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 773, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 777, \"height\": 506, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 428, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 947, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 969, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 929, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 948, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 735, \"height\": 985, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 710, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2109/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 745, \"height\": 278, \"label\": \"Table\"}]"
motivation: 远程监督关系抽取受噪声标注影响，LLM学习关系语义困难。
method: 先用DSRE模型获取候选关系，再通过动态示例检索的上下文学习进行纠正。
result: 在多个DSRE数据集上显著优于纯DSRE和纯ICL方法，跨语言有效。
conclusion: 混合框架有效利用DSRE和LLM的优势，提升关系抽取鲁棒性。
---

## Abstract
Distantly Supervised Relation Extraction (DSRE) remains a long-standing challenge in NLP, where models must learn from noisy bag-level annotations while making sentence-level predictions. While existing state-of-the-art (SoTA) DSRE models rely on task-specific training, their integration with in-context learning (ICL) using large language models (LLMs) remains underexplored. A key challenge is that the LLM may not learn relation semantics correctly, due to noisy annotation.In response, we propose HYDRE – HY brid D istantly Supervised R elation E xtraction framework. It first uses a trained DSRE model to identify the top- k candidate relations for a given test sentence, then uses a novel dynamic exemplar retrieval strategy that extracts reliable, sentence-level exemplars from training data, which are then provided in LLM prompt for outputting the final relation(s).We further extend HYDRE to cross-lingual settings for RE in low-resource languages. Using available English DSRE training data, we evaluate all methods on English as well as a newly curated benchmark covering four diverse low-resource Indic languages - Oriya, Santali, Manipuri, and Tulu. HYDRE achieves up to 20 F1 point gains in English and, on average, 17 F1 points on Indic languages over prior SoTA DSRE models and naive prompting baselines. Detailed ablations exhibit HYDRE ’s efficacy compared to other prompting strategies.

---

## 论文详细总结（自动生成）

# 论文总结：HYDRE：结合远程监督模型与上下文学习进行单语和跨语言关系抽取

## 1. 核心问题与整体含义（研究动机和背景）

- **任务定义**：远程监督关系抽取（DSRE）旨在从文本中抽取实体对之间的语义关系，训练时使用知识库自动标注的噪声数据（bag-level标注），但推理时需要在句子级进行预测。
- **核心挑战**：(1) 训练与推理的粒度不匹配（bag标注 vs 句子预测）；(2) 训练标签噪声大，导致现有DSRE模型容易混淆细粒度关系（如Nationality vs Place_of_Birth）。(3) 大型语言模型（LLM）虽擅长上下文学习（ICL），但直接应用于DSRE时，噪声标注会损害示例质量，LLM难以正确学习关系语义。
- **研究空白**：当前DSRE模型（如PARE、CIL）依赖任务特定微调，而LLM的ICL潜力未被充分挖掘；跨语言DSRE（尤其低资源语言）极少被探索。
- **本文目标**：提出HYDRE混合框架，将DSRE模型的高召回候选生成能力与LLM的推理能力结合，并扩展到跨语言低资源场景，显著提升句子级和跨语言关系抽取性能。

## 2. 方法论

### 核心思想
- **两阶段混合**：先用训练好的DSRE模型（如PARE）为测试句子生成高召回率的候选关系集合（top-k），再通过动态示例检索策略从训练数据中提取可靠的句子级示例，将其放入LLM的prompt中，引导LLM输出最终的关系。
- **三阶段示例选择流程**：候选关系选择 → 包（bag）选择 → 句子选择。

### 关键技术细节

#### Stage 1: 候选关系选择
- 使用DSRE模型（如PARE）对测试句子q计算每个关系r的置信度 \( f_{\text{PARE}}(q, r) \)，选取top-k（默认k=5）作为候选关系集合 \( R' \)。

#### Stage 2: 包选择
- 对于每个候选关系 \( r \in R' \)，从训练集中选出与该关系相关的包集合 \( \mathcal{B}_r \)，然后对每个包 \( B_j \) 计算得分：
  \[
  \text{score}(B_j, r) = (1 - \lambda) \cdot \text{sim}(q, B_j) + \lambda \cdot f_{\text{PARE}}(B_j, r)
  \]
  其中 \( \text{sim}(q, B_j) = \max_{s \in B_j} \text{sim}(q, s) \) 是语义相似度（使用e5-large-v2或BGE-M3等编码器），\( f_{\text{PARE}}(B_j, r) = \max_{s \in B_j} f_{\text{PARE}}(s, r) \) 是包中句子对关系r的最高置信度。参数 \( \lambda \) 在开发集上调优（英语λ=0.5，印地语λ=0.1），平衡语义相似度与模型置信度。

#### Stage 3: 句子选择
- 从选出的包 \( B_r \) 中，对每个句子s计算覆盖度 \( c(s) = \sum_{r_a \in \text{labelset}(B_r)} \mathbb{I}[f_{\text{PARE}}(s, r_a) > \tau] \)，其中 \( \tau = 0.5 \) 是置信度阈值。
- 选择覆盖度最大的句子；若多个句子覆盖度相同，则选择总置信度 \( \sum_{r_a} f_{\text{PARE}}(s, r_a) \) 最高的句子作为示例。
- 被选句子附带其完整的关系标签集合（即包的所有关系），而非仅候选关系，以支持多标签、增强多样性。
- 最终示例按 \( f_{\text{PARE}}(q, r) \) 升序排列（最相关的示例最靠近查询），构建prompt（包含任务指令、关系定义、示例、查询）。

#### 跨语言扩展
- 三种迁移设置：(1) English-only：仅用英语数据，对Indic语言测试时，不使用DSRE置信度（因为模型未训练），仅用多语言编码器进行语义检索。(2) Translate-train：将英语DSRE训练数据翻译为目标语言，训练对应的PARE-X和CIL-X模型用于置信度和相似度。(3) Translate-test：将目标语言测试查询翻译成英语，应用标准英语HYDRE流程。
- 对于Translate-train，使用CIL-X编码器做语义相似度（因其对比学习产生任务特定表示），PARE-X做置信度估算。

## 3. 实验设计

### 数据集与场景
- **主要数据集**：NYT-10m（英语），包含53.8条句子、722个标签（含30个NA）。测试集通过分层抽样确保关系平衡。
- **跨语言基准**：新构建的四种低资源印地语数据集：Oriya（奥里亚语）、Santali（桑塔利语）、Manipuri（曼尼普尔语）、Tulu（图卢语）。这些语言分属四个语系、不同文字。原始英语NYT-10m测试句被翻译并人工验证。
- **额外评估**：Wiki-20m（英语，81个关系，每包句子数较少）。
- **评估场景**：英语单语、跨语言（三种设置）。

### 基准方法
- **监督DSRE模型**：PARE、CIL及其目标语言版本（PARE-X、CIL-X）。
- **零样本提示LLM**：GPT-4o、Qwen3-235B-A22B、Llama3.1-8B、Llama3.1-8B-FT（微调版）。提示方式包括“直接”和“基于定义”两种。
- **少样本提示（示例检索）**：Random-K、TopK-sim（语义相似）、LM-MMR（多样性感知的MMR）。
- **HYDRE**：使用不同LLM作为推理引擎。

### 对比方法数量
- 共对比了6类方法（监督、零样本、随机少样本、相似性少样本、多样性少样本、HYDRE）在多个LLM上的表现。
- 英语实验：4种LLM × 各类提示方法。
- 跨语言实验：3种设置 × 4种语言 × 多种方法，表格中呈现了宏观F1和微观F1。
- 消融实验：6种变体（w/o候选选择、w/o包选择、w/o句子选择、w/o语义相似、w/o置信度、w/o ICL）在英语和印地语（translate-train）上进行。
- 敏感性分析：k值从1到25，分析Recall和F1变化。
- 额外分析：多标签覆盖、候选瓶颈、位置偏差等。

## 4. 资源与算力

- **文中明确说明**：对于本地推理和微调，使用单张NVIDIA A100 40GB GPU。
- **具体细节**：
  - Llama3.1-8B微调：使用LoRA（lora_alpha=64, lora_r=16, lora_dropout=0.0），余弦学习率调度，warmup 10%，per_device_train_batch_size=8，gradient_accumulation_steps=4，最大训练步数5000（约4个epoch），在单A100上完成。
  - Qwen3-235B-A22B（TogetherAI）和GPT-4o（OpenAI）作为外部API调用，未提及本地部署。
  - 语义检索模型e5-large-v2、BGE-M3、CIL-X编码器均使用本地或API。
- **未明确说明**：PARE和CIL模型训练所需的算力总时长、成本；跨语言设置中mBERT预训练的资源消耗。

## 5. 实验数量与充分性

- **实验数量非常充分**：
  - 英语：主表（Table 2）报告了5种LLM × 6类方法的结果，并附有统计显著性检验（McNemar检验，p<10^{-5}）。
  - 跨语言：三个设置下各4种语言，每个语言详细结果在附录（Tables 5-7）。
  - 消融：英语和印地语两套消融（Table 3），还包括Stage 3的候选评分消融（Table 8）、位置偏差分析、候选瓶颈分析（Table 12）、多标签覆盖分析（Table 10-11）。
  - 敏感性：k值分析（Figure 15）。
  - 额外数据集：Wiki-20m（Table 4）。
  - 定性分析：混淆矩阵（Figures 13-14）、工作/失败案例（Figures 5-12）。
- **实验客观公平**：对比了当前最强DSRE模型（PARE、CIL等）、多种LLM提示策略、以及不同示例选择方法。消融实验系统评估了每个组件的贡献。
- **潜在不足**：跨语言实验仅包含四种印地语，未扩展到其他语系；低资源语言缺乏人工标注的验证集（依赖翻译数据），且训练数据通过自动翻译获得，可能存在翻译偏差。

## 6. 主要结论与发现

- **HYDRE显著优于现有方法**：
  - 英语：HYDRE（GPT-4o）达到63/60 F1（微/宏），比最强监督模型CIL（43/32）和零点GPT-4o（56/57）分别提升20/28和7/3个点。
  - 跨语言：平均提升17 F1点（印地语），尤其在Translate-train和Translate-test设置下，HYDRE（Llama3.1-8B-FT）达到45/28和51/37。
- **组件贡献**：
  - 候选选择（Stage 1）降低复杂度，但过滤掉金关系时会造成性能瓶颈（约14%查询）。
  - 包选择（Stage 2）在英语中降7 F1，在印地语中降3 F1。
  - 句子选择（Stage 3）在英语中降6 F1，并将多标签恢复率提高（从38%提升至47%）。
  - 语义相似度和模型置信度在不同场景下权重不同：英语侧重语义相似度；印地语（translate-train）侧重置信度。
- **ICL的重要性**：去除ICL（仅提供候选关系）导致英语降7 F1、印地语降12 F1。
- **可扩展性**：k=5时达到最佳平衡；在Wiki-20m上也获得显著增益。

## 7. 优点

1. **创新混合框架**：首次系统地将DSRE模型的高召回与LLM的推理能力结合，克服了噪声标注对ICL的负面影响。
2. **动态示例检索**：三阶段选择策略（候选→包→句子）联合了语义相似度、模型置信度和标签覆盖度，有效提取高质量句子级示例，支持多标签。
3. **跨语言扩展**：提出三种迁移设置，并构建了首个低资源印地语DSRE基准，涵盖四种语系语言，填补了领域空白。
4. **实验全面性**：在英语和跨语言、多种LLM、多种提示策略下进行了详尽的对比和消融，统计显著性检验支持结论。
5. **实用性与开源**：代码和数据集已发布；该方法可部署于本地开源模型（Llama），降低API成本。
6. **定性分析深入**：提供了丰富的混淆矩阵和案例，揭示了错误类型（位置偏见、候选瓶颈、语义重叠），为后续改进指明方向。

## 8. 不足与局限

1. **低资源语言验证范围有限**：仅包含四种印地语，未覆盖其他语系（如非洲、东南亚语言），且数据集通过翻译获得，质量依赖机器翻译与人工校验，可能存在翻译误差和实体错位。
2. **候选生成瓶颈**：DSRE模型的Recall@5并非100%（约85%-71%），当金关系不在TOP-5时，HYDRE表现劣于零点提示，约14%查询受影响。
3. **位置偏差**：将最高置信度示例放在最接近查询处，导致LLM有34%的错误来源于过度信任第一个候选，造成部分多标签遗漏。
4. **计算资源**：大型LLM（如Qwen3-235B、GPT-4o）推理成本高；LoRA微调仍需单A40训练约4 epoch；对于极高资源场景（如PubMed、金融），未测试。
5. **未覆盖监督/人类标注场景**：仅适用于DSRE设置，未验证在干净标注数据上的效果；示例选择策略在完全监督下可能不再必要。
6. **长文本与高密度包限制**：句子选择假设仅需少量句子即可推理，但在高密度包（如Wiki-20m中1.8句/包）时Stage 3句选择的优势减弱。
7. **高token消耗**：跨语言设置中，高token fertility（如Santali）导致prompt长度超标，部分消融实验无法执行（以“-”标记）。

（完）
