---
title: Capability Decomposition for Unified Information Extraction via Hierarchical Mixture-of-Experts
title_zh: 通过分层混合专家进行能力分解的统一信息抽取
authors: "Jing Zhou, Peng Wang, Wenjun Ke, Jiajun Liu, Yao He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.561.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 统一信息抽取框架，结合多项IE任务
tldr: 现有统一信息抽取方法面临模式不一致、隐式推理和全参数适应等问题。本文提出UC-UIE，基于大语言模型，通过统一框架-槽模式显式分解为判断、定位和关联三种通用能力，并采用基于LoRA的分层混合专家架构。实验证明该方法在多个IE基准上实现了更强的泛化能力和参数效率。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.561/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.561/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.561/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.561/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1620, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.561/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 349, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 859, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 624, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 630, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 791, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.561/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1652, \"height\": 1359, \"label\": \"Table\"}]"
motivation: 现有统一信息抽取框架在模式表示、推理透明度和参数效率上存在局限，需要更通用的解决方案。
method: 提出UC-UIE，引入统一框架-槽模式，将IE推理分解为判断、定位、关联三种能力，并采用LoRA分层混合专家架构。
result: 在多个异构IE任务上取得最优或可比结果，同时显著减少可训练参数。
conclusion: 能力分解与高效微调结合可有效提升统一信息抽取的性能和可解释性。
---

## Abstract
Unified Information Extraction (UIE) aims to handle heterogeneous IE tasks within a single framework, but existing methods often suffer from inconsistent schema representation, implicitly intermediate reasoning and full-parameter adaptation, which limit generalization, interpretability and parameter efficiency. To address these issues, we propose UC-UIE (Universal Capabilities-based Unified Information Extractor), a unified framework based on Large Language Model (LLM), which introduces a unified frame-and-slots schema for IE tasks and explicitly decomposes IE reasoning into three universal capabilities: judging, locating, and associating. Furthermore, UC-UIE adopts a Low-Rank Adaptation (LoRA) based hierarchical Mixture-of-Experts (MoE) adapter to fine-tune LLMs for IE tasks, which explicitly models these three capabilities in a task-driven way while ensuring parameter efficiency. With only 1.24% trainable parameters, UC-UIE outperforms full-parameter tuning methods, showing excellent parameter efficiency. Zero-shot evaluation reveals its strong generalization ability to unseen domains and schemas, benefiting from unified schema representation and explicit capability decomposition. Further experiments validate that the hierarchical MoE adapter learns capability specialization and composition, which enhances both UIE performance and interpretability.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有统一信息抽取（UIE）方法在处理异构IE任务（如NER、RE、EE、ABSA）时面临三大挑战：
  - **模式表示不一致**：不同任务使用不同模板或解码器，限制了向未见模式的泛化。
  - **隐式中间推理**：多数方法将IE视为直接序列生成，在共享参数中隐式建模所有推理行为，缺乏可解释性。
  - **全参数微调**：针对百万级PLM尚可，但扩展到十亿级LLM时训练成本过高。
- **研究动机**：设计一个既能统一异构IE任务、又能显式分解推理步骤、且参数高效的LLM框架，以提升泛化能力、可解释性和实用性。
- **整体含义**：论文提出**UC-UIE**，首次将UIE的推理过程显式分解为`judging`（判断）、`locating`（定位）、`associating`（关联）三种通用能力，并通过分层MoE适配器实现能力专门化与参数高效微调，在多个基准上取得了领先性能。

## 2. 论文提出的方法论

### 核心思想
- **统一模式表示**：引入`frame-and-slots`模式（基于框架语义学和槽填充），将每个抽取目标抽象为一个语义框架（如关系类型）及若干带类型的槽（如主体、客体）。输出格式统一为`{(FT: FF): [(ST1: SF1), (ST2: SF2), ...]}`，覆盖不同IE任务。
- **显式能力分解**：受语言学中框架意义构建启发，将IE推理分解为三种任务无关的通用能力：
  - **Judging**：决定哪些框架和槽类型应被实例化（如实体类型、关系类型等）。
  - **Locating**：识别文本中填充这些框架和槽的文本跨度（如实体提及、触发词、论元等）。
  - **Associating**：将抽取的元素组织成连贯的结构（如主-客体配对、论元绑定等）。
- **参数高效微调**：设计基于LoRA的**分层Mixture-of-Experts (MoE) 适配器**，插入LLM的FFN线性层。

### 关键技术细节
- **分层MoE结构**：
  - **高层MoE**：包含一个**共享专家**（总是激活）和三个**能力专家**（Judging、Locating、Associating），由**任务驱动的路由器**（硬路由或软路由）决定激活。
    - **硬路由**：根据任务类型启发式选择能力专家（例如NER只激活Judging和Locating）。
    - **软路由**：学习一个可训练路由器，基于任务指令的平均池化表示预测各专家的贡献权重（使用sigmoid输出0~1）。软路由通过BCE损失监督。
  - **低层MoE**：每个能力专家内部由多个LoRA子专家（本实验Q=4）和一个令牌级路由器组成。所有子专家采用密集激活（而非稀疏激活）以避免负载不均衡，通过熵损失鼓励子专家权重平衡。
