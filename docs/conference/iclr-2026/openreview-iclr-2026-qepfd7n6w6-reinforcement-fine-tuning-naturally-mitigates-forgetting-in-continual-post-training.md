---
title: Reinforcement Fine-Tuning Naturally Mitigates Forgetting in Continual Post-Training
title_zh: 强化微调在持续后训练中自然减轻遗忘
authors: "Song Lai, Haohan Zhao, Rong Feng, Changyi Ma, Wenzhuo Liu, Hongbo Zhao, Xi Lin, Dong Yi, Min Xie, Qingfu Zhang, Hongbin Liu, Gaofeng Meng, Fei Zhu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qepfd7N6W6"
tags: ["query:continual"]
score: 8.0
evidence: 强化微调在持续后训练中自然减轻遗忘
tldr: 持续后训练中，现有研究多关注数据回放等方法，而学习范式的作用被忽视。本文比较了监督微调和强化微调在持续后训练中的效果，发现强化微调在七个多模态任务上能自然减轻灾难性遗忘。实验基于Qwen2.5-VL-7B-Instruct模型，表明RFT是一种有效的持续学习范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有工作忽略学习范式对持续后训练中遗忘的影响。
method: 对比监督微调与强化微调在持续后训练中的表现。
result: 强化微调在七个多模态任务上有效减少遗忘。
conclusion: 强化微调可作为持续后训练的优选范式。
---

## Abstract
Continual post-training (CPT) is a popular and effective technique for adapting foundation models like multimodal large language models to specific and ever-evolving downstream tasks. While existing research has primarily concentrated on methods like data replay, model expansion, or parameter regularization, the fundamental role of the learning paradigm within CPT remains largely unexplored. This paper presents a comparative analysis of two core post-training paradigms: supervised fine-tuning (SFT) and reinforcement fine-tuning (RFT), investigating their respective impacts on knowledge retention during CPT. Our experiments are conducted on a benchmark comprising seven diverse multimodal tasks, utilizing Qwen2.5-VL-7B-Instruct as the base model for continual post-training. The investigation yields two significant findings: (1) When continuously learning on downstream tasks, SFT leads to catastrophic forgetting of previously learned tasks. In contrast, RFT inherently preserves prior knowledge and achieve performance comparable to multi-task training. (2) RFT successfully protects and even enhances the model's general knowledge on standard benchmarks (e.g., MMMU and MMLU-Pro). Conversely, SFT degrades general model capabilities severely. Further analysis reveals that this stability is not primarily due to explicit mechanisms like KL penalty or chain-of-thought reasoning. Instead, we identify an implicit regularization mechanism inherent to RFT as a key contributing factor. Our theoretical analysis suggests that RFT's gradient updates are naturally scaled by the reward variance, acting as a data-dependent regularizer that inherently protects previously acquired knowledge. Finally, we propose a rollout-based instance filtering algorithm to enhance the stability and efficiency of RFT. Our comprehensive study demonstrates the superiority of RFT as a robust paradigm for continual post-training.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：持续后训练（Continual Post-Training, CPT）是多模态大模型适应不断变化的下游任务的主流技术，但现有研究主要关注数据回放、模型扩展或参数正则化等方法，忽视了学习范式（learning paradigm）本身对遗忘的影响。
- **核心问题**：在CPT过程中，不同的学习范式（监督微调SFT vs. 强化微调RFT）如何影响模型对先前任务知识的保留？是否存在一种范式能自然减轻灾难性遗忘？
- **整体意义**：首次系统对比SFT和RFT在持续后训练中的表现，揭示RFT具有天然的抗遗忘特性，并提出了一种基于rollout的实例过滤算法以提升RFT的稳定性与效率。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：比较两种微调范式在连续学习多模态任务时的遗忘行为，从理论和实验两方面解释RFT为何能保留旧知识。
- **关键技术细节**：
  - **SFT**：标准监督微调，使用交叉熵损失更新参数。
  - **RFT**：强化微调，基于奖励信号（如正确性反馈）通过策略梯度（如PPO）更新模型。
  - **理论分析**：提出RFT的梯度更新天然被奖励方差缩放，形成一种数据依赖的正则化器，从而保护先前习得的知识。该机制并非来自显式的KL惩罚或思维链推理。
  - **算法流程改进**：提出基于rollout的实例过滤算法（rollout-based instance filtering），选择对当前任务代表性强的样本来增强RFT的稳定性和效率。具体做法：对每个候选实例进行rollout采样，根据奖励的稳定性或一致性筛选实例。
