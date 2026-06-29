---
title: "MOSAIC: Multimodal Object and Semantic Segmentation with Adapter Integration and Contextual Fusion"
title_zh: MOSAIC：通过适配器集成和上下文融合的多模态目标和语义分割
authors: "Alan Chi-Man Lee, Wing-Sun Cheng, Calvin Chun-Kit Chan"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=WK1iMXRTiH"
tags: ["query:multimodal"]
score: 6.0
evidence: 多模态目标与语义分割框架
tldr: 本文提出MOSAIC框架，用于增强多模态RGB-IR目标检测和语义分割。采用Vision Transformer、可变形特征采样、注意力融合模块和上下文增强器，动态对齐和融合RGB-IR特征。在FLIR、LLVIP等基准上取得最先进结果，提升了鲁棒性和精度。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-wk1imxrtih/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 668, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-wk1imxrtih/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 571, \"height\": 215, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-wk1imxrtih/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 882, \"height\": 255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-wk1imxrtih/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 732, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-wk1imxrtih/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 734, \"height\": 854, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-wk1imxrtih/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 734, \"height\": 828, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1455, \"height\": 812, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 733, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1460, \"height\": 623, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 869, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 886, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-wk1imxrtih/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 914, \"height\": 266, \"label\": \"Table\"}]"
motivation: 多模态RGB-IR目标检测与分割面临特征对齐和融合的挑战，现有方法性能不足。
method: 构建基于Vision Transformer的框架，包含可变形特征采样、注意力融合和上下文增强模块。
result: 在多个RGB-IR基准数据集上取得最先进结果，显著提升鲁棒性和准确性。
conclusion: MOSAIC为多模态RGB-IR任务提供了有效的解决方案。
---

## Abstract
We introduce MOSAIC, a novel framework for enhancing multimodal RGB-IR object detection and semantic segmentation. MOSAIC utilizes Vision Transformers and introduces modules like the Deformable Feature Sampling, Feature Attention Fusion Block, and Contextual Feature Enhancer. These components dynamically align and integrate RGB-IR features, capturing multi-scale contextual information to enhance object detection and segmentation tasks. Extensive evaluations demonstrate that MOSAIC achieves state-of-the-art results on FLIR, LLVIP, MFNet and VT-series benchmark datasets, significantly improving robustness and accuracy in RGB-IR downstream tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **多模态RGB-IR视觉任务**：RGB图像在低光照、雾霾等恶劣环境下性能严重下降，而红外（IR）图像虽能稳定捕捉热结构但缺乏纹理细节。两者互补，融合可提升目标检测和语义分割的鲁棒性。
- **现有挑战**：当前方法在模态间特征对齐（如几何错位、视差）和融合效率方面仍存在不足，未能充分挖掘RGB与IR的互补性。典型的交叉注意力机制偏向全局特征融合，缺乏对局部错位和细粒度信息的有效处理。
- **本文目标**：提出MOSAIC框架，通过新型动态对齐和上下文融合模块，在多个下游任务（目标检测、语义分割、显著目标检测）上实现最优性能。

## 2. 方法论：核心思想与关键技术细节

### 总体架构
- 以Vision Transformer（ViT）为骨干，处理IR图像生成特征token。
- 引入**跨模态可变形特征采样池（CDFSP）** 和**上下文特征增强器（CFE）**，实现RGB-IR特征的动态对齐与多尺度融合。

### 关键技术模块
- **Cross-modal Deformable Feature Sampling Pool (CDFSP)**  
  - **Stem块**：使用ResNet类stem分别提取RGB和IR初层特征（1/4分辨率）。
  - **可变形特征采样（DFS）**：通过深度可分离卷积预测RGB与IR之间的偏移量（∆p），并用双线性插值在预测位置采样RGB特征，从而实现粗对齐。
  - **多模态感知融合（MPF）**：将对齐后的RGB与IR特征沿通道均分为四部分，分别用不同卷积核（3×3, 5×5, 7×7等）处理，然后通过**特征注意力融合块（FAFB）** 进行逐对融合。FAFB包含深度可分离卷积、通道注意力（Squeeze-and-Excitation）和空间注意力模块。
  - **特征金字塔**：通过步长2的卷积下采样生成多尺度特征，并投影到相同维度后flatten为token。

- **Contextual Feature Enhancer (CFE)**  
  - 使用多尺度可变形注意力从CDFSP的token中动态采样与ViT token位置相关的特征。
  - 采用类似于GRU的门控机制：对每一层ViT的输出，先用多头注意力建立当前增强特征与上一层的依赖，再通过更新门和重置门逐步融合，实现渐进式特征注入。

- **训练策略**：两阶段训练。第一阶段冻结ViT，只优化CDFSP和CFE；第二阶段联合微调所有参数。

