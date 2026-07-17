---
title: "HCRE: LLM-based Hierarchical Classification for Cross-Document Relation Extraction with a Prediction-then-Verification Strategy"
title_zh: HCRE：基于LLM的跨文档关系抽取层次分类与预测-验证策略
authors: "Guoqi Ma, Liang Zhang, Hongyao Tu, Hao Fu, Hui Li, Yujie Lin, Longyue Wang, Weihua Luo, Jinsong Su"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1985.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 基于大语言模型的跨文档关系抽取
tldr: 该论文提出HCRE框架，利用大语言模型进行跨文档关系抽取，采用层次分类和预测-验证策略。实验表明，尽管LLM参数庞大，但在跨文档关系抽取任务上并不总是优于小型语言模型。论文分析了性能不足的原因，为后续研究提供了重要参考。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 707, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1642, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 793, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1649, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 755, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1502, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 811, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1985/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 791, \"height\": 558, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1651, \"height\": 1229, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1382, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 545, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 522, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 567, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 813, \"height\": 573, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1653, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1657, \"height\": 717, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 778, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 807, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1620, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1985/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1662, \"height\": 1545, \"label\": \"Table\"}]"
motivation: 现有跨文档关系抽取方法依赖小型语言模型，语言理解能力有限。
method: 提出基于LLM的层次分类方法，结合预测-验证策略进行跨文档关系抽取。
result: LLM在跨文档关系抽取上并不总是超越小型语言模型。
conclusion: 为LLM在关系抽取中的应用提供了深入分析和未来方向。
---

## Abstract
Cross-document relation extraction (RE) aims to identify relations between the head and tail entities located in different documents. Existing approaches typically adopt the paradigm of “ Small Language Model (SLM) + Classifier ”. However, the limited language understanding ability of SLMs hinders further improvement of their performance. In this paper, we conduct a preliminary study to explore the performance of Large Language Models (LLMs) in cross-document RE. Despite their extensive parameters, our findings indicate that LLMs do not consistently surpass existing SLMs. Further analysis suggests that the underperformance is largely attributed to the challenges posed by the numerous predefined relations. To overcome this issue, we propose an LLM-based Hierarchical Classification model for cross-document RE (HCRE), which consists of two core components: 1) an LLM for relation prediction and 2) a hierarchical relation tree derived from the predefined relation set. This tree enables the LLM to perform hierarchical classification, where the target relation is inferred level by level. Since the number of child nodes is much smaller than the size of entire predefined relation set, the hierarchical relation tree significantly reduces the number of relation options that LLM needs to consider during inference. However, hierarchical classification introduces the risk of error propagation across levels. To mitigate this, we propose a prediction-then-verification inference strategy that improves prediction reliability through multi-view verification at each level. Extensive experiments show that HCRE outperforms existing baselines, validating its effectiveness.

---

## 论文详细总结（自动生成）

# 论文总结：HCRE: LLM-based Hierarchical Classification for Cross-Document Relation Extraction

## 1. 核心问题与整体含义（研究动机和背景）

- **任务定义**：跨文档关系抽取（Cross-document RE）旨在识别位于不同文档中的头实体和尾实体之间的关系。
- **现有方法局限**：现有方法普遍采用“小型语言模型（SLM）+分类器”的范式，但SLM的语言理解能力有限，限制了性能提升。
- **LLM探索发现**：论文通过初步研究发现，直接使用大语言模型（LLM）进行跨文档RE效果并不总是优于SLM，甚至有时更差。分析表明，主要瓶颈在于预定义的关系数量过多（CodRED数据集包含277个关系），导致LLM难以区分语义相似的关系，且过长的提示会分散注意力。
- **论文目标**：提出一种基于LLM的层次分类模型（HCRE），通过减少每层需要考虑的关系选项来提升LLM在跨文档RE上的性能，并解决层次分类中的错误传播问题。

## 2. 方法论：核心思想、关键技术细节

### 2.1 层次关系树构建
- 使用高级LLM（如GPT-4o）基于预定义关系的语义，递归地逐层划分关系节点，生成一棵层次关系树。
- 根节点包含所有关系；中间节点代表高层次概念；叶节点对应预定义关系。
- 第二层强制分为两个节点：“有效关系”（所有正例关系）和“无有效关系”（仅NA），以缓解类别不平衡。
- 每个层次生成一个文本划分标准（如“领域”、“实体类型”），确保同层节点间区分度高。

### 2.2 层次分类过程
- 对于每个实例（上下文、头实体、尾实体），LLM从根节点开始，逐层向下选择子节点，最终到达叶节点（即目标关系）。
- 每层 LLM 只需从少数子节点（平均5.5个）中选择，而非全部277个关系。

### 2.3 预测-验证（Prediction-then-Verification）推理策略
- **预测步骤**：在当前层，LLM从候选子节点中选出最优节点（ˆr1st）和次优节点（ˆr2nd）。
- **验证步骤**：构建三个验证选项集：
  1. 将ˆr1st替换为其子节点；
  2. 将ˆr2nd替换为其子节点；
  3. 同时替换两者。
- LLM分别从这三个验证集预测最佳节点。若多数验证集的预测结果与ˆr1st语义对齐（即等于ˆr1st或其子节点），则确认ˆr1st为当前层可靠预测；否则移除ˆr1st并重复上述步骤。
- 该策略通过多视角（finer-grained）验证减少了层级间的错误传播。

