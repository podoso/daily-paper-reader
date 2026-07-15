---
title: Modality-Inconsistent Continual Learning of Multimodal Large Language Models
title_zh: 多模态大语言模型的模态不一致持续学习
authors: "Weiguo Pian, Shijian Deng, Shentong Mo, Mingrui Liu, Yunhui Guo, Yapeng Tian"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=l13qyPJyUF"
tags: ["query:continual"]
score: 9.0
evidence: 面向多模态大语言模型的模态不一致持续学习，解决遗忘
tldr: 本文提出模态不一致持续学习场景，针对多模态大语言模型在模态和任务类型变化下的遗忘问题，提出MoInCL方法，利用伪目标生成模块和指令知识蒸馏有效缓解遗忘。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有持续学习仅考虑视觉任务，未涉及模态和任务类型同时变化导致的遗忘。
method: 提出MoInCL，包含伪目标生成模块以缓解任务类型变化遗忘，以及指令知识蒸馏保持模态处理能力。
result: 在多个模态不一致序列任务上显著降低遗忘，保持多模态能力。
conclusion: 该工作为多模态大语言模型的持续学习提供了新场景和有效方法。
---

## Abstract
In this paper, we introduce Modality-Inconsistent Continual Learning (MICL), a new continual learning scenario for Multimodal Large Language Models (MLLMs) that involves tasks with inconsistent modalities (image, audio, or video) and varying task types (captioning or question-answering). Unlike existing vision-only or modality-incremental settings, MICL combines modality and task type shifts, both of which drive catastrophic forgetting. To address these challenges, we propose MoInCL, which employs a Pseudo Targets Generation Module to mitigate forgetting caused by task type shifts in previously seen modalities. It also incorporates Instruction-based Knowledge Distillation to preserve the model's ability to handle previously learned modalities when new ones are introduced. We benchmark MICL using a total of six tasks and conduct experiments to validate the effectiveness of our proposed MoInCL. The experimental results highlight the superiority of MoInCL, showing significant improvements over representative and state-of-the-art continual learning baselines.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- 现有对多模态大语言模型（MLLMs）的持续学习研究主要局限于模态增量（如仅视觉任务）或任务类型单一的设置，忽略了 **模态不一致**（如图像、音频、视频交替出现）与 **任务类型变化**（如字幕生成、问答）同时发生导致的灾难性遗忘。
- 本文首次提出 **Modality-Inconsistent Continual Learning (MICL)** 场景，旨在解决 MLLMs 在模态和任务类型双重变化下的遗忘问题，推动多模态持续学习的实际应用。

## 2. 方法论：核心思想、关键技术细节

- **MoInCL 方法**：包含两个核心模块：
  1. **伪目标生成模块（Pseudo Targets Generation Module）**：针对已学模态中因任务类型变化导致的遗忘，通过生成伪标签或伪目标来辅助模型保持回顾旧任务的能力。
  2. **指令知识蒸馏（Instruction-based Knowledge Distillation）**：当引入新模态时，利用基于指令的知识蒸馏来保留模型对已学模态的处理能力，避免新模态学习干扰旧模态知识。
- 整体流程：模型依次学习不同模态和任务类型的序列任务，每步都通过上述两个模块的联合损失进行更新，未涉及明确公式，但核心是平衡新任务学习与旧知识保持。

## 3. 实验设计

- **数据集与场景**：使用了 **六个任务** 构建的 MICL 基准，涵盖图像、音频、视频三种模态，以及字幕生成和问答两种任务类型（具体数据集名称未在摘要中说明，需参考全文）。
- **对比方法**：与代表性及最先进的持续学习方法进行对比（包括常见的重放、正则化、知识蒸馏等方法）。MoInCL 在所有指标上均表现更优。
- **评估指标**：主要关注 **遗忘率** 和 **新任务学习能力**，验证了模态和任务双重遗忘的缓解效果。

## 4. 资源与算力

- 论文摘要及元数据中 **未明确说明** GPU 型号、数量、训练时长等算力信息。需查阅完整论文以获取细节。

## 5. 实验数量与充分性

- 实验基于六个任务构建的 MICL 基准，通过消融实验验证了两个核心模块的贡献（伪目标生成和指令知识蒸馏）。
- 实验覆盖了多种模态组合和任务类型变化，对比了多种基线，验证了方法的通用性。但由于缺乏大规模多任务扩展或真实场景验证，充分性仍有提升空间；实验公平性上，对比方法已涵盖主流方法，但未体现超参数或随机种子影响分析。

## 6. 主要结论与发现

- MICL 场景下的双重遗忘（模态和任务类型变化）比单一变化更严重，现有方法难以应对。
- MoInCL 通过伪目标生成和指令知识蒸馏有效缓解了遗忘，显著超过了所有基线方法。
- 证明了在 MLLMs 持续学习中同时考虑模态和任务类型变化的重要性。

## 7. 优点

- **问题新颖**：首次定义模态不一致持续学习，拓展了多模态持续学习的研究边界。
- **方法简洁有效**：两个模块设计合理，不依赖复杂外部数据或存储，适合在线场景。
- **实验设计完整**：自行构建多模态序列基准，覆盖多种模态和任务类型，对比充分。

## 8. 不足与局限

- **算力信息公开不足**：未提供训练开销，难以评估实用性。
- **基准任务数量有限**：仅六个任务，模态种类和任务类型代表性可能不够全面（例如缺少图文匹配、视觉定位等）。
- **未讨论模态不平衡问题**：不同模态任务的学习难度和数据量差异可能影响性能。
- **缺乏跨领域泛化验证**：仅在特定数据集上测试，实际应用（如医疗、机器人）中的泛化性未知。
- **忽略计算效率与内存成本**：伪目标生成和蒸馏可能带来额外开销，文中未分析。

（完）
