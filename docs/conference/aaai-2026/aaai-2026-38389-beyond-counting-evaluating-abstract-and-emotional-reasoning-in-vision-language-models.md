---
title: "Beyond Counting: Evaluating Abstract and Emotional Reasoning in Vision-Language Models"
title_zh: 超越计数：评估视觉语言模型中的抽象与情感推理
authors: "Yuan Zhou, Yan Zhang, Jianlong Chang, Xin Gu, Ying Wang, Kun Ding, Guangwen Yang, Shiming Xiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38389/42351"
tags: ["query:multimodal"]
score: 6.0
evidence: 视觉语言模型评估，感知与信息抽取，基准
tldr: 针对现有VLM基准忽视细粒度和高阶推理能力的问题，提出EmojiGrid基准，包含基于表情符号的视觉数据集和问答对，明确覆盖感知与信息抽取、关系与结构推理、抽象与情感推理三个认知层次，实验揭示了当前VLM在高阶推理上的不足。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有VLM基准局限于粗粒度物体识别和简单关系推理，缺乏对高阶推理能力的评估。
method: 利用表情符号构建网格视觉数据集，设计三个认知层次的问答任务进行诊断性评估。
result: 当前最优VLM在抽象和情感推理任务上表现不佳，凸显了高阶推理的挑战。
conclusion: 该基准为VLM高阶推理能力的评估和改进提供了重要参考。
---

## Abstract
Despite the rapid progress of Vision Language Models (VLMs), existing benchmarks still concentrate on coarse-grained object recognition or simple relational reasoning, leaving the fine-grained and higher-order reasoning abilities of these systems largely unexamined. 
To bridge this critical evaluation gap, we introduce EmojiGrid, a novel diagnostic benchmark specifically designed to probe these fine-grained and higher-order skills. 
Leveraging the universal and semantically rich nature of emojis, we synthesize a grid‑based visual dataset paired with 29,000+ QA pairs.
Each pair is explicitly anchored in a three-level cognitive taxonomy comprising (i) Perception and Information Extraction, (ii) Relational and Structural Reasoning, and (iii) Abstraction and Advanced Cognition.
These dimensions further decompose into nine categories covering a broad range of cognitive skills, including counting, spatial relations, compositional logic, semantic sentiment, and related higher-order reasoning tasks.
Our extensive evaluation of 25 state-of-the-art open-source and proprietary VLMs reveals a significant performance gap between foundational perceptual tasks and higher-level cognitive abilities, particularly in abstraction and advanced emotional reasoning.
Notably, all models struggle with compositional logic, spatial consistency, and especially emotional and semantic understanding. 
EmojiGrid provides a quantifiable, fine-grained benchmark to diagnose VLM limitations and guides future progress toward models that can truly perceive, reason about, and interpret complex, symbol-rich visual scenes.

---

## 论文详细总结（自动生成）

# 论文总结：《Beyond Counting: Evaluating Abstract and Emotional Reasoning in Vision-Language Models》

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：当前视觉语言模型（VLM）在粗粒度物体识别和简单关系推理上表现优异，但现有的基准（如 VQA v2、GQA）主要评估基础感知能力，缺乏对**细粒度感知**和**高阶认知推理**（如抽象、情感、组合逻辑、空间一致性和多步推理）的系统评估。
- **关键缺口**：现有基准无法揭示 VLM 在视觉混乱场景（小、密、多物体）中的感知缺陷，也缺乏对抽象语义、情感理解和复杂逻辑推理的诊断能力。人类不仅识别物体，还能理解符号背后的情绪和意图，而当前 VLM 评估体系难以衡量这种“从识别到解读”的跨越。
- **核心含义**：需要一种新的、具有认知层次结构的诊断基准，来系统性地揭示 VLM 在感知、关系推理和抽象认知方面的真实能力，而不仅仅是单一准确率。

## 2. 提出的方法论

- **核心思想**：利用表情符号（emoji）作为视觉基元，构建网格场景，并基于三层认知分类体系生成问答对，进行诊断性评估。
- **关键技术细节**：
  - **视觉基元选择**：使用150种人脸表情符号（及少量非人脸符号），因其具有小尺寸、富语义、情感明确、可程序化生成、网格布局可消除自然场景歧义等特点。
  - **场景构建**：程序化生成 N×N 网格（4×4 至 8×8），随机填充表情符号，控制密度、布局（随机、聚类、连续路径）等参数，并生成带坐标、数量、关系等信息的元数据作为真实标签。
  - **认知分类体系**：分为三个维度、九个任务：
    - **感知与信息抽取**：定位与识别（Localization & Identification）、视觉属性分析（Visual Attribute Analysis）、计数与聚合（Counting & Aggregation）。
    - **关系与结构推理**：空间与关系推理（Spatial & Relational Reasoning）、连通性与几何（Connectivity & Geometry）、一致性与模式（Consistency & Pattern）。
    - **抽象与高级认知**：语义与情感理解（Semantic & Emotional Understanding）、逻辑与假设推理（Logical & Hypothetical Reasoning）、组合推理（Compositional Reasoning）。
  - **问答生成**：基于模板（60+模板），输入场景元数据，自动生成语法正确、答案唯一的 QA 对，无需人工审核。
- **算法流程**：先收集筛选表情符号 → 程序化生成网格场景并提取元数据 → 根据元数据和模板批量生成 QA 对。采用“场景优先、问题其次”的方式确保逻辑一致性。

## 3. 实验设计

