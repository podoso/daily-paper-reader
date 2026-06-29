---
title: Multimodal Function Vectors for Spatial Relations
title_zh: 空间关系的多模态函数向量
authors: "Shuhao Fu, Esther A Goldberg, Ying Nian Wu, Hongjing Lu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yLYJbI8vdw"
tags: ["query:multimodal"]
score: 8.0
evidence: 视觉语言模型中空间关系的多模态函数向量
tldr: 大型多模态模型虽具备上下文学习能力，但空间关系推理的内部机制不明。本文通过因果中介分析，在OpenFlamingo和Qwen3-VL中发现少数注意力头编码空间关系表示，提取出多模态函数向量。操纵这些向量可改变模型关系预测性能，揭示了VLM中关系推理的神经基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 372, \"height\": 376, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1308, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1305, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1491, \"height\": 1086, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1448, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1441, \"height\": 310, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1431, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1429, \"height\": 1018, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1445, \"height\": 740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1448, \"height\": 754, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1437, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ylyjbi8vdw/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 858, \"height\": 438, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-ylyjbi8vdw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1403, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ylyjbi8vdw/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 674, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ylyjbi8vdw/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 680, \"height\": 265, \"label\": \"Table\"}]"
motivation: 多模态模型空间关系推理的内部机制不透明。
method: 通过因果中介分析识别编码空间关系的注意力头，提取多模态函数向量。
result: 操纵函数向量可有效改变模型关系预测性能。
conclusion: 揭示了VLM中关系推理的机制，为模型可解释性提供新视角。
---

## Abstract
Large Multimodal Models (LMMs) demonstrate impressive in-context learning abilities from limited multimodal demonstrations, yet the internal mechanisms supporting such task learning remain opaque. Building on prior work of large language models, we show that a small subset of attention heads in two vision–language model, OpenFlamingo and Qwen3-VL, is responsible for transmitting representations of spatial relations. The activations of these attention heads, termed function vectors, can be extracted and manipulated to alter an LMM’s performance on relational tasks. First, using both synthetic and real image datasets, we apply causal mediation analysis to identify attention heads that strongly influence relational predictions, and extract multimodal function vectors that improve zero-shot accuracy at inference time. We further demonstrate that these multimodal function vectors can be fine-tuned with a modest amount of training data, while keeping LMM parameters frozen, to significantly outperform in-context learning baselines. Finally, we show that relation-specific function vectors can be linearly combined to solve analogy problems involving novel and untrained spatial relations, highlighting the strong generalization ability of this approach. Our results show that LMMs encode spatial relational knowledge within localized internal structures, which can be systematically extracted and optimized, thereby advancing our understanding of model modularity and enhancing control over relational reasoning in LMMs.

---

## 论文详细总结（自动生成）

# 论文《Multimodal Function Vectors for Spatial Relations》详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：大型多模态模型（LMMs）在少量多模态示例下表现出强大的上下文学习能力，但其内部机制仍不透明。特别是视觉空间关系推理（如“上方”、“左侧”等）的神经表征方式未被揭示。
- **整体含义**：作者旨在探索LMMs是否像语言模型一样，存在编码关系任务的局部化内部结构（即函数向量），并通过因果分析和干预验证其可操控性与可迁移性。这项工作有助于理解模型模块化，并为可控推理提供新途径。

## 2. 方法论

### 核心思想
- 借鉴语言模型中的函数向量（Function Vectors）概念，将其扩展至多模态场景。假设LMMs中少数注意力头（attention heads）的激活模式编码了空间关系任务，这些激活可被提取、组合和优化。

### 关键技术细节
1. **因果中介分析（Causal Mediation Analysis）**
   - 对每个注意力头 \(a_{\ell j}\)，计算其“平均间接效应”（Average Indirect Effect, AIE）：
     - 使用**关系一致prompt**（4个示例均展示同一空间关系）和**无信息prompt**（示例中的关系被随机化）分别获取激活。
     - 将关系一致的平均激活 \(\bar{a}^t_{\ell j}\) 替换到无信息prompt的对应注意力头，测量模型预测正确关系标签的概率提升，即AIE。
   - 选择AIE最高的前10个注意力头作为任务相关子网络 \(A_t\)，求和得到关系特定的函数向量 \(v_t = \sum_{\bar{a}^t_{\ell j} \in A_t} \bar{a}^t_{\ell j}\)。

2. **零样本干预**
   - 将函数向量 \(v_t\) 直接加在无任何示例的零样本prompt的隐藏层最后token位置（选择中间层如第19层或第8层），评估模型预测正确关系标签的准确率。

3. **微调函数向量（Fine-tuned Function Vector, FFV）**
   - 冻结整个LMM参数，仅更新函数向量 \(v_t\)。使用1000个零样本示例，以负对数似然为目标函数训练20个epoch（Adam优化器，学习率0.001，余弦退火调度）。

4. **复合函数向量（Composite Function Vector, CFV）**
   - 对于未训练的复合关系（如“左上”），通过源类比示例中的目标对象预测概率计算每个基础关系函数向量的权重，加权求和得到复合向量，再用于目标类比推理（one-shot analogy）。

