---
title: Multimodal Aligned Semantic Knowledge for Unpaired Image-text Matching
title_zh: 多模态对齐语义知识用于未配对图文匹配
authors: "Laiguo Yin, Yixin Zhang, YUQING SUN, Lizhen Cui"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=d3CISVVO6v"
tags: ["query:multimodal"]
score: 7.0
evidence: 多模态对齐语义知识用于图文匹配
tldr: 未配对图文匹配中，现有方法难以处理分布外词汇，且不同词的可视表示方差大。本文提出MASK，利用词嵌入作为桥梁关联词与对应原型，实现模态间语义知识对齐，并针对OOD词构造代表原型。实验表明该方法在多种匹配场景下优于基线，有效提升了跨模态对齐的鲁棒性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-d3cisvvo6v/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1442, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-d3cisvvo6v/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1429, \"height\": 942, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-d3cisvvo6v/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-d3cisvvo6v/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1414, \"height\": 1374, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1443, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1438, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1439, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1440, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1430, \"height\": 796, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 865, \"height\": 768, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1446, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1414, \"height\": 1374, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1437, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1301, \"height\": 611, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1445, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 727, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-d3cisvvo6v/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1444, \"height\": 319, \"label\": \"Table\"}]"
motivation: 未配对图文匹配中OOD词表示缺失且视觉表示方差大。
method: 提出MASK，用词嵌入作为桥梁，对齐图像原型和文本语义知识。
result: 在未配对匹配任务上取得最佳性能。
conclusion: 语义知识对齐可有效改善跨模态匹配对OOD词的鲁棒性。
---

## Abstract
While existing approaches address unpaired image-text matching by constructing cross-modal aligned knowledge, they often fail to identify semantically corresponding visual representations for Out-of-Distribution (OOD) words. Moreover, the distributional variance of visual representations associated with different words varies significantly, which negatively impacts matching accuracy. To address these issues, we propose a novel method namely Multimodal Aligned Semantic Knowledge (MASK), which leverages word embeddings as bridges to associate words with their corresponding prototypes, thereby enabling semantic knowledge alignment between the image and text modalities. For OOD words, the representative prototypes are constructed by leveraging the semantic relationships encoded in word embeddings. Beyond that, we introduce a prototype consistency contrastive loss to structurally regularize the feature space, effectively mitigating the adverse effects of variance. Experimental results on the Flickr30K and MSCOCO datasets demonstrate that MASK achieves superior performance in unpaired matching.

---

## 论文详细总结（自动生成）

## 论文中文总结

### 1. 核心问题与整体含义（研究动机和背景）

论文聚焦于**未配对图像-文本匹配（Unpaired Image-Text Matching）** 这一实际需求——即不依赖大规模配对数据，而是通过建模跨模态知识完成匹配。现有基于知识的方法（如MACK）面临两大挑战：

- **分布外（OOD）词汇的处理能力不足**：无法利用已知词汇的语义结构为OOD词汇构建可用的视觉原型。
- **视觉表示分布方差异质性**：不同词汇对应的区域表示方差差异大，导致某些偏移样本易被误分类，影响匹配准确率。

### 2. 方法论：核心思想、关键技术细节

**核心思想**：利用预训练词嵌入作为桥梁，将词汇与对应的视觉原型进行语义对齐，构建“多模态对齐语义知识（MASK）”。关键组件包括：

- **图像嵌入分支**：通过**原型感知编码器（PAE）** 将原始区域表示编码为潜在表示（μ, σ），并利用**特征恢复模块（FRM）** 重建原始表示以保留信息。损失函数包括**信息保留损失 \(L_{ir}\)**（KL散度 + MSE）和**原型一致性对比损失 \(L_{cl}\)**（拉近同类区域与原型、推远异类原型）。

- **文本嵌入分支**：使用预训练词向量（GloVe）获取词嵌入，并通过**模态迁移模型（MTM）** 将区域表示映射到词嵌入空间，同时施加**跨模态对齐损失 \(L_{cm}\)**（余弦对齐 + 结构保持正则化），使得映射保持语义关系。

- **OOD词汇处理**：对于不在知识库中的词，取其词嵌入与知识库中词嵌入的相似度，加权聚合最相近的 m 个原型的视觉表示，得到 OOD 词汇的伪原型。

- **匹配过程**：对图像区域提取表示，对文本词汇通过知识桥接得到原型表示，计算相似度矩阵后使用 **max-mean pooling** 得到全局相似度。

- **总体损失函数**：\(L = L_{ir} + \lambda_1 L_{cm} + \lambda_2 L_{cl}\)，联合优化以实现高内聚、低耦合的区域表示。

