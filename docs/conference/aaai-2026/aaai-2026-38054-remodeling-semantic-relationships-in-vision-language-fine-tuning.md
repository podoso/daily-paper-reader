---
title: Remodeling Semantic Relationships in Vision-Language Fine-Tuning
title_zh: 重塑视觉语言微调中的语义关系
authors: "Xiangyang Wu, Liu Liu, Baosheng Yu, Jiayan Qiu, Zhenwei Shi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38054/42016"
tags: ["query:multimodal"]
score: 8.0
evidence: 通过语义关系重塑进行视觉语言微调
tldr: 针对现有微调方法忽略图像中语义关系的问题，提出一种基于语义关系重塑的多模态对齐融合方法，通过多级视觉特征提取和语义分组投影，有效提升了视觉语言模型在下游任务中的性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38054/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 842, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38054/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1740, \"height\": 971, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38054/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 880, \"height\": 736, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38054/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1701, \"height\": 829, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38054/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 853, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38054/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1619, \"height\": 723, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38054/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 348, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38054/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 280, \"label\": \"Table\"}]"
motivation: 现有方法忽略图像中的语义关系信息，导致对齐性能次优。
method: 提取多级语义特征，并将视觉特征投影到关系语义分组中。
result: 在多个视觉语言任务上显著提升对齐和融合性能。
conclusion: 该工作揭示了语义关系在视觉语言微调中的关键作用。
---

## Abstract
Vision-language fine-tuning has emerged as an efficient paradigm for constructing multimodal foundation models. While textual context often highlights semantic relationships within an image, existing fine-tuning methods typically overlook this information when aligning vision and language, thus leading to suboptimal performance. Toward solving this problem, we propose a method that can improve multimodal alignment and fusion based on both semantics and relationships.Specifically, we first extract multilevel semantic features from different vision encoder to capture more visual cues of the relationships. Then, we learn to project the vision features to group related semantics, among which are more likely to have relationships. Finally, we fuse the visual features with the textual by using inheritable cross-attention, where we globally remove the redundant visual relationships by discarding visual-language feature pairs with low correlation. We evaluate our proposed method on eight foundation models and two downstream tasks, visual question answering and image captioning, and show that it  outperforms all existing methods.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有的视觉语言（VL）微调方法在跨模态对齐时，未能充分利用图像内隐含的**语义关系**（如“女孩抱着猫”中的动作关系“抱”）。这导致视觉编码器输出的特征偏向于分类语义，而缺乏关系建模能力。
- **背景**：VL模型通常由预训练视觉编码器（如CLIP）和大语言模型组成，通过参数高效微调（PEFT）进行对齐与融合。但现有方法（如简单的MLP投影器、朴素交叉注意力）难以捕捉复杂的跨语义关系。
- **动机**：提升模型对图像中语义关系的理解，从而改善多模态对齐与融合的最终性能。

## 2. 方法论：核心思想与关键技术细节
**整体框架**：LSRM（Learnable Semantic Relationship Method）包含三个核心模块。

### 2.1 多级信息融合（Multilevel Information Fusion）
- **思想**：视觉编码器中间层保留关系信息，最终层保留高级语义。通过融合两者，平衡局部关系与全局语义。
- **实现**：从编码器中间层（如第12层）和最终层分别提取特征，各自通过独立的语义关系投影器（SRProj），然后取平均：
  \[
  X_v = \frac{1}{2}\left[ \text{SRProj}_m(X_mv) + \text{SRProj}_f(X_fv) \right]
  \]
  其中 \(X_mv\) 为中间层输出，\(X_fv\) 为最终层输出。

### 2.2 语义关系投影器（Semantic Relationship Projector, SRProj）
- **思想**：传统投影器（降维-激活-升维）的降维矩阵隐含了语义分组，但缺乏对关键语义组的动态加权。通过引入可学习对角矩阵 Λ，自适应增强重要关系组。
- **公式**：
  \[
  \text{SRProj}(X_v) = (\Lambda \cdot \text{SiLU}(X_v W_1)) W_2
  \]
  其中 \(W_1 \in \mathbb{R}^{d_1 \times d_h}\) 降维，\(W_2 \in \mathbb{R}^{d_h \times d_2}\) 升维，\(\Lambda = \text{diag}(\lambda_1, \dots, \lambda_{d_h})\) 为可学习对角矩阵。

### 2.3 可继承交叉注意力（Inheritable Cross-Attention）
- **思想**：在多Transformer层的交叉注意力中，持续抑制低相关性的视觉-文本token对，同时保持高相关性连接。通过层间共享的继承权重矩阵 **M** 实现渐进式衰减。
- **流程**：
  1. 初始化 **M** 为全1矩阵。
  2. 每层计算注意力得分 \(\alpha = \text{SiLU}(QK^T)\)。
  3. 对每个文本token（每行），找出最低 \(\delta\%\) 的得分，其对应位置 **M** 乘以衰减因子 \(\lambda\)。
  4. 最终输出：\(\text{Cross-Attn} = (\mathbf{M} \odot \alpha) V\)。
