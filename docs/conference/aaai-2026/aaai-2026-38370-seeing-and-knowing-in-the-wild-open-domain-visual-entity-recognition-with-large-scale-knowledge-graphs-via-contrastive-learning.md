---
title: "Seeing and Knowing in the Wild: Open-domain Visual Entity Recognition with Large-scale Knowledge Graphs via Contrastive Learning"
title_zh: 在开放域中看到并认知：基于知识图谱和大规模对比学习的视觉实体识别
authors: "Hongkuan Zhou, Lavdim Halilaj, Sebastian Monka, Stefan Schmid, Yuqicheng Zhu, Jingcheng Wu, Nadeem Nazer, Steffen Staab"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38370/42332"
tags: ["query:ie"]
score: 6.0
evidence: 开放域视觉实体识别，链接到知识图谱
tldr: 开放域视觉实体识别面临未见实体和长尾分布挑战。本文提出知识引导对比学习框架KnowCoL，将图像和文本描述联合映射到由Wikidata构建的共享语义空间。实验证明该方法在零样本和长尾场景下显著优于现有方法，实现鲁棒的视觉实体识别。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38370/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1822, \"height\": 677, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38370/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1722, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38370/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 857, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38370/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1820, \"height\": 377, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38370/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 857, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38370/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1834, \"height\": 613, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38370/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 857, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38370/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38370/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 840, \"height\": 263, \"label\": \"Table\"}]"
motivation: 开放域视觉实体识别中训练实体未见且长尾分布，现有方法泛化差。
method: 提出知识引导对比学习框架，结合图像、文本和结构化知识进行语义对齐。
result: 在多个开放域数据集上取得最先进结果，尤其擅长长尾实体识别。
conclusion: 融合知识图谱的对比学习有效提升视觉实体识别的开放域泛化能力。
---

## Abstract
Open-domain visual entity recognition aims to identify and link entities depicted in images to a vast and evolving set of real-world concepts, such as those found in Wikidata. Unlike conventional classification tasks with fixed label sets, it operates under open-set conditions, where most target entities are unseen during training and exhibit long-tail distributions. This makes the task inherently challenging due to limited supervision, high visual ambiguity, and the need for semantic disambiguation. We propose a Knowledge-guided Contrastive Learning (KnowCoL) framework that combines both images and text descriptions into a shared semantic space grounded by structured information from Wikidata. By abstracting visual and textual inputs to a conceptual level, the model leverages entity descriptions, type hierarchies, and relational context to support zero-shot entity recognition.
We evaluate our approach on the OVEN benchmark, a large-scale open-domain visual recognition dataset with Wikidata IDs as the label space. Our experiments show that using visual, textual, and structured knowledge greatly improves accuracy, especially for rare and unseen entities. Our smallest model improves the accuracy on unseen entities by 10.5% compared to the state-of-the-art, despite being 35 times smaller.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：传统视觉分类任务依赖固定类别集，但现实世界中的实体（如地标、艺术品、生物物种、公众人物）数量庞大且持续增长，出现长尾分布。开放域视觉实体识别任务要求将图像链接到大规模知识库（如Wikidata）中的具体实体，面临有限监督、视觉歧义和语义消歧等挑战。
- **整体含义**：现有方法（如CLIP双编码器、两阶段生成式方法）因仅匹配视觉特征与实体名称，忽略了实体间的结构化关系（如类型层次、关联关系），导致零样本泛化能力差、语义模糊（例如“Mercury”可指行星或化学元素）。本文提出利用大规模知识图谱（Wikidata）的结构化知识，通过对比学习将图像、文本与知识图谱嵌入对齐到共享语义空间，从而提升零样本识别能力。

## 2. 论文提出的方法论

- **核心思想**：Knowledge-guided Contrastive Learning (KnowCoL) 框架，将输入图像+文本查询与目标实体的多模态信息（文本描述、示例图像、知识图谱结构）投影到同一语义空间，通过三种损失函数联合优化，使模型在概念层面理解实体而非简单匹配标签。
- **关键技术细节**：
  - **嵌入模块**：使用冻结的CLIP图像编码器+可训练线性投影层得到图像嵌入（\(f_\theta\)）；冻结的CLIP文本编码器+可训练线性投影层得到文本嵌入（\(f_\lambda\)）。知识图谱嵌入（KGE）采用TransE（余弦相似度）将实体节点映射到相同维度空间（\(\phi(e)\)）。
  - **融合模块**：对输入图像和文本查询，通过加法融合得到 \(z_{\text{input}} = f_\gamma(f_\theta(x_p), f_\lambda(x_t))\)。实体多模态表示：文本嵌入 \(z_{\text{entityText}} = f_\lambda(t_e)\)，图像嵌入 \(z_{\text{entityImage}}\) 为其示例图像的平均嵌入（若无示例则用文本嵌入代替）。
  - **损失函数**（公式见论文方程(6)、(7)、(9)）：
    - **对齐损失** \(L_a\)：对称对比损失，拉近输入嵌入 \(z_{\text{input}}\) 与对应实体节点嵌入 \(\phi(e)\)。
    - **代理损失** \(L_p\)：对称对比损失，分别对齐节点嵌入与实体文本嵌入、实体图像嵌入，使节点成为多模态语义的“代理”。
    - **知识图谱嵌入损失** \(L_{\text{KE}}\)：对每个实体关联的三元组（头实体-关系-尾实体）使用负采样对比损失，学习结构化关系。
  - **总损失** \(L = L_a + \beta_1 L_p + \beta_2 L_{\text{KE}}\)，其中 \(\beta_1=\beta_2=1\)（默认）。
  - **推理**：计算输入嵌入与每个候选实体多模态表示（文本与图像嵌入的均值）的余弦相似度，取最大值对应实体。
