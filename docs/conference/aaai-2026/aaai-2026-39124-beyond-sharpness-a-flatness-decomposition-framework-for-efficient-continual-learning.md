---
title: "Beyond Sharpness: A Flatness Decomposition Framework for Efficient Continual Learning"
title_zh: 超越锐度：高效持续学习的平坦度分解框架
authors: "Yanan Chen, Tieliang Gong, Yunjiao Zhang, Wen Wen"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39124/43086"
tags: ["query:continual"]
score: 8.0
evidence: 持续学习方法避免遗忘
tldr: 持续学习中锐度感知方法虽能改善泛化，但存在计算开销大的问题。本文提出FLAD框架，将锐度感知扰动分解为梯度对齐和随机噪声分量，仅保留噪声分量进行正则化。在多个持续学习基准上，FLAD在保持性能的同时显著降低了计算成本，为持续学习提供了高效优化手段。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有锐度感知方法在持续学习中计算开销大，且未区分不同扰动分量的贡献。
method: 将锐度感知扰动分解为梯度对齐分量和随机噪声分量，仅使用噪声分量进行平坦度正则化。
result: 在多个持续学习数据集上，FLAD在减少计算量的同时保持了与现有方法相当的准确性。
conclusion: FLAD证明了选择性保留扰动分量可实现高效持续学习。
---

## Abstract
Continual Learning (CL) aims to enable models to sequentially learn multiple tasks without forgetting previous knowledge. Recent studies have shown that optimizing towards flatter loss minima can improve model generalization. However, existing sharpness-aware methods for CL suffer from two key limitations: (1) they treat sharpness regularization as a unified signal without distinguishing the contributions of its components. and (2) they introduce substantial computational overhead that impedes practical deployment. To address these challenges, we propose FLAD, a novel optimization framework that decomposes sharpness-aware perturbations into gradient-aligned and stochastic-noise components, and show that retaining only the noise component promotes generalization. We further introduce a lightweight scheduling scheme that enables FLAD to maintain significant performance gains even under constrained training time. FLAD can be seamlessly integrated into various CL paradigms and consistently outperforms standard and sharpness-aware optimizers in diverse experimental settings, demonstrating its effectiveness and practicality in CL.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

持续学习（Continual Learning, CL）旨在让模型顺序学习多个任务，同时避免灾难性遗忘。近年研究表明，优化至更平坦的损失极小值可以改善模型泛化。现有锐度感知方法（如 SAM、GAM、C-Flat）虽被引入 CL，但存在两大局限：  
- 将锐度正则化视为一个整体信号，未区分其组成部分对泛化的贡献；  
- 引入显著的计算开销（如双梯度或多次前向-后向传播），限制实际部署。  

本文提出 FLAD（Flatness Decomposition）框架，通过分解锐度感知扰动的方向，保留仅对泛化有益的随机噪声分量，并设计轻量调度方案，在保持性能增益的同时大幅降低计算成本。

## 2. 论文提出的方法论：核心思想、关键技术、算法流程

**核心思想**：将零阶锐度（SAM 型）和一阶锐度（GAM 型）的对抗扰动分解为**梯度对齐分量**和**随机噪声分量**，证明只有噪声分量能有效促进模型逃逸尖锐极小值、收敛到平坦区域；梯度对齐分量反而会干扰优化，应被丢弃。

**关键技术细节**：  
- 使用指数移动平均（EMA）估计全批梯度方向 \(\mathbf{m}_t\) 和梯度锐度方向 \(\mathbf{n}_t\)，避免计算全批梯度。  
- 零阶扰动方向：\(\delta_0 = \rho \frac{\hat{\mathbf{g}}_t - \sigma \mathbf{m}_t}{\|\hat{\mathbf{g}}_t - \sigma \mathbf{m}_t\| + c}\)，其中 \(\hat{\mathbf{g}}_t\) 是当前批梯度，\(\sigma\) 是余弦相似度常数。  
- 一阶扰动方向：\(\delta_1 = \rho \frac{\nabla\|\hat{\mathbf{g}}_t\| - \sigma \mathbf{n}_t}{\|\nabla\|\hat{\mathbf{g}}_t\| - \sigma \mathbf{n}_t\| + c}\)，其中 \(\nabla\|\hat{\mathbf{g}}_t\|\) 通过 Hessian-vector product 高效计算。  
- 更新步骤：\(\mathbf{w} = \mathbf{w} - \eta(\mathbf{g}_0 + \gamma \mathbf{g}_1)\)，\(\mathbf{g}_0\)、\(\mathbf{g}_1\) 分别为在扰动点 \(\mathbf{w}+\delta_0\) 和 \(\mathbf{w}+\delta_1\) 处的梯度。

