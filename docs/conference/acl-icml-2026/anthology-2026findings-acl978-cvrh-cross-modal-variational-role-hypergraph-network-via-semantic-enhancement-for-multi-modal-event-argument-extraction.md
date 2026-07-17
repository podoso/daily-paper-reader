---
title: "CVRH: Cross-modal Variational Role Hypergraph Network via Semantic Enhancement for Multi-modal Event Argument Extraction"
title_zh: CVRH：基于语义增强的跨模态变分角色超图网络用于多模态事件论元抽取
authors: "Bangze Pan, Yang Li, Ruili Pu, Suge Wang (王素格), Jian Liao (廖健), Jianxing Zheng, Xiaoli Li, Deyu Li (李德玉)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.978.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 使用角色超图的多模态事件论元抽取
tldr: 该论文针对多模态事件论元抽取任务，提出基于语义增强的跨模态变分角色超图网络CVRH，以事件角色信息为中心构建角色超图，有效整合多模态文档中的事件论元，显著提升了多模态场景下的论元抽取性能。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.978/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 675, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.978/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 1111, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.978/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.978/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 701, \"height\": 543, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.978/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.978/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1323, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.978/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 830, \"height\": 395, \"label\": \"Table\"}]"
motivation: 现有方法忽略事件角色信息对多模态事件论元抽取的影响。
method: 设计变分角色超图，通过语义增强构建角色超边来抽取多模态事件论元。
result: 在多模态事件论元抽取基准上取得最优结果。
conclusion: CVRH证明了事件角色信息在多模态事件抽取中的关键作用。
---

## Abstract
Multi-modal Event Argument Extraction task (MEAE) aims to extract all arguments related to a specific event from multiple modalities and identify their corresponding roles. Existing methods focus on weakly alignment of uni-modal representations and generatively data augmentation techniques. However, these methods ignore the potential impact of event role information on MEAE. To address this problem, we propose a Cross-modal Variational Role Hypergraph Network via Semantic Enhancement (CVRH). Unlike previous approaches, CVRH centers on event role information and designs a variational role hyperedge via semantic enhancement, which constructs a role hypergraph for event arguments within multi-modal documents. It explicitly modeling the high-order role correlations among cross-modal arguments in a document. Furthermore, CVRH introduces a modal shared encoder based on differential transformer, which effectively learns shared semantic representations across modalities and enhances the independence of argument representations. On the M2E2 benchmark, experimental results show that CVRH achieves a 6.9% improvement in F1-score on the MEAE compared to current state-of-the-art methods.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **任务背景**：多模态事件论元抽取（MEAE）旨在从文本、图像等多模态数据中提取与特定事件相关的所有论元并识别其角色。现有方法主要依赖单模态表示的弱对齐或基于生成的数据增强，忽略了事件角色信息在跨模态论元关联中的核心作用。
- **核心问题**：如何有效建模跨模态论元之间潜在的、高阶的角色语义关联，以解决论元混淆（例如图像中多个同类实体难以通过模态自身区分）的问题。
- **整体意义**：CVRH首次明确以事件角色为中心，通过变分角色超图显式建模跨模态论元的高阶角色相关性，突破了现有方法在角色语义建模上的空白。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：以事件角色作为超边，构建跨模态变分角色超图，利用LLM生成的语义先验与可学习的动态变分向量联合初始化超边，并通过多层超图注意力机制同步更新节点和超边表示，最终实现跨模态论元的角色关联建模。
- **关键技术**：
  - **差分Transformer模态共享编码器（DiffTrans）**：将差分注意力机制引入模态共享编码器，通过分离查询和键并计算差异注意力权重，增强语义相似论元（如不同模态的“人物”实体）表示间的独立性，缓解模型混淆。
  - **变分角色超边初始化**：针对每个角色，先利用LLM生成角色解释信息（RII，包含词义、使用场景、同义词），经人工审核后编码为静态语义先验；再引入服从标准正态分布的动态变分向量，二者拼接后通过高斯分布建模得到可学习的超边表示，平衡先验知识与动态适应性。
  - **超图构建与更新**：基于多模态注意力计算节点-超边关联强度，通过阈值β确定超图结构；之后利用多层超图注意力机制，先聚合节点信息更新超边，再聚集超边信息更新节点，并引入节点距离损失（Ld）促进同超边内节点表示紧凑。
  - **论元抽取**：将更新后的节点表示与角色查询计算匹配分数，通过阈值τ判定论元角色。
- **公式流程（文字说明）**：
  1. 文本/图像经单模态编码器得到表示，再经实体/目标检测提取候选论元表示。
  2. 候选论元经DiffTrans得到模态共享表示。
  3. 对每个角色ri，通过LLM获取RII文本并编码，与采样变分向量拼接后经高斯分布得到超边初始化He_i。
  4. 计算所有节点与超边的初始注意力权重，经β阈值化得到超图关联矩阵。
  5. 进行L层超图注意力更新：每层先更新超边（聚合其内节点信息），再更新节点（聚合其所属超边信息），更新中引入残差连接。
  6. 用sigmoid匹配分数进行论元分类，总损失为交叉熵损失+γ·节点距离损失。

