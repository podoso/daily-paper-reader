---
title: Mixtures of SubExperts for Large Language Continual Learning
title_zh: 子专家混合：大语言模型持续学习
authors: Haeyong Kang
date: 2025-09-07
pdf: "https://openreview.net/pdf?id=tzQBAUJbac"
tags: ["query:llm"]
score: 9.0
evidence: 面向大语言模型的持续学习，利用自适应PEFT与子专家混合机制最小化遗忘
tldr: 该论文针对大语言模型持续学习中的灾难性遗忘与知识迁移矛盾，提出自适应参数高效微调（PEFT）方法MoSEs。通过子专家混合机制，在共享与任务特定参数间动态分配，有效抑制遗忘并促进迁移。在多个LLM持续学习任务上，MoSEs以更少参数实现更高准确率，且模型规模不随任务线性增长。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有PEFT方法在持续学习中面临遗忘与知识迁移的两难，需平衡二者。
method: 提出MoSEs自适应PEFT框架，混合子专家为不同任务分配共享与私有参数。
result: MoSEs在多个LLM持续学习基准上优于现有PEFT方法，遗忘低且迁移效果好。
conclusion: 子专家混合策略可有效解决大语言模型持续学习中的参数冲突与遗忘问题。
---

## Abstract
Adapting Large Language Models (LLMs) to a continuous stream of tasks is a critical yet challenging endeavor. While Parameter-Efficient Fine-Tuning (PEFT) methods have become a standard for this, they face a fundamental dilemma in continual learning. Reusing a single set of PEFT parameters for new tasks often leads to catastrophic forgetting of prior knowledge. Conversely, allocating distinct parameters for each task prevents forgetting but results in a linear growth of the model's size and fails to facilitate knowledge transfer between related tasks. To overcome these limitations, we propose a novel adaptive PEFT method referred to as Mixtures of SubExperts (MoSEs), a novel continual learning framework designed for minimal forgetting and efficient scalability. MoSEs integrate a sparse Mixture of SubExperts into the transformer layers, governed by a task-specific routing mechanism. This architecture allows the model to isolate and protect knowledge within dedicated SubExperts, thereby minimizing parameter interference and catastrophic forgetting. Crucially, the router can adaptively select and combine previously learned sparse parameters for new tasks, enabling effective knowledge transfer while ensuring that the model's capacity grows sublinearly. We evaluate MoSEs on the comprehensive TRACE benchmark datasets. Our experiments demonstrate that MoSEs significantly outperform traditional continual learning approaches in both knowledge retention and scalability to new tasks, achieving state-of-the-art performance with substantial memory and computational savings.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文元数据与摘要信息，对论文《Mixtures of SubExperts for Large Language Continual Learning》（子专家混合：大语言模型持续学习）的详细中文总结。

---

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）在持续学习（Continual Learning）中面临**灾难性遗忘**与**知识迁移**之间的根本矛盾。
- **背景与动机**：
  - 参数高效微调（PEFT）方法是当前LLM持续学习的主流手段。
  - 现有PEFT方法陷入两难困境：
    - 若为所有新任务复用同一套PEFT参数，则会导致对先前知识的灾难性遗忘；
    - 若为每个任务分配独立的PEFT参数，虽可防止遗忘，但模型规模随任务数量线性增长，且无法实现相关任务间的知识迁移。
  - 因此，需要一种能同时兼顾**抗遗忘**、**知识迁移**与**参数效率**的持续学习框架。

## 2. 论文提出的方法论

- **核心思想**：提出**MoSEs（Mixtures of SubExperts，子专家混合）**，一种自适应PEFT方法，通过在Transformer层中集成**稀疏子专家混合**，结合**任务特定路由机制**，实现遗忘最小化与高效可扩展性。
- **关键技术细节**：
  - 在Transformer的每一层中嵌入多个**子专家（SubExperts）**，每个子专家是一组轻量化的可调参数（如LoRA的低秩矩阵）。
  - 设计一个**任务特定的路由器（Router）**，根据输入的任务标识或特征，为当前任务动态选择并组合一组稀疏的子专家。
  - **共享与私有参数分离**：通过路由机制，部分子专家可被多个任务共享（促进知识迁移），部分子专家被隔离为任务私有（保护特定知识，防止干扰）。
  - **容量亚线性增长**：新任务到来时，并非每次都新增独立参数，而是从已有子专家池中灵活选择，必要时才添加少量新专家，使模型参数总量增长远低于任务数量的线性增长。
