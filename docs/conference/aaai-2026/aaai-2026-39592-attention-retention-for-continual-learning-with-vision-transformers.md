---
title: Attention Retention for Continual Learning with Vision Transformers
title_zh: 视觉Transformer持续学习中的注意力保留
authors: "Yue Lu, Xiangyu Zhou, Shizhou Zhang, Yinghui Xing, Guoqiang Liang, Wencong Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39592/43553"
tags: ["query:continual"]
score: 8.0
evidence: 面向持续学习的注意力保留框架
tldr: 发现视觉Transformer中注意力漂移是灾难性遗忘的关键原因，提出注意力保留框架，通过反向传播时修改梯度来约束注意力的迁移，从而保持旧任务注意力模式。在多个持续学习基准上验证了有效性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有研究未明确注意力漂移在ViT持续学习中的影响，导致遗忘问题难以解释。
method: 提出注意力保留框架，通过两层过程：提取旧任务注意力图，并在反向传播时修改梯度以维持注意力。
result: 实验证明该方法显著减少遗忘，在各类持续学习设置中均优于基线。
conclusion: 注意力漂移是ViT遗忘的重要成因，约束注意力是缓解遗忘的有效手段。
---

## Abstract
Continual learning (CL) empowers AI systems to progressively acquire knowledge from non-stationary data streams. However, catastrophic forgetting remains a critical challenge. In this work, we identify attention drift in Vision Transformers as a primary source of catastrophic forgetting, where the attention to previously learned visual concepts shifts significantly after learning new tasks. Inspired by neuroscientific insights into the selective attention in the human visual system, we propose a novel attention-retaining framework to mitigate forgetting in CL. Our method constrains attention drift by explicitly modifying gradients during backpropagation through a two-step process: 1) extracting attention maps of the previous task using a layer-wise rollout mechanism and generating instance-adaptive binary masks, and 2) when learning a new task, applying these masks to zero out gradients associated with previous attention regions, thereby preventing disruption of learned visual concepts. For compatibility with modern optimizers, the gradient masking process is further enhanced by scaling parameter updates proportionally to maintain their relative magnitudes. Experiments and visualizations demonstrate the effectiveness of our method in mitigating catastrophic forgetting and preserving visual concepts. It achieves state-of-the-art performance and exhibits robust generalizability across diverse CL scenarios.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：持续学习（Continual Learning, CL）中的灾难性遗忘问题。尤其是在视觉Transformer（ViT）中，模型在学习新任务时，对先前学习过的视觉概念的注意力会发生显著偏移（attention drift），导致忘记旧知识。
- **研究动机**：人类视觉系统中存在选择性注意力机制，该机制能够稳定地锚定在先前学过的概念的特征上，即使学习新概念也不会被破坏。受此生物启发，作者认为防止注意力漂移是克服灾难性遗忘的关键。
- **背景**：现有方法包括重放、正则化、扩展等，但均未明确针对ViT中的注意力漂移进行约束。本文首次将注意力漂移识别为ViT中灾难性遗忘的主要来源，并提出保留注意力以缓解遗忘的框架。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：在反向传播过程中，通过显式修改梯度来约束注意力漂移，使得模型在学习新任务时不会改变先前任务中关键的注意力区域。
- **关键技术细节**：
  - **两步过程**：
    1. **自适应掩码生成**：完成上一个任务 \(T_{t-1}\) 后，提取注意力图，并生成实例自适应的二进制掩码 \(\bar{M}_{t-1}\)，标记出需要保留的注意力区域（掩码中这些区域设为0，其余为1）。
    2. **梯度掩码**：学习新任务 \(T_t\) 时，将掩码与当前任务的注意力矩阵 \(A_t\) 或 \(S_t\) 进行逐元素乘法，使得梯度中与旧任务注意力区域相关的部分被置零，从而阻止参数更新破坏旧注意力。
  - **注意力图提取**：采用**逐层展开（layer-wise rollout）** 机制，即从第一层到当前层逐层累积注意力矩阵，并取类别token与图像token之间的注意力权重，得到每个层的注意力图。
  - **自适应阈值**：由于softmax的锐化效应，注意力值中高值区域与背景区分明显。通过寻找排序后注意力值曲线二阶导数最小的点作为阈值，从而动态确定保留区域，无需固定阈值。
  - **优化器兼容**：为了与现代优化器（如Adam）兼容，进一步对参数更新进行比例缩放，使得掩码后的更新量与原始更新量的比值等于对应梯度的比值，即 \(\Delta W'_{\theta.t} = \frac{\nabla(W_{\theta.t})'}{\nabla(W_{\theta.t})} \odot \Delta W_{\theta.t}\)。
