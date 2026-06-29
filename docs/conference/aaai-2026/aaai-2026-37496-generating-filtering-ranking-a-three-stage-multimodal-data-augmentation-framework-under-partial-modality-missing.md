---
title: "Generating-Filtering-Ranking: A Three-Stage MultiModal Data Augmentation Framework Under Partial Modality Missing"
title_zh: 生成-过滤-排序：部分模态缺失下的三阶段多模态数据增强框架
authors: "Zhirui Kuai, Huan Zhang, Yang Yang, Yiping Ma, Mingjing Huang, Ning Gui, Li Kuang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37496/41458"
tags: ["query:multimodal"]
score: 6.0
evidence: 多模态数据增强处理缺失模态
tldr: 本文针对多模态缺失数据增强中的语义不准确和分布偏好差异问题，提出生成-过滤-排序三阶段框架，利用多模态大模型生成数据，并通过场景图匹配过滤保证语义一致性，最后排序选择高质量数据，实验证明有效增强模型性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 788, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1816, \"height\": 1050, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 837, \"height\": 966, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 840, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 863, \"height\": 668, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1826, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37496/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 842, \"height\": 543, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37496/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1815, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37496/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37496/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 876, \"height\": 785, \"label\": \"Table\"}]"
motivation: 现有方法合成缺失模态数据时存在语义不准确和分布偏差。
method: 通过多模态大模型生成候选数据，用场景图匹配过滤和排序选择最优数据。
result: 在多个下游任务上提升了使用增强数据训练的模型性能。
conclusion: GFR框架有效缓解了多模态数据缺失问题。
---

## Abstract
Multimodal data significantly improves the performance of pretrained models, but its practical application is often limited by missing or incomplete data across modalities. There are two key challenges that existing methods of synthesizing missing data face: (1) semantic inaccuracies due to model hallucinations and (2) discrepancies in distribution preferences between generated and original data. To address these challenges, we propose a novel three-stage multimodal data augmentation framework (GFR), which Generate, Filter, and Rank missing modality data. Our framework leverages multimodal large models for diverse data generation, designs a scene graph matching-based filtering algorithm to ensure semantic consistency, and constructs a preference-aware ranking model to align the generated data with both the original distribution and task relevance. Our framework not only enhances semantic diversity and consistency in data generation but also effectively captures the implicit characteristics of the original dataset and the target model. We demonstrate the effectiveness of GFR across multiple datasets by testing different missing types and missing ratios.

---

## 论文详细总结（自动生成）

好的，基于您提供的论文内容，以下是对该论文《Generating-Filtering-Ranking: A Three-Stage MultiModal Data Augmentation Framework Under Partial Modality Missing》的结构化、深入、客观的总结。

### 论文核心问题与整体含义

- **研究动机与背景**：现实世界中，多模态数据（如图像和文本）经常因硬件限制、隐私问题或环境干扰而面临**部分模态缺失**的问题。这会严重导致多模态预训练模型性能下降，甚至可能不如单模态模型。现有方法主要分为模型级（需修改架构）和数据级（重构缺失数据），其中数据级方法又分为检索式和生成式。
- **核心问题**：当前基于生成式的数据增强方法主要面临两大挑战：
    1.  **语义不准确**：生成模型（如多模态大语言模型 MLLM）可能产生幻觉，生成与原始数据语义不一致的内容。
    2.  **分布偏好差异**：生成数据在风格、结构等隐式特征上与原始数据集的分布存在偏差（例如，原始数据集为写实照片，生成模型却产出了卡通风格图像）。

### 论文方法论

