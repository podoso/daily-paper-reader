---
title: A Multilingual Dataset and Empirical Validation for the Mutual Reinforcement Effect in Information Extraction
title_zh: 多语言数据集及其对信息抽取中相互增强效应的实证验证
authors: "Chengguang Gan, Sunbowen Lee, Qingyu Yin, Yunhao Liang, Xinyang He, Hanjun Wei, Younghun Lim, Shijian Wang, Hexiang Huang, Qinghao Zhang, Shiwen Ni, Tatsunori Mori"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.88.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 信息抽取数据集与相互增强效应
tldr: 信息抽取中的相互增强效应（MRE）此前仅在日语中验证。本文构建多语言MRE数据集MMM，包含英语、日语和中文共21个子数据集，并提出LLM辅助的数据集翻译对齐框架。实验验证了MRE在多语言设置下的普适性，为联合建模提供了资源支持。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 737, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 185, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1484, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1273, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1597, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1586, \"height\": 801, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 806, \"height\": 896, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.88/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1549, \"height\": 790, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1407, \"height\": 2302, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 995, \"height\": 651, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 993, \"height\": 307, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 693, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 694, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 694, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1372, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.88/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1505, \"height\": 818, \"label\": \"Table\"}]"
motivation: 信息抽取中任务间相互增强效应的跨语言普适性缺乏验证和数据支持。
method: 构建多语言MRE数据集MMM，并设计LLM辅助的翻译对齐框架以降低标注成本。
result: 在英、日、中三种语言上验证了MRE的存在且任务间相互增益。
conclusion: 信息抽取中任务间的相互增强效应具有跨语言普适性。
---

## Abstract
The Mutual Reinforcement Effect (MRE) describes a phenomenon in information extraction where word-level and sentence-level tasks can mutually improve each other when jointly modeled. While prior work has reported MRE in Japanese, its generality across languages and task settings has not been empirically validated, largely due to the lack of multilingual MRE datasets. To address this limitation, we introduce the Multilingual MRE Mix dataset (MMM), which consists of 21 sub-datasets covering English, Japanese, and Chinese. We propose an LLM-assisted dataset translation and alignment framework that significantly reduces manual annotation effort while preserving the structural requirements of MRE tasks. Building on MMM, we adopt a unified input-output framework to train an open-domain information extraction model and conduct extensive empirical studies, including full fine-tuning ablations and the construction of knowledgeable verbalizers based on MRE-mix data. Experimental results show that 76 percent of the MMM sub-datasets consistently exhibit the Mutual Reinforcement Effect across languages. These findings provide systematic empirical validation of MRE in multilingual settings and demonstrate its practical value for information extraction.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：信息抽取（IE）中的“相互增强效应”（Mutual Reinforcement Effect, MRE）——即词级任务（如命名实体识别）与句级任务（如文本分类）在联合建模时能相互提升——此前仅在日语数据上得到验证，其跨语言普遍性缺乏实证支持。关键障碍在于缺少多语言MRE数据集。
- **研究动机**：验证MRE是否是语言特定的现象，还是IE任务中更一般的性质。通过构建多语言数据集并进行系统实证，为联合建模提供资源基础，并探索其在实际IE中的应用价值。
- **整体含义**：该工作首次大规模跨语言（英、日、中）验证了MRE的存在，证明了词级与句级信息之间的双向依赖关系，为设计更高效的多任务IE模型提供了理论依据和资源支撑。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出“Multilingual Mutual Reinforcement Effect Mix (MMM)”数据集，覆盖英、日、中三种语言共21个子数据集。采用LLM辅助的数据集翻译与对齐框架，在保持MRE任务结构要求的前提下大幅降低人工标注成本。基于MMM训练一个统一输入输出的开源信息抽取大语言模型（OIELLM），并通过消融实验和知识性言语器构造验证MRE。
- **关键技术细节**：
  - **数据集格式**：每条样本包含输入（文本+任务指令词，如`/NER`）和输出（文本级标签 + 词级标签-实体对，使用`:`和`;`分隔）。
  - **翻译框架**：先对日语MRE数据集进行规则匹配翻译标签（确定性翻译），然后将被翻译标签与原始文本和实体跨度整合，提供给GPT-3.5-Turbo进行自由文本翻译，使用指令提示和一次示例学习。输出经过两轮规则过滤（去除非翻译字符、对齐失败样本），再由十名多语言研究生进行人工校准。
  - **OIELLM设计**：基于LLaMA3-8B和LLaMA2-13B，采用统一输入输出格式，输入为文本+任务指令词（如`/NER`），输出为文本级标签+词级标签-实体对。全参数微调，BF16精度训练，FP16推理。
  - **知识性言语器（Knowledgeable Verbalizer, KV）实验**：从MRE混合数据中提取词级信息（WLI），取每个标签前100高频词作为特定标签的言语器，用于少样本文本分类（T5系列模型）。

## 3. 实验设计

