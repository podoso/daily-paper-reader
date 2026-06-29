---
title: Noise reduction in BERT NER SLM models for clinical entity extraction in clinical trials
title_zh: 临床试验中BERT NER SLM模型的噪声降低与实体抽取
authors: "Kuldeep Jiwani, Yash Kumar Jeengar, Ayush Dhaka"
date: 2025-09-05
pdf: "https://openreview.net/pdf?id=YyjjA5630A"
tags: ["query:ie"]
score: 9.0
evidence: 临床文本命名实体识别
tldr: 该论文针对临床实体抽取中NER模型精度不足的问题，提出噪声移除模型，通过分析概率序列并分类弱预测来提高精确率。方法直接应用于命名实体识别，属于信息抽取核心任务，且实验在临床数据上验证了有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-yyjja5630a/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1440, \"height\": 605, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1413, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 686, \"height\": 111, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 692, \"height\": 118, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1433, \"height\": 112, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1439, \"height\": 119, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 692, \"height\": 114, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 693, \"height\": 118, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1433, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 930, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1151, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1442, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-yyjja5630a/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1250, \"height\": 207, \"label\": \"Table\"}]"
motivation: 临床实体抽取需要高精确率，但传统NER模型召回高而精确不足。
method: 训练噪声移除模型分析NER输出的概率序列，将弱预测过滤或重分类。
result: 显著提升了临床实体抽取的精确率，同时保持召回。
conclusion: 后处理噪声移除是提升NER精度的有效手段，适用于高精度场景。
---

## Abstract
Precision is of utmost importance in the realm of clinical entity extraction from clinical notes and reports. Encoder Models fine-tuned for Named Entity Recognition (NER) are an efficient choice for this purpose, as they don't hallucinate. We pre-trained an in-house BERT over clinical data and then fine-tuned it for NER. These models performed well on recall but could not close upon the high precision range, needed for clinical models. To address this challenge, we developed a Noise Removal model that refines the output of NER. The NER model assigns token-level entity tags along with probability scores for each token. Our Noise Removal (NR) model then analyzes these probability sequences and classifies predictions as either weak or strong. A naïve approach might involve filtering predictions based on low probability values; however, this method is unreliable. Owing to the characteristics of the SoftMax function, Transformer based architectures often assign disproportionately high confidence scores even to uncertain or weak predictions, making simple thresholding ineffective. To address this issue, we adopted a supervised modeling strategy in which the NR model leverages advanced features such as the Probability Density Map (PDM). The PDM captures the Semantic-Pull effect observed within Transformer embeddings, an effect that manifests in the probability distributions of NER class predictions across token sequences. This approach enables the model to classify predictions as weak or strong with significantly improved accuracy. With these NR models we were able to reduce False Positives across various clinical NER models by 50\% to 90\%.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：在临床实体抽取（从电子病历、临床笔记中提取生物标志物、肿瘤分期等）中，要求极高精确率（Precision），但基于BERT微调的NER模型在召回上表现良好，却难以达到临床所需的高精确率。主要原因包括：真实临床数据的模糊性、标注不一致、采样偏差等引入的噪声；此外，SoftMax函数在Transformer中常对不确定或越界（OOD）预测赋予过高置信度，直接基于概率阈值过滤不可靠。
- **背景**：已有工作如温度缩放、MC Dropout等旨在校准概率或估计不确定性，但计算成本高或效果有限。作者旨在开发一种轻量级、可解释的后处理模型，在不修改原始NER模型的前提下过滤噪声预测，提升精确率。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：利用Transformer的自注意力机制导致相邻token概率分布存在“语义牵引效应”（Semantic-Pull），即真实实体附近的token也表现出非零的实体类概率，而虚假实体附近则无此特征。基于这一现象，构造概率密度图（Probability Density Map, PDM）及多种统计特征，输入决策树分类器，将NER预测分为“强”（Strong）和“弱”（Weak），弱预测视为噪声移除。

- **关键技术细节**：
  - **概率密度图（PDM）**：对于每个被预测为实体的token，以其位置为中心，将其邻域内所有token的概率向量（维度为K个NER类）按概率值分桶（例如B=10个桶），并用高斯衰减权重（`W_t = exp(-|t-t_pred|^2 / (2*R^2))`）对每个桶内的概率求和，形成3×10的特征图（若K=3）。该特征捕捉邻域内概率分布的密度差异。
  - **统计特征**：包括预测token、预测词、预测短语、相邻token、整个上下文的均值、最大值、变异系数、熵、概率比值、概率差值等。对每个NER类分别计算。
  - **分类器**：采用决策树（Decision Tree），因其可解释性，能够给出明确的决策路径，便于领域专家审查为何某实体被判定为噪声。

