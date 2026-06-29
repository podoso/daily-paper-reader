---
title: "ReProCon: Scalable and Resource-Efficient Few-Shot Biomedical Named Entity Recognition"
title_zh: ReProCon：可扩展且资源高效的少样本生物医学命名实体识别
authors: "Jeongkyun Yoo, Nela Riddle, Andrew Hoblitzell"
date: 2025-09-07
pdf: "https://openreview.net/pdf?id=Gs79UZy99p"
tags: ["query:ie"]
score: 8.0
evidence: 生物医学领域的少样本命名实体识别
tldr: 本文提出ReProCon，一种少样本生物医学命名实体识别框架。结合多原型建模、余弦对比学习和Reptile元学习，使用轻量级fastText+BiLSTM编码器，在内存占用大幅降低的同时达到接近BERT的性能。有效解决数据稀缺和标签不平衡问题。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-gs79uzy99p/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 690, \"height\": 1462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-gs79uzy99p/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1091, \"height\": 1019, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-gs79uzy99p/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1171, \"height\": 1021, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 889, \"height\": 1141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 892, \"height\": 1085, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 893, \"height\": 530, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 893, \"height\": 448, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 821, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1440, \"height\": 1060, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-gs79uzy99p/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1201, \"height\": 462, \"label\": \"Table\"}]"
motivation: 生物医学NER面临数据稀缺、标签分布不平衡，且大型模型资源消耗高。
method: 采用多原型建模、余弦对比学习和Reptile元学习，使用轻量级编码器。
result: 在多个少样本NER基准上性能接近BERT，内存占用显著降低。
conclusion: 为资源受限场景下的NER提供了高效且性能良好的方案。
---

## Abstract
Named Entity Recognition (NER) in biomedical domains faces challenges due to data scarcity and imbalanced label distributions, especially with fine-grained entity types. We propose ReProCon, a novel few-shot NER framework that combines multi-prototype modeling, cosine-contrastive learning, and Reptile meta-learning to tackle these issues. By representing each category with multiple prototypes, ReProCon captures semantic variability, such as synonyms and contextual differences, while a cosine-contrastive objective ensures strong interclass separation. Reptile meta-updates enable quick adaptation with little data. Using a lightweight fastText + BiLSTM encoder with much lower memory usage, ReProCon achieves a macro-F_1 score close to BERT-based baselines (around 99 percent of BERT performance). The model remains stable with a label budget of 30 percent and only drops 7.8 percent in F_1 when expanding from 19 to 50 categories, outperforming baselines such as SpanProto and CONTaiNER, which see 10 to 32 percent degradation in Few-NERD. Ablation studies highlight the importance of multi-prototype modeling and contrastive learning in managing class imbalance. Despite difficulties with label ambiguity, ReProCon demonstrates state-of-the-art performance in resource-limited settings, making it suitable for biomedical applications.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：生物医学领域的命名实体识别（NER）面临严重的数据稀缺和标签分布极不平衡问题，尤其是细粒度实体类型（如UMLS中的多种语义类型）。现有方法在大规模类别（如50类）下性能显著下降，且依赖大规模预训练模型（如BERT）计算资源需求高。
- **背景**：传统少样本NER方法（如原型网络、MAML等）在一般域（Few-NERD）表现尚可，但在生物医学域因类别多样性、标签歧义和长尾分布而效果有限。同时，跨域迁移存在词汇和上下文差异。
- **整体含义**：本文旨在提出一种资源高效、可扩展的少样本NER框架，在有限标注和计算条件下接近BERT性能，特别适用于资源受限的生物医学应用。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **多原型建模**：每个类别使用多个原型向量（M=10）捕获语义变体（如同义词、不同上下文）。
- **余弦对比学习**：优化正交分离：实体跨度向量与正确类别的最近原型对齐，与错误类别远离。
- **Reptile元学习**：一阶元更新，避免二阶梯度开销，快速适应少量样本。
- **轻量编码器**：fastText + BiLSTM（仅需约99% BERT性能，但内存大幅降低）。

### 关键技术细节
1. **原型表示**：每个类别c有M个可学习原型向量，经ℓ2归一化。损失函数包括：
   - **原型排斥损失**：最大化不同原型间的余弦距离，避免原型坍塌。
   - **跨度对齐损失**：对每个类别c，计算查询跨度与c的M个原型的最小余弦距离，然后按类别归一化，鼓励正确类别的距离最小。

2. **跨度生成**：使用SpaCy分词，提取长度≤8 tokens的连续跨度（覆盖99.95%实体），标记位置（MARK_POSITION）。采用加权均值池化处理多token单词的fastText嵌入，再与正弦位置编码拼接。

3. **编码器**：两种配置：
   - fastText+BiLSTM：静态嵌入（300维）+ 位置编码（200维） → 单层双向LSTM（隐藏尺寸1024/方向） → 线性投影到512维。
   - BERT：用BERT-base-cased提取隐状态，采用均值-最大池化得到512维跨度表示。

4. **元学习（Reptile）**：
   - 每个episode：均匀采样N个类别（19或50），每个类别取K个支持样本、固定验证/查询样本。
   - 内部循环（E个epoch）：在支持集上训练任务模型；外部循环：将微调后参数与初始参数差值乘α（0.4/0.5）更新元模型。
   - 使用余弦学习率衰减、梯度裁剪（最大范数1.0）。

