---
title: Reconstruction Alignment Improves Unified Multimodal Models
title_zh: 重建对齐改进统一多模态模型
authors: "Ji Xie, Trevor Darrell, Luke Zettlemoyer, XuDong Wang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=ppQWp8yrm7"
tags: ["query:multimodal"]
score: 6.0
evidence: 通过重建对齐改进统一多模态模型
tldr: 统一多模态模型的理解和生成对齐不充分。本文提出RecA，利用视觉理解编码器嵌入作为密集提示，通过自监督重建损失优化生成，无需文本标注。实验表明RecA显著提升图像生成质量和一致性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 724, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1434, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1409, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1444, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1450, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1449, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 490, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1445, \"height\": 1092, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1446, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 780, \"height\": 192, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1379, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 157, \"height\": 299, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 169, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 642, \"height\": 354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1429, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 418, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1436, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1443, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1420, \"height\": 861, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1433, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1424, \"height\": 932, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1444, \"height\": 1189, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1359, \"height\": 1951, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1103, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1103, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1102, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1104, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1098, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1104, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 1100, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 1102, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 1103, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 1102, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 1103, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 1307, \"height\": 984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-037.webp\", \"caption\": \"\", \"page\": 0, \"index\": 37, \"width\": 1307, \"height\": 984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-038.webp\", \"caption\": \"\", \"page\": 0, \"index\": 38, \"width\": 1309, \"height\": 983, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ppqwp8yrm7/fig-039.webp\", \"caption\": \"\", \"page\": 0, \"index\": 39, \"width\": 1306, \"height\": 985, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1438, \"height\": 568, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1436, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1427, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 923, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 824, \"height\": 134, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 695, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 820, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1414, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1440, \"height\": 893, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1396, \"height\": 701, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1408, \"height\": 628, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1343, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 625, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ppqwp8yrm7/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 632, \"height\": 247, \"label\": \"Table\"}]"
motivation: 统一多模态模型的理解和生成之间存在对齐误差，且依赖稀疏文本。
method: 利用理解嵌入作为提示，通过自监督重建损失重新对齐。
result: 在多个生成任务上图像质量和一致性显著提升。
conclusion: RecA是一种高效的无监督对齐方法，提升统一多模态模型性能。
---

## Abstract
Unified multimodal models (UMMs) unify visual understanding and generation within a single architecture.
However, conventional training relies on image–text pairs (or sequences) whose captions are typically sparse and miss fine-grained visual details, even when they use hundreds of words to describe a simple image. We introduce **Reconstruction Alignment (RecA)**, a resource-efficient post-training method that leverages visual understanding encoder embeddings as dense “text prompts,” providing rich supervision without captions. Concretely, RecA conditions a UMM on its own visual understanding embeddings and optimizes it to reconstruct the input image with a self-supervised reconstruction loss, thereby realigning understanding and generation. Despite its simplicity, RecA is broadly applicable: across autoregressive, masked-autoregressive, and diffusion-based UMMs, it consistently improves generation and editing fidelity. With only 27 GPU-hours, post-training with RecA substantially improves image generation performance on GenEval (0.73 → 0.90) and DPGBench (80.93 → 88.15), while also boosting editing benchmarks (ImgEdit 3.38 → 3.75, GEdit 6.94 → 7.27). Notably, RecA surpasses much larger open-source models and applies broadly across diverse UMM architectures, establishing it as an efficient and general post-training alignment strategy for UMMs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- 统一多模态模型（UMM）旨在一个架构内同时处理视觉理解与图像生成，但其训练依赖图像-文本对，而文本标注（caption）本质上是视觉信息的稀疏表示，即使数百词的描述也会丢失大量细粒度细节（如纹理、布局、颜色属性、空间关系等）。
- 这种稀疏监督导致理解与生成之间的系统性对齐误差：例如，模型可能正确识别“黄色西兰花”，但生成时却倾向于默认绿色（因为训练数据中“西兰花”常伴随绿色属性）。
- 因此，关键问题是如何在不依赖额外标注的情况下，提供更密集的视觉监督，以增强UMM的生成能力并重新对齐理解与生成。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：利用UMM自身的视觉理解编码器（如CLIP、SigLIP）提取的语义嵌入作为“密集文本提示”，代替稀疏caption；然后以自监督重建目标训练模型从这些嵌入中重构原始图像，从而提供丰富的语义级监督。
- **关键技术细节**：
  - **训练流程**（以公式说明）：
    - 标准UMM训练包含文本到图像损失（L_t2i）和图像到文本损失（L_i2t）。
    - RecA将L_t2i替换为重建损失：L_RecA = L( f_θ(concat(t_template, h_v)), I_gt )，其中h_v是视觉理解嵌入，t_template是触发描述的模板（如“详细描述这张图片”）。
    - 总损失：L_total = λ_RecA·L_RecA + λ_i2t·L_i2t。对于共享参数的UMM（如Harmon），保留L_i2t以维持理解能力；对于解耦的架构（如BAGEL、OpenUni），冻结理解组件并仅优化生成部分。
  - **模型结构**：视觉理解编码器通常冻结（除非与生成共享参数），图像通过编码器获得嵌入，与模板文本拼接后送入UMM，输出重建图像。推理时无需额外输入，与标准UMM相同。
  - **输入分辨率**：为鼓励模型关注语义级重建，将输入图像缩放到理解编码器的最小接受分辨率（如224×224），避免模型过度依赖像素级细节。
- **与现有工作的区别**：不同于扩散监督增强（如ViLex）、隐藏状态重建（如ROSS）、表示对齐（如REPA）或重建作为先验（如Lumos），RecA是首个将语义级重建作为UMM原生后训练目标的方法，无需辅助模块或额外文本图像数据。

## 3. 实验设计

