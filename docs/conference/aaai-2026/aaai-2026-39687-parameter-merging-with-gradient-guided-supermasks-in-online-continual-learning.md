---
title: Parameter Merging with Gradient-Guided Supermasks in Online Continual Learning
title_zh: 基于梯度引导超掩码的参数合并用于在线持续学习
authors: "Benliu Qiu, Heqian Qiu, Lanxiao Wang, Taijin Zhao, Yu Dai, Lili Pan, Hongliang Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39687/43648"
tags: ["query:continual"]
score: 9.0
evidence: 基于参数合并的在线持续学习解决灾难性遗忘
tldr: 在线持续学习面临灾难性遗忘与学习不充分的权衡。本文从贝叶斯视角建立损失与参数关系，提出基于梯度引导超掩码的参数合并方法，利用一阶和二阶梯度信息确定新旧模型合并权重，超越传统梯度下降。实验证明该方法在多个数据流上有效缓解遗忘并提升学习性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 在线持续学习因数据只能读取一次，面临遗忘与不学习的权衡。
method: 利用一阶和二阶梯度信息构建超掩码，决定新旧模型参数的合并权重。
result: 在多个在线持续学习基准上取得最佳权衡，遗忘显著降低。
conclusion: 参数合并结合梯度信息为在线持续学习提供了一种高效无遗忘的更新方式。
---

## Abstract
Online continual learning (OCL) aims at learning a non-stationary data stream in a way of reading each data sample only once, and hence suffers from the trade-off of catastrophic forgetting and insufficient learning. In this work, we firstly analytically establish relationship between loss functions and model parameters from the Bayesian perspective. Based on our analysis, we subsequently propose a parameter merging method with gradient-guided supermasks. Our method leverages 1-order and 2-order gradient information to construct supermasks that determine the merging weights between the old and new models. Our method performs direct arithmetic operations on parameters to update models, beyond traditional gradient descent. We further discover that a widely-used premise that 1-order gradients can be negligible is invalid in OCL, due to slow convergence incurred by insufficient learning. Additionally, we utilize a dual-model dual-view distillation strategy that can align output distributions of the new and merged models for each sample, further enhancing model performance. Extensive experiments are conducted on four benchmarks in OCL settings, including CIFAR-10, CIFAR-100, Tiny-ImageNet, and ImageNet-100. Experimental results demonstrate that our method is effective, and achieves a substantial boost over previous methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **背景**：在线持续学习（Online Continual Learning, OCL）要求模型在只能一次性读取每个数据样本的非平稳数据流中学习，面临**灾难性遗忘**（忘记旧知识）与**学习不充分**（新知识难以吸收）之间的权衡。
- **动机**：现有OCL方法多依赖经验回放（rehearsal）或知识蒸馏来间接影响参数更新，忽视了**知识直接存储于参数**这一事实。作者希望探索通过**直接合并参数**来融合新旧知识，从而更直观地解决遗忘与学习不充分问题。
- **核心问题**：如何设计一个基于参数合并的OCL方法，使其既能保留旧知识又能高效学习新知识，同时避免传统梯度下降的局限。

## 2. 方法论
### 核心思想
- 从贝叶斯角度推导OCL的优化目标，证明最小化累计损失等价于最大化后验概率。
- 利用泰勒展开建立损失函数与模型参数之间的解析关系，并基于**跨任务线性（Cross-Task Linearity）** 理论，将损失函数的线性关系传递到参数上，实现参数的直接合并。
- 提出**梯度引导的超掩码（Gradient-Guided Supermasks）**，利用一阶（1-order）和二阶（2-order）梯度信息构建掩码，决定新旧模型参数的合并权重。
- 额外引入**双模型双视角蒸馏策略（dual-model dual-view distillation）**，对齐新模型和合并模型在原始和增强图像上的输出分布，进一步提升性能。

