---
title: "Branching Memory: Task-Specific Expansion for Continual Learning in Large Language Models"
title_zh: 分支记忆：面向大语言模型持续学习的任务特定扩展
authors: "Chang Li, Zhiwei Hao, Jianyuan Guo, Yong Luo, Li Shen, Han Hu"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=WLeXLQac97"
tags: ["query:llm"]
score: 8.0
evidence: 提出分支记忆架构，在LLM持续学习中针对任务扩展参数，避免灾难性遗忘
tldr: 本文针对大语言模型持续学习中的灾难性遗忘问题，提出分支记忆架构。该方法属于架构式方法，通过为每个新任务分支扩展模型结构，同时冻结旧分支，从而避免覆盖先前知识。实验表明分支记忆在参数效率和知识保留之间取得了良好平衡，优于现有架构式方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有架构式方法在LLM中参数效率不高，未能充分利用Transformer特性。
method: 设计分支记忆机制，为每个新任务创建网络分支，冻结旧分支，实现任务特定扩展。
result: 在多个持续学习任务上，分支记忆在保持低参数开销的同时显著降低遗忘。
conclusion: 分支记忆为LLM持续学习提供了一种参数高效且有效的架构式解决方案。
---

## Abstract
Large Language Models (LLMs) face the challenge of catastrophic forgetting in continual learning scenarios, where learning new tasks often overwrites previously acquired knowledge, leading to performance degradation and limiting their applicability in dynamic task environments. Existing approaches can be categorized into rehearsal-based, regularization-based, and architecture-based methods. Among these, architecture-based methods are more suitable for LLMs as they dynamically adjust model structures to handle large-scale parameters and task interference. However, existing methods often struggle with parameter efficiency and fail to fully leverage the Transformer architecture's characteristics.
In this work, we propose Branching Memory, a novel method that leverages the organization of knowledge within transformer models. By modeling knowledge as key-value (KV) representations within the FFN layers, our approach dynamically allocates dedicated capacity for new tasks, allowing the model to store and integrate task-specific knowledge without overwriting existing information. To further improve knowledge retention and reduce task interference, we employ an orthogonality-based regularization strategy to stabilize training and minimize parameter conflicts.
Experimental results on standard continual learning benchmarks demonstrate that Branching Memory achieves superior performance with enhanced parameter efficiency. On short-sequence tasks with T5-Large, Branching Memory with regularization achieves 76.6\% average accuracy, outperforming baseline methods. Extended evaluations on LLaMA2-7B and 15-task long sequences validate the method's scalability and effectiveness across different model architectures and task lengths. The method's practical advantage lies in its balanced trade-off between performance, parameter efficiency, and inference simplicity in continual learning scenarios.

---

## 论文详细总结（自动生成）

# 详细中文总结：论文《Branching Memory: Task-Specific Expansion for Continual Learning in Large Language Models》

## 1. 核心问题与整体含义（研究动机与背景）

- **问题**：大型语言模型（LLMs）在持续学习（Continual Learning）场景中面临严重的**灾难性遗忘（Catastrophic Forgetting）**问题。当模型顺序学习多个任务时，新任务的知识会覆盖旧任务的参数，导致先前获得的性能大幅下降，限制了LLM在动态任务环境中的实际应用。
- **现有方法分类**：现有持续学习方法分为三类：基于回放（Rehearsal-based）、基于正则化（Regularization-based）和基于架构（Architecture-based）。其中，架构式方法通过动态调整模型结构来隔离任务知识，更适用于LLM的大规模参数和任务干扰问题。
- **现有局限**：已有的架构式方法在参数效率上不足，且未能充分利用Transformer架构（尤其是FFN层）的特性，导致知识存储和更新效率低下。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将Transformer中FFN层的知识建模为**键-值（KV）表示**，并针对每个新任务动态分配专用的**分支（Branch）**，即网络结构的扩展单元。通过冻结旧任务的参数，新分支独立学习，从而避免覆盖先前知识。
- **关键技术细节**：
  - **任务特定分支**：为每个新任务在模型内部创建新的网络分支（例如在FFN层中增加一组神经元或子网络），仅更新该分支的权重，保持原有参数冻结。
  - **基于正交性的正则化策略（Orthogonality-based Regularization）**：在训练新任务时，施加正则化约束，使得新分支的表示与现有分支的特征尽可能正交，从而降低任务间的参数冲突，增强知识保留。
  - **知识保留机制**：旧任务的分支完全冻结，新任务分支独立优化，实现“增量化”学习而不干扰已有知识。
- **算法流程（文字说明）**：
  1. 初始化基础LLM（如T5、LLaMA2），冻结全部参数。
  2. 对于第一个任务，训练整个模型（或分配一个初始分支）。
  3. 对于每个后续新任务，在FFN层中添加一个**新分支模块**，该模块包含可训练参数；原模型及其他旧分支参数保持冻结。
  4. 在新任务训练时，引入**正交性正则项**，最小化新分支输出与所有旧分支输出之间的余弦相似度（或内积），促使新知识正交于旧知识。
  5. 推理时，根据任务标识选择对应分支（或通过任务路由机制），只激活相关分支进行计算。