- **数据集**：
  - 主要后训练数据：MidjourneyV6（240K高质量开源数据，MIT许可），对于BAGEL使用10K FLUX生成样本（因分布匹配）；同时为保持理解能力，对共享参数模型加入LLaVA Mix-665K。
  - 避免使用GPT-4o蒸馏数据（如BLIP3o-60k）以避免GenEval模板泄漏导致的评估偏置。
- **基准与评估**：
  - 文本到图像生成：GenEval（包含6个子任务）、DPGBench、WISE（知识推理型生成）。
  - 图像编辑：ImgEdit、GEdit-Bench-EN。
  - 视觉理解：MME、POPE、GQA、MMMU、SEED。
- **对比方法**：
  - 生成专用模型：SD3-Medium、FLUX-dev、Playground-v3、DALL-E 3等。
  - 统一多模态模型：Show-o、Harmon、BAGEL、Janus-Pro、OmniGen2、BLIP3-o、Ovis-U1、GPT-4o-Image等。
- **模型架构覆盖**：四种主流UMM类型——离散（Show-o，MaskGIT）、掩码自回归（Harmon，MAR）、连续扩散（OpenUni、BAGEL）。

## 4. 资源与算力

- **GPU型号与数量**：单个NVIDIA A100 80GB GPU（所有后训练实验）。
- **训练时长**：对于Harmon-1.5B，Post-training仅需约27 GPU小时（对应于5K训练步数）。不同模型略有差异（如Show-o 4-9小时，BAGEL 4.5小时），但整体极为高效。
- **推理硬件**：Show-o、Harmon、OpenUni在RTX 4090 24GB上推理，BAGEL仍在A100上。

## 5. 实验数量与充分性

- **实验数量**：论文进行了大量实验，包括：
  - 在4种UMM架构、多个参数规模（0.5B~14B）上验证通用性（表2、表10）。
  - 在生成基准（GenEval、DPGBench、WISE）和编辑基准（ImgEdit、GEdit-Bench-EN）上的全面对比（表1、表3）。
  - 消融研究：数据规模（10K~240K）、数据来源（COCO、JourneyDB、BLIP3o、MidjourneyV6）、输入分辨率（224 vs 512）、编码器类型（理解 vs 生成）、训练顺序（SFT→RecA vs RecA→SFT）、是否使用GPT-4o蒸馏数据等（表5-7、表13-14）。
  - 动态分析：训练步数对GenEval子任务的影响（图15）、不同架构的重建质量对比（图17）。
- **充分性与客观性**：实验设计严谨，报告了12个随机种子的统计结果（标注*），避免基准泄漏（分离BLIP3o-60k中7K模板数据），对比方法涵盖最先进的开放和私有模型，结论可靠。

## 6. 主要结论与发现

- **RecA显著提升生成与编辑性能**：1.5B参数的Harmon经RecA后训练，在GenEval上从0.73提升至0.90（甚至超过GPT-4o-Image的0.84），在DPGBench上从80.93提升至88.15。编辑任务上ImgEdit提升0.37，GEdit提升0.33。
- **通用性极强**：RecA在四种不同架构（离散、MAR、连续扩散）中均带来一致且可观的改善，尤其Harmon和OpenUni提升最大（GenEval提升12.8和12.2）。
- **资源效率高**：仅需27 GPU小时，无需额外标注，优于需要大规模蒸馏或强化学习的方法。
- **最佳训练策略**：先进行SFT粗对齐，再应用RecA细粒度精调（SFT→RecA）效果最优；RecA单独使用也优于SFT。
- **视觉理解能力保持或提升**：在共享参数的UMM中，RecA不损害理解性能（MME等指标持平或略升）。
- **语义嵌入优于像素嵌入**：使用理解编码器（ViT）比使用生成编码器（VAE）效果显著更好；低分辨率输入（224×224）比高分辨率更有利于语义重建。

## 7. 优点

- **方法简洁高效**：自监督重建，无需任何文本标注，只需未标记图像。
- **通用性强**：适用于多种UMM架构，且在不同数据规模、来源下均稳健。
- **大幅超越现有方法**：以极小参数量（1.5B）和极低计算成本超越更大模型（如7B Janus-Pro、14B BAGEL、甚至闭源GPT-4o-Image）。
- **揭示关键洞察**：视觉理解嵌入可作为密集语义提示，有效弥合理解与生成之间的对齐差距。
- **免蒸馏与免强化学习**：规避了GPT-4o数据的高成本和模板泄漏风险，以及RL的复杂调参。
- **编辑能力显著提升**：在ImgEdit和GEdit上达到与闭源模型接近的性能。

## 8. 不足与局限

- **计数任务改进有限**：由于UMM对数字这类中高层语义的提取能力较弱，RecA在GenEval的计数子任务上增益不大（仅+2.7），需要未来结合计数数据集或强化学习。
- **对特定架构效果受限**：在BLIP-3o上应用RecA未带来增益甚至略有退化，可能因其预训练已包含重建目标；Show-o因CLIP语义能力不足且码本受限，提升相对较小。
- **推理能力（WISE）提升不均**：RecA主要提升语义对齐，但对需要世界知识推理的WISE基准增益有限（尤其BAGEL和Show-o几乎无提升），表明推理能力仍需专门设计。
- **依赖视觉理解编码器质量**：性能上限受限于编码器提取的语义丰富度（如Show-o的CLIP弱于SigLIP/IP-Adapter）。
- **数据偏差风险**：使用MidjourneyV6等合成数据可能引入分布偏差，尽管消融实验显示COCO等真实数据仍有改善，但最优点仍偏向高质量合成数据。
- **大规模模型验证不足**：论文最大模型为14B BAGEL，但对于更大规模（如几十B）的UMM，RecA的有效性尚未验证。

（完）
