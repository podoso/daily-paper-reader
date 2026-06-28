---
title: "AdaCuRL: Adaptive Curriculum Reinforcement Learning with Invalid Sample Mitigation and Historical Revisiting"
title_zh: AdaCuRL：具有无效样本缓解和历史回顾的自适应课程强化学习
authors: "Renda Li, Hailang Huang, Fei Wei, Feng Xiong, Yong Wang, Xiangxiang Chu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39479/43440"
tags: ["query:continual"]
score: 8.0
evidence: 课程强化学习，灾难性遗忘，大语言模型
tldr: 针对强化学习训练大语言模型时遇到的梯度饥饿、策略退化及灾难性遗忘等问题，提出自适应课程强化学习框架AdaCuRL，通过难度感知的课程学习和历史样本回放来缓解遗忘，实验证明其在提升推理能力的同时有效保持了先前知识。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有RL方法在混合难度样本上训练遭遇梯度饥饿和策略退化，课程学习面临灾难性遗忘。
method: 设计自适应课程学习策略，结合无效样本缓解和历史回顾机制，逐步增加训练难度。
result: 在多个LLM推理任务上，AdaCuRL提升了推理性能并显著减轻了灾难性遗忘。
conclusion: 自适应课程学习结合历史回放是应对RL训练中遗忘的有效策略。
---

## Abstract
Reinforcement learning (RL) has demonstrated considerable potential for enhancing reasoning in large language models (LLMs). 
However, existing methods suffer from Gradient Starvation and Policy Degradation when training directly on samples with mixed difficulty. To mitigate this, prior approaches leverage Chain-of-Thought (CoT) data, but the construction of high-quality CoT annotations remains labor-intensive. Alternatively, curriculum learning strategies have been explored but frequently encounter challenges, such as difficulty mismatch, reliance on manual curriculum design, and catastrophic forgetting.
To address these issues, we propose AdaCuRL, a Adaptive Curriculum Reinforcement Learning framework that integrates coarse-to-fine difficulty estimation with adaptive curriculum scheduling. This approach dynamically aligns data difficulty with model capability and incorporates a data revisitation mechanism to mitigate catastrophic forgetting. Furthermore, AdaCuRL employs adaptive reference and sparse KL strategies to prevent Policy Degradation. Extensive experiments across diverse reasoning benchmarks demonstrate that AdaCuRL consistently achieves significant performance improvements on both LLMs and MLLMs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：强化学习（RL）在提升大语言模型（LLM）和多模态大语言模型（MLLM）的推理能力方面展现出巨大潜力，特别是以 GRPO（Group Relative Policy Optimization）为代表的奖励驱动方法无需高质量 CoT 蒸馏数据即可实现自我改进。
- **核心问题**：当模型直接在混合难度的样本上训练时，会遭遇两个关键瓶颈：
  - **梯度饥饿（Gradient Starvation）**：若某组 rollout 的奖励全部为 1 或全部为 0，优势函数归零，导致策略梯度信号消失，模型无法学习。
  - **策略退化（Policy Degradation）**：当无效样本（全 0 或全 1 奖励）出现时，KL 惩罚项主导损失，迫使模型向保守的参考模型回归，损害已获得的推理能力。
- **现有方法的局限**：
  - 依赖人工 CoT 数据（成本高）或专家模型（偏差）。
  - 课程学习方法存在难度错配、手动课程设计、缺乏模型反馈、缺乏历史数据回放以缓解灾难性遗忘等问题。

## 2. 论文提出的方法论

### 2.1 核心思想
AdaCuRL（Adaptive Curriculum Reinforcement Learning）通过**粗到细的难度估计** + **自适应课程调度** + **历史数据回放** + **稀疏 KL 与自适应参考**四部分协同工作，动态对齐数据难度与模型能力，抑制无效样本导致的梯度饥饿和策略退化。

### 2.2 关键技术细节

#### (a) 粗到细难度估计（Coarse-to-Fine Difficulty Estimation）
- **粗阶段**：对每个问题用当前模型生成 5 次答案，根据正确次数分为三个粗粒度桶（G1:0-1 正确；G2:2-3 正确；G3:4-5 正确）。按预设比例（例如 2K/3K/5K）从各桶采样，构成候选集 S。
- **细阶段**：对 S 中的每个问题生成 N 次（N >> 5）答案，定义难度分数 `Difficulty(q) = 1 - 正确次数 / N`。过滤掉难度 >0.95 或 <0.05 的极难/极易样本，按难度升序排序形成最终训练集 D。

#### (b) 自适应课程强化学习
- **数据分桶**：将排序后的 D 等分为 K 个连续桶 B1..BK（易到难）。初始训练子集 Dc = B1。
- **渐进扩展**：当模型掌握当前桶后，合并下一个桶到 Dc，避免灾难性遗忘。
- **能力得分（Competence Score, CS）**：基于最近 M 个训练样本的平均奖励 r_bar，按公式更新：  
  `cs(t+1) ← cs(t) + (r_bar - 0.5) × max(1 - cs(t), γ)`  
  当 `cs ≥ (k-1)/K` 时（k 为下一桶索引），触发桶合并。
- **奖励函数**：格式奖励快速收敛后（Tf 步后），仅使用准确率奖励更新策略。
- **稀疏 KL**：当某 rollout 组内奖励全 0 或全 1（即优势 ˆAi = 0）时，忽略该组的 KL 项，避免策略退化。
- **自适应参考模型**：每次桶合并后，将参考模型 πref 重置为当前策略模型 πθ，防止过对齐初始参考模型。

