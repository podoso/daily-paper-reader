---
title: Enhanced Reasoning for Biomedical Document-Level Relation Extraction via a Novel Cascade Language Model Framework
title_zh: 通过新型级联语言模型框架增强生物医学文档级关系抽取的推理能力
authors: "Haohua Song, Wenhao Gu, Zhijing Li, Yunwenyu, Tiantian Zhu, Xiao Yang (杨潇), Zexuan Zhu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1517.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 使用级联PLM-LLM框架进行生物医学文档级关系抽取
tldr: 该论文提出CoRE级联框架，结合预训练语言模型和大语言模型的互补优势，通过检测-重思考范式增强生物医学文档级关系抽取的推理能力，有效缓解了大模型的幻觉问题，显著提升了复杂文档场景下的抽取性能。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1517/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 689, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1517/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1328, \"height\": 851, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1517/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1490, \"height\": 846, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1517/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1495, \"height\": 619, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1517/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 636, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 790, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 812, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 661, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1643, \"height\": 1814, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 796, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 798, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 800, \"height\": 97, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 796, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1517/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1658, \"height\": 180, \"label\": \"Table\"}]"
motivation: 预训练语言模型缺乏全局建模能力，而大语言模型在生物医学领域容易产生幻觉。
method: 提出检测-重思考级联框架，先由PLM检测候选关系，再由LLM进行推理验证。
result: 在生物医学文档级关系抽取上取得显著性能提升。
conclusion: CoRE框架有效结合了PLM和LLM的优势，为文档级关系抽取提供了新范式。
---

## Abstract
Biomedical document-level relation extraction poses significant challenges beyond sentence-level tasks, as it necessitates the integration of evidence from entire documents and the ability for coherent cross-sentence reasoning. While pretrained language models (PLMs) demonstrate efficiency in handling local contexts, they often struggle with global dependency modeling. Conversely, large language models (LLMs) exhibit strong reasoning capabilities but tend to generate hallucinations in knowledge-intensive biomedical domains. This paper introduces CoRE, a novel cascade framework that leverages the complementary strengths of PLMs and LLMs through a detect-then-rethink paradigm. The PLM serves as an efficient detector for high-confidence relations, while challenging cases are forwarded to an LLM enhanced with semantic retrieval and iterative reasoning mechanisms. Experimental results on BioRED and CDR datasets show that CoRE achieves substantial improvements over state-of-the-art baselines, validating the effectiveness of the proposed cascade paradigm for complex biomedical relation extraction.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：生物医学文档级关系抽取（BioDocRE）需要跨句子整合证据并进行连贯推理，远复杂于句子级任务。现有方法中，预训练语言模型（PLMs）擅长局部上下文处理但缺乏全局依赖建模能力；大语言模型（LLMs）推理能力强，但在知识密集型生物医学任务中容易产生幻觉（hallucination），并且计算成本高昂。
- **整体含义**：本文提出一种“检测-重思考”（detect-then-rethink）的级联框架CoRE，通过结合PLM的高效性和LLM的推理能力，在降低幻觉的同时提高复杂文档级关系抽取的准确性和效率。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用PLM作为初始检测器，对置信度高的样本直接输出；对于低置信度的困难样本，路由至LLM进行增强推理。
- **关键技术细节**：
  - **阶段一（PLM初始预测与路由）**：PLM（如DocuNet或e2eBioMedRE）对每个实体对预测关系类型并给出置信度分数 \(C(e_s, e_o) = \max_{r \in R} P(r|D, e_s, e_o)\)。通过验证集网格搜索确定阈值 \(\tau\)，仅当 \(C \ge \tau\) 时接受PLM预测，否则转入阶段二。
  - **阶段二（LLM增强推理）**：包含两个核心组件：
    - **基于提及聚合的语义检索（MASR）**：对每个实体的所有提及句子用Sentence-Transformer编码，然后通过LogSumExp（LSE）池化聚合得到实体向量，再拼接并L2归一化形成关系表示向量，用于从训练集中检索Top-K相似演示样例。
    - **迭代链式思维推理（ItCoT）**：包括动态错误经验库（DEEL）和经验驱动迭代自我反思（EDISon）。DEEL在推理前让LLM对检索到的演示进行预推理，对比黄金标签后总结错误类型和规避策略；EDISon则让LLM在生成初始推理后自我反思，若发现匹配DEEL中的错误模式则修正，直到确认或达最大迭代次数。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **CDR**（Chemical-Disease Relation dataset）：1500篇PubMed摘要，专注于化学物-疾病关系，训练/开发/测试各500篇。
  - **BioRED**：600篇PubMed文档，包含6种实体类型和多种关系类型（如正相关、负相关、关联等），训练/开发/测试各100篇。