- **延迟激活**：设置超参数 `shift epoch`，在训练若干epoch后才启用该机制，确保模型首先具备基础注意力能力。

## 3. 实验设计
- **数据集与任务**：
  - 视觉问答：ScienceQA（官方训练/测试集）。
  - 图像描述：COCO Captions（Karpathy分割）。
- **基准（Benchmark）**：
  - ScienceQA：按Subject（NAT/SOC/LAN）、Context（TXT/IMG/NO）、Grade（G1-6/G7-12）等维度报告平均准确率。
  - COCO：BLEU-4和CIDEr得分。
- **对比方法**：
  - 零样本/少样本：GPT-4、Human。
  - 全训练：UnifiedQA、MM-CoT、LLaVA、CoMD。
  - PEFT方法：PILL、LLaVA-LoRA、LLaMA-Adapter、MemVP（SOTA基线）。
- **模型组合**：
  - 视觉编码器：固定使用CLIP ViT-L/14。
  - 语言模型：8种不同规模（LLaMA-7B/13B、LLaMA2-7B/13B、LLaMA3-1B/3B/8B、Vicuna-7B）。
- **训练设置**：
  - ScienceQA：20 epoch，global batch size 32，初始学习率 9e-3（cosine衰减），投影器隐藏维度64，总可训练参数量与MemVP保持一致（3.9M/5.5M等）。
  - COCO Captions：类似设置，使用LLaMA-13B。

## 4. 资源与算力
- 论文提及在 8×A800 GPU 上进行训练和推理测量（表4给出了每batch时间：训练0.29s/batch（7B）、0.48s/batch（13B））。
- **未详细说明**：总训练时长、GPU内存消耗等。资源描述较简略，仅给出相对效率对比。

## 5. 实验数量与充分性
- **实验数量**：
  - **主要实验**：ScienceQA上8个语言模型（表1、表2），COCO Captions上1个模型（表3）。
  - **消融实验**：表5逐步验证三个模块的有效性（基线92.78% → +多级融合93.47% → +语义投影93.75% → +可继承交叉注意力93.94%）。
  - **超参数分析**：附录中包含超参数探讨（论文提及但正文仅简要说明）。
  - **定性分析**：图3展示了继承权重矩阵M的可视化效果，验证其对低相关性token的抑制。
- **充分性评价**：
  - **优点**：在多个模型家族（LLaMA1/2/3, Vicuna）上验证，跨任务（VQA、Caption）一致提升，实验设计较为全面。
  - **局限性**：仅使用两个下游任务，缺少更广泛的场景（如视觉推理、视觉定位、多模态对话等）；COCO Caption任务上对比方法较少（仅PEFT方法，无全参数方法对比）；消融实验较为简单（仅验证有无模块，未深入分析每个模块的变体）。

## 6. 主要结论与发现
- LSRM通过多级信息融合、语义关系投影器、可继承交叉注意力，显著提升了视觉语言微调中对语义关系的建模能力。
- 在ScienceQA上，LSRM在LLaMA-7B上达到93.94%准确率，超越SOTA MemVP 0.87%；在LLaMA-13B上达到94.41%，超越0.63%；在LLaMA3-1B上提升最大（+0.99%）。
- 在COCO Caption上，BLEU-4和CIDEr分别达到37.3和123.9，优于MemVP。
- 定性可视化表明，可继承交叉注意力能自动抑制低相关历史信息并扩大全局语义范围，但部分低权重区域在人类认知中仍具相关性，提示模型与人类感知存在差异。

## 7. 优点
- **方法创新性**：首次系统地将语义关系建模融入视觉语言微调，三个组件均有明确理论动机且相互协同。
- **高效性**：仅增加少量可学习参数（3.9M~5.5M），在参数量与SOTA持平的情况下取得明显提升。
- **泛化性**：在8种不同规模的语言模型上均一致优于基线，证明方法对模型规模不敏感。
- **可解释性**：通过可视化继承权重矩阵M，直观展示了注意力抑制机理，有助于理解模型行为。

## 8. 不足与局限
- **任务覆盖有限**：仅在VQA和Caption上验证，缺少在视觉定位、多模态推理、视频理解等任务上的评估。
- **对比基线有限**：COCO Caption实验仅对比了少量PEFT方法，未与全参数微调或更强大的预训练模型（如LLaVA-1.5完整版）比较，难以判断绝对性能差距。
- **超参数敏感**：可继承交叉注意力需要手动设置shift epoch（14/20）、δ（0.3）、λ（0.85），缺乏自适应机制；不同任务可能需要调参。
- **模型认知偏差**：可视化显示部分低权重区域在人类看来仍有相关性，暗示模型注意力可能存在偏差，可能影响对细粒度关系的理解。
- **资源细节缺失**：未报告完整训练时间、GPU内存占用、能耗等，不利于复现和效率比较。

（完）
