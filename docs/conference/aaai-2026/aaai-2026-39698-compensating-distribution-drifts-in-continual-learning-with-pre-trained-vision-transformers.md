---
title: Compensating Distribution Drifts in Continual Learning with Pre-trained Vision Transformers
title_zh: 使用预训练视觉Transformer补偿持续学习中的分布漂移
authors: "Xuan Rao, Simian Xu, Zheng Li, Bo Zhao, Derong Liu, Mingming Ha, Cesare Alippi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39698/43659"
tags: ["query:continual"]
score: 8.0
evidence: 持续学习中的分布漂移补偿
tldr: 针对类增量学习中的分布漂移问题，提出顺序学习与漂移补偿（SLDC）方法，通过引入潜在空间转换算子对齐旧类分布，缓解灾难性遗忘，提升了预训练ViT模型在持续学习中的分类效果。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有顺序微调策略易受分布漂移影响，导致旧类特征分布与新模型不匹配，降低分类器性能。
method: 提出SLDC框架，学习一个潜在空间转换算子将旧模型特征对齐到新模型，再进行分类器细化。
result: 在多个类增量基准上验证，SLDC显著优于现有方法，有效缓解遗忘并保持高精度。
conclusion: 通过明确补偿分布漂移，实现了更稳定的持续学习，适用于预训练视觉模型的增量场景。
---

## Abstract
Recent advances have shown that sequential fine-tuning (SeqFT) of pre-trained vision transformers (ViTs), followed by classifier refinement using approximate distributions of class features, can be an effective strategy for class-incremental learning (CIL). However, this approach is susceptible to
distribution drift, caused by the sequential optimization of shared backbone parameters. This results in a mismatch between the distributions of the previously learned classes and that of the updated model, ultimately degrading the effectiveness of classifier performance over time. To address this issue, we introduce a latent space transition operator and propose Sequential Learning with Drift Compensation (SLDC). SLDC aims to align feature distributions across tasks to mitigate the impact of drift. First, we present a linear variant of SLDC, which learns a linear operator by solving a regularized least-squares problem that maps features before and after fine-tuning. Next, we extend this with a weakly nonlinear SLDC variant, which assumes that the ideal transition operator lies between purely linear and fully nonlinear transformations. This is implemented using learnable, weakly nonlinear mappings that balance flexibility and generalization. To further reduce representation drift, we apply knowledge distillation (KD) in both algorithmic variants. Extensive experiments on standard CIL benchmarks demonstrate that SLDC significantly improves the performance of SeqFT. Notably, by combining KD to address representation drift with SLDC to compensate distribution drift, SeqFT achieves performance comparable to joint training across all evaluated datasets.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **核心问题**：在基于预训练视觉Transformer（ViT）的类增量学习（CIL）中，顺序微调（SeqFT）通过连续优化共享骨干参数来适应新任务，但会导致**分布漂移**——旧任务类别在旧模型下的特征分布与新模型下的特征分布不匹配，从而逐渐降低后续分类器细化的效果，造成灾难性遗忘。
- **整体含义**：现有方法多通过蒸馏、模型集成或梯度投影来抑制漂移，而该论文另辟蹊径，旨在**在漂移已经发生后，显式地补偿其负面影响**，通过建模连续任务之间特征空间的演化转换，使得旧类分布能够对齐到新特征空间，进而改善分类器性能。

## 2. 方法论：核心思想、关键技术细节
### 核心思想
- 引入**潜在空间转换算子（Latent Space Transition Operator）** `Pt-1→t`，该算子将任务t-1的特征空间映射到任务t的特征空间。
- 关键假设：类特征可近似为多元高斯分布（均值+协方差）。
- 通过利用当前任务数据（无需旧数据）来近似该算子，从而补偿旧类分布的漂移。

### 关键技术细节（两种变体 + 蒸馏增强）
- **线性变体 α1-SLDC**：
  - 对当前任务数据在旧模型和新模型上提取的特征进行L2归一化。
  - 通过求解**正则化最小二乘问题**（式6/7）学习线性变换矩阵 `At ∈ R^(d×d)`。
  - 针对样本数不足问题，采用启发式重加权（式8）将 `At` 向单位矩阵收缩。
  - 使用 `μc ← At μc`，`Σc ← At Σc At^T` 更新旧类分布。
- **弱非线性变体 α2-SLDC**：
  - 假设理想算子介于纯线性与全非线性之间，构造弱非线性变换（式10）：`T(f) = c1 A f + c2 ψ(f)`，其中 `A` 为可学习矩阵，`ψ` 为两层MLP（ReLU），`c1,c2≥0, c1+c2=1`。
  - 优化目标（式11）：最小化预测特征与真实特征的F范数，并加入正则项 `γα2(c1-1)^2` 控制非线性贡献。
  - 通过从原高斯分布采样、经 `T()` 变换后重新计算均值和协方差来更新旧类分布。
