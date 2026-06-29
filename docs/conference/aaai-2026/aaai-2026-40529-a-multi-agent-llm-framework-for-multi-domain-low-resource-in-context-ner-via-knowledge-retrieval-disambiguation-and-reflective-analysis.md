---
title: "A Multi-Agent LLM Framework for Multi-Domain Low-Resource In-Context NER via Knowledge Retrieval, Disambiguation and Reflective Analysis"
title_zh: 基于知识检索、消歧和反思分析的多智能体大语言模型框架用于多领域低资源上下文命名实体识别
authors: "Wenxuan Mu, Jinzhong Ning, Di Zhao, Yijia Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40529/44490"
tags: ["query:ie"]
score: 9.0
evidence: 多智能体大语言模型框架用于低资源上下文命名实体识别
tldr: 针对现有上下文学习中NER在低资源场景下依赖动态检索且泛化不足的问题，提出KDR-Agent多智能体框架。该框架包含知识检索、消歧和反思分析三个智能体，协同工作以利用外部知识增强实体识别。实验表明，在多领域低资源NER任务上，KDR-Agent显著优于现有ICL方法，有效解决了领域外泛化问题。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40529/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1824, \"height\": 1239, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40529/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1810, \"height\": 370, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40529/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1845, \"height\": 862, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40529/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 886, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40529/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 882, \"height\": 521, \"label\": \"Table\"}]"
motivation: 现有上下文NER方法在低资源下依赖标注样例检索且领域泛化差。
method: 设计多智能体框架，集成知识检索、消歧和反思分析来增强上下文NER。
result: 在多领域低资源NER任务上取得最佳性能。
conclusion: 多智能体协作有效扩展了LLM在低资源NER中的能力边界。
---

## Abstract
In-context learning (ICL) with large language models (LLMs) has emerged as a promising paradigm for named entity recognition (NER) in low-resource scenarios. However, existing ICL-based NER methods suffer from three key limitations: (1) reliance on dynamic retrieval of annotated examples, which is problematic when annotated data is scarce; (2) limited generalization to unseen domains due to the LLM's insufficient internal domain knowledge; and (3) failure to incorporate external knowledge or resolve entity ambiguities. To address these challenges, we propose KDR-Agent, a novel multi-agent framework for multi-domain low-resource in-context NER that integrates Knowledge retrieval, Disambiguation, and Reflective analysis. KDR-Agent leverages natural-language type definitions and a static set of entity-level contrastive demonstrations to reduce dependency on large annotated corpora. A central planner coordinates specialized agents to (i) retrieve factual knowledge from Wikipedia for domain-specific mentions, (ii) resolve ambiguous entities via contextualized reasoning, and (iii) reflect on and correct model predictions through structured self-assessment. Experiments across ten datasets from five domains demonstrate that KDR-Agent significantly outperforms existing zero-shot and few-shot ICL baselines across multiple LLM backbones.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：命名实体识别（NER）是信息抽取的基础任务，传统方法依赖大规模标注数据和监督微调，在低资源或新领域场景下泛化能力差。近年来，基于大语言模型（LLM）的上下文学习（ICL）成为低资源NER的有前景范式，但现有方法存在三大关键局限：
  1. **标注数据稀缺**：少样本ICL方法依赖从大规模标注支持集中动态检索示例，在低资源场景下难以奏效。
  2. **领域知识不足**：零样本ICL方法过度依赖LLM内部的领域知识，对于新兴或专业领域（如生物医学）泛化能力有限。
  3. **缺乏外部知识与消歧**：现有方法仅关注示例选择，忽略显式注入外部知识（如维基百科事实）和对歧义实体的系统性消歧。
- **研究动机**：为了解决上述问题，论文提出了一个多智能体框架KDR-Agent，通过集成知识检索、消歧和反思分析来增强低资源、多领域的上下文NER。

## 2. 方法论：核心思想与关键技术细节

### 2.1 整体框架

KDR-Agent包含两个阶段：
- **阶段一：知识上下文构建**：构建包含自然语言类型定义、静态少样本对比示例、外部检索知识和消歧信息的增强提示。
- **阶段二：反思与修正**：通过结构化自我评估检测并修正初始预测中的常见错误。

### 2.2 关键技术细节

- **自然语言类型定义**：为每个实体类型提供简洁的文本描述（包含包含和排除标准），帮助LLM理解类型语义，减少对大规模标注集的依赖。
- **静态少样本对比演示**：构建少量（5或10个）人工标注示例，每个示例中混入正确实体-类型对和四种常见错误的负例（边界错误、类型错误、虚假实体、遗漏实体），形成对比监督。这消除了动态检索的需要。
- **中央LLM规划器**：识别输入文本中需要外部知识的术语和歧义实体，生成维基百科搜索查询和歧义消解提示。
- **知识检索代理**：通过MediaWiki API从维基百科检索知识摘要，仅保留简介段落，作为外部事实背景。
- **消歧代理**：对标记为歧义的实体进行上下文推理，生成自然语言解释以澄清其语义角色。
- **反思分析代理**：对初始预测进行结构化错误分析（基于四种错误类型：跨度错误、类型错误、虚假检测、遗漏），生成诊断报告和修正建议。
- **修正输出**：结合反思报告和修正指令，进行第二轮预测，输出最终结果。

