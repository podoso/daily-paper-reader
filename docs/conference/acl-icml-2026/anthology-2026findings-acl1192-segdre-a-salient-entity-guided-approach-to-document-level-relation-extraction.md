---
title: "SegDRE: A Salient Entity Guided Approach to Document-Level Relation Extraction"
title_zh: SegDRE：一种基于显著实体引导的文档级关系抽取方法
authors: "Xing Yang, Chengxiang Tan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1192.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 基于显著实体引导的文档级关系抽取
tldr: 该论文针对文档级关系抽取中的类别不平衡和多跳推理难题，提出基于显著实体引导的SegDRE方法。通过将抽取空间分解为稠密和稀疏场景，限制稠密实体的搜索空间，并利用显著实体知识重构文档，有效提升了关系抽取的性能。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 812, \"height\": 446, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 1136, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 249, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1192/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 805, \"height\": 548, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 350, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1473, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1309, \"height\": 689, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 730, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1192/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 676, \"height\": 378, \"label\": \"Table\"}]"
motivation: 文档级关系抽取面临极端的类别不平衡和多跳推理复杂性。
method: 引入显著实体概念，将抽取空间解耦为稠密和稀疏场景。
result: 在多个文档级关系抽取基准上取得最优结果。
conclusion: 显式捕捉显著实体拓扑结构是解决文档级RE瓶颈的关键。
---

## Abstract
In Document-level Relation Extraction (DocRE), relational facts are typically organized around a few salient entities. Explicitly capturing this topological structure is pivotal to addressing the two critical bottlenecks of the task: the extreme class imbalance and the complexity of multi-hop reasoning. Based on this insight, we first introduce the concept of the salient entity and propose a novel approach that decouples the extraction space into dense and sparse scenarios. Specifically, our approach restricts the search space for dense pairs to mitigate the dominance of the negative samples, and innovatively injects the rich semantic knowledge of salient entities to explicitly reconstruct the document for bridging disjoint evidence in multi-hop reasoning. Extensive experiments demonstrate that our approach yields consistent improvements over various backbone models and achieves advanced performance compared to existing enhancement methods.

---

## 论文详细总结（自动生成）

### 论文中文详细总结

#### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：文档级关系抽取（DocRE）面临两大瓶颈：一是极端的正负类别不平衡（负样本占比超过94%-97%）；二是多跳推理的复杂性（实体对信息分散在不同句子中，需要跨句推理）。
- **整体含义**：论文观察到文档中的关系事实通常围绕少数“显著实体”（salient entities）组织，其定义为参与最多关系的实体。基于这一洞察，作者提出通过显式捕捉文档的显著实体拓扑结构，将抽取空间解耦为稠密（涉及显著实体）和稀疏（不涉及显著实体）场景，以同时缓解类别不平衡和改进多跳推理。

#### 2. 方法论
- **核心思想**：识别文档中的显著实体（salient entity），将关系抽取任务解耦为两个互补阶段：稠密关系抽取（仅处理与显著实体相关的实体对）和稀疏关系抽取（处理其余实体对）。通过将稠密阶段提取的关系三元组注入原始文档，显式重构上下文，辅助稀疏阶段的多跳推理。
- **关键技术细节**：
  - **显著实体识别**：使用零膨胀泊松（ZIP）回归模型替代标准分类头，预测每对实体的关系计数，并聚合到实体级别，选出计数最高的实体作为显著实体。
  - **稠密关系抽取**：仅对涉及显著实体的2*(|E|-1)个候选对进行抽取，显著减少负样本数量（约一半正关系被覆盖）。
  - **稀疏关系抽取**：利用K-Bert的知识注入机制，将稠密阶段预测的高置信度三元组（如(显著实体, 关系, 尾实体)）作为额外分支插入原文档的句子树中，通过软位置索引和可见矩阵保持语义正确性，然后对稀疏实体对进行抽取。
  - **推理阶段融合**：扩展ISE融合策略，对基础模型、稠密模型、稀疏模型的预测分数进行网格搜索优化阈值，获得最终预测。
- **公式/算法流程**（文字说明）：
  1. 训练一个计数回归头（ZIP模型），输出每对实体的预期关系数c(s,o)，聚合后选出显著实体esal。
  2. 使用原编码器对涉及esal的所有实体对进行关系分类（密集阶段），得到三元组Tdense。
  3. 将Tdense按比例α注入原文档（K-Bert），形成重构文档Dtrans。
  4. 在Dtrans上对剩余实体对（不涉及esal）进行关系分类（稀疏阶段），得到Tsparse。
  5. 融合基础模型、稠密模型、稀疏模型的预测分数（网格搜索阈值），输出最终结果。

