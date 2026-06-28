---
title: Adapt Before Continual Learning
title_zh: 在持续学习之前进行适配
authors: "Aojun Lu, Tao Feng, Hangjie Yuan, Chunhui Ding, Yanan Sun"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39584/43545"
tags: ["query:continual"]
score: 8.0
evidence: 持续学习前适配预训练模型以平衡可塑性与稳定性
tldr: 针对持续学习中冻结预训练模型限制可塑性而微调导致遗忘的矛盾，提出在学习前对预训练模型进行适配，在新的数据分布上获得更好的初始特征，再结合简单正则化方法显著提升持续学习性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有PTM-based CL要么冻结模型限制可塑性，要么顺序微调导致灾难性遗忘，缺乏有效平衡。
method: 提出在持续学习流程之前额外适配预训练模型，使其初始特征更适应新任务，再应用简单正则化。
result: 在多种持续学习基准上，该方法显著提升性能，尤其当新任务分布与预训练差异大时。
conclusion: 提前适配是一种简单有效的策略，能够同时提升可塑性和稳定性。
---

## Abstract
Continual Learning (CL) seeks to enable neural networks to incrementally acquire new knowledge (plasticity) while retaining existing knowledge (stability). Although pre-trained models (PTMs) have provided a strong foundation for CL, existing approaches face a fundamental challenge in balancing these two competing objectives. Current methods typically address stability by freezing the PTM backbone, which severely limits the model's plasticity, particularly when incoming data distribution diverges largely from the pre-training data. Alternatively, sequentially fine-tuning the entire PTM can adapt to new knowledge but often leads to catastrophic forgetting, highlighting the critical stability-plasticity trade-off in PTM-based CL. To address this limitation, we propose Adapting PTMs before the core CL process (ACL), a novel framework that introduces a plug-and-play adaptation phase prior to learning each new task. During this phase, ACL refines the PTM backbone by aligning embeddings with their original class prototypes while distancing them from irrelevant classes. This mechanism theoretically and empirically demonstrates desirable balance between stability and plasticity, significantly improving CL performance across benchmarks and integrated methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在基于预训练模型（PTM）的持续学习（CL）中，存在严重的稳定性-可塑性权衡困境。现有方法要么冻结PTM骨干以保持稳定性，但严重限制了模型对分布偏移较大新任务的可塑性；要么对整个PTM进行顺序微调，虽能适应新知识，却常导致灾难性遗忘。
- **研究动机**：在开放世界场景下，数据流式到达，要求模型增量学习新知识（可塑性）同时保留旧知识（稳定性）。PTM虽提供了强基础，但其特征空间并非对所有下游任务最优，尤其是当新任务分布与预训练数据分布差异显著时，冻结的固定特征表示成为瓶颈。因此需要一种机制，在不破坏PTM基础知识的前提下，将其特征空间重新对准新任务。
- **整体含义**：作者提出在学习每个新任务之前，先对PTM进行适应性调整（Adapt Before Continual Learning, ACL），作为即插即用的预处理阶段，以改善稳定性-可塑性平衡。

## 2. 论文提出的方法论

### 核心思想

- 在每轮CL核心学习过程之前，引入一个独立的适配阶段，对PTM骨干和轻量模块进行微调，使特征空间更有利于当前任务的判别，同时通过机制设计保持已有知识。
- 适配损失函数采用原型对比学习形式：鼓励当前样本的嵌入向其对应类别的原始原型（基于原PTM计算）靠近，同时远离其他类原型。这种设计能同时提升可塑性（降低当前任务分类误差上界）和稳定性（隐式正则化特征偏移）。

### 关键技术细节

1. **模型分解**：CL模型表示为 \( f(x) = C(\phi(x)) \)，其中 \(\phi\) 为PTM骨干，\(C\) 为分类头。现有方法通常冻结 \(\phi\)，仅训练额外模块\(\Theta\)（如prompt、adapter）和分类头。
2. **ACL两阶段流程**（以第k个任务为例）：
   - **Phase 1：适配**：给定数据集 \(D_k\)，对前一轮骨干 \(\phi_{k-1}\) 和模块 \(\Theta_{k-1}\) 进行适配，得到 \(\phi^*_{k-1}, \Theta^*_{k-1}\)。适配算法A使用ACL损失。
   - **Phase 2：核心学习**：冻结适配后的骨干 \(\phi^*_{k-1}\)，仅训练分类头 \(C_{k-1}\) 和适配后的模块 \(\Theta^*_{k-1}\) 来学习当前任务的分类。
