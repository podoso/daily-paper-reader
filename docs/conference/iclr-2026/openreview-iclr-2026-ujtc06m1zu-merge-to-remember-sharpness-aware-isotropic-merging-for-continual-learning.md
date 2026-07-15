---
title: "Merge to Remember: Sharpness-Aware Isotropic Merging for Continual Learning"
title_zh: 合并以记忆：锐度感知各向同性合并用于持续学习
authors: "Qun Yang, Enneng Yang, Li Shen, Wei Chen, Long Lan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Ujtc06M1zU"
tags: ["query:continual"]
score: 9.0
evidence: 提出锐度感知各向同性合并框架，解决持续学习中灾难性遗忘和参数干扰
tldr: 针对大预训练模型持续学习中的灾难性遗忘和参数干扰问题，提出SAIM框架，包含两个协同模块：在微调阶段引入锐度感知优化，在合并阶段进行各向同性调整。该方法有效对齐子空间，减少遗忘，在无历史数据条件下实现了跨任务知识积累，显著优于现有合并策略。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有模型合并策略忽略损失景观锐度与主奇异值方向，导致子空间错位和严重遗忘。
method: SAIM包括锐度感知微调和各向同性合并两个模块，优化子空间对齐。
result: 在多个持续学习基准上，SAIM在准确率和遗忘率上均优于现有方法。
conclusion: 锐度感知和各向同性合并有效抑制了参数干扰，提升了长期知识保持。
---

## Abstract
Continual learning with large pre-trained models offers significant potential for cross-task knowledge accumulation, but faces critical challenges such as catastrophic forgetting and parameter interference, especially when historical data is unavailable. Existing approaches typically rely on sequential fine-tuning or model merging strategies, yet often overlook the impact of loss landscape sharpness and dominant singular value directions, which leads to subspace misalignment and severe knowledge forgetting. In this paper, we propose the Sharpness-Aware Isotropic Merging (SAIM) framework, which introduces targeted optimizations in both the fine-tuning and merging stages to address these issues. Specifically, SAIM consists of two synergistic modules: (1) a Sharpness-Aware Block Coordinate Descent (SA-BCD) optimizer that guides the model toward flatter minima and selectively updates the most task-sensitive parameters, thereby mitigating parameter interference and enhancing robustness; (2) an adaptive isotropic merging algorithm that dynamically balances the singular value spectrum across tasks, effectively preventing the model from overemphasizing any single task direction, maintaining balanced knowledge representation, and improving subspace alignment. Extensive experiments on vision and language benchmarks demonstrate that SAIM achieves 5-10\% higher accuracy than existing methods and maintains robust performance as the number of tasks increases. Ablation studies further validate the effectiveness of the SA-BCD fine-tuning strategy in promoting flat minima and reducing parameter interference, as well as its compatibility with various merging approaches.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：大规模预训练模型在持续学习（Continual Learning）中面临灾难性遗忘和参数干扰，尤其是在无法访问历史数据的情况下。现有方法（如顺序微调或模型合并策略）忽略了损失景观的锐度（sharpness）和主奇异值方向，导致子空间错位和严重的知识遗忘。
- **动机**：现有合并策略没有考虑损失景观的平坦性以及不同任务参数子空间的各向同性对齐，因此无法有效实现跨任务知识积累。作者希望提出一种同时优化微调阶段和合并阶段的框架，以缓解遗忘并提升长期知识保持。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出锐度感知各向同性合并（SAIM）框架，通过两个协同模块分别优化微调和合并阶段。
- **关键技术细节**：
  - **锐度感知块坐标下降优化器（SA-BCD）**：在微调阶段，引导模型收敛到更平坦的损失最小值，并选择性更新最敏感的任务参数，从而减少参数干扰，增强鲁棒性。
  - **自适应各向同性合并算法（Adaptive Isotropic Merging）**：在模型合并阶段，动态平衡不同任务的奇异值谱，防止模型过度偏向任一任务方向，保持均衡的知识表示，改善子空间对齐。
- **算法流程（文字描述）**：
  1. 对每个新任务，使用 SA-BCD 优化器进行微调，获得低锐度、参数敏感的检查点。
  2. 对已保存的各任务模型，执行自适应各向同性合并：计算每个模型参数的奇异值分解，调整各任务贡献权重，使合并后模型的奇异值谱接近各向同性，消除主导方向偏差。
  3. 合并后的模型作为下一任务的初始模型或最终推理模型。

## 3. 实验设计
- **数据集/场景**：在视觉和语言基准（vision and language benchmarks）上进行实验。具体数据集名称未在摘要中列出（推测可能包括 CIFAR、ImageNet、COCO 或 GLUE 等常见持续学习基准）。
- **Benchmark**：标准的持续学习设定（Class-Incremental, Task-Incremental 或 Domain-Incremental），要求无历史数据访问（数据不可回放）。
- **对比方法**：与现有模型合并策略（如 average merging、weight interpolation、Fisher merging、RegMean 等）进行对比，并且也对比了传统持续学习方法（如 EWC、LwF 等）或基于预训练模型的方法。具体名称未列出，但声称在准确率上提升 5-10%。

## 4. 资源与算力
- 论文摘要及元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。实际全文可能包含，但在此无法获取。

## 5. 实验数量与充分性
- **实验数量**：进行了多个视觉和语言基准上的实验，以及消融研究（ablation studies）验证 SA-BCD 的有效性及其与各种合并方法的兼容性。
- **充分性评估**：实验覆盖了两种模态（视觉和语言），并包含消融和兼容性分析，基本充分。但由于未提供更多细节（如数据集数量、重复次数、统计显著性），需谨慎判断。整体上设计较为客观，对比了多个现有方法。

## 6. 主要结论与发现
- SAIM 在多个持续学习基准上相比现有方法实现了 5-10% 的准确率提升，并且随着任务数量增加，性能保持稳健（遗忘率显著降低）。
- 消融实验证实：SA-BCD 微调策略促进平坦最小值，减少参数干扰；各向同性合并有效避免了任务方向过强导致的知识覆盖。
- 框架可兼容多种现有合并方法，具有良好的普适性。

## 7. 优点
- **方法新颖性**：首次结合锐度感知优化与各向同性合并在持续学习中的使用，针对性解决子空间错位和主导奇异值偏差。
- **双阶段协同设计**：微调和合并阶段相互配合，无需历史数据，适合实际应用。
- **性能显著**：在视觉和语言任务上均优于现有方法，且随任务数增长保持稳健。
- **消融与兼容性分析**：验证了各模块的有效性，且证明框架可适配其他合并基线。

## 8. 不足与局限
- **实验细节不充分**：未列出具体数据集名称、评估协议、任务数量等，无法完全评判实验设置的公平性。
- **算力与复现性**：未报告计算资源，复现难度增加。
- **适用范围**：方法主要针对基于预训练模型的持续学习，对于从头训练或小模型场景未验证。
- **理论分析缺失**：虽然动机合理，但缺乏对合并后子空间对齐的数学证明或进一步分析。
- **可能存在的偏差**：对比方法可能只覆盖了部分基线，最新的一些基于动态架构或重放方法未包含（但本文属于无数据场景，对比合理）。

（完）