- **数据集/场景**：EmojiGrid 基准包含 **500 张网格图像** 和 **29,339 个 QA 对**。问题平衡分布：感知与信息抽取占 40.43%，关系与结构推理占 32.12%，抽象与高级认知占 27.44%。子任务覆盖 9 类，从 Localization 的 3.41% 到 Counting 的 23.62%。
- **基准与对比方法**：
  - **封闭源模型**：Claude-4-Sonnet、Gemini-2.5-Flash/Pro、GPT-4o、GPT-o4-mini、Qwen-VL-Max（部分具有推理增强能力）。
  - **开源模型**：DeepSeek-VL2、Gemma3-4B/12B/27B、GLM-4.1V-9B-Thinking、InternVL3-8B/14B/38B/78B、Kimi-VL-A3B-Instruct/Thinking、LLaVA-V1.6-Mistral-7B、Llama-3.2-11B-Vision-Instruct、Mistral-Small-3.1-24B-Instruct、Phi-4-Multimodal-Instruct、Qwen2.5-VL-7B/32B/72B、QVQ-72B-Preview，共 25 个模型。
  - **人类基线**：从基准中随机抽取 50 幅图像（>3000 QA 对）组成 EmojiGrid-lite，由 3 名人类参与者作答，结果作为人类水平参考。
- **评估指标**：精确匹配准确率（exact-match accuracy %），适用于数值、多选题和 Yes/No 回答。

## 4. 资源与算力

- 论文**未明确说明**训练或评估所使用的 GPU 型号、数量、训练时长等具体算力信息。所有实验均为推理评估，不涉及模型训练。但文中提及使用了“leading and proprietary VLMs”，这些模型的训练资源通常未公开。因此，资源部分未提供可总结的数字。

## 5. 实验数量与充分性

- **实验数量**：完整评估了 25 个模型在 9 个子任务上的表现（表 2），包括整体准确率和各维度/任务细分。此外，还分析了跨语言性能（英文 vs 中文，图 6）和推理效率（准确率 vs 输出 token 数，图 7）。
- **充分性**：实验覆盖多种规模（从 3B 到 78B 参数）和训练范式（指令微调、推理增强、闭源/开源），且包含人类基线。9 个子任务的平衡设计避免了单一任务主导，评估维度全面。
- **公平性**：使用严格精确匹配，自动化 QA 生成消除了人工标注歧义。但未进行多次运行或统计显著性检验；也未评估 prompt 敏感性（文中提及“performance is often brittle and sensitive to prompt phrasing”）。总体而言，实验设计客观，覆盖充分，但可进一步增加统计鲁棒性。

## 6. 主要结论与发现

- **抽象认知仍是前沿挑战**：模型在语义情感、组合推理等高级任务上表现显著低于感知任务，人类基线（94.05%）远超所有模型（最佳 Gemini-2.5-Pro 仅 73.37%）。
- **闭源 vs 开源性能差距持续存在**：闭源模型（特别是推理增强变体）在复杂多步推理上显著优于开源模型，但即使是顶尖模型，抽象认知任务准确率仍不足 70%。
- **空间推理随模型容量提升**：更大参数和推理增强架构（如 Gemini-2.5 系列、GLM-4.1V-Thinking）在空间关系任务上表现更好。
- **推理效率的差异性**：更长的推理链并不保证更高准确率，错误回答往往伴随着更冗长的输出（如 GPT-o4-mini），而 Gemini-2.5 系列实现了高准确率与低 token 消耗的平衡。
- **跨语言偏差**：大多数模型在英文上表现优于中文，但领先闭源模型（如 Gemini-2.5 系列）表现出鲁棒的双语能力；GLM-4.1V-Thinking 则中文优势突出。

## 7. 优点

- **创新性基准设计**：首次将抽象语义和情感推理纳入 VLM 诊断性评估，使用表情符号作为可精确控制语义和空间的基元，克服了自然图像歧义问题。
- **精细的认知分类**：三层九任务的层次结构不仅提供整体分数，还能生成详细的诊断剖面，揭示模型的具体弱点。
- **自动化生成与高可靠性**：程序化场景生成 + 基于元数据的模板问答，避免了人工标注偏差，保证 QA 对逻辑正确、答案唯一。
- **平衡的问题分布**：刻意避免某类任务主导，确保评估覆盖广泛认知技能。
- **人类基线**：设置 EmojiGrid-lite 提供人类水平参考，使性能差距量化清晰。
- **多维分析**：不仅报告准确率，还分析了跨语言表现和推理效率（token 成本），深化了对模型行为的理解。

## 8. 不足与局限

- **实验覆盖范围**：仅使用表情符号网格场景，与真实世界自然图像存在差距（过于抽象、缺少纹理、光照、背景等），可能影响泛化性诊断。
- **推理效率分析有限**：仅采样了部分推理增强模型进行分析，且 token 长度计算可能因模型输出格式不同而不统一。
- **Prompt 敏感性未深入**：论文提及 prompt 措辞影响性能，但未系统研究不同提示策略的影响。
- **统计显著性缺失**：未报告置信区间、多次运行结果或显著性检验，可能无法排除偶然波动。
- **人类基线构建**：仅 3 名参与者，尽管准确性高，但样本量较小，且未报告评分者间信度。
- **资源消耗未报告**：无法复现评估成本；对于需要长时间推理的模型，成本分析不足。
- **应用限制**：基准集中在模拟场景，直接应用于文档分析、医疗影像等需要细粒度感知的真实环境时，结论需要谨慎推广。

（完）
