---
title: Robust Semi-paired Multimodal Learning for Cross-modal Retrieval
title_zh: 鲁棒半配对跨模态学习用于跨模态检索
authors: "Yang Qin, Yuan Sun, Xi Peng, Dezhong Peng, Joey Tianyi Zhou, Xiaomin Song, Peng Hu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39684/43645"
tags: ["query:multimodal"]
score: 5.0
evidence: 鲁棒半配对多模态学习用于跨模态检索
tldr: 实际中大规模完美配对的多模态数据难以获取。本文研究半配对跨模态学习，提出RCSL方法，利用少量配对和大量未配对数据进行联合学习。在图像-文本检索任务上，该方法有效缓解了配对数据不足导致的优化不足问题，性能优于全监督和半监督基线。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39684/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 839, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39684/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39684/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 885, \"height\": 397, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39684/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39684/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1838, \"height\": 969, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39684/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1837, \"height\": 818, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39684/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 872, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39684/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39684/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 879, \"height\": 412, \"label\": \"Table\"}]"
motivation: 收集大规模配对多模态数据成本高，限制了跨模态检索性能。
method: 设计半配对学习框架，同时利用配对和未配对数据进行跨模态对齐。
result: 在图像-文本检索任务上超过传统配对方法和半监督方法。
conclusion: 为低成本多模态学习提供了有效方案。
---

## Abstract
Cross-modal retrieval is a fundamental application of multi-modal learning that has achieved remarkable success with large-scale well-paired data. However, in practice, it is costly to collect large-scale well-paired data. To alleviate the dependence on the amount of paired data, in this paper, we study a practical learning paradigm: semi-paired cross-modal learning (SPL), which utilizes both a small amount of paired data and a large amount of unpaired data to enhance cross-modal learning directly and is more accessible in practice. To achieve this, we take image-text retrieval as an example and propose a novel Robust Cross-modal Semi-paired Learning method (RCSL)  by addressing two challenges. To be specific, i) to overcome the under-optimization issue caused by too little paired data, we present Semi-paired Discriminative Learning (SDL) to fully learn visual-semantic associations from a small amount of image-text pairs by preserving the alignment and uniformity of modality representations. ii) To mine visual-semantic correspondences from unpaired data, RCSL first constructs pseudo-paired correlations across different modalities by nearest neighbor association. However, this may introduce noisy correspondences (NCs) due to inaccurate pseudo signals, which could degrade the model's performance. To tackle NCs, we devise Robust Cross-correlation Mining (RCM) based on the risk minimization criterion to robustly and explicitly learn visual-semantic associations from pseudo-paired data, thus boosting cross-modal learning. Finally, we conduct extensive experiments on four datasets, i.e., three widely used benchmark datasets of Flickr30K, MS-COCO, CC152K, and a newly constructed real-world dataset Drone-SP, to demonstrate the effectiveness of RCSL under semi-paired and noisy settings.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：传统跨模态检索（如图像-文本检索）依赖大规模完美配对的数据，但收集此类数据成本高昂、劳动密集，实际场景中往往只能获取少量配对数据和大量未配对数据（如从互联网爬取）。
- **整体含义**：本文提出了一种新的学习范式——**半配对跨模态学习（Semi-paired cross-modal learning, SPL）**，旨在同时利用少量精确配对数据和大量未配对数据来提升检索性能，降低对大规模配对数据的依赖，更符合实际应用需求。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：设计一个端到端的鲁棒半配对学习框架（RCSL），包含两个关键模块：
  - **Semi-paired Discriminative Learning (SDL)**：解决少量配对数据导致的模型欠优化问题。通过引入**Alignment（对齐）** 和**Uniformity（均匀性）** 两个正则化项，增强表征的稳定性和多样性，使少量配对数据也能学习到良好的视觉-语义关联。
  - **Robust Cross-correlation Mining (RCM)**：从未配对数据中挖掘潜在的跨模态关联。先通过最近邻相似度构建伪配对，但伪配对可能引入噪声对应（NCs）。RCM基于**风险最小化准则**设计鲁棒损失函数（Lm），理论上证明其在均匀噪声下具有噪声耐受性（当噪声率 η < (N-1)/N 时），从而能可靠地从伪配对数据中学习关联。