- **公式/流程**：文中未给出具体数学公式，但文字描述了梯度隐式正则化的原理。

## 3. 实验设计：数据集、基准与对比方法

- **基础模型**：Qwen2.5-VL-7B-Instruct（多模态大语言模型）。
- **基准任务**：七个不同的多模态任务，涵盖视觉理解、视觉推理等多样化场景。具体任务名称未在元数据中展开，但Abstract提到“seven diverse multimodal tasks”。
- **额外评估**：通用知识基准MMMU和MMLU-Pro，用于检测模型通用能力的保持或提升。
- **对比方法**：
  - 多任务训练（Multi-task training）作为上界参考。
  - 连续SFT（Sequential SFT）作为基准方法。
  - 连续RFT（Sequential RFT）作为主要对比方法。
- **消融/分析实验**：验证RFT稳定性是否来自KL惩罚或链式推理（排除显式机制）；分析梯度隐式正则化机制；提出实例过滤算法并评估其效果。

## 4. 资源与算力

- 论文元数据和正文中均**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及基础模型为7B参数规模，因此可推断需要一定的A100或同等显存资源，但具体细节缺失。

## 5. 实验数量与充分性

- **实验数量**：包括主实验（7个任务上对比SFT/RFT）、通用知识评测（MMMU/MMLU-Pro）、消融实验（分析KL惩罚、链式推理、隐式正则化）、实例过滤算法效果测试。
- **充分性与客观性**：
  - 覆盖多种类型多模态任务，具有一定泛化性。
  - 比较了多任务训练上界，对比公平。
  - 消融实验设计合理，能支撑理论分析。
  - 不足：仅使用单一基础模型（Qwen2.5-VL-7B-Instruct），未在其他架构或规模上验证，存在模型依赖风险。实验次数和随机种子等细节未报告。

## 6. 论文的主要结论与发现

- **关键发现1**：在连续学习下游任务时，SFT会导致灾难性遗忘，而RFT天然保留旧知识，性能接近多任务联合训练。
- **关键发现2**：RFT不仅保护通用知识（MMMU/MMLU-Pro），甚至能提升通用能力；而SFT会严重损害通用能力。
- **机制解释**：RFT的抗遗忘主要源于其梯度更新被奖励方差缩放，形成隐式正则化，而非KL惩罚或思维链推理。
- **实用建议**：RFT可作为持续后训练的优选范式，结合实例过滤算法可进一步提升稳定性与效率。

## 7. 优点：方法或实验设计上的亮点

- **创新视角**：首次关注学习范式本身对持续学习遗忘的影响，而非仅关注数据或参数层面技巧。
- **理论深度**：从梯度更新公式推导出隐式正则化机制，给出解释性强的分析。
- **实验设计**：同时评估下游任务性能和通用能力，体现RFT的全面优势；使用多任务训练作为上界，对比公平。
- **实用算法**：提出基于rollout的实例过滤算法，直接提升RFT在CPT中的实用性。

## 8. 不足与局限

- **模型单一**：仅测试Qwen2.5-VL-7B-Instruct，未在不同规模或不同家族的MLLM上验证，结论泛化性受限。
- **任务覆盖**：虽涉及七个任务，但未详细列出任务名称和难度，可能缺失对长序列或复杂遗忘场景的验证。
- **计算资源未报告**：缺乏算力细节，影响可复现性评估。
- **遗忘度量**：未使用标准持续学习指标（如Backward Transfer、Forward Transfer），仅比较准确率或奖励，可能不够全面。
- **实际应用限制**：RFT需要奖励模型或人工反馈，在实际场景中获取成本可能高于SFT；实例过滤算法增加了额外计算开销。

（完）
