---
title: Cross Modal Fine-grained Alignment via Granularity-aware and Region-uncertain Modeling
title_zh: 基于粒度感知和区域不确定性建模的跨模态细粒度对齐
authors: "Jiale Liu, Haoming Zhou, Yishu Liu, Bingzhi Chen, Yuncheng Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39544/43505"
tags: ["query:multimodal"]
score: 8.0
evidence: 细粒度图文对齐，跨模态，粒度感知，区域不确定性
tldr: 针对细粒度跨模态对齐中注意力机制噪声和区域-文本对应模糊性问题，提出粒度感知与区域不确定性建模，分别评估视觉和文本token的重要性并建模一对多不确定性，在多个下游任务上显著提升对齐精度。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39544/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 851, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39544/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1791, \"height\": 693, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39544/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 329, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39544/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 880, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39544/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39544/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 871, \"height\": 522, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39544/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 1449, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39544/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 894, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39544/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 374, \"label\": \"Table\"}]"
motivation: 现有方法缺乏健壮的模态内机制和细粒度不确定性建模，导致复杂场景下泛化差。
method: 提出粒度感知模块评估token重要性，并引入区域不确定性建模捕获一对多对应关系。
result: 在VQA、图像描述等任务上取得最佳性能。
conclusion: 该方法为细粒度多模态对齐提供了有效方案。
---

## Abstract
Fine-grained image-text alignment is a pivotal challenge in multimodal learning, underpinning key applications such as visual question answering, image captioning, and vision-language navigation. Unlike global alignment, fine-grained alignment requires precise correspondence between localized visual regions and textual tokens, often hindered by noisy attention mechanisms and oversimplified modeling of cross-modal relationships. In this work, we identify two fundamental limitations of existing approaches: the lack of robust intra-modal mechanisms to assess the significance of visual and textual tokens, leading to poor generalization in complex scenes; and the absence of fine-grained uncertainty modeling, which fails to capture the one-to-many and many-to-one nature of region-word correspondences. To address these issues, we propose a unified approach that incorporates significance-aware and granularity-aware modeling and region-level uncertainty modeling. Our method leverages modality-specific biases to identify salient features without relying on brittle cross-modal attention, and represents region features as a mixture of Gaussian distributions to capture fine-grained uncertainty. Extensive experiments on Flickr30K and MS-COCO demonstrate that our approach achieves state-of-the-art performance across various backbone architectures, significantly enhancing the robustness and interpretability of fine-grained image-text alignment.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：细粒度图像-文本对齐（fine-grained image-text alignment）是跨模态学习的关键挑战，广泛应用于视觉问答、图像描述和视觉语言导航等任务。现有方法存在两个根本局限：  
  - 缺乏有效的**模态内**显著性建模，跨模态注意力权重受检索目标驱动，往往关注视觉显著但语义无关的区域，导致噪声和泛化能力差。  
  - 缺乏**细粒度不确定性建模**，大多数方法仅在图像-文本对级别建模不确定性，忽略了一个区域可能对应多个词、一个词可能对应多个区域的“一对多/多对一”关系。

- **研究动机**：提出一种统一框架，通过**粒度感知**和**区域不确定性建模**来提升细粒度对齐的鲁棒性和可解释性，不依赖脆弱的跨模态注意力。

## 2. 论文提出的方法论

- **核心思想**：  
  - **模态内显著性建模**：利用各模态自身的统计偏置（而非跨模态交互）识别重要token，避免噪声干扰。  
  - **区域级不确定性建模**：将图像区域特征表示为混合高斯分布，捕捉细粒度语义歧义。

- **关键技术细节**：  
  1. **双编码器特征提取**：图像用 ViT/Swin，文本用 BERT，独立编码。  
  2. **显著性感知适配器（Significance-aware Adapter）** 和**粒度感知适配器（Granularity-aware Adapter）**：结构相同但独立训练，通过可学习权重生成每个patch/word的重要性得分，经Gumbel-Softmax二值化后与特征相乘，抑制冗余信息。  
  3. **区域提示（Region Prompting）**：引入K个可学习提示向量，通过与图像patch的注意力机制聚合得到区域均值 \(\mu_k\)。  
  4. **不确定性建模**：用预测网络估计每个区域的对数方差 \(\log \sigma_k^2\)，通过重参数化采样得到不确定性感知的区域表示 \(u_k\)（混合高斯分布）。  
  5. **多级双向对齐损失**：计算原始特征、显著性特征、不确定性区域-文本三者的双向相似性（text2image和image2text的max-pooling聚合），并用三重对比损失（含难负样本挖掘）训练。  
  6. **额外正则化**：语义一致性约束（\(L_{\text{recon}}\)）、KL散度（\(L_{\text{KL}}\)）和熵正则化（\(L_{\text{ent}}\)）保证区域分布多样且接近先验。