## 3. 实验设计

- **数据集**：M2E2（多模态事件抽取基准），含8个事件类型、15个角色类型，共245篇多媒体文档（6167句子、1014图像、309个多模态事件）。训练时额外使用ACE05（纯文本事件）和SWiG（视觉事件）进行迁移学习。
- **基准方法**：对比8种SOTA方法：WASE（att/obj）、CLIP-EVENT、UNICL、CAMEL、MGIM、MMUTF、VEGSRF、MGFSG-EE，涵盖弱对齐、数据增强、模板填充、场景图增强等多种范式。
- **评估场景**：文本论元抽取（Textual）、视觉论元抽取（Visual）、多模态论元抽取（Multi），主要指标为P、R、F1。

## 4. 资源与算力

- 训练细节：使用单块A100 GPU，训练10个epoch，batch size 32，学习率1e-5，优化器为AdamW。
- 文中未明确说明GPU数量（推测为单卡）、训练总耗时（小时数）等，也未提及模型参数量级。资源描述相对有限。

## 5. 实验数量与充分性

- **实验组数**：约6组主要实验：
  - 主结果对比（8种方法 × 3模态 = 24个对比点）。
  - 消融实验（5个变体：w/o RII、w/o dv、w/o DiffTrans、w/o Ld，共4×3=12个结果）。
  - 参数敏感性分析（β和τ两个超参数，各在0.2~0.8范围内取7个值，分别在文本、多模态、视觉场景下测试，共约21×2=42个数据点）。
  - MLLM对比（Qwen2.5-VL-7B、LLaVA1.5-7B，3模态，共6个结果）。
  - 附录中可能还有更多细节。
- **充分性评估**：实验设计较为充分，消融覆盖核心组件（RII、变分向量、DiffTrans、距离损失），参数灵敏度分析全面，且与8种SOTA对比，并补充了与主流MLLM的对比，验证了方法相对于强基线的优势。实验公平性体现在统一实验设置、遵循已有文献的预处理和评估协议。但视觉模态性能仍显著低于文本模态，表明方法存在偏置。

## 6. 主要结论与发现

- CVRH在M2E2上取得全部三种模态的最佳F1：文本40.2%、视觉25.3%、多模态40.1%。相比最佳基线MMUTF（文本38.2%）和CAMEL（视觉24.4%）、最佳多模态基线CAMEL（33.2%），多模态F1提升6.9%。
- 消融实验证明每个组件均起正向作用：移除RII导致F1下降3~4分，移除变分向量下降约2.5分，移除DiffTrans或距离损失也均有下降。其中RII对文本模态影响最大，表明角色语义先验直接可迁移。
- 参数敏感性分析表明模型对β和τ具有一定鲁棒性，多模态性能比单模态更稳定。
- MLLM（Qwen2.5-VL-7B、LLaVA1.5-7B）在MEAE上性能优于部分基线但不及CVRH，且视觉论元性能远低于文本，进一步揭示视觉模态仍为瓶颈。

## 7. 优点

- **创新性**：首次将事件角色信息引入超图建模，设计变分超边同时融合LLM先验和可学习动态性，实现高阶角色关联的显式建模，突破了传统弱对齐的局限。
- **技术优势**：差分Transformer有效缓解了同类实体间表示混淆；变分超边设计使角色表示兼具语义丰富度和适应性；无需依赖图像-文本配对数据进行显式对齐。
- **实验严谨**：消融实验充分验证各组件贡献；参数敏感性分析全面；与多种范式（弱对齐、生成式、模板式）的SOTA以及MLLM对比，证明了方法的优越性和通用性。
- **性能提升显著**：在多模态场景下实现6.9%的F1绝对提升，验证了角色超图对跨模态推理的有效性。

## 8. 不足与局限

- **视觉模态性能较低**：角色超边主要基于文本信息，视觉论元需要跨模态映射，导致信息损失，视觉F1仅25.3%，远低于文本。该局限已明确承认，并指出未来需设计基于多模态信息的角色超边。
- **数据集规模与泛化性**：M2E2仅有245篇文档，且角色类型有限（15个），CVRH可能仅在高度判别性角色上表现良好，对易混淆角色效果不明。论文将其列为未来研究方向。
- **可解释性不足**：未探讨多模态论元抽取的可解释性（例如为何某个视觉实体被分配到某角色），虽然提及但未进一步研究。
- **计算资源细节缺失**：未报告总训练时间、模型参数规模、消融实验是否重复多次取均值等，降低了复现的完整度。
- **潜在偏差**：RII由LLM生成后人工审核，但仍可能引入生成偏差；变分向量的正态性先验假设是否最优未经深入比较。

（完）
