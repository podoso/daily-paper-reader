---
title: "Aligning the True Semantics: Constrained Decoupling and Distribution Sampling for Cross-Modal Alignment"
title_zh: 对齐真实语义：约束解耦与分布采样实现跨模态对齐
authors: "Xiang Ma, Lexin Fang, Litian Xu, Caiming Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39609/43570"
tags: ["query:multimodal"]
score: 8.0
evidence: 跨模态对齐，语义解耦，分布采样用于多模态学习
tldr: 针对跨模态对齐中非语义信息干扰和模态差距导致语义偏差问题，提出约束解耦与分布采样方法，将嵌入分解为语义和模态成分，仅对齐语义部分，同时通过分布采样弥补模态间隙。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39609/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39609/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1838, \"height\": 728, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39609/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 835, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39609/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 817, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39609/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 480, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39609/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1838, \"height\": 1152, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39609/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 892, \"height\": 738, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39609/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 638, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39609/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 877, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39609/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 227, \"label\": \"Table\"}]"
motivation: 现有对齐方法忽略非语义信息，且模态差距导致语义偏差。
method: 提出嵌入解耦为语义和模态成分，仅对齐语义部分，并采用分布采样来消除模态间隙。
result: 在跨模态检索和分类任务上达到最佳性能。
conclusion: 该方法实现了更精确的跨模态语义对齐。
---

## Abstract
Cross-modal alignment is a crucial task in multimodal learning aimed at achieving semantic consistency between vision and language. This requires that image-text pairs exhibit similar semantics. Traditional algorithms pursue embedding consistency to achieve semantic consistency, ignoring the non-semantic information present in the embedding. An intuitive approach is to decouple the embeddings into semantic and modality components, aligning only the semantic component. However, this introduces two main challenges: (1) There is no established standard for distinguishing semantic and modal information. (2) The modality gap can cause semantic alignment deviation or information loss. To align the true semantics, we propose a novel cross-modal alignment algorithm via Constrained Decoupling and Distribution Sampling (CDDS). Specifically, (1) A dual-path UNet is introduced to adaptively decouple the embeddings, applying multiple constraints to ensure effective separation. (2) A distribution sampling method is proposed to bridge the modality gap, ensuring the rationality of the alignment process. Extensive experiments on various benchmarks and model backbones demonstrate the superiority of CDDS, outperforming state-of-the-art methods by 6.6% to 14.2%.

---

## 论文详细总结（自动生成）

# 论文总结：Aligning the True Semantics: Constrained Decoupling and Distribution Sampling for Cross-Modal Alignment

## 1. 核心问题与研究动机

- **问题背景**：跨模态对齐旨在实现视觉与语言间的语义一致性，是图像-文本检索、图像描述、文本-图像生成等任务的基础。传统方法（如基于对比学习的VSE++、SCAN等）追求嵌入（embedding）的全局一致性，认为嵌入相似即可等价于语义相似。
- **核心缺陷**：嵌入中混杂了大量非语义信息（如图像的颜色分布、文本的句法结构、训练数据噪声等），这些模态特有的信息无法跨模态匹配，但传统对齐方法仍强制对其进行对齐，引入语义偏差，导致“嵌入一致性≠语义一致性”。
- **直觉解决思路**：将嵌入解耦（decouple）为“语义成分”（semantic component）和“模态成分”（modality component），仅对齐语义成分。
- **两大挑战**：
  - 语义与模态信息耦合复杂，缺乏明确的分离标准。
  - 模态差距（modality gap）可能导致语义对齐偏差或信息损失。

## 2. 方法论：CDDS

### 核心思想
提出基于**约束解耦与分布采样**（Constrained Decoupling and Distribution Sampling, CDDS）的跨模态对齐算法。核心步骤：
1. 通过双路径UNet将嵌入自适应解耦为语义成分和模态成分；
2. 通过多重约束保证解耦有效性与信息完整性；
3. 通过分布采样方法间接实现语义对齐，避免直接调整嵌入带来的分布扭曲。

### 关键技术细节

#### (a) 嵌入提取
- 图像：使用ViT或Swin Transformer提取patch级视觉嵌入 \( V = \{v_i\} \)。
- 文本：使用BERT提取word级文本嵌入 \( T = \{t_j\} \)。

#### (b) 双路径UNet解耦架构
- **共享编码器** \( E_v \)（Vision Transformer层）将嵌入映射到高维表示 \( H_v \)。
- 引入高斯噪声 \( \Delta \)，生成多组扰动表示 \( \hat{H}_v \)，增强鲁棒性。
- **语义解码器**与**模态解码器**分别从扰动表示中提取语义成分 \( V_s \) 和模态成分 \( V_m \)，并利用跳跃连接保留不同抽象层次特征。
- 文本侧同理得到 \( T_s \) 和 \( T_m \)。

#### (c) 多重约束
1. **语义成分约束**（公式11）：
   - 通过分布采样得到跨模态语义成分（x-semantic component）\( V_x \) 和 \( T_x \)。
   - 约束 \( V_s \) 与 \( V_x \)、\( T_s \) 与 \( T_x \) 的对比学习损失，间接对齐不同模态的语义。
2. **模态成分约束**（公式12）：
   - 同一模态内的模态成分应保持分布一致性：使图像各patches的模态成分分布接近，文本各words亦如此。
