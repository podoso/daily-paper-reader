---
title: "ModalSyncSum: Synchronizing Image and Text for Reliable Summary Generation"
title_zh: ModalSyncSum：同步图像和文本以生成可靠摘要
authors: "Xuanqi Chen, Ziying Rong, Xinfeng Liao, Yiqian Wu, Bowei Zhang, Pengfei Fu, Shengyi Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40282/44243"
tags: ["query:ie"]
score: 4.0
evidence: 使用命名实体引导提高事实准确性
tldr: 针对多模态大模型在摘要任务中存在的幻觉和视觉-文本对齐弱的问题，提出ModalSyncSum统一框架。它通过图像感知信息提取、基于问答的描述验证和命名实体引导的细化来增强语义一致性和视觉忠实度。实验表明该方法能有效生成可靠的图文摘要。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40282/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 859, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40282/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1829, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40282/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 863, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40282/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 859, \"height\": 426, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40282/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1844, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40282/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 569, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40282/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40282/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 879, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40282/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 479, \"label\": \"Table\"}]"
motivation: 多模态大模型在摘要任务中常出现幻觉和视觉-文本弱对齐问题。
method: 提出包含图像感知提取、QA验证和命名实体引导细化的统一框架。
result: 该方法在MSMO任务上提升了语义一致性和视觉忠实度。
conclusion: 通过多阶段对齐和验证有效减少幻觉，提升摘要可靠性。
---

## Abstract
Multimodal summarization with multimodal output (MSMO) aims to generate coherent textual summaries while selecting the most semantically relevant images to enhance expressiveness. Despite the advancements of large multimodal models like GPT-4o, LLaMA-3, and Grok-3, these models often exhibit hallucination and weak visual-text alignment when applied to MSMO tasks. To address these challenges, we propose ModalSyncSum, a unified framework that enhances semantic consistency and visual faithfulness.    It incorporates image-aware information extraction to mitigate visual-text misalignment, QA-based description verification to detect and correct hallucinated image descriptions, and named entity-guided refinement to ensure factual accuracy and entity alignment across modalities.   Furthermore, we introduce a new evaluation metric M3AS, which jointly considers image content coverage, text-image alignment, and summary consistency, filling the gap in evaluating multimodal summary quality. Experimental results show that our model outperforms prompt-based baselines across multiple datasets, achieving significant gains on ROUGE, BLEU, and BERTScore, with BLEU improving by 21.95%.  In human evaluation, M3AS exhibits stronger correlation with human judgments in consistency, image-summary relevance, and focus, surpassing existing automatic metrics.

---

## 论文详细总结（自动生成）

以下是基于论文《ModalSyncSum: Synchronizing Image and Text for Reliable Summary Generation》的详细中文总结。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：多模态大模型（如 GPT-4o、GLM-4v、Grok-3）在多模态摘要生成（MSMO）任务中常出现**幻觉**（如描述中颜色错误、身份误解）和**视觉-文本弱对齐**（生成文本未能忠实反映图像内容）。
- **背景**：现有摘要模型多关注文本，对视觉信息利用不足；传统评估指标（ROUGE、BLEU）仅衡量词汇重叠，无法评估跨模态一致性；缺乏专门针对多模态摘要质量的评估方法。
- **目标**：提出一个统一框架，不微调大模型，仅通过多阶段对齐与验证，提高摘要的语义一致性和视觉忠实度；同时设计能同时评估图像覆盖、图文对齐和跨模态一致性的新指标。

## 2. 论文提出的方法论

### 核心思想
> 将多模态摘要任务分解为 **图像描述生成 → 描述验证 → 摘要生成与校验** 三阶段，通过提取图像感知文本、QA 校验和命名实体引导的迭代修正，实现可靠的图文同步。

### 关键技术细节

#### 阶段一：图像感知信息提取（Image-aware Information Extraction）
- 使用预训练 CLIP 模型计算每张图像 Iⱼ 与新闻文章各句子 sᵢ 的余弦相似度：
  - `sim(sᵢ, Iⱼ) = v_{sᵢ}·v_{Iⱼ} / (|v_{sᵢ}| |v_{Iⱼ}|)`
- 设置阈值 τ₁，选取相似度 ≥ τ₁ 的句子作为图像相关参考句子集合 Sⱼ。
- 将 Sⱼ 输入大型视觉语言模型（LVLM）生成图像描述 dⱼ。

#### 阶段二：基于 QA 的描述验证（QA-based Description Verification）
- 为每张图像 Iⱼ 生成多个候选描述 Dⱼ。
- **CLIP 过滤**：保留与图像余弦相似度 ≥ τ₂ 的描述 D^{CLIP}ⱼ。
- **BLIP VQA 校验**：对每个保留描述构造细粒度视觉问题 Qᵢ（如“人物衣服颜色”），使用 BLIP 回答；保留描述与答案语义一致的描述 D^{Final}ⱼ。
- **聚合**：将高质量描述合并为最终描述 d*ⱼ。

#### 阶段三：摘要生成与一致性校验（Summary Generation & Consistency Verification）
- 将图像描述嵌入文章：将 d*ⱼ 插入到与其语义最相似的句子之后，得到增强文章 A_{mod}。
- 利用 LLM 基于 A_{mod} 生成初始摘要 y。
- **命名实体引导修订**：
  - 用 NER 模型从 y 提取实体集 E。
  - 自动生成实体相关问题 Q_E，并分别从 y 和原始文章 A 获取答案 a_yᵢ、a_Aᵢ。
  - 若任意答案不一致 (`Consis(q_Eᵢ)=False`)，则用 LLM 根据原始答案修订摘要，迭代至所有实体一致。

