---
title: "EXCEEDS: Extracting Complex Events via Nugget-based Grid Modeling in Scientific Domain"
title_zh: "EXCEEDS: 通过基于核的网格建模抽取科学领域中的复杂事件"
authors: "Yi-Fan Lu, Xian-Ling Mao, Bo Wang, Xiao Liu, He-Yan Huang (黄河燕)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.271.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 科学领域事件抽取
tldr: 论文针对科学领域事件抽取缺乏数据集和专用方法的问题，构建了大规模多事件文档级数据集SciEvents（包含2508文档和24381个事件），并提出基于核的网格建模方法EXCEEDS来抽取复杂事件。该方法考虑了科学文档中更密集的核和更复杂的信息形式。实验证明了方法的有效性，为科学领域事件抽取提供了重要基准与方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 781, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 789, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1637, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 812, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1649, \"height\": 808, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1653, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1616, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1624, \"height\": 797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1627, \"height\": 960, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1610, \"height\": 1327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.271/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1621, \"height\": 2327, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1632, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1560, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1615, \"height\": 614, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 610, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 493, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 569, \"height\": 540, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 815, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 681, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 690, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 719, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 701, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 754, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 718, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 713, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 585, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 780, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 695, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1622, \"height\": 1747, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1595, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1589, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1030, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1242, \"height\": 521, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1158, \"height\": 522, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.271/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1221, \"height\": 882, \"label\": \"Table\"}]"
motivation: 科学文档中事件核更密集、信息形式更复杂，现有数据集和方法难以支持有效的科学事件抽取。
method: 提出基于核的网格建模方法EXCEEDS，构建了大规模多事件文档级数据集SciEvents。
result: 构建的SciEvents数据集包含2508文档和24381个事件，实验表明EXCEEDS方法能有效抽取科学领域复杂事件。
conclusion: 该工作填补了科学领域事件抽取的空白，为后续研究提供了数据集和方法基础。
---

## Abstract
It is crucial to understand a specific domain by events. Extensive event extraction research has been conducted in many domains such as news, finance, and biology. However, event extraction in scientific domain is still insufficiently supported by comprehensive datasets and tailored methods. Compared with other domains, scientific domain has two characteristics: (1) denser nuggets and events, and (2) more complex information forms. To solve the above problem, considering these two characteristics, we first construct SciEvents, a large-scale multi-event document-level dataset with a schema tailored for scientific domain. It consists of 2,508 documents and 24,381 events under multi-stage manual annotation and quality control. Then, we propose EXCEEDS, an end-to-end scientific event extraction framework by encoding dense nuggets into a grid matrix and simplifying complex event extraction as a nugget-based grid modeling task. Experiments on SciEvents demonstrate state-of-the-art performances of EXCEEDS. Both the SciEvents dataset and the EXCEEDS framework are released publicly to facilitate future research.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：科学领域的事件抽取（Event Extraction, EE）缺乏专门的数据集和适配方法。现有数据集和方法多针对新闻、金融、生物等域，但科学文本（尤其论文摘要）具有两个显著特性：
  - **更密集的核（nugget）与事件**：单位文本内事件、论元、核的密度远高于其他领域。
  - **更复杂的信息形式**：包括层级关系（子事件）、不连续论元、重叠核、逆序核、长距离论元链接。
- **研究动机**：科学文献快速增长，亟需有效的事件知识管理工具；但现有资源难以刻画上述特性，导致科学领域EE进展缓慢。
- **整体含义**：本文填补了科学领域EE的空白，通过构建大型数据集SciEvents和设计专用方法EXCEEDS，为后续研究提供了基准和方案。

## 2. 方法论
### 核心思想
- 将文档中所有token对的**关系**编码到一个**词-词网格（word-word event grid）**中，将事件抽取任务简化为**基于核的网格建模**问题。
- 网格中的关系类型包括：
  - **HTL（头-尾链接）**：表示核内相邻token的先后顺序。
  - **THL（尾-头链接）**：将核的最后一个token连回第一个token，携带核类型信息。
  - **EAL（事件-论元链接）**：表示触发词与论元之间、或主事件触发词与子事件触发词之间的关联。

### 关键技术细节
1. **上下文编码**：使用预训练语言模型（RoBERTa-large） + 双向LSTM + 条件层归一化（CLN），获得上下文感知的token表示 \(H \in \mathbb{R}^{l \times d}\)。
2. **成对网格构建**：对每对token \((x_i, x_j)\)，拼接表示 \(z_{i,j} = [h_i; h_j; d_{i,j}]\)（含相对距离嵌入），经MLP投影到网格特征 \(g_{i,j} \in \mathbb{R}^{C_g}\)。
3. **网格精化器**：使用K层轻量2D卷积残差块，在网格空间进行信息传播，输出精化后的网格表示 \(\tilde{G}\)。
4. **训练损失**：多标签分类损失（multi-label categorical cross-entropy），对每个网格单元同时优化正负标签。
5. **推理解码**：
   - 通过HTL链和THL闭合恢复核的跨度与类型。
   - 通过EAL连接触发词与论元，并使用模式约束过滤无效链接。
   - 算法使用DFS遍历，并应用两个剪枝启发式：① HTL链必须被THL关闭；② 论元必须能链接到至少一个触发词。

