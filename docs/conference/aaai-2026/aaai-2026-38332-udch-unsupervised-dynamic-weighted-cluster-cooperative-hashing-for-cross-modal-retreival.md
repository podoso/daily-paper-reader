---
title: "UDCH: Unsupervised Dynamic Weighted Cluster-cooperative Hashing for Cross-modal Retreival"
title_zh: UDCH：无监督动态加权聚类协同哈希用于跨模态检索
authors: "Yuanzhi Zhao, Fan Yang, Yudong Zhao, Xiaoyu Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38332/42294"
tags: ["query:multimodal"]
score: 4.0
evidence: 无监督跨模态哈希
tldr: 本文提出无监督动态加权聚类协同哈希框架，同时建模实例级对齐和聚类级语义结构，用于跨模态检索，避免了人工标注，在标签缺失条件下提升检索性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38332/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 1009, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38332/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1625, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38332/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38332/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 895, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38332/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 490, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38332/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1672, \"height\": 786, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38332/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 735, \"height\": 388, \"label\": \"Table\"}]"
motivation: 无监督跨模态哈希难以建模模态间共享语义结构。
method: 设计实例级对比损失和聚类级伪标签来引导一致性学习。
result: 在跨模态检索任务上优于现有无监督方法。
conclusion: UDCH实现了有效的无监督跨模态检索。
---

## Abstract
In cross-modal retrieval tasks, unsupervised hash code learning still faces key challenges, including the difficulty of modeling shared semantic structures across modalities and the inability to adaptively balance multiple supervision objectives during optimization. To address these issues, we propose a novel Unsupervised Dynamic Weighted Cluster-Cooperative Hashing (UDCH) framework, which jointly models feature-level alignment and cluster-level semantic structure to guide consistency learning across modalities under label-free conditions. Specifically, we design an instance-level contrastive loss in the feature branch to align the embedding spaces of images and texts, while employing K-Means clustering to generate pseudo-labels and construct a cluster-center contrast mechanism that captures semantic grouping information.  Furthermore, we integrate cross-modal feature similarity to construct a high-order structure matrix, enabling fine-grained structural supervision. To enhance the synergy of multi-objective optimization, we introduce a dynamic weighting strategy that adaptively adjusts the contributions of the feature and cluster branches based on the degree of modal alignment and semantic compactness. Extensive experiments on multiple cross-modal retrieval benchmarks demonstrate that UDCH achieves superior semantic alignment and retrieval performance under unsupervised settings, validating the effectiveness of multi-level semantic modeling and adaptive collaboration mechanisms in unsupervised hashing tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：无监督跨模态哈希检索面临两大挑战：一是难以在无标签条件下有效建模模态间的共享语义结构；二是现有方法通常采用静态损失加权，无法在训练过程中自适应地平衡多个优化目标（如实例级对齐与结构级建模），导致收敛不稳定或模态融合欠佳。
- **背景**：跨模态哈希因存储和检索效率高而广泛应用于大规模多媒体检索，但大多数深度有监督方法依赖大量人工标注，限制了实际应用。因此，发展无监督跨模态哈希技术具有重要价值。现有无监督方法多侧重于实例级对比学习，忽略全局语义模式和高阶样本关系；且未充分利用聚类结构来监督语义学习。

### 2. 论文提出的方法论

- **核心思想**：同时建模特征级对齐与聚类级语义结构，通过动态加权机制自适应平衡多个学习目标，从而在无监督条件下获得语义一致且判别性强的哈希码。
- **关键技术细节**：
  1. **特征级实例对比学习**：使用InfoNCE损失对齐图像和文本的连续嵌入空间，获得细粒度语义基础。
  2. **聚类感知语义对齐**：
     - 对模态融合后的表示进行K-means聚类，得到软伪标签和聚类中心。
     - 设计两个对比损失：**结构引导对比损失 L<sub>CSL</sub>**：拉近共享中心与同一聚类内的模态特定中心，推远不同聚类中心；**跨模态聚类感知对比损失 L<sup>cross</sup><sub>CSL</sub>**：对属于同一聚类的图像-文本对进行正对比，对不同聚类的对进行负对比。
  3. **高阶语义矩阵构建**：利用二阶传播融合图像内、文本内及跨模态相似性，得到细化后的结构监督矩阵 Ŝ，并通过Frobenius范数回归损失 L<sub>struct</sub> 约束共识嵌入的相似性结构与之匹配。
  4. **动态加权策略**：基于当前批次的伪标签一致性（NMI）和模态特征差异（MMD²）计算特征分支权重 w<sub>fea</sub> 和聚类分支权重 w<sub>clu</sub>，并采用指数移动平均（EMA）平滑与早期预热（前若干轮固定权重0.5）以稳定训练。
  5. **总损失**：L<sub>total</sub> = w<sub>fea</sub> · L<sub>HIC</sub> + w<sub>clu</sub> · (L<sub>Cluster</sub> + L<sub>struct</sub>)

