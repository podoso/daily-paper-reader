---
title: "T-APT: Text-Guided Modality-Aware Prompt Tuning for Arbitrary Multimodal Remote Sensing Data Joint Classification"
title_zh: T-APT：文本引导的模态感知提示调优用于任意多模态遥感数据联合分类
authors: "Qinghao Gao, Jiahui Qu, Wenqian Dong"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/42411/46372"
tags: ["query:multimodal"]
score: 5.0
evidence: 文本引导的跨模态提示调优用于多模态联合分类
tldr: 针对现有方法缺乏对动态多模态组合自适应泛化能力的问题，提出了T-APT框架，利用互补融合特征驱动基础模型，并通过文本引导的模态先验知识作为跨模态提示对预训练ViT进行微调，实验表明该方法在不同模态组合下均取得优异分类性能，为多模态遥感联合分类提供了统一解决方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 822, \"height\": 779, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1743, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1745, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 872, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 869, \"height\": 754, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 863, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-42411/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 820, \"height\": 807, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42411/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 839, \"height\": 873, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42411/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42411/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1837, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-42411/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 841, \"height\": 649, \"label\": \"Table\"}]"
motivation: 现有方法缺乏对动态多模态组合的自适应泛化能力。
method: 提出文本引导的任意模态提示调优框架，利用互补融合特征驱动基础模型，并采用Mamba架构处理任意模态输入。
result: 在多种模态组合下取得优异分类性能，验证了框架的泛化能力。
conclusion: T-APT为多模态遥感联合分类提供了统一的泛化解决方案。
---

## Abstract
Multimodal remote sensing image joint classification has achieved significant progress. However, existing methods primarily focus on designing modality-specific networks, lacking adaptive generalization capabilities in diverse and dynamic modality combinations encountered in real-world scenarios. Inspired by the generalization capabilities of visual foundation model in downstream tasks, we propose a unified Text-guided Arbitrary Modalitiy Prompting (T-APT) framework, which leverages complementary fused features to drive the foundation model and employs text-guided modality-specific prior knowledge as cross-modal prompts to fine-tune a pretrained Vision Transformer (ViT) model. Specifically, a Mamba-Based Arbitrary Modal-Focused Feature Capture (MAMF-FC) module is designed to extract complementary joint features and modality-specific prior knowledge from arbitrary modalities through a shared-specific scanning encoder-decoder architecture. Subsequently, a Text-Guided Modality-Aware Prompt Tuning (TMPT) module is proposed to support the adaptation of fused features to the foundation model, enabling our arbitrary remote sensing image classification task. Extensive experiments on public datasets spanning multispectral (MS), hyperspectral (HS), light detection and ranging (LiDAR), and synthetic aperture radar (SAR) modalities demonstrate that our T-APT achieves classification performance comparable to specialized networks across arbitrary modal combinations.

---

## 论文详细总结（自动生成）

# T-APT 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：现有多模态遥感图像联合分类方法大多针对固定模态组合（如 HSI+LiDAR 或 HSI+MSI）设计专用网络，当实际场景中模态组合动态变化（例如从两模态变为三模态，或替换其中一种模态）时，这些模型无法自适应，导致性能下降甚至无法训练。这被称为“任意模态联合分类（AMJC）”问题。
- **背景**：视觉基础模型（如 ViT）在大规模自然图像上预训练后展现强大的泛化能力，通过少量微调即可适配下游任务。然而，将基础模型直接用于多模态遥感时，面临模态间特征差异大、模态重要性不平衡（“模态惰性”）等挑战。
- **核心目标**：提出一个统一的框架，能够接受任意数量的遥感模态输入（MS、HS、LiDAR、SAR），并利用预训练 ViT 实现与专用网络相当甚至更优的分类性能，同时保持低参数更新量。

## 2. 方法论：核心思想、关键技术细节

### 2.1 整体框架（T-APT）
- **两阶段架构**：
  1. **MAMF-FC**：基于 Mamba 的任意模态聚焦特征捕获模块，用于提取互补联合特征和模态特定先验知识。
  2. **TMPT**：文本引导的模态感知提示调优模块，将模态特定信息转化为文本引导的视觉提示，注入冻结的 ViT 中进行微调。

### 2.2 MAMF-FC 模块
- **统一编码器-解码器结构**：
  - 对各模态输入 \( X_{M_j} \) 通过卷积投影到统一通道数 \( C \)。
  - 使用特定 Mamba 块 (\( \Phi_{\text{Spe}} \)) 进行通道方向扫描，捕获模态特有特征；使用共享 Mamba 块 (\( \Phi_{\text{Sha}} \)) 进行空间多方向扫描，捕获模态间公共信息。
  - 通过动态融合注入和跨模态扫描对齐模块（\( \Phi_{\text{Align}} \)）融合多模态特征，得到联合表示 \( G \)。
  - 解码器对 \( G \) 进行线性映射得到各模态图像特征 \( F_{M_j-I} \)，并计算重建损失 \( L_{\text{rec}} \) 以保留模态信息。

### 2.3 TMPT 模块
- **双文本引导的模态平衡提示生成**：
  - 使用 CLIP 文本编码器对类别描述 (\( T_{\text{class}} \)) 和模态描述 (\( T_{j-\text{modality}} \)) 进行编码。
  - 通过 KL 散度对齐损失 \( L_{\text{align}} \) 和 L2 均值约束，消除不同模态图像特征的幅度差异，并将模态文本特征作为任务提示。
- **模态感知控制（MAC）**：
  - 在冻结 ViT 的每一层注意力中，将生成的提示（含模态特定图像特征和模态文本特征）拼接到 Key 和 Value 上，通过 Query 引导跨模态信息注入。
  - 在前馈网络（FFN）中引入低秩适配器（类似 LoRA），进一步适应下游任务。
