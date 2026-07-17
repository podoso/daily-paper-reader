---
title: "DiZiNER: Disagreement-guided Instruction Refinement via Simulating Pilot Annotation for Zero-shot Named Entity Recognition"
title_zh: DiZiNER：通过模拟预标注进行分歧引导的指令优化以实现零样本命名实体识别
authors: "Siun Kim, Hyung-Jin Yoon"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.795.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 命名实体识别方法
tldr: 零样本命名实体识别（NER）中，大语言模型输出存在系统性错误。受人类标注过程中通过预标注解决分歧的启发，本文提出DiZiNER框架，模拟预标注过程，利用大语言模型迭代优化指令。在多个数据集上，DiZiNER显著提升了零样本NER的准确率，接近监督方法。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.795/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1609, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.795/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.795/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1478, \"height\": 1912, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.795/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1237, \"height\": 2337, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1552, \"height\": 964, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1664, \"height\": 749, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1660, \"height\": 1067, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1010, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 888, \"height\": 478, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1132, \"height\": 1067, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1271, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1185, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1271, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1114, \"height\": 1071, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1464, \"height\": 529, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.795/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1624, \"height\": 1408, \"label\": \"Table\"}]"
motivation: 大语言模型在零样本NER中错误频出，需改进指令质量。
method: 模拟人类预标注流程，利用多个LLM生成标注并检测不一致，据此优化指令。
result: 在多个NER基准上，DiZiNER显著优于现有零样本方法，接近监督基线。
conclusion: 分歧引导的指令优化能有效提升零样本NER性能。
---

## Abstract
Large language models (LLMs) have advanced information extraction (IE) by enabling zero-shot and few-shot named entity recognition (NER), yet their generative outputs still show persistent and systematic errors. Despite progress through instruction fine-tuning, zero-shot NER still lags far behind supervised systems. These recurring errors mirror inconsistencies observed in early-stage human annotation processes that resolve disagreements through pilot annotation. Motivated by this analogy, we introduce DiZiNER (Disagreement-guided Instruction Refinement via Pilot Annotation Simulation for Zero-shot Named Entity Recognition), a framework that simulates the pilot annotation process, employing LLMs to act as both annotators and supervisors. Multiple heterogeneous LLMs annotate shared texts, and a supervisor model analyzes inter-model disagreements to refine task instructions. Across 18 benchmarks, DiZiNER achieves zero-shot SOTA results on 14 datasets, improving prior bests by +8.0 F1 and reducing the zero-shot to supervised gap by over +11 points. It also consistently outperforms its supervisor, GPT-5 mini, indicating that improvements stem from disagreement-guided instruction refinement rather than model capacity. Pairwise agreement between models shows a strong correlation with NER performance, further supporting this finding.

---

## 论文详细总结（自动生成）

# 论文DiZiNER 结构化中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：大语言模型（LLM）在零样本命名实体识别（NER）中虽取得进展，但输出仍存在持续且系统性的错误（如难以遵循复杂指南、边界检测模糊、实体类型混淆），导致零样本NER性能远落后于监督学习方法。
- **动机**：这些错误模式与人类标注早期阶段通过“预标注（pilot annotation）”迭代解决标注者分歧的过程高度相似。受此启发，论文提出DiZiNER框架，模拟人类预标注流程，利用LLM同时扮演标注者和监督者，通过分歧引导的指令优化来提升零样本NER性能，且无需任何参数更新。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将多个异构开源LLM作为独立标注者，对同一组文档进行NER标注；然后一个监督LLM分析标注者之间的分歧，识别热点区域（hotspot spans）、分类分歧类型，并据此迭代优化任务指令（包括通用指令和模型特定指令）。通过多轮迭代（最多5轮）逐步减少模型间分歧，提升NER质量。
- **关键技术细节**：
  1. **独立交叉标注**：K个异构LLM（如mistral-small3.2:24b、phi4:14b等8个模型）独立对采样文档集进行NER，输出转换为BIO序列以进行token级比较。
  2. **分歧分析**：
     - 计算模型间严格span F1作为权重，通过加权多数投票得到共识标签。
     - 定义三类token级分歧指标：标签冲突（D_conf）、类型混淆（D_type）、边界不确定度（U_bnd），取最大值为分歧得分，排名前20%的token合并为热点span。
     - 生成文档化报告，包含热点统计、分歧类型分类（O→Ent、Ent→O、Ent→Ent、Span Error）及示例。
  3. **指令优化**（四阶段）：
     - 阶段1：分歧模式分析，提取可泛化的纠正原则（非个例修复）。
     - 阶段2：模型特定诊断，针对非精英模型（非前50%权重）的残余错误。
     - 阶段3：指令整合与冲突消解，依据最终任务目标（final task goal）解决矛盾。
     - 阶段4：层次化组织，通用规则在前，条件规则在后。
- **最终选择**：根据模型间平均pairwise F1与NER性能的强相关性（图2），选取排名前三的迭代-模型配置的平均F1作为最终结果。
- **无参数更新**：所有LLM仅通过提示推理，不进行微调。

## 3. 实验设计
- **数据集**：18个NER基准，涵盖：
  - 跨领域（CrossNER：AI、Literature、Music、Politics、Science）
  - 通用（CoNLL2003、ACE2005、OntoNotes、MultiNERD）
  - 生物医学（AnatEM、BC2GM、BC4CHEMD、BC5CDR、GENIA）
  - STEM（FabNER）
  - 社交/对话（BroadTwitter、MIT-Movie、MIT-Restaurant）