## 3. 实验设计

### 使用的数据集与基准
- **目标检测**：FLIR（对齐版，4129 train/1013 val，3类）、LLVIP（低光照行人检测，12025 train/3463 val）。
- **语义分割**：MFNet（城市场景，1569张，8类，2:1:1划分训练/验证/测试）。
- **显著目标检测**：VT821、VT1000、VT5000（VT5000按2500训练、余下测试）。

### 对比方法
- 目标检测：对比多种单模态（SSD, RetinaNet, Faster R-CNN, Cascade R-CNN, DDQ-DETR）和多模态（GAFF, ProbEn, LGADet, CSSA, UniRGB-IR等）。
- 语义分割：对比MFNet, RTFNet, MFFENet, EGFNet, MTANet, FEANet, GMNet, CCFFNet, CMX, FDCNet, ECGFNet, LASNet, UniRGB-IR, RoadFormer+等。
- 显著目标检测：对比MMCI, TANet, S2MA, JLDCF, MTMR, M3S-NIR, SGDL, FMSF, ADF, LSNet, UniTR, UniRGB-IR等。

### 评价指标
- 目标检测：COCO mAP（IoU 0.5:0.95）、AP50、AP75。
- 语义分割：mAcc、mIoU。
- 显著目标检测：S-measure、E-measure、F-measure、MAE。

## 4. 资源与算力

- **GPU型号**：NVIDIA GeForce RTX 4090。
- **具体数量**：文中未说明使用了多少张GPU。
- **训练时长**：目标检测两阶段共48 epoch（第一阶段36 epoch，第二阶段12 epoch），batch size=8；语义分割10,000 iterations，batch size=16；显著检测10,000 iterations，batch size=64。但未报告总训练时间或显存占用。

## 5. 实验数量与充分性

- **实验组数**：涵盖三大任务共6个数据集，每个数据集均与多个SOTA方法对比。
- **消融实验**：分别验证了DFS模块、FAFB中各子模块（DC、SE、空间注意力）、CFE中各组件（多头注意力、重置门）的有效性；还进行了输入模态（RGB vs IR）和训练策略（单阶段 vs 两阶段）的消融。
- **可视化**：提供了目标检测和语义分割的定性结果对比。
- **充分性与公平性**：消融实验较全面，对比方法均为近年SOTA，且在同一代码框架（MMDetection/MMSegmentation）中实现MOSAIC，保证了比较的相对公平。但未在更多样化的场景（如夜间、雾天、不同分辨率）或更多数据集上验证泛化性。

## 6. 主要结论与发现

- MOSAIC在FLIR上mAP达48.9，LLVIP上67.7，显著超过此前最优的UniRGB-IR（提升约4.8~4.5个点），在AP50和AP75上提升更大。
- 语义分割在MFNet上mIoU达66.9，mAcc达81.3，相比UniRGB-IR分别提升12.8%和7.4%。
- 显著目标检测在VT5000上取得SOTA，VT821和VT1000上接近SOTA。
- 消融实验表明：DFS模块有效处理模态错位；FAFB中空间注意力带来额外收益；CFE中的多头注意力和门控机制均不可或缺。
- IR作为ViT输入优于RGB，两阶段训练策略优于全程冻结ViT。

## 7. 优点

- **模块设计新颖**：可变形特征采样实现动态对齐，FAFB融合多感受野信息，CFE采用GRU门控渐进注入，整体设计针对RGB-IR错位和融合效率。
- **多任务验证**：在目标检测、语义分割、显著检测三个不同下游任务上均取得SOTA，展示了框架的通用性。
- **消融实验充分**：逐一验证了每个提出组件的贡献，且包含输入模态和训练策略的消融。
- **可视化结果**：定性显示了MOSAIC在困难场景（如行人被遮挡/漏检）下的改进，强化了说服力。

## 8. 不足与局限

- **实验覆盖有限**：仅在FLIR、LLVIP、MFNet和VT系列上测试，缺少自动驾驶更复杂场景（如雨天、雪天、不同红外波段）的验证。
- **计算开销未充分讨论**：未报告模型参数量、FLOPs或推理速度，多阶段模块可能增加延时，不利于实时应用。
- **失败案例未分析**：未讨论模型在哪些情况下仍会错误或失败，缺乏对局限性的坦诚说明。
- **ViT输入模态选择**：实验表明IR作为ViT输入优于RGB，但未尝试其他组合（如RGB输入+IR适配器），整体设计对模态依赖较大。
- **消融实验仅在两个数据集**：部分消融（如CFE组件）只在FLIR和LLVIP上做，未在分割和显著性数据集上验证。
- **代码与可复现性**：未提供开源代码，削弱了可信度。

（完）
