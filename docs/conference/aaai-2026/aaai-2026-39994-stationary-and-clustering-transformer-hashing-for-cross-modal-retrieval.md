---
title: Stationary and Clustering Transformer Hashing for Cross-modal Retrieval
title_zh: 基于平稳分布与聚类Transformer哈希的跨模态检索
authors: "Zhan Yang, Yiran Liu, Youyuan Huang, Yinan Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39994/43955"
tags: ["query:multimodal"]
score: 8.0
evidence: 无监督跨模态哈希，Transformer，对比哈希用于跨模态检索
tldr: 针对无监督跨模态哈希中语义鸿沟和细粒度全局结构缺失问题，提出SCTH方法，采用Transformer模态融合编码器和对比哈希学习统一二值表示，有效缩小跨模态语义差距。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39994/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1747, \"height\": 907, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39994/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1842, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39994/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1836, \"height\": 1357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39994/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1842, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39994/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1841, \"height\": 343, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39994/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39994/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1844, \"height\": 461, \"label\": \"Table\"}]"
motivation: 现有方法难以在无标签情况下弥合跨模态语义差距并捕获细粒度全局结构。
method: 提出SCTH，利用Transformer模态融合编码器提取跨模态表示，结合对比哈希学习。
result: 在多个跨模态检索基准上取得优异性能，并具有低存储和高效率优势。
conclusion: 该方法为无监督跨模态检索提供了新的有效范式。
---

## Abstract
Unsupervised cross-modal hashing has gained significant attention for efficient retrieval between heterogeneous modalities through encoding data into the unified binary representations, offering low storage cost and fast response. However, the constraints of existing methods persist in bridging the cross-modal semantic gap and capturing fine-grained global semantic structures without explicit labels. In this paper, we propose an innovative unsupervised Stationary distribution and soft Clustering Transformer Hashing approach for cross-modal retrieval, denoted as SCTH. Initially, a Transformer-based modality fusion encoder is employed to extract abundant cross-modal semantic representations, further integrated with contrastive hashing to minimize the semantic gap. To enhance the inter-modal alignment, a pseudo-classifier clustering module with entropy-regularized contrastive loss is presented, ensuring balanced and diverse cluster assignments in unsupervised settings. Additionally, a Markovian stationary distribution strategy stabilizes the feature representations through mitigating the interference of noise and outliers. Comprehensive experiments on MIRFlickr, NUS-WIDE, and IAPR-TC12 datasets validate that SCTH outperforms state-of-the-art hashing methods in cross-modal retrieval tasks, demonstrating superior generalization performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：跨模态检索（如图像检索文本、文本检索图像）在多媒体数据快速增长下需求迫切，但多数实际数据缺乏标签。无监督跨模态哈希方法旨在将异构模态数据编码为统一的二值哈希码，在节省存储和加快检索速度的同时，无需人工标注。然而现有无监督方法面临三大挑战：(1) 模态间语义鸿沟难以弥合，缺乏有效的特征对齐机制；(2) 无标签环境下硬聚类或简单相似度度量导致样本分配不准确，破坏语义完整性；(3) 大多方法仅关注局部样本关系，忽略全局语义结构，易受噪声和离群点干扰。
- **整体含义**：本文提出一种创新的无监督跨模态哈希方法 **SCTH**（Stationary and Clustering Transformer Hashing），通过融合 Transformer 的全局语义建模、软聚类的伪监督机制以及马尔可夫平稳分布的结构稳定性，在无标签条件下生成语义一致且鲁棒的哈希码，显著提升跨模态检索性能。

## 2. 论文提出的方法论

### 核心思想
SCTH 包含三个核心模块，端到端联合优化：
1. **基于 Transformer 的多模态表示融合**：利用标准 Transformer 编码器融合图像和文本特征，增强跨模态信息交互，并通过对比哈希目标缩小语义差距。
2. **个体模态特定的软聚类模块**：为每个模态设置伪分类器，生成软聚类分配（概率分布），并通过带熵正则化的跨模态对比损失确保聚类分配平衡多样，促进模态间语义对齐。
3. **基于马尔可夫平稳分布的全局监督**：利用融合表示构建转移概率矩阵，通过迭代求得平稳分布，将平稳概率作为权重指导哈希特征的相似性保持，抑制噪声和离群点的影响。

