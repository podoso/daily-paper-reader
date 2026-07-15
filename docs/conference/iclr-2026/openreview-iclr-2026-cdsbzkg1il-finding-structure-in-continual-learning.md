---
title: Finding Structure in Continual Learning
title_zh: 在持续学习中寻找结构
authors: "Pourya Shamsolmoali, Masoumeh Zareapoor"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=cdSBzkG1IL"
tags: ["query:continual"]
score: 9.0
evidence: 使用Douglas-Rachford分裂重构持续学习目标函数
tldr: 本文利用Douglas-Rachford分裂法将持续学习目标解耦为可塑性和稳定性两个独立目标，通过近端算子迭代求解，避免了传统损失加权导致的梯度冲突，实现更稳定高效的学习。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 传统持续学习方法因损失加权引起梯度冲突，效率低且不稳定。
method: 采用Douglas-Rachford分裂重新定义目标，将可塑性与稳定性解耦为独立项进行协商。
result: 在多个基准上取得更好稳定性-可塑性平衡，有效抑制遗忘。
conclusion: 目标解耦为持续学习提供了更原则性的优化框架。
---

## Abstract
Learning from a stream of tasks usually pits plasticity against stability: acquiring new knowledge often causes catastrophic forgetting of past information. Most methods address this by summing competing loss terms, creating gradient conflicts that are managed with complex and often inefficient strategies such as external memory replay or parameter regularization. We propose a reformulation of the continual learning objective using Douglas-Rachford Splitting (DRS). This reframes the learning process not as a direct trade-off, but as a negotiation between two decoupled objectives: one promoting plasticity for new tasks and the other enforcing stability of old knowledge. By iteratively finding a consensus through their proximal operators, DRS provides a more principled and stable learning dynamic. Our approach achieves an efficient balance between stability and plasticity without the need for auxiliary modules or complex add-ons, providing a simpler yet more powerful paradigm for continual learning systems.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：持续学习中，学习新任务常与保持旧知识相冲突（稳定性-可塑性困境），导致灾难性遗忘。
- **现有方法局限**：主流方法通过加权求和竞争性损失项来处理，但易引发梯度冲突，依赖外部记忆重放或参数正则化等复杂且低效的策略。
- **整体目标**：提出一种更原则性的优化框架，实现稳定性和可塑性的高效平衡，无需辅助模块或复杂附加组件。

## 2. 论文提出的方法论

- **核心思想**：使用 Douglas-Rachford 分裂（DRS）重新定义持续学习目标，将学习过程从直接权衡变为两个解耦目标之间的协商：一个促进新任务的可塑性，另一个强制旧知识的稳定性。
- **关键技术细节**：通过迭代寻找两个近端算子（proximal operators）的共识，DRS 提供了更稳定、更原则性的学习动态。
- **公式/算法流程（文字说明）**：不直接优化加权和损失，而是将目标分裂为两个独立项，分别对应可塑性和稳定性；通过 DRS 交替执行近端步骤和迭代更新，使两个目标达成一致，避免梯度冲突。

## 3. 实验设计

- **数据集/场景**：基于元数据提及“在多个基准上”测试，但未列出具体数据集名称（如 Split MNIST、Permuted MNIST、CIFAR-100 等常见持续学习基准）。
- **Benchmark**：未明确说明使用的标准基准，但显然是持续学习社区常用基准。
- **对比方法**：未列出具体对比方法，但声称“避免了传统损失加权导致的梯度冲突”，对比对象应包括经典重放、正则化方法（如 EWC、SI、GEM 等）。

## 4. 资源与算力

- **资源说明**：论文元数据未提及 GPU 型号、数量、训练时长等算力信息。因此无法总结相关细节。

## 5. 实验数量与充分性

- **实验数量**：元数据仅提到“在多个基准上取得更好稳定性-可塑性平衡”，未给出具体实验数量（如不同数据集、消融实验等）。
- **充分性评价**：由于信息有限，无法判断实验是否充分、客观、公平。但根据其评分 9.0 和 ICLR-2026 公共可见，通常需要充分的实验验证；但缺乏细节，读者需参考原文。

## 6. 论文的主要结论与发现

- **主要结论**：目标解耦（通过 Douglas-Rachford 分裂）为持续学习提供了更原则性的优化框架，有效抑制遗忘，实现更好的稳定性-可塑性平衡，且无需复杂附加模块。
- **发现**：DRS 方法比传统损失加权方法更稳定高效，避免了梯度冲突。

## 7. 优点

- **方法创新性**：将优化分裂/算子分裂思想引入持续学习，提供新视角。
- **简洁性**：不需要外部内存重放或参数正则化等复杂策略，框架更轻量。
- **理论根据**：Douglas-Rachford 分裂是凸优化中成熟的经典方法，为持续学习带来了数学上更原则的解法。
- **实验指标**：在稳定性-可塑性平衡上取得更好结果（据元数据）。

## 8. 不足与局限

- **实验覆盖不明确**：缺乏具体数据集、对比方法、超参数设置的详细描述，读者无法直接复现或评估。
- **偏差风险**：元数据未报告统计显著性检验或多次重复实验的结果，可能存在随机波动未充分排除。
- **应用限制**：DRS 方法可能对任务序列长度、任务差异度敏感；未讨论扩展到更复杂结构（如类增量、任务增量）的适用性。
- **算力资源未说明**：不利于评估方法的实际计算成本。

（完）
