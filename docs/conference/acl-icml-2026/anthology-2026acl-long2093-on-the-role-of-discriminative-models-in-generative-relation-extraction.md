---
title: On the Role of Discriminative Models in Generative Relation Extraction
title_zh: 论判别式模型在生成式关系抽取中的作用
authors: "Guozheng Li, Peng Wang, Zijie Xu, Jing Zhou, Jiajun Liu, Ziyu Shang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2093.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 关系抽取技术
tldr: 现有生成式关系抽取方法受限于大语言模型的性能瓶颈。本文提出判别式到生成式（D2G）框架，利用判别式模型生成候选关系集合，辅助生成式模型提升抽取效果。实验表明该框架有效结合了两类模型的优势，为关系抽取提供了新思路。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2093/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1470, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2093/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2093/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 658, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2093/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 622, \"height\": 393, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 1015, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1580, \"height\": 648, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1625, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1099, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1220, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 763, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 587, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 769, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1539, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2093/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1462, \"height\": 286, \"label\": \"Table\"}]"
motivation: 生成式关系抽取性能受限，亟需探索判别式模型如何辅助提升其效果。
method: 提出D2G框架，先由判别式模型生成top-k候选关系，再由生成式模型从中确定最终关系。
result: 在多个关系抽取基准上，D2G框架显著优于纯生成式方法。
conclusion: 判别式模型可以有效支撑生成式关系抽取，两者结合优于单一范式。
---

## Abstract
Relation extraction (RE) identifies semantic relations between entities in text, with existing methods falling into two main paradigms: discriminative and generative. Discriminative models encode sentences and entities into relation representations and classify the most likely relation, whereas generative models directly produce relation labels through sequence generation. Although the latter have benefited from recent advances in large language models (LLMs), their performance remains limited by bottlenecks. In this work, we present the systematic investigation of how discriminative models can support generative RE. We propose the Discriminative-to-Generative (D2G) framework, which first leverages discriminative models to produce a top-k set of candidate relations, and then integrates this knowledge into generative models via in-context or prompt learning. Extensive experiments on five widely used RE benchmarks demonstrate that D2G consistently achieves state-of-the-art performance, with notable gains on long-tailed relation classes.

---

## 论文详细总结（自动生成）

## 关于判别式模型在生成式关系抽取中的作用（ACL 2026）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：关系抽取（Relation Extraction, RE）存在两种主流范式——**判别式模型**（通过分类层输出概率选择关系标签）和**生成式模型**（通过序列生成直接产出关系标签）。尽管生成式模型得益于大语言模型（LLM）的进步，但性能仍受限于瓶颈。本文系统探究**如何利用判别式模型来支持生成式关系抽取**，以弥补生成式模型的不足。
- **研究动机**：作者发现判别式模型的 top-k 预测集通常包含正确标签（recall > 95% at top-3），且这些候选关系与真实关系语义高度相似，蕴含丰富的“判别式知识”。同时，生成式模型在元上下文学习（meta in-context learning）中，若提供的示例包含真实关系，性能会提升。因此，将判别式知识注入生成式模型有望显著提升性能。
- **整体含义**：本文提出不需要二选一，而是将两种范式**协同整合**，为关系抽取提供新的思路：判别式模型先给出候选，生成式模型再精确定位。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：提出 **判别式到生成式（D2G）框架**：先由判别式模型为每个样本生成 top-k 候选关系集，将这些候选关系编码为判别式知识，再通过**上下文学习（ICL）** 或**提示学习（Prompt Learning, PL）** 注入生成式模型，辅助其做出更准确的预测。
- **关键技术细节**：
  - **判别式模型**：使用 RoBERTa 等编码器，输出关系概率分布，选取 top-k 关系作为候选集。对于每个候选关系，从训练集中检索语义最相似的样本（基于判别模型隐藏空间的距离），形成判别式知识 \(K\)。
  - **上下文学习版本（D2G + ICL）**：将检索到的样本作为演示示例，与输入拼接后送入生成式模型（如 T5）进行元上下文学习，生成式模型输出最可能的关系（限制在候选集内）。
  - **提示学习版本（D2G + PL）**：为了解决 ICL 的检索开销和干扰项问题，将 top-k 概率分布压缩为原型向量（通过MLP），再通过残差连接和门控机制与原始提示向量融合，作为生成式模型的动态前缀提示，实现端到端联合训练。联合优化判别式损失和生成式损失。
- **算法流程**：
  - 训练判别式模型（交叉熵损失）。
  - 对于每个训练样本，用判别式模型获取 top-k 预测集及对应的概率分布。
  - ICL版本：检索对应样本作为示例，训练生成式模型（因果语言建模损失），推理时先由判别式模型生成知识，再输入生成式模型。
  - PL版本：将 top-k 概率经 MLP 生成原型向量，与提示向量融合后作为生成式模型前缀，联合优化两个模型。

