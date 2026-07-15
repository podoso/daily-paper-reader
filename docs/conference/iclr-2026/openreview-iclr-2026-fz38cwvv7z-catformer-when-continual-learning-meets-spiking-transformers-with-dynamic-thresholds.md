---
title: "CATFormer: When Continual Learning Meets Spiking Transformers With Dynamic Thresholds"
title_zh: CATFormer：持续学习与动态阈值脉冲Transformer的结合
authors: "Vaishnavi N, Kartikay Agrawal, Ayon Borthakur"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=fz38cWvV7z"
tags: ["query:continual"]
score: 9.0
evidence: 使用脉冲Transformer和动态阈值的持续学习
tldr: 深度神经网络在增量任务中易发生灾难性遗忘，而大脑能持续学习。本文提出CATFormer，将脉冲神经网络与Transformer结合用于类增量学习，通过动态阈值机制调节神经元激发，有效减轻遗忘。与现有脉冲网络方法相比，CATFormer在多个增量基准上显著降低了性能下降，展示了生物启发模型在持续学习中的潜力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 深度神经网络在增量学习中遗忘严重，而大脑可以持续学习，需要更有效的神经形态方法。
method: 提出CATFormer，融合脉冲神经网络与Transformer，利用动态阈值抑制旧知识干扰。
result: 在类增量学习基准上，CATFormer比现有脉冲网络方法显著提升了准确率，减少了遗忘。
conclusion: 脉冲Transformer结合动态阈值是缓解持续学习遗忘的有前途方向。
---

## Abstract
Although deep neural networks perform extremely well in controlled environments, they fail in real-world scenarios where the data isn't available all at once, and the model requires an update to adapt itself to the new data distribution, which might or might not follow the initial distribution. Previously acquired knowledge is lost during such subsequent updates from new data, a phenomenon commonly known as catastrophic forgetting. In contrast, the brain can learn without such catastrophic forgetting, irrespective of the number of tasks it encounters. Existing spiking neural networks (SNNs) for class-incremental learning (CIL) suffer a sharp performance drop as tasks accumulate. While Parameter-Efficient Fine-Tuning (PEFT) strategies have significantly mitigated this in non-spiking vision transformers by adapting minimal parameters but equivalent mechanisms in the spiking domain remain underexplored. We here introduce CATFormer (Context Adaptive Threshold Transformer), a scalable framework that overcomes this limitation. We observe that the key to preventing forgetting in SNNs lies not only in synaptic plasticity, but also in modulating neuronal excitability. At the core of CATFormer is the \textit{Dynamic Threshold Leaky Integrate-and-Fire (DTLIF)} neuron model, which leverages context-adaptive thresholds as the primary mechanism for knowledge retention. This is paired with a Gated Dynamic Head Selection (G-DHS) mechanism for inference. Extensive evaluation on both static (CIFAR 10/100/Imagenet 100/Tiny-Imagenet 200) and neuromorphic (CIFAR10-DVS/SHD) datasets reveals that CATFormer outperforms existing rehearsal-free CIL algorithms across various task splits, establishing it as an ideal architecture for energy-efficient and class incremental learning.

---

## 论文详细总结（自动生成）

# CATFormer：当持续学习遇上具有动态阈值的脉冲Transformer —— 详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：深度神经网络（DNN）在增量学习场景中面临严重的“灾难性遗忘”，即模型在学习新任务时会丢失先前任务的知识。尽管DNN在静态、一次性提供的数据集上表现优异，但现实世界中数据往往是流式到来，需要模型持续适应新分布，而现有方法无法有效保留旧知识。相比之下，人脑能够持续学习多个任务而不遗忘。
- **研究背景**：现有用于类增量学习（CIL）的脉冲神经网络（SNN）在任务数量增加时性能急剧下降。参数高效微调（PEFT）策略在非脉冲视觉Transformer中通过适配少量参数有效缓解了遗忘，但在脉冲域中类似的机制尚未充分探索。因此，需要一种既能利用脉冲神经元的生物合理性，又能显著减轻遗忘的持续学习方法。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：在脉冲神经网络中防止遗忘的关键不仅在于突触可塑性（synaptic plasticity），还在于调控神经元兴奋性（neuronal excitability）。CATFormer通过引入**动态阈值泄漏整合发放（DTLIF）神经元模型**，利用上下文自适应阈值作为知识保留的主要机制，并结合**门控动态头部选择（G-DHS）机制**进行推理。
- **关键技术细节**：
  - **CATFormer架构**：融合了脉冲神经网络（SNN）与Transformer的缩放框架。它将Transformer的注意力机制与脉冲神经元的时空动态特性结合，形成适合持续学习的模型。
  - **DTLIF神经元模型**：传统LIF神经元具有固定阈值；DTLIF的阈值可根据当前输入上下文动态调整。这种动态阈值使得神经元在遇到新任务时能够调节其发放倾向，从而抑制对旧任务知识的干扰。阈值是上下文可学习的，通过少量额外参数实现知识保留。
  - **门控动态头部选择（G-DHS）**：在推理阶段，根据任务或上下文动态选择Transformer的不同头部，进一步增强对新旧知识的平衡利用。
