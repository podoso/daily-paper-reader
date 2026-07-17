---
title: Comparing Human and Large Language Model Interpretation of Implicit Information
title_zh: 比较人类与大语言模型对隐式信息的理解
authors: "Antonio De Santis, Tommaso Bonetti, Andrea Tocchetti, Marco Brambilla"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1111.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 使用大语言模型从隐式信息构建知识图谱的抽取流程
tldr: 隐式含义理解在LLM中尚未充分研究。本文提出隐式信息抽取任务和基于LLM的流水线，从上下文句提取关系三元组、验证隐式推理和分析时序关系。人机对比实验表明，LLM提取的三元组与人类多数一致，但人类提出大量额外三元组，说明当前LLM覆盖不足。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 576, \"height\": 667, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 735, \"height\": 906, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 768, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 544, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 547, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 549, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 803, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 803, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1111/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 805, \"height\": 544, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 459, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 814, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1252, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1687, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1299, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1207, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1311, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1659, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1235, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1111/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1176, \"height\": 172, \"label\": \"Table\"}]"
motivation: LLM在隐式信息理解上的能力尚未被系统评估。
method: 提出隐式信息抽取任务和LLM流水线，提取关系三元组并验证推理。
result: 人类与LLM三元组一致但人类补充更多，表明LLM覆盖有限。
conclusion: 揭示了LLM在隐式信息抽取中的保守性和覆盖不足。
---

## Abstract
The interpretation of implicit meanings is an integral aspect of human communication. However, this framework may not transfer to interactions with Large Language Models (LLMs). To investigate this, we introduce the task of Implicit Information Extraction (IIE) and propose an LLM-based IIE pipeline that builds a structured knowledge graph from a context sentence by extracting relational triplets, validating implicit inferences, and analyzing temporal relations. We evaluate two LLMs against crowdsourced human judgments on two datasets. We find that humans agree with most model triplets yet consistently propose many additions, indicating limited coverage in current LLM-based IIE. Moreover, in our experiments, models appear to be more conservative about implicit inferences than humans in socially rich contexts, whereas humans become more conservative in shorter, fact-oriented contexts. Our code is available at https://github.com/Antonio-Dee/IIE_from_LLM.

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 核心问题与整体含义
- **研究动机**: 人类交流依赖隐式含义（implicit meaning），即文本字面之外可推断的信息。而大语言模型（LLM）的文本生成能力日益强大，但人类与LLM的沟通框架可能不同，LLM是否也能像人类一样推断隐式信息尚不清楚。
- **核心问题**: 人类与LLM在理解隐式信息方面存在哪些差异？LLM能否有效抽取隐式信息并构建结构化知识？
- **整体含义**: 揭示LLM在隐式信息理解上的能力边界，为更可靠的人机交互提供参考。

## 2. 方法论：核心思想与关键技术细节
- **核心思想**: 提出隐式信息抽取（Implicit Information Extraction, IIE）任务，设计一个基于LLM的自动流水线，从上下文句子中构建双层知识图谱（关系层 → 时序层），并与人类判断进行对比。
- **三阶段流水线**:
  1. **信息抽取**:
     - 抽取实体（使用Balali等人的本体类型标注）。
     - 抽取显式三元组（Subject, Relation, Object），类似开放信息抽取（OIE）。
     - 抽取隐式三元组，推理类型借鉴ATOMIC（前提/后置条件、意图、情感反应、属性等），支持嵌套三元组处理从属关系和体貌。
  2. **推理验证**:
     - 对每个隐式三元组，由同一LLM自我挑战（判断是否可合理推断），若否，则给出解释并尝试纠正（最多三次循环）。
     - 去除与显式三元组重复的三元组。
     - 对保留的隐式三元组，要求LLM提供其推理前提（显式三元组）。
  3. **时序分析**:
     - 对每个三元组判断是事件（event）还是状态（state），并抽取绝对时间参考。
     - 对所有三元组进行两两时序关系判断（before/after/while/none），并交叉验证一致性。
- **关键技术**: 使用few-shot prompting，无需微调或访问模型参数；采用RDF reification思路处理嵌套；无监督，模型黑盒兼容。

## 3. 实验设计
- **数据集**: 
  - SocialIQA（社交常识推理，15句）
  - COPA（因果关系选择，15句）