### 2.4 模型训练
- 对每个训练样本，沿层次树生成逐层的训练样本（共L-1个），形成数据集D1。
- 为模拟验证步骤，额外构建数据集D2：基于D1中的每个样本，用最优和次优节点（次优节点随机采样）替换为其子节点，生成三个验证训练样本。
- 最终联合D1∪D2对LLM进行LoRA微调。

## 3. 实验设计

- **数据集**：主实验使用CodRED（闭设置和开设置），包含8,263条正例路径、120,925条NA路径；另在DocRED上评估跨数据集泛化。
- **基准模型**：
  - 跨文档RE基线：End-to-End, ECRIM, MR.COD, KXDocRE, REIC, NEPD（基于BERT-base和RoBERTa-large）。
  - LLM层次文本分类基线：Rs-ICL, DFS-L., BFS-L.。
  - 直接微调LLM的Vanilla基线。
- **评估指标**：采用micro F1和binary F1（论文通过初步实验论证了最大F1和P@K存在可靠性问题，micro F1和binary F1更稳定）。
- **实验设置**：LLM骨干为LLaMA-3.1-8B-Instruct（主实验），树构建使用GPT-4o。

## 4. 资源与算力

- **GPU**：4张NVIDIA A100 80G GPU。
- **训练参数**：训练6,400步，采用LoRA（r=64, α=128），学习率5e-5，batch size 32。
- **树构建成本**：使用GPT-4o一次构建，API总成本约0.9641美元（输入334,793 tokens，输出12,713 tokens），开销极低。
- **推理效率**：虽然HCRE的LLM调用次数多于Vanilla（152,663 vs 40,740），但由于输入token平均减少61.6%（从1,499.76降至575.75），每实例延迟仅从0.21s增至0.29s，可接受。

## 5. 实验数量与充分性

论文进行了多组实验，覆盖不同角度：

- **主实验结果**：表3展示了闭设置和开设置下HCRE与所有基线的对比，HCRE在micro F1和binary F1上全面领先（闭设置micro F1 45.35 vs 次优NEPD 42.96；开设置micro F1 34.91 vs 30.12），统计显著性检验p<0.01。
- **消融实验**：表4包含5种变体（w/o multi-view, w/o PtV, w/o LTC, w/o LTC+PtV, w/o HRT），验证了各组件有效性。
- **错误传播分析**：图6展示PtV策略在各层级上提升准确率并降低错误传播比例。
- **树深度影响**：图7测试L=4,5,6，发现模型对深度不敏感（L=5最优）。
- **不同骨干**：表13使用Qwen2.5-0.5B/7B、Gemma2-9B，HCRE均带来增益。
- **跨数据集泛化**：表14在DocRED上HCRE优于AutoRE、EP-RSR等LLM基线。
- **Bag-level评估**：表11聚合路径预测，HCRE仍大幅领先。
- **常规指标**：表12在最大F1、AUC、P@K上HCRE也取得最优。
- **附录**：额外分析了树构造鲁棒性、误差类型、计算效率等。

实验设计充分、对比公平、消融清晰，多场景验证了方法的泛化性和有效性。

## 6. 主要结论与发现

- LLM在跨文档RE上性能受限的主要原因是**过多预定义关系**，减少关系选项可显著提升LLM性能。
- HCRE通过**层次关系树**将每层选项降至平均5.5个，有效解决了LLM的瓶颈。
- **预测-验证策略**通过多视角验证显著减少层级间错误传播，提升了预测可靠性。
- HCRE在CodRED闭/开设置下均超越所有SLM和LLM基线，并在DocRED上展现出良好的跨数据集泛化能力。
- 层次树构建成本低、模型对树深度不敏感、适用于不同LLM骨干，具有实用价值。

## 7. 优点

1. **创新性**：首次将层次分类引入LLM的跨文档RE，巧妙利用关系语义树减少推理复杂度。
2. **方法论严谨**：对评估指标进行了深入分析，摒弃了不稳定的最大F1和P@K，选择更合理的micro F1和binary F1。
3. **错误传播缓解**：提出多视角验证策略，不仅解决了层次分类的固有问题，且具有通用性。
4. **实验全面**：涵盖多个数据集、多组消融、多种骨干和跨场景验证，消融设计清晰，统计检验充分。
5. **资源高效**：树构建仅需一次GPT-4o API调用（成本不足1美元），模型训练使用LoRA，计算开销可控。
6. **代码开源**：提供GitHub仓库，便于复现和后续研究。

## 8. 不足与局限

1. **输入长度限制**：当前LLM每次只能处理单条文本路径，无法利用跨路径的依赖信息，可能错过全局线索。
2. **次优节点采样策略**：训练时随机选择一个节点作为次优节点，可能不是最优策略，影响验证步骤的训练质量。
3. **领域覆盖有限**：主实验仅使用CodRED（新闻领域）和DocRED，未在更多领域（如生物医学、金融）验证泛化性。
4. **LLM规模限制**：主实验骨干为8B模型，未探索更大规模（如Llama-70B或GPT-4）的效果，可能存在潜力未释放。
5. **层次树构建依赖GPT-4o**：虽然成本低，但可能引入GPT-4o的偏见或错误，影响树的质量（尽管附录显示鲁棒性较好）。
6. **多视角验证增加推理开销**：每层需多次调用LLM，虽然延迟可控，但在高吞吐场景下可能仍有压力。

（完）
