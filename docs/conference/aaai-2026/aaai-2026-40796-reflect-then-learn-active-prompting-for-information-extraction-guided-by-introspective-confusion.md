---
title: "Reflect Then Learn: Active Prompting for Information Extraction Guided by Introspective Confusion"
title_zh: 先反思再学习：基于内省困惑引导的主动提示信息抽取
authors: "Dong Zhao, Yadong Wang, Xiang Chen, Chenxi Wang, Hongliang Dai, Chuanxing Geng, Shengzhong Zhang, Shao-Yuan Li, Sheng-Jun Huang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40796/44757"
tags: ["query:ie"]
score: 9.0
evidence: 面向信息抽取的主动提示方法
tldr: 针对LLM在少样本文本抽取中对示例敏感的问题，提出APIE框架，通过内省困惑的双重不确定性指标指导示例选择，显著提升IE任务性能。该方法不仅考虑语义困惑，还量化格式生成难度，实验证明其有效性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: LLM在少样本文本抽取中性能高度依赖上下文示例选择，现有方法忽略格式生成带来的困惑。
method: 提出APIE，基于内省困惑原则，结合语义和格式两个维度的不确定性指标主动选择最具信息量的示例。
result: 在多个IE基准上，APIE显著优于传统示例选择策略，提升了少样本场景下的抽取性能。
conclusion: 内省困惑能有效引导示例选择，为提升LLM在结构化抽取任务中的表现提供了新思路。
---

## Abstract
Large Language Models (LLMs) show remarkable potential for few-shot information extraction (IE), yet their performance is highly sensitive to the choice of in-context examples. Conventional selection strategies often fail to provide informative guidance, as they overlook a key source of model fallibility: confusion stemming not just from semantic content, but also from the generation of well-structured formats required by IE tasks. To address this, we introduce Active Prompting for Information Extraction (APIE), a novel active prompting framework guided by a principle we term introspective confusion. Our method empowers an LLM to assess its own confusion through a dual-component uncertainty metric that uniquely quantifies both Format Uncertainty (difficulty in generating correct syntax) and Content Uncertainty (inconsistency in extracted semantics). By ranking unlabeled data with this comprehensive score, our framework actively selects the most challenging and informative samples to serve as few-shot exemplars. Extensive experiments on four benchmarks show that our approach consistently outperforms strong baselines, yielding significant improvements in both extraction accuracy and robustness. Our work highlights the critical importance of a fine-grained, dual-level view of model uncertainty when it comes to building effective and reliable structured generation systems.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大型语言模型（LLM）在少样本信息抽取（IE）任务中性能高度依赖于上下文示例（in-context examples）的选择。传统的示例选择策略（如随机采样、基于语义相似度的KNN）往往无法提供信息量丰富的指导，因为它们忽略了一个关键的模型失败来源：困惑不仅来源于文本的语义内容，还来源于IE任务对输出格式（如结构化的JSON）的严格要求。
- **整体含义**：论文认为，对LLM在结构化生成中的困惑进行细粒度的、双重维度的量化（格式不确定性与内容不确定性），可以更有效地指导主动示例选择，从而提升少样本IE的准确性和鲁棒性。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：提出 **APIE**（Active Prompting for Information Extraction）框架，基于**内省困惑（Introspective Confusion）** 原则，让模型通过自我反思评估其自身的困惑，主动选择最具挑战性和信息量的样本作为少样本示例。
- **关键技术细节**：
  - **双层次内省不确定性度量**：
    - **格式级不确定性（Format-Level Uncertainty, \(U_f\)）**：量化模型生成符合语法的结构化输出的困难程度。分为两部分：
      - 解析失败率（\(R_{fail}\)）：输出不能被严格解析器解析的比例。
      - 结构分歧（Structural Disagreement）：成功解析的输出在结构组成上的差异度。
    - **内容级不确定性（Content-Level Uncertainty, \(U_c\)）**：评估模型在成功解析输出中提取的语义信息的一致性，使用平均Jaccard相似度的补数。
  - **基础信号：生成分歧（\(U_d\)）**：基于编辑距离的原始输出文本差异度，作为基线信号。
  - **统一不确定性分数**：对\(U_d\)、\(U_f\)、\(U_c\)进行归一化后加权求和得到\(U_{total}\)，用于对未标注池排序，选择top-n样本作为示例。
  - **主动提示构建**：将选中的示例与任务指令、格式约束一起构建结构化提示，引导模型生成符合模式的输出。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：四个广泛使用的IE基准，涵盖NER和RE任务：
  - ACE04（NER，7类）
  - CoNLL03（NER，4类）
  - CoNLL04（联合NER+RE，4实体类型，5关系类型）
  - SciERC（联合NER+RE，6实体类型，7关系类型）
