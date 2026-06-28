---
title: Learning a Fix and Explore Framework for Continuous Generalized Category Discovery
title_zh: 持续广义类别发现的修复与探索框架
authors: "Chunming Li, Shidong Wang, Haofeng Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37530/41492"
tags: ["query:continual"]
score: 8.0
evidence: 持续广义类别发现中利用知识蒸馏缓解灾难性遗忘
tldr: 在持续广义类别发现中，模型需不断发现新类别并保持旧类辨别力。本文提出修复与探索框架，通过参数级知识蒸馏缓解灾难性遗忘。实验表明该方法在多个阶段有效平衡稳定性与可塑性，优于现有持续学习方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 传统转导式学习无法处理持续出现未知类别的现实场景，模型容易遗忘旧类。
method: 采用参数级知识蒸馏从历史模型转移知识，同时设计探索模块发现新类别。
result: 在多个基准上比现有方法更有效地保持旧类准确率并提升新类发现能力。
conclusion: 提出的框架解决了持续发现与遗忘之间的平衡问题。
---

## Abstract
To address the limitations of transductive learning in evolving real-world scenarios where unknown categories may continuously emerge, Continual Generalized Category Discovery (C-GCD) presents a novel paradigm that extends conventional category discovery frameworks. Unlike traditional static learning environments, C-GCD requires models to incrementally discover novel categories across multiple operational phases while maintaining discrimination capabilities for previously learned classes, posing significant challenges in balancing stability and plasticity. Prior approaches typically employ parameter-level knowledge distillation from historical models to alleviate catastrophic forgetting, which effectively preserves prior knowledge and optimizes computational efficiency. However, our analysis reveals that the persistent availability of samples from previous stages enables more sophisticated knowledge preservation strategies. Specifically, we present a Fix and Explore strategy that employs distinct learning methodologies for different types of potential data, aiming to preserve the features of old categories as much as possible and gradually exploring the potential distribution of new class latent spaces, we can enhance the model's ability to discover novel categories. This paper investigates this effect and introduces a novel heuristic paradigm to solve the C-GCD problem, called Fix and Explore (FaE), which aims to provide sufficient imaginative space for new classes while preserving the classification ability for old tasks. We conducted experiments across multiple datasets and performed detailed comparisons. The results demonstrate that our method achieves state-of-the-art performance at each stage across all datasets.

---

## 论文详细总结（自动生成）

# 论文《Learning a Fix and Explore Framework for Continuous Generalized Category Discovery》详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题背景**：现实场景中未知类别可能持续涌现，传统转导式学习的广义类别发现（GCD）仅支持单阶段推理，无法动态检测新类别。为此，持续广义类别发现（C-GCD）被提出，要求模型在多阶段操作中增量发现新类别，同时保持对已学类别的判别能力。
- **核心挑战**：在持续学习过程中，模型面临严重的**灾难性遗忘**问题，需要在**稳定性（旧知识保留）** 与**可塑性（新知识探索）**之间取得平衡。
- **现有方法不足**：已有方法（如Happy）采用参数级知识蒸馏缓解遗忘，但存在“一刀切”策略，未能区分新旧样本的不同需求，导致后期阶段新旧类别特征空间耦合加剧，抑制了新类发现能力。

## 2. 方法论：核心思想、关键技术细节

### 2.1 核心思想：Fix and Explore（FaE）框架
- **整体思路**：采用“分而治之”策略，先通过聚类区分潜在旧类和新类样本，然后对不同类型的样本施加不同的知识蒸馏策略（Fix项：固定旧类特征；Explore项：探索新类潜在分布），并引入图正则化进一步增强新类发现。
- **架构组成**：特征提取器 \(f_t\)、分类器 \(h_t\)、投影头 \(g_t\)；采用指数移动平均（EMA）更新防止过拟合。

### 2.2 关键技术细节

1. **分类器初始化**：
   - 每阶段使用K-means聚类将数据分成 \(K_t\) 类，选取离已知类原型最远的 \(K_{new}\) 个中心作为新类分类器初始值。
   - 利用预测结果将样本标记为潜在新类（\(B_t^{new}\)）或潜在旧类（\(B_t^{old}\)）。

2. **Fix项：不同蒸馏策略**：
   - **旧类样本**：采用余弦距离蒸馏损失（L2范数对齐），严格保留旧类特征：
     \[
     L_{old} = \frac{1}{|B_t^{old}|}\sum_{k} \left[1 - \cos(f_t(x_k^{old}), f_{t-1}(x_k^{old}))\right]
     \]
   - **新类样本**：采用图知识蒸馏（MSE损失），允许特征空间轻微偏移以支持新类探索：
     \[
     L_{new} = \frac{1}{|B_t^{new}|}\sum_{i,j} \left\| \cos(f_t(x_i^{new}), f_t(x_j^{new})) - \cos(f_{t-1}(x_i^{new}), f_{t-1}(x_j^{new})) \right\|_F^2
     \]
   - 总蒸馏损失：\(L_{distill} = L_{old} + L_{new}\)。

3. **Explore项：已知类感知图正则化**：
   - 利用旧类分类器的logit预测构建伪标签图 \(W^t\)，同时用投影层嵌入构建相似度图 \(W^z\)，最小化两者交叉熵：
     \[
     L_g = \frac{1}{|B_t^{new}|}\sum_{b=1} H(\hat{W}_{bj}^t, \hat{W}_{bj}^z)
     \]
   - 目的：使具有相似伪标签的新类样本在嵌入空间聚集，促进新类分离。