- **算法流程示意**：  
  - 输入图像和文本 → 编码得V和T → 通过两个适配器得\(\hat{V},\hat{T}\) → 区域提示+不确定性建模得U → 计算\(S_{\text{ori}}, S_{\text{key}}, S_{\text{unc}}\)三个相似度矩阵 → 加权对比损失+正则项联合优化。

## 3. 实验设计

- **数据集**：Flickr30K（1K测试集）、MS-COCO（1K和5K测试集）——标准图像-文本检索benchmark。  
- **评估指标**：Recall@K（K=1,5,10）和rSum（Recall之和）。  
- **对比方法**：  
  - 基于Faster R-CNN两大类的：VSE++、MV-VSE、CHAN、HERM、CORA。  
  - 基于ViT/Swin的：SCAN、VSE++、SGR、CHAN、LAPS、AVSE。  
- **视觉骨干**：ViT-Base-224/384、Swin-Base-224/384；文本骨干：BERT-base。  
- **实验场景**：图像到文本和文本到图像双向检索。

## 4. 资源与算力

论文中**未明确说明**使用的GPU型号、数量、训练时长或其他硬件资源。仅提供了代码仓库链接（https://github.com/H3IIoWorld/GRM），但无资源消耗细节。

## 5. 实验数量与充分性

- **主要实验**：Table 1 展示了在Flickr30K和MS-COCO上，使用4种视觉骨干、共约8种对比方法的完整结果，覆盖不同分辨率。  
- **消融实验**：  
  - Table 2：模块消融（移除SA、GA、RP、UM），验证各组件贡献。  
  - Table 3：损失消融（移除\(L_{\text{ori}}, L_{\text{key}}, L_{\text{unc}}, L_{\text{recon}}, L_{\text{reg}}\)），验证各目标重要性。  
- **超参数分析**：Figure 4(a) 探究区域提示数量（5~55）在不同骨干下的影响；Figure 4(b) 探究多级对齐权重组合（a,b,c）的影响。  
- **可视化**：Figure 5/6 分别展示patch-word热图和区域-文本对齐结果，定性证明方法效果。

**充分性评价**：实验覆盖了多个数据集、骨干、对比方法和消融维度，结果统计显著且一致，方法客观公平。但缺乏在VQA、captioning等下游任务的直接验证（尽管论文声称应用于此），而仅在检索任务上测试。

## 6. 论文的主要结论与发现

- 提出的GRM框架在Flickr30K和MS-COCO上**全面超越**所有现有方法，rSum提升2.1%~5.6%（Flickr30K）、1.3%~4.0%（MS-COCO 1K）、1.9%~5.6%（MS-COCO 5K）。  
- **模态内显著性建模**和**区域不确定性建模**均不可或缺，二者互补。  
- 多级对齐损失中，原始相似度和显著性相似度权重同等重要（a=b=0.4），过度依赖不确定性相似度（c过大）会降低性能。  
- 区域提示数量对性能敏感，ViT下最优为5，Swin下为50，源于局部注意与全局注意的差异。

## 7. 优点

- **创新性**：首次将模态内粒度感知与区域级不确定性结合，避免跨模态注意力的噪声。  
- **模块化设计**：适配器、区域提示、不确定性模块可独立替换或移除，便于后续改进。  
- **端到端**：不需要预训练的目标检测器（如Faster R-CNN），降低系统复杂性和误差传播。  
- **可迁移性**：在多种视觉骨干（ViT、Swin）和图像分辨率下均取得一致优势，泛化性强。  
- **消融与超参数分析充分**：多个维度验证了设计选择和损失贡献的合理性。

## 8. 不足与局限

- **实验局限**：仅在图像-文本检索任务上评估，未在VQA、captioning等下游任务上直接测试，削弱了“应用于这些任务”的论断。  
- **计算开销**：论文未报告训练时间和推理效率，区域提示模块和不确定性建模可能引入额外参数和计算成本，需进一步分析。  
- **数据集依赖性**：仅在Flickr30K和MS-COCO上验证，领域偏向于自然场景，在通用/跨域场景（如医疗、遥感）中的表现未知。  
- **超参数敏感**：区域提示数量K和损失权重a,b,c需要根据骨干调优，缺乏自适应策略。  
- **文本编码器固定**：仅使用BERT-base，未探索更大或更新的语言模型（如RoBERTa、LLaMA等）。

（完）
