---
title: "Relation-R1: Progressively Cognitive Chain-of-Thought Guided Reinforcement Learning for Unified Relation Comprehension"
title_zh: Relation-R1：渐进式认知思维链引导的强化学习统一关系理解
authors: "Lin Li, Wei Chen, Jiahui Li, Kwang-Ting Cheng, Long Chen"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37557/41519"
tags: ["query:joint-mer"]
score: 9.0
evidence: 视觉关系理解，多模态，链式思维强化学习用于关系理解
tldr: 针对多模态大语言模型在视觉关系理解上依赖语言先验而无法捕获多实体结构化语义依赖的问题，提出Relation-R1，首次融合认知链式思维引导的监督微调和强化学习，显式建模N元关系中的语义角色依赖，显著提升了复杂关系检测能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1746, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 883, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 181, \"height\": 144, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 176, \"height\": 136, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 883, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37557/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1635, \"height\": 230, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37557/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 585, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37557/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37557/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1696, \"height\": 354, \"label\": \"Table\"}]"
motivation: 现有MLLM在视觉关系理解中过度依赖语言先验，难以处理多实体N元关系。
method: 提出Relation-R1，整合认知链式思维引导的监督微调和强化学习，建模结构化语义依赖。
result: 在视觉关系检测基准上达到最优，尤其擅长N元关系。
conclusion: 该方法为多模态关系理解提供了新范式。
---

## Abstract
Recent advances in multi-modal large language models (MLLMs) have significantly improved object-level grounding and region captioning. However, they remain limited in visual relation understanding, struggling even with binary relation detection, let alone N-ary relations involving multiple semantic roles. The core reason is the lack of modeling for structural semantic dependencies among multi-entities, leading to over-reliance on language priors (e.g., defaulting to "person drinks a milk" if a person is merely holding it). To this end, we propose Relation-R1, the first unified relation comprehension framework that explicitly integrates cognitive chain-of-thought (CoT)-guided supervised fine-tuning (SFT) and group relative policy optimization (GRPO) within a reinforcement learning (RL) paradigm. Specifically, we first establish foundational reasoning capabilities via SFT, enforcing structured outputs with thinking processes. Then, GRPO is utilized to refine these outputs via multi-rewards optimization, prioritizing visual-semantic grounding over language-induced biases, thereby improving generalization capability. Furthermore, we investigate the impact of various CoT strategies within this framework, demonstrating that a specific-to-general progressive approach in CoT guidance further improves generalization, especially in capturing synonymous N-ary relations. Extensive experiments on widely-used PSG and SWiG datasets demonstrate that Relation-R1 achieves state-of-the-art performance in both binary and N-ary relation understanding.

---

## 论文详细总结（自动生成）

# 论文总结：Relation-R1: Progressively Cognitive Chain-of-Thought Guided Reinforcement Learning for Unified Relation Comprehension

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态大语言模型（MLLMs）在视觉关系理解方面存在严重局限，特别是难以处理涉及多个实体的 **N元关系**（N-ary relation），即使是二元关系（binary relation）检测也表现不佳。
- **根本原因**：现有模型缺乏对多实体间**结构化语义依赖**的建模，导致过度依赖**语言先验**（例如，仅因“牛奶”常与“喝”关联，即使人物只是拿着杯子，模型也默认输出“人喝牛奶”），而非基于视觉语义线索进行推理。
- **整体目标**：设计一个统一的框架，能够同时处理二元关系和N元关系检测，并具备强推理能力和泛化性能，避免语言偏见的干扰。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 **Relation-R1**，两阶段框架：
  1. **Stage 1: 监督微调（SFT）**：引入**认知思维链（Cognitive CoT）** 指导，使模型学习结构化的输出格式（思考过程 + 答案），建立基础推理能力。CoT包括对象识别、定位、关系推断等步骤。
  2. **Stage 2: 强化学习（RL）**：采用**组相对策略优化（GRPO）**，通过多奖励（格式奖励、二元关系奖励、N元关系奖励）优化模型输出，优先强化视觉语义接地能力，抑制语言偏置，提升泛化性。
- **关键技术细节**：
  - **渐进式CoT指导**：先使用**模板式CoT**（固定推理步骤）进行SFT，再使用少量**MLLM生成的CoT**（更灵活多样的推理路径）进行微调，实现从特定到一般的学习，提升模型探索同义N元关系的能力。
  - **GRPO算法**（公式1-3）：
    - 目标函数：\( J_{GRPO}(\theta) = \mathbb{E}_{q\sim Q,\{o_i\}_i\sim\pi_{\theta_{old}}} \left[ \frac{1}{G}\sum_{i=1}^G \min(\rho_i A_i, \text{clip}(\rho_i,1-\epsilon,1+\epsilon)A_i) - \beta D_{KL}(\pi_\theta \parallel \pi_{ref}) \right] \)
    - 优势 \( A_i = \frac{r_i - \text{mean}(\{r_1,...,r_G\})}{\text{std}(\{r_1,...,r_G\})} \)
  - **奖励设计**：
    - 格式奖励 \( r_{form} \)：是否包含 `<think>...</think>` 和 `<answer>...</answer>`。
    - 二元关系奖励 \( r_{binary} = \alpha \cdot R + (1-\alpha) \cdot mR \)：R为样本级三元组召回率，mR为谓词类别平均召回率（要求框IoU≥0.5）。
    - N元关系奖励 \( r_{n-ary} = \beta \cdot V_e + (1-\beta) \cdot V_{grnd} \)：V_e为实体类别与角色准确性，V_{grnd}为空间定位准确性（IoU≥0.5）。