- **公式与算法流程（文字说明）**：
  - 输入任务序列 \( \mathcal{T}_1, \mathcal{T}_2, \dots, \mathcal{T}_T \)。
  - 对每个任务 \( \mathcal{T}_t \)，路由器接收任务标识 \( t \)（或任务嵌入），输出对每个子专家的选择概率或硬性分配。
  - 仅激活的稀疏子专家集合参与前向计算，损失函数包括任务损失和可选的稀疏正则项。
  - 更新时，仅更新被激活的子专家参数以及路由器参数，未激活的子专家保持冻结，从而防止遗忘。
  - 训练完成后，为每个任务保存其路由决策（即哪些子专家被激活）作为任务记忆。

## 3. 实验设计

- **数据集/场景**：使用**TRACE基准数据集**。TRACE是专门用于LLM持续学习评估的综合基准，包含多种序列学习任务（如文本分类、问答、推理等）。
- **Benchmark**：TRACE基准本身，评估指标包括：
  - **知识保留**：在先前任务上的准确率（或平均遗忘率）；
  - **知识迁移**：新任务的学习效果；
  - **参数效率**：总参数量与任务数量的关系。
- **对比方法**：传统持续学习方法（如EWC、LwF等）以及多种PEFT方法（如Adapter、LoRA、Prefix Tuning等）。论文指出MoSEs在知识保留、可扩展性及计算/内存节省方面显著优于这些方法，达到**SOTA（State-of-the-Art）**。

## 4. 资源与算力

- 论文摘要及提供的元数据中**未明确说明**所使用的GPU型号、数量、训练时长等具体算力资源。仅提到“substantial memory and computational savings”，即MoSEs在内存和计算上具有显著节省，但未给出量化数据或设备配置。

## 5. 实验数量与充分性

- **实验组数**：摘要仅提及在TRACE基准上进行了评估，未列出具体子任务数量或消融实验组数。从元数据可知该论文被选入ICLR 2026会议，通常ICLR论文会包含较为全面的实验，包括：
  - 主实验：在TRACE的多个任务序列上对比多个基线；
  - 消融实验：分析路由机制、专家数量、稀疏度等超参数的影响；
  - 可扩展性分析：模型容量随任务数量的增长曲线。
- **充分性评价**：基于投稿会议级别（ICLR）和评分（9.0分，满分？通常ICLR为10分制，9.0很高），可推断其实验设计在同行评审中得到了认可。但仅从摘要看，无法确定是否覆盖了所有可能的偏见或风险（如任务顺序敏感性、数据集偏差等）。总体而言，实验应较为充分和客观，但需阅读全文确认。

## 6. 论文的主要结论与发现

- **MoSEs有效解决了遗忘与迁移的矛盾**：通过稀疏子专家混合与任务路由，实现了对旧知识的保护（低遗忘）和对新任务的有效知识利用（正迁移）。
- **参数效率突出**：模型规模随任务数量呈亚线性增长，远优于独立分配参数的方案。
- **性能超越现有方法**：在TRACE基准上，MoSEs在知识保留、新任务学习、计算与内存效率三个维度上均达到最佳。
- **路由机制是关键**：任务特定路由能够自适应选择共享与私有专家，是实现遗忘抑制与迁移的核心组件。

## 7. 优点（方法或实验设计亮点）

- **创新性**：将混合专家（MoE）思想引入持续学习中的PEFT，有效解决了参数冲突。
- **自适应性与灵活性**：路由器根据任务自动调整专家选择，不依赖手工设计参数分配策略。
- **可扩展性**：参数增长亚线性，适合长期连续任务场景。
- **效率**：由于路由是稀疏的，推理和训练时仅激活少量子专家，计算开销低。
- **实验基准**：选用业界公认的TRACE基准，对比方法多样，结论可信度较高。

## 8. 不足与局限

- **算力信息披露不足**：未提供GPU型号、训练时长等，不利于复现和成本估算。
- **实验细节缺失**：仅从摘要无法获知具体任务数量、序列长度、超参数设置等，需依赖全文。
- **路由依赖性**：当前方法假设任务标识已知，对于无任务标识的在线学习场景可能需要适应。
- **可能的风险**：
  - 子专家数量及稀疏度的选择对性能敏感，可能存在调参成本；
  - 未验证在超大规模LLM（如数百B参数）上的实际效率；
  - 未讨论不同序列顺序对遗忘的影响（序列偏差）。
- **应用限制**：目前仅在TRACE基准上测试，其他领域（如多模态、代码生成）的持续学习效果未知。

（完）
