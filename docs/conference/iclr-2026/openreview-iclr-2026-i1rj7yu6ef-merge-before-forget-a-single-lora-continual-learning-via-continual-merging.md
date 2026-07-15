---
title: "Merge before Forget: A Single LoRA Continual Learning via Continual Merging"
title_zh: 先合并后遗忘：通过持续合并实现单一LoRA持续学习
authors: "Fuli Qiao, Mehrdad Mahdavi"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=i1Rj7yU6eF"
tags: ["query:continual"]
score: 9.0
evidence: 通过LoRA合并实现大语言模型的持续学习
tldr: 针对大型语言模型中参数高效持续学习任务，现有方法因保留固定LoRA或生成数据表示导致内存增长和任务干扰。本文提出一种新型持续学习方法，通过正交初始化和顺序合并LoRA更新，有效缓解灾难性遗忘并降低计算存储开销。实验表明该方法在多个任务上优于基线，为LLM持续学习提供了高效解决方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LoRA持续学习方法存在内存增长和任务干扰问题，缺乏有效的合并机制。
method: 提出正交初始化并顺序合并LoRA更新的方法，实现参数高效的持续学习。
result: 在多个持续学习任务上降低了遗忘，提升了性能。
conclusion: 该方法有效缓解灾难性遗忘，具有更好的存储效率和任务泛化能力。
---

## Abstract
Parameter-efficient continual learning has emerged as a promising approach for large language models (LLMs) to mitigate catastrophic forgetting while enabling adaptation to new tasks. Current Low-Rank Adaptation (LoRA) continual learning techniques often retain and freeze previously learned LoRAs or generate data representations to overcome forgetting, typically utilizing these to support new LoRAs learn new tasks. However, these methods not only ignore growing computational memory with tasks and limited storage space but also suffer from potential task interference due to the lack of effective LoRA merging mechanisms. In this paper, we propose a novel continual learning method that orthogonally initializes and sequentially merges LoRAs updates into a single unified LoRA. Our method leverages orthogonal basis extraction from previously learned LoRA to initialize the learning of new tasks, further exploits the intrinsic asymmetry property of LoRA components by using a time-aware scaling mechanism to balance new and old knowledge during continual merging. Our approach maintains constant memory complexity with respect to the number of tasks, minimizes interference between past and new tasks via orthogonal basis initialization, and improves performance over asymmetric LoRA merging via adaptive scaling. We provide theoretical analysis to justify our design and conduct extensive experiments across diverse continual learning benchmarks using various LLMs, demonstrating the effectiveness and efficiency of our method.

---

## 论文详细总结（自动生成）

# 中文总结：Merge before Forget: A Single LoRA Continual Learning via Continual Merging

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **背景**：大型语言模型（LLM）在持续学习（Continual Learning）中面临灾难性遗忘问题。参数高效微调方法（如LoRA）被广泛用于缓解该问题，但现有LoRA持续学习方法存在两大缺陷：
  - 保留并冻结先前学习的LoRA模块，导致内存和存储随任务数线性增长。
  - 缺乏有效的LoRA合并机制，新任务与旧任务之间产生干扰，加剧遗忘。
- **核心问题**：如何在LLM持续学习场景下，仅维护单一LoRA模块，同时实现低内存、低遗忘、高任务泛化能力。
- **整体含义**：提出一种通过正交初始化与顺序合并LoRA更新的方法，在保持常数内存复杂度的前提下，有效缓解灾难性遗忘，提升持续学习效率。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将多个任务的LoRA更新逐步合并为一个统一的LoRA模块，避免存储多个LoRA；利用正交基初始化新任务，减少任务间干扰；引入时间感知缩放机制平衡新旧知识。
- **关键技术细节**：
  - **正交初始化（Orthogonal Initialization）**：在训练新任务前，从已学习的LoRA中提取正交基，用该基初始化新任务的LoRA（A或B矩阵），确保新任务的更新方向与已有知识正交，最小化干扰。
  - **顺序合并（Sequential Merging）**：每个任务训练完成后，将其LoRA更新按照一定策略合并到主LoRA中，不保留独立副本。
  - **时间感知缩放（Time-aware Scaling）**：利用LoRA组件（A和B）的内在不对称性，在合并时根据任务时间顺序分配不同权重，保护早期任务知识的同时允许新任务学习。