3. **ACL损失函数**（公式3）：
   \[
   L_{\text{ACL}}(x_i, y_i) = -\log \frac{\exp(\cos(\phi^*(x_i), p_{y_i})/\tau)}{\sum_j \exp(\cos(\phi^*(x_i), p_j)/\tau)}
   \]
   其中 \(p_c = \mathbb{E}_{(x,y)\in D_k, y=c}[\phi(x)]\) 为基于原PTM计算的类原型，所有嵌入和原型经过\(\ell_2\)归一化到单位超球面。\(\tau\)为温度参数。
4. **理论分析**：
   - **可塑性**：通过命题1证明，最小化ACL损失等价于最小化当前任务分类误差的概率上界。
   - **稳定性**：通过命题2证明，ACL损失隐式约束了适配前后特征偏差，因为原型是原特征空间中最小化期望欧氏距离的点，适配过程迫使新特征靠近原型，从而避免过大偏移。

### 算法伪代码（文字说明）

- 输入：初始PTM骨干\(\phi_0\)、轻量模块\(\Theta_0\)、分类头\(C_0\)、增量数据集\(\{D_1,\dots,D_K\}\)。
- 对每个任务k=1到K：
  1. 获取训练集\(D_k\);
  2. 使用ACL损失优化\(\phi_{k-1}\)和\(\Theta_{k-1}\)得到\(\phi^*_{k-1}, \Theta^*_{k-1}\);
  3. 保存\(\phi_k = \phi^*_{k-1}\);
  4. 冻结\(\phi_k\)，使用核心CL方法（如L2P）优化\(\Theta^*_{k-1}\)和\(C_{k-1}\)得到\(\Theta_k, C_k\)。

## 3. 实验设计

### 数据集与场景

- **数据集**：ImageNet-R（包含不同风格/渲染的鲁棒性图像）和ImageNet-A（自然对抗样本），两者与ImageNet预训练数据存在显著领域差异。每个数据集被平均划分为多个不重叠的任务。
- **任务配置**：两种增量设置：Inc-10（10个类/任务，共20个任务）和Inc-20（20个类/任务，共10个任务）。
- **场景**：类增量学习（Class Incremental Learning），无旧任务数据回放。

### 基准方法（对比方法）

- **六种SOTA PTM-based CL方法**：L2P, DualPrompt, RanPAC, FeCAM, SSIAT, MOS。ACL作为即插即用组件集成到这些方法中。
- **Aper系列**：仅在第一个任务上使用标准分类损失对PTM进行适配的方法，包括Finetune, VPT-Deep, VPT-Shallow, SSF, Adapter。
- **SimpleCIL**：使用余弦分类器且训练后不再更新的基线方法。

### 评估指标

- **LA (Last Accuracy)**：最终任务后所有已学类的准确率。
- **AIA (Average Incremental Accuracy)**：每学完一个任务后平均准确率。

## 4. 资源与算力

- 论文在“Limitations”部分明确指出：适配整个PTM会引入额外的GPU内存消耗，在实验设置（Tab.1）中约为 **7GB**。
- 未说明具体GPU型号、数量及训练时长。仅提到每个增量任务限制适配阶段为1个训练周期（epoch）以减少计算开销。

## 5. 实验数量与充分性

### 实验组数

- **主实验**（Tab.1）：6种CL方法 × 4个数据集配置（ImageNet-R-Inc20/Inc10, ImageNet-A-Inc20/Inc10） × 5次随机任务顺序 → 共6×4×5=120次实验，报告均值±标准差。涵盖多种方法类型（prompt-based, adapter-based, head-only等）。
- **与Aper对比**（Tab.2）：6种Aper变体 vs ACL，在相同数据集配置下。
- **消融实验**（Fig.3）：三种消融变体（改用标准分类损失、仅第一任务适配、仅适配轻量模块冻结骨干），集成到6种方法中。
- **适配epoch消融**（Fig.4）：在RanPAC和SSIAT上测试不同epoch数（1-4）下的性能，同时对比全PTM适配 vs 仅轻量模块适配。
- **可视化**（Fig.5）：t-SNE特征分布和Grad-CAM热力图。
- **额外骨干验证**（Tab.3）：使用ViT-B/16-IN21K（仅在ImageNet21K预训练）在ImageNet-A-Inc20上测试6种CL方法。
- **视觉语言模型验证**（Tab.4）：使用CLIP的Continual CLIP方法，在ImageNet-R-Inc20上对比。