- **Benchmark**：零样本设置（不使用任何gold标签训练），测试集评估严格span微F1。
- **对比方法**：
  - 零样本基线：ChatGPT、GPT-4、InstructUIE、UniNER-7B/13B、GLiNER、GoLLIE、KnowCoder-7B、GNER、B2NER、IRRA、EvoPrompt、GPT-5 mini。
  - 监督基线：BERT-base、InstructUIE、UniNER、GLiNER、KnowCoder、GNER、B2NER等（使用gold标签训练的SFT模型）。
  - 集成基线：多数投票（MV）、Dawid-Skene（DS）、GLAD、MACE（静态聚合初始输出）。
- **消融实验**：
  - 标注者多样性（异构 vs 单一家族）、标注者数量（4/8/12/16）
  - 监督模型能力（不同GPT版本）
  - 最终任务目标是否存在
  - 是否移除最不一致的标注者
  - 迭代文档集大小（15/25/50/100）
  - 使用黄金标签代替分歧信号（DiZiNER with gold）

## 4. 资源与算力
- **未明确说明GPU型号和训练时长**：因方法无需微调，仅使用LLM推理和API调用。
- **成本**：
  - 每次迭代平均成本：推理$1.90，监督$0.77，总计$2.67/迭代。
  - 每个基准约5次迭代 × 3种参数配置 = 约15次迭代，总成本约$40.1/基准。
- **标注模型**：8个开源LLM（均≤24B参数），通过OpenRouter API调用。
- **监督模型**：GPT-5-mini-2025-08-07（OpenAI API），温度0.0等确定性解码。

## 5. 实验数量与充分性
- **实验数量**：非常丰富。
  - 主实验：18个数据集上的零样本结果（表1、2），对比了10+种基线。
  - 消融实验：7大类，覆盖多样性、规模、监督能力、目标、移除、集大小、黄金数据等（表9-16）。
  - 指令分析：指令类别分布（表17）、定性示例（表18）。
  - 相关性分析：图2（18个子图）展示F1与配对一致性的强相关。
  - 敏感性分析：5种种子、5种初始指令的稳定性测试。
- **充分性**：极高。实验设计系统，覆盖多领域、多模型、多配置，消融实验验证了各组件贡献，结果趋势清晰。对比方法涵盖主流零样本和监督方法，集成基线排除了“仅集成”的解释。但所有实验均在公开英文基准上进行，未涉及低资源语言或多语言零样本NER，存在覆盖偏差。

## 6. 论文的主要结论与发现
1. **零样本SOTA**：在18个基准中，DiZiNER在14个上达到零样本新SOTA，平均提升之前最佳结果+8.0 F1（表1、2）；将零样本与监督的差距从-32.0缩小到-20.9 F1。
2. **超越监督模型**：DiZiNER持续超越其监督模型GPT-5 mini（平均+5.0 F1），证明提升源于分歧引导的指令优化而非监督能力。
3. **协议与性能强相关**：模型间平均配对严格span F1与gold标准F1高度相关（Pearson ρ最高0.922），可作为无监督性能代理（图2）。
4. **标注者多样性关键**：异构小模型（≤24B）优于单一家族的更大模型（表14）；8个标注者最佳，过多（12个以上）引入噪声（表15）。
5. **最终任务目标不可或缺**：跳过该组件导致平均F1下降约5.7（表11）。
6. **迭代峰值**：多数任务在平均2.7次迭代达到最佳，但存在过修正风险（如MIT-Movie早期峰值后下降）。

## 7. 优点
- **创新性**：将人类标注中解决分歧的“预标注”流程引入LLM零样本NER，不同于以往基于ICL或自我改进的方法，利用多模型分歧作为监督信号。
- **无需微调**：完全基于提示，避免参数更新，可快速适配新LLM（即插即用）。
- **可解释性**：分歧分析提供了结构化报告（热点、分歧类型、模型偏差），使优化过程透明。
- **鲁棒性**：多个种子和初始指令下F1标准差低（0.8%-2.1%），参数配置影响有限。
- **经济性**：总成本仅约$40/基准，适合实际应用。
- **实验充分**：18个数据集、广泛消融、与多种集成方法的比较，证据链完整。

## 8. 不足与局限
- **性能方差**：不同基准增益差异大（如ACE05仅+2.1但OntoNotes达+24.8），且部分任务（如Science）未超越前最佳（-4.6 F1），可能存在过拟合采样偏差。
- **指令漂移风险**：由于不访问gold标签，仅依赖文档池和schema，优化出的指令可能逐渐偏离数据集实际标注规范（论文明确提及）。
- **固定schema**：迭代中不修改实体类型集（如合并、新增），与真实标注流程不符；论文建议未来需增加schema-refinement组件。
- **依赖API**：监督模型使用GPT-5 mini（私有API），存在复现性风险和成本波动。
- **多语言/低资源缺失**：全部为英文数据集，未评估跨语言零样本NER能力。
- **迭代次数固定**：统一使用最多5次迭代，但部分任务可能在更早或更晚达到最优，缺乏早停机制。
- **标注模型选择**：仅使用8个模型，且均为≤24B开源模型，未测试更大模型或不同架构（如Mistral Large、Llama 70B）作为标注者，多样性效应未充分探索。

（完）