**算法流程（Algorithm 1）**：  
1. 初始化参数和 EMA 缓存；  
2. 对每个任务中的每个批次，计算批梯度 \(\hat{\mathbf{g}}_t\)，更新 EMA \(\mathbf{m}_t\)；  
3. 计算零阶扰动 \(\delta_0\)，在扰动点求梯度 \(\mathbf{g}_0\)；  
4. 通过 Hessian-vector product 计算 \(\nabla\|\hat{\mathbf{g}}_t\|\)，更新 EMA \(\mathbf{n}_t\)；  
5. 计算一阶扰动 \(\delta_1\)，在扰动点求梯度 \(\mathbf{g}_1\)；  
6. 用 \(\mathbf{g}_0 + \gamma \mathbf{g}_1\) 更新参数。  
每一步仅需 2 次前向和 4 次后向传播，计算量显著低于传统 SAM/GAM。

## 3. 实验设计：数据集、基准、对比方法

**数据集**：  
- CIFAR-10（5 任务，每任务 2 类）  
- CIFAR-100（5 任务/8 任务，每任务 20 类/10 类）  
- Tiny-ImageNet（8 任务，每任务 25 类）

**基准（CL 方法）**：覆盖三种主流范式  
- 记忆回放型：Replay、iCaRL、PODNet  
- 正则化型：WA  
- 扩展型：FOSTER、MEMO

**对比优化器**：SGD（基优化器）、SAM、GAM、C-Flat、FLAD（本文方法）。每种 CL 方法分别与上述优化器组合，共 6×4=24 种组合，每个设置重复 3 次。

**评估指标**：最终平均准确率（Acc）和任意时刻平均准确率（AAA）。

## 4. 资源与算力

论文明确说明：**所有实验在 RTX 4090Ti GPU（96GB RAM）上完成**，但未给出 GPU 数量及总训练时长。文中提及 FLAD 仅需 2 前向 + 4 后向传播/步，且通过部分应用策略（仅 10%~30% 的 epochs 启用 FLAD）可进一步降低开销，相比全量 SAM/GAM 节省至少 50% 的计算时间。

## 5. 实验数量与充分性

实验数量充足，覆盖全面：  
- **主实验结果**（Table 1）：6 种 CL 方法 × 4 种优化器 × 3 个数据集 × 多个任务数（如 CIFAR-100 有 N=5 和 N=10），共 72 个主要设置 + 重复；  
- **消融实验**（图 3）：ρ 和 γ 参数敏感性、分解策略对比（零阶/一阶各 6 种方法）；  
- **泛化分析**（图 2）：Hessian 特征值分布、损失景观可视化、Tr(HΣ) 演化；  
- **收敛与计算开销**（图 4、图 5）：不同 epoch 占比下的准确率与时间对比。  

实验设计公平：所有方法使用相同架构、超参数调优一致（λ ∈ {0.5,0.7,0.9}），统计 3 次重复。结论稳健。

## 6. 论文的主要结论与发现

- **普适性**：FLAD 在所有 6 种 CL 方法上均一致提升性能（平均 AAA 提升约 0.97%~1.90%），不依赖具体 CL 机制；  
- **分解有效性**：仅保留随机噪声分量即可获得最优泛化，梯度对齐分量会干扰优化（图 1a）；  
- **平坦性**：FLAD 训练出的模型具有更小的 Hessian 最大特征值和迹，损失景观更平坦（图 2）；  
- **高效性**：只需 10%~20% 的 epochs 应用 FLAD 即可取得接近全量使用的性能，计算时间优于 SAM/GAM/C-Flat（图 5）；  
- **收敛速度**：FLAD 收敛最快，最终准确率最高（图 5a）。

## 7. 优点：方法与实验设计的亮点

- **创新性**：首次将锐度感知扰动分解为有明确几何意义的两个分量，并理论验证噪声分量的关键作用；  
- **计算效率**：通过 EMA 近似全梯度 + 仅使用噪声分量 + 可部分应用，极大降低开销；  
- **兼容性**：即插即用，无需修改 CL 模型架构，可直接替换优化器；  
- **实验全面**：覆盖 3 个数据集、6 种 CL 范式、多种优化器，消融和可视化充分，结论可信。

## 8. 不足与局限

- **额外超参数**：需调节 λ₀、λ₁、σ 等，文中 σ 设为固定常数，可能需针对不同任务微调；  
- **EMA 近似误差**：用 EMA 近似全梯度在非稳态 CL 场景中可能存在偏差，尤其当任务分布剧烈变化时；  
- **数据集规模有限**：仅在 CIFAR/Tiny-ImageNet 上验证，未见大规模数据集（如 ImageNet-1K full）或在线/流式 CL 场景；  
- **理论证明范围**：定理 1 仅针对非凸随机优化，未讨论凸情形或全局收敛性；  
- **计算仍高于 SGD**：虽然远低于 SAM，但仍需 2 前向 4 后向，相比 SGD 仍有 2 倍左右增加（但若部分应用则持平）。

（完）
