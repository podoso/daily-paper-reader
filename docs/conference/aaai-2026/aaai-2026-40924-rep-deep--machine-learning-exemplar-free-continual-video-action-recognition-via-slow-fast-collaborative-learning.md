---
title: "Rep Deep & Machine Learning: Exemplar-Free Continual Video Action Recognition via Slow-Fast Collaborative Learning"
title_zh: 无样本持续视频动作识别：基于慢速-快速协作学习
authors: "Xueyi Zhang, Chengwei Zhang, Zheng Li, Xiyu Wang, Siqi Cai, Mingrui Lao, Yanming Guo, Huiping Zhuang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40924/44885"
tags: ["query:continual"]
score: 9.0
evidence: 无样本持续学习用于视频动作识别
tldr: 针对现有持续学习方法依赖样本重放导致存储负担和隐私风险的问题，本文研究无样本持续视频动作识别，提出慢速-快速协作学习（SFCL）框架。SFCL集成基于梯度驱动的慢速分支（适应新任务）和基于解析学习的快速分支（保留旧知识），在不存储历史数据的情况下有效缓解灾难性遗忘。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续学习方法依赖样本重放，存在存储开销和隐私问题。
method: 提出慢-快协作学习，融合梯度驱动和解析学习分支实现无样本持续学习。
result: 在持续视频动作识别任务上，无样本方法性能优于依赖重放的方法。
conclusion: 无样本持续学习框架有效平衡了适应性和对旧知识的保留。
---

## Abstract
In real-world applications, video action recognition models must continuously learn new action categories while retaining previously acquired knowledge. However, most existing approaches rely on storing historical data for replay, which introduces storage burdens and raises data privacy concerns. To address these challenges, we investigate the problem of Exemplar-Free Continual Video Action Recognition (EF-CVAR) and propose a novel framework named Slow-Fast Collaborative Learning (SFCL). SFCL integrates two complementary learning paradigms: a slow branch based on gradient-driven deep learning, which provides strong adaptability to new tasks, and a fast branch based on analytic learning (e.g., Recursive Least Squares), which efficiently preserves old knowledge without requiring access to past samples. To enable effective collaboration between the two branches, we design the Slow-Fast Dynamic Re-parameterization (SFDR) mechanism for adaptive fusion, and the Knowledge Reflection Mechanism (KRM), which mitigates forgetting and task-recency bias via pseudo-feature generation and dual-level knowledge distillation. Extensive experiments on UCF101, HMDB51, and Something-Something V2 demonstrate that SFCL achieves superior performance compared to existing replay-based methods, despite being exemplar-free. Notably, in long-duration continual learning scenarios, SFCL exhibits remarkable robustness, achieving up to a 30.39\% improvement in accuracy over baselines while maintaining a low forgetting rate, highlighting its scalability and effectiveness in real-world video recognition tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：现实世界中，视频动作识别模型需要持续学习新动作类别，同时保留已学知识。现有方法大多依赖存储历史数据以供重放（replay），这带来了存储负担和隐私风险。
- **核心问题**：如何在**不存储任何历史样本**（即无样本/Exemplar-Free）的条件下，实现持续的视频动作识别（EF-CVAR），并克服灾难性遗忘和任务-最近偏差（task-recency bias）。
- **整体含义**：提出一种全新框架，将梯度驱动的深度学习（适应新任务）与解析学习（稳定保留旧知识）有机结合，在不依赖样本重放的情况下，达到甚至超越基于重放方法的效果，为隐私敏感的实际应用提供可扩展解决方案。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想：慢速-快速协作学习（Slow-Fast Collaborative Learning, SFCL）
- **慢速分支（Slow Branch）**：基于梯度反向传播（BP）的深度学习分支，负责增量学习新任务，提供强适应性（plasticity）。
- **快速分支（Fast Branch）**：基于解析学习（如递归最小二乘法 RLS）的分支，通过闭式解快速整合知识，无需历史数据，提供稳定性（stability）。
- 两个分支通过动态重参数化机制融合，并辅以知识反思机制，实现知识平衡与迁移。

### 关键技术细节

