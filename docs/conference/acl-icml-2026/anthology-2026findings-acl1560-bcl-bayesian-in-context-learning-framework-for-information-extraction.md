---
title: "BCL: Bayesian In-Context Learning Framework for Information Extraction"
title_zh: BCL：面向信息抽取的贝叶斯上下文学习框架
authors: "Haoliang Liu, Chengkun Cai, Xu Zhao, Han Zhu, Shizhou Huang, Xinglin Zhang, Tao Chen, Jenq-Neng Hwang, Zhang Huaping, Lei Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1560.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 信息抽取框架
tldr: 当前基于上下文学习的信息抽取方法缺乏系统优化且泛化性差。本文提出BCL-IE，首个使用粒子滤波和贝叶斯更新来系统优化标签表示的信息抽取框架。该方法适用于序列标注和关系分类范式，在多个IE基准上取得显著提升。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1560/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 837, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1560/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 818, \"height\": 771, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1560/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1560/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1486, \"height\": 691, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1560/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1481, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1560/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1469, \"height\": 768, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1642, \"height\": 959, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 782, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 834, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 559, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 819, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 821, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 998, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 735, \"height\": 410, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1560/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 905, \"height\": 317, \"label\": \"Table\"}]"
motivation: 现有基于上下文学习的信息抽取方法性能不稳定且缺乏通用优化。
method: 提出贝叶斯上下文学习框架BCL-IE，通过粒子滤波和贝叶斯更新迭代优化标签表示。
result: 在多个信息抽取任务上，BCL-IE显著优于现有上下文学习方法。
conclusion: 贝叶斯优化能有效提升上下文学习在信息抽取中的性能与泛化能力。
---

## Abstract
Existing information extraction (IE) tasks increasingly adopt in-context learning (ICL) with large language models. However, current approaches either show inconsistent performance across model scales or lack systematic optimization and generalizability. Building on this, we propose BCL-IE (Bayesian In-Context Learning Framework for Information Extraction), the first optimization framework that uses particle filtering with Bayesian updates to systematically refine label representations across IE tasks. Through four steps—initialization, observation, weight update, and resampling, BCL-IE generalizes to both sequence labeling and relation classification paradigms. Extensive experiments demonstrate substantial improvements over existing approaches (up to 30%), achieving prior performance while other methods either fail to generalize or show limited effectiveness.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **背景**：当前信息抽取（IE）任务广泛采用基于大规模语言模型（LLM）的上下文学习（ICL）方法。现有方法主要分为两类：任务迁移方法（如 ChatIE、CodeIE）和指南式方法（如 GuideNER）。
- **问题**：
  - 任务迁移方法在不同模型规模上性能不稳定：在超大型商业模型上有效，但在轻量级模型（如 7B）上甚至不如简单的一次性提示（one-shot）。例如，ChatIE 在 NER 任务上远低于 one-shot，CodeIE 在 RE 任务上接近零 F1。
  - 指南式方法（GuideNER）仅适用于 NER，且依赖简单的频率筛选，缺乏系统优化和泛化能力。
- **整体含义**：需要一种通用、可控且可优化的 ICL 框架，能够统一处理序列标注（NER）和关系分类（RE）任务，并在不同模型规模上保持稳定高效。

### 2. 提出的方法论（核心思想、关键技术细节）

- **核心思想**：将粗粒度的标签（如“Person”）分解为多个细粒度语义子类别（如“athlete”、“politician”），这些子类别作为**可控离散变量（粒子）**。通过粒子滤波（Particle Filtering）和贝叶斯更新，以迭代方式优化每个粒子的权重，使 LLM 更好地理解标签在特定数据集中的具体含义。
- **关键技术细节**：
  1. **粒子表示**：每个粒子是一个子类别模式-标签对，如 `(athlete, Person)`. 在时刻 t，规则配置为 \( R_t = \{(p_i^{(t)}, c_i, w_i^{(t)})\} \)。
  2. **初始化**：从训练数据中用 LLM 提取候选子类别模式（每个标签初始生成 N=10 个粒子），并基于语言模型的困惑度（Perplexity）计算先验权重：\( w_i^{(0)} = \exp(-PPL(p_i^{(0)})) / \sum \exp(...) \)，困惑度越低（语言更自然）权重越高。
  3. **观察（评估）**：对每个粒子，在验证批次上执行 ICL 推理，计算其平均对数概率（似然）作为性能得分 \( y_i^{(t)} = \exp(L_c(p_i^{(t)},\theta)) / \sum \exp(...) \)。
  4. **权重更新（贝叶斯后验）**：结合先验和似然，更新粒子权重：\( \tilde{w}_i^{(t)} = w_i^{(t-1)} \cdot \exp(\beta \cdot y_i^{(t)}) \)，再归一化。
  5. **重采样**：两层策略：Tier-1 保留权重前 50% 的粒子（去除低质量），Tier-2 通过 LLM 变异（ refining / generalization / contextualization ）产生新粒子，新粒子权重基于困惑度计算。保留和新生粒子组成下一轮规则集。
  6. **收敛条件**：连续 3 次迭代相对提升 < 3%，或训练样本用完。

### 3. 实验设计