### 3. 实验设计

- **数据集**：Flickr30K（31,783幅图片，每图5句描述）和 **MSCOCO**（123,287幅图片，每图5句描述）。
- **评估指标**：R@1、R@5、R@10 及总和 Rs。
- **对比方法**：
  - 基于模型的方法：CHAN、DSRLN、CORA、BOOM、3SHNet。
  - 基于知识的方法：MACK、MACK-VG-M。
  - 零样本重排序场景：CLIP、ALBEF 作为基座，对比 MACK、LeaPRR、FR 等重排序策略。
- **实验场景**：
  - **未配对图文匹配**（主实验）
  - **零样本图文匹配**（重排序）
  - **跨数据集匹配**（MSCOCO→Flickr30K 和 Flickr30K→MSCOCO）
  - **OOD词汇分析、损失消融、超参数分析、采样尺寸分析、重排序权重分析**等。

### 4. 资源与算力

论文未明确说明训练所用 GPU 型号、数量及训练时长，仅在正文中提及使用 **Adam 优化器，学习率 1e-4**，以及批量大小（首200epoch 为4096，后200epoch为2048）。硬件细节缺失。模型总参数量约为 **8.1M**（见表8），测试时单样本时间约为 **0.04秒**（在 NVIDIA L40 上）。

### 5. 实验数量与充分性

论文进行了**大量且系统的实验**，包括：
- 4张核心基准表（Table 1-4），以及若干扩展表（Table 5-15）；
- 消融实验覆盖损失项（L_cm, L_cl）、OOD词汇、区域原型、max-mean pooling；
- 超参数灵敏度分析（λ1/λ2、α、采样尺寸 m）；
- 不同检测器（BUTD、DETR、DINO）对比；
- 不同预训练词向量（GloVe、Word2Vec、FastText）对比；
- 不同模型架构深度对比；
- 跨数据集泛化实验。

这些实验**覆盖了多个维度，对比基线全面，消融设计合理，且在多数据集上验证**，充分性较好。但在零样本重排序实验中，仅使用了 CLIP 和 ALBEF 两种基座模型，对其他大型多模态模型（如 BLIP-2）的泛化性未验证，存在一定局限性。

### 6. 主要结论与发现

- MASK 在 **未配对图文匹配** 和 **零样本重排序** 任务上均超越现有方法，尤其在 MSCOCO 上提升显著（Rs 达到 209.5，比 MACK 高约 7.8）。
- **OOD词汇的构建** 能有效提升匹配准确性（在 Flickr30K 上 Rs 从 116.2 升至 122.8）。
- **原型一致性对比损失 L_cl** 贡献最大，能显著降低类内方差、提高类间分离度。
- **跨模态对齐损失 L_cm** 通过结构保持约束使区域表示继承词嵌入的语义结构。
- 最优超参数配置为 λ1=λ2=3，采样尺寸 m=50，重排序权重 α=0.15。
- 使用 **GloVe 词向量** 优于 Word2Vec 和 FastText，因其全局共现统计更适合跨模态语义对齐。

### 7. 优点（亮点）

1. **创新的OOD词汇处理机制**：利用词嵌入的局部线性性质为 OOD 词插值原型，拓展了知识覆盖范围。
2. **双重损失结构**：同时优化信息保留、跨模态对齐和原型一致性，使区域表示具有高内聚低耦合特性。
3. **轻量灵活**：模型参数量仅 8.1M，测试时间短（0.04秒），易于集成到已有模型作为重排序模块。
4. **理论支撑充分**：附加证明（附录B-G）说明等距映射、余弦与欧氏距离等价性、梯度对结构保持的作用等，增强了方法可信度。

### 8. 不足与局限

1. **依赖特定检测器**：当前使用 BUTD（Faster-RCNN），实验表明若换成DETR/DINO（未在VG预训练）性能大幅下降，若换成更强骨架（如Swin）可提升，但未提供统一预训练设置下的全面对比。
2. **仅处理名词为主的词汇**：论文承认对副词、形容词、代词等非视觉词汇无效（见Table 10负面案例），这些词引入噪声。
3. **训练算力未报告**：缺乏GPU型号、数量及训练时长信息，难以复现和评估计算成本。
4. **零样本重排序基座有限**：仅测试了 CLIP 和 ALBEF，未验证在 BLIP、BLIP-2 等更强模型上的效果。
5. **跨数据集泛化增益有限**：在 MSCOCO→Flickr30K 上 R@1 提升约3-5%，但在 Flickr30K→MSCOCO 上提升较小，且文中未深入讨论原因。

（完）
