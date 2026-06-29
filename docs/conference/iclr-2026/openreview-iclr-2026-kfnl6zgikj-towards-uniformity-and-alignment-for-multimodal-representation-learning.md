---
title: Towards Uniformity and Alignment for Multimodal Representation Learning
title_zh: 面向多模态表示学习的均匀性与对齐方法
authors: "Wenzhe Yin, Pan Zhou, Zehao Xiao, Jie Liu, Shujian Yu, Jan-Jakob Sonke, Stratis Gavves"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=KfNl6zgIKJ"
tags: ["query:multimodal"]
score: 8.0
evidence: 多模态表示中对齐和均匀性的原则性解耦
tldr: 本文识别并分析多模态InfoNCE目标中存在的对齐-均匀性冲突和内部对齐冲突，并提出原则性的解耦方法。理论证明该方法能缓解冲突，减少模态间的分布差距。为多模态表示学习提供了新的理论视角。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-kfnl6zgikj/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1258, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-kfnl6zgikj/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1404, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-kfnl6zgikj/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1426, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-kfnl6zgikj/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1405, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-kfnl6zgikj/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1386, \"height\": 1756, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-kfnl6zgikj/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1405, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kfnl6zgikj/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 586, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kfnl6zgikj/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1205, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kfnl6zgikj/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1460, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-kfnl6zgikj/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 819, \"height\": 224, \"label\": \"Table\"}]"
motivation: 现有InfoNCE目标在多模态学习中引入冲突，导致模态间分布差距和表示不均匀。
method: 提出解耦对齐和均匀性的方法，通过理论分析保证缓解冲突。
result: 理论证明方法有效性，并通过实验验证改进的多模态表示质量。
conclusion: 为多模态表示学习中的冲突问题提供了有效的理论解决方案。
---

## Abstract
Multimodal representation learning aims to construct a shared embedding space in which heterogeneous modalities are semantically aligned. Despite strong empirical results, InfoNCE-based objectives introduce inherent conflicts that yield distribution gaps across modalities. We identify and formally analyze two conflicts in the multimodal regime, both exacerbated as the number of modalities \(M\) increases: (i) an alignment–uniformity conflict, whereby uniform repulsion undermines positive-pair alignment, and (ii) an intra-alignment conflict stemming from the non-collinearity of multi-way positives. To address these issues, we propose a principled decoupling of alignment and uniformity. We then demonstrate a theoretical guarantee that our method mitigates the distribution gap by introducing a global Hölder divergence over multiple modality distributions. We show that our decoupled losses act as efficient proxies for minimizing this cross-modal divergence. Extensive experiments on retrieval and UnCLIP-style generation demonstrate consistent gains. Overall, this work provides a conflict-free recipe and theoretical guidance for multimodal learning that simultaneously supports discriminative and generative use cases without task-specific modules.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

*   **研究动机**：多模态表示学习旨在构建一个共享的嵌入空间，使不同模态（如图像、文本、音频、视频等）在语义上对齐。当前主流方法（如CLIP及其多模态扩展）依赖InfoNCE对比损失函数，但该目标函数在模态数量 \(M \ge 3\) 时存在固有冲突，导致模态之间存在**分布差距**，影响表示质量与下游任务（如跨模态检索和生成）性能。
*   **核心问题**：作者识别并形式化分析了两种冲突：
    *   **对齐-均匀性冲突**：InfoNCE中的均匀性项（使嵌入在单位超球面上均匀分布）与对齐项（拉近正样本对）相互对抗，加剧分布差距。
    *   **内部对齐冲突**：当存在多个模态时，正样本嵌入不共线，导致对齐合力减弱，且随模态数 \(M\) 增加而加剧。
*   **整体含义**：现有InfoNCE框架在多模态场景下存在根本性的内在矛盾，需要一种无冲突的新学习原则来同时提升表示的可区分性（对检索有益）和跨模态分布的一致性（对生成有益）。

## 2. 论文提出的方法论：核心思想、关键技术细节