### 3. 实验设计

- **数据集**：
  - MIRFLICKR-25K（20015对有效，2000查询，余为库）
  - NUS-WIDE（选取前10类共186577对，2100查询）
  - MS COCO（122218对，5000查询）
- **Benchmark与对比方法**：与6种无监督跨模态哈希方法（DJSRH、JDSH、AGCH、CIRH、SCH、VLKD）对比。
- **评估指标**：mAP（16/32/64/128位）、Top-N精度曲线、收敛曲线、t-SNE可视化、聚类数敏感度分析。
- **检索方向**：图像到文本（I→T）和文本到图像（T→I）。

### 4. 资源与算力

- 论文明确说明：**单块NVIDIA GeForce RTX 3080 Ti GPU**，使用PyTorch框架，Adam优化器（学习率5e-4，权重衰减1e-6），批大小256，InfoNCE温度τ=0.9，动态加权参数β=0.3，EMA平滑系数ρ=0.9。
- **未提及**：具体训练时长、总训练轮数、模型参数量等细节。

### 5. 实验数量与充分性

- **数量**：共进行三大类实验：
  - 主表（表1）：3个数据集 × 4种码长 × 2个检索方向 = 24个mAP数值对比。
  - 可视化：Top-N精度曲线（3数据集）、收敛曲线（2个数据集）、t-SNE聚类对齐图。
  - 超参数分析：聚类数K敏感度（1~25）。
  - 消融实验（表2）：逐步去掉L<sub>Cluster</sub>、L<sub>struct</sub>、动态权重，在MS COCO 128位上验证各模块贡献。
- **充分性**：实验覆盖了多种码长、多个数据集、双向检索，并进行了详细的消融和参数分析，对比方法均为近年代表性工作，实验设计客观、公平，结论可信度高。

### 6. 论文的主要结论与发现

- UDCH在所有三个数据集、四种码长、两个检索方向上均显著优于所有对比方法，尤其在大规模、语义复杂的数据集（如MS COCO）上优势更明显。
- 动态加权策略有效平衡了特征级与聚类级学习，提升了训练稳定性和最终性能。
- 聚类感知模块增强了类内紧凑性和类间可分性，t-SNE可视化证实了嵌入空间的语义分离。
- 消融实验表明：各损失组件均有贡献，完整模型达到最佳效果（MS COCO 128位 I→T 91.35%，T→I 91.15%）。

### 7. 优点

- **方法新颖**：首次将动态加权机制引入无监督跨模态哈希，自适应调整多目标损失配比。
- **多层次语义建模**：同时利用实例级、聚类级和高阶结构级信息，形成全局-局部-结构闭环，弥补了传统方法只关注局部对齐的不足。
- **实验扎实**：覆盖多个基准、多种码长、丰富可视化，且对聚类数、各损失组件进行了充分分析和验证。
- **代码与可复现**：虽未在文中公开代码，但提供了详尽超参数配置，便于复现。

### 8. 不足与局限

- **实验局限**：未报告训练时间/效率与模型参数量，在大规模流式或开放词汇场景下的泛化能力仅作为未来工作提及。
- **偏差风险**：聚类数K需预设，实验中使用约类别数三分之一的经验值，但未给出自动选择K的方法；不同数据集K不同，依赖先验知识。
- **应用限制**：当前框架为批处理式离线训练，未考虑在线或流式跨模态检索场景；且需要图像和文本成对出现，对缺失模态或不对齐数据可能鲁棒性不足。
- **可解释性**：动态权重基于NMI和MMD²，但未深入分析其在训练过程中的变化规律与语义关联。

（完）