#### (a) Slow-Fast Dynamic Re-parameterization (SFDR)
- **双分支结构**：慢速分支（BP）和快速分支（解析）在分类器层共享特征提取器（TSM骨干+瓶颈层），但使用不同学习方式。
- **解析学习分支**：  
  - 基类任务后，用全部训练数据求解闭式解（Moore-Penrose伪逆）得到最优全连接层权重。  
  - 后续增量任务通过**递归最小二乘（RLS）**更新权重，仅需当前任务数据即可逐步更新，无需存储旧数据。  
  - 公式：最优权重 \(\hat{\theta}_{AD,k} = \theta_{AD,k-1} - R_k (F^T_{AU,k} F_{AU,k} \theta_{AD,k-1} - F^T_{AU,k} Y_k)\)，其中 \(R_k\) 通过递归公式更新。
- **动态重参数化**：  
  - 将解析分支的权重复制一份作为可训练的BP分支初始值。  
  - 引入**流式判别器（Streaming Discriminator）**，根据输入特征动态生成融合权重 \(a\)（0~1），用于加权融合两个分支的权重和偏置。  
  - 前向过程：\(F^{M} = (a \cdot W^{AL} + (1-a) \cdot W^{RE}) F + ...\)，输出 \(\hat{Y}^M\)。  
  - 通过基类数据训练判别器和BP分支，使其学会自适应融合。

#### (b) Knowledge Reflection Mechanism (KRM)
- **高斯记忆合成（Gaussian Memory Synthesis, GMS）**：  
  - 对每个旧类别，计算其特征均值 \(\mu_i\) 和协方差矩阵 \(v_i\)，构成多元高斯分布。  
  - 在增量任务中，从高斯分布中采样伪特征，与当前新类特征拼接，形成平衡的训练集。
- **双级知识蒸馏（Dual Knowledge Distillation）**：  
  - **特征级蒸馏**：冻结前一任务的BP分支作为教师网络，计算学生网络瓶颈层输出的均方误差（MSE）。  
  - **预测级蒸馏**：将学生网络的预测中旧类概率归一化，与学生网络的旧类概率计算KL散度。  
  - 总损失：\(Loss = Loss_{Main} + \alpha Loss_{Feat} + \beta Loss_{Prob}\)，其中 \(\alpha, \beta\) 设为1。

### 算法流程（文字描述）
1. **基类训练**：用TSM骨干+瓶颈层+分类头在基类数据上训练50 epochs，得到特征提取器。
2. **解析分支初始化**：用基类所有数据求解线性层闭式解，得到解析分类器。
3. **重参数化初始化**：复制解析分支权重作为BP分支，用基类数据训练流式判别器和BP分支10 epochs。
4. **增量任务循环**（每到来一个新任务k）：
   - 冻结特征提取器，用RLS更新解析分类器（只使用当前任务数据）。
   - 从高斯记忆库中采样旧类伪特征，与当前新类特征拼接。
   - 运行动态重参数化前向过程，计算主损失与双级蒸馏损失，联合优化BP分支和判别器。
5. **推理**：使用动态融合后的模型对所有已知类别进行分类。

## 3. 实验设计

### 数据集与场景
- **UCF101**：101个动作类别。基类51类，增量分为10×5、5×10、2×25任务等设置。
- **HMDB51**：51个类别。基类26类，增量分为5×5、1×25任务设置。
- **Something-Something V2**：174类。基类84类，增量分为10×9、5×18、3×30、1×90等长任务设置。

### Benchmark
- 遵循TCD（Park et al. 2021）协议，使用固定随机种子划分任务。
- 评估指标：平均增量准确率（Accuracy）、遗忘率（Forgetting Rate）、性能下降率（PD）。
- 对比方法分为两类：
  - **基于重放（exemplar-based）**：iCaRL、UCIR、PODNet、TCD、SNRO、FrameMaker、HCE等。
  - **无样本（exemplar-free）**：普通微调（Finetuning）、LwFMC、LwM、DBK等。
  - 上界：Oracle（使用所有历史数据）。

### 结果简述
- 在三个数据集的所有设置下，**SFCL（无样本）**均超越所有无样本方法，并优于大多数基于重放的方法，甚至在某些设置下接近Oracle。
- 长任务场景（如UCF101 1×50、SSV2 1×90）中，准确率提升高达**30.39%**，遗忘率极低。