- **算法流程**：训练时，批次输入图像-文本对及对应实体ID；提取输入嵌入与实体多模态嵌入；计算三种损失并反向传播。测试时，对每个输入计算与所有候选实体（或预检索子集）的相似度，输出最高分实体。

## 3. 实验设计

- **数据集与Benchmark**：OVEN（Open-domain Visual Entity Recognition）数据集，包含约606万训练样本，融合14个图像识别数据集。测试集包含15,888个实体（8,355个已见，7,533个未见）。标签空间为Wikidata QID。评估指标为已见/未现实体Top-1准确率的调和均值（HM）。
- **对比方法**：
  - **双编码器基线**：CLIP、CLIPFusion、CLIP2CLIP。
  - **两阶段生成式基线**：BLIP-v2、PaLI-3B/17B、GIT-Large、GER-ALD、Auto-VER-7B/14B。
- **训练细节**：从Wikidata提取子图含32,122实体、501种关系。采用AdamW优化器（lr=0.001, batch size=4096, weight decay=0.0001），温度 \(\tau=0.07\)。使用OpenCLIP不同规模骨干网络（ViT-L/14, ViT-H/14, ViT-bigG/14）。

## 4. 资源与算力

- 论文明确提到：“作者感谢HoreKa高性能计算机提供的计算时间”，但未给出具体GPU型号、数量或训练时长。仅提到模型参数量（最大2.0B），训练数据规模（600万样本），及使用了NHR@KIT的高性能计算资源。具体算力细节未公开。

## 5. 实验数量与充分性

- **实验数量**：论文进行了多组实验，包括：
  - 与8种主流方法在主指标上的对比（表1）。
  - 模型规模消融（3种骨干网络，表2）。
  - 知识类型消融（有无示例图像、有无层次结构知识，表3）。
  - 融合函数比较（加法、MLP、Transformer Encoder等，表4）。
  - KGE方法比较（TransE、TransH、DistMult，表5）。
  - 超参数敏感性分析（\(\beta_1, \beta_2\)、潜在空间维度 \(d_e\)、温度 \(\tau\)，图4）。
- **充分性评价**：实验覆盖了关键消融，对比基线全面（包括当时SOTA），且对每个设计选择进行了量化分析。所有实验均基于统一OVEN测试集，指标一致。消融实验控制变量合理，结果客观。不足：未包含对更大KG子图或不同关系类型的完整探索；未对推理速度或内存占用进行比较。

## 6. 论文的主要结论与发现

- KnowCoL显著优于所有双编码器基线和多数生成式方法，特别是对于未见实体。最小模型（KnowCoL-L，0.4B参数）在未见实体上达到29.1%准确率，比之前最佳双编码器CLIP2CLIP（10.5%）提升10.5个百分点（相对提升约2.8倍），且参数少35倍。
- 多模态知识（结构化KG+文本描述+示例图像）均至关重要：去除示例图像导致HM下降1.5%；去除KG层次知识（Instance-of、subclass-of等）导致HM下降3.2%，对未见实体影响更大。
- 简单加法融合在平衡已见/未实现上优于更复杂的融合方法（MLP或Transformer），后者容易对已见过拟合。
- TransE（余弦相似度）作为KGE方法效果最佳；较高的代理损失权重（\(\beta_1\)）和KE损失权重（\(\beta_2\)）均有利于性能提升；较大模型需要更高维潜在空间。

## 7. 优点

- **创新性**：首次将大规模知识图谱（Wikidata）的结构化知识显式融入开放域视觉实体识别，利用对比学习对齐多模态与结构化空间，有效缓解语义歧义。
- **零样本泛化能力强**：在未见实体上大幅超越现有方法，且模型更小，展示了知识增强的泛化潜力。
- **实验系统全面**：消融实验覆盖知识类型、融合策略、KGE方法、超参数等，结论可靠。
- **开源代码**：提供GitHub仓库（https://github.com/boschresearch/KnowCoL），促进可重复性研究。
- **效率优势**：双编码器范式推理速度快，无需生成式模型的文本生成步骤，且参数量更小。

## 8. 不足与局限

- **知识图谱子图规模有限**：实验仅使用32,122实体（占Wikidata约0.03%），大规模全景下的表现未知。
- **融合策略简单**：加法融合虽然平衡性好，但可能无法充分捕获跨模态交互；更复杂的融合（如交叉注意力）在已见实体上更好但牺牲泛化，需要更好权衡。
- **缺少推理效率分析**：未报告推理时间或内存占用，对实际部署参考不足。
- **数据集覆盖偏置**：OVEN虽包含14个数据集，但主要覆盖常见物体/场景，对罕见专业领域（如医学、工程）的实体识别能力未验证。
- **未讨论误差分析**：对错误案例（如相似实体混淆）缺乏定性分析，难以洞察模型盲点。
- **训练资源未量化**：未提供GPU型号、数量、训练时长，难以评估可复现性成本。

（完）
