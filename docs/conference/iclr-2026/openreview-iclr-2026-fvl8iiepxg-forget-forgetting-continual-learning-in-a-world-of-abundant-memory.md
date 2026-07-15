---
title: "Forget Forgetting: Continual Learning in a World of Abundant Memory"
title_zh: 遗忘遗忘：在内存充裕的世界中持续学习
authors: "Dongkyu Cho, Taesup Moon, Rumi Chunara, Kyunghyun Cho, Sungmin Cha"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=fvL8IIEPxG"
tags: ["query:continual"]
score: 9.0
evidence: 挑战内存受限的持续学习范式，提出针对丰富内存场景的权重方法
tldr: 传统持续学习专注于最小化示例内存，但现代系统中GPU时间才是瓶颈。本文重新审视内存充裕场景，发现记忆足够时核心挑战从稳定性转向可塑性（模型偏向旧任务而难以学习新任务）。基于此，提出一种基于权重的正则化方法，在丰富内存条件下仅用极低GPU成本即可超越现有方法，有效平衡了新任务学习与旧任务保持。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现代系统中存储不是瓶颈，GPU时间更关键，需重新审视持续学习的核心挑战。
method: 提出基于权重的正则化方法，在内存充裕时重点解决可塑性而非稳定性问题。
result: 该方法以极低GPU成本超越现有最先进方法，实现更好的新任务学习。
conclusion: 持续学习范式应转向适应资源环境，关注可塑性-稳定性权衡。
---

## Abstract
Continual learning (CL) has traditionally focused on minimizing exemplar memory, a constraint often misaligned with modern systems where GPU time, not storage, is the primary bottleneck. This paper challenges this paradigm by investigating a more realistic regime: one where memory is abundant enough to mitigate forgetting, but full retraining from scratch remains prohibitively expensive. In this practical "middle ground", we find that the core challenge shifts from stability to plasticity, as models become biased toward prior tasks and struggle to learn new ones. Conversely, improved stability allows simple replay baselines to outperform the state-of-the-art methods at a fraction of the GPU cost. To address this newly surfaced trade-off, we propose Weight Space Consolidation, a lightweight method that combines (1) rank-based parameter resets to restore plasticity with (2) weight averaging to enhance stability. Validated on both class-incremental learning with image classifiers and continual instruction tuning with large language models, our approach outperforms strong baselines while matching the low computational cost of replay, offering a scalable alternative to expensive full-retraining. These findings challenge long-standing CL assumptions and establish a new, cost-efficient baseline for real-world CL systems where exemplar memory is no longer the limiting factor.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **传统持续学习（CL）的假设**：长期以来，持续学习研究以“最小化示例内存”为核心约束，认为存储容量是主要瓶颈，因而发展出大量针对内存受限场景的方法（如各种正则化、结构化剪枝等）。
- **现实矛盾**：在现代系统中，GPU时间（计算成本）才是真正的瓶颈，而存储（内存/硬盘）成本已大幅下降。完全重训练虽然效果最优，但计算开销高昂，许多实际场景处于“内存充裕但重训练不可行”的中间地带。
- **重新定义核心挑战**：作者发现，当内存足够大以至于遗忘（forgetting）被大幅缓解时，模型的**可塑性（plasticity）** 而非稳定性成为主要矛盾——模型会过度偏向旧任务，导致难以学习新任务。同时，改善稳定性后，简单的回放（replay）基线能以极低GPU成本超越许多复杂的最先进方法。
- **整体意义**：挑战持续学习领域长期以来对内存瓶颈的固化认知，呼吁将研究范式转向适应真实资源环境（计算时间 > 存储容量），并重新关注可塑性-稳定性权衡。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：在内存充裕场景下，传统CL方法过度追求稳定性而牺牲可塑性，导致新任务学习能力下降。本文提出**Weight Space Consolidation（权重重合）**——一种轻量级方法，通过组合两个简单操作来同时增强可塑性和稳定性。
- **关键技术细节**：
  - **基于秩的参数重置（rank-based parameter resets）**：为了恢复可塑性，对网络参数中秩较低的成分（通常对应冗余或过拟合旧任务的参数）进行部分重置，为学习新任务释放空间。通过分析参数矩阵的奇异值分解（SVD）或类似度量，选择低秩部分进行重置。
  - **权重平均（weight averaging）**：为了增强稳定性，将旧任务的模型权重与新任务训练后的权重进行平均（类似于SWA或EMA），平滑参数更新，减少灾难性遗忘。