### 3. 实验设计
- **数据集**：使用五个公开关系抽取基准：**SemEval**（9个关系）、**TACRED**（41个关系）、**TACREV**（修正版TACRED）、**Re-TACRED**（40个关系）、**Wiki80**（80个关系）。
- **Benchmark**：对比了多种现有方法，包括：
  - 纯判别式方法（SpanBERT, LUKE, IRE, KLG, PTR, KnowPrompt, GenPT）
  - 纯生成式方法（REBEL, RELA, TANL, RE⁴）
  - 以及自己训练的判别式模型（DM）和生成式模型（GM）基线。
  - 还测试了**开源模型**（BERT+ BART, RoBERTa+T5, Llama-3-8B）和**闭源模型**（GPT-4o, DeepSeek-V3, DeepSeek-R1）。
- **评估指标**：Micro-F1 分数，取三次运行的平均值。

### 4. 资源与算力
- 论文提及所有实验在**一张 NVIDIA A100 (80GB) GPU**上完成。使用混合精度 fp16。
- 对于 Llama 等大模型，采用 LoRA 微调（rank=8, alpha=32）。
- 未明确总训练时长，但给出了各阶段的超参数（例如：判别模型训练10 epoch，生成模型训练5 epoch，批大小等）。

### 5. 实验数量与充分性
- 论文进行了**大量实验**：
  - **主实验**（5个数据集 × 多种方法组合，结果见表1和表2）。
  - **消融实验**（ICL和PL的组件：MLP、残差连接、门控机制）。
  - **敏感性分析**（top-k取值对性能影响，k从1到12）。
  - **长尾分析**（按关系频次分组，分析头类和尾类性能）。
  - **错误传播分析**（将测试集分为三组：top-1正确、top-k正确但top-1错误、top-k缺失，考察鲁棒性）。
  - **额外补充实验**（附录中包括判别器多样性、噪声注入、浅层消融、模型大小对比、k选择分析、效率分析等）。
- **充分性评判**：实验设计较为全面，覆盖了不同模型规模、不同提示方式、不同场景（开源/闭源），并深入分析了长尾、误差传播、超参数敏感性等。对比基线囊括了近年主流方法，结果客观。但未进行跨领域（如生物医学）的评估。

### 6. 论文的主要结论与发现
- **D2G框架**在五个基准上均取得**最先进（SOTA）性能**，显著优于纯判别式或纯生成式模型。
- **提示学习版本（D2G + PL）** 比上下文学习版本（D2G + ICL）更优，且对干扰更具鲁棒性，因为将判别信息压缩为向量，避免了检索噪声。
- **长尾关系**上提升尤为明显：D2G 缩小了头类与尾类的性能差距（D2G 差距~3.3%，而单独模型差距~6%），表明判别式知识有助于“拯救”长尾类。
- **错误传播**分析显示：即使判别式模型的 top-k 集不包含正确标签，D2G+PL 仍能通过原型向量传递辅助信号，表现优于纯生成式模型。
- **模型泛化性**：不同判别式架构（LUKE, SpanBERT）对最终性能影响很小；开源与闭源模型均受益。

### 7. 优点
- **方法创新**：系统地将判别式与生成式框架有机结合，提出两种实用注入方式（ICL/PL），其中 PL 设计巧妙（原型向量 + 残差门控），兼顾效果和效率。
- **实验全面**：覆盖5个数据集、多种模型大小（BERT到Llama）、两类使用场景（开源微调与闭源ICL），并深入分析长尾、误差传播等关键问题。
- **鲁棒性分析**：通过噪声注入和错误分组实验，证明了 PL 变体的鲁棒性优于 ICL。
- **代码与复现**：提供了详细超参数和算法伪代码，附录包含充分补充实验。

### 8. 不足与局限
- **实验覆盖有限**：仅基于五个标准英文 RE 基准，缺少跨领域（如生物医学、法律）或低资源语言的验证。
- **模型依赖性**：虽然判别式架构多样性影响不大，但整体框架依赖判别式模型的 top-k 召回率（≥95%），如果判别式模型质量极差，可能失效。
- **计算成本**：虽然推理时只需一次前向，但训练时需要联合优化两个模型（PL版本），显存和训练时间高于单模型。论文未给出完整训练时间。
- **闭源模型场景**：闭源模型只能使用 ICL 方式，性能仍低于微调后的开源模型，且对长尾数据集（如Wiki80）改善有限。
- **理论解释**：为何压缩概率分布比检索示例更有效，缺乏更深层理论分析（如信息论角度）。
- **超参数敏感**：top-k 取值需要基于验证集调整，可能存在跨数据集不稳定的情况。

（完）
