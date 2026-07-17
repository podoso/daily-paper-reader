---
title: "NSF-SciFy: Mining the NSF Awards Database for Scientific Claims"
title_zh: NSF-SciFy：从NSF奖项数据库中挖掘科学声明
authors: "Delip Rao, Weiqiu You, Eric Wong, Chris Callison-Burch"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2118.pdf"
tags: ["query:ie"]
score: 7.0
evidence: 使用零样本提示联合抽取科学声明和调查提议
tldr: 科学声明验证数据集规模有限。本文构建NSF-SciFy，包含280万条科学声明，覆盖全学科。使用零样本提示从摘要中联合抽取声明和调查提议，并展示在下游任务中的实用性。该数据集和抽取方法为科学信息挖掘提供了重要资源。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2118/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1583, \"height\": 523, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1559, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 825, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 726, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 716, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 722, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1618, \"height\": 2123, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1613, \"height\": 2461, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2118/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1648, \"height\": 1296, \"label\": \"Table\"}]"
motivation: 现有科学声明数据集规模小且领域有限。
method: 利用零样本提示从NSF摘要中联合抽取科学声明和调查提议。
result: 构建了包含280万条声明的大规模数据集，验证了抽取方法的有效性。
conclusion: 大规模科学声明数据集可支持多项下游科学分析任务。
---

## Abstract
We introduce NSF-SciFy, a comprehensive dataset of scientific claims and investigation proposals extracted from National Science Foundation award abstracts. While previous scientific claim verification datasets have been limited in size and scope, NSF-SciFy represents a significant advance with 2.8 million claims from 400,000 abstracts spanning all science and mathematics disciplines. We present two focused subsets: NSF-SciFy-MatSci with 114,000 claims from materials science awards, and NSF-SciFy-20K with 135,000 claims across five NSF directorates. Using zero-shot prompting, we develop a scalable approach for joint extraction of scientific claims and investigation proposals. We demonstrate the dataset’s utility through three downstream tasks: non-technical abstract generation, claim extraction, and investigation proposal extraction. Fine-tuning language models on our dataset yields substantial improvements, with relative gains often exceeding 100%, particularly for claim and proposal extraction tasks. Our error analysis reveals that extracted claims exhibit high precision but lower recall, suggesting opportunities for further methodological refinement. NSF-SciFy enables new research directions in large-scale claim verification, scientific discovery tracking, and meta-scientific analysis.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：科学出版物以每年约4%的速度增长，17年翻一番。研究者、审稿人和公众难以区分虚假主张与有根据的主张（如LK-99超导、量子霸权等）。现有的科学声明验证数据集（如SciFACT、PubHEALTH、CLIMATE-FEVER）规模小（最多数千条）、领域局限（多集中于生物医学或特定主题），且数据来源单一（主要来自已发表论文或事实核查网站）。
- **核心问题**：缺乏大规模、跨学科的科学声明数据集，难以支持鲁棒的声明验证系统和对科学主张的早期追踪。
- **本文目标**：构建规模至少比现有数据集大一个数量级、覆盖全部基础科学的声明数据集，并探索新的数据源——基金申请摘要（grant abstracts），以捕获研究初始阶段的声明和调查意向。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用零样本提示（zero-shot prompting）从美国国家科学基金会（NSF）奖项摘要中联合抽取两类信息：
    - **科学声明（Claims）**：摘要中声称或假设为真的陈述。
    - **调查提议（Investigation Proposals）**：摘要中提出的前瞻性研究活动。
- **关键技术细节**：
    - **数据来源**：从NSF Awards数据库下载XML格式的全部奖项记录（1970-2024年，超过50万条），解析后得到412,155个可解析奖项。
    - **抽取模型**：使用Anthropic的Claude-3.5-Sonnet（20240620版），设置温度为0以保持一致性。提示设计为返回JSON格式，包含奖项ID、技术摘要、非技术摘要、声明列表、调查提议列表。
    - **联合抽取的优势**：单独抽取声明时，模型易将前瞻性调查提议误判为事实声明；联合抽取能保持声明与提议的区分。
    - **数据清洗**：移除技术/非技术摘要近重复（trigram Jaccard相似度>0.9）以及字符级10-gram相似度>0.6的条目，最终得到11,141个数据点用于微调。
    - **下游任务微调**：采用LoRA（rank=128, lora_alpha=64）对Mistral-7B-Instruct-v0.3和Qwen2.5-7B-Instruct进行参数高效微调，学习率1e-5，线性调度，更新query/key/value/output投影层及MLP门/上/下投影层，训练3个epoch，100步预热，batch size=2，梯度累积4步。

## 3. 实验设计

- **数据集/场景**：
    - **NSF-SciFy**：全量412K摘要，280万声明。
    - **NSF-SciFy-MatSci**：材料科学子集（16K摘要，114K声明），作为主要微调数据。
    - **NSF-SciFy-20K**：跨5个理事会（MPS, GEO, ENG, CSE, BIO）的20K摘要（135K声明），用于验证跨领域泛化。
- **Benchmark**：三个下游任务：
    1. **非技术摘要生成**：从技术摘要生成非技术摘要。
    2. **声明抽取**：从摘要中抽取科学声明。
    3. **调查提议抽取**：从摘要中抽取调查提议。
- **对比方法**：
    - 基础模型（未微调） vs. 微调模型（Mistral-7B和Qwen2.5-7B）。
    - 额外在NSF-SciFy-20K上仅对Mistral-7B进行微调评估（附录F）。