- **算法流程**（文字说明）：
  1. 输入一段文本，经过训练好的BERT NER模型，获得每个token的实体标签及K维概率向量。
  2. 对于每个被预测为实体（B或I类）的token，提取其PDM特征和统计特征。
  3. 将特征送入预训练的决策树NR模型，输出{Strong, Weak}。
  4. 预测为Weak的token被标记为假阳性，从最终输出中移除（或标记待审核）。

- **公式**：文中给出了概率密度图计算算法（Algorithm 1），以及SoftMax公式、温度缩放公式等作为背景。

## 3. 实验设计

- **数据集**：
  - **EMR**：2024年5万名肺癌和乳腺癌患者的真实临床数据，包含实体标注（True Positives由临床主题专家SME标注，False Positives为语义相似但上下文不符的实体）。实体类型包括Biomarker、Tumor type、Surgery、Medication、Tumor Grade、Histology。
  - **MIMIC-III**：公开的匿名化临床数据（4万名患者、200万份文档），用EMR训练的模型直接推理，少量抽样并由SME标注评估。

- **Benchmark方法**：
  - 基线：原始BERT NER模型（F1 ~0.9）。
  - SoftMax阈值法：直接截断概率。
  - 温度缩放（Temp. Scaling）：后处理校准概率。
  - MC Dropout：多次随机前向传播，用均值-方差截断。
  - 作者提出的NER+NR（决策树噪声移除模型）。

- **评估指标**：F1分数（EMR数据集），以及相对TP降低百分比和FP降低百分比（MIMIC-III，因为ground-truth不全）。

## 4. 资源与算力

- **文中未明确说明**：未提及使用的GPU型号、数量、训练时长等具体算力信息。仅提到模型轻量，且NR模型训练数据较少（从FP/TP样例中学习）。

## 5. 实验数量与充分性

- **实验数量**：在EMR上报告6种实体的F1对比表（Table 1），在MIMIC-III上报告4种实体的相对降低百分比（Table 2）。此外，给出了特征重要性示例和决策路径解释。
- **充分性与客观性**：实验覆盖了多个实体类型和两个不同分布的数据集（内部临床数据+公开数据），对比了三种主流后处理方法。消融方面未单独测试各特征组贡献，但通过决策路径说明了关键特征的使用。总体实验设计较充分，但缺少对特征敏感性和超参数（如桶数B、衰减率R）的消融研究。MIMIC-III上采用相对比较而非绝对F1，可能因标注不全，但仍能体现FP降低效果。

## 6. 主要结论与发现

- **结论**：提出的NR模型在EMR数据集上，5/6实体类型取得最佳F1；在MIMIC-III上，3/4实体类型实现了最大FP降低（47%~88%），同时TP降低控制在6%以内。NR模型能显著提升精确率，且对召回影响极小。
- **关键发现**：基于概率密度图和统计特征的后处理方法，能够有效区分真实实体和噪声，即使噪声被NER模型赋予了高SoftMax概率。决策树的可解释性允许专家审查决策理由，增加了实际部署的可信度。

## 7. 优点（方法或实验设计的亮点）

- **轻量高效**：无需修改NER模型或进行多次推理，仅对NER输出进行后处理，计算开销小。
- **可解释性强**：使用决策树，能提供明确的决策路径，便于临床专家理解和验证。
- **特征创新**：概率密度图（PDM）有效利用了Transformer的“语义牵引效应”，从邻域概率分布中提取区分信号，相比简单阈值法更鲁棒。
- **通用性**：在内部数据集和公共MIMIC-III上均有效，且对多种实体类型表现一致。
- **精度提升显著**：在保持高召回的同时，大幅削减假阳性（50%~90%），直接满足临床高精度需求。

## 8. 不足与局限

- **实验覆盖局限**：仅使用单一NER架构（BERT）和一种分类器（决策树），未探索其他模型（如LSTM-CRF）或更复杂分类器（如GBDT、MLP）的适用性。
- **特征敏感性未充分讨论**：概率密度图的桶数B、衰减率R是超参数，文中未做网格搜索或敏感性分析，可能影响泛化。
- **依赖标注质量**：训练NR模型需要手动标注TP/FP（SME参与），标注成本高，且可能存在主观偏差。
- **仅适用于特定标签体系**：文中以CoNLL格式（BIO）为例，但未讨论在不重叠实体或嵌套实体场景下的适配性。
- **术语“OOD”使用较宽松**：MIMIC-III被视为OOD，但其与EMR的分布差异程度未量化，可能影响结论普适性。
- **性能对比中缺失统计显著性检验**：表1和表2未给出误差范围或显著性差异，难以判断提升是否显著。
- **应用限制**：模型设计针对临床文本，对于其他领域的NER噪声问题，特征是否仍然有效有待验证。

（完）
