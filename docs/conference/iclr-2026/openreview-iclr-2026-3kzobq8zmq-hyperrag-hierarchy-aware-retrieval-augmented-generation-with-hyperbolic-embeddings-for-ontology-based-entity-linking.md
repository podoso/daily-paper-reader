---
title: "HyperRAG: Hierarchy-Aware Retrieval-Augmented Generation with Hyperbolic Embeddings for Ontology-Based Entity Linking"
title_zh: HyperRAG：基于双曲嵌入的层次感知检索增强生成用于本体实体链接
authors: "Thomas Labbé, Moussa BADDOUR, Axel Bonesteve, Paul ROLLIER, de Tayrac, Olivier Dameron"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=3kzoBq8ZmQ"
tags: ["query:ie"]
score: 8.0
evidence: 基于层次感知RAG和双曲嵌入的实体链接
tldr: 本文提出HyperRAG，结合大语言模型、检索增强生成和双曲嵌入用于本体实体链接。引入层次感知的评价框架，摆脱传统精确匹配的局限。在结构化知识提取任务中有效利用层级关系。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1445, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1439, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1309, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1161, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 727, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1446, \"height\": 783, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1160, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1162, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 849, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 597, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 878, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1148, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1006, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 856, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3kzobq8zmq/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1445, \"height\": 840, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-3kzobq8zmq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1453, \"height\": 533, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-3kzobq8zmq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1518, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-3kzobq8zmq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 615, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-3kzobq8zmq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 616, \"height\": 381, \"label\": \"Table\"}]"
motivation: 从非结构化文本中提取结构化知识时，目标概念常具有复杂层级关系，现有方法未充分利用。
method: 集成LLM、RAG和双曲嵌入进行层级感知的实体链接与检索。
result: 在本体实体链接任务上表现优越，层级感知评价更合理。
conclusion: HyperRAG为知识抽取中的层级结构利用提供了新思路。
---

## Abstract
Extracting structured knowledge from unstructured text is a fundamental challenge in machine learning, particularly when the target concepts are organized within complex hierarchical ontologies. We present HyperRAG, a novel framework that integrates Large Language Models (LLMs) with Retrieval-Augmented Generation (RAG) and hierarchical reranking using hyperbolic embeddings. Our approach is designed to improve entity linking and retrieval in settings where the label space exhibits rich hierarchical relationships. In addition, we introduce a hierarchy-aware evaluation framework that leverages ontology structure to provide a more nuanced assessment of model performance, moving beyond conventional exact-match metrics. Through comprehensive experiments on both benchmark and real-world datasets, including a newly curated and challenging set of clinical notes for phenotype extraction in precision medicine, we demonstrate that HyperRAG substantially improves ranking accuracy and recall, especially for implicit or nuanced entity mentions. While our primary application is in the biomedical domain, the proposed framework is broadly applicable and generalizable to hierarchical entity linking and retrieval tasks in other domains. All code, models, and datasets are released to support reproducibility.

---

## 论文详细总结（自动生成）

# 论文《HyperRAG: Hierarchy-Aware Retrieval-Augmented Generation with Hyperbolic Embeddings for Ontology-Based Entity Linking》详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：从非结构化文本中提取结构化知识时，目标概念通常组织在复杂的分层本体（如人类表型本体HPO）中。现有方法（如基于平面的稠密检索、精确匹配评估）无法有效利用层级关系，导致对隐含或细微提及的表型识别困难，且缺乏符合临床实践的评估体系。
- **研究动机**：双曲几何天然适合建模树状层级结构，但在此类任务中未被充分探索；RAG虽能缓解LLM幻觉并缩小候选空间，但未结合层级信息。
- **整体含义**：HyperRAG首次将双曲嵌入融入RAG管道，结合LLM跨度检测与层级感知重排序，显著提升本体实体链接的召回和排序质量，并引入层次化评估框架，使评价更贴近真实临床需求。该方法不限于生物医学，可推广至任何具有层级化本体的领域（如法律、电商）。

## 2. 方法论

### 核心思想
利用双曲空间（Poincaré球）训练层级嵌入，使本体中的父子关系、兄弟关系在嵌入空间中得到更忠实反映；再通过RAG检索候选，并结合语义（余弦相似度）与层级（归一化双曲距离）进行混合重排序。

### 关键技术细节
1. **跨度检测**：使用ChatGPT-3.5从临床报告中识别可能与表型相关的文本片段（包括隐式提及）。
2. **候选检索**：基于all-MiniLM-L12-v2作为基础模型，双曲模型在此基础上微调。欧氏模型使用FAISS检索Top-k（k=30）；双曲模型使用专用索引，计算归一化双曲距离。
3. **重排序策略**：
   - **晚交互重排序**：微调ColBERTv2，进行细粒度token级匹配。
   - **全双曲重排序**：将输入跨度与欧氏RAG候选嵌入双曲空间，按归一化双曲距离重排。
   - **混合重排序**：公式为 \( S_{hybrid}(C_i, span) = \gamma \cdot S_{cos} - (1-\gamma) \cdot \hat{d}_H \)，默认γ=0.5。
4. **层级感知评估**：定义直接关系（祖先/后代）和间接关系（堂亲）的加权分数，用于计算加权MRR、NDCG等；同时分析平均跳数、分支覆盖率、关系类型分布。

### 算法流程（文字说明）
1. 输入临床报告 → LLM提取表型文本跨度。
2. 将跨度嵌入欧氏/双曲空间 → RAG检索Top-30候选（基于HPO本体）。
3. 对候选进行重排序（晚交互/全双曲/混合）。
4. 使用标准精确匹配指标和层级感知加权指标进行评估。

