---
title: "LoRA in LoRA: Towards Parameter-Efficient Architecture Expansion for Continual Visual Instruction Tuning"
title_zh: LoRA in LoRA：面向持续视觉指令调优的参数高效架构扩展
authors: "Chang Che, Ziqi Wang, Pengwan Yang, Cheems Wang, Hui Ma, Zenglin Shi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39082/43044"
tags: ["query:continual"]
score: 8.0
evidence: 用于多模态大语言模型的持续学习方法避免灾难性遗忘
tldr: 持续视觉指令调优面临灾难性遗忘和参数膨胀问题。本文提出LiLoRA，通过跨任务共享LoRA矩阵A并扩展矩阵B，实现高效架构扩展。实验表明LiLoRA在减少参数开销的同时有效缓解遗忘，为MLLM持续学习提供了可扩展的解决方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有架构扩展方法为每个任务扩展整个层，导致参数过多且可扩展性差。
method: 跨任务共享LoRA矩阵A，仅扩展矩阵B，实现参数高效的架构扩展。
result: 在持续视觉指令调优任务中以更少的参数实现了竞争性的遗忘缓解。
conclusion: 该方法为多模态大模型的持续学习提供了一种轻量级、可扩展的范式。
---

## Abstract
Continual Visual Instruction Tuning (CVIT) enables Multimodal Large Language Models (MLLMs) to incrementally learn new tasks over time. However, this process is challenged by catastrophic forgetting, where performance on previously learned tasks deteriorates as the model adapts to new ones. A common approach to mitigate forgetting is architecture expansion, which introduces task-specific modules to prevent interference. Yet, existing methods often expand entire layers for each task, leading to significant parameter overhead and poor scalability. To overcome these issues, we introduce LoRA in LoRA (LiLoRA), a highly efficient architecture expansion method tailored for CVIT in MLLMs. LiLoRA shares the LoRA matrix A across tasks to reduce redundancy, applies an additional low-rank decomposition to matrix B to minimize task-specific parameters, and incorporates a cosine-regularized stability loss to preserve consistency in shared representations over time. Extensive experiments on a diverse CVIT benchmark show that LiLoRA consistently achieves superior performance in sequential task learning while significantly improving parameter efficiency compared to existing approaches.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：多模态大语言模型（MLLMs）在视觉问答、图像描述等任务中表现优异，通常通过多阶段训练（预训练 + 视觉指令微调）实现。但在实际应用中，模型需要持续学习新任务，即**持续性视觉指令微调（CVIT）**。然而，连续学习面临严重的**灾难性遗忘**问题——学习新任务会导致旧任务性能急剧下降。
- **现有方法的不足**：目前CVIT方法主要分为两类：
  - 静态架构方法（如MoE、SMoLoRA等）：使用固定容量共享参数，任务增多时竞争加剧，可扩展性差。
  - 动态架构扩展方法（如Eproj、DER等）：为每个任务添加独立模块，但通常扩展整个网络层，导致参数冗余严重、计算开销大，难以扩展到大规模场景。
- **核心目标**：提出一种**参数高效的架构扩展方法**，在缓解遗忘的同时大幅降低参数增长，实现轻量级、可扩展的持续学习。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 2.1 核心思想
- **观察**：作者通过CKA相似度分析发现，不同任务学到的LoRA矩阵A（低秩分解中的一个小矩阵）具有高度相似性，而矩阵B差异显著。这表明矩阵A承载任务不变信息，可以共享；矩阵B则包含任务特定适应信息。
- **LiLoRA整体设计**：基于低秩适应（LoRA），通过跨任务共享矩阵A、对矩阵B进行二次低秩分解，并引入正则化损失稳定共享基础，实现参数高效的架构扩展。

### 2.2 关键技术细节

1. **任务不变矩阵A共享**：所有任务共享同一个矩阵A，每个任务仅保留自己的矩阵Bi。更新公式为 ΔWi = BiA，大幅减少参数（相比每个任务独立LoRA，参数减少约40%以上）。

2. **任务特定矩阵B的分解**：将每个任务原本的Bi进一步分解为共享基础B0和任务特定残差 (ẼBi·ẼAi)，其中ẼBi∈R^(d×~r)，ẼAi∈R^(~r×r)，且~r < r。任务权重表示为：
   ΔWi = (αB0 + (1−α)ẼBi·ẼAi)·A
   其中α是**可学习的融合系数**，由Sigmoid(N(0,1))初始化，通过反向传播动态调节共享与任务特定知识的权重。

3. **余弦正则化基础稳定性损失（Lreg）**：当新任务到来时，若其任务特定表示（ẼBt·ẼAt）与前一个任务的任务特定表示余弦相似度低，则限制对共享基础B0的更新幅度。定义为：
   Lreg = (1 − sim_t) · ||B0^t − B0^(t−1)||_F^2
   其中sim_t = cos(ẼBt·ẼAt, ẼB_{t-1}·ẼA_{t-1})。该损失仅在t>1时激活，强制B0在任务偏离时保持稳定。

