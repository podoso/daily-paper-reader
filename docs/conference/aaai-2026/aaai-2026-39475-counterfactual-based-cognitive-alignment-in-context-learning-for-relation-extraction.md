---
title: Counterfactual-based Cognitive Alignment In-Context Learning for Relation Extraction
title_zh: 基于反事实认知对齐的上下文学习关系抽取
authors: "Qibin Li, Shengyuan Bai, Nai Zhou, Nianmin Yao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39475/43436"
tags: ["query:ie"]
score: 9.0
evidence: 关系抽取上下文学习认知对齐
tldr: 针对大模型上下文学习在关系抽取中示例选择与认知机制不匹配的问题，提出反事实认知对齐框架，通过认知启发的反事实生成优化示例选择，提升关系抽取性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有上下文学习关系抽取中示例选择与认知机制不匹配。
method: 提出反事实认知对齐框架，利用反事实生成对齐人类关系推理认知原理。
result: 在多个关系抽取数据集上取得改进。
conclusion: 将认知科学原理融入示例选择，提升了关系抽取效果。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable In-Context learning (ICL) capabilities for relation extraction (RE). While ICL has shown promise in RE tasks, current approaches face challenges in example selection and utilization. These challenges stem from the misalignment between example selection methods and LLMs' inherent cognitive processing mechanisms, particularly in pattern recognition and relational reasoning. To address these limitations, we propose Counterfactual Cognitive Alignment (CCA), a novel framework that systematically enhances ICL performance in RE by aligning example selection with cognitive principles underlying human relational reasoning. The framework incorporates a cognitive-inspired counterfactual generation mechanism that creates semantically diverse yet relationally coherent examples, mirroring human "what-if" reasoning processes. Additionally, it employs a cognitive alignment approach that integrates structural identification features with semantic understanding to better align with LLMs cognitive processing patterns. Extensive experiments across multiple RE benchmarks reveal the effectiveness of our cognitive alignment approach through the synergistic integration of counterfactual reasoning and cognitively-guided selection.

---

## 论文详细总结（自动生成）

# 基于反事实认知对齐的上下文学习关系抽取——详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLMs）在关系抽取任务中展现出强大的上下文学习能力，但现有示例选择方法存在严重不足——它们多基于表面语义相似度，忽略了LLMs内在的认知处理机制（尤其是模式识别和关系推理的双过程机制）。
- **核心问题**：示例选择方法与人类关系推理的认知过程不匹配，导致I CL性能瓶颈：一方面示例分布缺乏多样性与一致性，无法激活相关参数；另一方面示例选择未能同时兼顾语义理解与结构模式识别。
- **动机**：受到心理学中反事实推理（"what-if"思考）和双过程认知理论的启发，本文旨在通过认知对齐优化示例空间构建与选择，从而提升LLMs在关系抽取中的I CL性能。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出反事实认知对齐框架，通过模拟人类反事实推理创建语义多样且关系一致的示例，并利用认知处理模式（长度、实体距离、实体对POS）与语义理解的联合表征进行示例选择，实现对LLMs关系推理认知机制的更好对齐。
- **关键技术细节**：
  - **反事实示例生成**：三种认知启发的生成策略：
    1. 概念替换（利用WordNet替换实体，保持关系不变）
    2. 上下文细化（借助DeepSeek-R1生成不同场景下的关系表达）
    3. 结构变化（使用带掩码的语言模型生成结构不同的同义表达，并通过融合原始和掩码表示的认知插值增强生成质量）
  - **认知处理模式提取**：对每个示例提取三个特征：示例长度、实体距离、实体对词性标签。将这些特征组合成描述性文本，再用语言模型编码为认知模式嵌入。
  - **认知对齐示例选择**：将示例的语义嵌入和认知模式嵌入通过池化与拼接形成全面的认知表征，然后基于余弦相似度从扩充的示例空间中选出与目标实例最相似的k个示例作为演示。
  
- **伪算法流程**：
  - 输入：原始示例空间E，目标实例x*
  - 通过三种反事实生成策略将E扩充为E'
  - 对E'中每个示例xi，提取认知模式I(xi)并编码得到Hi^I，同时对文本xi编码得到Hi^S
  - 拼接Hi^S和Hi^I的池化结果得到Hi^C
  - 计算x*的认知表征与每个Hi^C的余弦相似度，取Top-k作为演示集D
  - 将D和x*一起输入LLM进行关系预测