- **基准（SOTA方法）**：对比了10余种方法，包括：
  - PLM基础方法：BioGPT、Bio-RFX、SSAN、KG-DGAN、FILR、ATLOP、BioREx、BERT-GT、PubMedBERT、DocuNet、e2eBioMedRE等。
  - 零样本大语言模型：Llama3.1-8B、Qwen2.5-7B、Deepseek-v3.2、GPT-4o、GPT-4.1、GPT-5等。
- **对比方式**：报告精确率、召回率、F1分数，并在CDR和BioRED的开发和测试集上评估。

## 4. 资源与算力

- 论文中未明确说明使用的GPU型号、数量、训练时长等具体硬件资源细节。仅在附录E中给出了基于GPT-5（2-shot）的API调用成本和延迟对比：在CDR测试集上，全量LLM推理（标准CoT）花费54.7美元、1220分钟；CoRE级联路由后降至29.8美元、648分钟。但未提及PLM微调或LLM部署所需的本地算力。

## 5. 实验数量与充分性

- **实验数量**：非常充分。包括：
  - 主实验：在CDR和BioRED两个数据集上对比了6种零样本LLM和9种PLM基线，并报告了6种LLM+CoRE的结果。
  - 消融实验：在BioRED上按7种实体对类型细化F1，并对比了Naïve CoT、LoRA微调、仅PLM级联（SLM）等变体。
  - 组件分析：在不同LLM上验证了MASR池化策略（三种）、检索策略（BM25、PURE、MASR）、错误经验格式（原始样例 vs DEEL）。
  - 阈值稳定性测试：在CDR开发集上验证了0.21~0.31阈值范围内的F1稳定性。
  - 幻觉量化分析：给出了低置信度子集上的假阳性率（FPR）和错误发现率（FDR）。
  - 成本效率分析：给出了token、费用、延迟对比。
- **充分性与公平性**：实验设计较为全面，覆盖了多个LLM系列和规模，消融实验验证了各组件的必要性。但部分对比（如LoRA）仅在CDR上进行了，BioRED上缺失；且未与最新其他级联框架（如仅用CoT的级联）进行系统比较，只对比了GPT-RE。总体公平。

## 6. 论文的主要结论与发现

- CoRE在CDR上达到88.20% F1，超过最佳PLM DocuNet（86.32%）1.88%；在BioRED上达到66.35% F1，超过最佳PLM e2eBioMedRE（64.44%）1.91%。
- 级联范式对多种LLM均有效，甚至小型LLM（如Llama3.1-8B）在CoRE中可超越大型模型单独使用的结果。
- 在长尾关系（如Chemical-Variant）上，CoRE带来显著提升（+35.57% F1），表明LLM阶段特别擅长处理训练数据稀疏的困难样本。
- 假阳性率大幅降低：在CDR低置信度子集上，Deepseek-v3.2的FPR从41.42%降至26.19%；GPT-4o的FPR从25.84%降至22.83%。
- 效率方面，选择性路由使API成本降低45.55%、延迟降低46.89%。

## 7. 优点

- **方法创新性**：提出“检测-重思考”级联范式，巧妙结合PLM和LLM的互补优势，同时解决了PLM推理不足和LLM幻觉过高的双重问题。
- **检索增强设计**：Mention-Aggregation-based语义检索（LSE池化）有效聚合跨句证据，优于传统句子级检索；DEEL+EDISon的迭代反思机制能够从错误中学习并抑制幻觉。
- **实验全面性**：覆盖多种LLM（7B~闭源旗舰）、多种PLM、多维度消融和幻觉分析，验证了方法的通用性和鲁棒性。
- **实用导向**：给出了成本效率分析，表明级联路由在实际部署中具有可负担性。

## 8. 不足与局限

- **阈值依赖**：置信度阈值需在验证集上手动调优，尽管文中指出稳定区间较宽，但仍依赖人为选择，未实现自适应机制。
- **检索受限**：MASR依赖训练集存在相关样本；若查询样本与训练集差异过大，检索效果可能下降。
- **延迟瓶颈**：低置信度样本需经历LLM推理和迭代反思，引入了额外延迟，可能不适用于实时场景。
- **硬件资源未详述**：未报告PLM微调、LLM部署的具体GPU算力和时间，不利于复现和公平比较。
- **消融实验覆盖不全**：LoRA微调仅在CDR上测试，未在BioRED上验证；且未与其他级联框架（如仅用CoT的级联）进行系统对比，仅与GPT-RE对比。
- **偏置风险**：实验主要基于英文生物医学文献，对多语言或其他领域（如临床记录）的泛化性未验证。

（完）