### 充分性评价

- **全面性**：覆盖了主流PTM-based CL方法（6种），多种领域偏移数据集，多种任务配置，多种预训练骨干（IN21K, CLIP）。
- **公平性**：遵循开源库PILOT的超参数设置，每项实验报告5次随机种子结果，避免任务顺序偏差。
- **消融设计合理**：系统性地隔离了损失函数、适配步骤、适配组件的影响。
- **对比公平**：与Aper系列对比时，采用相同的数据集和简单分类器（SimpleCIL）以保证基线一致。
- **潜在的不足**：仅在图像分类数据集上验证，未涉及NLP或多模态其他任务；未与基于回放的经典方法（如GEM、iCaRL）对比（但论文聚焦PTM-based方法，可以理解）。

## 6. 论文的主要结论与发现

1. **现有PTM-based CL方法的瓶颈**：冻结PTM骨干导致可塑性不足，尤其是当新任务数据分布与预训练数据分布有明显偏移时。
2. **ACL的有效性**：通过在学习每个新任务之前进行适配（使用原型对比损失），可以同时提升可塑性（降低当前任务分类误差）和保持稳定性（约束特征偏移），从而获得更好的稳定性-可塑性平衡。
3. **性能提升显著**：在ImageNet-R和ImageNet-A上，ACL为六种SOTA方法带来稳定且显著的性能提升（LA提升最高达7.87%，AIA提升最高达5.98%）；在ImageNet-R-Inc20的Inc-10设置下，AIA提升甚至接近10%相对值。
4. **优于单次适配**：与仅在第一个任务上适配的Aper方法相比，ACL在各任务持续适配效果更好，在所有设置上均超越Aper最佳变体。
5. **通用性**：ACL不仅适用于不同PTM骨干（ViT-B/16-IN1K, ViT-B/16-IN21K），也适用于视觉语言模型（CLIP）。
6. **特性效果**：Grad-CAM可视化显示，ACL能使模型更关注与类别相关的区域，而冻结模型易关注背景等无关区域。

## 7. 优点

- **方法论创新性**：提出在核心CL过程之前进行适配的新范式，而非修改CL算法本身，易于作为即插即用组件集成到任意现有方法。
- **理论支撑**：从概率角度证明了ACL损失同时优化可塑性和稳定性的上界，提供了坚实的理论基础。
- **实验设计严谨**：涵盖多种代表性方法、多种数据集配置、多次随机种子、多种消融实验，证据链完整。
- **高效性**：每个任务仅需1个epoch的适配，计算开销可控（额外7GB显存，可以接受）。
- **泛化能力强**：在视觉语言模型（CLIP）上也验证了有效性，暗示跨模态拓展潜力。
- **开源代码**：提供代码链接，便于复现和社区应用。

## 8. 不足与局限

- **计算资源开销**：额外适配阶段需要约7GB显存，对于资源受限场景可能不友好（尽管只增加1 epoch训练）。
- **实验覆盖范围**：仅在图像分类数据集上验证，未涉及其他CL基准（如CORe50、CIFAR-100、Split TinyImageNet）或更复杂的任务（如语义分割、目标检测）。
- **未与回放类方法对比**：虽然聚焦PTM-based方法，但缺少与经典回放+微调方法（如iCaRL、ER）的对比，无法评估ACL相对于传统方法在平衡稳定性-可塑性方面的绝对优势。
- **未讨论超参数敏感性**：温度系数τ固定为0.1，未给出不同τ下的性能波动。
- **潜在过拟合风险**：适配阶段使用当前任务数据，若任务数据量极少，可能有欠拟合或过拟合问题；论文未测试数据量极小的情况。
- **理论证明的局限性**：命题1和2依赖于余弦分类器和单位超球面假设，对线性分类器或其他分类器是否严格成立未讨论（但实验表明对线性分类器L2P等仍有效）。
- **长任务序列可扩展性**：论文实验最多20个任务，未测试更长的任务序列（如50或100个任务），适配阶段累积的影响未分析。

（完）