## 4. 资源与算力
- 论文中**未明确说明**所使用的GPU型号、数量及总训练时长。
- 实现细节：骨干网络使用TSM（ResNet34或ResNet50），ImageNet预训练；batch size：UCF101为32，HMDB51和SSV2为64；学习率1e-3，SGD动量0.9，权重衰减5e-4；基类训练50 epochs，重参数化训练10 epochs。
- 推理和增量更新开销较小（解析分支为闭式解，无需大量梯度计算），但未提供具体时间对比。

## 5. 实验数量与充分性

### 实验数量
- **主要对比**：在UCF101（3种增量设置）、HMDB51（2种设置）、SSV2（4种设置）上进行了全面比较，共9组对比。
- **消融实验**：针对KRM的GMS、特征蒸馏、概率蒸馏三个组件进行了消融（表4）。
- **分析实验**：比较解析学习与BP分支的优势与不足（表3），可视化长任务准确率曲线（图5）和logit分布（图6）以展示任务-最近偏差缓解。
- **长任务鲁棒性**：额外测试UCF101 1×50、SSV2 3×30和1×90任务（表5）。

### 充分性与公平性判断
- **充分性**：数据集覆盖小（HMDB51）到大（SSV2），增量设置包括少步长和多步长，对比方法包含主流基线，消融实验覆盖关键组件，实验设计较为全面。
- **公平性**：所有方法均在相同骨干（TSM）和协议下比较，且本文方法不使用任何历史数据（无样本），对比的有样本方法默认保存一定数量样本，因此公平性较好。但未与最新的其他无样本方法（如基于提示或记忆网络的方法）直接对比，略显不足。
- **偏差风险**：实验仅在三个数据集上进行，且均为受限场景（预定义任务顺序），缺乏开放世界或域漂移场景验证；此外，重复实验次数未说明（仅提固定随机种子3次或1次），统计稳定性可能不足。

## 6. 主要结论与发现
- **无样本持续学习可行**：SFCL在不存储任何历史样本的情况下，性能显著优于现有无样本方法，并超越多数有样本方法，证明了慢-快协作学习架构的有效性。
- **适应性与稳定性的平衡**：慢速分支（BP）使模型能快速适应新动作，快速分支（解析）有效保留旧知识，动态融合由流式判别器自动调节，避免了传统方法的严重遗忘或适应不足。
- **长任务鲁棒性突出**：在长达90个增量任务的长序列中，SFCL准确率下降非常缓慢，遗忘率低，展示了卓越的稳定性。
- **任务-最近偏差显著缓解**：通过KRM（伪特征生成+蒸馏），模型对旧类和新类的预测概率分布更加均衡，克服了传统方法偏向新类的问题。

## 7. 优点
- **方法创新性**：首次将梯度驱动深度学习与解析学习在连续学习框架中深度结合，提出动态重参数化机制，且解析分支可通过RLS递归更新而无需存储历史数据，思路新颖。
- **实用性强**：无需样本重放，保护隐私，降低存储开销，适合实际部署。
- **实验全面**：在多个数据集、多种增量设置、不同评价指标下验证，并包含详细消融和分析，结论可信度较高。
- **可视化分析**：通过logit分布可视化直观展示任务-最近偏差的缓解，增加说服力。

## 8. 不足与局限
- **实验覆盖范围有限**：仅评估视频动作识别任务，未验证其他模态（如图像分类、音频识别）或跨模态场景，泛化性未知。
- **计算与推理效率未讨论**：虽然解析分支计算量小，但双分支结构及动态重参数化增加了前向和训练开销；未与基线方法对比训练/推理时间或参数量。
- **对特征提取器依赖较强**：解析分支依赖固定特征提取器（训练后冻结），若特征分布在新任务中变化大，可能限制性能。这种方法在类增量设置下假设特征质量足够好。
- **缺少与最新无样本方法的对比**：如基于提示学习（L2P, DualPrompt等）或基于结构的方法，对比方法多为2022-2024年间的基线。
- **伪特征采样的潜在偏差**：高斯假设可能不准确，对于长尾分布或复杂模态，协方差估计可能出现偏差，导致伪特征质量下降。
- **超参数敏感性**：权重α、β固定为1，未进行敏感性分析；流式判别器结构也未见详细探讨。

（完）
