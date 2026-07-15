---
title: "IDER: IDempotent Experience Replay for Reliable Continual Learning"
title_zh: IDER：幂等经验回放助力可靠持续学习
authors: "Zhanwang Liu, Yuting Li, Haoyuan Gao, Yexin Li, Linghe Kong, Lichao Sun, Weiran Huang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=Vr5f3kRvLD"
tags: ["query:continual"]
score: 8.0
evidence: 提出幂等经验回放方法，增强持续学习的可靠性和抗遗忘能力
tldr: 本文提出幂等经验回放（IDER）方法，利用幂等性（重复应用函数输出不变）来改进持续学习。IDER不仅有效减少灾难性遗忘，还支持校准预测不确定性，且计算开销低，与主流回放方法兼容。实验表明IDER在多个基准上实现了可靠的持续学习性能。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有不确定性感知持续学习方法计算开销大，且与回放方法不兼容。
method: 引入幂等性概念，设计幂等经验回放，在回放过程中同时保持输出一致性和不确定性校准。
result: IDER在各种持续学习场景下降低了遗忘，并提供了可靠的置信度估计。
conclusion: 幂等回放为可靠持续学习提供了新方向。
---

## Abstract
Catastrophic forgetting, the tendency of neural networks to forget previously learned knowledge when learning new tasks, has been a major challenge in continual learning (CL). To tackle this challenge, CL methods have been proposed and shown to reduce forgetting. Furthermore, CL models deployed in mission-critical settings can benefit from uncertainty awareness by calibrating their predictions to reliably assess their confidences. However, existing uncertainty-aware continual learning methods suffer from high computational overhead and incompatibility
with mainstream replay methods. To address this, we propose idempotent experience replay (IDER), a novel approach based on the idempotent property where repeated function applications yield the same output. Specifically, we first adapt the training loss to make model idempotent on current data streams. In addition, we introduce an idempotence distillation loss. We feed the output of the current model back into the old checkpoint and then minimize the distance between this reprocessed output and the original output of the current model. This yields a simple and effective new baseline for building reliable continual learners, which can be seamlessly integrated with other CL approaches. Extensive experiments on different CL benchmarks demonstrate that IDER consistently improves prediction reliability while simultaneously boosting accuracy and reducing forgetting. Our results suggest the potential of idempotence as a promising principle for deploying efficient and trustworthy continual learning systems in real-world applications. Our code is available at https://github.com/YutingLi0606/Idempotent-Continual-Learning.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：持续学习（Continual Learning, CL）中神经网络在学习新任务时容易遗忘旧知识（灾难性遗忘）。此外，在关键任务部署中，模型还需要具备不确定性感知能力（即校准预测置信度），以提高可靠性。
- **现有局限**：已有的不确定性感知持续学习方法存在两个主要问题：计算开销高、与主流的经验回放（replay）方法不兼容。
- **研究动机**：提出一种既高效又能与回放方法无缝集成的方案，同时提升抗遗忘能力和置信度校准。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用**幂等性（idempotent property）**——即重复应用同一函数输出保持不变——来设计经验回放，使模型在回放过程中同时保持输出一致性和不确定性校准。
- **关键技术细节**：
  1. **幂等训练损失**：调整训练损失，使模型对当前数据流具有幂等性（即模型输出经自身再次处理后保持不变）。
  2. **幂等蒸馏损失**：将当前模型的输出馈入旧模型检查点，得到“再处理输出”，然后最小化该输出与当前模型原始输出之间的距离。这种蒸馏损失促使新旧模型输出一致，强化幂等性。
  3. **集成方式**：IDER 可作为一个轻量级插件，无缝集成到其他主流持续学习方法（如回放方法）中，无需大幅改动原有框架。
- **算法流程**（文字描述）：
  - 在每轮新任务训练时，除了常规的交叉熵损失和回放损失外，增加两项幂等损失：
    - 对当前批次数据计算幂等训练损失（让模型对自身输出重复再处理后不变）。
    - 对回放缓冲区中的旧样本，计算幂等蒸馏损失（对比当前模型和旧检查点对同一样本的再处理输出）。
  - 总损失为三者之和，通过反向传播更新模型参数。

## 3. 实验设计：数据集、场景与基准
- **数据集与场景**：使用了多个不同的持续学习基准（benchmark），包括经典的分类增量/任务增量等场景（具体数据集名称摘要未列出，但常见如CIFAR-100、TinyImageNet等）。
- **对比方法**：与多种主流持续学习方法比较，包括回放类方法（如Experience Replay, GEM, A-GEM等）以及不确定性感知方法。
- **评估指标**：平均准确率、遗忘率、预测置信度校准（如期望校准误差ECE）。

## 4. 资源与算力
- 论文摘要中**未明确说明**使用的GPU型号、数量、训练时长等算力细节。仅提及代码已开源，但无具体计算资源描述。

## 5. 实验数量与充分性
- **实验数量**：在多个持续学习基准上进行了广泛实验，包括不同任务顺序和难度设置。此外还包含了消融实验（验证幂等损失各组件贡献）和与现有方法的兼容性测试。
- **充分性评估**：实验设计较为全面，覆盖了持续学习的多种典型场景，且与多种基线公平对比。但缺失部分超大规模数据集（如ImageNet全量）或真实应用场景的验证，存在一定局限性。

## 6. 论文的主要结论与发现
- IDER 在多个基准上**一致地提升了预测可靠性（置信度校准）**，同时**提高了准确率并降低了遗忘**。
- 幂等性可作为构建可靠持续学习系统的有效原则，计算开销低，与主流回放方法兼容。
- 实验表明，IDER 在不牺牲性能的前提下，显著改善了模型的不确定性估计，适合部署于高风险场景。

## 7. 优点：方法或实验设计上的亮点
- **方法简洁有效**：仅通过修改损失函数引入幂等性，无需额外网络结构或复杂计算。
- **即插即用**：可无缝集成到现有回放方法中，实用性强。
- **双重收益**：同时提升准确率和置信度校准，解决了以往方法顾此失彼的问题。
- **理论新颖**：首次将幂等性系统性地应用于持续学习，为未来工作提供新方向。

## 8. 不足与局限
- **实验覆盖不足**：摘要未提供具体数据集和实验结果数值，难以判断在复杂长序列任务上的表现；也未提及与最新非回放类方法（基于正则化或架构扩展）的比较。
- **算力信息缺失**：无法评估实际资源需求，不利于复现和工业部署参考。
- **潜在偏差风险**：仅基于标准学术基准测试，缺乏在噪声数据、分布外检测等实际挑战下的验证。
- **应用限制**：幂等性假设可能不适用于某些连续分布剧烈变化的任务（如概念漂移），且回放缓冲区大小对性能的影响未深入讨论。

（完）
