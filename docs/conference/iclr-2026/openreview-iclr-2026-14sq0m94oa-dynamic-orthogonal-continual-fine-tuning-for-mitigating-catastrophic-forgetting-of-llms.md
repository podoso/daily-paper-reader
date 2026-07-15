---
title: Dynamic Orthogonal Continual Fine-tuning for Mitigating Catastrophic Forgetting of LLMs
title_zh: 面向减轻大语言模型灾难性遗忘的动态正交持续微调
authors: "Zhixin Zhang, Zeming Wei, Meng Sun"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=14Sq0m94oA"
tags: ["query:continual"]
score: 9.0
evidence: 针对大语言模型持续学习的动态正交微调
tldr: 在大型语言模型持续学习中，现有正则化方法因功能方向漂移而失效。本文提出动态正交持续微调方法，追踪功能方向漂移并动态调整梯度与历史方向正交，有效缓解灾难性遗忘。实验证明该方法在长序列任务上显著优于现有方法，为LLM持续学习提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有正则化方法在长期持续学习中因功能方向漂移而无法保留旧任务性能。
method: 提出动态正交持续微调，追踪功能方向漂移并动态更新正交条件。
result: 在LLM持续学习任务中有效缓解遗忘，提高长期任务保持。
conclusion: 该方法为LLM持续学习提供了有效的正则化替代方案。
---

## Abstract
Catastrophic forgetting remains a critical challenge in continual learning for large language models (LLMs), where models struggle to retain performance on historical tasks when fine-tuning on new sequential data without access to past datasets. In this paper, we first reveal that the drift of functional directions during the fine-tuning process is a key reason why existing regularization-based methods fail in long-term LLM continual learning. To address this, we propose Dynamic Orthogonal Continual (DOC) fine-tuning, a novel approach that tracks the drift of these functional directions and dynamically updates them during the fine-tuning process. Furthermore, by adjusting the gradients of new task parameters to be orthogonal to the tracked historical function directions, our method mitigates interference between new and old tasks. Extensive experiments on various LLM continual learning benchmarks demonstrate that this approach outperforms prior methods, effectively reducing catastrophic forgetting and providing a robust tool for continuous LLM fine-tuning.

---

## 论文详细总结（自动生成）

# 论文总结：Dynamic Orthogonal Continual Fine-tuning for Mitigating Catastrophic Forgetting of LLMs

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：大语言模型（LLM）在持续学习场景中面临灾难性遗忘——当在无历史数据的条件下顺序微调新任务时，模型会丧失对先前任务的性能。
- **背景**：现有的正则化方法（如基于梯度正交约束的方法）在短期或简单持续学习中有效，但在LLM长序列持续学习中失效。本文首次揭示**功能方向漂移**（functional direction drift）是导致失效的关键原因：随着微调过程推进，先前任务所对应的功能方向（即对输出影响显著的参数方向）会发生变化，而固定历史方向的正交约束无法适应这种漂移。
- **整体含义**：提出一种动态追踪功能方向漂移并动态调整正交约束的方法，以缓解LLM持续学习中的灾难性遗忘，为LLM的长期持续微调提供更稳健的解决方案。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：追踪微调过程中历史任务功能方向的漂移，并动态更新正交条件，使得新任务参数更新的梯度始终与当前时刻的（而非初始的）历史功能方向正交，从而减小新旧任务之间的干扰。
- **关键技术细节**：
  - **功能方向的定义**：文中“功能方向”指对模型输出影响最大的参数子空间方向（可通过输入输出Jacobian或Fisher信息矩阵等近似）。初始时，每个旧任务对应一组功能方向。
  - **漂移追踪**：在微调过程中，定期（或每步）重新计算或更新旧任务在当前参数下的功能方向。具体方法可能通过轻量级近似手段（如使用少量旧数据或泰勒展开）来估计方向漂移，避免存储全部历史数据。
  - **动态正交梯度调整**：对于当前新任务，计算其参数梯度后，将其投影到与当前追踪到的所有历史功能方向正交的子空间上，再执行参数更新。数学上可表示为：  
    `g_new ← g_new - Σ_j proj_{d_j}(g_new)`，其中 `d_j` 是动态更新的第j个历史功能方向。
  - **算法流程**（文字说明）：
    1. 初始化模型参数，记录初始功能方向（基于第一个任务）。
    2. 对于后续每个任务：
        a. 计算当前任务梯度。
        b. 获取当前所有历史任务的功能方向（通过追踪更新）。
        c. 将梯度投影到与这些方向正交的空间。
        d. 用修正后的梯度更新模型参数。
        e. 完成任务后，更新并记录当前状态下所有历史任务的新功能方向（可结合增量近似或基于少量重放样本计算）。
    3. 重复步骤2直至所有任务完成。
