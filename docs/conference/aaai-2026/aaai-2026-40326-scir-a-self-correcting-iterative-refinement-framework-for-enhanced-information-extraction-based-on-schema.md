---
title: "SCIR: A Self-Correcting Iterative Refinement Framework for Enhanced Information Extraction Based on Schema"
title_zh: "SCIR: 基于模式的自校正迭代细化框架用于增强信息抽取"
authors: "Yushen Fang, Jianjun Li, Mingqian Ding, Chang Liu, Xinchi Zou, Wenqi Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40326/44287"
tags: ["query:ie"]
score: 9.0
evidence: 信息抽取研究论文
tldr: 当前基于大语言模型的信息抽取系统存在训练成本高、与模型偏好对齐困难等问题。本文提出自校正迭代细化框架SCIR，通过双路径自校正模块和反馈驱动优化，实现即插即用，显著降低训练成本。同时构建了包含10万条数据的多任务双语自校正数据集MBSC，验证了框架的有效性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有大语言模型驱动的信息抽取系统面临高训练成本和难以对齐模型偏好两大局限。
method: 提出双路径自校正模块和反馈驱动优化的SCIR框架，实现即插即用且低成本。
result: 在多个信息抽取任务上，SCIR框架在降低训练成本的同时保持了竞争性能。
conclusion: SCIR框架为LLM信息抽取提供了一种高效、可扩展的范式。
---

## Abstract
Although Large language Model (LLM)-powered  information extraction (IE) systems have shown impressive capabilities, current fine-tuning paradigms face two major limitations: high training costs and difficulties in aligning with LLM preferences. To address these issues, we propose a novel universal IE paradigm—the Self-Correcting Iterative Refinement (SCIR) framework—along with a Multi-task Bilingual (Chinese-English) Self-Correcting (MBSC) dataset containing over 100,000 entries. The SCIR framework achieves plug-and-play compatibility with existing LLMs and IE systems through its Dual-Path Self-Correcting module and feedback-driven optimization, thereby significantly reducing training costs. Concurrently, the MBSC dataset tackles the challenge of preference alignment by indirectly distilling GPT-4's capabilities into IE result detection models.	Experimental results demonstrate that SCIR outperforms state-of-the-art IE methods across three key tasks— named entity recognition, relation extraction, and event extraction—achieving a 5.27 percent average improvement in span-based Micro-F1 while reducing training costs by 87 percent compared to baseline approaches. These advancements not only enhance the flexibility and accuracy of IE systems but also pave the way for lightweight and efficient IE paradigms.

---

## 论文详细总结（自动生成）

# SCIR: 基于模式的自校正迭代细化框架用于增强信息抽取——详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：当前基于大语言模型（LLM）的信息抽取（IE）系统虽然性能强大，但主流的微调范式存在两大局限：一是训练成本高昂且模型灵活性差（难以快速适配新模型）；二是难以对齐LLM的偏好（人工标注的边缘错误无法通过数据量简单消除，缺乏动态反馈与自校正能力）。
- **整体含义**：本文提出一种全新的、无需微调提取模型的IE范式——SCIR框架，旨在实现即插即用、低成本、高性能的IE系统，同时解决模型偏好对齐问题，推动轻量高效IE的发展。

## 2. 论文提出的方法论

- **核心思想**：通过“双路径自校正模块”和“反馈驱动优化”构建迭代细化闭环，在不重新训练提取模型的前提下，利用轻量级检测器（基于Qwen3-4B）识别提取结果的冗余、遗漏和格式错误，并生成针对性提示引导LLM逐步改善输出。
- **关键技术细节**：
  - **信息提取模块**：支持三种配置（未训练LLM、域适应微调模型、现有IE框架），使用基础指令模板进行初始提取，后续迭代使用优化提示。
  - **结果剪枝模块**：基于Qwen3-4B分类器（在MBSC上训练），将提取结果分为正样本（直接输出）和负样本（送自校正模块），减少不必要迭代。
  - **双路径自校正模块**：并行运行冗余检测路径（识别冗余信息）和缺失检测路径（识别遗漏信息），同时收集格式错误。两个路径均为Qwen3-4B微调模型。
  - **反馈驱动优化**：基于检测结果生成冗余提示、缺失提示、格式错误提示，与基础提示融合形成复合提示，驱动LLM在下一次迭代中改进。
- **算法流程**（文字说明）：
  1. 初始化空答案集，基础提示。
  2. while 数据非空且迭代轮次≤K：
     - LLM根据当前提示生成提取结果。
     - 剪枝模型将结果分为正/负样本：正样本加入答案集并从数据集中移除；负样本送双路径自校正模块。
     - 冗余检测和缺失检测分别生成冗余集和缺失集。
     - 根据检测结果生成改进提示，与基础提示融合后进入下一轮。
  3. 达到最大迭代次数后，剩余负样本也加入答案集。

