---
title: "MyGram: Modality-aware Graph Transformer with Global Distribution for Multi-modal Entity Alignment"
title_zh: MyGram：面向多模态实体对齐的模态感知图Transformer与全局分布
authors: "Zhifei Li, Ziyue Qin, Xiangyu Luo, Xiaoju Hou, Yue Zhao, Miao Zhang, Zhifang Huang, Kui Xiao, Bing Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39003/42965"
tags: ["query:multimodal"]
score: 7.0
evidence: 多模态实体对齐，视觉-语言，图Transformer
tldr: 针对多模态知识图谱实体对齐中模态结构上下文信息被忽视的问题，提出MyGram模型，包含模态扩散学习模块以捕捉深度结构上下文并实现细粒度多模态融合，通过全局分布对齐有效提升实体对齐性能，实验表明其优于现有方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法忽略每个模态内的结构上下文信息，易受浅层特征干扰。
method: 开发模态扩散学习模块捕获模态内深度结构上下文，并设计全局分布对齐实现细粒度多模态融合。
result: 在多个多模态实体对齐数据集上，MyGram显著优于现有方法。
conclusion: 模态感知的结构上下文建模对多模态实体对齐至关重要。
---

## Abstract
Multi-modal entity alignment aims to identify equivalent entities between two multi-modal Knowledge graphs by integrating multi-modal data, such as images and text, to enrich the semantic representations of entities. However, existing methods may overlook the structural contextual information within each modality, making them vulnerable to interference from shallow features. To address these challenges, we propose MyGram, a \textbf{m}odalit\textbf{y}-aware \textbf{gra}ph transformer with global distribution for \textbf{m}ulti-modal entity alignment. Specifically, we develop a modality diffusion learning module to capture deep structural contextual information within modalities and enable fine-grained multi-modal fusion. In addition, we introduce a Gram Loss that acts as a regularization constraint by minimizing the volume of a 4-dimensional parallelotope formed by multi-modal features, thereby achieving global distribution consistency across modalities. We conduct experiments on five public datasets. Results show that MyGram outperforms baseline models, achieving a maximum improvement of 4.8\% in Hits@1 on FBDB15K, 9.9\% on FBYG15K, and 4.3\% on DBP15K.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：多模态实体对齐（MMEA）旨在融合图像、文本等多模态数据来识别跨知识图谱的等价实体。现有方法多采用模态内对比学习，忽略了每个模态内部的**结构上下文信息**，导致易受浅层特征干扰（如视觉或属性相似但本体不同的实体）。
- **动机**：需要更精细地捕获模态内部的结构语义，并实现跨模态特征的全局一致性，以提升对齐鲁棒性。

### 2. 方法论
- **核心思想**：提出 **MyGram** 框架，包含两个关键模块：
  - **模态扩散学习（Modality-aware Diffusion Learning）**：对每种模态（结构、关系、属性、视觉）分别执行图卷积扩散，捕获高阶邻居信息，得到富含结构上下文的模态特征；随后用 Transformer 自注意力机制融合多模态特征。
  - **Gram 全局分布对齐（Gram-based Distribution Alignment）**：构造 4 维平行体（由源实体的结构特征与目标实体的视觉、属性、关系特征组成），通过最小化其体积（Gram 矩阵行列式的平方根）作为正则化约束，强制跨模态特征保持几何上的一致分布。
- **关键技术细节**：
  - 结构特征：采用 RRGAT（关系反射图注意力网络）聚合邻居。
  - 关系、属性、视觉特征：先线性投影到共享空间，再经 MGD（模态图卷积扩散）迭代传播（公式 5-6）。
  - 融合：多头自注意力（公式 7-8），按注意力权重加权融合（公式 9-10）。
  - 损失函数：总损失 \( \mathcal{L} = \mathcal{L}_{\text{InfoNCE}} + \lambda \mathcal{L}_{\text{Gram}} \)，其中 Gram 损失基于 top-K 候选实体的平行体体积计算（公式 16）。
- **算法流程**：特征提取 → 模态扩散 → Transformer 融合 → 联合损失训练。

### 3. 实验设计
- **数据集与场景**：
  - 跨知识图谱：FB15K-DB15K（FBDB15K）、FB15K-YAGO15K（FBYG15K），种子比例 20%、50%、80%。
  - 双语：DBP15K（ZH-EN、JA-EN、FR-EN），种子比例 30%。
- **基准对比方法**：PoE、MMEA、MSNEA、MCLEA、ACK-MMEA、MoAlign、MEAformer、GEEA、SimDiff、DESAlign、PMF、IBMEA、SNAG、GSIEA 等 14 种 SOTA 方法。
- **评估指标**：Hits@1、Hits@10、MRR。

### 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量及训练时长。仅提及参数设置：隐藏层 300 维，训练 1000 轮，学习率 5e-3，VGG-16 提取图像特征，Transformer 中间层 400 维、5 个注意力头。硬件资源信息缺失。

### 5. 实验数量与充分性
- **实验数量**：主表对比 9 个设置（3 个跨 KG 数据集 × 3 种子比例 + 3 个双语数据集 × 1 种子比例）；模态消融 2 个数据集（表 3）；关键组件消融 2 个数据集（图 3）；低资源实验（种子比例 5%~30%）；案例研究 1 例。
- **充分性**：覆盖了不同规模、不同语言、不同稀疏度的场景，对比方法全面，消融实验验证了每个模块的贡献，低资源实验证明了鲁棒性。实验设计客观、公平（采用统一种子比例和评估指标）。

### 6. 主要结论与发现
- MyGram 在所有数据集和指标上**显著超越**现有方法：FBDB15K 上 Hits@1 最高提升 4.8%，FBYG15K 上提升 9.9%，DBP15K 上提升 4.3%。
- 模态扩散学习有效抑制了浅层特征干扰，Gram Loss 提升了跨模态语义一致性。
- 关系模态贡献最大；低资源场景（5%~30% 种子）下 MyGram 保持领先（如 FBDB15K 30% 种子时 Hits@1 达 0.696，优于 SimDiff 的 0.589）。
- 案例显示 MyGram 能正确对齐受浅层干扰的实体（如“上海” vs “香港”）。

### 7. 优点
- **方法创新**：首次将模态内图卷积扩散引入 MMEA，捕获结构上下文；Gram Loss 从几何体积角度约束跨模态分布，对比传统点式对比学习更具全局性。
- **实验全面**：涵盖跨 KG 和双语场景、多种种子比例、详细消融、低资源测试，代码开源。
- **性能突出**：在多个数据集上取得 SOTA，尤其低资源场景提升明显，实用性强。

### 8. 不足与局限
- **硬件资源未报告**：无法评估模型的可复现性与计算开销。
- **模态数量假设**：Gram Loss 构造 4 维平行体需要恰好四种特征（结构、视觉、属性、关系），若模态不足（如缺少某些属性）或模态数更多，需调整设计。
- **场景覆盖有限**：未在真实噪声环境、大尺度 KG 或跨语言异构图下测试；未评估对缺失模态（如图像缺失严重）的鲁棒性。
- **未来工作**：论文提及计划结合大语言模型（LLM），但当前未探索其潜力，故方法在复杂语义理解上可能仍有局限。

（完）