### 2.3 算法流程
- 冻结预训练模型M。
- 对每个任务Dt：
  - 若t=1，初始化共享矩阵B0和A。
  - 初始化当前任务特定矩阵ẼBt、ẼAt。
  - 按公式计算ΔWt，计算自回归损失Ltask。
  - 若t>1，计算Lreg；否则Lreg=0。
  - 最小化Ltask + λLreg，更新B0、A、ẼBt、ẼAt、α。

## 3. 实验设计

### 3.1 数据集与Benchmark
- 使用**CVIT Benchmark**（Wang et al., 2024c），包含6个指令数据集：**ScienceQA、TextVQA、Flickr30k、ImageNet、GQA、VQAv2**，覆盖视觉问答、图像分类、图像描述三类任务。
- 实验设置两种场景：
  - **Single-type instruction**：6个任务按顺序学习，每个任务指令格式相近。
  - **Five-type instruction**：任务指令格式更多样（5种不同类型）。

### 3.2 对比方法
- **上界**：DirLoRA（每个任务独立LoRA）。
- **下界**：Zero-shot（无微调）。
- **基线方法**：SeqLoRA、DoRA、MoeLoRA、C-LoRA、Replay、EWC、EWC+TIR、Eproj。
- **最新SOTA**：SMoLoRA（同为CVIT专用方法）。

### 3.3 评估指标
- **AP** (Average Performance)：最终所有任务平均准确率。
- **MAP** (Mean Average Performance)：所有学习阶段AP的平均值。
- **BWT** (Backward Transfer)：衡量遗忘程度（正值表示正向迁移）。
- **MIF** (Mean Instruction Following)：衡量指令遵循一致性。

## 4. 资源与算力

- 文中未明确说明使用的GPU型号、数量或训练总时长。
- 仅说明采用LLaVA-v1.5-7B作为基座模型，训练1个epoch，batch size=64，学习率2e-5，使用Adam优化器。
- 参数规模：LiLoRA总可扩展参数为985.1MB（Single-type），每个任务新增104.6MB，相比DirLoRA（2,143.9MB/357.3MB）节省54%总参数和70%每任务参数。
- **注意**：论文未提及具体计算资源（如A100数量/小时数），读者需自行估计。

## 5. 实验数量与充分性

- **主要结果**：表1展示Single-type和Five-type两种设置下的完整对比（10+种方法，6个任务的逐任务准确率、AP、MAP、BWT、MIF）。
- **消融实验**：
  - 表2：对共享A、分解B、Lreg三个组件进行消融，并给出参数效率分析。
  - 表3：研究共享秩r（64/128）和任务特定秩~r（r/2,r/4,r/8）的影响。
  - 表4：对融合系数α的不同固定值/可学习设置进行对比。
  - 图3：展示学习后α在层间的分布变化。
- **稳定性分析**：图4绘制ScienceQA和TextVQA在连续学习过程中准确率曲线，验证抗遗忘能力。
- **跨模型泛化性**：表5在Qwen2-VL-2B上重复实验，对比DirLoRA、SeqLoRA、Eproj。
- **充分性评价**：实验覆盖多种任务类型、多种基线、多种秩配置、不同基座模型，且消融实验系统。但在更大规模任务序列（如>10任务）或不同领域（如医疗、遥感）上的实验缺失。总体设计较为客观公平。

## 6. 论文的主要结论与发现

- LiLoRA在所有评估指标（AP、MAP、BWT、MIF）上显著优于非扩展方法，与DirLoRA上界性能接近，但参数开销大幅降低。
- 共享矩阵A和分解矩阵B是减少参数的关键，但必须配合余弦正则化损失Lreg才能保持共享基础稳定，防止遗忘恶化。
- 可学习融合系数α能够自动适应不同任务，更好地平衡共享与任务特定知识。
- LiLoRA在LLaVA和Qwen2-VL上均表现良好，证明了跨模型泛化能力。

## 7. 优点

- **参数效率极高**：在几乎不损失性能的前提下，每任务参数减少70%以上，总参数减少54%。
- **方法简洁有效**：基于LoRA的巧妙再分解，无需复杂门控或回放存储，易实现。
- **正则化设计合理**：余弦正则化依据任务相似性自适应约束共享基础，避免了简单L2正则化的过度惩罚。
- **可学习的融合系数**：提供了更灵活的共享-特化权衡，且不同层自动分化。
- **评估全面**：包含多种指标（AP、MAP、BWT、MIF）和两种指令多样性设置，消融实验系统。

## 8. 不足与局限

- **计算资源未公开**：未说明具体的GPU型号和训练时间，复现成本难以估计。
- **任务序列长度有限**：仅6个任务，未验证在10+或更多任务场景下的可扩展性。
- **任务多样性不足**：数据集仅包含VQA、分类、描述三类，缺乏推理、生成等更复杂任务。
- **忽略任务顺序敏感性**：未进行不同任务顺序的鲁棒性测试。
- **仅适用于LoRA类方法**：若基座模型不支持LoRA，则无法直接应用。此外，共享矩阵A的假设（矩阵A任务不变）是否对所有LoRA变体成立仍存疑。
- **与基线公平性**：部分基线（如Replay、EWC）在更大内存或更优超参数下可能表现更好，但文中统一设置1 epoch、固定超参，可能不利于非专用方法。

（完）
