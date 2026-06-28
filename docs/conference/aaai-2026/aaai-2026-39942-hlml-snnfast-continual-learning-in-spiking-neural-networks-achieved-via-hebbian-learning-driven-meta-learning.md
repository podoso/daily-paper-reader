---
title: HLML-SNN：Fast Continual Learning in Spiking Neural Networks Achieved via Hebbian Learning-Driven Meta-Learning
title_zh: HLML-SNN：通过赫布学习驱动的元学习实现脉冲神经网络快速持续学习
authors: "Jiangshuai Xu, Peiyun Xue, Jiacheng Song, Xuhui Huang, Qingshan Hou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39942/43903"
tags: ["query:continual"]
score: 9.0
evidence: 提出基于脉冲神经网络的持续学习框架以解决灾难性遗忘
tldr: 本文提出HLML-SNN框架，结合赫布可塑性与元学习，模拟大脑皮层-海马记忆机制，在脉冲神经网络中实现快速持续学习。短时阶段通过样本级赫布学习快速适应新输入，长时阶段通过任务级元学习巩固知识。实验证明该方法在资源受限场景下高效缓解灾难性遗忘，兼具生物合理性与能效优势。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续学习方法在资源受限场景下计算成本高昂，而脉冲神经网络具有生物合理性和能效优势。
method: 集成赫布可塑性与元学习的双阶段框架：短时赫布学习快速适应，长时元学习巩固知识。
result: 在持续学习基准上，HLML-SNN以低计算开销达到领先的遗忘抑制效果。
conclusion: 为节能型持续学习提供了神经形态计算新途径。
---

## Abstract
Catastrophic forgetting remains a fundamental barrier to artificial continual learning (CL) - a capability innate to humans. Existing CL methods often incur prohibitive computational costs in resource-constrained scenarios. Spiking neural networks (SNNs), with their biological plausibility and energy efficiency, offer distinct advantages for CL. Inspired by cortico-hippocampal memory mechanisms, we propose a spiking neural network framework integrating Hebbian plasticity with meta-learning, named HLML-SNN. This architecture emulates a dual-phase CL process: (1) In the short-term phase, sample-level Hebbian learning rapidly adapts to new inputs through local synaptic updates; (2) In the long-term phase, task-level meta-learning optimizes cross-task parameters using consolidated synaptic weights, mimicking cortical memory integration to refine shared representations and initialize subsequent Hebbian learning. HLML-SNN incrementally transforms short-term adaptations into stable long-term knowledge, where the synergy of rapid synaptic updates and meta-driven global optimization enables efficient continual learning while balancing stability and plasticity. Empirical results establish HLML-SNN's state-of-the-art performance across split-MNIST/CIFAR10/CIFAR100/TinyImageNet while markedly reducing training time compared to existing methods, demonstrating substantial practical potential for rapid deployment scenarios. The code and appendix are available on https://github.com/JiangshuaiXu/HLML SNN.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：人工持续学习（CL）面临灾难性遗忘——学习新任务时覆盖旧知识，导致性能骤降。现有CL方法（正则化、重放、动态架构）计算成本高，难以在资源受限场景下快速部署。
- **研究动机**：人类大脑具备持续学习能力，源于皮层-海马回路的多尺度记忆机制（快速编码与缓慢巩固）及突触可塑性（赫布可塑性）。脉冲神经网络（SNN）因其生物合理性和能效优势，被视为实现高效CL的潜在载体。
- **整体含义**：本文受皮层-海马记忆机制启发，提出结合赫布可塑性与元学习的SNN框架（HLML-SNN），旨在模拟双阶段记忆过程，实现快速适应与稳定保留的平衡，为资源约束下的持续学习提供新范式。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **双阶段学习机制**：短时阶段通过赫布学习（局部突触可塑性）快速适应新任务；长时阶段通过元学习（全局参数优化）巩固跨任务知识，模拟大脑中记忆从海马向皮层转移的过程。

### 关键技术细节
- **脉冲神经元模型**：使用LIF（Leaky Integrate-and-Fire）神经元，通过替代梯度解决不可微问题。
- **赫布学习（短时阶段）**：
  - 计算预-后突触神经元在T个时间步内的平均发放率：$\overline{pre} = \frac{1}{T}\sum_t pre(t)$, $\overline{post} = \frac{1}{T}\sum_t post(t)$。
  - 权重更新：$\Delta w(k) = \eta_h(k) \cdot \overline{post}^\top \overline{pre} \cdot \frac{1}{B}$，基于共发放强化原则。
  - 偏置更新：$b(k+1) = b(k) + \eta_h(k) \cdot \overline{post} \cdot \frac{1}{B}$，调节神经元兴奋性。
  - 学习率指数衰减：$\eta_h(k) = \eta_{h0} \cdot \gamma^k$，先快速调整后精细收敛。
- **元学习（长时阶段）**：
  - 元参数 $\theta_{\text{meta}}$ 为SNN线性层参数（权重和偏置）。
  - 对第m个任务，从元参数克隆得到快速参数 $\theta_{\text{fast}}^{(m,0)}$，在支持集上执行K步赫布学习得到 $\theta_{\text{fast}}^{(m,K)}$。
  - 在查询集上计算交叉熵损失 $L_m$，通过梯度下降更新元参数：$\theta_{\text{meta}} \leftarrow \theta_{\text{meta}} - \eta_{\text{meta}} \cdot \nabla_{\theta_{\text{meta}}} L_m$。梯度简化为 $\nabla_{\theta_{\text{meta}}} L_m = \nabla_{\theta_{\text{fast}}^{(m,K)}} L_m$（因恒等映射）。
  - 元学习率使用余弦退火调度。