## 3. 实验设计
### 数据集
- **SciEvents**：自建数据集，包含2,508篇ACL会议摘要、24,381个事件、56,411个论元。模式涵盖10种事件类型和20种论元类型，明确标注了不连续、重叠、逆序核以及子事件等复杂结构。
- 划分为80%/10%/10%训练/开发/测试。

### Benchmark与对比方法
- **全局模型**：OneIE（联合建模实体、关系、事件）。
- **判别模型**：EEQA、Tagprime、PAIE、DEEIA、ScentedEAE。
- **生成模型**：BartGen、DEGREE、KnowCoder（基于LLaMA 2-7B）。
- 评估指标：Trigger Identification (TI)、Trigger Classification (TC)、Argument Identification (AI)、Argument Classification (AC)、Event Correlation (EC，衡量子事件层级关系)。
- 此外，在复杂场景子集（不连续、重叠、逆序、子事件）上单独评测。

## 4. 资源与算力
- **硬件**：大部分模型在NVIDIA RTX 3090上训练/推理；基于LLM的KnowCoder在NVIDIA A800 80GB PCIe上使用LoRA微调。
- **训练成本**（表8：平均每epoch GPU小时）：
  - EXCEEDS：0.0609小时/epoch（训练），0.1692小时（推理）。
  - 对比模型：OneIE 0.1816；Tagprime 0.2510（ED）；PAIE 0.7536；DEGREE 0.3639；KnowCoder 0.2381（ED）+1.5869（EAE）等。
- **超参数**：EXCEEDS使用RoBERTa-large学习率1e-5，批大小2，网格通道256，精化层数K=2，核大小3。

## 5. 实验数量与充分性
- **实验组数**：
  - **整体对比**（表3）：所有模型在5个指标上的F1值，含3次独立运行取平均。
  - **复杂场景对比**（表4）：在4类复杂结构子集上的性能。
  - **消融实验**：移除上下文模块（CLN等）和移除网格精化器（2D卷积块），验证各组件贡献。
  - **误差分析**（图4、图5）：分类错误分布、识别错误类型（遗漏/边界/重叠）。
- **充分性与公平性**：
  - 对比模型均使用相同预训练骨干（RoBERTa-large或BART-large）；KnowCoder使用LLaMA 2-7B属不同骨干但已说明。
  - EAE-only方法统一使用表现最佳的Tagprime预测触发词，避免ED差异影响。
  - 多次运行报告标准差，结果具统计意义。
- **不足**：未进行跨域泛化测试（仅NLP领域）；未对比最新基于GPT-4等闭源LLM的零样本方法。

## 6. 论文的主要结论与发现
1. **SciEvents数据集**反映了科学文本的信息密集性和结构复杂性（每100 token含5.54事件、39.49核token；33.7%重叠核、25.63%子事件）。
2. **EXCEEDS方法**在整体性能上达到SOTA，尤其在AC（43.20%）和EC（48.25%）上显著优于次优模型（分别高0.51%和0.53%）。
3. **复杂场景挑战**：不连续、重叠、逆序核上所有模型性能大幅下降，但EXCEEDS仍领先；生成模型（DEGREE、KnowCoder）在复杂结构上表现更差，甚至无法处理逆序或重叠。
4. **主要错误模式**：识别错误中遗漏占89.2%（TI）和84.6%（AI），边界精度非瓶颈；分类错误集中于语义相似类型（如MDS与WKS、TriedC.与BaseC.、Subject与Object）。
5. **消融实验**：去掉上下文模块导致AC下降1.06%，去掉网格精化器也有一致下降，说明两者均重要。

## 7. 优点
- **数据集创新**：首个面向科学领域、同时标注层级/不连续/重叠/逆序等复杂结构的大规模文档级EE数据集，模式设计基于论文修辞结构（背景、相关工作、方法、结果）。
- **方法统一性强**：EXCEEDS通过单一网格表示统一处理事件检测、论元抽取和事件关联，无需分离管道，能捕获全局上下文和复杂关系。
- **端到端且轻量**：仅需原始文本输入，网格精化采用2D卷积而非Transformer，计算复杂度可控（表8显示训练成本较低）。
- **评估全面**：引入Event Correlation指标评价子事件抽取，并专门分析复杂场景，揭示了现有方法的局限性。

## 8. 不足与局限
- **数据范围限制**：仅基于ACL论文摘要，未覆盖全文（图表、公式、跨节引用），且仅限NLP子领域，**跨学科泛化性未验证**。
- **复杂场景性能仍低**：不连续核F1仅13.86%，逆序核7.27%，说明模型处理罕见复杂结构的能力有限。
- **网格复杂度**：O(l²)空间和时间复杂度对超长文档（如全文）可能成为瓶颈。
- **缺失多模态与跨域基准**：未与多模态EE或更多通用域数据集（如MAVEN）对比。
- **LLM对比深度不足**：仅实验了KnowCoder（LLaMA 2-7B），未测试GPT-4等更大模型，且KnowCoder在复杂场景上表现不佳可能与微调策略有关。

（完）
