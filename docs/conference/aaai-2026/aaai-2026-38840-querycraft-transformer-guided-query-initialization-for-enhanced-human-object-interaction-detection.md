---
title: "QueryCraft: Transformer-Guided Query Initialization for Enhanced Human-Object Interaction Detection"
title_zh: QueryCraft：Transformer引导的查询初始化用于增强人-物交互检测
authors: "Yuxiao Wang, Wolin Liang, Yu Lei, Weiying Xue, Nan Zhuang, Qi Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38840/42802"
tags: ["query:multimodal"]
score: 6.0
evidence: 跨模态Transformer用于人-物交互检测
tldr: 针对DETR方法查询缺乏语义的问题，提出QueryCraft框架，其核心ACTOR模块是一个跨模态Transformer编码器，联合关注视觉区域和文本提示，通过语义先验初始化查询，显著提升人-物交互检测的精度。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38840/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38840/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1836, \"height\": 784, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1673, \"height\": 1380, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 509, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 887, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 846, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 830, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 830, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 799, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38840/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 802, \"height\": 253, \"label\": \"Table\"}]"
motivation: 随机初始化的查询缺乏显式语义，导致检测性能次优。
method: 提出ACTOR跨模态Transformer，联合视觉区域和文本提示进行语义引导的查询初始化。
result: 在HOI检测基准上取得显著提升，验证了语义先验的有效性。
conclusion: QueryCraft为HOI检测提供了可插拔的语义查询初始化方案。
---

## Abstract
Human-Object Interaction (HOI) detection aims to localize human-object pairs and recognize their interactions in images. Although DETR-based methods have recently emerged as the mainstream framework for HOI detection, they still suffer from a key limitation: Randomly initialized queries lack explicit semantics, leading to suboptimal detection performance. To address this challenge, we propose QueryCraft, a novel plug-and-play HOI detection framework that incorporates semantic priors and guided feature learning through transformer-based query initialization. Central to our approach is ACTOR (Action-aware Cross-modal TransfORmer), a cross-modal Transformer encoder that jointly attends to visual regions and textual prompts to extract action-relevant features. Rather than merely aligning modalities, ACTOR leverages language-guided attention to infer interaction semantics and produce semantically meaningful query representations. To further enhance object-level query quality, we introduce a Perceptual Distilled Query Decoder (PDQD), which distills object category awareness from a pre-trained detector to serve as object query initiation. This dual-branch query initialization enables the model to generate more interpretable and effective queries for HOI detection. Extensive experiments on HICO-Det and V-COCO benchmarks demonstrate that our method achieves state-of-the-art performance and strong generalization.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

人-物交互（Human-Object Interaction，HOI）检测旨在定位图像中的人-物对并识别其交互动作，生成 `<human, action, object>` 三元组。近年来，基于 DETR 的端到端方法成为主流框架，但其存在关键局限：**查询（query）随机初始化缺乏显式语义**，导致模型难以准确表示对象类别和交互语义，检测性能次优。本文旨在通过注入语义先验和引导特征学习来解决该问题，提升 HOI 检测的精度和泛化能力。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
提出 **QueryCraft** 框架，它是一个即插即用的模块，可集成到任何基于查询的 HOI 检测器中。通过双分支语义查询初始化——**PDQD**（感知蒸馏查询解码器）提供对象感知表示，**ACTOR**（动作感知跨模态Transformer）提供动作感知表示——替代传统随机初始化，从而生成更可解释、更有效的查询。

### 关键技术细节
- **PDQD**：
  - 使用可学习投影令牌 P，通过一个 Transformer 解码器与编码图像特征交互，获得对象特征 `F_obj`。
  - 对 `F_obj` 进行全局平均池化后经 MLP 做多标签分类（80类），训练时以预训练 YOLO 检测器的结果作为伪标签，通过交叉熵损失蒸馏对象类别知识。
  - 在推理时，P 用于初始化实例解码器的对象查询 `Q_o`（`Q'_o = Q_o + λ1·P`），并在解码输出后残差增强 `V'_o = V_o + λ2·P`。

- **ACTOR**：
  - 利用预训练文本编码器将动作类别描述（如“a person is [verb-ing] an [object]”）编码为文本嵌入 T。
  - 对图像提取视觉特征 I，将其扩展为 N_q 个查询种子，通过交叉注意力机制（L=3层）让视觉特征查询语义字典 T，输出动作感知查询 A。
  - A 用于初始化交互解码器查询 `Q'_a = Q_a + γ1·A`，并在解码输出后残差增强 `V'_a = V_a + γ2·A`。

- **整体流程**：图像经主干网络（ResNet-50 或 Swin Transformer）提取特征后，输入 Transformer 编码器；实例解码器使用 PDQD 增强的查询预测人和物边界框及类别；交互解码器使用 ACTOR 增强的查询预测动作类别。后处理使用 NMS 过滤冗余。