## 3. 实验设计

### 数据集
- **ID-68**：公开基准数据集（Anazi et al., 2017），用于表型提取。
- **CHU-50**：内部数据集，50份合成临床笔记，共971个表型标注，约30%为隐式提及，更具挑战性。
- **训练数据**：HPO三元组（子-父关系+同义词增强）训练双曲模型；ChatGPT-4o-mini生成91,760条高质量跨度-标签对，用于训练ColBERTv2。

### 基准方法
- **PhenoBERT**：现有开源SOTA方法（Feng et al., 2023）。
- 对比方法：欧氏RAG、双曲RAG、HPO-ColBERT重排、双曲重排、混合重排。

### 评估指标
- 标准：Recall@k、Miss Rate@k、Precision@1、MRR、NDCG。
- 层级感知：加权Recall、加权MRR、加权NDCG、平均跳数、分支覆盖率、关系类型分布。

### 实验场景
- 主要实验：在ID-68和CHU-50上比较各模型。
- 消融实验：对混合重排的γ参数进行扫描（0.1～0.9）。
- 跨本体实验：使用SNOMED训练的模型在HPO数据集上评估。
- 内部验证：双曲模型的一跳/多跳距离分布、同义词与负例距离分析。

## 4. 资源与算力

- **训练配置**：所有模型训练在单个**NVIDIA RTX A3000 GPU**上进行，以控制预算和能耗。
- **双曲模型**：20个epoch，batch size 32，学习率1e-5，梯度累积8步。
- **ColBERTv2**：2个epoch，batch size 8，学习率1e-5，梯度累积2步。
- 文中未明确给出总训练时长。

## 5. 实验数量与充分性

### 实验数量
- 主干实验：2个数据集 × 5种模型 × 多个k值（1,3,5,10,15）。
- 消融实验：γ参数取5个值（0.1,0.3,0.5,0.7,0.9）在2个数据集上。
- 跨本体实验：1个附加模型（SNOMED）在2个数据集上。
- 内部一致性实验：一跳/多跳距离分布、同义词/负例距离（图3）。
- 数据质量评估：50句人工标注（Cohen's kappa=0.64）、1000句LLM-as-judge评估。

### 充分性与公平性
- **充分**：覆盖多种指标（精确匹配与层级感知），同时分析深层本体关系（跳数、分支、关系类型），消融覆盖关键参数。
- **公平**：与PhenoBERT对比时采用相同实验设置；跨本体实验测试泛化性；合成数据有严格过滤和人工验证。
- **潜在局限**：CHU-50为合成数据，可能存在分布偏差；仅与一个SOTA开源模型对比；未与其他RAG变体（如GraphRAG）比较。

## 6. 主要结论与发现

- **双曲嵌入有效捕获层级结构**：一跳/多跳距离分布更窄、均值更低，同义词更接近，负例仍保持分离（图3）。
- **混合重排在召回和排序上最优**：在ID-68上Recall@1达到0.857（加权Recall提升+9），CHU-50上Recall@1比PhenoBERT提升+23，Miss Rate降低18%。
- **层级感知指标更符合临床价值**：加权MRR和NDCG显示双曲模型在非精确匹配场景下表现更好，祖先/堂亲关系占比更高。
- **跨本体通用性**：SNOMED模型虽不如HPO专用模型，但混合策略仍带来增益，表明结构信息可补充语义。
- **隐式提及处理**：HyperRAG在CHU-50（含30%隐式提及）上显著优于PhenoBERT，证明LLM+层次重排对隐式表型的有效性。

## 7. 优点

- **方法创新**：首次系统地将双曲嵌入集成到RAG管道中，并设计混合重排策略整合语义与层级信号。
- **评估框架创新**：提出层次感知评价指标（加权分数、跳数、分支覆盖率、关系类型），更贴近临床实际，可推广至其他本体任务。
- **全面开源**：代码、模型、训练和评估数据集全部公开，有助于可复现性和后续研究。
- **实验设计严谨**：多维度评估（检索、排序、本体结构、跨本体）；数据质量经多轮人工和自动验证。
- **跨领域适用性**：不依赖特定领域特征，仅需层级本体和文本，可直接应用于法律、电商等领域。

## 8. 不足与局限

- **领域局限性**：主要实验在生物医学领域，虽然理论可推广，但缺乏非生物医学数据集验证（如产品分类、法律条款）。
- **计算效率未充分讨论**：双曲嵌入的检索和距离计算尚未与传统向量库（FAISS）高效结合，可能在大规模场景下成为瓶颈。
- **隐式提及依赖LLM质量**：跨度检测依赖ChatGPT-3.5，可能存在漏检或冗余；人工标注数据仅50句，样本量小。
- **合成数据偏差风险**：CHU-50为合成数据，虽经人工验证，但无法完全替代真实临床记录，可能高估模型在真实场景的表现。
- **未与最新生成式方法（如直接使用GPT-4）全面比较**：仅与PhenoBERT对比，未与直接提示GPT-4或微调LLM对比，基准不够全面。
- **双曲模型在精确匹配上略逊于欧氏模型**：在Top-1精确匹配率上双曲低于欧氏（0.814 vs 0.857），说明层级信息可能牺牲部分精确性。
- **混合策略的γ值未自动优化**：论文固定γ=0.5，虽然消融显示对性能不敏感，但可能存在更优设置。
- **对人类注工程度的依赖**：层次关系打分函数（α,β）依赖临床专家经验设定，可能影响可迁移性。

（完）
