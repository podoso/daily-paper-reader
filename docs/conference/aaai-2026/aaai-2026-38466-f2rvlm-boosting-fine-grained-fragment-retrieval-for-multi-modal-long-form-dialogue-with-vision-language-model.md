---
title: "F2RVLM: Boosting Fine-grained Fragment Retrieval for Multi-Modal Long-form Dialogue with Vision Language Model"
title_zh: F2RVLM：利用视觉语言模型提升多模态长程对话的细粒度片段检索
authors: "Hanbo Bi, Zhiqiang Yuan, Zexi Jia, Jiapei Zhang, Chongyang Li, Peixiang Luo, Ying Deng, Xiaoyue Duan, Jinchao Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38466/42428"
tags: ["query:multimodal"]
score: 6.0
evidence: 利用视觉语言模型进行多模态对话检索
tldr: 针对长程多模态对话中语义片段检索需求，定义了细粒度片段检索任务，构建了最长轮次的多模态对话数据集MLDR，并提出了基于视觉语言模型的F2RVLM方法，有效定位跨模态相关片段。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 872, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1749, \"height\": 909, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 881, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1833, \"height\": 1060, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 764, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38466/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 630, \"height\": 276, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38466/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 684, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38466/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1452, \"height\": 768, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38466/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 703, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38466/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 707, \"height\": 185, \"label\": \"Table\"}]"
motivation: 传统方法难以检索长程多模态对话中语义连贯的片段。
method: 定义细粒度片段检索任务，构建长程数据集，并利用视觉语言模型进行检索。
result: 在构建的数据集上取得优异检索性能，验证了任务和方法的有效性。
conclusion: 该工作填补了多模态对话片段检索的空白。
---

## Abstract
Traditional dialogue retrieval aims to select the most appropriate utterance or image from recent dialogue history. However, they often fail to meet users’ actual needs for revisiting semantically coherent content scattered across long-form conversations. To fill this gap, we define the Fine-grained Fragment Retrieval (FFR) task, requiring models to locate query-relevant fragments, comprising both utterances and images, from multimodal long-form dialogues. As a foundation for FFR, we construct MLDR, the longest-turn multimodal dialogue retrieval dataset to date, averaging 25.45 turns per dialogue, with each naturally spanning three distinct topics. To evaluate generalization in real-world scenarios, we curate and annotate a WeChat-based test set comprising real-world multimodal dialogues with an average of 75.38 turns. Building on these resources, we explore existing generation-based Vision-Language Models (VLMs) on FFR and observe that they often retrieve incoherent utterance-image fragments. While optimized for generating responses from visual-textual inputs, these models lack explicit supervision to ensure semantic coherence within retrieved fragments. To address this, we propose F2RVLM, a generative retrieval model trained in a two-stage paradigm: (1) supervised fine-tuning to inject fragment-level retrieval knowledge, and (2) GRPO-based reinforcement learning with multi-objective rewards to encourage outputs with semantic precision, relevance, and contextual coherence. In addition, to account for difficulty variations arising from differences in intra-fragment element distribution, ranging from locally dense to sparsely scattered, we introduce a difficulty-aware curriculum sampling that ranks training instances by predicted difficulty and gradually incorporates harder examples. This strategy enhances the model’s reasoning ability in long-form, multi-turn dialogue contexts. Experiments on both in-domain and real-domain sets demonstrate that F2RVLM substantially outperforms popular VLMs, achieving superior retrieval performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：传统对话检索只能从近期对话历史中选择最合适的单条语句或图像，无法满足用户对长程多模态对话中语义连贯片段（同时包含语句和图像）的检索需求。实际场景中，对话往往跨越多个话题、几十轮次，用户需要准确定位与查询相关的、分散在对话中的连贯片段。
- **核心问题**：如何定义并实现从长程多模态对话（文本+图像）中细粒度地检索出查询相关的、语义连贯的“片段”（包含若干语句和图像）。
- **整体含义**：该研究填补了多模态长程对话片段检索的空白，提出了新任务（Fine-grained Fragment Retrieval, FFR）、新数据集（MLDR）、新方法（F2RVLM），为智能助手、信息回溯等应用提供了基础。

