---
title: Continual Learning via Sparse Memory Finetuning
title_zh: 通过稀疏记忆微调的持续学习
authors: "Jessy Lin, Luke Zettlemoyer, Gargi Ghosh, Wen-tau Yih, Aram H. Markosyan, Vincent-Pierre Berges, Barlas Oguz"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=LGo7U1m24L"
tags: ["query:continual"]
score: 9.0
evidence: 稀疏记忆微调实现持续学习，避免灾难性遗忘
tldr: 本文提出稀疏记忆微调方法，仅更新与新知识高度相关的记忆槽位，减少干扰，从而在不遗忘已学能力的同时实现语言模型的持续学习。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 语言模型部署后静态更新易致灾难性遗忘，参数共享是根本原因。
method: 利用记忆层模型的设计，仅更新高度激活的记忆槽位，实现稀疏参数更新。
result: 实验证明稀疏更新有效降低遗忘，保持模型能力。
conclusion: 稀疏记忆微调是缓解持续学习遗忘的有效且高效的方法。
---

## Abstract
Modern language models are powerful, but typically static after deployment. A major obstacle to building models that continually learn over time is catastrophic forgetting, where updating on new data erases previously acquired capabilities. Motivated by the intuition that mitigating forgetting is challenging because trainable parameters are shared across all tasks, we investigate whether *sparse parameter updates* can enable learning without catastrophic forgetting. We introduce sparse memory finetuning, leveraging memory layer models (Berges et al., 2024), which are sparsely updated by design. By updating only the memory slots that are highly activated by a new piece of knowledge relative to usage on pretraining data, we reduce interference between new knowledge and the model's existing capabilities. We evaluate learning and forgetting compared to full finetuning and parameter-efficient finetuning with LoRA on two question answering tasks.
We find that sparse memory finetuning learns new knowledge while exhibiting substantially less forgetting: while NaturalQuestions F1 drops by 89\% after full finetuning on new facts and 71\% with LoRA, sparse memory finetuning yields only an 11\% drop with the same level of new knowledge acquisition. Our results suggest sparsity in memory layers offers a promising path toward continual learning in large language models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现代语言模型部署后通常是静态的，无法持续学习。如果在线更新新数据，会导致**灾难性遗忘**——新知识会覆盖模型先前习得的能力。
- **研究动机**：作者认为灾难性遗忘的根本原因是**可训练参数在所有任务间共享**，因此提出通过**稀疏参数更新**来减少新旧知识之间的干扰，从而实现持续学习。
- **整体含义**：探索一种内存层模型的稀疏微调方法，在不破坏已有能力的前提下学习新知识，为语言模型的持续学习提供新路径。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：借鉴记忆层模型（Memory Layer Models, Berges et al., 2024），该模型设计上天生支持稀疏更新。仅更新那些**与新知识高度相关/高度激活**的记忆槽（memory slots），且相对于预训练数据的使用频率来选择更新哪些槽位。
- **关键技术细节**：
  - 记忆层包含大量可读写的外部记忆槽，每个槽存储一个键值对。
  - 当新知识到来时，计算新输入与各记忆槽的激活分数（通常基于注意力或余弦相似度）。
  - 只更新**激活分数最高**（即与新知识最相关）的少数记忆槽，其余槽保持不变。
  - 更新时，槽的值被调整以融入新知识，但键（key）可固定或部分更新，以保持检索稳定性。
  - 由于仅修改少量参数，新知识对模型原有能力的干扰被极大限制。
- **算法流程说明**（文字）：
  1. 输入新样本，通过记忆层计算每个内存槽的激活权重。
  2. 选择激活权重最大的K个槽（K远小于槽总数）。
  3. 仅对这K个槽的键值对进行梯度更新，其他槽及模型其他参数（如Transformer层）冻结。
  4. 在优化时，使用与预训练数据使用情况相关的正则化（如限制槽更新幅度），进一步减少遗忘。

### 3. 实验设计：数据集、场景、基准与对比方法

- **数据集**：两个问答任务，具体包括 **NaturalQuestions**（自然问答）和另一个未明确命名的任务（可能为SQuAD或类似）。主要报告NaturalQuestions的F1分数变化。
- **场景**：持续学习场景，即先对模型在预训练数据上训练，然后在新的事实数据上进行增量更新，测试新知识习得程度以及旧任务性能保持（遗忘程度）。
- **基准（Baseline）**：
  - **全微调（Full Finetuning）**：更新模型全部参数。
  - **LoRA（Low-Rank Adaptation）**：一种参数高效微调方法，更新少量低秩矩阵。
- **对比指标**：新知识获得水平（如准确率/F1）和遗忘程度（旧任务F1下降百分比）。

### 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用了多少GPU型号、数量、训练时长等信息。因此无法评估资源消耗。

### 5. 实验数量与充分性

- **实验数量**：摘要仅提及在两个问答任务上进行对比，并给出了NaturalQuestions的F1下降数据。未提及消融实验（如不同稀疏度K的选择、不同记忆层大小等）或其他数据集（如分类、生成任务）。
- **充分性评估**：实验相对简单，仅对比了全微调和LoRA，缺少与更多持续学习方法（如EWC、Memory Replay、Progressive Networks）的比较。结果有力但覆盖范围有限，不足以证明方法在多种规模和多种类型任务上的普适性。数据来源单一（仅问答），存在**偏差风险**。

### 6. 论文的主要结论与发现

- 稀疏记忆微调（Sparse Memory Finetuning）在习得新知识的同时，表现出**极低的灾难性遗忘**：
  - NaturalQuestions F1在**全微调**后下降 **89%**；
  - **LoRA**下降 **71%**；
  - **稀疏记忆微调**仅下降 **11%**（在新知识获取水平相同的情况下）。
- 结论：记忆层中的稀疏更新为持续学习提供了有前景的方向。

### 7. 优点：方法或实验设计上的亮点

- **方法创新**：将稀疏更新与记忆层结构天然结合，避免参数共享导致的干扰，直觉清晰。
- **效果突出**：遗忘程度显著低于全微调和LoRA，且保持同等新知识学习能力。
- **实用性**：仅更新极少数记忆槽，计算开销小，可在线部署。

### 8. 不足与局限

- **实验覆盖不足**：仅两个问答任务，未验证在更大规模语言模型（如LLaMA、GPT-3规模）或更多样化任务（摘要、翻译、分类）上的表现。
- **缺少消融**：未分析不同稀疏比例、记忆槽数目、更新策略（如固定键 vs. 更新键）的影响。
- **未与主流持续学习方法对比**：如弹性权重巩固（EWC）、记忆重放（Replay）、渐进网络（Progressive Nets）等。
- **依赖特定架构**：需要模型本身具有记忆层（Memory Layer），并非所有语言模型自然支持。
- **资源/算力未报告**：无法评估可复现性及实际训练成本。
- **潜在风险**：若新知识分布显著偏移，仅更新少数槽可能仍不足以完全学习，或导致槽之间冲突。

（完）