### 公式描述（文字说明）
- PDQD 训练损失：多标签二分类交叉熵，以 YOLO 检测结果作为标签。
- 查询增强：线性加权组合，权重 λ1、λ2、γ1、γ2 默认均为1。
- ACTOR 跨模态注意力：计算视觉查询与文本键的相似度，加权求和得到更新后的查询。

## 3. 实验设计

### 数据集与基准
- **HICO-DET**：47,776 张图像，600 个 HOI 类别，按训练样本数分为 Rare（<10）和 Non-Rare。
- **V-COCO**：10,346 张图像，80 个交互类别（对应 29 种动作）。
- **HICO-Det-IC / V-COCO-IC**：用于评估不及物（非接触）交互。
- **零样本设置**：Unseen Verb（UV）、Unseen Object（UO）、Non-Finetuned Unseen Composition（NF-UC）、Rare-Finetuned Unseen Composition（RF-UC）。

### 对比方法
- **两阶段方法**：HO-RCNN、InteractNet、iCAN、UnionDet、IP-Net 等。
- **Transformer/DETR 方法**：HOTR、MSTR、GEN-VLKT、RLIPv2、TED-Net、LOGICHOI、KI2HOI。
- 将 QueryCraft 作为插件集成到 GEN-VLKT、RLIPv2、TED-Net、LOGICHOI、KI2HOI 中进行对比。

### 评估指标
- mAP（平均精度均值），在 Full、Rare、Non-Rare 子集上分别报告。

## 4. 资源与算力

论文中**未明确说明**训练所使用的 GPU 型号、数量、训练时长等具体算力资源。仅在训练效率分析中提到各方法达到最优 epoch 的轮数对比（如 GEN-VLKT 87→76 轮，TED-Net 97→79 轮等），但未给出实际时间或硬件配置。

## 5. 实验数量与充分性

论文进行了**大量实验**，包括：
- **主表（Table 1）**：在 HICO-Det 上对比 8 种基准方法（含不同骨干网络的 RLIPv2），每种方法均报告 Full、Rare、Non-Rare mAP。
- **Table 2**：在 V-COCO 上对比 6 种方法。
- **Table 3**：零样本检测（4 种协议 × 3 种方法 × 3 个指标）。
- **Table 4**：不及物交互检测（HICO-Det-IC 和 V-COCO-IC）。
- **Table 5**：训练收敛速度对比（5 种方法）。
- **消融实验（Table 6-9）**：组件分析、权重参数 λ1/λ2、γ1/γ2、文本模板 T1-T4。
- 实验设计**充分、客观、公平**：
  - 所有基线采用官方代码复现，公平对比。
  - 消融实验控制变量，分析每个模块贡献。
  - 覆盖常规、零样本、不及物等多种场景，验证泛化能力。

## 6. 论文的主要结论与发现

- **性能提升显著**：在 HICO-Det 的 Full 子集上提升 +0.92~+1.17 mAP，Rare 子集提升 +1.21~+1.72 mAP；V-COCO 提升 +1.0~+1.7 mAP。
- **零样本泛化能力强**：在 Unseen Verb 和 Unseen Object 设置下分别提升 +2.10 和 +2.45 mAP。
- **训练加速**：各方法收敛所需 epoch 减少 12.6%~18.6%。
- **模块协同**：PDQD 和 ACTOR 结合效果优于单个模块，且超过两者独立增益之和（34.51→34.63，实际总和为 1.06 vs 1.12），表明正协同。
- **权重参数敏感性**：初始化权重（λ1, γ1）比残差增强权重（λ2, γ2）更重要，尤其是 ACTOR 的 γ1 对性能影响最大。
- **文本模板鲁棒**：不同动作描述模板（T1-T4）性能差异极小，表明 ACTOR 对语言变化稳健。

## 7. 优点

- **创新性**：首次将语义查询初始化应用于 DETR 式 HOI 检测，通过跨模态注意力蒸馏动作知识，对象感知蒸馏检测知识，思路清晰。
- **即插即用**：QueryCraft 可无缝集成到多种现有方法，通用性强。
- **实验全面**：覆盖常规、零样本、不及物交互、训练效率等多个维度，消融实验设计严谨。
- **可解释性**：通过语言引导的注意力可视化（文中未展示但暗示），提供语义理解。
- **开源友好**：提供代码和扩展版本 arXiv 链接。

## 8. 不足与局限

- **算力资源未说明**：未报告训练时间和硬件配置，无法评估实际效率。
- **依赖外部检测器**：PDQD 需要预训练 YOLO 的蒸馏结果，可能引入领域适应偏差。
- **文本模板局限性**：虽然测试了四种模板，但未探索更复杂的语言描述（如带上下文的句子），也未分析不同 CLIP 版本的影响。
- **未分析大规模场景**：仅在 HICO-Det 和 V-COCO 上评估，缺乏在大规模 HOI 数据集（如 VidHOI）上的验证。
- **可能过拟合蒸馏标签**：YOLO 检测结果存在噪声，PDQD 可能学习到错误标签，论文未分析该风险。
- **未讨论推理速度**：双分支查询初始化增加的额外计算开销未量化。

（完）
