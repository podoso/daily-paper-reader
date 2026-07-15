---
title: "Little By Little: Continual Learning via Self-Activated Sparse Mixture-of-Rank Adaptive Learning"
title_zh: 逐步积累：基于自激活稀疏混合秩自适应学习的持续学习
authors: "Haodong Lu, Chongyang Zhao, Jason Xue, Lina Yao, Kristen Moore, Dong Gong"
date: 2025-09-05
pdf: "https://openreview.net/pdf?id=IyUq9NwOTS"
tags: ["query:continual"]
score: 8.0
evidence: 自激活稀疏混合专家秩自适应学习方法，避免灾难性遗忘和任务干扰
tldr: 本文针对基于LoRA的混合专家（MoE）持续学习中的干扰、冗余和模糊路由问题，提出自激活稀疏混合秩自适应学习（SMoR）。该方法通过细粒度秩级选择激活，减少子空间干扰，并选择性重用跨任务有用组件。实验表明SMoR有效缓解灾难性遗忘，优于现有LoRA-MoE方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LoRA-MoE方法存在专家激活干扰、冗余和路由模糊问题，导致遗忘和低效。
method: 提出自激活稀疏秩级混合专家，每个输入仅激活部分秩，避免完整LoRA子空间干扰。
result: 在多个持续学习基准上遗忘更低，参数效率更高，且任务间干扰显著减少。
conclusion: 秩级稀疏激活是提升持续学习中MoE效率的有效设计。
---

## Abstract
Continual learning (CL) with large pre-trained models is challenged by catastrophic forgetting and task interference. Existing LoRA-based Mixture-of-Experts (MoE) approaches mitigate forgetting by assigning and freezing task-specific adapters, but suffer from interference, redundancy, and ambiguous routing due to coarse adapter-level selection. However, this design introduces three key challenges: 1) *Interference*: Activating full LoRA experts per input leads to subspace interference and prevents selective reuse of useful components across tasks. 2) *Redundancy*: Newly added experts often duplicate or contradict existing knowledge due to unnecessary activation of unrelated ranks and insufficient reuse of relevant ones. 3) *Ambiguity*: Overlapping features across tasks confuse the router, resulting in unstable expert assignments. As more experts accumulate, earlier task routing degrades, accelerating forgetting. We propose ***MoRA***, a **M**ixture-**o**f-**R**ank **A**daptive learning approaches with self-activated and sparse rank activation for CL. Unlike mixing multiple low-rank matrices, MoRA decomposes each rank-r update into r rank-one components, each treated as an independent expert, enabling fine-grained rank-one expert utilization while mitigating interference and redundancy. To avoid ambiguous routing, we propose that each rank-one expert can infer its own relevance via intermediate activations. Coupled with our proposed rank pruning and activation budgets, MoRA adaptively selects a sparse mixture of ranks per input. We validate MoRA on continual learning benchmarks using CLIP and language models, analyzing both in-domain learning and out-of-domain forgetting/generalization during fine-tuning. MoRA shows significant effectiveness on enhancing CL with PTMs, and improving generalization while mitigating forgetting.

---

## 论文详细总结（自动生成）

好的，以下是根据提供的论文摘要和元数据内容生成的结构化总结。由于可获得的完整文本仅包含摘要和少量元数据，部分细节（如具体数据集名称、实验数量、算力等）无法从提供的内容中获取，将在相应位置注明。

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：持续学习（Continual Learning, CL）结合大规模预训练模型时，面临**灾难性遗忘**和**任务间干扰**两大挑战。
- **现有方法不足**：基于LoRA的混合专家（Mixture-of-Experts, MoE）方法通过为每个任务分配并冻结特定的适配器来缓解遗忘，但存在三个关键问题：
  1. **干扰**：激活完整LoRA专家会导致子空间干扰，阻碍跨任务有用组件的选择性重用。
  2. **冗余**：新增的专家因不必要地激活不相关的秩以及未能充分重用相关组件，导致重复或矛盾的知识。
  3. **歧义**：任务间的特征重叠使路由器混淆，造成不稳定的专家分配。随着专家数量累积，早期任务路由退化，加速遗忘。