- **核心思想**：受推荐系统启发，提出一个名为 **GFR (Generating-Filtering-Ranking)** 的三阶段数据增强框架，旨在解决语义不准确和分布偏好差异问题。
- **技术细节与算法流程**：
    1.  **生成阶段**：利用预训练的多模态大模型（MLLM）生成缺失模态的候选数据。例如，使用 **Stable Diffusion XL**（图像生成）和 **Qwen2.5-VL**（文本生成）。此阶段通过数据增强（如随机裁剪、色彩变换、同义词替换）和精心设计的提示词来生成多样化的候选集。
    2.  **过滤阶段**：采用**场景图匹配**算法来过滤掉语义不一致的候选数据，以缓解幻觉问题。
        -   首先，将现有模态数据和生成的候选数据均转换为场景图（Scene Graph），提取实体和关系三元组。
        -   然后，通过**字符串匹配**和**语义相似度匹配**（使用BGE编码器计算余弦相似度）来比对生成的场景图与原始场景图。
        -   只有生成的场景图**包含了原始场景图中的所有实体节点**，且至少存在一条相似关系的候选数据才会被保留。此过程也考虑了多样性，避免保留重复的内容。
    3.  **排序阶段**：训练一个**偏好感知排序模型**，对候选数据进行打分，从而选择与原始数据集分布和目标任务最一致的样本。
        -   **训练数据构建**：将生成的候选数据与原始的另一模态数据配对，输入到目标多模态分类模型中，根据其分类结果（预测正确与否）构建正负样本对（Partial-order pairs）。
        -   **排序模型**：使用与目标模型（如ViLT）结构相似的排序模型进行打分。
        -   **损失函数**：使用 **Circle Loss** 在多个正负样本对之间最大化分数差距，以捕捉数据集的隐式特征（如风格、任务相关性）。

### 实验设计

- **数据集**：实验在多个多模态分类数据集上进行，包括：
    -   **多标签分类**：MM-IMDb（电影类型）、IU-Xray（医学报告）。
    -   **多类/单标签分类**：Food101（食物）、MVSA（情感）、Pascal VOC（物体）。
- **Benchmark与评估指标**：
    -   主要评估指标为**性能恢复能力** (Δ)，即 `(M - N) / N`，其中 `N` 是完整模态下的性能，`M` 是补全后的性能。主实验还报告了F1-Score（多标签）和Accuracy（多类/单标签）。
- **对比方法**：
    -   **基线模型**：CLIP-based Baseline, ViLT-based Baseline。
    -   **缺失数据基线**：Baseline + missing。
    -   **当前最优方法 (SOTA)**：MMIN, DiCMoR, MPLMM, Knowledge Bridger (KB), Missing-aware-prompts (MAP), MACP。
    -   **单一缺失场景下的所有模型**在同一状态下呈现。

### 资源与算力

-   论文中**未明确提及**实验所需的GPU型号、数量及具体训练时长等算力信息。它仅提及使用了中央民族大学高性能计算中心的计算资源。

### 实验数量与充分性

-   **实验数量**：实验设计较为充分，主要包括：
    1.  **主实验**：在两个主要数据集（MM-IMDb, IU-Xray）上，对比在30%、50%、70%的图像缺失率下，GFR与多种SOTA方法的性能。
    2.  **消融实验**：分别对**过滤阶段**（对比无过滤、文本相似度过滤、大模型判断过滤、场景图匹配过滤）和**排序阶段**（对比无排序、Pairwise Loss、Circle Loss）进行了组件级分析。
    3.  **泛化性实验**：在三个额外数据集（Food101, MVSA, Pascal VOC）上，针对图像和文本缺失两种场景，测试了60%和70%缺失率下的性能。
    4.  **可视化分析**：展示了GFR生成图像与直接生成的图像在视觉质量上的对比。
-   **充分性与公平性**：
    -   **充分**：实验覆盖了不同的缺失类型（图像缺失、文本缺失）和缺失比例，并进行了消融研究验证了各模块的有效性，体现了实验的严谨性。
    -   **客观公平**：作者进行了公平的对比，包括与其他SOTA方法的性能比较，并在统一的基线模型（ViLT）上实现和评估了部分方法，以避免算力差异带来的影响。同时，使用**性能恢复能力**作为主要指标，消除了不同骨干网络带来的偏差。

### 论文主要结论与发现

