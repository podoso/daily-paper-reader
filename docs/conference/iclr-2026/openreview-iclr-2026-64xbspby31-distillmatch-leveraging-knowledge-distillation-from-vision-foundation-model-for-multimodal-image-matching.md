---
title: "DistillMatch: Leveraging Knowledge Distillation from Vision Foundation Model for Multimodal Image Matching"
title_zh: "DistillMatch: 利用视觉基础模型知识蒸馏进行多模态图像匹配"
authors: "Meng Yang, Fan Fan, Zizhuo Li, Ruimin Huang, Songchu Deng, Yong Ma, Jiayi Ma"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=64xbSPBy31"
tags: ["query:multimodal"]
score: 8.0
evidence: 利用视觉基础模型知识蒸馏进行多模态图像匹配
tldr: 多模态图像匹配因模态差异和数据稀缺而困难。本文提出DistillMatch，通过从视觉基础模型（VFM）进行知识蒸馏，提取通用且鲁棒的特征，实现了跨模态像素级对应。在多个多模态匹配基准上超越现有方法，展示了VFM在跨模态任务中的迁移能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-64xbspby31/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1395, \"height\": 345, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-64xbspby31/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1370, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-64xbspby31/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1423, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-64xbspby31/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1443, \"height\": 158, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-64xbspby31/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 777, \"height\": 647, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-64xbspby31/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1467, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-64xbspby31/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-64xbspby31/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1054, \"height\": 631, \"label\": \"Table\"}]"
motivation: 多模态图像匹配中标注数据稀缺且模态差异大，现有方法泛化性差。
method: 提出DistillMatch，通过知识蒸馏从视觉基础模型迁移鲁棒的跨模态特征。
result: 在多个多模态匹配数据集上取得最优效果。
conclusion: 知识蒸馏可有效提升多模态匹配的泛化性和精度。
---

## Abstract
Multimodal image matching seeks pixel-level correspondences between images of different modalities, crucial for cross-modal perception, fusion and analysis. However, the significant appearance differences between modalities make this task challenging. Due to the scarcity of high-quality annotated datasets, existing deep learning methods that extract modality-common features for matching perform poorly and lack adaptability to diverse scenarios. Vision Foundation Model (VFM), trained on large-scale data, yields generalizable and robust feature representations adapted to data and tasks of various modalities, including multimodal matching. Thus, we propose DistillMatch, a multimodal image matching method using knowledge distillation from VFM. DistillMatch employs knowledge distillation to build a lightweight student model that extracts high-level semantic features from VFM to assist matching across modalities. To retain modality-specific information, it extracts and injects modality category information into the other modality's features, which enhances the model's understanding of cross-modal correlations. Furthermore, we design V2I-GAN to boost the model's generalization by translating visible to pseudo-infrared images for data augmentation. Experiments show that DistillMatch outperforms existing algorithms on public datasets.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与整体含义（研究动机和背景）

- **研究动机**：多模态图像匹配旨在建立不同模态图像（如可见光与红外）之间的像素级对应，是跨模态感知、融合与分析的关键。然而，不同模态间存在巨大的外观差异（纹理、对比度、强度等），使得该任务极具挑战性。
- **核心困难**：
  1. 高质量标注的多模态匹配数据集极为稀缺，导致现有深度学习方法泛化能力差，难以适应多样场景。
  2. 现有方法大多只提取模态间“共同特征”进行匹配，丢弃了模态特有信息，限制了特征表达力。
- **解决思路**：利用视觉基础模型（VFM，如DINOv2）在大规模数据上预训练获得的通用、鲁棒特征表示，通过知识蒸馏将高层次语义知识迁移到轻量级学生模型，以克服模态差异和数据稀缺问题。

## 二、方法论：核心思想与关键技术细节

### 1. 整体框架：DistillMatch
- 包含四个主要模块：KD-VFM（基于VFM知识蒸馏的特征提取）、CEFG（类别增强特征引导模块）、STFA（语义与纹理特征聚合模块）、粗到细匹配模块（CMM+FMM+SRM）。
- 额外提出V2I-GAN用于可见光→红外图像翻译，作为数据增强手段。

### 2. 关键技术细节
#### (a) KD-VFM（知识蒸馏特征提取）
- 三分支结构：ResNet提取基础纹理特征（1/2、1/4、1/8尺度）、DINOv2（ViT-S/14+注册令牌）提取高层语义特征、轻量Transformer学生模型。
- 教师模型输出 \(F_{tea}=F_{DINO}\)，学生模型输出 \(F_{stu}\)，通过在线知识蒸馏学习：
  - MSE损失（像素级对齐）
  - Gram矩阵损失（空间关系保持）
  - KL散度损失（概率分布对齐）
  - 总蒸馏损失：\(L_{KD} = \alpha L_{MSE} + \beta L_{Gram} + \gamma L_{KL}\)

#### (b) CEFG（类别增强特征引导模块）
- 使用Restormer+Transformer编码器提取浅层特征与可学习的模态类别表征 \(f_{clc}\)。
- 通过交叉熵损失 \(L_{ce}\) 使类别表征准确反映模态。
- 将另一模态的类别表征注入当前模态深度特征（通过元素加和并经非共享Transformer块），得到类别增强特征 \(\tilde{F}_{vis/ir}\)。
- 与ResNet特征融合生成增强纹理特征 \(\tilde{F}_{Res}^{1/8}\)。

