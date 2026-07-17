---
title: "AnchorAlign: A Novel Anchor Alignment-enhanced Generative Method for Joint Named Entity Recognition and Relation Extraction"
title_zh: "AnchorAlign: 一种新颖的锚点对齐增强生成式联合命名实体识别和关系抽取方法"
authors: "Xiaolong Weng, Yuanyun Zhou, Boyu Qiu, Zehua Wang, Ying Xiong, Buzhou Tang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1898.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 基于锚点对齐的生成式联合命名实体识别和关系抽取
tldr: 针对联合命名实体识别和关系抽取中实体与关系、关系与关系之间的不对齐问题，提出AnchorAlign方法，通过锚点实体选择机制和锚点对齐策略，在生成式框架下实现更精准的联合抽取。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1898/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1898/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 981, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1898/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1656, \"height\": 999, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1898/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 665, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1898/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 660, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1898/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 665, \"height\": 440, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1612, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 152, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 503, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1898/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1663, \"height\": 416, \"label\": \"Table\"}]"
motivation: 现有生成式联合方法存在实体与关系间的错配问题。
method: 引入锚点实体选择机制和对齐策略，增强生成式的联合抽取。
result: 在多个数据集上显著提升联合NER和RE的准确率。
conclusion: 锚点对齐是提升生成式联合信息抽取效果的有效技术。
---

## Abstract
Named Entity Recognition (NER) and Relation Extraction (RE) are two fundamental and interdependent tasks in information extraction (IE), aiming to identify entities and relations from unstructured text. Recently, generative methods have become mainstream instead of discriminative methods for IE, especially joint multi-task IE, due to their promising performance and flexibility. For joint NER and RE, existing methods suffer from misalignment between entities and relations, as well as misalignment among relations. To address these issues, we propose AnchorAlign, a novel generative method enhanced by anchor alignment. Specifically, we first introduce an anchor entity selection mechanism to identify key entities in the text as anchor points, which serve as semantic pivots to bridge the two tasks. Then, we design a dual-level anchor alignment module: at the semantic level, we construct a cross-task semantic alignment space to align the semantic representations of anchor entities and their associated relations; at the generation level, we introduce an anchor-guided generation constraint to guide the model to generate entities and relations with strict alignment based on the anchor points. Extensive experiments on five benchmark datasets show that AnchorAlign outperforms state-of-the-art baselines, demonstrating its effectiveness. Our work provides a new perspective for optimizing the joint modeling of NER and RE, and has potential to be extended to more complex multi-task IE such as NER and Event Extraction (EE).

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在生成式联合命名实体识别（NER）和关系抽取（RE）任务中，实体与关系之间存在**错位（misalignment）**，同时关系与关系之间也存在错位。现有生成式方法主要关注任务间依赖（NER→RE），但忽视了任务内依赖（RE内部的关系-关系对齐），且输出范式不统一。
- **背景与动机**：信息抽取（IE）中 NER 和 RE 是基础且相互依赖的子任务，生成式方法（如 UIE、REBEL）因其灵活性和强大性能成为主流。然而，现有对齐机制往往仅将 NER 中的实体与 RE 中最接近的实体对齐，忽略了同一实体参与多个关系时的偏差，导致联合抽取精度受损。作者旨在通过引入**锚点实体（anchor entity）** 统一输出范式并设计新的对齐机制，同时考虑任务间与任务内对齐，以提升生成式联合抽取的效果。

### 2. 论文提出的方法论：核心思想、关键技术细节

#### 核心思想
- **锚点实体**：将 NER 和 RE 共享的实体定义为**实体-关系锚点**，将多个关系共享的实体定义为**关系-关系锚点**，以此作为跨任务和任务内对齐的语义枢纽。
- **双级对齐**：
  - **语义级别对齐**：在概率空间中对齐 NER 解码器与 RE 解码器（正向和反向）的输出分布，以及正向与反向 RE 解码器之间的分布，确保决策层一致性。
  - **生成级别约束**：推理时利用 NER 输出作为高置信度参考，过滤掉包含未识别实体的关系三元组，提升精度。

#### 关键技术细节
1. **锚点实体选择机制**：自动识别文本中同时出现在 NER 和 RE 中的实体作为实体-关系锚点，以及出现在多个关系中的实体作为关系-关系锚点。
2. **输出范式**：采用**实体分组（entity-centric factorization）** 方式，将同一主语的所有关系聚合成块，减少冗余，提升对齐效率。具体为 Paradigm 3（NER 输出全部实体，RE 输出按主语分组的关系块）。
3. **跨任务语义对齐损失**：
   - NER-RE 对齐：让 RE 解码器（正向和反向）的输出概率分布向 NER 的分布靠拢，使用 KL 散度。
   - 正向-反向 RE 对齐：对于同一关系三元组，强制正向和反向解码器的概率分布对称（使用对称 KL 散度）。
4. **负抑制损失**：对无关令牌（不在 NER 或 RE 目标集合中的令牌）施加概率惩罚，进一步锐化分布。
5. **总体训练目标**：生成损失（交叉熵）+ α × NER-RE 对齐损失 + β × 正向-反向对齐损失 + γ × 负抑制损失。
6. **生成约束**：推理时合并正向和反向 RE 输出后，只保留两个实体都在 NER 输出中的三元组，提升精度。
7. **两阶段训练**：任务自适应预训练（包含实体类型理解、渐进目标激活）+ 监督微调（课程学习：先简单样本后全数据）。

