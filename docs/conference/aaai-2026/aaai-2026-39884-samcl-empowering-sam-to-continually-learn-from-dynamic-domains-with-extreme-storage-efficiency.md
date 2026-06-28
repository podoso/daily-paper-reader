---
title: "SAMCL: Empowering SAM to Continually Learn from Dynamic Domains with Extreme Storage Efficiency"
title_zh: SAMCL：赋能SAM以极高存储效率持续学习动态域
authors: "Zeqing Wang, Kangye Ji, Di Wang, Haibin Zhang, Fei Cheng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39884/43845"
tags: ["query:continual"]
score: 8.0
evidence: SAM的持续学习方法避免灾难性遗忘
tldr: SAM在开放域动态场景中微调易导致灾难性遗忘。本文提出SAMCL方法，将增量知识分解为独立模块并训练选择器推理时调用。通过AugModule和数据增强解决了模块学习和存储效率挑战。实验证明SAMCL在多种域上保持高性能且存储开销极低。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: SAM在开放域中简单微调会导致灾难性遗忘，无法持续学习新域。
method: 将增量知识分解为独立模块，训练选择器动态选择合适模块，并引入数据增强优化模块学习。
result: 在多个动态域上保持SAM高性能，同时存储效率显著优于现有方法。
conclusion: SAMCL实现了高效持续学习，适用于开放世界视觉模型。
---

## Abstract
Segment Anything Model (SAM) struggles in open-world scenarios with diverse domains. In such settings, naive fine-tuning with a well-designed learning module is inadequate and often causes catastrophic forgetting issue when learning incrementally. To address this issue, we propose a novel continual learning (CL) method for SAM, termed SAMCL. Rather than relying on a fixed learning module, our method decomposes incremental knowledge into separate modules and trains a selector to choose the appropriate one during inference. However, this intuitive design introduces two key challenges: ensuring effective module learning and selection, and managing storage as tasks accumulate. To tackle these, we introduce two components: AugModule and Module Selector. AugModule reduces the storage of the popular LoRA learning module by sharing parameters across layers while maintaining accuracy. It also employs heatmaps—generated from point prompts—to further enhance domain adaptation with minimal additional cost.
Module Selector leverages the observation that SAM’s embeddings can effectively distinguish domains, enabling high selection accuracy by training on low-consumed embeddings instead of raw images.
Experiments show that SAMCL outperforms state-of-the-art methods, achieving only 0.19% forgetting and at least 2.5% gain on unseen domains. Each AugModule requires just 0.233 MB, reducing storage by at least 24.3% over other fine-tuning approaches. The buffer storage for Module Selector is further reduced by up to 256x.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

Segment Anything Model（SAM）在封闭集预训练中表现优异，但在开放世界动态场景中，面对多样化域（如伪装、阴影、医学图像）时，简单微调会导致**灾难性遗忘**——学习新域时严重丢失旧域知识。现有方法要么依赖固定学习模块（如SAM-Adapter），要么采用重放或正则化策略，但存在存储开销大或知识干扰严重的问题。因此，论文旨在为SAM设计一种**极致的存储效率下实现持续学习**的方法，使其能在不断涌现的新域中学习、保持已有知识，并具备向未见域迁移的能力。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
将增量知识分解为**独立的模块**（每个域对应一个AugModule），并训练一个**轻量级选择器（Module Selector）**，在推理时自动选择最合适的模块，从而避免任务间干扰，消除灾难性遗忘。

### 关键技术细节
- **AugModule**：由两部分组成
  - **SLoRA**（Shared LoRA）：在所有层共享一个低秩矩阵A，每个层仅保留独立的矩阵B。相比标准LoRA，参数存储减半（0.233 MB vs 0.30 MB），且性能相当甚至更优。
  - **Prompt Augmentation**：将点提示转化为热图，通过线性层对齐维度后注入图像编码器的所有SLoRA中，增强域适应能力，无需训练掩码解码器。
  公式：Y_i = W_i X_i + B_i (A X_i + P)，其中P为提示热图。

- **Module Selector**：由一个四层MLP组成，训练时仅使用从图像编码器中间块（第6块）提取的低维嵌入（如768维），而非原始图像。选择器通过交叉熵损失训练，推理时根据输入图像的嵌入自动选择对应模块。存储嵌入相比原始图像减少256倍（SAM）或512倍（SAM2）。

- **训练与推理流程**：训练新域时，新增一个AugModule，同时收集少量嵌入更新选择器；推理时，先通过选择器确定域ID，再加载对应模块进行推理。此外，通过COCO子集训练一个“虚拟模块”实现回退到原始SAM。

