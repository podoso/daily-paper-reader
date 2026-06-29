---
title: "HFR-MKGC: Hierarchical Fusion Reasoning with MLLMs for Multi-modal Knowledge Graph Completion"
title_zh: HFR-MKGC：基于层次融合推理和多模态大语言模型的多模态知识图谱补全
authors: "Di Wang, Junping Du, Zhe Xue, Meiyu Liang, Guanhua Ye, Yingxia Shao, Haisheng Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38613/42575"
tags: ["query:multimodal"]
score: 5.0
evidence: 使用MLLM和层次融合的多模态知识图谱补全
tldr: 多模态知识图谱补全面临模态对齐不一致和推理深度不足问题。本文提出HFR-MKGC，通过关系引导的层次模态融合模块进行细粒度视觉内融合和跨模态集成，并利用微调的MLLM进行推理。实验表明该方法在多个MMKGC基准上优于现有方法，生成更准确的实体预测。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38613/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38613/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1831, \"height\": 768, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38613/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 1031, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38613/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 882, \"height\": 514, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38613/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 873, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38613/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 655, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38613/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 785, \"height\": 393, \"label\": \"Table\"}]"
motivation: 现有方法模态对齐不一致、推理深度有限。
method: 提出关系引导的层次融合模块和微调MLLM进行推理。
result: 在多个多模态知识图谱补全基准上取得最优。
conclusion: 层次融合结合MLLM显著增强多模态知识图谱补全性能。
---

## Abstract
Multi-modal knowledge graph completion (MMKGC) aims to infer missing entities of triples by leveraging heterogeneous information in knowledge graph (KG). However, existing approaches often struggle with inconsistent modality alignment, limited reasoning depth, and insufficient negative sample quality. In this work, we propose HFR-MKGC, a novel framework that integrates hierarchical modal fusion and Multimodal Large Language Model (MLLM) reasoning for robust and expressive MMKGC. Specifically, we introduce a relation-guided hierarchical modal fusion module, which conducts fine-grained intra-visual fusion and relation-guided cross-modal integration to yield rich entity representations. HFR-MKGC employs a fine-tuned MLLM to perform instruction-based triple reasoning, producing candidate entities for completion. Then, it constructs hard negative samples through textual perturbation by MLLM and visual feature augmentation with rotation and noise. HFR-MKGC optimizes the model via adversarial training. Extensive experiments on three MMKGC benchmarks demonstrate that our method outperforms state-of-the-art methods, validating its effectiveness in MMKGC.

---

## 论文详细总结（自动生成）

# HFR-MKGC 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：多模态知识图谱补全（MMKGC）旨在利用文本、图像等多模态信息推断知识图谱中缺失的三元组。然而，现有方法存在三个关键挑战：（1）模态对齐不一致，简单拼接或平均融合忽略不同关系下各模态重要性的差异；（2）推理深度有限，尤其是基于大语言模型（LLM）的方法仅聚焦文本和结构模态，未充分利用视觉语义且缺乏动态适应；（3）负样本质量不足，难以训练出鲁棒的判别模型。
- **整体含义**：本文提出 HFR-MKGC 框架，通过关系引导的层次模态融合与多模态大语言模型（MLLM）推理，实现更精确、更具适应性的多模态知识图谱补全，从而提升预测准确性和模型鲁棒性。

## 2. 论文提出的方法论

### 核心思想
- **两阶段层次融合**：先进行细粒度视觉内融合（利用 MLLM 生成的图像描述），再进行关系引导的跨模态融合（根据当前关系自适应加权文本、视觉、结构模态）。
- **MLLM 增强推理与评分**：微调 LLaVA 模型，为每个不完整三元组生成结构化指令并推理出候选实体；通过门控机制将 MLLM 的输出与多模态联合表征融合，并采用 RotatE 评分函数计算三元组得分。
- **多模态负样本优化**：通过 MLLM 进行文本扰动、对视觉特征进行旋转与噪声注入生成硬负样本，结合对抗训练增强模型判别力。

### 关键技术细节
1. **模态编码**：使用 CLIP 编码图像，BERT 编码文本；每个实体生成结构嵌入 e<sub>S</sub>、视觉嵌入 e<sub>I</sub>、文本嵌入 e<sub>T</sub>。
2. **阶段1：视觉内融合**：利用 LLaVA 生成图像描述，编码为 e<sub>Ic</sub>；通过相似度门控融合 e<sub>Ic</sub> 和原始视觉嵌入 e<sub>Iv</sub>：  
   e<sub>I</sub> = σ(⟨e<sub>Iv</sub>, e<sub>Ic</sub>⟩)·e<sub>Ic</sub> + (1−σ(⟨e<sub>Iv</sub>, e<sub>Ic</sub>⟩))·e<sub>Iv</sub>。
3. **阶段2：关系引导跨模态融合**：计算模态间相似矩阵 A<sub>i,j</sub>，基于关系嵌入 r 和模态内相似度计算每个模态的交互得分 α<sub>m</sub>，再通过 softmax 得到权重 w<sub>m</sub>，最终联合嵌入 H<sub>joint</sub> = Σ w<sub>m</sub>·e<sub>m</sub>。
4. **MLLM 推理与门控融合**：构造固定指令和可变指令（含头实体图像、文本、邻居、关系），用 LoRA 微调 LLaVA 生成候选尾实体 t̂<sub>MLLM</sub>；将 t̂<sub>MLLM</sub> 编码为 T<sub>MLLM</sub>，通过两层神经网络生成门控向量 g，插值融合 T<sub>joint</sub> 和 T<sub>MLLM} 得到 ˜T<sub>joint</sub>；采用 RotatE 评分函数（复空间旋转）计算得分。
5. **多模态负样本生成与对抗训练**：
   - 文本扰动：MLLM 生成语义等价但句法不同的描述。
   - 视觉增强：旋转矩阵 R（QR 分解获得）+ 高斯噪声，扰动强度 λ 随 epoch 线性增加。
   - 对抗损失：使用加权的 sigmoid 损失 L<sub>kgc</sub> 和生成器损失 L<sub>g</sub>（鼓励生成更难区分的负样本），并加入梯度惩罚稳定训练。

