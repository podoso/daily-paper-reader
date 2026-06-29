---
title: Unsupervised Semantic Discovery via Global and Local Semantic Alignment in Multimodal Clustering
title_zh: 基于全局与局部语义对齐的无监督多模态语义发现
authors: "Zhengzhong Zhu, Pei Zhou, Weihong Du, Shiquan Min, Jiangping Zhu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40832/44793"
tags: ["query:multimodal"]
score: 7.0
evidence: 无监督多模态语义发现，使用全局和局部对齐
tldr: 针对现有多模态聚类方法仅对齐实例层面而忽略语义一致性，以及对比学习中产生错误负样本的问题，提出GLAD方法。该方法在全局和局部语义层面进行对齐，全局语义对齐整合不同模态的语义表示，局部语义对齐保留细粒度语义结构。实验表明，GLAD在多个多模态基准上优于现有无监督方法，有效改善了语义发现质量。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 261, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1824, \"height\": 775, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1769, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1806, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 698, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40832/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 638, \"height\": 455, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40832/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 844, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40832/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 839, \"height\": 459, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40832/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40832/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 886, \"height\": 217, \"label\": \"Table\"}]"
motivation: 现有多模态聚类未能建模语义一致性且对比学习产生错误负对。
method: 提出全局和局部语义对齐（GLAD），分别对齐多模态数据的全局和局部语义。
result: 在多个多模态基准上取得最先进的无监督聚类效果。
conclusion: 通过语义级对齐有效缓解了模态差异和负样本噪声问题。
---

## Abstract
Unsupervised multimodal semantic discovery aims to learn discriminative representations from multimodal data. However, existing methods suffer from two key limitations. First, they only align instances across modalities without modeling semantic-level consistency, which fails to mitigate semantic bias caused by the gaps among feature distributions of multiple modalities. Second, they inevitably generate incorrect negative pairs during contrastive learning, pushing semantically similar samples apart.
To address these challenges, we propose GLAD (Global and Local semantic Alignment for unsupervised multimodal semantic Discovery), which aligns multimodal data at both global and local semantic levels. At the global level, GSA integrates multi-modal features into a shared space and employs joint clustering via optimal transport to capture common semantic patterns while mitigating cross-modality semantic bias. At the local level, LSA adaptively weights samples within each cluster based on their semantic importance, alleviating the effect of incorrect negative pairs.
Through the joint optimization of GSA and LSA, GLAD effectively captures both the global semantic structure and the local semantic nuances of multimodal data. Extensive experiments on three benchmark datasets demonstrate  GLAD significantly outperforms state-of-the-art methods, with an average improvement of 3.22%.

---

## 论文详细总结（自动生成）

# 论文总结：基于全局与局部语义对齐的无监督多模态语义发现

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有多模态无监督聚类方法存在两个关键局限。第一，它们仅对齐实例级别的跨模态表示，未建模语义级一致性，无法缓解多模态特征分布差异导致的语义偏差。第二，对比学习中不可避免地产生错误负样本对，将语义相似的样本推开。
- **研究背景**：多模态语义发现旨在自动从人类话语中挖掘潜在语义结构，应用于对话系统、客户查询、人机交互等。现有监督方法依赖标注，无监督方法如UMC虽然引入多模态，但未能解决上述问题。
- **本文目标**：提出GLAD框架，通过全局和局部语义对齐实现更准确、一致的语义发现。

## 2. 论文提出的方法论

### 核心思想
- 全局语义对齐（GSA）：将多模态特征整合到共享空间，利用最优传输（Optimal Transport, OT）进行联合聚类，捕获跨模态的共同语义模式，缓解语义偏差。
- 局部语义对齐（LSA）：基于样本在聚类空间中的语义重要性自适应加权，抑制不可靠样本，缓解错误负样本的影响。
- 联合优化GSA和LSA损失实现整体训练。

### 关键技术细节
1. **全局语义对齐（GSA）**：
   - 对每个样本的多模态特征取平均得到公共嵌入 \( h^c_i \)。
   - 在公共嵌入上执行k-means得到K个联合聚类中心。
   - 对每个模态m，计算余弦相似度矩阵 \( S_m \)，使用熵正则化OT得到软分配矩阵 \( Q_m^* \)（通过Sinkhorn算法求解）。
   - 对 \( Q_m^* \) 按列做softmax得到概率分配。
   - 损失包括：
     - KL散度损失 \( L_{kl} \)：迫使预测分布与OT分配对齐。
     - OT语义对齐损失 \( L_{OT} \)：包含语义匹配项和熵正则项。
     - 总GSA损失：\( L_{GSA} = L_{kl} + L_{OT} \)。