## 2. 论文提出的方法论

- **核心思想**：将FFR建模为结构化预测任务，给定长程多模态对话和用户查询，模型输出相关语句ID集和图像ID集。采用生成式视觉语言模型（VLM），通过两阶段训练实现精准检索：
  - 第一阶段：监督微调（SFT）注入片段级检索知识。
  - 第二阶段：基于GRPO的强化学习，设计多目标奖励函数，鼓励输出语义精确、相关、上下文连贯的片段。
- **关键技术细节**：
  - 输入结构：在对话中插入特殊标记（如`<|utt id start|>`、`<|img id start|>`）以标识每条语句和图像的ID。
  - 输出格式：模型输出为 `<|utt ids start|>[...]<|utt ids end|>` 和 `<|img ids start|>[...]<|img ids end|>`。
  - 奖励函数（三部分）：
    1. **格式奖励（R_Format）**：二进制奖励，要求输出完全符合格式，且无重复ID。
    2. **检索F1奖励（R_F1）**：基于F1分数并加入长度偏差指数惩罚，平衡精确率和召回率，抑制过度检索。
       \[
       R_{F1} = \sum_{m\in\{utt,img\}} \lambda_m \cdot F1(I_m^{pred}, I_m^{gt}) \cdot \gamma^{||I_m^{pred}| - |I_m^{gt}||}
       \]
    3. **片段顺序一致性奖励（R_Fragment）**：计算检索出的语句和图像按原始位置排列后，相邻元素的CLIP余弦相似度均值，鼓励跨模态连贯性。
  - **难度感知课程采样（Difficulty-aware Curriculum Sampling）**：利用冷启动模型对每个训练样本计算预测F1分数和预测熵，将样本划分为Easy、Confusing、Hard、Medium四类。训练时先使用Easy样本，逐步引入更难样本，提升长程推理能力。
- **算法流程**：
  1. 使用MLDR数据集对基础VLM（如Qwen2-VL系列）进行LoRA微调（SFT）。
  2. 对SFT模型进行冷启动预测，计算每个样本的F1和熵，划分难度等级。
  3. 采用GRPO进行强化学习，每批次从当前难度池中采样样本，用多目标奖励优化策略。

## 3. 实验设计

- **数据集/场景**：
  - **MLDR**：自建的长程多模态对话检索数据集，平均25.45轮/对话，每个对话包含三个不同话题，是目前最长轮次的多模态对话数据集。
  - **WeChat真实测试集**：从12位志愿者收集的真实微信对话，平均75.38轮/对话，经过人工标注，共580个对话片段、1250个查询-对话对，用于评估模型在开放域中的泛化能力。
  - 对比基准：MLDR验证集（in-domain）和WeChat测试集（real-domain）。
- **Benchmark**：对比了多种主流VLM，包括：
  - 嵌入型：CLIP、BLIP2、E5-V、GME。
  - 生成型闭源：GPT-4o、Gemini-2.5-Flash、Claude-Sonnet-4、Doubao-Seed-1.6、Qwen2.5-VL-72B。
  - 生成型开源：Qwen2-VL、Qwen2.5-VL、MiMo-7B-RL、DeepSeek-VL2、LLaVA-1.5、InternVL3、mPLUG-Owl3、Ovis2等。
- **评价指标**：Precision、Recall、F1、MCC（Matthews Correlation Coefficient），分别对语句ID和图像ID计算后取平均。
- **对比方式**：闭源模型和嵌入型模型为零样本推理（不经过MLDR微调）；开源模型经过MLDR SFT微调后评估。F2RVLM基于Qwen2-VL和Qwen2.5-VL（2B、3B、7B）作为骨干，同样经过SFT+GRPO训练。

## 4. 资源与算力

- 论文中未明确说明使用的GPU型号、数量、训练时长等具体算力信息。
- 仅提及采用LoRA参数高效微调，以及基于ms-swift框架实现。未提供训练硬件配置细节。

## 5. 实验数量与充分性