3. **信息完整性约束**（公式13-14）：
   - 语义成分 \( V_s \) 与模态成分 \( V_m \) 可重建原始嵌入 \( V \)；
   - 同时x-语义成分 \( V_x \) 与模态成分 \( V_m \) 也可重建原始嵌入，避免对齐过程信息丢失。

#### (d) 分布采样方法（核心创新）
- **相关语义识别**：计算每个特征列的分布（\( C_v, C_t \)），用KL散度衡量相关性，通过自适应软阈值（基于概率统计特性）筛选强相关分布。
- **分布采样**：对于当前分布 \( C_i^v \)，从文本侧强相关分布 \( C_j^t \) 中按照概率分位点对应采样，加权聚合得到 \( C_i^x \)（x-语义分布），再逆映射为 \( V_x \)。此过程将图像语义“翻译”为文本描述形式，弥合模态间隙。

#### 损失函数（公式15）
\[
L = \alpha_s L_s + \alpha_m L_m + \alpha_f L_f + (1-\alpha_f)L_x
\]
\( \alpha_s, \alpha_m, \alpha_f \) 为超参数。

## 3. 实验设计

### 数据集与评价指标
- **Flickr30K**：29,000训练、1,000验证、1,000测试，每图5个描述。
- **MS-COCO**：82,738训练、5,000验证、5,000测试，报告1K（5折平均）和5K结果。
- 指标：Recall@K (K=1,5,10) 及 rSum（各Recall和）。

### 基准方法
- **粗粒度**：VSE++, SCAN, SGR, CHAN, LAPS。
- **预训练模型对比**：VILT, SOHO, ALBEF, BLIP；以及将CDDS集成到CLIP的零样本/全微调比较。

### 不同骨干网络
- ViT-224 (14×14 patches)、ViT-384 (24×24)、Swin-224 (7×7)、Swin-384 (12×12)，特征维度统一为512。

## 4. 资源与算力

- **文中说明**：训练25个epoch，使用**NVIDIA L40 GPU**，**batch size=64**，优化器AdamW，学习率2e-4。
- **未明确说明**：具体使用了多少块GPU、单卡还是多卡、显存占用、训练时长等细节。因此无法确认总计算资源量。

## 5. 实验数量与充分性

- **主要实验**：在2个数据集（Flickr30K, MS-COCO）上，采用4种骨干网络（ViT-224/384, Swin-224/384），对比了5种SOTA方法（VSE++, SCAN, SGR, CHAN, LAPS），并进行了与VLP模型（CLIP系列）的对比。
- **消融实验**（表3）：
  - 移除解耦模块 (w/o Dec.)
  - 移除模态约束 (w/o Mod.)
  - 移除信息完整性约束 (w/o Int.)
  - 移除高斯噪声 (w/o Gau.)
  - 将分布采样替换为直接对比学习 (w/o Sam.)
- **迁移性实验**（表4）：将分布采样方法应用到其他模型（VSE++, SCAN, SGR, CHAN, LAPS）中观察性能提升。
- **可视化分析**（图5）：显示解耦后文本嵌入因同一图像的各描述更聚集。
- **效率讨论**（表5）：比较了分布采样的不同执行方式（每batch/随机/全数据集）的耗时与效果。
- **充分性评价**：实验覆盖了多种骨干、多种分辨率、多种对比方法，消融和迁移实验设计合理，结果客观。但缺少在更大规模预训练模型（如CLIP Large）上的完整微调对比（仅有基于CLIP的少量实验）。

## 6. 主要结论与发现

- CDDS在所有骨干和数据集上均显著优于SOTA方法（提升6.6%~14.2% rSum）。
- 约束解耦与分布采样的各组件均为必要：移除任一部分均造成性能下降（表3）。
- 分布采样方法具有通用性，可嵌入其他模型提高性能（表4）。
- 解耦操作能有效去除模态信息，使同一语义的不同文本嵌入在语义空间中更接近（图5）。
- 效率是主要局限：每batch计算分布相关性（\( O(N^2) \)）耗时较高；简化方案会大幅降低效果。

## 7. 优点

- **问题洞察深刻**：明确指出嵌入一致性不代表语义一致性，并通过解耦+分布采样的方式解决了模态信息干扰问题。
- **方法创新**：双路径UNet自适应解耦+分布采样实现跨模态语义对齐，无需强行调整分布，避免信息损失。
- **约束设计全面**：语义一致性、模态一致性、信息双重重建约束共同保证解耦效果。
- **实验扎实**：在多个骨干上验证，包含消融、迁移、可视化分析，结果具有说服力。
- **开源友好**：未提及开源代码，但方法描述详细，可复现。

## 8. 不足与局限

- **效率瓶颈**：分布采样每batch需计算所有特征列分布的KL散度，复杂度\( O(N^2) \)，面对大规模特征列时开销大；文中简化方案（随机/全数据集）会显著降低效果。
- **实验覆盖**：
  - 未在更大规模预训练模型（如CLIP ViT-L/14）上做完整的微调对比（表2中仅CLIP基础版）。
  - 缺少在更多模态（如视频、音频）上的验证。
- **可解释性**：虽然可视化展示了嵌入空间变化，但对解耦后语义成分和模态成分的具体含义缺乏深入定性分析。
- **应用限制**：分布采样依赖于特征列的条件概率估计，若特征列数较少（如低维嵌入）可能效果下降。
- **假设强度**：假设嵌入中语义与模态信息可线性解耦（通过重建损失保证），实际中可能更复杂。

（完）