#### 提出的评估指标 M³AS (Multimodal Triple-factor Assessment Score)
由三个子分数加权求和（α=0.25, β=0.25, γ=0.5）：
- **Score_img_info** = √(Img_coverage · Img_density) 衡量图像信息覆盖与密度。
- **Score_img&sum** = √(sim(d*, y) · sim(I, y)) 度量图像与摘要的语义一致性。
- **Score_consist** = Σ(rᵢ·cᵢ·mᵢ/Μ·δ) / Σcᵢ  综合语义正确性、重要性和跨模态对齐。

## 3. 实验设计

### 数据集
- **MSMO**：英文，来自 Daily Mail，含人工写摘要和关联图像。
- **M3LS**：多语言多模态摘要数据集。
- **E-Liputan**：印尼语多模态摘要数据集。
- 每个数据集随机采样 5,000 个实例（M3LS 按语言分层抽样）。

### 对比基准（Baselines）
- **传统多模态方法**：Vision-GPLM, VG-GPLMs, Va-SOGM（需微调）。
- **大模型直接提示（LVLM + Prompt）**：GPT-4o, GLM-4v, Grok-3, Gmini, Doubao（直接输入图像+文本生成）。
- **本文方法 ModalSyncSum**：基于上述 LVLM 作为生成器，但使用提出的三阶段框架。

### 评估指标
- **自动指标**：ROUGE-1/2/L, BLEU-1/2, BERTScore, 以及 M³AS。
- **人工评估**：15 名研究生从 4 个维度（一致性、流畅性、焦点与覆盖、图像-摘要相关性）对 500 个样本进行 0–4 评分。

## 4. 资源与算力

- 论文**未明确说明**训练所消耗的 GPU 型号、数量或时长。
- 方法特点：**不微调大模型**，仅使用预训练模型（CLIP、BLIP、BERT、LVLM）进行推理和验证，因此算力需求较低，主要开销来自多次调用大模型（生成描述、QA 回答、摘要生成与修订）。
- 适用于现有大模型 API 或本地部署的推理环境。

## 5. 实验数量与充分性

### 实验组数
- **主实验**：在 3 个数据集上与 8+ 个基线模型对比（表 1、表 2）。
- **消融实验**（表 3）：移除图像一致性模块（w/o ImgC）、移除摘要一致性模块（w/o SumC）、直接图像输入对比。
- **超参数搜索**（表 5）：对 τ₁ (0.1–0.5) 和 τ₂ (0.1–0.5) 进行组合调优。
- **M³AS 扰动分析**（表 4）：在 4 种扰动（修改图像描述、替换无关图像、修改摘要细节、无扰动）下验证各子分数的敏感性。
- **人类评估**（图 3）：与 5 个基线模型在 4 个维度上的评分对比。
- **指标相关性分析**（图 4）：M³AS 与人类评分在 4 个维度上的相关系数。

### 充分性评价
- **充分**：覆盖多数据集（英、多语、印尼）、多模型（传统+大模型）、完整消融、参数分析和人类评估。
- **客观公平**：所有实验均报告多次运行的均值和标准差；人类评估采用双盲评分并提前培训评分者；指标相关性使用 Pearson 相关系数。

## 6. 论文的主要结论与发现

1. **ModalSyncSum 显著优于直接提示大模型**：在 MSMO 上，相比 GPT-4o 直接提示，BLEU-2 提升 25.8%，BERTScore 提升 7.8%，M³AS 提升 23.5%。
2. **传统多模态方法在 M³AS 上远低于本方法**：表明现有方法在跨模态对齐和一致性上不足。
3. **消融实验证明两个验证模块（ImgC 和 SumC）均至关重要**：移除任一模块都会导致 BERTScore 和 M³AS 下降。
4. **M³AS 与人类判断高度相关**：在一致性(0.96)、图像-摘要相关性(0.92)和焦点覆盖(0.87)上显著优于 ROUGE/BLEU/BERTScore；流畅性相关稍低(0.46)。
5. **阈值选择影响性能**：τ₁=0.3, τ₂=0.4 达到最佳平衡。

## 7. 优点

- **无需微调大模型**：框架可即插即用于任何 LVLM，降低计算和部署成本。
- **多阶段验证消除幻觉**：CLIP+BLIP 二阶段验证图像描述，NER+QA 验证摘要事实，形成闭环纠错。
- **全面评估指标 M³AS**：首次同时考虑图像覆盖、图文对齐和跨模态一致性，比现有指标更贴合多模态摘要质量。
- **跨语言泛化性**：即使在低资源语言（印尼语）上，M³AS 仍显著优于传统方法。
- **实验设计完整**：覆盖多数据集、多模型、消融、参数分析和人类评估，结果可信度高。

## 8. 不足与局限

- **低资源语言性能受限**：在 M3LS（多语）和 E-Liputan（印尼语）上，ROUGE/BLEU 分数低于传统方法，说明预训练模型在多语言理解上仍有不足。
- **流畅性评估相关低**：M³AS 与人工评分的流畅性相关系数仅 0.46，是该指标的主要弱点。
- **依赖预训练模型能力**：图像描述和 QA 验证依赖于 CLIP/BLIP 的准确性，若它们本身存在偏见或错误，会影响整体结果。
- **阈值依赖经验**：τ₁、τ₂ 需人工调节，不同数据集可能需重新搜索，未提出自适应机制。
- **未探索端到端训练方案**：框架基于零样本推理，可能无法完全发挥大模型潜力（如通过微调进一步提升）。
- **算力成本未量化**：虽然不微调，但多次调用大模型（生成描述、QA、摘要修正）在 API 成本或推理延迟上可能较高。

（完）