- **多任务门控**：根据答案中是否包含 `<ref>` 标签动态选择应用二元还是N元奖励。

## 3. 实验设计：使用的数据集/场景、benchmark、对比方法
- **数据集**：
  - **PSG（Panoptic Scene Graph）**：48,749张图像，56个关系类别，用于二元关系检测。实验采用两种格式：场景图标题格式（scene graph caption，遵循ASMv2）和标准场景图格式。
  - **SWiG（Grounded Situation Recognition）**：25,200张测试图像，504个动词类别，190个语义角色，用于N元关系（接地情境识别）检测。
- **基准与评估指标**：
  - 二元关系：**Recall**（三元组召回率）、**mRecall**（谓词平均召回率，均要求IoU≥0.5）。
  - N元关系：**Verb**（动词准确性）、**Value**（名词角色准确性）、**Value-all**、**Grnd**（接地准确性）、**Grnd-all**（全角色接地准确性）。
- **对比方法**：
  - 二元关系：封闭式方法（IMP, MOTIFS, VCTree, GPSNet, PSGFormer），开放式方法（TextPSG, R1-SGG, ASMv2, SpaceSGG）。
  - N元关系：封闭式（ISL, JSL, GSRTR, CoFormer, SituFormer, GSRFormer）及开放式（OpenSU）。

## 4. 资源与算力
- **论文正文未明确说明**所使用的GPU型号、数量或训练时长。作者仅在“实现细节”部分标注“refer to the Appendix”，但提取文本中未包含附录内容，因此无法确定具体算力配置。

## 5. 实验数量与充分性
- **实验组数**：
  - **主实验**：在PSG（表1）和SWiG（表2）上分别与多个SOTA比较，涵盖两种任务。
  - **消融实验**（表3）：对比不同CoT策略（无CoT / 模板式 / MLLM生成 / 渐进式）对二元和N元任务的影响。
  - **奖励分析**（图3）：展示训练过程中奖励变化曲线（二元和N元任务）。
  - **完成长度分析**（图5）：统计GRPO训练中输出长度的变化。
  - **定性分析**（图4）：可视化二元关系检测的思考过程。
- **充分性与公平性**：
  - 对比方法覆盖广泛，包括封闭式和开放式方法，且超参数β（0.5）和α（0.5）有说明。
  - 消融实验系统比较了CoT变体，并分析了去掉动词约束的影响（表3蓝色指标），验证了渐进式策略的优势。
  - 但主要仅依托两个公开数据集，缺少跨数据集泛化验证；未见对超参数（α, β, 奖励权重）进行敏感性分析；未提供误差分析或失败案例讨论。

## 6. 论文的主要结论与发现
- **核心发现**：Relation-R1在二元和N元关系检测上均达到**当前最优（SOTA）**，特别是在PSG数据集上Recall提升约6.84-6.90%，在SWiG上Grnd-all提升14.48%。
- **渐进式CoT是关键**：相比单独使用模板式或MLLM生成的CoT，**特定→一般的渐进式指导**显著提升了模型在N元关系中的泛化能力，特别是学会了输出**同义关系表达**。
- **RL优于纯SFT**：仅SFT受限于语言先验和过拟合，而RL通过多奖励优化有效地将视觉接地置于优先地位。
- **参数效率高**：3B参数模型超越了13B参数方法（ASMv2, SpaceSGG）。不同CoT策略的性能分析。

## 7. 优点：方法或实验设计上的亮点
- **创新性**：首次将二元和N元关系检测统一到一个框架中，并融合“认知CoT + RL”范式，针对语言偏见问题提出针对性解决方案。
- **启发性**：通过渐进式CoT（模板→MLLM生成）展示了如何平衡推理规范性与探索多样性，为多模态关系推理提供了新思路。
- **实验设计稳健**：
  - 使用两个互补数据集（场景图 + 情境识别）全面评估。
  - 消融实验深入分析了CoT策略和奖励设计，图3和图5提供了训练动态的可视化证据。
  - 定性示例（图4）清晰地展示了模型的可解释性思考过程。
- **实践价值**：3B模型达到优异性能，降低部署成本。

## 8. 不足与局限
- **实验覆盖有限**：仅使用PSG和SWiG两个数据集，未在更多场景（如视频、3D场景）验证泛化性。
- **计算资源未明确**：未报告训练所需的具体GPU时长或参数量，影响可复现性评估。
- **超参数敏感性未知**：奖励公式中α和β设为固定值（α=0.5, β=0.5），缺乏对其最优值的探索或鲁棒性分析。
- **语言先验的残余风险**：尽管RL鼓励视觉接地，但CoT本身由模板或MLLM生成，仍可能隐含语言偏见，文中未系统评估这种影响。
- **对CoT质量的依赖**：MLLM生成的CoT若不准确，可能会误导模型（表3中MLLM CoT在N元任务Verb上反而不如模板式），框架鲁棒性有待进一步验证。
- **缺少失败案例分析**：未讨论模型在何种条件下可能犯错（如长尾关系、模糊场景等），降低了结论的深度。

（完）