- **数据集**：6 个主流 IE 基准
  - NER：CoNLL-2003（新闻，4类）、ACE2005（新闻/对话，7类）、GENIA（生物医学，5类）
  - RE：NYT（新闻，24类）、CoNLL04（通用，5类）、SciERC（科学论文，7类）
- **模型**：4 种不同规模和来源的 LLM：Qwen2.5-3B、Qwen2.5-7B、Llama3.1-8B、Pixtral-12B
- **对比方法**：
  - One-shot（1个示例）
  - ChatIE（转化为对话任务）
  - CodeIE（转化为代码生成）
  - GuideNER（基于指南的规则方法，仅适用于 NER）
  - BCL-IE（本文方法）
- **评估指标**：实体级 F1（NER 要求边界和类型完全匹配；RE 要求实体和关系类型均匹配），以及 Token 成本（平均每样本输入+输出 tokens）
- **设置**：温度=0.0，固定种子=42，粒子数=10，观察批次大小在 {1,3,5,7,9,11,13,15} 中网格搜索最优。

### 4. 资源与算力

- **文中提及**：使用配备 H100 GPU 的计算集群，PyTorch 2.6.0 和 Transformers 4.51.3。
- **未明确说明**：未给出具体 GPU 数量、训练时长或总计算量（如 GPU 小时数）。仅说明方法在优化阶段需要 \( O(K \times M) \) 次 LLM 推理，其中 K=10，M 约为训练集的 3%~5%。

### 5. 实验数量与充分性

- **实验数量**：
  - 主实验：4 种模型 × 6 个数据集 × 5 种方法（部分方法不适用RE），共约 4×6×5=120 个条件，但 GuideNER 仅 NER，实际表格含 80+ 项。
  - 消融实验（表2）：移除权重更新、Tier-1 重采样、Tier-2 重采样，共 4 组对比。
  - 参数敏感性：训练数据量（5 种比例）、上下文窗口长度（8 种长度），共 2 组实验。
  - 跨模型泛化（表3）：2 种源模型规则迁移到 GPT-3.5-turbo。
  - 语义分解消融（附录C）：2 种模型 × 2 数据集。
  - 长尾分析（附录D）：2 种模型 × 2 数据集 × 3 频次组。
- **充分性与公平性**：
  - 实验覆盖多个模型尺度、多领域数据集，结论具有统计显著性（p<0.05）。
  - 所有方法在同一设置下比较，公平。
  - 消融实验系统验证了每个组件的贡献。
  - 不足之处：缺少对更大规模模型（如 70B）的验证；未与其他优化 ICL 方法（如 Dr.ICL、MAPS）直接对比。

### 6. 主要结论与发现

- BCL-IE 在所有模型和数据集上均优于现有方法，F1 提升最高达 30%（如 Qwen2.5-7B 在 CoNLL03 上 72.83 vs 65.10）。
- 任务迁移方法（ChatIE、CodeIE）在轻量模型上性能崩坏，而 BCL-IE 保持稳定。
- BCL-IE 是首个在 RE 任务上取得有效结果的 ICL 方法（其他方法接近 0 F1）。
- 数据效率极高：仅需 1% 训练数据即可接近最优性能（CoNLL03 上 69.12 vs 峰值 72.83）。
- 贝叶斯权重更新是核心组件（去除后降 11 F1），多样性变异（Tier-2）也至关重要（降 9.85 F1）。
- 学习到的规则可跨模型迁移（从 Llama-3.1-8B 迁移到 GPT-3.5-turbo 性能提升）。

### 7. 优点

- **系统性优化**：首次将贝叶斯推理与粒子滤波引入 ICL 的规则优化，避免了启发式筛选。
- **通用性**：统一适用于 NER 和 RE 两类主流 IE 任务，而此前方法往往专精一种。
- **数据高效**：只需少量验证样本即可收敛，降低了标注成本。
- **可解释性**：粒子的权重反映了不同子类别模式对最终性能的贡献。
- **跨模型泛化**：优化结果可迁移到更强大的模型，无需重新优化。
- **鲁棒性**：对长尾实体频次不敏感，频率分层性能差距 < 2 F1。

### 8. 不足与局限

- **计算成本**：优化阶段需要 \( O(K \times M) \) 次 LLM 推理（K=10, M≈3-5%训练集），虽低于全数据遍历，但仍比一次性方法昂贵，不适合频繁更新场景。
- **样本偏差风险**：理论上粒子滤波可能偏向训练集中高频模式，尽管实验显示影响轻微，但未在极度长尾分布（如极稀有实体）上验证。
- **模型规模覆盖**：未测试 70B 以上大模型（如 Llama-3-70B、GPT-4），无法确定在超大规模模型上的相对优势。
- **依赖生成质量**：初始粒子和变异依赖于 LLM 的生成能力，若 LLM 本身对语义分解能力弱，可能影响上限。
- **缺乏与其他先进 ICL 优化方法的直接对比**：如 C-ICL、Dr.ICL 等，虽然它们并非专门针对 IE 规则优化，但可视为竞争基线。
- **无开放代码/数据声明**：文中提到代码将开源，但未给出链接，影响可复现性。

（完）
