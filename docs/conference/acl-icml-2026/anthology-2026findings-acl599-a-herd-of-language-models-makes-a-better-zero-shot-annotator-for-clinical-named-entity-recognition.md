---
title: A Herd of Language Models Makes a Better Zero-shot Annotator for Clinical Named Entity Recognition
title_zh: 一群语言模型比单个模型更好地实现零样本临床命名实体识别标注
authors: "Seiji Shimizu, Shoko Wakamiya, Eiji Aramaki"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.599.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 命名实体识别：临床NER
tldr: 临床命名实体识别标注成本高，大语言模型零样本标注质量有限。本文提出MARY，聚合多个不同LLM（通用、医疗适配、NER专用）的标注，并针对少数模型提取的实体（真阳性多但噪声大）设计标签建模方法。在临床NER数据集上显著提升零样本标注质量。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 665, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1486, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1431, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1626, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.599/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 793, \"height\": 443, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1418, \"height\": 1464, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 672, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 520, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 515, \"height\": 506, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1151, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.599/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1152, \"height\": 640, \"label\": \"Table\"}]"
motivation: 大语言模型在临床NER中零样本性能有限，且单一模型标注不稳定。
method: 提出MARY方法，聚合多个异构LLM的标注结果，并对少数模型提取的实体进行置信度建模。
result: 在多个临床NER数据集上，MARY的零样本标注质量显著优于单个最佳模型。
conclusion: 多模型聚合与噪声建模能有效提升零样本NER标注效果。
---

## Abstract
Clinical named entity recognition (NER) remains difficult to scale due to the high cost of manual annotation. Although large language models (LLMs) enable zero-shot annotation, their performance on clinical NER is still limited. To this end, we improve the annotation quality by aggregating annotations from *a herd of diverse LLMs*, including general-purpose, medically adapted, and NER-specialized models. A key challenge in this multi-LLM setting is effectively leveraging entities extracted by only a minority of models: although they account for a substantial portion of true positives, they are heavily intermixed with noise. To address this, we introduce **MARY**, a label-modeling method for **M**ulti-LLM **A**nnotation using **R**epresentation learning to capture contextual similarit**Y**. During aggregation, MARY selectively incorporates minority-extracted entities whose contexts are similar to those of majority-extracted entities, yielding more reliable and comprehensive annotations. Experimental results show that MARY improves the average F1 score by 8.6% over vanilla zero-shot baselines while reducing annotation costs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **临床命名实体识别（NER）** 是临床自然语言处理的基础任务，但构建高性能NER系统面临两大障碍：一是严格的数据共享限制使得标注临床语料困难，二是专家标注成本高、耗时长。
- 虽然大型语言模型（LLM）能够实现零样本（zero-shot）标注，但在临床NER上性能仍有限。单一模型无论通用、医疗适应还是NER专用，都难以达到可靠标注质量。
- 本文核心动机：**通过聚合多个具有不同特性的LLM（通用、医疗适应、NER专用）的输出，来提升零样本临床NER的标注质量**，并将聚合后的高质量自动标注用于下游模型训练，从而大幅减少人工标注成本。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- 利用 **多LLM群（herd of diverse LLMs）** 进行零样本标注，每个模型生成实体集合。标注后，按模型共识程度将实体分为三个层级：\(E_3\)（所有3个模型都提取）、\(E_2\)（2个模型提取）、\(E_1\)（仅1个模型提取）。
- 多数模型提取的实体（\(E_2 \cup E_3\)）精度高但覆盖有限；少数模型提取的实体（\(E_1\)）包含大量真阳性，但混杂噪声。
- 关键挑战：**如何有效利用\(E_1\)中的真阳性实体，同时过滤噪声**。MARY通过**上下文相似性**解决：仅当少数模型提取的实体与多数模型提取的实体在上下文中语义相似时，才将其纳入最终标注。

### 关键技术细节：MARY框架
MARY由三个训练阶段组成，以RoBERTa-base为骨干编码器\(G\)，加上序列标注头\(F\)：

1. **领域自适应预训练（Domain-Adaptive Pre-training, DAPT）**  
   - 在目标无标注临床语料\(D\)上执行掩码语言模型（MLM）预训练，使编码器能捕捉临床实体间的上下文相似性。

2. **加权对比学习（Weighted Contrastive Learning）**  
   - 对每个实体类型\(c\)，使用所有3个模型都提取的实体（\(E_3^c\)）计算类中心\(\mu_c\)。  
   - 对每个实体\(e_n\)，其权重为其模型同意数\(w_n\)（=1,2,3）。**加权对比损失**将实体拉向其对应类中心，拉动力与\(w_n\)成正比。  
     \[
     \mathcal{L}_{ct} = -\frac{1}{N}\sum_{n=1}^N w_n \log \frac{\exp(\text{sim}(\mathbf{e}_n, \mu_{c_n}))}{\sum_{c=1}^C \exp(\text{sim}(\mathbf{e}_n, \mu_c))}
     \]
   - 同时用交叉熵损失\(\mathcal{L}_{ce}\)训练序列标注头，基于LLM标注解析的BIO序列。总损失\(\mathcal{L} = \mathcal{L}_{ct} + \mathcal{L}_{ce}\)。

3. **自训练（Self-Training）**  
   - 在对比学习后，模型可能保守。通过用当前模型预测的伪标签\(\tilde{y}=L(d)\)再微调模型（\(\mathcal{L}_{st}\)），迭代5轮，进一步扩大实体覆盖。

### 算法流程（文字说明）
1. 使用3个LLM（Med42-8B, UniNER-7B-type, Llama-3.3-70B）对每个临床样本进行零样本标注，解析为BIO序列。
2. 在无标注语料上对RoBERTa-base进行MLM预训练。
3. 用加权对比损失和交叉熵损失联合训练标签模型\(L\)。
4. 迭代5轮自训练，每次用\(L\)的预测作为伪标签重新训练，最终输出聚合后的标注结果。

