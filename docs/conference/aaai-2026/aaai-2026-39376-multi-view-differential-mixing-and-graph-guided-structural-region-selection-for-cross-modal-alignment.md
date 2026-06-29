---
title: Multi-View Differential Mixing and Graph-Guided Structural Region Selection for Cross-Modal Alignment
title_zh: 多视图差异混合和图引导结构区域选择用于跨模态对齐
authors: "Linlin Ji, Li Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39376/43337"
tags: ["query:multimodal"]
score: 5.0
evidence: 多视图差异混合和图引导区域选择的跨模态对齐
tldr: 跨模态对齐中全局和局部方法常忽略相互依赖。本文提出MG-Net，包括多视图差异混合器（捕获全局表示）和图引导结构区域选择器（保留局部空间拓扑）。两个模块协同工作，在多个跨模态检索基准上达到最先进结果，优于分别考虑全局或局部的方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39376/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 888, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39376/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 662, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39376/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1742, \"height\": 774, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39376/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1440, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39376/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 859, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39376/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1827, \"height\": 1122, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39376/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 804, \"height\": 1086, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39376/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 883, \"height\": 494, \"label\": \"Table\"}]"
motivation: 现有跨模态对齐方法忽视全局与局部特征的相互依赖关系。
method: 设计多视图差异混合器和图引导结构区域选择器联合建模全局和局部。
result: 在多个跨模态检索数据集上取得最优性能。
conclusion: 为跨模态对齐提供了兼顾全局和局部的新框架。
---

## Abstract
Cross-modal alignment is a promising yet challenging task in multimodal learning. Existing methods typically assess it by measuring the cross-modal semantic similarity from both global and local perspectives. However, these methods often neglect their potential interdependence. Specifically, global matching methods suffer from the over-compression of local features, while local matching methods rarely consider the inherent spatial topology of image patches. To address these limitations, we propose MG-Net, a unified framework with two collaborative modules: Multi-View Differential Mixer (MDM) and Graph-Guided Structural Region Selector (GSRS). The MDM is designed to capture discriminative global representations. It generates a series of views by decomposing feature vectors through multi-order differential operations, and adaptively fuses them via a lightweight Mixture-of-Experts (MoE) network. Meanwhile, the GSRS organizes image patches as a spatial graph and employs text-guided contextual reasoning to select spatially coherent and semantically complete structural regions. Extensive experiments on the Flickr30K and MS-COCO benchmarks demonstrate that the proposed MG-Net outperforms state-of-the-art methods in most cases.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：跨模态对齐是多模态学习中的关键任务，现有方法通常从全局（global）和局部（local）两个视角衡量语义相似度，但普遍忽视了二者的相互依赖关系。全局方法（如简单池化）过度压缩局部特征，导致信息瓶颈；局部方法（如固定网格分割）忽略图像块的空间拓扑结构，选取的视觉区域分散、语义不连贯。
- **核心问题**：如何同时提升全局表示的判别性和局部表示的空间语义完整性，使二者协同工作，从而突破现有方法的性能瓶颈。
- **整体含义**：本文提出MG-Net统一框架，通过多视图差异混合器（MDM）和图引导结构区域选择器（GSRS）分别解决全局和局部缺陷，实现更精准的跨模态对齐。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用多阶差分操作生成特征的多视图表示，并通过轻量级MoE自适应融合，增强全局表示；同时构建图像块的空间拓扑图，通过文本引导的图注意力网络选择空间连贯、语义完整的结构区域，用于局部匹配。