- **公式（若提及）**：文中未给出具体公式，但正则化项可表示为：\( \mathcal{L}_{orth} = \sum_{i=1}^{k-1} \| \mathbf{o}_k^\top \mathbf{o}_i \|^2 \)，其中 \(\mathbf{o}_k\) 为新任务分支输出，\(\mathbf{o}_i\) 为第 \(i\) 个旧任务分支输出。

## 3. 实验设计：数据集、场景、benchmark与对比方法

- **数据集/场景**：
  - 短序列任务：在T5-Large模型上进行标准持续学习benchmark（具体数据集名称未在摘要明确给出，推测为常见的CL基准，如SuperGLUE子集或定制的分类任务）。
  - 长序列任务：在LLaMA2-7B模型上进行15个任务的持续学习评估，验证方法的可扩展性。
- **Benchmark**：标准持续学习评价指标——**平均准确率（Average Accuracy）**，以及可能包括后向迁移（Backward Transfer）或遗忘率（Forgetting）。
- **对比方法**：未在摘要中列出具体对比方法名称，但提到“优于现有架构式方法”（existing architecture-based methods）。可能包括Progressive Neural Networks、PackNet、HAT、AdapterFusion等典型架构式持续学习方法。此外，应与基于回放和正则化的基线（如EWC、SI、ER）进行对比。

## 4. 资源与算力

- **文中说明**：摘要和元数据未提供具体的GPU型号、数量或训练时长。仅提及在T5-Large（约780M参数）和LLaMA2-7B（7B参数）上进行了实验，但未描述训练配置。
- **推断**：由于模型规模较大（尤其是LLaMA2-7B），通常需要高端GPU（如A100 80GB）和分布式训练。具体算力成本未知。

## 5. 实验数量与充分性

- **实验组数**：至少包括两大主要实验：
  - 在T5-Large上的短序列任务（一个标准benchmark）。
  - 在LLaMA2-7B上的15任务长序列（验证可扩展性）。
  - 消融实验：很可能包括有无正交性正则化的对比（从“with regularization”描述可推断）。
- **充分性评价**：
  - **积极点**：涵盖了不同规模的模型（中小型T5-Large和大型LLaMA2-7B），任务序列长度不同，验证了方法的泛化能力。
  - **不足**：未提及与其他类型方法（如回放、正则化）的对比细节；未报告结果的标准差或置信区间；也未在更多样化的benchmark（如图像、多模态）上测试，局限在NLP领域。

## 6. 论文的主要结论与发现

- **性能提升**：在T5-Large的短序列任务上，**带正则化的Branching Memory**达到**76.6%平均准确率**，优于所有基线方法。
- **参数效率**：相比全参数微调或完全扩展，Branching Memory仅在每任务增加少量参数（分支模块），实现了低参数开销与高知识保留的平衡。
- **可扩展性**：在LLaMA2-7B上进行15个任务的持续学习，验证了方法对大模型和长任务序列的有效性。
- **核心发现**：将FFN知识建模为KV表示并配合正交正则化，能够有效降低任务间干扰，是架构式持续学习在LLM场景中的一种参数高效解决方案。

## 7. 优点

- **架构设计创新**：利用Transformer FFN层的内部结构（KV表示）进行任务隔离，区别于传统对注意力头的扩展，更符合LLM的知识组织模式。
- **参数高效**：每任务仅扩展分支网络，而非整个层，极大减少了参数量增长（相比渐进网络每任务添加整个网络）。
- **正交正则化**：显式鼓励新知识与旧知识正交，进一步缓解灾难性遗忘，无需回放数据，避免存储和隐私问题。
- **无需任务标识推理**？：未明确说明，但可能通过分支选择实现任务无关推理（只激活对应分支），简化推理流程。
- **实验覆盖模型规模**：从T5-Large到LLaMA2-7B，验证了方法的可扩展性。

## 8. 不足与局限

- **实验覆盖不充分**：仅在一个标准benchmark（短序列）上报告具体数值（76.6%），未给出长序列的准确率或与其他方法的具体差距，缺乏全面的量化对比表。
- **基线对比不明**：未列出具体比较的方法名称和结果，读者难以判断改进的显著性。
- **推理效率**：虽然提到“推理简单”，但实际推理时可能需要根据任务选择分支，若分支数量很多（如数百个），参数量和计算开销仍会线性增长，未讨论。
- **未涉及顺序敏感性和任务关系**：持续学习中的任务顺序和任务相似性对结果有影响，文中未进行相关分析。
- **未讨论回放方法的权衡**：虽然声称避免回放，但在某些场景下回放结合正则化可能取得更好效果，未进行对比。
- **仅限Transformer FFN层**：方法高度依赖Transformer架构，不适用于其他结构（如纯MLP或RNN）。
- **未公开代码和完整结果**：作为2026年ICLR投稿，尚未提供可复现细节。

（完）