#### 3. 实验设计
- **数据集**：DocRED（原始版）和Re-DocRED（纠正版），两个标准的文档级关系抽取基准。
- **Benchmark**：使用F1、Ign-F1、Intra-F1、Inter-F1作为评价指标。
- **对比方法**：
  - 基础模型：ATLOP、DREEAM（使用BERT base和RoBERTa large）。
  - 增强方法：HingeABL、PEMSCL、P³M、APRDL、AMTL、JMRL等（损失优化或插件式方法）。
  - 消融实验：移除显著实体识别、移除稠密/稀疏阶段、移除知识注入、移除阈值网格搜索、朴素集成等。
  - 对比显著实体选择策略：Max Mention、Edit Distance、Aggregation、线性回归、ZIP回归。

#### 4. 资源与算力
- 文中明确提到：使用PyTorch和HuggingFace Transformers；BERT base实验在单张NVIDIA 5060Ti 16GB GPU上运行；RoBERTa large实验在单张NVIDIA 4090 24GB GPU上运行。
- 未明确说明具体训练时长或总GPU小时数，但声称超参数与原始基线一致。

#### 5. 实验数量与充分性
- **实验数量**：主结果（表2、3）在DocRED和Re-DocRED上测试了多种基础模型与增强方法的组合（共约12组主要结果）；消融实验（表4）覆盖7种变体；显著实体选择对比（表5）5种策略；知识注入比例α分析（图4、附录A.2）；阈值偏移分析（图5）；案例研究（附录A.3）。
- **充分性**：实验设计较为充分，涵盖了不同编码器、数据集、消融组件、超参数敏感性、选择策略对比，并提供了5次运行的平均值和标准差（表2、3的SegDRE列），显示结果稳定。但稀疏阶段的实验仅用一个数据集消融（表7），未跨数据集验证鲁棒性。

#### 6. 主要结论与发现
- SegDRE在DocRED和Re-DocRED上均一致提升ATLOP和DREEAM的F1和Ign-F1，尤其是Inter-F1（多句推理）提升显著（如RoBERTa large上Inter-F1提升1.0-1.0）。
- 在Re-DocRED上，ATLOP-SegDRE超越之前最优的ATLOP-P³M和ATLOP-AMTL（Test F1 80.25 vs 80.02/79.97）；DREEAM-SegDRE w. ISF达到81.32 F1，略超SOTA方法APRDL。
- ZIP回归的显著实体识别准确性最高（74.35%），且下游性能最优；错误识别会导致稀疏阶段性能大幅下降（F1从40.79跌至约24），验证了显著实体知识的桥梁作用。
- 知识注入比例α设为100%最佳；注入稠密预测与注入真实标签的性能差距很小，表明方法鲁棒。
- 网格搜索阈值时，稠密部分阈值倾向降低，基础/稀疏部分倾向升高，反映融合策略对稠密关系的高置信度依赖。

#### 7. 优点
- **创新性**：首次将显著实体作为显式信号用于任务解耦，思路新颖且符合人类认知策略（先抓核心，再处理边缘）。
- **模型无关性**：可以作为插件集成到各种DocRE基础模型（ATLOP、DREEAM）中，提升通用性。
- **有效缓解负面问题**：通过将搜索空间从O(n²)降至线性O(n)，显著减少了负样本干扰。
- **增强多跳推理**：通过知识注入重构文档，将隐式推理变为显式上下文，降低推理难度。
- **实验充分且公平**：在多个主流数据集上对比了多种SOTA增强方法，报告了均值和标准差，消融实验完整。

#### 8. 不足与局限
- **单显著实体假设**：方法假设每篇文档只有一个显著实体，然而实际文档可能存在多个实体簇，该假设在更复杂场景下可能失效。作者在局限性部分也承认这一点。
- **统一超参数设计**：为公平比较，所有阶段使用相同超参数和架构，但若针对稠密/稀疏阶段分别优化，性能可能进一步提升。
- **计算资源消耗**：需要额外训练计数回归头和两阶段推理，推理时需加载两个编码器（重构文档也需要单独编码），计算开销比基础模型大，但文中未量化效率。
- **对显著实体识别质量的依赖**：如果识别错误，会极大损害稀疏阶段性能（表5显示），在实际应用中可能存在风险。
- **数据偏差风险**：实验仅在DocRED/Re-DocRED上验证，未在其他领域（如生物医学、法律）的DocRE数据集上测试，泛化性有待检验。

（完）