### 关键技术细节与公式（文字说明）
- **模态融合**：图像和文本特征经线性变换后拼接，作为 Transformer 编码器输入，通过自注意力机制得到融合表示 \(\mathbf{F}'\)。进一步分解为图像和文本特定表示 \(\mathbf{F}_I\)、\(\mathbf{F}_T\)，并计算对比损失 \(L_{\text{fusion}}\)（包含表示级和哈希特征级对比）。
- **哈希特征生成**：通过 MLP 将融合表示映射为哈希特征 \(\mathbf{H}_I\)、\(\mathbf{H}_T\)。
- **软聚类**：对每个模态的特征通过伪分类器得到软聚类矩阵 \(\mathbf{C}_m \in \mathbb{R}^{n \times c}\)，其行和为 1。定义聚类级对比损失 \(L_{\text{cluster}}\)，包含模态间聚类匹配与模态内聚类区分项，并加入信息熵正则化 \(H(\mathbf{C}_m)\) 鼓励均匀分布，防止崩塌。
- **马尔可夫平稳分布**：利用融合表示 \(\mathbf{F}_I\)、\(\mathbf{F}_T\) 构造转移概率矩阵 \(\mathbf{P} = \text{softmax}(\cos(\mathbf{F}_I, \mathbf{F}_T))\)，满足行随机性、不可约且非周期，根据 Perron-Frobenius 定理存在唯一正平稳分布 \(\pi\)。通过功率迭代法求解 \(\pi\)，并设计平稳损失 \(L_{\text{steady}} = \sum \pi_i \|\mathbf{P}_i - \mathbf{S}_{H,i}\|_2^2\)，其中 \(\mathbf{S}_H\) 为哈希特征相似矩阵，迫使重要样本的排列一致。
- **总损失**：\(L = \alpha L_{\text{fusion}} + \beta L_{\text{cluster}} + \gamma L_{\text{steady}}\)，超参数通过网格搜索确定。

## 3. 实验设计

- **数据集**：三个公开基准数据集：
  - **MIRFlickr**（24 类，约 25,000 图像-文本对，文本用 1386 维 BoW）
  - **NUS-WIDE**（10 个常见概念，约 187,000 对，文本用 1000 维 BoW）
  - **IAPR-TC12**（255 个标签，约 20,000 对，文本用 2912 维 BoW）
  每个数据集划分：5000 训练、2000 查询、剩余作为检索集。
- **基准任务**：图像→文本 (I→T) 和文本→图像 (T→I) 检索。
- **对比方法**：9 种近年主流无监督跨模态哈希方法：**DGCPN** (AAAI 21)、**CIRH** (TKDE 23)、**UCCH** (TPAMI 23)、**PT-FUCH** (ACM MM 23)、**CMCL** (TKDE 24)、**SCH** (TPAMI 24)、**GCMLH** (TNNLS 24)、**SMSH** (AAAI 25)、**VTM-UCH** (AAAI 25)。所有基线均使用开源代码复现。
- **评估指标**：平均检索精度（mAP，Top-50）和 Top-k 精度曲线（P@k）。

## 4. 资源与算力

- 原文仅提到实验硬件配置：Intel Xeon Silver 4210 CPU @2.20 GHz，NVIDIA GeForce RTX 4060，128 GB RAM。未明确说明训练时长、GPU 使用数量或能耗。因此无法评估具体算力消耗。

## 5. 实验数量与充分性

- **实验数量**：
  - **主表（Table 1）**：在三个数据集上针对四种哈希码长度（16、32、64、128 bits）报告 mAP，覆盖 I→T 和 T→I 两个方向，共 3×4×2 = 24 组结果。
  - **消融实验（Table 2）**：移除 Transformer 编码器（SCTH-T）、移除软聚类模块（SCTH-C）、移除平稳分布模块（SCTH-S），在相同设置下比较，共 3×3×4×2 = 72 组结果。
  - **参数灵敏度分析（Figure 3）**：对 α, β, γ, c 进行网格搜索，以 64 bits 为例，覆盖三个数据集。
  - **可视化与案例研究**：t-SNE 聚类可视化（Figure 4）和 Top-30 检索示例（Figure 5）。
- **充分性与客观性**：
  - 实验覆盖了所有主流基线，使用统一代码复现，公平性较好。
  - 消融实验分别验证了每个模块的贡献，具有清晰的因果归因。
  - 参数分析展示了方法对超参数变化不敏感，增强了鲁棒性。
  - 不足：未报告方差（如多次重复实验的标准差），也未讨论随机种子影响；未在更大规模数据集（如 COCO、Flickr30k）上验证；缺少与更近期（2025-2026）方法的比较（但已包括 AAAI 25 的方法，属同期）。

## 6. 论文的主要结论与发现

- SCTH 在所有三个数据集和所有码长下均显著超过已有无监督哈希方法，尤其在 I→T 任务上平均 mAP 提升 1.2%~1.5%，在 T→I 任务上提升 4.4%~5.3%，证明其跨模态对齐和全局结构建模的有效性。
- 消融实验表明三个模块均不可或缺，其中 Transformer 融合和软聚类贡献最大，平稳分布进一步稳定特征。
- 参数分析显示方法对候选值范围具有良好鲁棒性，聚类数 c 对性能影响不显著。
- 可视化表明软聚类明显改善了模态内部的区分性和模态间的对齐性。

## 7. 优点

- **创新性**：首次将马尔可夫平稳分布引入无监督跨模态哈希，利用稳态概率加权损失，有效抑制噪声与离群点。
- **完整性**：将 Transformer 的全局建模、软聚类的伪监督与平稳分布的稳定性有机结合，形成一个端到端可训练的框架。
- **实用性**：无监督设定适用于大量无标签场景，且对超参数不敏感，易于部署。
- **实验严谨性**：在三个不同规模、不同语义粒度的数据集上进行验证，消融实验和参数搜索设计完整，可视化直观。
- **理论支持**：利用 Perron-Frobenius 定理证明了平稳分布的存在性和收敛性，为方法提供理论依据。

## 8. 不足与局限

- **实验覆盖范围有限**：仅使用三个中等规模数据集，且图像特征均采用 VGG-19，未在更现代的特征（如 CLIP、ResNet）或更大规模数据集（如 Conceptual Captions）上验证。
- **计算资源未充分报告**：未提供训练时间、显存占用、收敛迭代次数等信息，难以与其他方法在效率上直接对比。
- **统计严谨性缺失**：未报告多次实验的均值与方差，也未讨论不同随机种子下的结果稳定性。
- **模块复杂度**：加入了 Transformer 和马尔可夫迭代，相比传统简单哈希方法可能带来额外计算开销，文中未做效率分析。
- **潜在偏见**：数据集的标签体系（类别数、图像质量）可能影响聚类模块性能；对比方法的部分实现可能未完全优化，导致 SCTH 的相对提升可能被放大。

（完）
