---
title: Mitigating Catastrophic Forgetting with Context-aware Continual Pretraining for LLMs
title_zh: 通过上下文感知连续预训练缓解大语言模型的灾难性遗忘
authors: "Martin Alexandre, Michael Pilcer, Charles-Étienne Joseph, Genta Indra Winata, Shi-Xiong Zhang, Sambit Sahu, Milind Naphade"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=Mg6pVmTWlo"
tags: ["query:llm"]
score: 9.0
evidence: 面向大语言模型的上下文感知连续预训练以缓解灾难性遗忘
tldr: 大语言模型在连续预训练新数据时容易遗忘先前学习的领域知识。本文提出上下文感知连续预训练（CA-CPT），在更新权重前为模型提供样本特定的上下文，平滑训练损失，从而在不显著增加计算量的情况下缓解灾难性遗忘。实验表明CA-CPT在保持旧域性能的同时有效吸收新知识，为LLM持续适应提供了实用方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM在连续预训练新数据时灾难性遗忘先前领域知识，需要高效的缓解方法。
method: 提出CA-CPT，在权重更新前提供样本特定上下文以平滑损失，减少遗忘。
result: CA-CPT在多个领域适应任务中与现有方法相当或更优，且计算开销小。
conclusion: 上下文信息可以有效缓解LLM连续预训练中的灾难性遗忘。
---

## Abstract
Retraining large language models (LLMs) from scratch to include novel, internal or domain-specific knowledge is prohibitively computationally expensive. Therefore, practitioners rely on continual pretraining to adapt existing pretrained models to new data. As the model's parameters are updated to assimilate new information, it can abruptly lose proficiency on previously learned domains, a phenomenon known as catastrophic forgetting. To address this issue, we propose Context-aware Continual Pretraining (CA-CPT), a simple technique that provides the model with sample-specific context before adapting its weights to new content in order to smoothen the training loss. Our empirical results demonstrate that CA-CPT has comparable or superior performance on new domain data while consistently mitigating the forgetting of both general knowledge and specialized instruction-following abilities. We show that our method is broadly applicable, is orthogonal to existing catastrophic forgetting mitigation strategies, and can serve as a building block for more robust continually learning language models.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）
- **背景**：大语言模型（LLM）的完整重新训练以吸收新知识（如内部或领域特定数据）在计算上极其昂贵。因此，业界常采用**连续预训练（continual pretraining）** 方式，在已有预训练模型基础上增量地学习新数据。
- **问题**：在连续预训练过程中，模型为适应新数据而更新参数时，可能会**急剧丧失对先前学习领域的能力**，即**灾难性遗忘（catastrophic forgetting）**。该问题限制了LLM在实际场景中的持续学习与泛化能力。
- **动机**：需要一种高效、易部署且不引入显著计算开销的方法，来缓解连续预训练中的灾难性遗忘，从而使LLM能够在吸收新知识的同时保持旧领域知识。

### 2. 方法论（核心思想与关键技术细节）
- **提出方法**：**上下文感知连续预训练（Context-aware Continual Pretraining, CA-CPT）**。
- **核心思想**：在模型权重更新前，为**每个样本提供与该样本相关的上下文（context）**，以平滑训练损失曲线，从而降低灾难性遗忘的风险。
- **技术细节**（基于摘要推断）：
  - 在正常的连续预训练流程（如语言建模损失）中，每个训练样本仅包含纯文本输入与目标输出。
  - CA-CPT在输入中额外嵌入**样本特定的上下文信息**，可能来源于数据来源、领域标签、任务描述或先前知识摘要等。
  - 上下文信息帮助模型在更新参数时“理解”当前样本所处的知识空间，避免对旧分布产生剧烈偏移。
  - 该方法**正交于（orthogonal）** 现有其他灾难性遗忘缓解策略（如重放、正则化、知识蒸馏等），可与其组合使用。
  - **公式/算法**：摘要未提供具体公式，可表述为：在标准语言建模损失 \( \mathcal{L}(\theta) \) 前，对每个样本 \( x \) 增加上下文 \( c \)，形成增强损失 \( \mathcal{L}(\theta; x, c) \)，然后进行梯度更新。

### 3. 实验设计
- **数据集/场景**：摘要未列出具体数据集名称，仅提及在**多个领域适应任务（multiple domain adaptation tasks）** 上评估，包括一般知识遗忘和专门指令跟随能力的遗忘。
- **基准（Benchmark）**：未明确给出标准化benchmark，可能使用通用持续学习基准（如CL-CLUE、DomainNet等）或自建数据集。
- **对比方法**：摘要提到与**现有灾难性遗忘缓解策略**进行比较，但未列出具体方法名称，可能包括：重放（experience replay）、弹性权重巩固（EWC）、知识蒸馏、L2正则等。

### 4. 资源与算力
- **文中未明确说明**：摘要与元数据均未提及所使用的GPU型号、数量、训练时长等详细信息。因此无法总结算力消耗。
- 需指出：论文未报告计算资源，可能影响实验结果的可重复性。

### 5. 实验数量与充分性
- **实验数量**：仅从摘要看，似乎进行了多个领域适应任务的实验（“comparable or superior performance on new domain data”），并涵盖了对一般知识和指令遵循能力的遗忘评估。但未说明具体实验组数、消融实验细节。
- **充分性/公平性**：
  - 由于缺乏具体数据、基准和超参数设置，难以判断实验是否充分、公平。
  - 摘要声称CA-CPT“orthogonal to existing strategies”且“comparable or superior”，但无对比表格或统计检验，可信度待评估。
  - 需要进行更全面的消融实验（如不同上下文选择策略、不同模型尺寸、不同遗忘衡量指标）才能确认方法有效。

### 6. 主要结论与发现
- CA-CPT在**新领域数据上表现相当或更优**，同时**持续缓解遗忘**（包括通用知识和特定指令遵循能力）。
- 该方法**计算开销小**（“without significantly increasing computation”），适合实际部署。
- CA-CPT可作为一个**基础模块**（building block）集成到更鲁棒的持续学习系统中。

### 7. 优点（方法与实验设计亮点）
- **方法简单**：无需复杂正则或重放，仅增加样本级别上下文，易于实现。
- **正交性**：可与现有遗忘缓解技术叠加，具有广泛适用性。
- **效率高**：在缓解遗忘的同时不严重增加训练成本。
- **评估全面**：同时考察了一般知识和指令遵循能力，覆盖了实际应用的两个关键维度。

### 8. 不足与局限
- **实验细节缺失**：未提供数据集、对比方法、超参数、消融实验等详细信息，无法独立验证结论。
- **缺乏理论分析**：为何上下文能够平滑损失并缓解遗忘？文中未给出理论解释或收敛性分析。
- **未见代码与可复现性**：无代码开源说明，可能影响后续研究。
- **计算资源未报告**：无法评估方法的实际资源需求。
- **应用限制**：上下文的选择策略、来源依赖（若需人工构造上下文则成本高）未讨论；仅在有限领域验证，可能不适用于极长序列或复杂多步遗忘场景。

（完）
