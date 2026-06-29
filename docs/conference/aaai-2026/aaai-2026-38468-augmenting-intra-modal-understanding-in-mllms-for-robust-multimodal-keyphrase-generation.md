---
title: Augmenting Intra-Modal Understanding in MLLMs for Robust Multimodal Keyphrase Generation
title_zh: 增强多模态大语言模型的模态内理解以实现鲁棒的多模态关键词生成
authors: "Jiajun Cao, Qinggang Zhang, Yunbo Tang, Zhishang Xiang, Chang Yang, Jinsong Su"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38468/42430"
tags: ["query:multimodal"]
score: 6.0
evidence: 利用多模态大语言模型进行多模态关键词生成
tldr: 针对多模态大语言模型在关键词生成任务中存在的模态偏差和细粒度特征提取不足问题，提出增强模态内理解的方法，有效提升在噪声数据上的鲁棒性，生成更准确的关键词集合。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38468/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 870, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38468/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 778, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38468/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 854, \"height\": 526, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38468/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1838, \"height\": 890, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38468/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 876, \"height\": 985, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38468/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 834, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38468/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1845, \"height\": 682, \"label\": \"Table\"}]"
motivation: MLLMs存在模态偏差和细粒度特征提取不足的问题。
method: 通过增强模态内理解模块，提升MLLM对噪声数据的鲁棒性。
result: 在多个多模态关键词生成基准上取得鲁棒且优越的性能。
conclusion: 增强模态内理解是提升MLLM多模态生成任务的关键。
---

## Abstract
Multimodal keyphrase generation (MKP) aims to extract a concise set of keyphrases that capture the essential meaning of paired image–text inputs, enabling structured understanding, indexing, and retrieval of multimedia data across the web and social platforms. Success in this task demands effectively bridging the semantic gap between heterogeneous modalities. While multimodal large language models (MLLMs) achieve superior cross-modal understanding by leveraging massive pretraining on image-text corpora, we observe that they often struggle with modality bias and fine-grained intra-modal feature extraction. This oversight leads to a lack of robustness in real-world scenarios where multimedia data is noisy, along with incomplete or misaligned modalities. To address this problem, we propose AimKP, a novel framework that explicitly reinforces intra-modal semantic learning in MLLMs while preserving cross-modal alignment. AimKP incorporates two core innovations: (i) Progressive Modality Masking, which forces fine-grained feature extraction from corrupted inputs by progressively masking modality information during training; (ii) Gradient-based Filtering, that identifies and discards noisy samples, preventing them from corrupting the model’s core cross-modal learning. Extensive experiments validate AimKP’s effectiveness in multimodal keyphrase generation and its robustness across different scenarios.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务定义**：多模态关键词生成（MKP）旨在从配对的图像-文本输入中提取一组简洁、语义丰富的关键词，用于多媒体数据的结构化理解、索引和检索。
- **核心问题**：尽管多模态大语言模型（MLLMs）通过海量预训练在跨模态理解上表现优异，但它们在处理真实世界的噪声、不完整或错配的多模态数据时，存在**模态偏差**（如文本偏好）和**细粒度模态内特征提取不足**的问题。这导致模型在单模态场景下性能急剧下降，尤其是在图像缺失时，其表现甚至落后于专用单模态模型8%。
- **研究动机**：现有MLLMs优先学习跨模态关联，牺牲了模态内语义的精细理解；而MKP任务要求模型既能锚定特定模态的关键线索，又能进行跨模态融合。直接部署MLLMs无法满足这一需求，因此需要设计专门框架增强其模态内理解能力。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **框架名称**：AimKP（Augmenting intra-modal understanding in MLLMs for Robust MKP）。
- **核心思想**：在保持MLLMs跨模态对齐能力的同时，显式增强其模态内语义学习。通过两种创新机制实现：
  - **渐进式模态掩码（Progressive Modality Masking）**：在训练过程中逐步增加对图像或文本模态的掩码程度，迫使模型从受损输入中提取细粒度特征。掩码策略基于步长γ：图像使用2D网格掩码（保留率1/γ²），文本使用1D固定间隔掩码（保留率1/γ）。γ从2开始每轮翻倍，遵循课程学习原则。
  - **基于梯度的过滤（Gradient-Based Filtering）**：计算原始样本损失梯度与掩码样本损失梯度的余弦相似度，作为掩码样本信息量的代理。相似度高于阈值τ的样本保留为辅助损失，否则丢弃，并动态调整下一轮的掩码强度（相似度高则加倍γ，低则减半）。