### 2.3 公式流程（文字说明）

- 初始预测：`ˆy(0) = LLM(x, Ptype, Pdemo, Pknow, Pdisamb, Ptask)`
- 反思生成：`R = Reflect(x, ˆy(0), PReflection)`
- 最终预测：`ˆy(1) = LLM(x, ˆy(0), PReflection, R, PCorrection)`

## 3. 实验设计

### 3.1 数据集与场景

- **五个领域、十个标准NER数据集**：
  - 生物医学：BC5CDR、NCBI
  - 任务型对话：MIT Movie、MIT Restaurant
  - 新闻：CoNLL-2003、OntoNotes 5.0
  - 社交媒体：Twitter Broad、Twitter NER-7
  - 开放域：WikiANN（英文子集）、WNUT-17
- **低资源设置**：少样本示例数设为5（多数数据集）或10（类型较多的数据集）。每个领域仅使用少量标注示例共享。

### 3.2 基准方法

- **零样本ICL NER**：ChatIE、Self-Improving、CMAS
- **少样本ICL NER**：GPT-NER、Code-IE
- **LLM骨干**：GPT-4o（商业闭源）、DeepSeek-V3（开源）、Qwen-2.5-72B（开源）

### 3.3 评估指标

- 主要指标：F1分数（实体级别识别性能）

## 4. 资源与算力

- **论文中未明确说明**使用的GPU型号、数量、训练时长等算力信息。因此无法总结算力消耗。
- 代码已开源：https://github.com/MWXGOD/KDR-Agent

## 5. 实验数量与充分性

- **主要实验**：在三个LLM骨干上，对10个数据集进行了完整对比（共30组主要结果）。
- **消融实验**：在NCBI、OntoNotes 5.0、Twitter NER-7三个代表性数据集上，以GPT-4o为骨干，去除了四个关键组件（反思阶段、知识检索代理、消歧代理、负例对比示例），共进行了4个变体的消融分析。
- **骨干规模影响实验**：使用4种不同大小的Qwen模型（7B、14B、32B、72B）在NCBI、OntoNotes 5.0、Twitter NER-7上测试了F1性能。
- **错误分析**：在三个数据集上，对比了有无反思阶段的四种错误率（跨度、类型、虚假、遗漏）。
- **充分性评价**：实验覆盖了多种领域、多种骨干、多种基线方法，消融和错误分析全面，对比公平（基线方法采用同一骨干和设定）。但在低资源设定下，未与其他多智能体NER框架（如CMAS）进行更深层的组件对比；且未涉及跨语言或更大型数据集（如FewNERD）的测试。

## 6. 论文的主要结论与发现

1. **KDR-Agent在所有领域和骨干上显著超越所有零样本和少样本基线**，证明了多智能体框架的有效性。
2. **少样本对比演示（静态）方法优于动态检索方法**，在低资源场景下既降低了延迟又提升了鲁棒性。
3. **在生物医学和社交媒体等复杂领域中，KDR-Agent的提升尤为显著**，说明外部知识检索和消歧对专业领域至关重要。
4. **反思与修正阶段持续降低所有错误类型**，特别是虚假检测和类型错误。
5. **骨干模型规模对复杂领域影响更大**，小模型在生物医学和社交媒体上性能下降更明显。

## 7. 优点

- **方法创新**：首次将多智能体协作（规划、知识检索、消歧、反思）系统性地应用于低资源NER，解决了传统ICL方法的三个关键局限。
- **实用性**：仅需少量静态标注示例，无需大规模支持集和动态检索，降低了部署成本。
- **可解释性**：通过显式知识检索和反思报告，提供了可追溯的错误修正路径。
- **广泛验证**：在5个领域10个数据集上使用3种骨干模型验证，结果稳健。
- **代码开源**：便于复现和进一步研究。

## 8. 不足与局限

- **计算开销**：多智能体框架需多次调用LLM（初始推理 + 反思修正），虽然避免了检索，但推理成本仍高于单次ICL方法。论文未分析成本对比。
- **外部知识依赖**：知识检索依赖于维基百科，对于极专业化或非英语资源有限的领域可能不适用。
- **消歧范围有限**：仅处理中央规划器识别的歧义实体，可能遗漏未标记的隐性歧义。
- **实验覆盖**：未测试在极低资源（如仅1-2个示例）下的表现；未与基于微调的小型NER模型对比；未涉及跨语言场景。
- **类型定义生成**：虽然提到可从标注指南自动蒸馏，但实际实验中是否人工编写或自动生成未明确，可能影响可复现性。
- **偏差风险**：仅使用英文数据集，结论可能不适用于其他语言。维基百科内容本身可能存在领域或文化偏差。

（完）
