---
title: "MetaGDPO: Alleviating Catastrophic Forgetting with Metacognitive Knowledge Through Group Direct Preference Optimization"
title_zh: MetaGDPO：通过组直接偏好优化与元认知知识缓解灾难性遗忘
authors: "Lanxue Zhang, Yuqiang Xie, Fang Fang, Fanglong Dong, Rui Liu, Yanan Cao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40777/44738"
tags: ["query:continual"]
score: 8.0
evidence: 利用元认知知识缓解大语言模型灾难性遗忘
tldr: 针对小于8B的LLM微调易遗忘先验技能的问题，提出MetaGDPO方法，通过元认知知识保留训练数据与模型能力的关系，并采用组直接偏好优化约束知识保持，实验证明能有效缓解灾难性遗忘。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有数据集和微调方法忽略训练知识与模型固有能力的关联，且训练目标缺乏知识保持约束，导致小模型灾难性遗忘。
method: 提出MetaGDPO，引入元认知知识建模数据与能力关系，结合组直接偏好优化在微调中约束先验知识保留。
result: 在多个持续学习基准上，MetaGDPO有效减少了遗忘，保持了较高性能。
conclusion: 该工作为缓解小模型微调中的遗忘提供了新范式，具有实用价值。
---

## Abstract
Large Language Models demonstrate strong reasoning capabilities, which can be effectively compressed into smaller models. However, existing datasets and fine-tuning approaches still face challenges that lead to catastrophic forgetting, particularly for models smaller than 8B. First, most datasets typically ignore the relationship between training data knowledge and the model's inherent abilities, making it difficult to preserve prior knowledge. Second, conventional training objectives often fail to constrain inherent knowledge preservation, which can result in forgetting of previously learned skills. To address these issues, we propose a comprehensive solution that alleviates catastrophic forgetting from both the data and fine-tuning approach perspectives. On the data side, we construct a dataset of 5K instances that covers multiple reasoning tasks and incorporates metacognitive knowledge, making it more tolerant and effective for distillation into smaller models. We annotate the metacognitive knowledge required to solve each question and filter the data based on task knowledge and the model's inherent skills. On the training side, we introduce GDPO (Group Direction Preference Optimization), which is better suited for resource-limited scenarios and can efficiently approximate the performance of GRPO. Guided by the large model and by implicitly constraining the optimization path through a reference model, GDPO enables more effective knowledge transfer from the large model and constrains excessive parameter drift. Extensive experiments demonstrate that our approach significantly alleviates catastrophic forgetting and improves reasoning performance on smaller models.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的中文总结。

# 论文总结：MetaGDPO

## 1. 核心问题与整体含义（研究动机与背景）
- **研究动机**：大型语言模型（LLM）展现出强大的推理能力，但将这些能力蒸馏到参数量小于8B的小型模型中时，会面临严重的**灾难性遗忘**问题。即模型在学习新任务（特别是复杂的推理任务）时，会忘记之前已经掌握的技能。
- **问题根源**：
    - **数据层面**：现有数据集（如LIMO, STAR-1）仅以“难度”作为筛选标准，忽视了训练数据与模型已有“元认知知识”（即解决问题所需的知识类型）之间的关联，导致模型为了学习新知识而覆盖旧知识。
    - **训练方法层面**：传统的微调目标（如SFT）或参数高效微调方法（如LoRA）缺乏对模型已有知识的约束，难以在优化过程中保留先验知识。
- **总体目标**：提出一种综合解决方案，在提升小模型推理能力的同时，有效缓解灾难性遗忘。

## 2. 方法论：核心思想、关键技术细节与算法流程
该方法从**数据构建**和**训练方法**两个角度入手，整体框架称为 **MetaGDPO**。

### a) 核心思想
- **数据侧**：构建与模型内在能力对齐的**元认知知识**数据集（**MetaKL**），确保训练数据既包含模型缺乏的新知识，也涵盖模型已掌握的旧知识（作为“提醒”），从而巩固现有能力。
- **训练侧**：提出**组直接偏好优化（GDPO）**，从大模型生成的响应组中学习偏好分布，通过约束参数漂移来实现更稳定的知识转移。

### b) 关键技术细节
- **数据构建（MetaKL）**：
    1.  **数据收集**：从多个现有数据集（如NuminaMath, MMLU, CommonsenseQA, LogiQA）中收集约38K个实例，覆盖数学、常识、安全等任务。
    2.  **元认知知识提取**：使用GPT-4o为每个问题提取解决问题所需的元认知知识，并聚类为约8,325个知识单元（经人工评估，一致性达92.18%）。
    3.  **基于知识的筛选**：
        - 保留需要超过5种知识单元的复杂问题。
        - 根据小模型的原有知识水平（按知识单元统计准确率）进行选择。
        - 采用贪心策略：对每个知识单元，先保留20个问题，然后根据所有模型的平均熟练度，选择更充分的问题。
        - 最终获得**5K**个训练样本（MetaKL）。