## 3. 实验设计

- **数据集与场景**：选用11个双语（中文/英文）基准数据集，覆盖三大任务：
  - 事件抽取（EE）：CCF Law、FewFC、RAMS、WikiEvents
  - 命名实体识别（NER）：Boson、Weibo、CrossNER
  - 关系抽取（RE）：COAE2016、SKE2020、Wiki-ZSL、FewRel
- **基准方法（Baseline）**：
  - 未调优LLM：LLama3.1-8B、Qwen3-8B、DeepSeek-R1-Distill-Qwen3-8B
  - 域特定模型：YAYI-UIE、IEPile-LLama2、ChunkUIE、OneKE
  - 主流IE框架：RUIE（仅英文）
- **SCIR变体**：SCIR-LLama3.1、SCIR-Qwen3、SCIR-DeepSeek-R1、SCIR-OneKE、SCIR-RUIE
- **评价指标**：span-based Micro-F1（零样本设置，测试集完全排除于训练数据）

## 4. 资源与算力

- **训练**：
  - 使用4块RTX4090 GPU，SCIR框架中双路径自校正模块（基于Qwen3-4B）在MBSC数据集上训练耗时约**3小时**。
  - 对比传统域特定模型训练需22小时，训练成本降低**87%**。
- **推理**：
  - 文中未给出绝对时间数值，但给出相对时间增加比例：EE增加13.72%，NER增加11.96%，RE增加14.32%，平均时间开销增加13.33%，同时性能提升平均44.86%。
- **迭代次数**：设为2（实验验证第一、二轮增益显著，后续饱和）。

## 5. 实验数量与充分性

- **实验组数**：
  - 在11个数据集上对比9种基线方法（含SCIR变体共约15种配置）。
  - 模块消融实验：比较完整双路径、仅冗余检测、仅缺失检测三种配置，共33组子实验（11数据集×3配置）。
  - 模型消融实验：比较未训练Qwen3-4B vs 训练后Qwen3-4B在11数据集上的表现。
  - 迭代轮次实验：展示了0-3轮平均F1曲线。
  - 剪枝有效性可视化：以SKE2020数据集展示迭代剪枝分布。
  - 时间成本分析：给出了不同任务平均时间开销比例。
- **充分性判断**：
  - 实验覆盖了三大核心IE任务、双语场景，对比了多种类型基线（未调优LLM、微调模型、现有框架），消融实验完整验证了各模块贡献。但未在更多大规模英文基线上（如GPT-4直接对比）进行验证；英文数据集上性能增益略低于中文，且RUIE框架本身已是强基线。总体实验设计较为充分、客观、公平。

## 6. 论文的主要结论与发现

- SCIR框架在零样本设置下，在中文和英文IE任务上均取得显著性能提升，平均F1提升5.27%（对比当前最优双语模型OneKE）。
- 双路径自校正机制是关键：冗余检测在EE任务上更有效，缺失检测在NER任务上更有效；两者互补增强。
- 剪枝模块能有效提前终止正确结果，避免错误传播，且随迭代进行剪枝准确率提升。
- 仅需少数迭代（2轮）即可达到稳定增益，继续迭代收益递减。
- 训练成本降低87%，推理时间仅增加约13%即可获得巨大性能提升。
- SCIR可即插即用，与不同提取器（LLM、域模型、现有框架）无缝集成。

## 7. 优点

- **方法创新**：提出无需微调提取模型的迭代自校正范式，打破了传统“静态标注→静态推理”的局限。
- **数据集创新**：构建MBSC数据集，通过GPT-4实际错误模式进行训练，实现模型偏好对齐。
- **即插即用**：支持灵活更换底层提取模型，且检测模块只需训练一次，极大降低迁移成本。
- **训练效率高**：仅需3小时训练时间，比传统方法降低87%成本。
- **可解释性**：双路径检测提供冗余、缺失、格式错误的具体信号，优化过程透明。

## 8. 不足与局限

- **英文数据集性能增益较小**：由于双路径自校正模块基于Qwen3-4B（中文语料更优），在英文任务上增益不如中文明显，可能依赖基模型语言能力。
- **迭代次数依赖经验设定**：超参数K设为2虽基于实验，但未在更大范围内探索或自适应终止。
- **未与GPT-4直接对比**：虽然使用GPT-4生成MBSC，但未在同等条件下与GPT-4直接作为提取器进行对比。
- **实验覆盖有限**：未涉及更多语言（如其他非中英文语种）或更细粒度任务（如嵌套实体、跨句关系）。
- **推理时间开销**：虽仅增加约13%，但未在超大吞吐场景下测试，可能对实时性要求高的应用仍有压力。

（完）