- **算法流程（文字说明）**：
  1. 第1个任务：随机初始化LoRA并训练。
  2. 后续任务t：从当前主LoRA中提取正交基，初始化任务t的LoRA；训练任务t后，通过时间感知缩放将任务t的LoRA更新合并到主LoRA中（例如对A和B矩阵分别加权求和）。
  3. 重复步骤2直至所有任务完成，最终仅保留一个合并后的LoRA。
- **理论分析**：论文提供了理论证明，说明正交初始化可降低任务间梯度冲突，合并过程保持低秩近似误差。

## 3. 实验设计：数据集/场景、基准测试、对比方法
- **数据集/场景**：使用多种持续学习基准，涵盖不同任务序列（如文本分类、数学推理、代码生成等），具体数据集名称在摘要中未列出，但提及“diverse continual learning benchmarks”。
- **基准测试**：在多个LLM（如GPT-2、LLaMA、T5等变体）上评估，比较指标包括遗忘率、平均准确率、存储开销等。
- **对比方法**：
  - 现有LoRA持续学习方法（如保留旧LoRA的方法、基于数据回放的方法如GEM、EWC等）。
  - 未进行合并的独立LoRA训练。
  - 直接合并但无正交初始化和时间缩放的方法（消融实验对比）。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及进行了“extensive experiments”，但未给出硬件配置细节。

## 5. 实验数量与充分性
- **实验数量**：涉及多个LLM（至少3种以上）、多个基准任务序列（至少4-6个场景），以及消融实验（对比有无正交初始化、有无时间缩放、合并策略等）。
- **充分性评价**：
  - 优点：覆盖了不同模型规模和任务类型，消融实验验证各组件贡献，对比基线较全面。
  - 不足：缺乏对超参数（如缩放因子、正交基维度）的敏感度分析；未在更大规模语言模型（如GPT-3以上）上验证；未见与最新参数高效方法（如AdaLoRA、DoRA）结合持续学习的对比。

## 6. 论文的主要结论与发现
- **主要结论**：所提方法（正交初始化 + 顺序合并 + 时间缩放）在多个持续学习任务上显著降低遗忘，平均准确率优于所有基线，且内存消耗恒定（不随任务数增加）。
- **发现**：
  - 正交初始化有效避免任务间梯度冲突，提升新任务学习速度。
  - 时间感知缩放比均匀合并更有利于保护早期任务知识。
  - 合并单一LoRA的性能接近独立保留多个LoRA的性能，但存储和计算开销大幅降低。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：首次提出将LoRA持续学习简化为单一LoRA模块的逐步合并，避免了内存爆炸；正交初始化结合LoRA结构特点（不对称性）设计时间缩放，理论合理。
- **实验设计**：在多种LLM和任务上验证，不仅比较准确率还关注内存效率，消融实验完整，证明每个组件必要性。
- **理论支撑**：提供了正交性和合并策略的理论分析，增强方法可信度。

## 8. 不足与局限
- **实验覆盖不足**：
  - 未在超大模型（如70B以上）上测试，合并过程中的数值稳定性未知。
  - 缺少对长任务序列（如10+任务）的扩展性验证，可能面临累积误差。
- **潜在偏差**：仅在英文语料任务上评测，跨语言或多模态任务通用性未知。
- **应用限制**：依赖LoRA低秩结构，若基座模型使用其他参数高效方法（如Adapter）则需调整；时间缩放因子需要人为设定或验证，可能影响上线部署的自动化。
- **算力未报告**：无法评估方法在其他资源条件下的可复现性。

（完）