#### (c) STFA（语义与纹理特征聚合模块）
- 通道注意力聚合（CAA）：以语义特征 \(F_S\) 为Query，纹理特征 \(F_T\) 为Key/Value，沿通道维度进行交叉注意力，实现软对齐。
- 空间注意力聚合（SAA）：以 \(F_T\) 为Query，CAA输出为Key/Value，沿空间维度聚合。
- 残差连接得到最终聚合特征 \(F_T^{STFA}\)。

#### (d) 粗到细匹配模块
- **粗匹配（CMM）**：在1/8尺度上通过LoFTR风格的自注意力+交叉注意力，计算相似度矩阵并双softmax得到概率，阈值过滤得到粗匹配 \(M_c\)。
- **精细匹配（FMM）**：利用1/2和1/4尺度特征，在粗匹配周围提取1×1、3×3、5×5窗口，计算局部相似度并双softmax，阈值得到 \(M_f\)。
- **亚像素细化（SRM）**：MLP预测局部偏移 \(\delta_{vis},\delta_{ir}\)，修正匹配坐标至亚像素精度，损失采用对称极线距离 \(L_{sub}\)。

#### (e) V2I-GAN（图像翻译数据增强）
- 基于PearlGAN框架，在FMB数据集上训练，包含两个生成器和两个判别器。
- 生成器中集成STFA模块聚合DINOv2特征，并引入结构化梯度对齐损失保持语义一致性。
- 训练时随机将MegaDepth中的一张可见光图翻译为伪红外图，提供带标注的“可见光-红外”图像对。

### 3. 损失函数
- 总损失：\(L_{total} = \lambda_{KD} L_{KD} + \lambda_{ce} L_{ce} + L_{match}\)
- 匹配损失 \(L_{match}\) 包含粗匹配焦点损失、精细匹配焦点损失、亚像素细化对称极线损失。

## 三、实验设计

### 1. 数据集与Benchmark
- **训练集**：MegaDepth（可见光单模态数据集），训练时用V2I-GAN随机将一幅图转为伪红外。
- **相对位姿估计**：METU-VisTIR数据集（cloud-cloud和cloud-sunny场景），指标AUC@5°/10°/20°。
- **单应性估计**：四个数据集——无人机遥感、室内、夜间、雾霾场景。指标AUC@3/5/10像素或5/10/20像素。
- **零样本实验**：光学-SAR、光学-地图、光学-深度、医学PD-T1-T2、视网膜、跨时间图像对等，指标为正确匹配数（NCM）和均方根误差（RMSE）。

### 2. 对比方法
- SAMFeat、SDME、SCFeat、SemaGlue、LiftFeat、DenseAffine、MTV-LoFTR、JamMa、XoFTR、MINIMA LoFTR、MINIMA E-LoFTR、MINIMA XoFTR 等12种方法。

## 四、资源与算力
- **GPU**：3块NVIDIA GeForce RTX 4090
- **训练时长**：120小时（20个epoch）
- **优化器**：AdamW，学习率6×10⁻³，批次大小1
- 论文明确说明了硬件与训练配置。

## 五、实验数量与充分性
- 共进行**4大类实验**：相对位姿估计（2个场景×3个阈值）、单应性估计（4个数据集×3个阈值）、零样本实验（6种模态×2个指标）、消融实验（6组）。
- 消融实验（表3）验证了CAA、SAA、KD-VFM、CEFG、V2I-GAN各模块的有效性。
- 实验覆盖了多种模态场景（遥感、室内、夜间、雾霾、医学、合成孔径雷达等），对比方法覆盖了近年主流和SOTA。
- **充分性**：实验设计较为全面，基准多样，对比充分。但缺少在通用车载/无人机多模态数据集上的评估（如KAIST、FLIR），以及更多元化的数据增强效果单独实验。

## 六、主要结论与发现
- DistillMatch在相对位姿估计、单应性估计、零样本匹配等任务上**显著优于所有对比方法**（在绝大多数阈值下AUC最高）。
- 在零样本实验中，NCM指标全面领先，表明其跨模态泛化能力突出。
- 消融实验证实每个组件（CAA、SAA、KD-VFM、CEFG、V2I-GAN）均贡献正面增益。
- 知识蒸馏成功将VFM的高层语义理解注入轻量模型，同时通过保留模态特有信息增强跨模态相关性。

## 七、优点
1. **创新性**：首次系统地将VFM知识蒸馏引入多模态匹配，并设计CEFG保留模态特有信息，克服了传统只提取公共特征的缺陷。
2. **轻量高效**：学生模型轻量，推理时不依赖VFM，适合部署。
3. **数据增强实用**：V2I-GAN生成带标注的伪红外图，解决标注稀缺，且保留几何结构。
4. **泛化性强**：零样本实验表现优秀，证明方法的扩展性和鲁棒性。
5. **实验详尽**：在多领域、多模态、多指标下验证，消融完整。

## 八、不足与局限
1. **训练数据依赖**：主要基于MegaDepth（室内外场景）生成伪红外，与真实红外数据分布可能有差异，在真实红外场景上的效果需进一步验证。
2. **计算开销**：在线知识蒸馏需同时运行DINOv2教师模型，训练耗时（120小时×3 GPU），资源需求较高。
3. **零样本部分指标落后**：在光学-地图等某些模态上RMSE略逊于MINIMA XoFTR，说明仍存在模态适应性改进空间。
4. **实验场景覆盖**：未包含如KAIST、FLIR等车载红外行人数据集，缺乏对自动驾驶典型场景的评估。
5. **未讨论失败案例**：论文未分析匹配失败典型情况或模型局限性，对实际应用中的瓶颈未作说明。
6. **可重复性细节**：尽管提供了匿名代码和配置链接，但超参数（如损失权重）设置的解释不够深入，可能影响复现。

（完）
