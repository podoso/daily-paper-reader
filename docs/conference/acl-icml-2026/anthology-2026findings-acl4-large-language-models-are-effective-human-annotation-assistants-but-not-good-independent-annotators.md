---
title: "Large Language Models Are Effective Human Annotation Assistants, But Not Good Independent Annotators"
title_zh: 大语言模型是有效的人工标注助手，但不是好的独立标注者
authors: "Feng Gu, Zongxia Li, Carlos R. Colon, Benjamin Evans, Ishani Mondal, Jordan Lee Boyd-Graber"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.4.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 事件标注、事件共指消解和论元抽取
tldr: "该论文评估了事件共指消解和论元抽取在纯AI、AI辅助和纯人工三种模式下的工作流，发现AI在共指消解上召回率远超基线，但远不及专家；AI辅助模式下专家采用AI提取论元的比例为60%，提取时间减少25%。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1641, \"height\": 582, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1645, \"height\": 827, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 734, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 759, \"height\": 61, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1200, \"height\": 720, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1242, \"height\": 1850, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1236, \"height\": 1797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.4/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1222, \"height\": 2113, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.4/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.4/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 770, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.4/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 585, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.4/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.4/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1642, \"height\": 506, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.4/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 362, \"height\": 428, \"label\": \"Table\"}]"
motivation: 事件标注是理解社会趋势的关键，但专家昂贵且低效。
method: 设计包含事件共指消解和论元抽取的工作流，比较AI-only、AI辅助和人工模式。
result: AI辅助模式显著减少人工标注时间，但AI单独表现远不如专家。
conclusion: LLM适合作为标注助手而非独立标注员。
---

## Abstract
Event annotation is important for identifying, monitoring, and understanding sociological trends. Although expert annotators set the gold standard, they are expensive and inefficient. While state-of-the-art NLP models are an attractive alternative, they are often evaluated on standalone subtasks rather than entire workflows. Thus, we evaluate a holistic workflow that summarizes news with event coreference resolution and argument extraction in three modes: AI-only, AI assistance, and human only. Although AI’s recall is seven times higher than the tf-idf baseline at coreference resolution, it is far from replacing experts. However, experts adopt AI-extracted arguments 60% of the time, reducing extraction time by 25%. Our code and data are in https://github.com/Obertura777/gtd-data.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：事件标注（event annotation）是社会学趋势识别、监测和理解的关键，但专家标注成本高、效率低。尽管大语言模型（LLM）被广泛看好，但现有NLP研究通常评估孤立子任务（如事件抽取、共指消解），而非完整的标注工作流。论文希望回答：LLM能否替代或辅助真实场景中的专家标注？
- **背景**：真实事件数据集（如全球恐怖主义数据库GTD）需要跨文档共指消解（将多个报道归为同一事件）和变量编码（从文本中提取结构化论元）。现有自动化系统（如GDELT）规模大但质量差；专家标注准确但昂贵。LLM作为辅助工具能否在实际工作流中提升效率？

## 2. 方法论：核心思想、关键技术细节

### 核心思想
将完整的新闻事件标注工作流分解为两个子任务，分别评估LLM在“独立完成”和“辅助专家”两种模式下的表现：
- **事件集合整理（Event Set Curation）**：跨文档共指消解——将多个文档聚类为同一事件。
- **变量编码（Variable Coding）**：从事件描述中提取结构化论元（如国家、武器类型、伤亡数等）。

### 关键技术细节
- **事件集合整理方法**：
  - **LLM-CLS（成对分类）**：使用GPT-4o-mini判断两篇文档是否描述同一事件。可选预处理步骤SEG（用LLM将多事件摘要文档分割为单事件文本块）。
  - **EMBEDDING（嵌入相似度）**：计算文档向量的余弦相似度，阈值0.859（通过网格搜索在验证集上优化F1）。
  - **K-LLM MEANS**：结合K-Means聚类与LLM摘要迭代更新簇中心，每次迭代用LLM生成簇摘要作为新质心。
- **变量编码模式**：
  - 手动模式（Human only）：专家独立标注。
  - 混合模式（Hybrid）：专家可查看LLM预提取的变量值，接受或修改。
  - AI-only：LLM直接输出。