## 3. 实验设计

- **数据集**：5个具有挑战性的域，伪装（COD、CAMO）、阴影（ISTD）、医学（ISIC、Kvasir）。默认顺序：Kvasir → CAMO → ISTD → ISIC → COD。
- **评估指标**：平均精度（AA）、遗忘度量（FM）、前向迁移（FT），基于mIoU、mF1、mMAE。
- **对比方法**：
  - 常规SAM微调：SAM-Adapter、SAM-LST、AutoSAM
  - 通用持续学习方法（基于LoRA）：EWC、ER、DER
  - 架构基础方法：O-LoRA
  - 持续分割方法：SPPA、LAG
  - SAM专属持续学习：MoDA + HQ-SAM
  - 同时测试了SAM和SAM2版本。
- **消融实验**：验证AugModule（SLoRA vs 其他LoRA变体）、Module Selector（有/无）的效果；不同模块选择位置（图像编码器块号）；不同任务顺序下的鲁棒性（6种随机顺序）。

## 4. 资源与算力

文中未明确说明具体的GPU型号、数量及训练时长。仅提到：
- SAM批次大小8，SAM2批次大小16。
- SAMCL使用AdamW优化器，学习率0.005，余弦衰减。
- 每个域训练20个epoch，选择器训练25个epoch。
- 未报告推理时间或总计算量。

## 5. 实验数量与充分性

- 主要对比实验（表1）：使用5个域，在SAM和SAM2上均进行了对比，覆盖12种以上方法。
- 鲁棒性分析（图6）：变换6种任务顺序，与ER和MoDA对比。
- 消融实验（表2、表3、图3、图7、图8）：分别验证SLoRA、Prompt Augmentation、Module Selector的作用；测试不同存储嵌入数量、不同选择块位置等。
- 附录中提供了更多可视化结果和数据集上的逐域详细指标。

**充分性评价**：实验设计较为全面，覆盖了多个域、多种基线、多个评估维度和消融条件。但缺少与其他最先进持续分割方法（如基于蒸馏的方法）的直接对比，且所有域均属于图像级分割任务，未涉及视频或3D数据。

**客观性与公平性**：对比方法均采用官方或广泛认可的配置（如LoRA秩=10，重放样本数300等），且在同一代码框架下实现，较为公平。

## 6. 论文的主要结论与发现

- SAMCL在持续学习性能上显著优于所有对比方法：AA最高（mIoU 0.836），**遗忘率仅0.19%**（FM = 0.0019），前向迁移提升至少2.5%。
- 存储效率极高：每个AugModule仅0.233 MB（SAM）或0.079 MB（SAM2），相比LoRA减少24.3%以上；选择器缓冲存储比存储原始图像减少256倍。
- SLoRA共享矩阵A的设计在不损失精度的情况下大幅减少参数；Prompt Augmentation能有效提升域适应能力。
- Module Selector仅需少量嵌入即可实现高精度域识别（准确率接近100%），并且能够自动为未见域选择最相关的已学模块，实现知识迁移。

## 7. 优点

- **创新性强**：提出SLoRA（跨层共享低秩矩阵）和Prompt Augmentation（点提示转热图）两种轻量化适配手段，结合统一。
- **存储极低**：模块化设计加基于嵌入的选择器，使得每个域额外存储仅几十KB到几百KB，极具实际部署价值。
- **持续学习性能优异**：几乎零遗忘，且具备正向迁移能力，优于现有所有持续分割方法。
- **通用性**：同时适用于SAM和SAM2，结构简单，易于扩展。

## 8. 不足与局限

- **计算资源未报告**：缺少GPU型号、训练总时长等关键信息，无法量化训练成本。
- **域覆盖有限**：仅测试了伪装、阴影、医学三个域，未涉及遥感、自动驾驶、自然场景等常见域，通用性仍需验证。
- **依赖预训练嵌入的区分能力**：Module Selector的有效性高度依赖SAM图像编码器能否天然区分不同域，若域间特征高度相似，选择器可能失效（论文未讨论此风险）。
- **负迁移风险**：当未见域与多个已学域均不相似时，选择器可能随机选择，导致次优性能（论文仅展示了正向案例）。
- **未与最新蒸馏/正则化方法对比**：如PLOP、MiB等持续语义分割方法未被纳入。
- **提示依赖**：实验中使用点提示，但在实际应用中可能无法获取准确提示，影响方法有效性。

（完）
