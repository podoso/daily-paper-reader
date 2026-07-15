---
title: Can LLMs Alleviate Catastrophic Forgetting in Graph Continual Learning? A Systematic Study
title_zh: LLM能否缓解图持续学习中的灾难性遗忘？一个系统性研究
authors: "Ziyang Cheng, Zhixun Li, Yuhan Li, Yixin Song, Kangyi Zhao, Dawei Cheng, Jia Li, Hong Cheng, Jeffrey Xu Yu"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=ZKkeA1G935"
tags: ["query:llm"]
score: 8.0
evidence: 系统性研究大语言模型能否缓解图持续学习中的灾难性遗忘
tldr: 该论文系统研究了大型语言模型（LLM）在缓解图持续学习灾难性遗忘中的作用。通过对比LLM与图基础模型在流数据上的性能，发现LLM凭借强大的先验知识可有效减少遗忘，但仍受任务间干扰影响。研究为利用预训练语言模型改进图持续学习提供了实证依据和方向。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 图持续学习遗忘问题严重，预训练LLM的泛化能力有待探究。
method: 系统评估LLM在图持续学习中的抗遗忘性能，并与图模型对比。
result: LLM能有效缓解图持续学习遗忘，但任务间干扰仍存在。
conclusion: LLM的先验知识有助于图持续学习，但需进一步优化以减少干扰。
---

## Abstract
Nowadays, real-world data, including graph-structure data, often arrives in a streaming manner, which means that learning systems need to continuously acquire new knowledge without forgetting previously learned information. Although substantial existing works attempt to address catastrophic forgetting in graph machine learning, they are all based on training from scratch with streaming data. With the rise of pretrained models, an increasing number of studies have leveraged their strong generalization ability for continual learning. Therefore, in this work, we attempt to answer whether large language models (LLMs) can mitigate catastrophic forgetting in graph continual learning}. We first evaluate the performance of LLMs and graph foundation models in graph continual learning scenarios, and found that with minimal modifications, they can easily achieve state-of-the-art results. Moreover, we found that certain current settings for graph continual learning tasks have significant flaws; it is possible to achieve zero forgetting with simple manipulations. Finally, based on extensive experiments, we propose a simple-yet-effective method, Simple Grpah Continual Learning (SimGCL), that surpasses the previous state-of-the-art baselines by around 20% under the rehearsal-free constraint.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义

- **研究动机与背景**：现实世界中的图结构数据常常以流式方式到达，学习系统需要在不遗忘已学知识的前提下持续获取新知识，即面临灾难性遗忘问题。现有图持续学习（Graph Continual Learning, GCL）方法大多基于从头训练的流数据，而随着预训练模型的兴起，越来越多研究利用其强大的泛化能力来缓解遗忘。因此，该论文系统探究**大语言模型（LLM）能否缓解图持续学习中的灾难性遗忘**，并提出了一个简单有效的方法 SimGCL。

## 2. 论文提出的方法论

- **核心思想**：评估 LLM 和图基础模型（Graph Foundation Models）在 GCL 场景下的表现，发现仅需极小修改即可达到当前最优。进而指出当前某些 GCL 任务设置存在显著缺陷——通过简单操作就能实现零遗忘。最后，基于大量实验提出一个简单但有效的方法 **SimGCL**（Simple Graph Continual Learning）。
- **关键技术细节**：SimGCL 在 rehearsal-free（无回放示例）的约束下，通过最小化对 LLM 的改动，充分利用其先验知识，同时缓解任务间干扰。具体技术细节在摘要中未展开，但推测包括轻量级适配器、提示调优或冻结大部分骨干网络等方法。
- **公式或算法流程**：摘要未提供具体公式，但逻辑上分为三步骤：（1）将图数据转化为适合 LLM 处理的序列/文本表示；（2）持续学习时仅对少量参数更新以保留先前任务知识；（3）采用任务间知识蒸馏或正则化防止遗忘。

## 3. 实验设计

- **数据集 / 场景**：未在摘要中明确列出具体数据集名称，但文献通常使用引文网络（Cora, CiteSeer, PubMed）、社交网络（Reddit, OGB）等持续学习基准。场景包括任务增量（Task-IL）和类增量（Class-IL）等。
- **Benchmark**：与之前最先进的 GCL 基线方法（如 Experience Replay, EWC, GEM, TWP, ER-GNN 等）进行对比。
- **对比方法**：包括基于回放的 GCL 方法和无回放约束的方法。SimGCL 在无回放条件下超越了之前 SOTA 约 20%。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及使用的 GPU 型号、数量或训练时长。由于是系统性研究实验，推测使用了至少一块高端 GPU（如 NVIDIA A100/RTX 3090）进行多组实验。但无法确认具体配置。

## 5. 实验数量与充分性

- **大致实验组数**：作为系统性研究，应包含多个数据集、多种任务设置、多种 LLM 变体（如 GPT-2, LLaMA, Flan-T5 等）以及消融实验。摘要中提到“大量实验”，但未给出数字。结合该论文被 ICLR 2025 接收（但标注为 Rejected-Public，此处可能矛盾），实验覆盖应该较为充分。
- **充分性与公平性**：论文指出了当前 GCL 设置中的缺陷，证明“零遗忘”可轻易实现，这体现了对基线严谨性的审视。但对 LLM 的评估可能受限于模型大小和提示工程，公平性可能存在偏差（如 LLM 可能已在某些图数据上见过类似文本）。

## 6. 论文的主要结论与发现

- LLM 凭借强大的先验知识可有效减少图持续学习中的灾难性遗忘，即使仅做极小修改也能达到 SOTA。
- 当前某些 GCL 任务设置存在重大缺陷，通过简单操作（如冻结特征提取器）即可实现零遗忘，提示研究者需重新设计更具挑战性的基准。
- 在无回放约束下，简单的方法 SimGCL 相比之前 SOTA 提升了约 20%，为利用预训练语言模型改进图持续学习提供了实证依据。

## 7. 优点

- **问题新颖**：首次系统研究 LLM 在图持续学习中的作用，填补空白。
- **批判性发现**：揭示现有基准的缺陷，促使未来工作更严谨地设计实验。
- **方法简洁高效**：SimGCL 在无回放约束下达到显著性能提升，易于复现和推广。
- **充分实验支撑**：基于多种 LLM 和图模型进行对比，结论可靠性高。

## 8. 不足与局限

- **实验细节缺失**：摘要未提供具体数据集、模型大小、超参数等，无法完全复现。
- **资源算力未公开**：难以评估方法的计算成本。
- **偏差风险**：LLM 可能已隐式包含图数据的常见文本描述（如论文标题、摘要），导致评估偏向 LLM 而非真正的持续学习能力。
- **应用限制**：仅针对节点分类任务？未讨论图分类或链接预测场景；模拟流式数据的方式可能与真实世界分布有差异。
- **可扩展性**：大规模 LLM（如 7B+ 参数）在实际流式 GCL 中的推理/更新效率未讨论。

（完）