*   **核心思想**：将**对齐**与**均匀性**进行原则性解耦，避免InfoNCE中的相互抵消。
    *   **均匀性**：采用**模态内均匀性**，即每个模态内部独立地对其样本施加均匀分布约束（基于高斯核的排斥力），而不跨模态施加均匀性，从而消除对齐-均匀性冲突。
    *   **对齐**：采用**基于锚点的对齐**策略。选择一个锚定模态（如图像），其他模态的所有样本均与锚定模态的对应样本进行欧氏距离对齐（均方误差），避免多模态正样本不共线导致的合力抵消。
*   **关键技术细节**：
    *   **模态内均匀性损失** \( \mathcal{U}(\mathbf{Z}^{(m)}) \)：对每个模态 \(m\) 的批次内样本计算核密度估计的均匀性，使用高斯核 \(\kappa(\mathbf{z}_i, \mathbf{z}_j) = \exp\left(-\|\mathbf{z}_i - \mathbf{z}_j\|_2^2 / (2\tau^2)\right)\)。梯度主要作用于附近“硬负样本”，避免跨模态冲突。
    *   **基于锚点的对齐损失** \( \mathcal{L}_{\text{align}} \)：选取模态 \(a\) 为锚点，其他模态 \(n\) 的样本向锚点对齐：\(\frac{1}{B(M-1)} \sum_{i=1}^B \sum_{n \neq a} \|\mathbf{z}_i^{(a)} - \mathbf{z}_i^{(n)}\|_2^2\)。
    *   **体积增强项**（可选）：
        *   **体积均匀性** \(\mathcal{U}(\mathbf{C})\)：对所有模态的加权质心进行均匀性约束，促进元组级别的分散。
        *   **体积对齐** \(\mathcal{L}_{\text{vol}}\)：最小化每个样本的 Gram 矩阵行列式（即模态向量张成的简单体积），鼓励模态向量共线。
    *   **总损失**：\( \mathcal{L} = \lambda_{\text{uni}} \sum_{m=1}^M \mathcal{U}(\mathbf{Z}^{(m)}) + \lambda_{\text{align}} \mathcal{L}_{\text{align}} + \lambda_{\text{vol}} \mathcal{L}_{\text{vol}} \)。
    *   **理论保证**：作者引入全局 Hölder 散度来衡量多个模态分布的总体差异。通过核密度估计，证明模态内均匀损失和对齐损失分别可作为该散度中均匀项和对齐项的计算代理，从而最小化跨模态分布差距。

## 3. 实验设计：数据集、Benchmark、对比方法

*   **数据集**：
    *   **检索任务**：训练在 **VAST-150K** 数据集上；零样本评测在 **MSR-VTT**、**DiDeMo**、**ActivityNet** 三个视频-文本基准上。
    *   **生成任务**：使用 **VGGSound** 数据集（音频-视觉对），并利用 VAST 提供的字幕模型生成文本描述，构建视频-音频-文本三元组。
*   **Benchmark**：
    *   检索：零样本文本到视频（T2V）和视频到文本（V2T）的 Recall@1。
    *   生成：文本到图像（T2I）、音频到图像（A2I）和模态插值（文本+音频→图像）的 Fréchet Inception Distance（FID）。
*   **对比方法**：
    *   检索基线：UMT、OmniVL、TVTSv2、ViCLIP、VideoCoCa、Norton、ImageBind、InternVideo、HiTeA、mPLUG-2、VideoPrism、LanguageBind、VAST、GRAM（最新 SOTA）。
    *   生成基线：ImageBind、GRAM（重新训练），使用 Kandinsky 和 Stable UnCLIP 两种解码器。
*   **模型架构**：使用与 VAST/GRAM 一致的骨干网络：BERT-B（文本）、BEATs（音频）、EVA-CLIP ViT-G（视频）。

## 4. 资源与算力

*   论文明确提到：**所有实验使用 4 块 NVIDIA A6000 GPU**。
*   训练配置：AdamW 优化器，学习率 \(2\times 10^{-5}\)，每 GPU 批量大小 128（全局批量 512），其他优化器参数默认。
*   训练时长：检索任务训练 5 个 epoch；生成任务训练 50 个 epoch。

## 5. 实验数量与充分性

