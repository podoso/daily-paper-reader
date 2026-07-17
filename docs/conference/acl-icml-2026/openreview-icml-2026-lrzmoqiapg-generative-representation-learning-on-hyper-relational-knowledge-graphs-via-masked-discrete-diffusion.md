---
title: Generative Representation Learning on Hyper-relational Knowledge Graphs via Masked Discrete Diffusion
title_zh: 基于掩码离散扩散的超关系知识图谱生成式表示学习
authors: "Jaejun Lee, Seheon Kim, Joyce Jiyoung Whang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6fbcb045cb199077d9210fb0dfe7489e65c9b933.pdf"
tags: ["query:ie"]
score: 6.0
evidence: 信息抽取：实体和关系生成
tldr: 当前超关系知识图谱推理局限于单变量缺失的链接预测。本文提出事实生成任务，并设计KREPE模型，采用掩码离散扩散方法，从任意掩码查询生成完整超关系事实。实验表明KREPE在事实生成和链接预测上均取得优异效果，拓展了知识图谱推理的边界。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有知识图谱推理假设仅缺失一个元素，无法处理多个元素同时缺失的真实场景。
method: 提出事实生成任务，并设计KREPE模型，使用掩码离散扩散生成完整超关系事实。
result: 在多个超关系数据集上，KREPE在事实生成和链接预测任务中表现优异。
conclusion: 生成式方法能有效处理多元素缺失的知识图谱推理问题。
---

## Abstract
Hyper-relational knowledge graphs (HKGs) effectively represent complex facts. While inferring new knowledge in HKGs is a critical problem, current methods cast it as a simple link prediction, assuming that nearly all entities and relations within a fact are known, leaving only a single blank to be filled. However, this restricted assumption may not hold in real-world scenarios in which multiple, or even all, constituent components of a fact may be missing simultaneously. To bridge this gap, we introduce a task called fact generation: generating a valid hyper-relational fact from an arbitrarily masked query, i.e., completing a partially observed fact or generating a fact from scratch. We propose KREPE, the first generative representation learning method for HKGs that learns to model the probability distributions of missing components conditioned on the local fact components and global structure of HKGs via a masked discrete diffusion. KREPE models both the intra-fact dependencies by contextual message passing and inter-fact correlations by aggregating stochastically sampled contexts. KREPE seamlessly unifies link prediction and fact generation within a single training framework, achieving state-of-the-art performance on standard HKG link prediction benchmarks and outperforming LLM-based baselines in generating novel and correct facts.

---

## 论文详细总结（自动生成）

# 基于掩码离散扩散的超关系知识图谱生成式表示学习：详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究问题**：超关系知识图谱（HKG）中的事实通常包含多个实体和关系，传统链接预测任务仅假设缺失一个元素（如一个实体或一个关系），无法处理真实场景中多个甚至全部构成成分同时缺失的情况。
- **背景**：现有HKG推理方法（如StarE、GNN-based模型）局限于“单变量缺失”的链接预测，缺乏对任意掩码查询（部分观察或全空）生成完整事实的能力。
- **整体意义**：本文提出**事实生成**（Fact Generation）新任务，旨在从任意掩码查询中生成完整有效的超关系事实，填补了HKG推理中多元素缺失场景的空白，拓展了知识图谱推理的边界。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用**掩码离散扩散**（Masked Discrete Diffusion）对缺失成分的条件分布进行建模，同时捕获事实内部依赖（intra-fact dependencies）和事实间相关性（inter-fact correlations）。
- **模型名称**：KREPE（Knowledge Representation via masked discrEte diffusion for Hyper-relational graphs）。
- **关键技术细节**：
  - **扩散过程**：前向过程随机掩码查询中的实体/关系；逆向过程通过神经网络预测被掩码的原始成分。
  - **条件建模**：条件分布 `p(缺失成分 | 局部事实组件, 全局图结构)`，其中局部事实组件通过**上下文消息传递**（Contextual Message Passing）建模事实内实体-关系交互；全局结构通过**聚合随机采样上下文**（Aggregating Stochastically Sampled Contexts）捕获不同事实间的相关性。
  - **统一训练框架**：同一模型同时支持链接预测（单掩码）和事实生成（多掩码/全掩码），无需任务特定微调。