- **评估指标**：
    - 非技术摘要生成：BERTScore（P/R/F1）、ROUGE-1/2/L/Lsum。
    - 声明/提议抽取：自定义LLM评估指标（基于GPT-4o-mini的成对判断），计算Precision、Recall、F1。该指标经人工验证具有近完美相关性。
- **验证**：人工标注120个奖项（每个区域20个），使用GPT-4o辅助识别遗漏和错误，并与人类标注者验证一致性。

## 4. 资源与算力

- **训练硬件**：单块A100 GPU（未明确说明型号，推测40GB或80GB）。
- **训练时间**：每个epoch约1小时，共3个epoch（总时长约3小时）。
- **其他**：使用Claude-3.5 API进行零样本抽取（具体调用次数和成本未说明）。
- **说明**：文章未详细说明GPU数量、内存用量、API调用总成本等细节，但LoRA微调本身算力需求相对较低。

## 5. 实验数量与充分性

- **主要实验组数**：
    - 三个任务分别在NSF-SciFy-MatSci上对两种模型（Mistral、Qwen）进行微调对比（共6组实验，对应表2-4）。
    - 额外在NSF-SciFy-20K上对Mistral-7B微调并评估三个任务（附录F，表A5-A7）。
    - 错误分析：对120个奖项进行详细错误分类。
    - 数据集分析：包括声明类型分布、提议类型分布、技术/非技术摘要风格差异等。
- **充分性评价**：
    - 实验设计较为全面：覆盖三个不同任务，两种架构模型，两组不同数据集（材料科学子集和跨领域子集）。
    - 消融实验：对比了是否微调（基础模型 vs. 微调模型），清晰显示微调带来的增益。
    - 但不足：未包含更多基线模型（如其他7B/13B模型、不同零样本方法等），也未在更大模型上验证。作者在局限中承认了这一点。
    - 评估指标新颖但依赖LLM，尽管经过人工验证，仍存在一定偏差风险。
    - 总体上，实验设计公平、对比清晰，但算力限制导致基线数量较少。

## 6. 主要结论与发现

- **数据规模**：NSF-SciFy是迄今为止最大的科学声明数据集（280万声明），覆盖全部数学与科学领域。
- **声明类型**：最常见的声明类型是“能力/技术/方法应用”（32.8%）、“问题/知识缺口陈述”（21.0%）和“观察到的现象/性质”（18.9%）。
- **调查提议类型**：最多的是“理论分析与计算建模”（36.9%）、“实验技术与工具开发”（16.8%）和“学术培训与课程开发”（12.8%）。
- **零样本抽取质量**：声明抽取具有高精度但较低召回（F1中等），调查提议抽取相对更均衡。
- **微调效果**：
    - 声明抽取：Mistral微调后F1提升101.8%（0.7097），Qwen提升63.3%。
    - 调查提议抽取：Mistral微调后F1提升90.97%（0.7261），Qwen提升112.6%。
    - 非技术摘要生成：提升较小（BERTScore-F1仅提升0.36%），说明基础模型在该任务上已表现良好。
- **错误分析**：声明生成错误率2.6%，主要错误类型为“过度自信”（overconfidence）和“过度概化”（overgeneralization）。调查提议错误率2.4%，主要为“内容不匹配”和“过度具体化”。
- **应用价值**：数据集可支持大规模声明验证、科学发现追踪、元科学分析。

## 7. 优点

- **规模与覆盖**：比现有数据集（最多1.4万条）大两个数量级（280万），且覆盖全部学科，反映了美国科学界的研究图景。
- **新颖数据源**：首次使用基金申请摘要作为声明来源，提供了研究初始阶段的主张和意向，比论文发表更早。
- **可扩展方法**：零样本联合抽取方法无需人工标注即可大规模构建数据集，且通过微调可实现从大型模型到中小模型的迁移。
- **高质量**：NSF的专家评审机制为摘要内容提供了高质量保证。
- **多子集设计**：提供材料科学专注子集和跨领域子集，便于不同研究需求。
- **公开性**：代码、数据和模型均开放（Apache-2.0），促进社区研究。
- **详细分析**：提供了声明/提议的类型学分类、风格差异分析、错误分析，增强了数据集的可解释性。

## 8. 不足与局限

- **来源局限**：仅包含美国NSF资助的项目，未覆盖未获资助的提案、国际资助机构（如欧盟ERC）或其他国家科学基金。NSF虽占美国联邦基础研究的25%，但仍存在国家/地区偏差。
- **抽取方法局限**：零样本抽取的召回率较低，虽然数据量大可以部分弥补，但仍有大量声明可能被遗漏。误差分析中即使使用Claude也存在2.1%的误差，且包含行政元数据幻觉。
- **评估指标依赖LLM**：虽然人工验证了LLM判断的准确性，但GPT-4o-mini作为评估器仍可能引入偏差，尤其在不同学科声明判别上。
- **时间覆盖不完全**：早期奖项缺乏关联出版物，限制了纵向追踪声明演化的能力。
- **基线模型有限**：仅使用了两个7B参数量模型，未探索更大模型（如13B、70B）或不同架构（如LLaMA、Falcon等）的效果。
- **下游任务有限**：仅验证了三种任务，未涉及声明验证（verification）或事实检查等直接相关任务。
- **应用风险**：自动构建的数据集可能存在错误，若直接用于验证或决策需谨慎；数据集仅代表NSF视角，不反映未被资助的科学主张。

（完）