## 3. 实验设计

### 数据集与场景
- **i2b2 2010**：问题、治疗、检测三类实体。
- **i2b2 2014**：受保护健康信息（PHI，合并为单一类别）。
- **n2c2 2018**：药物不良反应（ADE）相关实体。
- 每个数据集采用训练集进行零样本标注，测试集评估最终NER性能。

### Benchmark与对比方法
- **单模型基线**：Med42-8B、UniNER-7B-type、Llama-3.3-70B的零样本性能。
- **零样本精炼方法**（与MARY兼容）：
  - Self-consistency（多轮采样过滤）
  - Self-verification（模型自验证）
  - Conflict resolution（多轮冲突解决，最高性能）
- **标签模型基线**：
  - 多数投票（MV）在不同阈值\(T=1,2,3\)
  - 隐马尔可夫模型（HMM）
  - 条件隐马尔可夫模型（CHMM）
- **下游微调对比**：
  - 主动学习（AL）基线（Zero-shot+AL, Few-shot+AL）
  - LLM-FT+FT（先微调LLM再微调NER模型）
  - MARY+AL（本文方法）

## 4. 资源与算力

- **GPU**：2 × NVIDIA A100（80GB）。
- **LLM推理**：Llama-3.3-70B使用4位量化。
- **训练时间**：文中给出各模型在三个数据集上的每批推理时间及总推理时长（例如i2b2 2010上Llama-70B总耗时4.46小时，Med42-8B 0.23小时）。训练MARY的具体时间未明确给出，但使用固定超参数和5轮自训练，整体开销合理。
- 注意：**算力信息已明确**。

## 5. 实验数量与充分性

### 实验数量
- **主要结果表（Table 1）**：在3个数据集上，覆盖3种零样本精炼方法（vanilla, self-consistency, self-verification, conflict resolution），每种对比单模型、MV(T=1/2/3)、HMM、CHMM、MARY，共约3×4×7=84个F1值。
- **消融实验**（Appendix B）：评估DAPT、加权对比学习、自训练各组件的贡献，共8种配置，在3个数据集上报告F1。
- **模型多样性分析**（Appendix A）：比较不同模型组合（架构多样、规模多样、领域专用）。
- **下游微调实验**：在3个数据集上，比较4种方法（Zero-shot+AL, Few-shot+AL, LLM-FT+FT, MARY+AL），每个方法5个AL迭代，绘制学习曲线。
- **少数模型实体分析**（Figure 4）：按\(w_n\)分层评估MARY的二分类性能（精度/召回）。
- **此外**：还有Venn图分析、精度-召回权衡图、HMM/CHMM敏感性分析等。

### 实验充分性与公平性
- **充分性**：实验覆盖了零样本标注、标签模型聚合、下游微调三大场景；消融实验验证各组件；模型多样性试验；分层分析。实验设计较为全面。
- **公平性**：所有基线使用相同零样本方法（如冲突解决）时公平对比；MARY使用固定超参数（无开发集调优），与标签模型基线（HMM/CHMM也使用默认参数）公平；实验结果基于三个随机种子平均，增加可靠性。
- **潜在偏差**：对于HMM和CHMM，原文承认其设计对噪声敏感，而LLM标注噪声大，导致其性能不佳——这不一定是模型本身缺陷，而是应用场景不匹配。但文章对此进行了客观分析。

## 6. 主要结论与发现

1. **多LLM聚合显著优于单模型**：MARY在平均F1上比最强单模型（Llama-3.3-70B）提升+5.9（vanilla）至+8.6（冲突解决）。
2. **MARY超越所有标签模型基线**：在几乎全部设置中MARY取得最高F1，而MV、HMM、CHMM性能不稳定。
3. **MARY有效利用少数模型实体**：在\(w_n=1\)的实体中，MARY以高精度识别真阳性（Figure 4），实现比MV(T=2)更高的召回率，同时保持可比精度。
4. **MARY兼容多种零样本精炼方法**：与冲突解决组合效果最佳。
5. **下游微调大幅减少人工标注**：MARY+AL在100个标注样本下达到仅由AL需要2.6-3.4倍样本才能匹敌的效果，证明其有效降低标注成本。

## 7. 优点

- **方法创新性**：利用**上下文相似性**选择性整合少数模型提取的实体，而非简单投票或统一阈值，解决了多LLM聚合中噪声与真阳性共存的核心难题。
- **框架通用性**：MARY不依赖特定LLM或精炼方法，可灵活适配不同模型组合和零样本策略。
- **实验设计全面**：覆盖多个临床NER数据集、多种基线、多角度分析（消融、模型多样性、下游用例），结果可复现。
- **实用性**：显著降低人工标注成本，对无标注临床语料场景具有实际应用价值。

## 8. 不足与局限

- **模型组合固定**：主要实验使用3个特定LLM（Med42-8B, UniNER-7B-type, Llama-70B），虽然附录部分探索了其他组合，但未系统研究最优选择策略或更多模型联合的扩展规律。
- **零样本设置下超参数固定**：由于缺少验证集，MARY使用固定超参数，可能不是最优；未来可探索无监督超参数优化。
- **计算开销**：多LLM推理相比单模型成本增加（但通过混合大小模型可缓解）。
- **边界错误**：部分实体（如日期“04/03/83”被提取为“04”）存在部分匹配问题，影响严格F1；虽下游微调可纠正，但零样本评估中仍存在。
- **未探索与数据增强的协同**：零样本标注与合成数据生成是正交方向，未来可结合。

（完）