- **任务场景**: 人工评估对比（Mistral Large 2 vs GPT-4o mini）
- **Benchmark**: 无现有IIE基准，本文首次提出。对比对象为人类标注（206名大学生+101名MTurk工人，经筛选后保留205+75人）。
- **对比方法**: 两个LLM互相对比，并与人类共识对比。额外在附录中引入NLI（DeBERTa-large-MNLI）作为外部验证探针（但不作为主要对比）。

## 4. 资源与算力
- **未明确说明**: 论文未提及GPU型号、数量、训练时长、推理开销等具体算力信息。由于采用API调用（黑盒LLM），未进行微调，计算开销主要集中在推理成本，但数值未给出。

## 5. 实验数量与充分性
- **总体实验组数**:
  - 两个数据集（各15句）× 两个LLM = 60个流水线运行。
  - 每个流水线输出若干三元组，经过多个评估环节（三元组分类、推理验证审查、事件/状态分类、时序比较、模型错误纠正），共生成多组对比数据。
  - 附录中额外进行了NLI探针实验（覆盖所有三元组）。
- **是否充分**:
  - **优点**: 涉及两个不同领域的数据集、两个主流LLM、多维度评估（分类、验证、时序），并收集了大量人类标注。
  - **不足**: 示例数量偏少（仅30句），可能不足以全面反映模型行为；人群差异（SocialIQA用大学生，COPA用MTurk）对结果的可能影响未严格控制；未进行消融实验或超参数分析；仅两种模型，推广性存疑。
  - **客观公平性**: 使用相同prompt模板，采用few-shot而非微调，但模型输出受提示敏感；人类标注经过注意力检查过滤，可靠性较高。

## 6. 主要结论与发现
- **总体一致性**: 模型-人类一致率（MHA）中等，Mistral在多数子任务上优于GPT；最高一致率出现在模型错误纠正和事件/状态分类，最低在时序比较。
- **覆盖缺口**: 人类总是提出大量模型未生成的三元组（尤其是前提、后置条件、属性），表明LLM覆盖不足。
- **严格性差异**:
  - 在社交丰富语境（SocialIQA）下，LLM（尤其是GPT）对隐式推理更保守，人类更宽松；在事实导向短句（COPA）下，人类变得更保守，模型差异缩小。
  - 模型自我验证环节会过度剔除一些人类认为合理的三元组。
- **时序分析**: LLM在事件/状态分类上表现良好，但在时序关系判断上一致性低，模型常倾向选择“无明确关系”，而人类更倾向于推断隐含时序。
- **人类共识**: 除推理验证和时序比较外，多数环节人类一致率较高，说明任务在主观性轮廓内仍有可靠信号。

## 7. 优点
- **任务新颖性**: 首次系统定义并操作化“隐式信息抽取”任务，填补了OIE与NLI之间的空白。
- **流水线设计**: 模型无关、黑盒兼容、无需微调，可应用于任意LLM；双重知识图谱（关系+时序）结构清晰，便于对比。
- **评估全面**: 融合直接对比和同意度打分，覆盖抽取、验证、时序多个维度；同时引入外部NLI探针作为补充分析。
- **数据集选择**: 兼顾社交推理（SocialIQA）和因果推理（COPA），体现语境差异。
- **人类标注质量**: 采用注意力检查、多人投票、过滤不合格回答，确保可靠性。

## 8. 不足与局限
- **样本量小**: 仅30句文本，可能导致统计显著性不足或遗漏模式。
- **人群偏差**: SocialIQA与COPA的标注人群不同（大学生 vs MTurk），可能混淆数据集效应与人群效应。
- **标注主观性**: 隐式含义本身具有解释可变性，尽管采用多数投票，仍难完全消除歧义。
- **缺乏消融**: 未验证流水线各阶段（例如推理验证、时序过滤）的独立贡献。
- **模型覆盖有限**: 仅测试两个模型（Mistral Large 2, GPT-4o mini），且未探索不同大小、架构或微调方式的影响。
- **时序分析瓶颈**: 低一致性表明流水线在此模块设计或prompt需改进。
- **伦理考量**: 虽提及透明性，但未深入讨论LLM盲从隐式含义（如把假想当事实）的风险。

（完）