- **基准（Benchmark）**：采用端到端设置，模型仅接收原始文本，直接生成目标结构。
- **对比方法**：
  - Zero-Shot (ZSL)
  - Random-Sample (RSL)
  - KD Sort（基于知识密度的课程策略）
  - Active-Prompt（基于输出分歧的不确定性引导基线）
- **评价指标**：micro F1-score，所有结果均为多次独立运行的平均值。

## 4. 资源与算力
- 论文**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。由于APIE是训练-free的框架，仅在推理阶段计算不确定性并进行示例选择，因此不需要大规模训练资源。文中使用的模型规模包括12B、14B、660B参数级别，但未提及推理硬件细节。

## 5. 实验数量与充分性
- **实验数量**：在4个数据集×4个LLM后台上进行主实验，共16组对比。此外还包括：
  - 消融实验（DeepSeek-R1-14B模型上，移除各不确定性分量和模式提示）
  - 鲁棒性分析（10次独立运行性能分布）
  - 可扩展性分析（不同规模模型）
  - 不确定性分布可视化（violin plots）
  - 案例研究（定性分析）
- **充分性与公平性**：
  - 覆盖了多种任务（NER、RE）和多种模型架构（不同系列、不同规模），对比了当前主流的四种基线方法。
  - 所有实验结果严格匹配协议（严格匹配），并报告了多次运行的平均值。
  - 消融实验系统地验证了每个组件的必要性。
  - 总体实验设计较为全面，能够支撑主要结论。但缺失对更多基线（如基于prompt工程的优化）及更多IE任务（如事件抽取）的覆盖，稍显不足。

## 6. 论文的主要结论与发现
- **APIE一致超越所有基线**：在几乎所有的数据集和模型上，APIE均取得最高F1分数，尤其在复杂联合抽取任务上增益显著（如SciERC上RE相对提升18.3%）。
- **鲁棒性更强**：相比随机采样，APIE在不同运行下性能方差更小，提示构建更稳定。
- **对小规模模型尤其有效**：在Gemma-3-4B等小型LLM上，API提升超过10个F1点，表明结构不确定性引导能弥补模型能力不足。
- **不确定性信号互补**：格式不确定性与内容不确定性捕获了模型困惑的不同维度，二者共同作用优于单独使用。
- **模式提示（pattern prompt）至关重要**：缺失模式提示会导致RE任务性能大幅下降，验证了结构约束在引导输出中的关键作用。

## 7. 优点
- **方法创新**：首次将LLM在IE任务中的困惑解耦为格式和内容两个正交维度，提出对应的不确定性度量，这是对传统仅考虑输出分歧的主动提示方法的显著改进。
- **无需额外训练**：APIE是完全训练-free的，仅通过LLM自身输出即可估计不确定性，具有很好的通用性和易用性。
- **实验全面且严谨**：在多个模型、多个数据集上进行了系统对比，并包含消融、鲁棒性、可扩展性分析，论证有力。
- **注意力聚焦于实际问题**：意识到LLM在结构化生成中的格式错误常被忽略，本工作针对性地解决，具有重要的实践价值。

## 8. 不足与局限
- **计算开销**：虽然训练-free，但需要进行多次推理（论文中k次生成）以估计不确定性，对于大规模模型（如660B）或大量未标注样本，可能产生较高的推理成本。
- **超参数依赖**：权重α、β、γ需要手动调节以适配不同任务，且未讨论自动调参方法。
- **标注依赖**：所选示例需要人工标注以获得真实标签（ground-truth labels），尽管标注量少，但仍有成本。
- **任务覆盖有限**：实验仅涵盖NER和RE，未包括事件抽取（EE）、关系映射等更复杂的IE任务；也未验证在更多语言或域外的泛化能力。
- **仅使用开源模型**：未实验闭源模型（如GPT-4），可能存在架构偏差；且所有模型均为同类型（Decoder-only LLM），未探索编码器-解码器结构。
- **不确定性计算假设**：假设模型多次生成独立抽取结果，但实际中存在同质化问题；且解析失败率可能受解析器严格程度影响，存在主观性。

（完）