- **协同机制**：元参数提供高质量初始化，赫布学习快速微调，元学习根据微调结果优化全局参数，形成闭环。

### 算法流程（文字描述）
- 预训练特征提取器（如ResNet）提取特征，经泊松编码输入SNN。
- 对每个任务：① 从当前元参数克隆快速参数；② 在支持集上重复K步赫布学习（权重和偏置衰减更新）；③ 在查询集上计算损失；④ 反向传播更新元参数；⑤ 进入下一任务。

## 3. 实验设计

### 数据集与任务配置
- **split-MNIST**：5个任务，每任务2类。
- **split-CIFAR10**：5个任务，每任务2类。
- **split-CIFAR100**：10任务（每任务10类）/ 20任务（每任务5类）。
- **split-TinyImageNet**：10任务（每任务20类）/ 20任务（每任务10类），含数据隔离（W）和非隔离（N）设置。
- 每任务训练数据按2:8分为支持集和查询集。

### 基准方法
- **经典方法**：SI、LWF（正则化）、ER、A-GEM（重放）、XdG、SepNet（动态架构）。
- **先进方法**：SNN方法（HLOP、CH-HNN）、ANN方法（EsaCL、HALRP、RKR）。
- 对比指标：平均准确率（%）、训练时间（秒）。

### 网络架构
- 单隐层SNN，隐层神经元数：MNIST/CIFAR10用256，CIFAR100/TinyImageNet用1024。
- 使用预训练ResNet作为特征提取器（除HLOP外）。

## 4. 资源与算力

- **硬件**：单个NVIDIA RTX4090 GPU。
- **软件**：基于PyTorch框架实现。
- **训练时长**：文中以秒为单位给出了各方法在各数据集上的训练时间（例如split-CIFAR10上HLML-SNN耗时7.91秒，而ER耗时39.54秒）。未提供整体训练总时长或具体迭代次数。

## 5. 实验数量与充分性

- **对比实验**：在4个基准数据集上与多种经典/先进方法进行了系统对比（共约12种基准对比），所有实验报告了5次随机种子的均值与方差。
- **超参数敏感性分析**：考察了元学习率（1e-2至1e-5）和时间步长T（2,4,10）对性能的影响。
- **消融实验**：在split-CIFAR10和10-split-CIFAR100上，分别移除赫布学习（HL）、移除元学习（ML）、保留完整双阶段（HLML），并对比了无任何机制的基模型。
- **机制分析**：
  - 计算任务间参数更新方向的相关性热图（检验正交性）。
  - 分析每轮更新方向与已有参数累积向量的角度变化。
  - 额外验证：加入显式正交约束未提升性能但训练时间增加4倍。
- **充分性与公平性**：实验覆盖多个复杂度和规模的数据集，对比方法涵盖主流范式，超参数设置明确（如初始赫布学习率0.00001，衰减因子0.95，内循环步数K=3），使用相同预训练特征提取器（除HLOP外），多次随机种子保证统计稳定性。整体设计较为充分、客观、公平。

## 6. 主要结论与发现

- HLML-SNN在split-MNIST（99.1%）、split-CIFAR10（93.1%）、10-split-CIFAR100（90.2%）、10-split-TinyImageNet（80.1%非隔离）上均达到SOTA，显著优于经典方法和大多数先进方法。
- 训练时间大幅降低：相比重放/正则化方法减少3~7.5倍，相比HLOP减少约420~770倍，相比CH-HNN减少7~8倍。
- 赫布学习提供快速适应（加速训练），元学习防止灾难性遗忘（维持高准确率），两者协同优于单一机制。
- 参数更新自动趋于正交（任务间相关性接近0，角度接近90°），无需显式正则化即可减少干扰，实现自然遗忘抑制。

## 7. 优点

- **生物合理性**：模拟皮层-海马记忆双阶段机制，可解释性强。
- **高效性**：无需内存重放或网络动态扩展，训练时间极短，适合资源受限场景和快速部署。
- **性能优异**：在复杂数据集（CIFAR100、TinyImageNet）上精度领先，且遗忘幅度小。
- **参数正交性自然涌现**：无需额外约束，降低设计复杂度。
- **消融与机制分析完整**：验证了各模块的必要性和正交性假说，增强了可信度。
- **开源代码与附录**：提供代码和补充材料，便于复现。

## 8. 不足与局限

- **预训练依赖性**：方法依赖于预训练特征提取器（PFE），在无预训练的端到端场景下效果未知（文中仅HLOP无PFE但性能较低）。
- **场景覆盖有限**：仅在任务增量学习（Task-IL）下验证，未测试类增量（Class-IL）或域增量（Domain-IL）等更复杂场景。
- **超参数敏感**：元学习率、时间步长等对性能影响较大，需手动调优（如最优元学习率为1e-4）。
- **时间步长权衡**：较长时间步数提升精度但增加训练时间，需根据任务复杂度折衷。
- **对比方法局限**：与最新SNN方法（如ALADE-SNN）对比不够充分（文中仅提及但未列入主表），且部分方法（如EsaCL）未报告标准差。
- **潜在偏差**：支持集与查询集划分（2:8）及预训练数据（如TinyImageNet中类别重叠）可能引入偏差，虽通过隔离设置缓解但非完美。
- **理论深度**：虽证明参数自动正交，但未给出严格理论保证或泛化界。

（完）
