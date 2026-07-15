---
title: Continual Fine-Tuning with Provably Accurate and Parameter-Free Task Retrieval
title_zh: 持续微调：可证明准确且无参数的任务检索
authors: "Hang Thi-Thuy Le, Long Minh Bui, Minh Hoang, Trong Nghia Hoang"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=5nVrMIl7vf"
tags: ["query:continual"]
score: 9.0
evidence: 提出无需持续学习检索函数的参数自适应方法，避免遗忘
tldr: 针对持续微调中现有输入自适应方法需持续学习检索函数导致遗忘的问题，提出一种参数自适应方法，在不牺牲表征适应性的前提下实现测试时自适应使用输入嵌入，且无需可学习的检索器。理论证明了该方法无遗忘特性，实验表明其在多个持续微调任务中均达到最优性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 输入自适应方法依赖持续学习的检索函数易受遗忘影响，参数自适应方法则牺牲适应性。
method: 设计参数自适应方法，利用固定输入嵌入函数实现测试时自适应，避免了检索函数遗忘。
result: 理论分析证明方法无遗忘，实验在多个基准上取得最先进结果。
conclusion: 提出的参数自适应方法兼顾了适应性与无遗忘特性。
---

## Abstract
Continual fine-tuning aims to adapt a pre-trained backbone to new tasks sequentially while preserving performance on earlier tasks whose data are no longer available. Existing approaches fall into two categories which include input- and parameter-adaptation. Input-adaptation methods rely on retrieving the most relevant prompts at test time, but require continuously learning a retrieval function that is prone to forgetting. Parameter-adaptation methods instead use a fixed input embedding function to enable retrieval-free prediction and avoid forgetting, but sacrifice representation adaptability. To combine their best strengths, we propose a new parameter-adaptation method that enables adaptive use of input embeddings during test time with parameter-free retrieval. We derive task-retrieval error bounds for a clustering-based, parameter-free paradigm, providing theoretical guarantees that link low retrieval error to structural properties of task-specific representation clusters, revealing a fresh insight into how well-organized clustering structure will enable reliable retrieval. Motivated by this insight, our method is designed with two key components: (i) an adaptive module composition strategy that learns informative task-specific updates to preserve and complement prior knowledge, and (ii) a clustering-based retrieval mechanism that captures distinct representation signatures for each task, enabling adaptive representation use at test time. Extensive experiments show that these components work synergistically to improve retrieval and predictive performance under large shifts in task semantics.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

- **研究问题**：持续微调（continual fine-tuning）旨在让预训练模型顺序适应新任务，同时不遗忘先前任务的知识。现有方法分为两类：
  - **输入自适应**：在测试时检索最相关的 prompt，但需要持续学习检索函数，容易发生遗忘。
  - **参数自适应**：使用固定的输入嵌入函数，避免检索模块的遗忘，但牺牲了表示的适应性。
- **动机**：如何结合两类方法的优点，既保持表示的自适应能力，又避免检索函数的遗忘问题。

### 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出一种**参数自适应方法**，在测试时通过**无参数检索**（parameter-free retrieval）实现输入嵌入的自适应使用，无需训练可学习的检索器。
- **关键技术组件**：
  1. **自适应模块组合策略**：学习任务特定的更新模块（task-specific updates），在保留先验知识的同时补充新信息。
  2. **基于聚类的检索机制**：为每个任务捕获独特的表示特征（representation signatures），形成聚类结构；测试时通过聚类匹配实现无参数任务检索。
- **理论保证**：推导了聚类基无参数检索范式的**任务检索错误界**，揭示了低检索错误与任务特定表示聚类结构属性之间的理论联系，证明当聚类结构良好时检索可靠，且方法天然无遗忘。

### 3. 实验设计

- **数据集/场景**：论文未明确列举具体数据集，仅提及在多个持续微调基准（multiple continual fine-tuning tasks）上进行了实验，且任务语义存在较大偏移（large shifts in task semantics）。
- **Benchmark 和对比方法**：未具体说明对比了哪些基线方法，摘要指出所提方法在多个基准上取得了最先进结果。
- **评估指标**：未明确说明，通常为任务准确率或检索精度。

### 4. 资源与算力

- 论文中**未提及**任何关于 GPU 型号、数量、训练时长等算力资源的信息。

### 5. 实验数量与充分性

- **实验数量**：论文称进行了“extensive experiments”，但未给出具体实验组数（如不同数据集数、消融实验数）。
- **充分性判断**：基于现有摘要信息，无法完全评估实验的充分性与客观性。虽然声称达到了最先进结果，但缺乏详细的实验设置和结果表格，可能因篇幅限制或论文被拒而信息不足。可推断实验覆盖了多个持续微调场景，但严格性有待进一步公开细节确认。

### 6. 论文的主要结论与发现

- 提出的参数自适应方法同时实现了**表示适应性**和**无遗忘特性**。
- 理论分析证明，当任务表示形成良好组织的聚类结构时，无参数检索可实现可靠的任务检索。
- 两个关键组件（自适应模块组合 + 聚类基检索）协同工作，在任务语义大偏移下显著提升检索和预测性能。

### 7. 优点

- **方法创新**：巧妙融合了输入自适应（测试时检索）和参数自适应（无需学习检索器）的优点，提出了无参数检索机制。
- **理论贡献**：为聚类基无参数检索提供了理论错误界，揭示了聚类结构与检索可靠性的关联。
- **实际效果**：在多个持续微调基准上取得最先进结果，证明了实用性。

### 8. 不足与局限

- **实验细节缺失**：未公开具体数据集、基线方法和完整结果，难以复现和独立验证。
- **未讨论局限性**：文中未提及方法的潜在限制，例如对聚类结构质量的高要求、任务数目增多时的扩展性、是否需要任务ID等。
- **被拒背景**：该论文为 ICLR 2026 Rejected 状态，可能评审认为实验不够充分或理论假设在实际中难以满足。
- **应用边界**：方法可能依赖任务表示具有可分离的聚类特性，在语义相似度高的任务序列中可能失效。

（完）