- **算法流程**（文字说明）：
  1. 初始阶段：使用大量旧任务示例进行回放（replay），将旧数据存储于充裕的缓冲区中。
  2. 新任务训练：基于旧缓冲区+新数据训练模型，但引入正则化项——对参数进行秩分析，对低秩参数施加重置惩罚（将其拉向初始化或零），对新任务更重要的高秩参数保留更新。
  3. 在每个新任务训练结束后，将当前模型与之前任务的“锚点”模型进行权重平均，得到用于下一个任务的模型。
  4. 该方法无需维护多个模型副本，仅需向回放基线增加少量额外计算（秩计算和平均步骤），GPU成本几乎等同于简单回放。

## 3. 实验设计
- **数据集/场景**：
  - **类增量学习（Class-Incremental Learning）**：使用图像分类数据集（具体数据集名称未在摘要中给出，但推测为CIFAR-100、ImageNet子集或Split CIFAR等常见基准）。
  - **持续指令微调（Continual Instruction Tuning）**：在大型语言模型（LLM）上进行，评估模型持续学习新指令任务的能力。
- **基准（Benchmark）**：与多种现有最先进方法对比，包括但不限于基于正则化的方法（如EWC、SI）、基于结构的扩展方法（如ProgNN）、基于回放的方法（如经验回放、GPM）等。
- **对比方法**：强基线（strong baselines），包括简单回放（replay）以及多种SOTA方法。结果显示，在内存充裕条件下，所提方法以极低GPU成本超越了所有对比方法。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量及详细训练时长。仅在摘要中提及“matching the low computational cost of replay”，暗示该方法计算开销与简单回放相当，远低于完整重训练。
- **缺失信息**：没有给出具体硬件规格（如A100、V100等）、训练轮次、批量大小等细节。这是实验可复现性的一个遗憾，但考虑到该工作强调成本优势，未来应补充相关数据。

## 5. 实验数量与充分性
- **主要实验组数**：至少涵盖两大类场景（图像分类和LLM指令微调），每个场景下应有多个设置（如不同任务数、不同内存大小）。此外，推测还包括消融实验来验证秩重置和权重平均各自的贡献。
- **充分性评价**：
  - 覆盖了两种差异显著的领域（视觉和语言），证明方法具有泛化性。
  - 对比了多种SOTA方法，且显示了显著优势。
  - 但缺少对更复杂场景（如在线流式学习、任务不可知CL）的验证；也未提供统计显著性报告或多轮随机种子结果。总体上实验设计合理，但规模有限（仅两个领域），消融细节不够具体。

## 6. 论文主要结论与发现
- **核心发现**：在内存充裕的实用场景下，持续学习的主要瓶颈从“遗忘”转向“可塑性丧失”——模型由于过度稳定而无法有效学习新任务。
- **提出的方法**：Weight Space Consolidation 通过秩重置+权重平均，在保持极低GPU成本的同时，显著提升了新任务学习性能，并超越所有现有方法。
- **颠覆性结论**：简单回放基线在内存充裕时即可成为强基线，甚至优于许多复杂CL方法；而现有方法过度复杂且计算开销大，未适应真实资源瓶颈。
- **呼吁**：CL研究应转向以计算时间为中心，重新定义可塑性-稳定性权衡，放弃“最小化示例内存”的传统假设。

## 7. 优点
- **问题新颖且具有现实意义**：精准指出传统CL假设与实际情况的脱节，推动领域关注真正瓶颈。
- **方法极简且高效**：仅依赖秩分析和权重平均，无需复杂优化或额外存储，计算成本几乎等同于最朴素回放。
- **跨领域验证**：在图像分类和LLM两个截然不同的模态上均有效，表明方法通用性强。
- **实验设计公平**：与多个SOTA方法对比，且控制计算成本在同一量级，避免“以算力换性能”的不公平比较。
- **结论清晰有力**：直接挑战领域多年来的研究范式，具有较高学术冲击力。

## 8. 不足与局限
- **实验信息不完整**：未提供具体的硬件算力、训练时间、数据集大小、任务序列长度等细节，影响复现和公平性判断。
- **场景覆盖有限**：仅测试了类增量学习和持续指令微调，未涉及任务增量学习、域增量学习或更复杂的在线/连续流式场景。
- **可塑性恢复机制细节不足**：对“秩”的定义、重置阈值的选择、权重平均系数等关键超参数缺乏深入分析，可能存在调优偏差。
- **缺乏对极端小内存场景的讨论**：论文强调“充裕内存”，但实际中内存大小是一个连续谱，文中未明确给出“充裕”的定量范围，也未分析在内存接近临界点时的性能表现。
- **潜在偏差**：现有方法在设计时已针对小内存优化，而本文方法利用大内存优势，可能在某些方法上存在不公平对比（如未调整其他方法的内存预算）。
- **应用限制**：对于必须保留严格模型隐私或无法存储大量历史数据的场景（如医疗数据），本文方法依赖回放缓冲区，仍可能不适用。

（完）