- **公式流程**（文字说明）：
  - 训练完旧任务后，计算逐层rollout注意力图并生成二进制掩码。
  - 训练新任务时，在反向传播中，将掩码与梯度对应的注意力矩阵相乘，得到掩码后的梯度。
  - 然后计算原始梯度下的参数更新量，再根据上述比例公式调整更新量，最终用调整后的更新量更新参数。

## 3. 实验设计：使用的数据集/场景、benchmark、对比方法

- **数据集与场景**：采用类增量学习（Class-Incremental Learning, CIL）场景，包括四个基准：
  - 10-split ImageNet-R
  - 20-split ImageNet-R
  - 10-split CIFAR-100
  - 10-split DomainNet
- **对比方法**：包括近年来（2022-2025）的多种方法，如 L2P、DualPrompt、CODA-Prompt、APG、ESN、OS-Prompt++、EvoPrompt、PGP、OVOR-Deep、ConvPrompt、InfLoRA、EASE、CPrompt、VPT-CPG、CAPrompt、SD-LoRA、BiLoRA、LoRA-DRS、CPrompt-KAC、SEMA 等，以及 Seq-FT 基线（仅微调无防遗忘）。
- **评价指标**：最终平均准确率（Acc.）和最终平均遗忘（Forgetting）。

## 4. 资源与算力

- **文中未明确说明**：论文没有提及所使用的GPU型号、数量、训练时长等具体算力资源。仅在实验设置中提到优化器为Adam，学习率等超参数，但未提供硬件信息。

## 5. 实验数量与充分性

- **实验数量**：
  - 主表（Table 1）在四个基准上与15+种最新方法对比。
  - 消融实验（Table 2）：对注意力图提取方式（raw attention、naive rollout、layer-wise rollout）和阈值策略（固定 vs 自适应）进行6种组合比较。
  - 掩码区域消融（Table 3）：对比随机掩码、非注意力掩码、注意力掩码。
  - 泛化实验（Table 4）：使用不同预训练权重（DINO-1k、iBOT-1k）进行实验。
  - 长序列实验（Table 5）：在50-split和100-split的ImageNet-R和DomainNet上测试。
  - 可视化分析（Figure 1）：定性展示注意力的保留情况，并定量计算注意力漂移值。
- **充分性与公平性**：实验较为充分，覆盖了多个数据集、多种任务划分、多种基线方法，消融实验验证了每个设计选择的有效性。对比方法结果尽量从原文或可复现来源获取，并标注了复现标记。但缺少在真实大规模数据集（如完整ImageNet）上的实验，以及不同ViT架构（如ViT-L）的验证。

## 6. 论文的主要结论与发现

- 注意力漂移是ViT中灾难性遗忘的主要来源，通过约束注意力漂移可以有效缓解遗忘。
- 提出的ARCL-ViT方法在四个基准上均达到或超越了现有最先进方法，准确率最高提升3.7%，平均提升1.8%。
- 与Seq-FT基线相比，准确率提升37%，遗忘减少46%。
- 该方法对不同预训练权重（自监督、有监督）和长序列任务具有良好泛化性。
- 可视化表明该方法有效保持了旧任务的注意力图案，定量分析显示注意力漂移值最低（6.0%），远低于Seq-FT（25.9%）。

## 7. 优点

- **创新性**：首次明确将注意力漂移作为ViT持续学习遗忘的根本原因，并提出直接约束注意力的方法。
- **方法简洁有效**：通过梯度掩码实现，无需存储旧数据，属于正则化方法，存储开销低。
- **自适应阈值**：避免了手动调参，且能适应不同图像中判别区域的大小差异。
- **优化器兼容**：对参数更新进行比例缩放，保证了与现代优化器（如Adam）的兼容性，训练稳定。
- **实验充分**：包含多个数据集、多种设置、消融实验和可视化分析，验证了方法的有效性和泛化性。
- **性能优异**：在多个基准上达到SOTA，尤其在长序列设置下显著领先。

## 8. 不足与局限

- **未提供算力资源**：缺少GPU型号、训练时间等细节，不利于复现和评估效率。
- **实验覆盖有限**：仅在ViT-B/16上验证，未测试其他ViT变体（如ViT-L、Swin Transformer）或其他骨干网络（如ConvNeXt）。
- **缺少真实大规模数据集**：实验限于ImageNet-R（200类）和CIFAR-100，未在完整ImageNet-1k或更大规模数据集上评估。
- **遗忘度较高**：在长序列设置下，虽然准确率高，但遗忘值仍较高（如100-split DomainNet遗忘25.63%），说明在极端序列下仍有遗忘。
- **依赖预训练**：方法基于预训练ViT，未探讨从头训练的场景。
- **仅针对注意力漂移**：可能忽略了其他导致遗忘的因素（如特征表示漂移），但论文通过实验证明了其有效性，并未声称解决所有问题。
- **未讨论计算开销**：梯度掩码和注意力图提取可能增加额外计算成本，但论文未分析。

（完）