2. **局部语义对齐（LSA）**：
   - 计算各模态样本间的余弦相似度矩阵并取平均得到 \( S_{ij} \)。
   - 计算融合表示 \( \hat{h}_i \) 与各模态表示 \( h^m_i \) 的余弦相似度 \( C \)。
   - 基于结构相似度 \( s_{ij} \)（反映样本是否属于同一语义簇）对对比学习进行加权，抑制不相似样本的对比强度。
   - LSA损失 \( L_{LSA} \) 如式(14)，采用加权InfoNCE形式。

3. **联合训练**：
   - 总损失：\( L_{total} = \lambda_1 L_{GSA} + \lambda_2 L_{LSA} \)。

## 3. 实验设计
- **数据集**：三个多模态基准数据集——MIntRec、MELD-DA（M-DA）、IEMOCAP-DA（I-DA）。均为多模态意图/对话行为分类任务。
- **Benchmark**：对比六种先进无监督方法：SCCL、CC、USNID、MCN、UMC（仅文本）、UMC（完整多模态）。
- **评估指标**：归一化互信息（NMI）、准确率（ACC）、调整兰德指数（ARI）、Fowlkes-Mallows指数（FMI）。

## 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量或训练时长。仅在实验设置中提到使用预训练BERT和AdamW优化器，未提供硬件细节。因此算力信息不详。

## 5. 实验数量与充分性
- **主实验**：在三个数据集上各报告4项指标，与6种基线对比，结果清晰。
- **消融实验**：
  - 分别去除GSA、LSA、sij加权（w/o sij）评估各模块贡献。
  - 在GSA内部将OT替换为余弦相似度或完全移除OT。
- **统计显著性检验**：使用Almost Stochastic Order（ASO）方法在95%置信水平下检验GLAD与UMC、MCN、USNID的差异，所有ε_min均远小于0.5，表明显著优势。
- **可视化分析**：t-SNE特征可视化、混淆矩阵对比。
- **聚类方案对比**：k-means vs 预测向量argmax。
- **收敛性分析**：损失和性能随epoch变化的曲线。
- **超参数敏感性**：对τ、λ1、λ2进行实验。
- **评价**：实验覆盖全面，消融设计合理，统计检验增强说服力，实验公平且充分。

## 6. 论文的主要结论与发现
- GLAD在所有数据集上显著超越现有方法，平均提升3.22%（在I-DA上提升3.33%）。
- GSA和LSA均不可或缺，其中GSA贡献更大（移除后性能大幅下降）。
- 最优传输（OT）比简单余弦相似度更有效，是全局对齐的关键。
- LSA通过加权对比学习有效缓解了错误负样本问题。
- 模型收敛快（约50 epoch），且超参数调整在合理范围内表现稳健。

## 7. 优点
- **创新性强**：首次提出全局和局部语义对齐双重机制，超越实例级对齐，解决了模态语义偏差和错误负样本两大关键问题。
- **技术合理**：使用最优传输进行语义分配，理论基础扎实；局部自适应加权对比学习设计巧妙。
- **实验充分**：涵盖多数据集、多种基线、全面消融、统计检验、可视化、收敛分析和参数敏感性，结论可靠。
- **效果领先**：在三个基准上均达到SOTA，平均提升3.22%，且可视化显示聚类更紧凑。
- **可解释性好**：通过混淆矩阵和t-SNE图直观展示改进。

## 8. 不足与局限
- **计算复杂度高**：每轮迭代复杂度为 \( O(M(2B^2 + BKI + K^2)) \)，在大规模或实时应用中可能受限（作者也指出此局限）。
- **未提资源开销**：未说明GPU型号、数量及训练时间，影响可复现性。
- **数据集多样性有限**：仅使用三个英文对话数据集，跨语言、跨领域（如视觉主导数据）的泛化性未知。
- **超参数敏感**：λ1和λ2对性能影响较大，需仔细调参（论文通过实验给出建议值0.5）。
- **未探索模型规模影响**：所有方法均使用相同骨干网络（BERT等），未分析不同规模骨干对结果的影响。
- **应用限制**：依赖预训练模型，在低资源环境下可能受限。

（完）