- **整体含义**：本文旨在通过更细粒度的秩级选择与自激活机制，从根本上解决上述三个问题，从而提升持续学习的效率和泛化能力。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出**MoRA（Mixture-of-Rank Adaptive learning）**，将每个秩为 \( r \) 的LoRA更新分解为 \( r \) 个秩为1的组件，每个组件视为一个独立专家，实现**细粒度秩级专家利用**，同时缓解干扰和冗余。
- **关键技术细节**：
  - **自激活稀疏秩激活**：避免使用独立的模糊路由器，而是让每个秩1专家通过中间**激活值**自行推断其与当前输入的相关性。
  - **秩剪枝与激活预算**：结合提出的秩剪枝策略和激活预算机制，使得MoRA能够为每个输入**自适应地选择稀疏混合的秩**，避免所有专家同时激活。
  - **流程说明**：
    1. 将预训练模型的权重更新矩阵分解为若干秩1子矩阵（专家）。
    2. 输入数据通过中间特征计算每个秩1专家的自激活分数。
    3. 根据激活预算和剪枝策略，仅激活分数最高的部分秩，从而形成稀疏的专家混合。
    4. 被激活的秩1专家进行前向传播，其余专家保持冻结，实现知识选择性保留与重用。
- **与现有方法对比**：不同于混合多个低秩矩阵（如LoRA-MoE），MoRA在更细的**秩级别**进行选择和混合，减少了子空间干扰。

## 3. 实验设计
- **使用的数据集/场景**：论文在**持续学习基准**上使用**CLIP**和**语言模型**进行验证。具体数据集名称和任务类型未在提供文本中明确列出（需查看完整论文）。
- **Benchmark**：典型的持续学习设定（如类增量、任务增量；域增量等），同时分析了**域内学习**和**域外遗忘/泛化**。
- **对比方法**：论文提及与现有的**LoRA-MoE方法**进行对比，但未列出具体基线方法名称（如EWC、SI、DER等持续学习方法以及其它基于适配器的MoE方法）。

## 4. 资源与算力
- **提供文本未明确说明**使用的GPU型号、数量、训练时长等算力信息。需要查看完整论文的实验设置部分。

## 5. 实验数量与充分性
- **从摘要推断**：实验至少覆盖了（1）CLIP上的持续学习，（2）语言模型上的持续学习，以及（3）域内学习和域外遗忘/泛化的分析。
- **充分性评估**：
  - **积极方面**：同时评估了图像模型和语言模型，且关注了域外泛化，提升了实验覆盖范围。
  - **局限性**：由于缺乏具体数据集数量和消融实验细节（如秩剪枝预算的敏感性、专家数量影响等），无法判断实验的**统计显著性**和**对比公平性**。仅凭摘要，无法确认是否进行了充分的消融和超参数调优。

## 6. 主要结论与发现
- MoRA在持续学习基准上**显著降低了遗忘**，同时**提高了参数效率**，任务间干扰明显减少。
- 秩级稀疏激活是一种**高效的设计**，能够在混合专家框架下更好地平衡记忆新知识和保留旧知识。
- MoRA在增强持续学习效果的同时，也**改善了泛化能力**，验证了细粒度选择机制的优势。

## 7. 优点
- **细粒度设计**：将专家粒度从LoRA级别降至秩级别，有效减少子空间干扰和冗余，是MoE方法在持续学习中的重要改进。
- **自激活路由**：抛弃传统易歧义的路由器，让专家根据自身激活值决定是否参与，提升了路由稳定性和可解释性。
- **关注泛化**：不仅关注域内性能，还分析了域外遗忘/泛化，体现了对模型实际应用能力的重视。
- **跨模态验证**：在视觉模型（CLIP）和语言模型上均进行了验证，表明方法具有一定通用性。

## 8. 不足与局限
- **实验细节缺失**：提供的文本中缺乏具体数据集、基线方法、超参数设置、消融实验等关键信息，无法完整评估方法的优越性和鲁棒性。
- **算力与效率分析不足**：未提及训练/推理的计算成本，无法判断秩级稀疏激活在实际大规模部署中的资源和时间消耗。
- **可能的应用限制**：秩级分解可能引入更多专家参数（\(r\)个秩1专家 vs 1个完整LoRA专家），虽然激活是稀疏的，但模型存储和初始化的开销可能增加，对极端资源受限场景未必友好。
- **公平性风险**：仅与LoRA-MoE方法对比，未与标准持续学习方法（如基于回放、正则化、结构的方法）进行比较，可能高估了在特定设定下的性能。
- **未提及代码与可复现性**：文中未声明是否开源代码或提供详细实现细节。

（完）