- **分类头**：使用最后一个 Transformer 层的 [CLS] 令牌通过 MLP 输出类别预测。

### 2.4 训练目标
- 总损失 \( \mathcal{L} = \mathcal{L}_{\text{cls}} + \alpha_1 \mathcal{L}_{\text{rec}} + \alpha_2 \mathcal{L}_{\text{align}} \)，其中 \( \mathcal{L}_{\text{cls}} \) 为交叉熵损失，\( \alpha_1=0.1, \alpha_2=0.5 \)。

## 3. 实验设计

### 3.1 数据集
| 数据集 | 模态 | 尺寸 | 类别数 |
|--------|------|------|--------|
| Houston2013 | HSI, MSI, LiDAR | 349×1905 | 15 |
| MUUFL | HSI, LiDAR (DSM) | 325×220 | 11 |
| Augsburg | HS, SAR, LiDAR | 332×485 | 7 |

### 3.2 对比方法
- **Houston2013（HSI+LiDAR）**：HyperMLP, Sal2RN
- **Houston2013（HSI+MSI）**：MFT, MSFM
- **MUUFL（HSI+LiDAR）**：MSFE-IFN, AM3Net, AMSSE, M2FNet
- **Augsburg（HSI+LiDAR）**：S2ENet, FDNet
- **Augsburg（HSI+SAR）**：DSTD, MACN

### 3.3 评估指标
- 总体精度（OA）、平均精度（AA）、Kappa 系数（×100）。

## 4. 资源与算力

- **GPU**：单张 NVIDIA GeForce 3090。
- **训练参数**：epochs=250，学习率=1e-4，优化器=Adam。
- **模型参数量**：单模态~5M，双模态~8-9M，三模态~13M。
- **训练时间**：未明确给出具体时长，仅提到“250 epochs”。

## 5. 实验数量与充分性

- **主要对比实验**（表1）：在三个数据集的五种双模态组合以及两种三模态组合上，与9种以上最新方法对比，T-APT 在绝大多数组合下取得最好或接近最好的结果。
- **跨数据组合泛化实验**（表2）：将训练好的 T-APT 直接用于不同模态组合（如 Houston HSI+MSI 和 Augsburg HSI+SAR），与专用网络对比，专用网络性能显著下降甚至失效，而 T-APT 保持稳定。
- **消融实验**：
  - **损失函数消融**（表3）：分别移除 \( L_{\text{rec}} \)、\( L_{\text{align}} \) 或两者均移除，OA/AA/Kappa 均下降。
  - **组件替换消融**（图8）：将 Mamba 结构替换为其他编码、将 MAC 替换为仅 Adapter，性能均有下降。
  - **文本引导消融**（表4）：移除文本引导提示后，多模态分类性能下降，且单模态基线显示模态贡献不均衡被有效缓解。
- **单模态基线**（表4）：展示了 HS、MS、LiDAR、SAR 各自的独立分类性能，用于说明模态不平衡问题。
- **充分性评价**：实验覆盖了多种模态组合、多种数据集、充分的消融，指标全面，对比方法均为近年 SOTA，具有客观性和公平性。

## 6. 主要结论与发现

- T-APT 在任意模态组合下（两模态或三模态）均能达到与专用网络相当甚至更优的分类精度，验证了统一框架的有效性。
- 文本引导的提示机制有效缓解了模态惰性问题（即强弱模态不平衡导致弱模态被忽略），通过 KL 对齐和均值约束使不同模态贡献均衡。
- Mamba 架构在捕获跨模态依赖关系上优于传统编码结构，MAMF-FC 中的特定-共享交织扫描是关键设计。
- 冻结基础模型只调提示的方法显著降低了参数量和训练开销，同时保持了高性能。

## 7. 优点

1. **统一性强**：首次为任意模态遥感分类提出统一框架，无需针对不同组合重设计网络。
2. **高效微调**：仅通过提示和少量适配器参数（占总参数量很小比例）即可适配预训练 ViT，资源消耗低。
3. **模态平衡**：通过双文本引导（类别文本+模态文本）有效消除模态尺度差异，避免模型偏向强模态。
4. **创新结构**：MAMF-FC 中的共享-特定交织 Mamba 结构兼顾了通用特征和特有特征，对齐 Mamba 实现跨模态扫描。
5. **实验充分**：在三种数据集、五种模态组合、三模态组合上验证，对比最先进方法，消融实验系统全面。

## 8. 不足与局限

1. **模态覆盖不全**：仅测试了 MS、HS、LiDAR、SAR 四种遥感模态，未涉及高光谱-多光谱-雷达以外的模态（如红外、热红外、天文数据等）。
2. **文本描述依赖**：提示生成依赖 CLIP 文本编码器，若模态描述或类别描述不准确，可能影响性能；文本模板设计较为简化，未探索自动生成。
3. **超参数固定**：\( \alpha_1 \)、\( \alpha_2 \) 在所有实验中固定为 0.1 和 0.5，未进行系统调优或自适应调整。
4. **缺乏与其他统一多模态方法对比**：如直接与多模态基础模型（如 RemoteCLIP、GeoFM 等）比较；当前仅与针对固定组合的专用网络对比。
5. **任务单一**：仅针对像素级地物分类，未验证在分割、检测或变化检测等其他遥感任务上的泛化性。
6. **未报告训练时间**：虽然提到单 GPU 训练，但未给出具体小时数，难以评估效率。
7. **潜在偏差**：数据集空间分辨率、类别分布不均可能影响结果，文中未进行偏差分析。

（完）