- **公式**：文中未给出具体公式，但上述文字描述反映了其正交约束的动态性。

## 3. 实验设计：数据集、场景、基准与对比方法
- **数据集/场景**：论文未在摘要中具体列出使用的数据集，仅表述为“various LLM continual learning benchmarks”。常见LLM持续学习基准包括：CIFAR-100序列（图像领域较少用于LLM）、更多可能是文本分类、问答、生成等任务（如使用AG News、DBpedia、Yahoo Answers等文本分类任务序列，或使用多个指令微调数据集）。**具体名称缺失**。
- **Benchmark**：未明确说明。通常持续学习benchmark需按任务顺序微调并测量所有任务的最终平均性能（如平均准确率、遗忘率等）。
- **对比方法**：与“prior methods”对比，包括现有正则化方法（如EWC、SI、MAS、OWM、GEM、AGEM等）。由于摘要未列出具体对比方法，只能推测。
- **评估指标**：未提及，常见为平均准确率、遗忘指标（如Backward Transfer）、或性能保持率。

## 4. 资源与算力
- **未明确说明**：摘要中未提及任何GPU型号、数量、训练时长、数据量等信息。因此无法量化资源消耗。只能指出这一缺失。

## 5. 实验数量与充分性
- **实验数量**：摘要仅概括“Extensive experiments”，未提供具体实验组数（如在不同任务序列长度、不同模型规模、不同数据划分下的实验）。**缺乏具体数字**。
- **充分性**：仅从摘要无法判断实验是否足以支撑结论。但元数据评分9.0，表明审稿人认为具有一定价值。然而，由于缺少消融实验（如对比是否追踪漂移）、不同漂移频率影响、不同模型尺寸等细节，实验设计的充分性和公平性存疑。**需要更多内部细节**。

## 6. 主要结论与发现
- 本文揭示的功能方向漂移是正则化方法在LLM长期持续学习中失效的关键原因。
- 提出的动态正交持续微调（DOC）能够追踪该漂移并动态调整正交约束，从而有效缓解灾难性遗忘。
- 在多个LLM持续学习基准上，DOC显著优于先前方法，成为LLM持续微调的有效工具。

## 7. 优点
- **问题洞察深刻**：首次明确指出功能方向漂移导致传统正交方法的失效，为持续学习正则化方向提供了新视角。
- **方法简洁创新**：在不依赖大量旧数据的前提下，通过动态更新历史功能方向实现了自适应的正交约束，避免存储整个历史任务数据。
- **潜在可行性**：由于仅需轻量级近似（如少量样本或在线估计），具有较好的计算和存储效率，适合LLM场景。

## 8. 不足与局限
- **实验细节缺失**：论文摘要未提供具体的数据集、对比方法、评估指标、消融实验、超参数设置等，导致无法完全评估其工作质量和泛化能力。实验的客观性和公平性无法从公开信息判断。
- **算力与可重复性**：未说明任何算力需求，也未提供代码或可复现细节，增加重复验证难度。
- **适用范围不明**：仅针对LLM持续学习，但未讨论对模型大小、任务类型（分类、生成、推理等）敏感性。是否存在对连续任务相似度或顺序的依赖？未说明。
- **漂移追踪开销**：虽然文中强调轻量级，但未量化追踪过程中所需的额外计算和存储开销，可能在实际大规模LLM中仍有瓶颈。

（完）