*   **实验数量**：
    *   检索：在 3 个基准上报告了 6 个评估指标（T2V 和 V2T），并给出平均结果，对比了 12 种以上方法。
    *   生成：在 2 个解码器（Kandinsky 和 Stable UnCLIP）上测试了 T2I、A2I、插值，对比了 ImageBind 和 GRAM，且包含了自重建上界（*标记）。
    *   消融实验：在 MSR-VTT 上对体积均匀性 \(\mathcal{U}(C)\) 和体积对齐 \(\mathcal{L}_{\text{vol}}\) 进行了消融（表2），并对质心均匀性的温度 \(\tau_{\text{ctr}}\) 进行了消融（表5）。
    *   可视化：t-SNE 图展示分布差距。
*   **充分性与公平性**：
    *   **充分**：覆盖了主要任务（检索与生成），并包含消融、可视化、定量指标。
    *   **公平**：与基线使用相同骨干网络、相同初始化（VAST 预训练权重），解码器部分固定并给出上界。方法未引入额外模块，计算复杂度与 InfoNCE 相当。

## 6. 论文的主要结论与发现

*   **理论发现**：InfoNCE 在多模态（\(M \ge 3\)）中确实存在对齐-均匀性冲突和内部对齐冲突，且随 \(M\) 增加而加剧（Corollary 1 & 2）。解耦损失能够有效最小化全局 Hölder 散度，从而缩小分布差距。
*   **检索性能**：UniAlign 在零样本视频检索上一致优于所有对比方法，在 MSR-VTT 上 T2V 达到 58.7 R@1（比 GRAM 高约 4.5 个点），V2T 达 54.6。
*   **生成性能**：在 VGGSound 上，UniAlign 在 T2I、A2I 和插值任务中均显著降低 FID（比 GRAM 低 10-40），接近自重建上界，表明模态间分布差距大幅减小。
*   **定性结果**：t-SNE 可视化显示 UniAlign 下不同模态特征紧密重叠，而 InfoNCE 方法仍呈现明显聚类分离。模态插值生成图像能有效融合多个模态语义。
*   **结论**：无冲突的分解原则能同时提升判别式和生成式任务，无需任务特定模块，为多模态学习提供了可扩展的理论与实践框架。

## 7. 优点：方法或实验设计上的亮点

*   **理论深度**：首次严格形式化多模态 InfoNCE 的两类冲突，并给出渐近分析（Corollary 1 & 2），提供了坚实的理论支撑。
*   **方法简洁但有效**：解耦策略直观（模态内均匀性 + 锚点对齐），无需复杂网络结构，计算复杂度与传统 InfoNCE 相同。
*   **理论-实践闭环**：提出全局 Hölder 散度，并将所提损失与该散度建立联系，证明优化损失等价于最小化分布差距，赋予方法理论保证。
*   **实验设计全面**：同时涵盖判别（检索）和生成任务，并在多个基准和两种解码器上验证，通用性强。
*   **可视化与定性展示**：t-SNE 和生成样图直观证明分布差距被有效缓解，增强了说服力。

## 8. 不足与局限

*   **实验覆盖局限**：
    *   仅验证了文本-视频-音频三种模态，未涉及深度图、触觉、红外等更多模态。
    *   生成任务仅在 VGGSound 数据集上评估，且该数据集本身视频质量嘈杂，可能限制生成质量上限。
*   **锚点依赖**：当前对齐策略依赖于选择一个固定锚点模态（图像），当锚点模态缺失或质量下降时可能导致性能退化。作者未讨论锚点选择的敏感性。
*   **温度与超参数敏感性**：虽然消融显示一定程度上鲁棒，但三个损失项权重（\(\lambda_{\text{uni}}, \lambda_{\text{align}}, \lambda_{\text{vol}}\)）需要手动调整，且在不同任务中采用了不同的 \(\lambda_{\text{vol}}\)（检索设为1，生成设为0.1），缺乏自适应策略。
*   **理论假设可能与实际偏差**：Assumption 1 中假设残差异噪声零均值且独立，但在复杂数据中可能不严格成立，理论结论的稳健性需更多实证。
*   **大规模训练验证不足**：实验仅用 4×A6000 训练 5 epoch（检索）或 50 epoch（生成），未展示更大规模数据（如完整 VAST 规模或 LAION）上的可扩展性。

（完）