### 3. 实验设计：数据集、benchmark、对比方法

- **数据集**：5个标准基准数据集：
  - ACE05（新闻领域，5105样本）
  - SciERC（科学论文，1861/275/551）
  - ADE（医学病例，约13845样本，10折交叉验证）
  - NYT（远监督，56196/5000/5000）
  - Text2DT（中文医疗决策树，7400/100/3144）
- **评估指标**：
  - Relation Strict F1（实体提及、类型、关系类型均正确）
  - Relation Boundary F1（仅要求提及和关系类型正确，忽略实体类型）
- **对比方法**：
  - **生成式**：UIE、REBEL、YAYI-UIE、InstructUIE、KnowCoder
  - **判别式**：BiSPN、PL-Marker、USM

### 4. 资源与算力

- 论文**未明确说明**训练所使用的 GPU 型号、数量及训练时长。
- 仅报告了推理阶段参数：模型为 BART-Large（914M 参数），在 ACE05 测试集上单 GPU batch size 40，推理时间 105.1 ms/sample，吞吐量 9.51 samples/s。训练相关资源未披露。

### 5. 实验数量与充分性

- **实验数量**：总计进行了8组主要实验：
  1. 主结果对比（5个数据集 × 2个指标，共10项比较）。
  2. 输出范式设计对比（4种范式 × 3个数据集）。
  3. 消融实验（8个组件/策略的逐个移除）——表2。
  4. 复杂结构分析（嵌套实体、重叠关系）——表3。
  5. 推理效率比较——表4。
  6. 案例研究（两个示例）。
  7. 共享实体密度与范式增益的关系分析（表7）。
  8. 语义对齐损失可视化（附录C）。
- **充分性与公平性**：
  - 对比了多个SOTA生成式和判别式方法，覆盖不同架构。
  - 消融实验覆盖了训练和推理两个阶段的所有关键组件，验证了各自贡献。
  - 在复杂结构（嵌套实体、重叠关系）上专门分析，显示了方法的鲁棒性。
  - 不足之处：NYT 和 Text2DT 仅报告了 Boundary F1（因数据集特性），但已与先前工作保持一致；部分基线（如 USM）仅报告了部分数据集，无法完全公平对比；超参数调节仅基于开发集，且 ADE 使用了 10 折交叉验证，较为合理。

### 6. 论文的主要结论与发现

- **主要结论**：AnchorAlign 在五个数据集上达到了新的 SOTA 或接近 SOTA 的性能，尤其在 Relation Boundary F1 上在 ACE05、SciERC、ADE、Text2DT 上均取得最高分（分别提升 0.72%、1.00%、0.88%、0.12%）。Relation Strict F1 在 SciERC 和 ADE 上超过之前最佳。
- **关键发现**：
  - 实体分组输出范式（Paradigm 3）优于其他三种，且性能增益与共享实体密度正相关。
  - 跨任务语义对齐是提升效果的最关键组件（移除下降 2.00%），其中 NER-RE 对齐贡献最大。
  - 推理阶段的生成约束和双向解码器聚合协同作用，分别提升精度和召回，组合使用效果最佳（联合移除下降 2.72%）。
  - 对齐机制在处理重叠关系时效果显著（SciERC 提升 +2.64%），但对嵌套实体边界问题改善有限。

### 7. 优点

1. **创新性**：
   - 首次将锚点实体概念系统化，统一了现有的多种输出范式，并衍生出两种新范式。
   - 同时考虑任务间（NER↔RE）和任务内（RE↔RE）对齐，弥补了现有工作的盲区。
   - 对齐在概率空间而非特征空间进行，更有利于决策层一致性。
2. **实验全面性**：
   - 覆盖了新闻、科学、医学、远监督、中文等多个领域的数据集，跨领域验证了方法通用性。
   - 消融实验设计精细，分别量化了训练组件和推理策略的贡献。
   - 对复杂结构（嵌套、重叠）进行专门分析，揭示了方法的优势与局限。
3. **工程细节**：
   - 使用两阶段训练（预训练+微调）和课程学习，有效利用数据增强注入先验知识。
   - 负抑制损失设计巧妙，无额外监督信号即可锐化分布。

### 8. 不足与局限

1. **方法层面**：
   - 语义对齐虽改善了实体边界，但无法纠正实体语义错误（如实体封装错误），且对齐约束无法完全补偿模型领域知识不足导致的头尾颠倒或关系方向错误。
   - 依赖于共享实体密度，在共享实体较少的场景下（如 ACE05 仅为 3.3% 样本级别共享密度）提升有限。
2. **实验局限**：
   - 仅评测了英文和中文数据集，未验证多语言泛化性。
   - 推理效率较低（914M 参数，105ms/sample），对比单解码器判别式方法有显著差距。
   - 未对不同数据增强策略做消融，预训练阶段的具体增益仅通过移除预训练整体评估（下降 1.17%），未分解子阶段。
   - 未报告训练时间、GPU 型号等计算资源细节。
3. **应用限制**：
   - 需要复杂的三解码器架构（NER、正向RE、反向RE），增加模型训练和部署成本。
   - 锚点选择机制依赖标注数据中的共享实体，对低资源或无标注场景可能需要额外设计。

（完）
