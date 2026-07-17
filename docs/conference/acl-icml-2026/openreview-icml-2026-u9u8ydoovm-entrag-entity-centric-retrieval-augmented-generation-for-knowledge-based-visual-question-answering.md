---
title: "EntRAG: Entity-Centric Retrieval-Augmented Generation for Knowledge-based Visual Question Answering"
title_zh: EntRAG：面向知识型视觉问答的以实体为中心的检索增强生成
authors: "Yiheng Hu, Xiaoyang Wang, Qing Liu, Xiwei Xu, Qian Fu, Wenjie Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/2eb9a2b523840cf5ba8ce9e8aca27f7f53a763f1.pdf"
tags: ["query:multimodal"]
score: 6.0
evidence: 以实体为中心的多模态检索用于视觉问答
tldr: 知识型视觉问答中现有方法对视觉歧义敏感且孤立处理多模态信号。本文提出EntRAG，一个以实体为中心的检索增强生成框架，通过EntBind对齐查询与多模态实体嵌入，并引入重排序机制。在KB-VQA基准上，EntRAG在细粒度实体识别和回答准确率上取得提升。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有KB-VQA方法依赖以图像为中心的检索，对视觉歧义敏感。
method: 提出以实体为中心的多模态检索增强框架，包括多模态实体对齐绑定和重排序。
result: 在KB-VQA任务上实现更准确的实体定位和答案生成。
conclusion: 实体级多模态对齐可有效提升知识型视觉问答的鲁棒性。
---

## Abstract
Knowledge-based Visual Question Answering (KB-VQA) remains a challenging task, particularly when queries require precise identification and grounding of fine-grained entities within large-scale knowledge base. Existing methods often treat visual and textual signals in isolation and rely heavily on image-centric retrieval, which makes them sensitive to visual ambiguities. To address these limitations, we propose EntRAG, an entity-centric retrieval-augmented generation framework. Our approach first introduces EntBind to align query representations with multimodal entity embeddings by explicitly binding entity tokens to latent visual features, retrieving a set of relevant candidate entities. A reranking mechanism is applied to these candidate entities to select the most informative context by combining entity-level alignment with overall contextual relevance. The selected evidence is incorporated into context-aware generation module to produce final answer. By explicitly operating at the entity level, EntRAG achieves more consistent and reliable results.
Extensive experiments demonstrate that EntRAG consistently outperforms prior methods, achieving scores of 46.1 on E-VQA and 44.5 on InfoSeek.

---

## 论文详细总结（自动生成）

### 论文详细中文总结

#### 1. 核心问题与整体含义（研究动机和背景）
- **研究问题**：知识型视觉问答（KB-VQA）任务要求模型在大型知识库中准确识别并定位细粒度实体，以回答复杂的视觉问题。现有方法普遍存在两个缺陷：
  - **隔离处理多模态信号**：将视觉和文本信息独立建模，缺乏有效的跨模态对齐。
  - **以图像为中心的检索**：过度依赖图像整体特征进行检索，对视觉歧义（如目标遮挡、光照变化、视角差异）非常敏感，导致错误实体检索和答案生成。
- **研究动机**：为了克服上述局限，作者提出一个以实体为中心的检索增强生成框架 **EntRAG**，通过显式绑定实体标记与潜在视觉特征，实现更鲁棒、更精确的知识问答。

#### 2. 方法论：核心思想、关键技术细节
- **核心思想**：将KB-VQA从“以图像为中心”的检索范式转向“以实体为中心”的检索范式，通过显式对齐查询与多模态实体嵌入，并引入重排序机制精选上下文，最后生成答案。
- **关键技术细节**：
  - **EntBind 对齐模块**：将问题查询表示与多模态实体嵌入对齐，具体通过将实体标记（entity tokens）显式绑定到潜在视觉特征，从而在共享嵌入空间中检索出相关候选实体。
  - **重排序机制**：对候选实体进行再排序，结合**实体级对齐**和**整体上下文相关性**两个维度，选出最富信息量的上下文证据。
  - **上下文感知生成模块**：将精选的实体证据融入问题上下文，输入生成模型（如大语言模型）产生最终答案。
- **算法流程**（文字说明）：
  1. 输入：图像和问题文本。
  2. 多模态编码：提取图像视觉特征和问题文本特征。
  3. EntBind：将实体标记与视觉特征绑定，构建多模态实体嵌入库，计算查询与每个实体的相似度，检索Top-K候选实体。
  4. 重排序：基于实体级和上下文级评分对候选实体重新排序，选择Top-M作为最终证据。
  5. 生成：将证据与问题拼接，输入生成模型（如T5或LLM），输出答案。

#### 3. 实验设计
- **数据集**：E-VQA 和 InfoSeek 两个KB-VQA基准数据集。
- **基准（Benchmark）**：KB-VQA任务，评估指标为准确率（得分）。
- **对比方法**：与“prior methods”进行对比，但未在摘要中列出具体方法名称。元数据中提及“在KB-VQA基准上，EntRAG在细粒度实体识别和回答准确率上取得提升”。

#### 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及GPU型号、数量、训练时长等算力信息。需要阅读完整论文才能获取。

#### 5. 实验数量与充分性
- **实验数量**：摘要中仅报告了两个数据集（E-VQA和InfoSeek）上的最终分数（46.1和44.5），未提及消融实验、超参数分析、跨场景泛化等。元数据提到“EntRAG在KB-VQA基准上取得提升”，但缺乏实验细节。
- **充分性评价**：基于现有信息，实验数量较少，未展示消融研究、对比多基线、或在不同难度/实体类型上的细分结果。不足以全面证明方法的优越性和鲁棒性。客观性方面，只提供了最终分数，未报告方差或统计显著性检验。需依赖完整论文评估。

#### 6. 主要结论与发现
- **核心结论**：以实体为中心的多模态对齐（通过EntBind和重排序）可显著提升KB-VQA的鲁棒性和准确性，尤其在细粒度实体识别和答案生成上优于先前方法。
- **定量结果**：在E-VQA上得分46.1，在InfoSeek上得分44.5，均“consistently outperforms prior methods”。

#### 7. 优点
- **方法创新性**：首次提出“以实体为中心”的检索增强范式，显式将实体标记与视觉特征绑定，克服了传统图像级检索的歧义问题。
- **跨模态对齐策略**：EntBind设计精巧，能有效融合多模态信息到统一实体空间，并利用重排序进一步提升证据质量。
- **框架通用性**：可灵活集成到现有生成模型（如LLM）中，适用于知识型视觉问答。

#### 8. 不足与局限（基于现有信息推断）
- **实验覆盖不充分**：当前只报告了两个数据集上的最终结果，缺少消融实验（如EntBind vs. 无绑定的对比、重排序贡献分析）和跨数据集泛化测试（如VQA v2.0、OK-VQA等）。
- **偏差风险**：未讨论数据集本身的实体分布偏差、长尾实体表现、以及视觉歧义程度对方法的影响。也未分析失败案例。
- **应用限制**：方法依赖于预先构建的多模态实体嵌入库，对于新兴实体或动态知识库需要重新编码，部署成本较高。未明确说明推理效率（如检索延迟）。
- **算力与可复现性**：未提供训练资源、超参数设置、代码开源计划，影响可复现性。
- **语言限制**：仅提供英文摘要，中文元数据为推测，实际论文应以英文为准。

（完）