## 3. 实验设计

### 数据集
- **合成图像数据集**：基于Big and Small Objects dataset的42个物体，生成7000张800×800图像，包含4种基本空间关系（上、下、左、右），还额外生成含4种复合关系的1000张测试图像以及含10个新物体的泛化测试集。
- **真实图像数据集（GQA）**：从GQA 113K图像中筛选出4226张，包含7种空间关系（above, below, left of, right of, next to, behind, in front of），分为训练集和测试集各半。

### Benchmark与对比方法
- **模型**：OpenFlamingo-4B, LLaVA-OneVision-1.5-4B-Instruct, Qwen3-VL-4B-Instruct。
- **对比设置**：
  - 零样本基线（0-shot LMM）
  - 少样本ICL（1-shot, 4-shot, 8-shot）
  - 初始（未微调）函数向量（Initial FV）
  - 微调函数向量（FFV）
  - 复合函数向量（CFV） vs. 零样本、1-shot、4-shot ICL（用于复合关系任务）。
- **评估指标**：Top-1预测准确率（预测第一个token是否正确）。

### 消融实验
- 注入层的影响（不同层）
- 注意力头数量的影响（1-50个）
- 上下文大小的影响（2-shot, 4-shot, 8-shot）

### 其他实验
- 迁移性实验：将合成数据集上训练的函数向量直接用于GQA数据集。
- 交叉模型RSA相似性分析。

## 4. 资源与算力

- 论文中**未明确说明**使用的GPU型号、数量及训练时长。仅在附录中提到Qwen3-VL的十-shot实验因GPU内存限制被省略，但未提供具体硬件细节。

## 5. 实验数量与充分性

- **实验数量**：至少包括以下几组：
  - 主实验：两个模型在两类数据集上的零样本/少样本/初始FV/FFV对比（合成4种关系×2模型，GQA 7种关系×1模型（OpenFlamingo））。
  - 消融实验：注入层、头数、上下文大小各一组（多个关系）。
  - 泛化实验：新物体测试、复合关系类比任务。
  - 迁移实验：跨数据集（合成→GQA）。
  - 结构相似性分析。
- **充分性判断**：实验设计较为系统，覆盖了不同数据集、模型、关系类型，并进行了多视角消融。但存在以下不足：
  - 仅测试了3个模型，且只有OpenFlamingo和Qwen3-VL进行了函数向量实验（LLaVA仅报告了ICL Baseline）。
  - 真实图像数据集GQA只报告了OpenFlamingo的FFV结果，Qwen3-VL仅用于合成数据及类比任务。
  - 复合关系类比任务仅测试了4种复合关系，样本量有限。
  - 未与更先进的基于LoRA或prompt tuning的方法比较，公平性可能受限。

## 6. 主要结论与发现

1. **空间关系编码于局部注意力头**：通过因果中介分析，发现每个空间关系由LMM中少数（约10个）位于中间层的注意力头因果驱动。
2. **函数向量可提取并提升零样本性能**：直接注入初始函数向量即可显著提升零样本准确率（如从4.8%提升至8-9%）。
3. **微调函数向量大幅超越ICL**：在合成数据集上，FFV最高可达72.2%（Qwen3-VL），远高于4-shot ICL的26.8%；在GQA上精度从零样本11.8%提升至约25%，超越4-shot ICL的19.0%。
4. **线性组合支持新关系类比**：复合函数向量在未训练的复合关系上达到16.8%（OpenFlamingo）和45.1%（Qwen3-VL），优于4-shot ICL（8.1%和28.7%）。
5. **跨数据集迁移有效**：合成数据集上训练的函数向量直接用于GQA，性能与GQA原生函数向量相当或更优。

## 7. 优点

- **方法创新**：首次将函数向量概念从纯语言模型系统扩展到多模态模型，并针对空间关系进行因果分析。
- **可解释性强**：通过AIE定位关键注意力头，可视化哪些层和头对关系推理最重要。
- **灵活性高**：函数向量可微调、可组合、可迁移，且全部操作冻结模型参数，计算效率高。
- **泛化验证充分**：包括新物体、新关系（复合）、跨数据集迁移等多个维度验证。

## 8. 不足与局限

- **关系范围有限**：仅研究基本空间关系（上下左右等），未涉及物理关系（如推、拉）、社会关系（如交互）等更复杂的视觉关系。
- **模型覆盖不足**：仅深入分析OpenFlamingo和Qwen3-VL，LLaVA仅作ICL对比，缺乏对更多架构（如BLIP、LLaVA-NeXT等）的验证。
- **真实图像实验受限**：GQA数据集因规模有限，函数向量提取和微调共用2,113张训练图，统计显著性可能不足；且只对OpenFlamingo进行了完整的FFV分析。
- **类比任务依赖源示例**：复合函数向量构建需要一对一源类比（one-shot），不能完全零样本，且权重计算假设线性可分性，可能不适用于非线性关系。
- **算力资源未报告**：缺少可重复性所需的具体硬件与时间信息。
- **公平基线缺失**：未与参数高效微调方法（如LoRA、Adapter）直接对比，结论推广需谨慎。

（完）
