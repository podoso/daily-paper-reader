---
title: Geometry-Aware Noisy Correspondence Mitigation for Cross-Modal Text-Based Person Retrieval
title_zh: 面向跨模态文本人物检索的几何感知噪声对应缓解方法
authors: "Xinpan Yuan, Shaomin Xie, Liujie Hua, Chengyuan Zhang, Guihu Zhao, Lin Yuanbo Wu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38218/42180"
tags: ["query:multimodal"]
score: 6.0
evidence: 跨模态检索中的噪声对应缓解，多模态对齐
tldr: 针对跨模态文本人物检索中文本与图像间的弱对应或错误对应（噪声对应）问题，提出几何感知的噪声对应缓解方法。该方法同时建模跨模态和模态内几何结构，利用图约束增强鲁棒匹配。在多个基准上验证了有效性，提升了检索精度。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38218/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 765, \"height\": 883, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38218/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1822, \"height\": 784, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38218/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38218/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38218/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 845, \"height\": 678, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38218/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1823, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38218/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 883, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38218/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 883, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38218/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 882, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38218/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 883, \"height\": 513, \"label\": \"Table\"}]"
motivation: 真实场景中文本与图像的对应关系常存在噪声，影响跨模态匹配。
method: 引入几何感知的噪声对应缓解，同时利用跨模态和模态内几何结构进行鲁棒匹配。
result: 在多个人物检索基准上提升了检索精度。
conclusion: 几何感知建模有效应对了跨模态检索中的噪声对应问题。
---

## Abstract
Text-Based Person Retrieval (TBPR) aims to accurately retrieve target individuals from large-scale image databases using only textual descriptions. Existing methods typically assume a ground-truth correspondence between text and images (i.e., strongly correlated). However, in real-world scenarios, this assumption may not be able to hold for the cross-modal matching due to weak or even corrupted correlations between textual descriptions and visual content, referred to as noisy correspondence (NC). Such NC largely disrupts the correspondence learning between visual and semantic modalities. Though prior works have improved single-modal robustness against noisy labels, systematic modeling of both cross-modal and intra-modal geometric structures in TBPR remains limited attention. In this paper, we propose Geometric Structure Consistency Alignment (GSCA) to TBPR, which leverages cross-modal cosine similarity and intra-modal nearest-neighbor affinity to learn visual-semantic consistency under noisy correspondence. To mitigate the structural corruption caused by noisy pairs, we introduce the Structure Refinement and Mining (SRAM) module. By partitioning training data into clean, ambiguous, and noisy subsets, SRAM enables the model to strategically refine the cross-modal correspondence by mining reliable pairs, thus enhancing the reliability of positive or negative samples discrimination and preserving structural consistency across modalities. Extensive experiments demonstrate that our method achieves state-of-the-art performance across three public datasets. On CUHK-PEDES, it boosts Rank-1 by 1.42% in noise-free conditions, sustaining a robust 74.25% Rank-1 under a 50% noise ratio.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：文本人物检索（TBPR）要求仅凭自然语言描述从大规模图像库中准确检索目标人物。现有方法通常假设训练数据中文本-图像对完全正确对齐（即强对应关系），然而真实场景中这种假设常不成立，存在弱对应甚至错误对应，即**噪声对应（Noisy Correspondence, NC）**。NC严重破坏跨模态匹配中的语义-视觉一致性学习。
- **研究动机**：虽然以往工作针对单模态噪声标签有所改进，但对跨模态和模态内**几何结构**的系统建模在TBPR中仍很有限。噪声对应会扭曲跨模态相似度图和模态内几何结构，导致模型过拟合于错误匹配。
- **整体含义**：本文旨在通过同时利用跨模态和模态内的几何结构差异，区分干净与噪声样本，并修复结构坍塌，从而实现鲁棒的跨模态对齐。

## 2. 论文提出的方法论

### 核心思想
提出**几何结构一致性对齐（GSCA）** 和**结构细化与挖掘（SRAM）** 两个即插即用模块。GSCA利用跨模态余弦相似度和模态内最近邻亲和度学习视觉-语义一致性；SRAM通过将训练数据划分为干净、模糊和噪声子集，针对性地精炼正对一致性并挖掘负对潜在一致性，缓解结构坍塌。

### 关键技术细节
#### 2.1 GSCA
- **跨模态几何结构**：定义为图像\(I_i\)与所有文本\(T_j\)的相似度集合，优化跨模态对比损失（公式6），并基于对应指示器\(y_i\)进行净化。
- **模态内几何结构**：定义为图像之间、文本之间的相似度集，确保匹配对在各自模态内保持相似的结构。优化模态内损失（公式7），其中用\(y_z\)过滤噪声样本对相似度聚合的影响。
- **噪声判别与净化**：利用深层网络早期记忆效应，通过两个指示器识别噪声：
  - 跨模态指示器\(y_i^{cm}\)：基于双向softmax比值，干净样本接近1，噪声接近0。
  - 模态内指示器\(y_i^{im}\)：对模态内一致性分数拟合双分量高斯混合模型（GMM），取更干净分量的后验概率。
  - 最终软标签\(y_i = \min(y_i^{cm}, y_i^{im})\)，取两者最小值以增强可靠性。
- 总损失：\(L_{gsca} = L_{cm} + \alpha L_{im}\)，其中\(\alpha=0.4\)。