- **蒸馏增强变体 β1/β2-SLDC**：
  - 在微调过程中加入特征级蒸馏损失（式14）和特征范数正则化（式15），以限制表示过度变化。
- **辅助数据增强（ADE）**：在样本不足时，引入任意无标签辅助数据（如CIFAR-10、SVHN、ImageNet）来改进算子估计，不违反无样例CIL约束。

## 3. 实验设计
### 数据集与场景
- 四个标准CIL基准：**CIFAR-100**（100类）、**ImageNet-R**（200类）、**CUB-200**（200类，细粒度鸟类）、**Cars-196**（196类，细粒度车型）。
- 场景：每个数据集均匀划分为**10个任务**（无特殊强调）；还扩展到20任务长序列及混合CIL（四个数据集各作为一个任务）。
- 预训练模型：**ViT-B/16** 两种初始化——自监督MoCo-V3（ImageNet-1K）与监督ImageNet-21K。

### 基准方法与对比
- 对比基线：BiC、LwF、RanPAC、SLCA、SLCA++、CoMA、CoFiMA、SeqFT、SeqKD、MLPDC（MLP分布补偿）。
- 度量：**Inc-Acc**（所有任务平均准确率）和**Last-Acc**（增量结束后最终准确率）。
- 公平性：所有实验基于PILOT框架，采用一致随机种子。

## 4. 资源与算力
- **论文未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。
- 仅提及优化器为Adam，学习率 `10^(-4)`，权重衰减 `3×10^(-5)`，LoRA秩为4。
- 可从代码仓库推测为单卡或多卡实验，但无详细数据，属于**信息缺失**。

## 5. 实验数量与充分性
- **实验数量丰富**：
  - 主表两个（表1：MoCo-V3预训练；表2：Sup-21K预训练），每个表覆盖四个数据集、十多种方法。
  - 额外实验：20任务长序列（图2）、混合CIL（图3）、超参数消融（αtemp、γα2，图4-5）、ADE样本选择（图6）。
  - 蒸馏对比、MLPDC对比、ADE增强对比等。
- **充分性与公平性**：
  - 实验设置遵循主流协议，对比方法均为近年SOTA，使用相同框架。
  - 消融实验较为全面，验证了各模块贡献。
  - 但**缺乏统计显著性检验**（如p值），仅报告了均值与标准差。
- **总体评价**：实验覆盖广泛，设计合理，结论可信度较高，但算力细节缺失。

## 6. 主要结论与发现
1. 原始SeqFT遗忘严重，SLDC能**大幅提升**其性能（例如α2-SLDC在CUB-200上较SeqFT提升+14.58%）。
2. **弱非线性（α2-SLDC）一致优于线性（α1-SLDC）和纯非线性（MLPDC）**，验证了“算子介于线性与非线性之间”的假设。
3. 蒸馏（β1/β2-SLDC）与SLDC**协同效应显著**，使性能逼近联合训练（差距仅+0.50%至-3.29%）。
4. 辅助数据ADE能**稳定线性变体**（尤其Sup-21K预训练下），并进一步提升弱非线性变体。
5. 在20任务长序列和混合CIL场景下，SLDC同样保持优势。

## 7. 优点
- **创新性**：首次将“分布漂移补偿”概念与特征空间转换算子显式建模，与主流抑制漂移思路互补。
- **实用性**：无需存储旧任务数据（exemplar-free），可即插即用于现有SeqFT/SeqKD方法。
- **设计巧妙**：弱非线性通过可学习系数平衡线性与非线性，避免了过拟合或欠拟合。
- **实验全面**：覆盖多种数据集、预训练模型、序列长度、混合场景及大量消融，验证充分。
- **性能突出**：与蒸馏结合后接近联合训练上界，表明方法已近乎解决PTM-based CIL的遗忘问题。

## 8. 不足与局限
- **线性变体的不稳定性**：在Sup-21K预训练下的细粒度数据集（CUB-200、Cars-196）中，α1-SLDC表现甚至低于SeqFT，需依赖ADE才能稳定（Last-Acc从46.78%提升至73.01%），暴露了线性假设在强迁移场景下的适用性局限。
- **理论深度有限**：对算子性质的探讨仅引用了神经正切核（NTK）理论，但未给出严格证明或收敛性分析。
- **多模态模型未验证**：论文提及开放性问题是SLDC在多模态模型（如CLIP）上的应用，但实验只涉及视觉模型。
- **计算开销**：α2-SLDC需对每个旧类进行蒙特卡洛采样（N=10d），且弱非线性变换训练需端到端优化，可能增加训练成本（未量化比较）。
- **实验覆盖局限**：
  - 未在更大规模数据集（如ImageNet-1K full）或真实长尾场景下验证。
  - 未与其他需要任务身份识别的方法（如L2P、DualPrompt）进行公平比较（论文解释其需要任务预测，但可视为局限性）。
  - 未讨论不同数据顺序对结果的影响（仅提及“类似”）。

（完）