- **训练方法（GDPO）**：
    - **核心思想**：离线生成大模型对给定问题的G个响应，计算每个响应的优势值（基于正确性、格式和长度），并利用排序组内相邻响应间的偏好关系来优化小模型。
    - **损失函数**：`L_GDPO(θ) = -1/(G-1) * Σ σ( β/A_i * log(π_θ/π_ref) - β/A_j * log(π_θ/π_ref) )`，其中`σ`是sigmoid函数，`β`是温度系数，`A`是优势，`π`是策略。
    - **复杂度优化**：将原本O(G²)的组内偏好计算简化为O(G)的相邻对计算，适用于资源受限场景。
    - **理论支持**：证明当组大小G≥10时，GDPO的梯度误差相对于2组时小于10%，能有效逼近GRPO的性能。

## 3. 实验设计
- **评估数据集**：从**数学推理、通用推理、安全性**三个维度进行全面评估。
    - **数学推理**: AIME24, AMC23, MATH500, GSM8K, OlympiadBench, Minerva
    - **通用推理**: MMLU, CommonsenseQA, GPQA
    - **安全性**: TrustLLM, StrongReject, WildJailbreak
- **基线模型**：在多种主流小模型架构上进行评估，包括 Qwen3-8B, DeepSeek-R1-Qwen-7B, DeepSeek-R1-LLaMA-8B。
- **对比方法**：
    - **训练数据**：与仅包含难题的LIMo、STAR-1以及它们的混合（L+S）进行对比。
    - **训练方法**：与SFT、DPO（含LoRA变体）进行对比。

## 4. 资源与算力
- 论文中**未明确说明**使用了何种GPU型号、数量及训练时长等具体算力信息。

## 5. 实验数量与充分性
- **实验数量充分**：作者在多处进行了深入分析，包括：
    - **主实验**：在12个标准Benchmark上，对比了多个小模型和多种对比方法。
    - **消融实验**：验证了GDPO中优势权重的效果。
    - **缩放法则分析**：探究了组大小(G)和训练数据规模对性能的影响。
    - **数据构成分析**：比较了不同数据（如纯LIMo、纯MetaKL等）在GDPO框架下的效果。
    - **训练方法对比**：将GDPO与SFT、DPO进行直接对比。
- **客观性和公平性**：实验设计较为合理，控制了数据来源、模型规模和训练参数等变量。使用统一的评测方法（如unbiased pass@1）确保了比较的公正性。

## 6. 主要结论与发现
- **性能提升**：MetaGDPO在所有模型上均实现了总体性能的稳定提升，相对增益约5-10%。
- **缓解遗忘**：
    - 直接使用LIMo或L+S进行训练会导致严重灾难性遗忘（如在GSM8K上下降40-50%），而使用MetaGDPO能有效避免，甚至在GSM8K等任务上有所提升。
    - 在安全性和通用推理任务上，MetaGDPO能在不显著牺牲原有能力的情况下提升或保持性能。
- **方法优势**：
    - 相比于SFT和DPO，GDPO在推理任务上表现更优。
    - 小规模的纯难题数据（如10个样本）也能通过GDPO的组分布学习带来性能提升。
    - 组大小G≥10时，整体性能更优。

## 7. 优点
- **问题导向明确**：清晰定位并解决了小模型灾难性遗忘这一核心痛点。
- **系统性解决方案**：从数据和训练方法双管齐下，而非单点改进，体现了全面的思考。
- **数据构建有理论支撑**：提出“元认知知识”作为数据和模型能力间的桥梁，并进行了人工验证，具有创新性和可解释性。
- **训练方法高效**：GDPO通过离线生成和减少偏好对计算，降低了训练成本，符合资源有限场景的诉求。
- **实验验证充分**：通过多模型、多任务、多方法的对比实验，以及多种分析，证明了方法的有效性和泛化性。

## 8. 不足与局限
- **算力资源未明确**：未能提供具体的算力（GPU型号、时长）消耗数据，不便于读者进行成本评估或复现。
- **数据蒸馏依赖**：方法依赖于从强大的大模型（如DeepSeek-R1）中生成高质量的响应组，这本身需要一定的计算资源。
- **安全与推理的权衡**：实验指出，GDPO在数学/推理任务上表现优于SFT，但SFT在安全性任务上更优，表明方法在推理增强与安全对齐之间可能依然存在微妙的权衡。
- **潜在数据偏差**：数据主要来源于现有的几个公开集合，虽然经过了筛选，但仍可能受到原始数据分布偏差的影响。
- **应用限制**：当前模型和实验主要在7B/8B量级上验证，对于更小（如1B-3B）或更大规模的模型效果未知，可能存在泛化性边界。

（完）