5. **硬负样本挖掘**：初轮训练后识别高置信度误分类跨度，再采样进行第二轮训练。

## 3. 实验设计

### 数据集
- **MedMentions**：生物医学NER标准语料，标注UMLS语义类型。经处理得到两种分类设置：
  - **19类**（深度约束level 3，低频合并阈值100）
  - **50类**（深度约束level 4，低频合并阈值50）
- 使用PageRank算法解决多标签歧义（选择最中心的类型）。

### 基准方法
- **基线**：SpanProto、CONTaiNER、NNShot、StructShot、Decomposed、ESD、Three-stage等（主要在Few-NERD上报告结果，因VRAM限制未能在MedMentions上复现）。
- **消融**：对比单原型（M=1）、交叉熵损失、无硬负样本挖掘。

### 主要对比
- fastText vs. BERT在不同训练-查询比例（0.3~0.8）下的macro-F1。
- 类别扩展性：19类→50类的F1下降率（7.8%），与文献中Few-NERD上的下降率（10%~32%）比较。
- 标签集扩展实验：将18类（除UnknownType）分成3组，分两阶段训练，评估新旧标签的F1变化。

## 4. 资源与算力

- **GPU**：单块NVIDIA L4（22.5GB VRAM），在Google Colab高RAM环境下运行。
- **训练时长**：未明确给出总时长，但提到内部epoch数（fastText: E=5, BERT: E=3）、元epoch数M未具体说明，外循环200个episodic任务集。
- **内存**：fastText+BiLSTM模型显著低于BERT，文中指出“much lower memory use”。

## 5. 实验数量与充分性

### 实验数量
- **主实验**：6种训练-查询比例（0.3~0.8）× 2种分类数（19/50）× 2种编码器（fastText/BERT）= 24组macro-F1结果（表1）。
- **可扩展性对比**：与8种基线方法的相对下降率对比（表2）。
- **消融实验**：4种配置（完整、单原型、硬负样本关闭、交叉熵）在19类0.3分割下的F1（表3）。
- **标签扩展实验**：3种分割（A/B/C）× 2阶段 × 3次迭代，报告Full F1和Base F1及p值（表4）。
- **混淆矩阵**：一个典型模型的分类细节（图3）。

### 充分性与公平性
- **充分**：覆盖了编码器对比、数据量变化、类别规模变化、消融、标签扩展，实验设计较全面。
- **客观/公平**：
  - 与基线对比存在局限：因资源限制未能在相同数据集（MedMentions）上训练基线模型，而是引用Few-NERD上的相对下降率，这导致可比性降低（作者已注明caveat）。
  - 超参数通过交叉验证选定，种子固定（42），保证可重复性。
  - 消融实验控制单一变量，结论清晰。

## 6. 主要结论与发现

- **性能接近BERT**：fastText+BiLSTM在19类和50类上的平均macro-F1分别为47.95%和49.45%，BERT分别为47.90%和52.01%，差异很小（约±2%）。
- **数据高效性**：使用30%训练数据时F1稳定甚至略高（50.80%），证明少样本能力。
- **类别可扩展性**：从19类扩至50类，F1仅下降7.8%，远优于基线（10~32%）。
- **多原型与对比学习关键**：单原型导致F1下降约1.7个百分点；交叉熵损失直接崩溃（2.7%）；硬负样本挖掘反而降低性能（从50.80%降至56.66%? 原文实际：关闭硬负样本后F1升至56.66%，但模型为50.80%，原因推测梯度不稳定）。
- **标签扩展鲁棒**：新增类别的引入对原有类别性能影响不显著（p>0.05多数）。

## 7. 优点

- **资源高效**：使用fastText+BiLSTM在极低计算成本下达到BERT水平，适合部署在受限环境。
- **多原型建模**：有效捕获语义多样性，优于单原型。
- **余弦对比损失**：在高维空间下比欧氏距离更稳定，解决类别不平衡。
- **Reptile元学习**：避免二阶梯度，训练快速稳定。
- **数据预处理**：通过PageRank消解多标签、通过层次整合减少稀疏类别，提升了学习效率。

## 8. 不足与局限

- **公平性受限**：无法在相同数据集上直接比较基线方法（因VRAM限制），引用不同数据集（Few-NERD）的相对下降率，比较不完全等价。
- **绝对性能较低**：macro-F1最高仅约56%（关闭硬负样本后），远低于实际应用要求（如80%+），可能仅适用于初步筛选。
- **硬负样本挖掘失效**：实验显示硬负样本反而使性能下降，表明方法在该设置下不稳定。
- **标签歧义问题**：混淆矩阵显示部分类别（如Activity、Phenomenon）相互误分类严重，表明模型对语义相似类别区分能力有限。
- **测试集单一**：仅在MedMentions（经处理后）上评估，未在其他生物医学NER语料（如BC2GM、NCBI-Disease）上验证，泛化性存疑。
- **代码与复现**：虽然提供了GitHub，但未明确说明环境配置和完整训练日志，复现可能存在门槛。

（完）