- **两阶段训练策略**：
  - **阶段一（能力预热）**：分别用针对三种能力构建的子数据集训练对应的能力专家（仅激活该能力专家和共享专家）。
  - **阶段二（多任务学习）**：在全量多任务、多领域数据上微调，学习自适应的能力组合。
- **优化目标**：主任务损失（next token prediction）+ 辅助BCE损失（软路由） + 辅助熵损失（子专家平衡）。总损失：\( \mathcal{L}_{total} = \mathcal{L}_{task} + \gamma \mathcal{L}_{bce} + \beta \mathcal{L}_{entropy} \)，其中γ=β=0.1。

## 3. 实验设计

### 数据集与场景
- **覆盖任务**：NER（21个数据集）、RE（6个）、EE（3个）、ABSA（4个），共34个数据集。
- **来源**：30个来自IE INSTRUCTIONS，额外补充SemEval 14/15/16的ABSA数据集。
- **场景**：监督学习（全量数据）、低资源学习（1%/5%/10%训练数据）、零样本学习（未见领域/未见任务）。

### 评估指标
- 基于span的偏移Micro-F1。

### 对比方法
- **13个基线**：乌斯曼（USM, UniEX, RexUIE, Mirror, TRUE-UIE, UIE, LasUIE, InstructUIE, YAYI-UIE, GoLLIE, KnowCoder, RUIE, KnowCoder-X）。涵盖链接式方法和生成式方法。

### 实验设置
- Backbone：LLaMA-2-7B，冻结预训练权重。
- 适配器：分层MoE（84M可训练参数，占整体1.24%）。LoRA rank=4, α=8。每个能力专家含4个子专家。
- 超参数：学习率3e-4，batch size 16，训练3个epoch，共21042步。

## 4. 资源与算力

- **硬件**：3块 NVIDIA RTX 3090Ti GPU。
- **训练时长**：未明确给出具体耗时，但提到112,229个训练实例，3个epoch，21,042步，且使用3块GPU并行。推算训练时间在数小时到十数小时级别（具体取决于实现）。
- **显存需求**：LLaMA-2-7B约需14GB显存（FP16），加上适配器参数，单卡应能容纳。三卡并行可能用于数据并行或流水线。

## 5. 实验数量与充分性

- **主实验**：监督设置下在21个NER、6个RE、3个ED、3个EAE数据集上报告结果（表1），覆盖广泛。
- **低资源实验**：在CoNLL2003、CoNLL2004、ACE2005上设置1%/5%/10%比例（表2），与UIE、LasUIE、KnowCoder对比。
- **零样本实验**：7个未见领域NER、2个未见领域RE、1个未见任务ABSA（表3），并与多个基线对比。
- **消融实验**（表4）：分别移除软路由、共享专家、能力预热、熵损失、BCE损失，验证各组件的贡献。
- **深入分析**：
  - 子专家数量影响（图5）：1-8个，在监督/低资源/零样本下均测试。
  - 能力专门化与组合（表5、6）：通过不同专家激活组合评估三种能力子任务和完整IE任务的表现。
  - 熵损失效果：可视化子专家路由权重分布（图6）。
- **充分性**：实验设计系统、对比基线全面、涵盖多种场景和消融，验证了方法各部分的必要性。公平性方面，采用了相同的评估指标和公开数据集，并报告5次平均结果，较为客观。

## 6. 论文的主要结论与发现

- **性能超越**：UC-UIE在监督设置下平均F1达84.51%，超越所有基线（第二名KnowCoder-X为83.61%），且仅使用1.24%可训练参数，参数效率极高。
- **强泛化**：零样本场景下，在多个未见领域NER和RE上达到或超过监督方法的半水平；在未见任务ABSA上超越1-shot方法。
- **能力分解有效**：通过消融和专门化分析，证实三种能力专家各自独立且能有效组合，提供可解释性。
- **分层MoE设计关键**：共享专家、软路由、熵损失、能力预热均显著提升性能。子专家数量为4时最优。

## 7. 优点

- **统一性与灵活性**：frame-and-slots模式覆盖异构任务，无需任务特定模板；软路由允许自适应激活能力。
- **显式可解释推理**：能力分解使得模型推理过程透明，容易诊断和调试。
- **参数极致高效**：仅更新1.24%参数即超越全参数方法，适合大模型应用。
- **系统全面的实验**：涵盖34数据集、多种场景、深入消融和分析，结论可靠。
- **MoE设计精细**：共享专家减少冗余，低层密集激活避免负载不均，熵损失保证平衡。

## 8. 不足与局限

- **任务覆盖有限**：仅评估4种IE任务，未涉及文档级IE、多语言IE、开放IE等更广泛场景；也未推广到其他NLP任务如文本分类。
- **模式依赖**：frame-and-slots模式适合预定义模式的任务，不适用于schema-free（开放IE、按需IE），需进一步研究。
- **计算资源优化空间**：尽管参数高效，但推理时仍需要LLM前向传播和MoE路由，可能对资源受限场景不够友好。
- **未讨论负载均衡详细分析**：虽然通过密集激活和熵损失缓解，但未给出实际的负载指标（如专家利用率）。
- **未报告训练时间**：缺少与基线在推理/训练时间上的对比。

（完）