### 关键技术细节
- **参数合并公式**：
  - 最终合并参数 \( \theta_s^* \) 通过两次线性插值得到：
    \[
    \theta_s^* = (1 - \alpha m'') \odot \theta_{s-1}^* \odot (1 - \alpha m') + \alpha m'' \odot \theta_s \odot (1 - \alpha m') + \alpha m' \odot \theta_s
    \]
    其中 \( m' = \sigma\left(\frac{\nabla_\theta L_{1:s}(\theta_{s-1}^*)}{\|\theta_{s-1}^*\|_1}\right) \)，\( m'' = \sigma\left(\frac{\nabla_\theta^2 L_{1:s}(\theta_{s-1}^*)}{\|\theta_{s-1}^*\|_2}\right) \)，\(\sigma\) 为sigmoid函数。
  - 实际上等价于一步线性插值：\( \theta_s^* = (1 - \hat{\alpha}) \theta_{s-1}^* + \hat{\alpha} \theta_s \)，其中 \(\hat{\alpha} = \alpha m' + \alpha m'' - \alpha^2 m' \odot m''\)。
- **梯度信息**：
  - 一阶梯度不可忽略：作者发现OCL中一阶梯度的范数甚至大于二阶梯度，因为单次训练导致收敛缓慢，传统CL中忽略一阶梯度的做法在OCL中不成立。
  - 二阶梯度用Fisher信息矩阵近似，简化计算。
- **优化目标**：
  - 包含交叉熵损失 \( L_{ce} \) 和双模型双视角蒸馏损失 \( L_{kd} \)，总损失 \( L_{total} = L_{ce} + \lambda L_{kd} \)，默认 \(\lambda = 5.5\)。
- **算法流程**：
  1. 初始化内存 \( M \) 和参数 \( \theta_0^* \)。
  2. 对每个任务每个批次：
     - 采样当前批次 \( B_s \) 和记忆批次 \( B_m \)。
     - 计算总损失，反向传播更新得到 \( \theta_s \)。
     - 计算一阶和二阶梯度超掩码 \( m', m'' \)。
     - 根据公式合并得到 \( \theta_s^* \)。
     - 更新内存。

## 3. 实验设计
### 数据集与场景
- **四个基准数据集**：CIFAR-10（5个任务，每任务2类）、CIFAR-100（10个任务，每任务10类）、Tiny-ImageNet（100个任务，每任务2类）、ImageNet-100（20个任务，每任务5类）。
- **场景**：在线类增量学习（online class-incremental learning），每个样本仅训练一次。
- **内存大小**：CIFAR-10上使用500和1000；CIFAR-100上使用1000、2000、5000；Tiny-ImageNet上使用2000、5000、10000；ImageNet-100上使用2000、5000。

### 对比方法
- 主要对比方法：ER、DER++、ERACE、GSA、PCR、OCM、CCLDC、MOSE、S6MOD。其中ER和DER++适用于在线和离线，其余专门为OCL设计。所有方法均采用ResNet18+线性分类器，遵循相同设置。

## 4. 资源与算力
- **文中未明确说明使用的GPU型号、数量及训练时长**。仅提及使用Adam优化器，学习率0.0005，批次大小（新数据10，记忆数据64）。未给出具体硬件配置或训练时间。

## 5. 实验数量与充分性
- **实验数量**：
  - 主要结果：8种不同数据集×内存组合下的平均最终准确率（EndACC）和平均遗忘率（FM），共16组对比。
  - 额外在ImageNet-100上补充结果（表中未列出）。
  - 消融实验：在CIFAR-10（M=500）和CIFAR-100（M=1000）上分析组件贡献（4种变体）。
  - 敏感性分析：对 \(\lambda\) 在6个值上进行测试（CIFAR-100，M=1000）。
  - 可视化分析：损失景观和准确率曲线（线性插值路径）、梯度范数图（图1）、任务准确率矩阵（图2）。
- **充分性与公平性**：
  - 覆盖了多个内存规模和不同复杂度的数据集，比较充分。
  - 所有实验均基于相同骨干网络（ResNet18），遵循统一的训练协议（在线一次训练）。对比方法使用其原始数据增强，作者方法使用额外增强（随机裁剪、翻转、色彩抖动、灰度化）。
  - 结果以5次不同随机种子的均值±标准差报告，具有统计意义。
  - **可能的不公平**：作者的方法使用了额外的数据增强（color jitter, grayscale），而部分基线可能未使用这些增强，可能带来不公平优势。

## 6. 主要结论与发现
- **有效性**：提出的参数合并方法在多数设置下取得最优或次优的EndACC，特别是在小内存条件下增益显著（例如Tiny-ImageNet M=2000时超过第二名4.01%）。
- **抗遗忘能力**：平均遗忘率（FM）较低，在CIFAR-10和CIFAR-100上排名前三，在Tiny-ImageNet上最佳，表明其较好地平衡了记忆与学习。
- **一阶梯度的重要性**：发现一阶梯度在OCL中不可忽略，忽略会导致学习新知识能力下降，验证了图1的观察。
- **两阶超掩码的必要性**：同时使用一阶和二阶超掩码才能达到最佳平衡，单独使用会导致新任务准确率下降（图2）。
- **蒸馏策略的作用**：双模型双视角蒸馏进一步提升了平均准确率，主要贡献于抗遗忘。
- **鲁棒性**：损失景观可视化显示合并后的模型具有更平坦的损失曲面，表明泛化性和鲁棒性更好。
- **参数合并的优越性**：直接对参数进行算术操作（而不是仅依赖梯度下降）能更有效地融入新旧知识。

## 7. 优点
- **理论指导性强**：从贝叶斯优化和泰勒展开出发，推导出参数合并的数学形式，具有清晰的物理解释。
- **方法简洁高效**：通过两次线性插值即可实现参数合并，避免了复杂的网络结构修改或多步优化。
- **发现重要现象**：首次指出OCL中一阶梯度不可忽略，修正了传统CL中的常见假设，对后续研究有指导意义。
- **实验全面**：覆盖多个数据集、内存大小、消融分析和可视化，验证了方法的鲁棒性和有效性。
- **性能优越**：在小内存场景下表现尤为突出，体现了参数合并对缓解遗忘的优势。
- **蒸馏策略创新**：双模型双视图蒸馏充分利用新旧模型和增强数据，进一步提升性能。

## 8. 不足与局限
- **计算开销**：虽然Fisher信息近似简化了二阶梯度计算，但合并过程中仍需计算梯度并构造掩码，可能比纯回放方法增加额外计算成本。文中未分析时间复杂度。
- **实验未提及GPU和训练时间**：缺少实际部署资源需求，限制了实用性评估。
- **数据增强差异**：作者的方法使用了额外的数据增强（color jitter, grayscale），而对比方法可能未使用，导致比较不够完全公平。需要控制增强策略的一致性。
- **场景局限**：仅针对类增量场景，未在任务增量或域增量场景下验证。且任务边界清晰，未测试模糊边界（blurry task boundaries）情况。
- **超参数敏感性**：虽然 \(\lambda\) 的敏感性较低，但 \(\alpha\) 的默认值（0.01）仅在文中提及，未进行系统分析，可能对性能有影响。
- **可解释性**：超掩码的具体含义（哪些参数被合并更多）未深入分析，缺乏对合并后参数行为的定量解释。
- **内存更新策略**：方法基于ER的内存更新（如随机替换），未探索其他先进内存管理策略，可能限制进一步提升。

（完）
