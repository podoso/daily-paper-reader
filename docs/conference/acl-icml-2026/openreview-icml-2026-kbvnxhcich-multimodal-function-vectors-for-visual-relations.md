---
title: Multimodal Function Vectors for Visual Relations
title_zh: 面向视觉关系的多模态函数向量
authors: "Shuhao Fu, Esther A Goldberg, Ying Nian Wu, Hongjing Lu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8c1aabf24a213fc9a4c7b2d756a346e677590124.pdf"
tags: ["query:multimodal"]
score: 7.0
evidence: 多模态学习：视觉关系函数向量
tldr: 大型多模态模型（LMM）的上下文学习机制尚不透明。本文发现LMM中少数注意力头负责传递视觉关系表示，称为函数向量。通过因果中介分析提取这些向量，并操纵它们可提升零样本视觉关系预测准确率。揭示了多模态模型内部关系推理的关键机制。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大型多模态模型内部如何实现任务学习尚不清楚。
method: 通过因果中介分析识别影响视觉关系预测的注意力头，提取并操纵多模态函数向量。
result: 在合成和真实图像数据集上，函数向量操作提升了零样本关系预测准确率。
conclusion: 多模态函数向量是LMM中处理视觉关系的关键组件，可被操控以改善性能。
---

## Abstract
Large Multimodal Models (LMMs) demonstrate impressive in-context learning abilities from few multimodal demonstrations, yet the internal mechanisms supporting such task learning remain opaque. Building on prior work of Large Language Models, we show that a small subset of attention heads in Large Multimodal Models is responsible for transmitting representations of visual relations. The activations of these attention heads, termed $\textit{function vectors}$, can be extracted and manipulated to alter an LMM’s performance on relational tasks. First, using synthetic and real image datasets, we apply causal mediation analysis to identify attention heads that strongly influence relational predictions, and extract multimodal function vectors that improve zero-shot accuracy at inference time. We further demonstrate that these multimodal function vectors can be fine-tuned with a modest amount of training data, while keeping LMM parameters frozen, to significantly outperform in-context learning baselines. Finally, we show that relation-specific function vectors can be linearly combined to solve analogy problems involving novel and untrained visual relations, highlighting the strong generalization ability of this approach. Through experiments on two LMMs, including OpenFlamingo and Qwen3-VL, our results show that these models encode visual relational knowledge within localized internal structures, which can be systematically extracted and optimized, thereby advancing our understanding of model modularity and enhancing control over relational reasoning in LMMs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

大型多模态模型（LMM）在少量多模态演示下展现出强大的上下文学习能力，但其内部实现任务学习的机制仍然不透明。受大型语言模型（LLM）中函数向量研究的启发，本文旨在揭示 LMM 在视觉关系推理任务中如何编码和传递知识，并探索能否通过提取和操控这些内部表示来提升模型性能。理解这些机制对于增强模型可控性、可解释性及泛化能力具有重要意义。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：LMM 中的少数注意力头负责传递视觉关系表示，其激活模式称为“多模态函数向量”（Multimodal Function Vectors）。这些向量可以被提取、操纵甚至微调，从而直接改变模型在关系预测任务上的表现。
- **关键技术细节**：
  - **因果中介分析**：通过干预注意力头激活来识别哪些头对关系预测结果有显著因果影响。
  - **函数向量提取**：从识别出的关键注意力头中提取激活向量，作为关系表示的编码。
  - **函数向量操纵**：在推理时向模型中注入或修改这些向量，用于零样本关系预测改进。
  - **函数向量微调**：保持 LMM 参数冻结，仅用少量训练数据对提取的函数向量进行微调，以提升性能。
  - **线性组合**：将不同关系对应的函数向量进行线性组合，用于解决未见过的新型视觉关系类比问题。
- **公式/算法流程**（文字说明）：
  1. 选定一组少量多模态示范样本（包含图像和文本描述）
  2. 对每个注意力头，在前向传播时记录激活值
  3. 通过因果中介分析（如交换激活值或进行干预）评估每个头对最终关系预测的影响程度
  4. 筛选出高影响注意力头，将其激活值平均后得到该关系的函数向量
  5. 在零样本测试时，通过添加或替换函数向量来调节模型输出

## 3. 实验设计

- **数据集**：
  - 合成图像数据集（用于可控性验证）
  - 真实图像数据集（具体名称未在摘要中给出，推测包含视觉关系常用基准）
- **Benchmark**：在零样本视觉关系预测任务上评估准确率
- **对比方法**：
  - 标准零样本 LMM 基线（无函数向量操纵）
  - 上下文学习基线（使用少量示范进行上下文学习）
  - 函数向量微调后的结果与以上基线对比
- **模型**：OpenFlamingo 和 Qwen3-VL 两种 LMM

## 4. 资源与算力

论文摘要和元数据中**未明确说明**使用的具体 GPU 型号、数量、训练时长等算力信息。仅提及“使用少量训练数据”进行函数向量微调，整体计算开销相对较低，但详细硬件配置未披露。

## 5. 实验数量与充分性

- **实验组数**：摘要提到在合成和真实图像数据集上做了零样本预测对比，涉及函数向量提取、微调、线性组合三项主要实验；每个实验至少包含两种模型（OpenFlamingo, Qwen3-VL），以及多种基线方法。
- **充分性评估**：
  - 实验覆盖了合成和真实场景，支持泛化性验证。
  - 包含两种不同架构的 LMM，增强结论鲁棒性。
  - 消融实验（如仅操纵单个头 vs 组合头）未在摘要中明确提及，可能存在于全文。
  - 对比了标准零样本和上下文学习基线，较为公平。
  - 线性组合实验验证了未见关系的泛化能力，设计合理。
  - 总体实验设计较为充分，但缺少详细统计和误差分析。

## 6. 主要结论与发现

- LMM 中确实存在少量注意力头负责编码视觉关系，其激活构成多模态函数向量。
- 提取并操纵这些函数向量可以在零样本条件下提升视觉关系预测准确率。
- 函数向量经过少量数据微调（模型冻结），性能显著超过传统上下文学习基线。
- 不同关系的函数向量可线性组合，使模型能解决从未训练过的视觉关系类比问题，体现了强泛化能力。
- 这些发现证明 LMM 中视觉关系知识存储在局部化内部结构中，可被系统提取和优化。

## 7. 优点

- 首次将 LLM 中的函数向量概念系统性地拓展到多模态领域，具有创新性。
- 方法简单有效：仅需少量数据即可微调函数向量，无需更新整个模型参数，计算高效。
- 线性组合实验展示了模型的可组合性和强泛化潜力，有助于理解模型模块化。
- 在两种不同架构的 LMM 上验证，增强了结论可靠性。

## 8. 不足与局限

- 实验仅覆盖视觉关系预测这一任务，未在更广泛的多模态任务（如视觉问答、图像描述）上验证函数向量通用性。
- 未披露具体数据集名称和规模，影响可复现性。
- 未提供算力消耗细节，难以评估实际资源门槛。
- 因果中介分析仅针对注意力头，忽略了 MLP 层或其他组件可能的作用。
- 线性组合实验只在简单关系组合上测试，复杂场景下可能失效。
- 实际应用时，需先对每个新关系提取函数向量，流程仍依赖示范样本，并非完全零样本。

（完）