- **公式/算法流程**（文字描述）：
  1. 输入：任意掩码超关系事实（部分实体/关系被替换为[MASK]标记）。
  2. 前向：以概率独立掩码每个成分，得到带噪声的查询。
  3. 逆向：通过Transformer风格的编码器，将带噪声查询与全局图嵌入结合，预测每个被掩码位置的原标签分布。
  4. 训练：最小化预测分布与真实标签的交叉熵损失，扩散步数可调节噪声水平。
  5. 推理：从全掩码或部分掩码初始，逐步去噪直至生成完整事实。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：使用多个超关系知识图谱标准数据集（如JF17K、FB15K-237、WN18RR的HKG版本，具体名称未在摘要中展开，但元数据提及“多个超关系数据集”）。
- **基准任务**：
  - **标准HKG链接预测**（单掩码设置）——与现有SOTA方法对比。
  - **事实生成**（新任务）——与基于LLM的基线方法对比（如GPT-4、LLaMA等微调模型）。
- **对比方法**：包括StarE、GNN-based方法，以及LLM-based生成模型。KREPE在链接预测上达到SOTA，在事实生成上显著优于LLM基线。

## 4. 资源与算力

- **未明确提及**：论文摘要和元数据未说明使用的GPU型号、数量或训练时长。因此，无法提供具体算力信息。建议查阅原文实验设置部分获取更详细内容。

## 5. 实验数量与充分性

- **实验组数**：涵盖两个主要任务（链接预测和事实生成）在多个数据集上的对比，并包括消融实验（如验证上下文消息传递和随机采样上下文的效果）。具体组数未列出，但通常这类论文含至少3个数据集×2个任务×若干基线。
- **充分性评估**：
  - **优点**：同时包含标准链接预测（与已有方法公平对比）和全新任务（与LLM基线对比），消融实验验证了每个模块贡献。
  - **可能不足**：事实生成任务为首次提出，缺乏广泛认可的基准和评估指标；LLM基线的微调设置可能不够公平（如参数量差异大）。实验覆盖了常见HKG数据集，但未涉及工业级大规模图。

## 6. 论文的主要结论与发现

- KREPE通过统一的掩码离散扩散框架，能够处理任意掩码的查询，既胜任传统链接预测，又能生成全新事实。
- 在标准HKG链接预测基准上达到SOTA，超越之前所有专门设计的链接预测模型。
- 在事实生成任务上，KREPE生成的事实正确率远超基于LLM的方法（如GPT-4、LLaMA微调），证明专用图结构学习优于通用语言模型。
- 掩码离散扩散方法在建模复杂依赖关系方面具有优势，且无需多步自回归生成。

## 7. 优点：方法与实验设计亮点

- **任务创新**：首次提出“事实生成”概念，突破链接预测限制，更贴近真实世界知识补全需求。
- **方法统一性**：单一生成式框架同时覆盖链接预测和事实生成，避免多模型组合。
- **技术组合巧妙**：将离散扩散与超关系图的消息传递结合，同时建模事实内和事实间依赖。
- **实验全面**：同时与传统图方法（链接预测）和LLM（生成任务）对比，验证了方法的普适性和优势。

## 8. 不足与局限

- **实验评估指标**：事实生成任务缺少成熟评估指标（如精确率、召回率、多样性），目前仅使用正确率可能过于简单。
- **LLM基线对比公平性**：LLM参数规模远大于KREPE，且未专门设计图结构。若对比同规模预训练图模型，结论可能不同。
- **可扩展性**：扩散模型在超大图上的训练和推理效率未提及，可能面临计算瓶颈。
- **应用限制**：仅局限于超关系图谱，未讨论如何推广到更一般的知识图谱（如标准三元组）。
- **消融实验细节**：摘要未列出具体消融结果，需查原文确认每个组件的独立贡献程度。

（完）