- **评估指标**：精确率、召回率、F1；标注时间；人类-LLM一致率（使用三种匹配方法：归一化匹配NM、BERT匹配BEM、PEDANTS）。

## 3. 实验设计

### 数据集
- **全局恐怖主义数据库（GTD）**：真实、大规模、专家标注的开源事件数据库。
- 使用2022年2月的500篇文档作为事件集合整理测试集，人工创建371个事件集作为标准答案。
- 变量编码使用212个事件集，涵盖9个变量（国家、地点、目标、实施者、攻击类型、武器类型、具体武器、死亡数、受伤数）。

### 基准（Baseline）
- TF-IDF（现有系统的基线，用于文档相似度检索）。
- 其他对比方法：DistilBERT、ModernBERT、text-embedding-3-small、Gemini-embedding-001等嵌入方法。

### 对比的方法
- 事件集合整理：TF-IDF、EMBEDDING、LLM-CLS（有无SEG）、K-LLM MEANS（多种嵌入模型）。
- 变量编码：多个LLM模型（GPT-4o-mini、Claude Sonnet 4、Gemini 2.5 Pro/Flash、Llama 3.3 70B、Mixtral 8x7B等），以及人类在手动/混合模式下的表现。

## 4. 资源与算力

文中未明确提及使用的GPU型号、数量或训练时长。所有LLM通过API调用（如GPT-4o-mini），未进行微调。K-LLM MEANS的成本估算：生成2355个文本嵌入和5565次摘要共花费13.67美元。未提及本地训练资源。

## 5. 实验数量与充分性

- **事件集合整理**：对比了7种方法（TF-IDF, EMBEDDING, LLM-CLS +/- SEG, K-LLM MEANS三种嵌入），在500篇文档的基准上评估。
- **变量编码**：测试了8个LLM模型，三类事件集（人工、LLM、共识），两种标注条件（手动、混合），共9个变量。评估了人类-LLM一致率、标注时间、NA识别准确率。
- **总体评价**：实验覆盖了完整工作流，但仅使用GTD一个数据集，缺乏跨数据集的泛化验证。消融实验包括SEG预处理、不同嵌入阈值等。对比方法多样，但缺少与SOTA端到端系统（如ACLED、ICEWS）的直接比较。实验设计较为充分，但受限于单一领域（恐怖主义）。

## 6. 主要结论与发现

- **LLM不能替代专家事件共指消解**：最佳方法（LLM-CLS+SEG）的F1仅0.63，远低于专家水平；但EMBEDDING的精确率高达0.89，可辅助专家快速定位相似文档。
- **LLM作为辅助工具有效**：混合模式下专家采用LLM提取论元比例为60%，标注时间减少25%。
- **模型大小与准确率无强相关**：较大模型（如Gemini Pro）并不显著优于小模型（如GPT-4o-mini）。
- **LLM在NA（信息缺失）识别上表现差**：多数模型对缺失变量产生幻觉（幻觉率约50-75%），Mixtral 8x7B甚至几乎从不输出NA。
- **人类-LLM一致率与人类间一致率无显著差异**：说明LLM提供的变量值具有“近人类水平”的实用性。

## 7. 优点

- **真实场景工作流评估**：不局限于独立子任务，而是模拟完整事件标注流程，更贴近现实需求。
- **详尽的错误分析与缓解策略**：识别了指令模糊、文档歧义、时间冲突、主观判断等错误类型，并给出了提示优化方法。
- **实用性导向**：不仅关注准确率，还测量标注时间节省和人类接受率，直接体现LLM作为助手的价值。
- **多模型对比**：涵盖开源/闭源、不同规模模型，且进行了成本-效率分析。

## 8. 不足与局限

- **单一数据集**：仅使用GTD（恐怖主义事件），可能无法泛化到其他领域（如金融、医疗）。
- **未测试跨文档变量编码**：仅对单事件文档进行论元提取，未考虑跨文档整合（该步骤在实际中也很关键）。
- **未进行微调**：所有LLM为零样本，未尝试领域微调或提示优化，可能低估了LLM潜力。
- **计算成本未充分讨论**：成对分类复杂度为O(n²)，限制了大规模文档集的直接应用（虽K-LLM MEANS缓解了部分问题）。
- **人工评估者偏差**：混合模式中可能存在的“自动化偏差”未做深入控制（仅提及但不排除影响）。

（完）