- **数据集**：MMM数据集包含21个子数据集，每个语言7个：SCNM（句子分类+NER）、SCPOS: RW（情感分类+关联词）、SCPOS: Adj&N、SCPOS: Adj、SCPOS: N、TCREE（文本分类+关系/事件抽取）、TCONER（开放域文本分类+NER）。数据集来源包括日语原有MRE数据集翻译和新增的TCONER（基于Universal-NER/Pile-NER-type构建）。
- **基准对比**：
  - 基线模型：USA-7B（原日语MRE模型）、GIELLM-13B-jp（日语通用IE模型）、GPT-3.5-Turbo、GPT-4o-mini、GPT-4o（在一次性指令+上下文学习设置下测试，但均因格式违反导致F1趋近于0）。
  - 主模型：OIELLM-8B（基于LLaMA3-8B-Instruct和Base）、OIELLM-13B（基于LLaMA2-13B）。
- **评价指标**：严格结构化预测下的F1分数，包括文本级F1（TL）、词级F1（WL）和两者同时正确的ALL F1。

## 4. 资源与算力

- **训练资源**：
  - 使用三张A800 80GB GPU和三张RTX 6000 Ada 48GB GPU。
  - 训练时间：12至20小时，取决于模型大小。
  - 训练精度：BF16（训练），FP16（推理）。
  - 学习率：1×10⁻⁵，训练3个epoch。
- **数据翻译资源**：使用GPT-3.5-Turbo进行翻译，但对比了GPT-4o（未显著减少人工修正成本，且部分数据集翻译保留率更低）。
- **人工修正**：十名多语言研究生参与人工校准。

## 5. 实验数量与充分性

- **实验数量**：
  - 主实验：在21个子数据集上训练OIELLM并报告F1，涵盖三个语言变体（表1）。
  - 消融实验：在所有21个子数据集上进行，对比是否提供词级信息（WLI）和文本级信息（TLI）对另一级任务的影响（表2）。
  - KV实验：在18个固定标签子数据集（排除TCONER）上进行，比较WLI-KV与原始KV（表3）。
- **充分性与公平性**：
  - 采用严格的结构化评价协议，确保公平比较。GPT系列模型因格式不符合而得分极低，但作者指出这反映的是格式遵循能力而非语义理解，分析合理。
  - 消融实验设计巧妙：直接向输入拼接另一级信息，输出仅要求预测本级，避免了额外指令或提示偏差。
  - KV实验进一步验证了MRE在文本分类下游任务中的迁移性。
  - 实验覆盖了三种语言、多个任务组合，消融76%显示正向增强，表明结论稳健。
  - 不足之处：TCONER表现较弱，归因于数据稀疏；部分SCPOS子数据集因标签相关性弱导致MRE不显著。但整体上实验设计系统、客观。

## 6. 主要结论与发现

- **MRE的跨语言普适性**：在21个子数据集上的消融实验中，76%的数据集表明一级信息增强另一级性能，验证了MRE在英、日、中三种语言中的存在。
- **OIELLM性能**：训练后的OIELLM在多数数据集上优于专门设计的日语模型GIELLM-13B-jp，说明多语言MRE监督能更有效地激活预训练知识。
- **知识性言语器增益**：基于WLI构造的KV在16/18个数据集上优于原始KV，尤其在情感分类中提升显著，说明MRE学到的词级信息可有效增强文本分类。
- **语言特性影响**：在字符型语言（中、日）中，MRE效果更明显。

## 7. 优点

- **数据集构建创新**：提出LLM辅助的翻译对齐框架，结合规则匹配、LLM翻译、人工校准，大幅降低人力成本，同时保持结构一致性；数据集规模大（21个子数据集），覆盖多任务组合。
- **验证方法严谨**：设计了消融实验直接测试信息级之间的互惠性，避免多任务优化中的混杂因素；采用严格的评价协议（ALL F1）确保输出可用性。
- **多角度验证**：不仅在本任务（IE）内验证，还通过KV实验验证MRE向其他任务（文本分类）的迁移。
- **实用价值**：构建的OIELLM模型和MMM数据集可直接用于多语言IE研究，开源模型可复现。
- **分析细致**：指出GPT系列模型在结构化输出上的不足，以及翻译模型选择（GPT-3.5 vs GPT-4o）的实证对比。

## 8. 不足与局限

- **模型覆盖有限**：主要基于LLaMA系列（8B/13B），未尝试更大参数模型或更先进的架构；翻译模型仅对比了GPT-3.5和GPT-4o，未测试其他LLM。
- **翻译框架非全自动**：当前框架仍需人工校准（约10%样本需修正），自动翻译质量指标未报告，仅提供了样本保留率作为间接度量。
- **开放域任务表现弱**：TCONER数据集由于数据稀疏和标签多样性，性能明显低于其他任务；MRE在开放域场景下的有效性有待进一步验证。
- **语言范围有限**：仅涵盖英、日、中三种语言，未涉及其他语系（如印欧语系、闪米特语系等），MRE的普适性还需更多语言验证。
- **任务组合局限**：仅研究了文本分类与NER、情感分类与词性、文本分类与关系/事件抽取等特定组合，其他可能的组合（如篇章级任务与词级任务）未探索。
- **未探讨负面迁移**：少数数据集（如TCONER英文）未显示出MRE，甚至出现负向影响，论文未深入分析其原因或提出自动筛选有益任务组合的方法。
- **算力成本较高**：全参数微调13B模型需要6块高端GPU，训练时间较长，对小规模团队可能资源门槛高。

（完）
