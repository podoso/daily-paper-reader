---
title: Decoupling Continual Semantic Segmentation
title_zh: 解耦持续语义分割
authors: "Yifu Guo, Yuquan Lu, Wentao Zhang, Zishan Xu, Dexia Chen, Siyu Zhang, Yizhe Zhang, Ruixuan Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/42446/46407"
tags: ["query:continual"]
score: 9.0
evidence: 直接解决持续学习中的灾难性遗忘问题
tldr: 针对持续语义分割中的灾难性遗忘问题，本文提出DecoupleCSS两阶段框架，将类别感知检测与类别无关分割解耦。第一阶段利用LoRA适配的预训练文本和图像编码器，有效保留旧知识同时学习新类别。实验表明该方法在平衡保留与可塑性方面优于现有单阶段方法，为密集预测任务的持续学习提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续语义分割方法因分割掩码与类别标签紧耦合，导致新旧类别学习相互干扰、遗忘严重。
method: 提出两阶段框架DecoupleCSS，先进行类别无关分割，再进行类别感知检测，使用LoRA适配预训练编码器。
result: 在多个持续语义分割基准上，该方法显著提升旧类保留能力，同时保持新类学习性能。
conclusion: 解耦策略有效缓解了灾难性遗忘，为持续语义分割提供了更优的保留-可塑性权衡。
---

## Abstract
Continual Semantic Segmentation (CSS) requires learning new classes without forgetting previously acquired knowledge, addressing the fundamental challenge of catastrophic forgetting in dense prediction tasks. However, existing CSS methods typically employ single-stage encoder-decoder architectures where segmentation masks and class labels are tightly coupled, leading to interference between old and new class learning and suboptimal retention-plasticity balance. We introduce DecoupleCSS, a novel two-stage framework for CSS. By decoupling class-aware detection from class-agnostic segmentation, DecoupleCSS enables more effective continual learning, preserving past knowledge while learning new classes. The first stage leverages pre-trained text and image encoders, adapted using LoRA, to encode class-specific information and generate location-aware prompts. In the second stage, the Segment Anything Model (SAM) is employed to produce precise segmentation masks, ensuring that segmentation knowledge is shared across both new and previous classes. This approach improves the balance between retention and adaptability in CSS, achieving state-of-the-art performance across a variety of challenging tasks.

---

## 论文详细总结（自动生成）

## 论文中文总结：Decoupling Continual Semantic Segmentation

### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：持续语义分割（CSS）面临灾难性遗忘，在密集预测任务中学习新类别时容易丢失旧知识。
- **现有方法的不足**：大多数现有CSS方法采用单阶段编码器-解码器架构，分割掩码与类别标签在模型参数中紧耦合。这种耦合导致新旧类别学习相互干扰，造成“保留-可塑性”平衡欠佳。
- **本文的目标**：提出一种两阶段框架DecoupleCSS，通过将类别感知检测与类别无关分割解耦，实现更有效的持续学习，在保留旧知识的同时学习新类别。

### 2. 方法论
- **核心思想**：将分割过程分解为两个独立阶段：第一阶段检测图像中包含哪些前景类别（类别感知），第二阶段对每个检测到的类别生成精确的分割掩码（类别无关）。
- **第一阶段：语言驱动的任务感知类别检测（LTCD）**
  - 使用预训练的文本编码器（如CLIP）和图像编码器（Swin Transformer作为Grounding DINO骨干），通过LoRA添加任务特定的可适应模块。
  - 为每个类别生成多个描述性短语（由LLM生成），经文本编码后得到多个文本嵌入；根据与输入图像视觉特征的余弦相似度自适应加权聚合，得到最终类别嵌入。
  - 文本-图像交叉注意力模块（含LoRA）输出增强的视觉嵌入V'和文本嵌入E'。
  - 计算亲和矩阵Si = cos(V', E'^T)，经阈值τ过滤弱关联，选取与至少一类强关联的视觉token及其对应类别。
- **第二阶段：类别特定提示生成（SPG）与类别无关分割（CAS）**
  - SPG模块对每个类选取的视觉token进行展平、填充/截断至固定长度，添加可学习的类别特定嵌入，通过类别特定的两层MLP生成m个提示令牌pk（位置提示）。
  - SAM（冻结）接收这些提示，生成每个类别的二进制掩码及置信度，最后按置信度聚合得到最终语义分割图。
- **训练**：只训练任务特定的LoRA和类别特定的pGen MLP；损失函数包括SAM的原始分割损失和多标签非对称损失。