- **主要实验结果表**：表2（主对比实验）、表3（片段一致性与查询相似度）、表4（消融实验）、图5（不同对话轮次性能）、图6（人工主观评价）。
- **实验数量**：
  - 主对比实验：在MLDR验证集和WeChat测试集上，对比了超过15种模型，包括不同规模、不同流派（嵌入型/生成型、开源/闭源）。
  - 消融实验：表4分别去掉了RF1、RFragment、课程采样，验证每个组件的贡献。
  - 额外分析：图5按对话轮次分组（<35、35-65、>65）比较性能；图6人工评价200个样本的覆盖率、相关性、连贯性；表3比较片段顺序一致性和查询-片段相似度。
- **充分性与公平性**：
  - 对比模型涵盖了当前主流VLM，且区分了零样本和微调场景，较为全面。
  - 消融实验清晰证明了各模块的有效性。
  - 在真实微信数据上验证了泛化能力，并进行了人工评价，增加了结论可信度。
  - 缺点：未对比更多基于检索的专用模型（如ColBERT等文本检索模型），但考虑到多模态对话检索的独特性，对比VLM是合理的。

## 6. 论文的主要结论与发现

- **任务有效性**：所定义的FFR任务具有实际需求，现有VLM在此任务上表现不佳，容易检索出语义不连贯的片段。
- **数据集价值**：MLDR是目前最长轮次的多模态对话检索数据集，其微调能显著提升模型在真实场景中的检索性能（如Qwen2.5-VL-7B零样本F1仅12.58%，微调后提升至51.71%）。
- **方法优越性**：F2RVLM在MLDR验证集上达到87.25% F1，在WeChat测试集上达到62.07% F1，全面超越对比模型（包括更大规模的闭源模型），且泛化能力更强（域间性能下降最小）。
- **关键设计作用**：
  - GRPO多目标奖励（F1奖励+片段顺序一致性奖励）能显著提升检索的精确度和语义连贯性。
  - 难度感知课程采样进一步提升了训练稳定性和长对话场景下的推理能力。
- **人工评价**：F2RVLM-7B在覆盖率、相关性和连贯性三个维度上均获得最高偏好票数。

## 7. 优点

- **任务创新**：首次正式定义并系统研究多模态长程对话中的细粒度片段检索任务，填补了现有研究空白。
- **数据集规模与质量**：MLDR平均25.45轮，包含三话题结构，是迄今最长轮次；同时构建了真实微信测试集（平均75.38轮），具有高现实挑战性。
- **方法设计巧妙**：结合监督微调与基于GRPO的强化学习，专门为片段检索设计多目标奖励（特别是片段顺序一致性奖励），以及难度感知课程采样，技术贡献明确。
- **实验全面**：既在域内数据集上评估，又在真实噪声数据上验证泛化；包含零样本、微调、消融、人工评价等多维度分析。
- **代码与数据开源**：提供了代码和数据集链接，便于复现和后续研究。

## 8. 不足与局限

- **算力信息缺失**：未提供训练所需GPU型号、数量、时间等，难以评估方法的经济性和可复现性。
- **数据集潜在偏差**：
  - MLDR由短对话拼接生成，可能缺乏真实对话的自然噪声和话题转换模式。
  - WeChat测试集仅来自12位志愿者，且主题分布偏重工作和科技（>50%），可能无法代表所有用户群体。
- **对比模型覆盖**：虽然对比了许多VLM，但未包括纯文本检索模型（如BM25、ColBERT）或专门的多模态检索模型（如UniIR），难以区分VLM的优势是否来自跨模态理解。
- **评估指标局限**：仅使用ID匹配的F1/MCC，未考虑语义等价但ID不同的情况（例如同义语句或相似图像）。片段顺序一致性奖励依赖CLIP，可能受CLIP局限性影响。
- **方法可扩展性**：F2RVLM基于生成式VLM，推理开销较大；对于超长对话（>100轮），当前模型可能难以处理，实验中已对超长对话进行了分割（>100轮时切片），但未测试不切片的情况。
- **缺乏对错误案例的深入分析**：未讨论失败案例或模型性能的边界（如查询过于模糊、片段跨度极大时的表现）。

（完）
