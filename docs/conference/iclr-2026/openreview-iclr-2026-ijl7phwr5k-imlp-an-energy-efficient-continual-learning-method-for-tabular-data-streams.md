---
title: "IMLP: An Energy-Efficient Continual Learning Method for Tabular Data Streams"
title_zh: IMLP：一种面向表格数据流的能效持续学习方法
authors: "Yuandou Wang, Filip Gunnarsson, Rihan Hai"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ijL7phwr5k"
tags: ["query:continual"]
score: 8.0
evidence: 面向表格数据流的能效持续学习方法
tldr: 在边缘设备上处理表格数据流时，现有持续学习方法的回放缓冲区不断增长导致能耗高。本文提出IMLP，一种面向表格数据流的能效持续学习方法，通过优化记忆和计算资源，在减轻灾难性遗忘的同时保持低能耗。实验证明IMLP在多个基准上取得与现有方法相当的性能且大幅降低能耗。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有持续学习方法在边缘设备上处理表格数据流时能效和内存效率不足。
method: 提出IMLP方法，优化回放机制以实现低能耗持续学习。
result: 在表格数据流任务中达到与现有方法相当的遗忘缓解效果，同时能耗显著降低。
conclusion: 为资源受限环境下的持续学习提供了实用方案。
---

## Abstract
Tabular data streams are rapidly emerging as a dominant modality for real-time decision-making in healthcare, finance, and the Internet of Things (IoT). These applications commonly run on edge and mobile devices, where energy budgets, memory, and compute are strictly limited. Continual learning (CL) addresses such dynamics by training models sequentially on task streams while preserving prior knowledge and consolidating new knowledge. While recent CL work has advanced in mitigating catastrophic forgetting and improving knowledge transfer, the practical requirements of energy and memory efficiency for tabular data streams remain underexplored. In particular, existing CL solutions mostly depend on replay mechanisms whose buffers grow over time and exacerbate resource costs.

We propose a \textit{context-aware incremental Multi-Layer Perceptron (IMLP)}, a compact continual learner for tabular data streams. IMLP incorporates a windowed scaled dot-product attention over a sliding latent feature buffer, enabling constant-size memory and avoiding storing raw data. The attended context is concatenated with current features and processed by shared feed-forward layers, yielding lightweight per-segment updates.
\textcolor{blue}{We evaluate IMLP against state-of-the-art (SOTA) tabular models on real-world concept drift benchmark tabular datasets designed to assess models under temporal distribution shifts. Compared to TabPFNv2 under the \textit{incremental} concept drift, IMLP has 22.7\% total energy reduction while only a 0.05 final balanced accuracy drop. The results show that the proposed attention-based feature memory design can effectively guide the energy consumption while achieving the highest final accuracy in the abrupt concept drifts among all network baselines. }

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在边缘设备（如医疗、金融、物联网场景）上处理实时表格数据流时，现有持续学习方法面临能效和内存效率不足的挑战。尤其是回放机制中缓冲区不断增长，导致能耗和存储资源持续增加，难以满足资源受限环境的需求。
- **研究动机**：表格数据流是实时决策的重要模态，而现有持续学习（CL）研究虽在缓解灾难性遗忘方面取得进展，但针对表格数据流的能效和内存效率实际需求尚未充分探索。
- **整体含义**：提出IMLP方法，旨在保持模型持续学习能力的同时，显著降低计算和存储开销，为边缘设备上的表格数据流学习提供实用方案。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：提出一种上下文感知的增量多层感知机（IMLP），通过紧凑的持续学习结构，避免存储原始数据，实现常量大小的记忆，从而降低能耗和内存占用。
- **关键技术细节**：
  - **窗口化缩放点积注意力**：在滑动潜在特征缓冲区上应用注意力机制，使记忆大小保持恒定，不随时间增长。
  - **上下文融合**：将注意力加权后的上下文与当前特征拼接，然后通过共享的前馈层处理，实现轻量级的逐段更新。
  - **增量学习**：模型以逐段（per-segment）方式更新，无需存储整个数据流，适合流式处理。
- **算法流程（文字说明）**：
  1. 维护一个固定大小的滑动潜在特征缓冲区（存储近期特征）。
  2. 对当前输入特征，使用缩放点积注意力计算与缓冲区中各特征的相似度，得到上下文向量。
  3. 将上下文向量与当前特征拼接，输入共享的MLP前馈层。
  4. 模型参数通过反向传播更新（具体优化器与损失函数未在摘要中详述，推测为标准监督学习）。

### 3. 实验设计：数据集、基准场景、对比方法

- **数据集**：使用真实世界概念漂移基准表格数据集，专门设计用于评估模型在时间分布偏移下的性能。
- **基准场景**：包含两种概念漂移类型：
  - **增量概念漂移**（incremental drift）
  - **突变概念漂移**（abrupt drift）
- **对比方法**：与**TabPFNv2**（一种基于Transformer的表格数据方法）等最新表格模型对比。摘要未列出全部对比方法，但提到“与SOTA表格模型”对比，推断还包括其他持续学习方法（如经验回放、弹性权重巩固等），但未明确。

### 4. 资源与算力

- **摘要未明确说明**：论文内容未提及GPU型号、数量、训练时长等具体算力信息。仅从“能效”和“边缘设备”背景推测，实验很可能在资源受限的设备（如树莓派、移动端CPU）或低配GPU上进行，但无直接数据。需要指出这一点。

### 5. 实验数量与充分性

- **实验数量**：摘要仅给出了一个典型结果（与TabPFNv2在增量漂移下对比能耗和准确率），并提到在突变漂移下取得最高最终准确率。未列出完整实验数量（例如多少数据集、多少次重复、消融实验等）。
- **充分性与客观性**：信息不足。由于只有摘要，无法判断实验是否覆盖多种漂移类型、多种数据规模、多种基线方法。结论声称“在所有网络基线中突变漂移下取得最高准确率”，但未说明基线数量。存在选择性报告风险。因此，**实验充分性存疑**，需要完整论文验证。

### 6. 论文的主要结论与发现

- **主要结论**：IMLP在缓解灾难性遗忘的同时，大幅降低能耗。与TabPFNv2相比，在增量概念漂移下，IMLP总能耗降低22.7%，而最终平衡准确率仅下降0.05。在突变概念漂移下，IMLP在所有网络基线中取得最高最终准确率。
- **发现**：基于注意力的特征记忆设计可以有效引导能耗，同时保持甚至提升性能。

### 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次将窗口化注意力机制应用于表格数据流持续学习，实现恒定内存开销，避免原始数据存储，适合边缘设备。
- **能效突出**：取得与SOTA方法接近的准确率，但能耗显著降低（22.7%），极具实用价值。
- **场景针对性强**：专注于表格数据流，填补了持续学习在能效和内存效率方面的空白。

### 8. 不足与局限

- **实验覆盖不足**：仅通过摘要可见单一对比和两个漂移场景，缺乏多数据集、多基线、消融实验等充分验证。未报告统计显著性等。
- **信息不完整**：未提供模型结构详情、超参数设置、训练细节，难以复现。
- **偏差风险**：对比方法仅提及TabPFNv2，可能忽略其他更先进的CL方法。对实验结果的选择性强调（只突出高准确率场景）可能引入报告偏差。
- **应用限制**：方法依赖滑动窗口和注意力机制，对非常长的数据流或极高维度的特征可能仍有开销；边缘设备实际部署还需考虑硬件兼容性。

（完）