## 3. 实验设计

- **数据集**：三个标准关系抽取基准——SemEval（2010 Task 8）、TACRED、SciERC。采用少样本设置：每类关系5/10/20/50个标注示例。
- **基准对比方法**：
  - 三类backbone：随机选取、SimCSE检索、BERT+PURE+ICL（训练好的相似度检索器）
  - 五个baseline模型：R-BERT、KnowPrompt、Self-Refine、Self-Consistency、I²CL
  - 同时比较了"仅用语义理解"、"仅用认知模式"、"仅用反事实生成+认知模式"等消融变体
- **实验场景**：覆盖开源LLMs（LLaMA2-7B-chat、Qwen2.5-7B/72B-Instruct）和闭源LLMs（GPT-3.5、Claude-3.5-Sonnet），保证通用性。

## 4. 资源与算力

- **文中未明确说明**：未提及所使用的GPU型号、数量、训练时长等具体算力信息。论文强调无需模型微调或人工标注，但反事实生成环节调用了DeepSeek-R1和BERT等模型，实际算力消耗取决于这些模型的推理成本。整体框架属于基于检索的ICL，算力需求相对较小。

## 5. 实验数量与充分性

- **实验数量丰富**：
  - 主实验：3个数据集 × 4个shot设置 × 3个backbone × 3个开源LLM + 2个闭源LLM = 约200+组实验（部分省略）。
  - 与5个SOTA baseline的比较。
  - 消融实验：①三种反事实生成策略单独及组合的效果（6种变体）；②不同表征组件（仅语义、仅认知模式、反事实+认知模式等）的贡献。
  - 可视化分析：示例空间分布流形对比。
- **充分性与公平性**：实验设计较为全面，对比方法涵盖BERT-based和LLM-based主流方法，backbone选择典型，shot数量覆盖广泛，消融实验系统。但仍未在更多领域（如生物医学RE、跨语言RE）上验证，可能存在领域偏差。

## 6. 主要结论与发现

- CCA框架在所有数据集、所有shot设置、所有LLM上均一致优于对应baseline，平均F1提升约3.35%（以SimCSE和BERT+PURE+ICL为backbone时更明显）。
- 三种反事实生成策略各有贡献，其中结构变化的增益最大；组合使用效果最佳。
- 认知模式（长度/实体距离/POS）单独使用时优于随机，但弱于语义理解；两者联合后显著提升，证实双过程对齐的有效性。
- 流形可视化显示反事实生成使示例空间分布更均匀、语义连续、覆盖更平衡。
- 证明了将认知科学原理（反事实推理、双过程处理）融入ICL示例选择是一种有效且通用的增强策略。

## 7. 优点

- **创新性强**：首次将反事实推理和认知对齐引入ICL的示例选择，填补了认知科学与计算语言学的交叉空白。
- **方法模块化**：反事实生成、认知模式提取、认知对齐选择三个组件可独立替换或组合，便于后续改进。
- **无参高效**：无需微调LLM，仅通过改进输入示例即可提升性能，计算开销低。
- **通用性好**：在多个LLM（7B~72B、开源/闭源）、多种backbone上均有效。
- **实验设计严谨**：消融实验覆盖了方法每个设计选择，可视化分析进一步解释了性能提升原因。

## 8. 不足与局限

- **实验覆盖有限**：仅使用了三个英文RE数据集，未在中文、生物医学、金融等特定领域或更多复杂关系类型上验证。
- **认知模式的普适性**：长度、实体距离、POS这三种特征是否适用于所有RE场景？对于长文本、跨段落关系抽取可能需调整。
- **反事实生成依赖外部模型**：上下文细化依赖DeepSeek-R1，结构变化依赖BERT，生成质量受限于这些模型的能力，且可能产生噪声样本。
- **未讨论失败案例**：论文报告平均提升，但未分析哪些关系类型或示例选择中CCA仍会退化的情况。
- **计算成本未量化**：反事实生成阶段增加了额外的推理开销，但论文未给出具体时间或GPU资源消耗对比。
- **与更先进示例选择方法对比不足**：仅比较了SimCSE和BERT+PURE+ICL，未与最新的大模型专用检索器（如基于GPT的检索）对比。

（完）