#### 2.2 SRAM
- **数据划分**：基于双向余弦相似度\(p_{i2t}^i\)和\(p_{t2i}^i\)，与阈值\(\gamma=0.5\)比较，分为干净集\(D_p\)、模糊集\(D_v\)、噪声集\(D_n\)。
- **一致性精炼**：对不同子集应用不同标签调整策略，引入角度校正因子\(\exp(-\theta^2/(2\sigma^2))\)，其中\(\theta=\arccos(s(I_i,T_i))\)，\(\sigma=0.1\)。干净对强化、模糊对软化、噪声对抑制。
- **一致性挖掘**：从噪声对中挖掘潜在正对：计算方向匹配强度\(\omega_{i2t}^{i,j}\)，通过自适应阈值\(\beta\)过滤不可靠对，保留高质量负对用于对比学习。
- **精炼与挖掘损失**：联合优化精炼后的干净样本和挖掘出的负样本，损失函数如公式(17)(18)。

### 算法流程（文字说明）
1. 使用CLIP提取图像和文本特征。
2. 计算跨模态余弦相似度，构建跨模态和模态内几何结构。
3. 通过GSCA估计干净度指示器\(y\)，对损失进行净化。
4. SRAM根据相似度划分数据集，分别计算精炼后的标签和挖掘权重。
5. 联合优化GSCA和SRAM的总损失（\(L_{gsca} + L_{sram}\)），训练60个epoch。

## 3. 实验设计

- **数据集**：CUHK-PEDES、ICFG-PEDES、RSTPReid，均为TBPR标准基准。
- **基准设置**：以IRRA和RDE作为基线方法，在干净(0%噪声)和合成噪声(20%、50%)下进行评测。
- **对比方法**：包括ViTAA、DSSL、LapsCore、LBUL、Han et al.、SAF、TIPCB、CAIBC、AXM-Net、LGUR、IVT、CFine、IRRA、LAIP、PLOT、RDE、IRLT、WoRA、DM-Adapter、VFE-TPS等20余种近期SOTA方法。
- **评估指标**：Rank-1/5/10、mAP、mINP。
- **实验充分性**：
  - 在三个数据集、三种噪声比例（0%、20%、50%）下进行系统对比。
  - 在CUHK-PEDES上进行了充分消融实验（表5），分别测试GSCA和SRAM单独及联合效果。
  - 参数分析（图3）：对GSCA的\(T_1\)和\(\alpha\)、SRAM的\(T_2\)和\(\gamma\)进行敏感性实验。
  - 可视化分析（图4、5）：展示训练初期和末期干净/噪声样本分布，以及Grad-CAM定位效果。

## 4. 资源与算力

- **GPU**：单张NVIDIA RTX 3090（24GB显存）。
- **训练配置**：Adam优化器，cosine学习率调度，初始学习率\(1\times10^{-5}\)，共60个epoch。
- **训练时长**：文中未明确给出具体时长，但基于单卡3090和标准数据集规模，通常需数小时至一天。
- **数据增强**：图像随机水平翻转、随机裁剪填充、随机擦除；文本随机掩码、替换、删除。输入图像尺寸384×128，最大文本长度77。

## 5. 实验数量与充分性

- **实验数量**：约20余组主要对比（三个数据集×三种噪声×两种基线），加上消融（5组×三种噪声）、参数分析（4组）、可视化（2组），总计超30组实验。
- **充分性与客观性**：
  - 对比方法覆盖范围广，包括近年所有重要工作，且排名表清晰。
  - 在同一基线下使用相同训练策略，控制变量公平。
  - 消融实验验证了每个模块的贡献，参数分析提供了最优设置。
  - 可视化进一步直观证明效果。
- **潜在不足**：噪声是人工合成的（随机替换文本-图像对），可能与真实场景噪声分布有差异。未在更大规模数据集（如MSMT17）上验证。

## 6. 论文的主要结论与发现

- 提出GSCA和SRAM模块能有效缓解TBPR中的噪声对应问题，显著提升检索精度和鲁棒性。
- 在干净条件下，CUHK-PEDES上R@1提升1.42%（RDE基线），ICFG-PEDES上提升0.58%，RSTPReid上提升1.22%。
- 在50%高噪声比下，CUHK-PEDES维持74.25% R@1（RDE基线仅71.25%），ICFG-PEDES上66.47%，RSTPReid上64.28%。
- 几何结构一致性对齐和结构细化挖掘相结合，优于仅使用单模态噪声处理或软标签方法。

## 7. 优点

- **创新性**：首次将跨模态和模态内几何结构同时建模用于噪声对应缓解，方法简洁且有效。
- **即插即用**：两个模块可灵活嵌入现有TBPR框架（如IRRA、RDE），无需大幅修改模型结构。
- **鲁棒性**：在高噪声环境下性能衰减远小于基线，表明强大的抗噪能力。
- **实验全面**：覆盖三个标准基准、多种噪声比、充分消融和参数分析，结论可靠。
- **可解释性**：通过可视化展示了干净/噪声样本分布变化和实体定位改进，为理解噪声对应问题提供直观证据。

## 8. 不足与局限

- **噪声类型单一**：实验仅使用随机替换的合成噪声，未考虑真实场景中更复杂的部分相关或语义偏移噪声，泛化性需进一步验证。
- **依赖基线模型**：GSCA和SRAM为辅助模块，性能上限受基线模型（IRRA、RDE）影响，最佳结果仍需依赖现有强基线。
- **计算开销**：SRAM涉及数据划分和双向相似度计算，可能增加训练时间，但文中未给出额外开销分析。
- **跨模态判别器设计**：公式(3)中的双向softmax比值可能受批次大小影响，小批次下估计不稳定。
- **应用限制**：当前方法主要服务人物检索领域，能否直接推广到其他跨模态任务（如图文检索、视觉问答）尚不明确。

（完）