### 3. 实验设计
- **数据集与场景**：
  - PASCAL VOC 2012（20类）和ADE20K（150类）。
  - 采用重叠协议（overlapped setting），即当前任务图像可能包含旧类、新类和未来类，未来类被标注为背景。
  - 多种任务划分设置：19-1（2任务）、15-5（2任务）、15-1（6任务）、10-1（11任务），以及ADE20K上的100-50（2任务）、100-10（6任务）、100-5（11任务）。
  - 额外挑战性设置：2-2（10任务）、4-2（9任务）、4-4（5任务）。
- **对比方法**：
  - 数据重放类：MicroSeg-M, SSUL-M, RECALL, SATS-M, IPSeg-M等。
  - 无数据重放类：MiB, PLOP, MiB+NeST, PLOP+NeST, MicroSeg, CoMFormer, CoMasTRe, IPSeg, SATS, BARM, SSUL等。
- **评价指标**：mIoU（类平均交并比），分别报告旧类、新类和总体均值。

### 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量或训练时长。仅在实现细节中提及使用AdamW优化器，PASCAL VOC上训练5个epoch，ADE20K上训练20个epoch。
- 作者提供了代码仓库（GitHub），但未披露具体算力配置。

### 5. 实验数量与充分性
- **主实验**：在PASCAL VOC 2012的四种常见设置和ADE20K的三种设置上进行了全面评估，结果表明显著超越所有对比方法。
- **消融实验**：验证了三个关键组件（LoRA、类别特定pGen、语义聚合）的必要性；还将类别特定pGen替换为共享pGen，性能大幅下降。
- **敏感性分析**：对LoRA秩、MLP隐藏层数、LLM描述短语数量进行了范围测试，显示方法鲁棒。
- **附加实验**：
  - 将SAM作为后处理模块应用到现有CSS方法，提升有限（<6% mIoU），验证了本文SPG的必要性。
  - 使用Grounding DINO的GT框作为提示，接近本文性能（84% vs 83% on VOC），说明SPG有效。
  - 计算成本分析：单任务推理0.3s/图，6任务约1.9s/图；参数增长少（每个类别增加8MB，所有LoRA共22.18MB，占模型总大小0.62%）。
- **充分性评价**：实验覆盖多个数据集、多种设置，消融和敏感性完备，对比方法包含近年SOTA，结果客观。未额外比较弱监督或类增量设置，但符合CSS标准。

### 6. 主要结论与发现
- DecoupleCSS在所有测试设置上达到了最优性能，尤其在挑战性更大的10-1、2-2等设置中优势巨大（如10-1总体83.12% mIoU，超出IPSeg 4.52%）。
- 解耦策略有效避免了传统单阶段方法中的新旧类别干扰，实现了出色的“保留-可塑性”平衡。
- 利用预训练的VLM和SAM，将持续学习限制在检测阶段，分割知识跨类别共享，降低了遗忘风险。

### 7. 优点
- **框架创新**：首次将CSS解耦为类别感知检测和类别无关分割，提供全新视角，模块化设计利于扩展。
- **利用基础模型**：充分挖掘SAM和CLIP的能力，分割质量高，且冻结SAM避免其参数遗忘。
- **参数高效**：仅使用轻量LoRA和MLP适配器，每任务新增参数少，避免存储爆炸。
- **鲁棒性与泛化性**：在PASCAL和ADE20K上均SOTA，且在极不平衡的设置（如10-1）中仍保持高旧类准确率。

### 8. 不足与局限
- **推理延迟**：由于需要顺序切换任务特定的LoRA和pGen模块，推理时间随任务数线性增长（6任务约1.9s/图），不适合实时应用。作者提到可与S-LoRA服务机制结合，但未充分验证实时场景。
- **依赖预训练模型**：强依赖SAM和CLIP的质量，若后续任务类别与预训练知识分布差异大，可能影响泛化。
- **参数增长**：尽管每类参数少，但随类别数增加（ADE20K 150类）pGen模块总参数量仍可观；未讨论内存上限。
- **实验覆盖**：未在更多样化的场景（如自动驾驶、医学影像）上验证，也未与基于动态网络的方法（如CoMasTRe）在完全相同的代码基线下比较（部分复现来自作者实现）。
- **隐私风险**：虽然不保存原始数据，但LoRA参数可能隐含任务特定信息，未讨论隐私保护。

（完）