- **关键公式与流程**（文字说明）：
  - 总损失：`L_overall = L_sdl + L_rcm`
  - `L_sdl` = 修改后的三元组损失（仅用于已知配对）+ 对齐与均匀性正则项。
  - `L_rcm` = 图像→文本方向与文本→图像方向的鲁棒挖掘损失之和，利用双向匹配概率计算，并基于风险最小化理论推导其噪声鲁棒性。
- **扩展应用**：作者还将RCSL拓展到处理噪声对应学习（NCL）问题，通过预热阶段将数据划分为“干净集”（视为配对）和“噪声集”（视为未配对），从而用半配对框架解决传统噪声对应问题。

## 3. 实验设计
- **数据集**：共使用四个数据集：
  - 三个广泛使用的基准：Flickr30K、MS-COCO、CC152K（真实噪声数据集）
  - 一个自建的真实场景数据集：**Drone-SP**（无人机图像-文本检索，仅962个配对，其余为未配对数据）
- **半配对设置**：将Flickr30K和MS-COCO的配对数据量分别设为25K和2.5K，其余数据通过打乱生成未配对数据。
- **对比方法**：
  - 半配对场景下对比了10种基线方法（全局级：VSE∞、2AD、HREM、ESA、FEM；局部级：NAAF、RCAR、CHAN、LAPS、X-Dim），且这些基线仅使用配对数据训练。
  - 噪声场景下对比了4种专门针对噪声对应的方法（NCR、DECL、MSCN、CREAM）。
- **评价指标**：Recall@1/5/10 及 rSum（总和），双向检索（图像→文本、文本→图像）。

## 4. 资源与算力
- 论文中提到实验在 **Nvidia GeForce RTX 3090 和 A800 GPU** 上运行，但未明确说明具体数量、训练时长、算力消耗等细节。

## 5. 实验数量与充分性
- 实验数量充足：涵盖了半配对（3个数据集+不同配对量）、噪声设置（3个噪声率+真实噪声数据集）、消融实验（8种变体）、在Drone-SP上的现实应用验证。
- 充分性和公平性：所有基线统一了骨干网络；消融实验详细分析了每个组件的贡献；噪声实验覆盖20%~80%的噪声率，并包括真实噪声数据。实验设计较为客观、公平。

## 6. 主要结论与发现
- 在**半配对设置**下，RCSL在所有指标上显著优于10种基线，尤其在配对数据极少（2.5K）时，多数基线无法收敛，而RCSL仍能通过未配对数据获益。
- 在**噪声设置**下，RCSL-NC在各类噪声率下均超过现有噪声对应学习方法，在高噪声（80%）下优势尤为明显（rSum提升41.7%和9.7%）。
- 在**真实场景Drone-SP**上，RCSL超越微调CLIP约23.6% rSum，证明了实用价值。
- 消融实验证实：SDL中的对齐-均匀正则项、RCM中的双向鲁棒挖掘均对性能有正向贡献，且两者结合效果最佳。

## 7. 优点
- **范式创新**：首次系统研究半配对跨模态学习，并提出完整框架，理论分析扎实。
- **方法鲁棒性**：RCM损失函数具有理论保证的噪声耐受性，避免了传统对比损失（如InfoNCE、TRL）的过拟合问题。
- **实验全面**：覆盖多个数据集、多种设置（不同配对量、不同噪声率、真实噪声），消融实验充分。
- **实际可用性**：在自建Drone-SP上验证了在真实数据稀少场景下的有效性，且可利用未配对数据大幅提升性能。

## 8. 不足与局限
- **计算资源未详细说明**：论文未报告训练时长、GPU数量、显存占用等，不利于复现和性能评估。
- **泛化性有待加强**：实验仅集中于图像-文本检索，未在其他模态对（如视频-文本、音频-文本）上验证。
- **理论假设较强**：RCM的噪声鲁棒性证明依赖于均匀噪声假设，而真实噪声可能非均匀，理论保证可能不严格成立。
- **伪配对构建简单**：仅用最近邻相似度，未考虑更复杂的匹配策略（如跨模态哈希或聚类），可能在复杂场景下引入更多噪声。
- **未与大规模预训练模型（如CLIP、ALIGN）的微调方法进行公平对比**：虽然在Drone-SP中对比了CLIP微调，但未在主要基准上比较CLIP的半配对微调变体。

（完）