- **关键技术细节**：
  - **Token特征提取**：使用预训练ViT/Swin作为视觉编码器，BERT作为文本编码器，提取图像块特征 \(V \in \mathbb{R}^{N\times d}\) 和单词特征 \(T \in \mathbb{R}^{M\times d}\)。
  - **多视图差异混合器（MDM）**：
    - 基视图：选择L1范数最大的K个特征，加权平均得到 \(V^0_{glo}\)。
    - 差分视图：对每个块特征计算c阶差分（\(\Delta^c v_i\)），以差分的L2范数作为显著性分数，选出top-K索引，加权平均得到 \(V^c_{glo}\)（\(c=1,\dots,C\)）。
    - 融合：将所有视图通过轻量级MoE（MLP+Softmax加权）动态融合为最终全局视觉特征 \(V_{glo}\)；文本端相同操作得到 \(T_{glo}\)；余弦相似度计算 \(S_g(I,S)\)。
  - **图引导结构区域选择器（GSRS）**：
    - 文本引导：利用全局文本特征生成缩放参数 \(\gamma_i\) 和偏置 \(\beta_i\)，对每个视觉特征进行仿射变换后与文本特征拼接，得到 \(v'_i\)。
    - 空间图构建：将图像块视为节点，根据空间邻接关系（8邻域）构建图 \(G=(V,E)\)。
    - 图注意力网络（GAT）：计算邻居间注意力权重 \(\alpha_{ij}\)，更新节点特征为 \(h'_i\)（汇聚空间上下文）。
    - 可微分选择：对各节点logits使用Gumbel-Softmax采样得到选择概率掩码 \(M\)。
  - **模态内/间交互**：
    - 使用掩码 \(M\) 过滤原始视觉特征 \(V'\)，通过交叉注意力增强跨模态特征 \(V_{cross}\)。
    - 计算模态内上下文向量 \(\bar{v}_{glo}\)，再与局部特征点积得到显著性图 \(S_V\)；文本侧同理。
    - 通过门控机制融合 \(S_V\) 和 \(S_T\)，再经MDM得到最终表示，计算相似度 \(S_m(I,S)\)。
  - **损失函数**：双向三元组损失（含难负样本挖掘），同时作用于 \(S_g\) 和 \(S_m\)，总损失 \(L = L_g + \lambda L_m\)。

## 3. 实验设计

- **数据集**：
  - **Flickr30K**（约31k图像，每图像5个描述）
  - **MS-COCO**（1K测试集和5K测试集）
- **评估指标**：Recall@K（K=1,5,10），rSum（六项R@K之和），涵盖图像到文本（I->T）和文本到图像（T->I）两个方向。
- **对比方法**：
  - 全局方法：VSE++、GPO、HREM
  - 局部方法：SCAN、IMRAM、CAAN、LAPS、PICO等
  - 对比方法均使用相同骨干网络（ViT-Base-224、Swin-Base-224、Swin-Base-384）以保证公平。
- **实现细节**：
  - 统一特征维度 \(d=512\)，训练30个epoch，AdamW优化器。
  - 图像分辨率224×224或384×384，对应不同patch大小。

## 4. 资源与算力

论文中**未明确说明**所使用的GPU型号、数量、训练总时长等具体算力信息。仅在计算复杂度分析中提到MG-Net在Flickr30K（Swin-224）上推理耗时7.01秒，远快于LAPS（17.37秒）和VSE++（9.78秒），但训练资源未给出。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验：在两个数据集（Flickr30K、MS-COCO-1K和MS-COCO-5K）上，采用三种骨干网络配置，对比7种以上基线方法（每个配置均给出完整R@1/5/10及rSum），共约6×3=18组对比实验。
  - 消融实验：在Flickr30K（Swin-224）上进行，评估MDM的不同差分阶数（C=0,1,2,3）以及GSRS去除图引导（w/o G）和去除文本引导（w/o T）的效果。
  - 定性分析：可视化GSRS选择的结构区域（图4）和细粒度对齐矩阵（图5）。
  - 复杂度分析：比较推理时间。
- **充分性与公平性**：实验较为充分。对比方法均使用相同骨干网络，超参数（margin α、批次样本）保持一致。消融实验覆盖了各模块的贡献。但未进行跨数据集泛化实验（如在DomainNet等更复杂场景测试），也未进行人机评估，存在一定局限。

## 6. 主要结论与发现

- MG-Net在几乎所有设置下均超越当前最先进方法（SOTA）。例如：
  - Flickr30K（Swin-384）上rSum达到556.4，比PICO（548.2）高8.2；I->T R@10达到100%。
  - MS-COCO（Swin-384）上rSum达到472.3，优于PICO（471.8）。
- MDM通过多阶差分视图显著提升全局表示质量：仅使用C=2即可获得544.0 rSum，高于max pooling（541.7）。
- GSRS选择空间连贯、语义完整的区域，避免了传统方法的碎片化问题，定性结果和稀疏对齐矩阵验证了有效性。

## 7. 优点

- **创新性**：首次将多阶差分分解用于跨模态对齐的全局表示，提出了新颖的多视图融合策略。
- **实用性**：复杂度保持线性（\(O(Nd)\)，C≤3），推理速度显著快于同类局部方法。
- **可解释性**：通过可视化展示GSRS选择的结构化区域和对齐矩阵，增强了模型可解释性。
- **全面性**：在多个骨干网络和数据集上验证，消融实验覆盖差分阶数、图引导、文本引导等关键组件。

## 8. 不足与局限

- **实验覆盖有限**：仅在两个标准检索数据集（Flickr30K、MS-COCO）上测试，缺少在大规模多样化数据集（如Conceptual Captions、Laion）或零样本/跨域场景下的验证。
- **计算资源未披露**：未报告训练所需GPU数量、型号及时长，影响其他研究者的复现和效率判断。
- **方法设计偏重图像**：MDM差分操作在文本特征上的有效性可能较弱（文本序列长度可变且语义离散），论文未深入分析文本端差分的效果。
- **潜在偏差风险**：模型性能可能受预训练骨干（ViT/BERT）的分布影响，未讨论在低资源或小规模数据上的行为。
- **对比方法选择**：未与最新的基于大语言模型或扩散模型的图文对齐方法（如CLIP-based fine-tuning的先进方法）进行比较，部分基线年代较早（如VSE++、SCAN）。

（完）