- **算法流程简述**：
  1. 输入数据经过脉冲编码后进入CATFormer的脉冲Transformer层。
  2. 在每个LIF神经元中，采用DTLIF机制，根据当前输入和任务信息动态调整发放阈值。
  3. 在注意力多头中，利用G-DHS根据任务标识或嵌入选择激活的头部子集。
  4. 整个模型以类增量学习方式训练，不使用经验回放（rehearsal-free），仅通过当前任务数据更新参数，但动态阈值机制避免了旧知识的严重覆盖。

（论文摘要未提供详细公式和算法伪代码，因此此处仅作文字描述。）

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **静态图像数据集**：CIFAR-10、CIFAR-100、ImageNet-100、Tiny-ImageNet-200
  - **神经形态数据集**：CIFAR10-DVS、SHD（Spiking Heidelberg Dataset）
- **基准场景**：类增量学习（Class-Incremental Learning, CIL），即任务按顺序到达，模型在新任务上训练后需能识别所有已见类别，不提供任务ID（需进行任务无关推理）。
- **对比方法**：论文对比了现有的无回放（rehearsal-free）CIL算法，特别关注基于脉冲神经网络的方法。具体方法名称在摘要中未列举，但指出CATFormer优于这些算法。

## 4. 资源与算力

- **提及情况**：论文摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。通常此类论文在正文中会有实验设置部分，但本摘要未包含。因此无法提供具体数值。

## 5. 实验数量与充分性

- **实验数量**：论文在**6个数据集**（4个静态+2个神经形态）上进行了评估，涉及多种任务划分（task splits，即不同数量的增量步数）。此外，CATFormer包含了两个核心组件（DTLIF和G-DHS），可以推断进行了相应的消融实验（例如移除DTLIF或G-DHS）。但摘要未列出具体消融组数。
- **充分性与公平性**：
  - **充分性**：覆盖了常见静态基准和神经形态基准，场景多样，且与现有无回放CIL方法对比，实验设计较为全面。
  - **公平性**：强调与“现有的无回放CIL算法”对比，说明在同一设定下比较（均无回放）。但由于未列出具体对比方法名称和数值，无法完全判断是否包括了最先进的脉冲和非脉冲方法。结论宣称CATFormer“成为节能和类增量学习的理想架构”，实验支撑应该比较充分。

## 6. 论文的主要结论与发现

- CATFormer通过动态阈值脉冲神经元（DTLIF）和门控头部选择（G-DHS），显著缓解了脉冲神经网络在类增量学习中的灾难性遗忘。
- 在静态和神经形态数据集上，CATFormer在多种任务划分下均优于现有无回放CIL算法，性能下降幅度最小。
- 证实了调控神经元兴奋性（而非仅突触可塑性）是防止遗忘的有效生物启发机制。
- 表明脉冲Transformer+动态阈值是持续学习的一个有前途方向，同时保持了脉冲神经网络固有的能效优势。

## 7. 优点（方法或实验设计亮点）

- **生物合理性创新**：首次将动态阈值机制引入脉冲Transformer用于持续学习，与大脑神经元兴奋性调节相对应，具有理论启发价值。
- **无需回放（Rehearsal-free）**：规避了存储旧样本带来的隐私和存储问题，更贴近实际增量场景。
- **可扩展框架**：CATFormer是脉冲Transformer的通用框架，可适配不同规模模型。
- **多数据集验证**：既包含静态图像也包含神经形态数据集，证明了方法的通用性。
- **节能潜力**：基于SNN架构，天然具有低功耗优势，适合边缘设备持续学习。

## 8. 不足与局限

- **实验细节缺失**：摘要未报告具体的任务划分数量（如5-task、10-task等），也未给出准确的性能数值（如平均准确率、遗忘率），无法定量评估效果。
- **对比范围有限**：仅提及与“现有无回放CIL算法”对比，未明确是否包含最先进的非脉冲持续学习方法（如基于提示或正则化的方法）。若仅与脉冲方法对比，则说服力有限。
- **未讨论泛化风险**：在更长任务序列或更复杂数据集（如完整ImageNet）上的表现未知。
- **算力开销未说明**：动态阈值和门控机制引入了额外计算开销，但未与基线方法比较推理/训练效率。
- **消融是否完整**：虽然提到了核心机制，但未在摘要中报告对各组件（DTLIF与G-DHS各自贡献）的量化分析。
- **理论分析不足**：对于为何动态阈值有效缺乏深入的理论解释或数学支持。

（完）