## 3. 实验设计

- **数据集**：三个广泛使用的 MMKGC 基准：DB15K（12,842 实体，279 关系）、MKG-W（15,000 实体，169 关系）、MKG-Y（15,000 实体，28 关系）。每个实体均提供文本描述和图像。
- **评价指标**：MRR、Hits@1/3/10（链接预测任务）。
- **对比方法**：14 个基线，分三类：
  - 单模态 KGC：TransE、RotatE、DistMult、ComplEx。
  - 多模态 KGC：IKRL、RSME、MYGO、NativeE、AdaMF-MAT、SNAG、DHNS、APKGC。
  - MLLM 推理模型：LLaMA2-7B（仅文本+结构）、LLaVA-1.5-7B（含图像输入）。
- **实验设置**：标准 train/valid/test 划分；由于部分基线未公开完整数据或代码，作者在统一多模态设置下复现了代表性基线，使用相同的视觉和文本编码器，确保公平比较。

## 4. 资源与算力

- **硬件**：2 块 NVIDIA RTX A6000 GPU（共 48GB），操作系统 Ubuntu。
- **训练配置**：训练 250 epochs，嵌入维度选自 {128, 256, 512}，负样本数选自 {32, 64, 128}，学习率选自 {1e−5, 1e−4, 1e−3}，batch size 选自 {128, 256, 1024}，优化器 Adam。
- **未明确说明**：总训练时间、单次实验耗时、微调 LLaVA 所需额外资源等未提及。

## 5. 实验数量与充分性

- **实验数量**：
  - 主实验：在 3 个数据集上对比 14 个基线，每个指标（MRR、Hits@1/3/10）均有报告。
  - 消融实验：在 MKG-W 上进行了 8 组设置：移除关系引导层次融合（RHF）、移除 MLLM 增强推理（MER）、移除文本/图像扰动（PTI）、移除对抗训练（MNO），以及分别移除结构/文本/视觉/MLLM 视觉语义模态。
  - 超参数敏感性分析：在 MKG-W 上验证了不同嵌入维度和负样本数量对 MRR/Hits@1/3/10 的影响。
  - 案例研究：选取具体三元组展示关系引导融合的效果。
- **充分性与公平性**：
  - 实验设计较为全面，覆盖了主要模块和模态的贡献验证。
  - 对基线进行统一复现（相同编码器）保证了公平性。
  - 超参数分析揭示了模型对不同设置的敏感度，有助于理解模型特性。
  - 不足：消融实验仅在 MKG-W 上进行，未在其他两个数据集重复验证；未报告统计显著性检验（如多次运行的标准差）；未讨论不同数据集特性差异导致的性能差异。

## 6. 论文的主要结论与发现

- HFR-MKGC 在所有三个数据集上的 MRR、Hits@1/3/10 均达到最优，显著超越现有 SOTA（如 NativeE 等）。
- 在 MKG-W 上，MRR 提升 1.83 个百分点（38.62% vs 36.79%），Hits@1 提升 2.01 个百分点。
- MLLM 推理模块（MER）贡献最大（MRR 从 33.52 提升到 38.62），关系引导融合（RHF）次之；结构模态（S）对性能影响最大。
- 视觉描述（VT）能提供互补信息，但单独使用效果不如多模态联合。
- 嵌入维度和负样本数量需要协调调整：高维度需搭配更多负样本，中等维度搭配中等负样本效果最佳。
- 纯 LLM 方法（LLaMA、LLaVA）性能远弱于联合训练方法，表明结构化评分和融合机制的必要性。

## 7. 优点

- **创新性**：首次将关系引导的层次融合与 MLLM 推理结合，实现了细粒度视觉语义融合和动态跨模态加权。
- **鲁棒性增强**：通过 MLLM 文本扰动和视觉旋转噪声生成硬负样本，结合对抗训练，提升了判别力。
- **充分消融**：系统分析了每个模块和每种模态的贡献，验证了设计的合理性。
- **公平比较**：统一复现基线，使用相同编码器，避免不公平优势。
- **可解释性**：案例研究直观展示了关系引导融合如何抑制噪声模态、突出关键信息。

## 8. 不足与局限

- **实验覆盖**：消融实验仅在 MKG-W 上完成，未在 DB15K 和 MKG-Y 上验证模块泛化性；超参数敏感性也只在一个数据集上分析。
- **统计验证缺失**：未报告多次运行的平均值和标准差，无法判断性能提升的统计显著性。
- **计算资源未明确**：训练总时间、MLLM 微调开销、推理效率等未给出，限制了实际部署评估。
- **潜在偏差**：三个数据集均源自特定领域（通用知识图谱），未在工业级、稀疏或噪声较大的多模态 KG 上测试；MLLM 依赖指令构建，可能对提示设计敏感。
- **局限**：框架复杂度较高，包含 MLLM 微调、多模态融合、对抗训练等组件，训练和推理成本可能高于轻量方法；未讨论扩展到更多模态（如音频、视频）的可行性。

（完）