-   **核心结论**：GFR框架能有效解决生成式数据增强中的语义不准确和分布偏好差异两大挑战，在部分模态缺失的场景下，显著恢复了模型的性能。
-   **关键发现**：
    -   GFR在多种数据集和缺失情况下均优于所有对比的SOTA方法，尤其在IU-Xray等高缺失率场景下表现突出。
    -   消融实验证明，**过滤阶段**（特别是场景图匹配）和**排序阶段**（特别是Circle Loss）是GFR不可或缺的组成部分，各自对性能提升有显著贡献。
    -   定性分析显示，GFR能生成与原始数据高度一致（内容、风格、关系）的样本，而简单生成则存在幻觉和风格不匹配问题。

### 论文优点

-   **创新方法**：提出了**生成-过滤-排序**的三阶段框架，将生成式模型、结构化的场景图匹配和偏好学习的思想巧妙结合，是一个系统性、完整的解决方案。
-   **有效解决两大挑战**：场景图匹配机制直接针对**语义不一致**问题，而偏好学习排序机制则有效处理了**分布偏好差异**问题，且其排序数据来源于目标模型分类结果，而非单一的真实标签，更贴近实际应用。
-   **通用性强**：框架具有很高的通用性，不限于特定任务或骨干网络，作者也通过实验验证了其在多个不同领域（美食、医疗、公共物体）和不同任务（多标签、单标签）上的有效性。
-   **消融实验设计合理**：消融实验清晰揭示了过滤和排序环节中不同子技术的效果，为框架的优化提供了明确方向。

### 不足与局限

-   **计算成本与资源**：第1阶段依赖MLLM生成候选数据，第3阶段需要训练排序模型，这带来了额外的计算成本和资源消耗。论文未提供具体的算力开销分析。
-   **应用场景限制**：框架假设语义一致性是必要的。作者指出，在**多模态隐喻、多模态仇恨言论分析**等任务中，模态间可能存在冲突性信息（即一致性假设可能不成立），此时框架的适用性需要进一步考察。
-   **实验覆盖有限**：虽然使用了多个数据集，但主要集中在**视觉-语言**分类任务上。缺少对其他常见多模态任务（如视觉问答、图像描述、跨模态检索）的直接验证，其泛化性主要通过对分类任务的实验来论证。
-   **潜在的选择偏差**：排序阶段的训练样本构建依赖于目标分类模型的行为，这可能存在一定程度的**分布内选择偏差**，即模型更倾向于选择它自己“喜欢”的而不是真正最优的样本，导致过拟合的风险。

您指出的“请继续补全”处实际上是我上一轮输出的一个格式错误（误将结束词写成了提示）。在“不足与局限”之后，应有如下内容：

### 未来工作方向

- **降低计算开销**：可探索轻量化生成模型或知识蒸馏技术，减少MLLM生成阶段的资源消耗；同时可尝试将排序模块集成到目标模型中，实现端到端的统一优化。
- **扩展应用场景**：将GFR框架应用于语义冲突（如讽刺、隐喻）的多模态任务，验证其在非一致性数据上的鲁棒性；或迁移至视觉问答、图像描述等生成式任务。
- **增强排序模型的泛化能力**：引入对抗训练或元学习，缓解因目标模型行为偏置导致的选择偏差问题；也可利用无监督或自监督排序策略，减少对目标模型分类结果的依赖。
- **多模态缺失混合场景**：当前仅考虑了单一模态完全缺失的情况，未来可研究同时缺失不同比例图像和文本的混合场景，以及模态部分缺失（如图像模糊、文本截断）的细粒度补全。

### 总结

论文《Generating-Filtering-Ranking: A Three-Stage MultiModal Data Augmentation Framework Under Partial Modality Missing》提出了一个系统性的生成-过滤-排序三阶段框架，有效解决了生成式数据增强在部分模态缺失任务中的语义不对准和分布偏移两大核心挑战。通过场景图匹配保障语义一致性，并通过偏好排序模型隐式学习任务适配风格，GFR在多个多模态分类数据集上展现了显著的性能恢复能力，并借助充分的消融与泛化实验验证了各模块的有效性与框架的普适性。尽管存在计算成本较高和应用场景限制等不足，该工作为多模态缺失场景下的数据增强提供了新颖且实用的思路，具有重要的理论价值与应用潜力。

（完）