#### (c) 自步机制（Re-AdaCuRL）
- 第一轮训练完成后，用更新后的策略重新估计样本难度，过滤掉难度 <0.2 的已掌握样本，重新分桶并再次执行课程 RL，实现自我迭代优化。

## 3. 实验设计

### 3.1 数据集
- **MLLM 训练集**：约 100K 样本，来自 CLEVR、CLEVR-Math、Geo3K、GeoMverse、GeoQA+、IconQA、Super-CLEVR、TabMWP、UniGeo、GEOS、WeMath、SceMQA、PolyMath 等，涵盖几何、代数、计数等类型。经粗到细估计后得到 10K 训练集（2K 易、3K 中、5K 难）。
- **LLM 训练集**：Open-RS 数据集（7K 样本），直接进行细粒度难度估计与排序。

### 3.2 评测基准（Benchmarks）
- **MLLM 数学推理**：DynaMath、Math-Vista MINI、Math-V、MathVerse MINI、LogicVista。
- **MLLM 通用推理**：MMStar、MMMU、HallusionBench、AI2D、MMVET。
- **LLM 数学推理**：AIME24、AMC23、MATH500、Minerva、Olympiad-bench。

### 3.3 对比方法
- 基线：Base Model、SFT、原始 GRPO。
- 课程变体：AdaCuRL (Easy) / (Hard) 分别只用易或难样本。
- 消融版本：移除非关键组件（如 -SparseKL、-Reset Ref、-Revisiting、-KL）。
- 朴素课程学习（Naive CL）：固定桶顺序，无自适应调度。

## 4. 资源与算力

- **明确指出**：论文未明确说明使用的 GPU 型号、数量、训练时长。仅在实验设置中提到使用 Qwen2.5-VL-3B/7B 和 Qwen2.5-Math-1.5B/7B，超参数如 `N=100` 次生成、`M=512` 样本更新能力得分、`K=4`（MLLM）/ `K=3`（LLM）等，但未提供硬件配置与训练时间。

## 5. 实验数量与充分性

- **实验总量**：在 2 种模型族（MLLM 和 LLM）、4 个具体模型（3B/7B × 2）上，覆盖 10+ 个推理基准，共报告约 20 组主要结果（表1、表2）。此外包含：
  - **消融实验**：表5（KL 设计、历史回顾、训练调度器）、表2（LLM 消融）、表7（动态调度 vs 朴素 CL）。
  - **分析与可视化**：图3（难度估计准确性）、图4（训练动态对比）、图5（难度分布影响）、表3（数据分布变化）、表6（重访与退化次数统计）。
- **充分性评价**：
  - **正面**：实验覆盖了多种难度设置、多种组件消融、跨模态（MLLM 和纯 LLM）验证，对比了 SFT、原始 GRPO 及多个课程变体，统计了重访与退化次数以支撑回忆机制的必要性。
  - **不足**：未报告训练与推理的计算开销对比（如总 GPU 小时数），未在更大尺寸模型（如 14B 或 70B）上验证。缺少在非数学推理任务（如代码、常识推理）上的实验，泛化性有待证明。

## 6. 主要结论与发现

1. **原始 GRPO 提升有限**：在 MLLM 上仅提升约 0.85%，SFT 甚至导致性能下降；在 LLM 上提升约 3%，但 AdaCuRL 显著超越之。
2. **AdaCuRL 一致优于基线**：在 MLLM 数学推理上平均提升 3.17%～2.16%，在 LLM 上提升 3.45%～5.53%。
3. **历史回顾（Revisiting）防止灾难性遗忘**：表6显示大量样本在后续阶段出现奖励下降，而 AdaCuRL 通过合并旧桶缓解遗忘。
4. **自适应调度优于固定课程**：表7中朴素 CL 显著落后于 AdaCuRL，证明模型反馈的重要性。
5. **稀疏 KL 与自适应参考不可或缺**：移除任意一个均导致性能下降（表5、表2）。
6. **自步机制（Re-AdaCuRL）进一步收益**：在 MLLM 上额外提升 1.37%～1.03%，表明迭代重估计可挖掘更多可学习样本。

## 7. 优点

- **方法创新**：首次结合粗到细难度估计 + 自适应课程调度 + 历史回放 + 稀疏 KL，系统性地解决 GRPO 中的梯度饥饿和策略退化问题。
- **无需外部资源**：不依赖人工 CoT 数据、专家模型或额外蒸馏，完全基于模型自身反馈。
- **复合消融设计**：逐一验证了每个子模块（KL 计算方式、参考重置、历史回顾、动态调度）的必要性，归因清晰。
- **跨模态验证**：在 LLM 和 MLLM 上均有效，表明方法的通用性。
- **自步迭代机制**：Re-AdaCuRL 通过重估计进一步利用数据，提高天花板。

## 8. 不足与局限

- **计算开销**：粗到细估计需要在初始阶段对每个问题生成 5 次（粗）和 100 次（细）答案，可能带来较大的推理开销，论文未报告具体耗时。
- **实验范围有限**：仅聚焦于数学推理任务（文本和视觉），未涉及代码生成、常识推理等更广泛的场景。模型尺寸最大仅 7B，未在更大规模模型上验证。
- **潜在偏差**：困难度过滤（剔除难度>0.95 或 <0.05）可能使模型对极端难/易样本的处理能力不可测；自步机制依赖固定难度阈值（0.2），可能不普适。
- **缺乏与最新方法的直接对比**：相比于 DeepSeek-R1 等使用蒸馏+RL 的方法，论文未进行同设置比较，仅对比自身变体。
- **资源信息缺失**：未提供 GPU 时数、训练温度等可重复性关键细节，不利于学术验证。

（完）