4. **其他损失**：
   - **组软熵正则化** \(L_{entropy}\)：平衡新旧类及类内分布，防止预测偏向样本量多的旧类。
   - **难度感知原型采样特征回放** \(L_{hap}\)：按样本难度加权回放旧类特征，进一步缓解遗忘。
   - **自蒸馏损失** \(L_{self}\)：同Happy，增强表示鲁棒性。
   - 总损失：\(L = L_{distill} + L_g + L_h\)，其中 \(L_h = L_{hap} + L_{self} + L_{entropy}\)。

5. **EMA更新**：防止模型过早收敛到局部最优。

## 3. 实验设计

### 3.1 数据集与场景
- **数据集**：CIFAR-100、ImageNet-100、Tiny-ImageNet（通用图像）、CUB-200（细粒度鸟类）。
- **场景**：持续学习分5阶段（Stage-0初始化 + Stage-1~5）和10阶段（Table 3）两种设置。
- **评估指标**：总体准确率（All）、旧类准确率（Old）、新类准确率（New）；额外指标：最大遗忘（\(M_f\)）、最终发现（\(M_d\)）。

### 3.2 对比方法
- 基线：K-means、VanillaGCD、SimGCD、SimGCD+LwF（知识蒸馏基线）；
- C-GCD方法：FRoST、GM、MetaGCD、Happy（当前SOTA）。

### 3.3 基准设置
- 初始化阶段使用SimGCD损失（交叉熵+监督/自监督对比学习）；持续阶段使用本文FaE框架。
- 所有方法均使用ViT-B/16（DINO预训练），仅微调最后一个块。

## 4. 资源与算力
- **GPU**：NVIDIA GeForce RTX A6000。
- **训练时长**：初始化阶段100 epochs，持续阶段每30 epochs。未明确给出总时长或GPU数量（推测单卡）。
- **补充**：文中未提及具体训练时间或显存消耗，仅说明硬件型号。

## 5. 实验数量与充分性

### 5.1 实验组数
- **主实验**：4个数据集 × 5阶段（Table 1），2个数据集 × 10阶段（Table 3）。
- **对比方法**：8种方法（含基线、SOTA）。
- **消融实验**：Table 4，分析蒸馏策略（旧类/新类采用不同蒸馏）和图正则化的贡献。
- **训练策略分析**：Figure 3，比较最佳epoch输出 vs 最后epoch输出。
- **未知类别数估计**：Table 5，使用轮廓系数估计类别数时的性能。
- **额外指标**：Table 2，报告遗忘和发现指标。

### 5.2 充分性与公平性
- **充分性**：覆盖多个数据集、多种阶段数、多种指标，消融实验完整。对比方法包括近年代表性工作。
- **客观性**：所有方法在相同骨干、相同初始化下比较（初始化损失一致），评估协议严格（ACC计算需匈牙利匹配）。注意Happy在每阶段选择最佳epoch输出，而FaE使用最后epoch输出，作者指出FaE在更实际设置下仍优于Happy（Figure 3）。
- **潜在偏差**：假设每阶段新类别数量已知（除Table 5），实际应用中可能需估计。实验对此进行了补充分析。

## 6. 主要结论与发现
- **总体性能**：FaE在CIFAR-100、ImageNet-100、Tiny-ImageNet、CUB-200上均超越所有对比方法，在5阶段设置中所有阶段均取得最佳结果（Table 1）。
- **遗忘缓解**：最大遗忘（\(M_f\)）显著降低（CIFAR-100: 11.22→6.82；Tiny-ImageNet: 9.75→5.43），新类发现（\(M_d\)）大幅提升（51.36→55.60；43.38→52.60）（Table 2）。
- **10阶段挑战**：性能差距进一步扩大（CIFAR-100: 57.81→64.07；Tiny-ImageNet: 50.69→61.83），证明方法在复杂场景下更稳健（Table 3）。
- **消融验证**：“旧类用余弦蒸馏+新类用图蒸馏”组合结合图正则化效果最佳（Table 4）。
- **实用场景**：在未知类别数估计和最后epoch输出下，FaE仍保持优势（Table 5, Figure 3）。

## 7. 优点
- **创新性**：首次在C-GCD中提出**分而治之的蒸馏策略**，区分旧类和新类样本，分别使用L2范数和图蒸馏，有效平衡稳定性和可塑性。
- **技术亮点**：
  - 引入**已知类感知图正则化**，利用旧类分类器指引新类表征学习，避免新类嵌入与旧类混淆。
  - 使用**聚类初始化和EMA**提高训练稳定性。
  - 包含**组软熵正则化**和**难度感知回放**等辅助损失，进一步提升性能。
- **实验充分**：在多数据集、多阶段设置、多种指标下验证，消融实验齐全，分析深入（如训练策略影响、未知类别数估计）。
- **结果显著**：几乎所有指标均达到SOTA，尤其在10阶段长期设置下性能提升明显。

## 8. 不足与局限
- **假设限制**：方法假设每阶段新类别数量已知（除Table 5补充实验），实际应用中可能需额外估计机制。
- **算力需求**：虽采用ViT-B/16（DINO预训练）并仅微调最后一层，但未报告训练时间或显存，可能对资源要求较高。
- **未覆盖场景**：实验仅在图像分类数据集上进行，未在更复杂任务（如目标检测、语义分割）或真实流式数据上验证。
- **对比方法局限**：部分对比方法（如GM、FRoST）非专为C-GCD设计，可能未充分调优；Happy采用最佳epoch选择策略，而FaE使用最后epoch，直接比较存在设置差异（尽管Figure 3已分析）。
- **消融缺失**：未对各子损失（如 \(L_{hap}\)、\(L_{self}\)、\(L_{entropy}\)）进行独立贡献分析，仅呈现整体消融。
- **可解释性**：聚类初始化可能引入噪声，对长期累积误差的影响未深入讨论。

（完）