- **训练目标**：总损失L_total = 原始损失L + λ_V·L̃_V + λ_T·L̃_T，其中L̃_V和L̃_T分别为图像掩码和文本掩码下的辅助损失，λ为0-1开关（由梯度相似度决定）。原始损失为标准的交叉熵损失。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：使用CMKP数据集（Wang et al., 2020），包含53,701条英文推文（图片-文本对），用户生成的标签作为关键词，按8:1:1划分训练/验证/测试集。
- **评估指标**：F1@K（Macro-F1 on top-K predictions）和MAP@K（mean average precision on top-K），K取1、3、5。
- **对比方法**：
  - **传统MKP模型**：CO-ATT、FLAVA、M3H-ATT、MM-MKP、BART-large、CopyBART。
  - **MLLMs标准微调**：LLaVA-1.5-7B、Qwen2-VL-7B。
  - **单模态专家**：仅用图像或仅用文本微调的LLaVA（作为上限参考）。
- **实验场景**：三种输入设置——完整多模态、仅文本、仅图像。

## 4. 资源与算力

- 文中明确说明：训练在**4块NVIDIA A6000 GPU**上进行，学习率2e-4，总batch size 64，采用LoRA微调。训练时长未具体说明，但提及“先训练一个epoch正常数据，然后应用渐进式掩码和梯度过滤”。使用Adam优化器。

## 5. 实验数量与充分性

- **主要实验**：在主测试集上进行全指标对比（表1），涵盖图像/文本/多模态三种输入，对比了10+种方法。
- **消融实验**（表2）：验证了双模态掩码、梯度过滤、渐进式 vs 固定掩码等组件的重要性。
- **案例研究**（图5）：4个具体案例展示生成质量差异。
- **充分性评估**：实验设计较为全面，包含了不同架构（LLaVA、Qwen2-VL）、不同输入条件、不同模型规模（7B级），并进行了3次随机种子平均。消融实验覆盖了所有关键组件。但仅在单一数据集（CMKP）上验证，未在更多MKP数据集或跨领域数据上测试，可能限制泛化性结论。此外，无计算成本或训练时间的详细对比。

## 6. 论文的主要结论与发现

- **MLLMs在MKP上的潜力**：标准微调的MLLMs（如LLaVA-1.5）在完整多模态输入上大幅超越传统模型（F1@1提升10.16%），但单模态场景表现差，存在模态内理解缺陷。
- **AimKP的有效性**：所提框架在LLaVA和Qwen2-VL上均带来一致提升，多模态F1@1提升1.1-1.58%，MAP@5提升1.11-1.89%。在单模态场景下，图像输入MAP@5从37.68%提升至41.94%，文本输入从53.92%提升至55.45%，缩小了与单模态专家的差距。
- **组件贡献**：双模态掩码、梯度过滤和渐进式策略均不可或缺。固定掩码或去除过滤都会导致性能下降。
- **鲁棒性**：AimKP不仅提升一般性能，还增强了模型在噪声或模态缺失场景下的鲁棒性。

## 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次系统地将MLLMs适配到MKP任务，通过渐进式掩码+梯度过滤的组合，同时解决模态偏差和噪声样本问题，设计精巧。
- **实验设计严谨**：考虑了三种输入设置（多模态/仅文本/仅图像）和单模态专家上限，清晰揭示了MLLMs的短板和AimKP的改进。
- **跨架构验证**：在两种代表性MLLMs（LLaVA、Qwen2-VL）上验证了方法的泛化性。
- **辅助分析**：提供了梯度相似度与困惑度增加之间的负相关关系（图3），为梯度过滤提供了经验证据。
- **消融实验充分**：系统去除了每个组件，并比较了固定掩码策略，证明了渐进式设计的必要性。

## 8. 不足与局限

- **数据集单一**：仅在CMKP（Twitter推文）上验证，缺乏在其他领域（如新闻、电商）或多语言数据上的测试，结论的泛化性有限。
- **计算资源未详细报告**：未说明训练总时长或FLOPs，难以评估方法的实际部署成本。
- **评估指标局限性**：F1@K在生成少于K个关键词时用空标签填充，可能低估了模型性能；且仅使用Macro-F1，未报告Micro-F1或BLEU等。
- **未与更多SOTA MLLMs对比**：仅对比了LLaVA和Qwen2-VL，未包含GPT-4V、Gemini等更强模型（可能受限于开源或计算资源）。
- **阈值选择依赖经验**：梯度过滤的阈值τ（图像0.4，文本0.1）通过验证集调试，未讨论其在不同数据上的敏感性。
- **未来方向提及不足**：论文指出未来可扩展到其他多模态任务，但未讨论当前方法在更复杂场景（如视频、音频）或更大模型上的潜在挑战。

（完）
