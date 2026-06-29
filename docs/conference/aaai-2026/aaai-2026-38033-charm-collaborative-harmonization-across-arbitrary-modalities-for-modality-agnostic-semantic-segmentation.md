---
title: "CHARM: Collaborative Harmonization Across Arbitrary Modalities for Modality-Agnostic Semantic Segmentation"
title_zh: CHARM：跨任意模态的协作调和实现模态无关语义分割
authors: "Lekang Wen, Jing Xiao, Liang Liao, Jiajun Chen, Mi Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38033/41995"
tags: ["query:multimodal"]
score: 5.0
evidence: 跨模态协作的模态无关语义分割
tldr: 针对模态无关语义分割中显式对齐会稀释模态特性的问题，提出CHARM互补学习框架，通过互感知单元实现隐式对齐，保留各模态独特优势，在多种模态组合下实现鲁棒的场景理解。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1801, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1818, \"height\": 984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 878, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1799, \"height\": 655, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 852, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 871, \"height\": 790, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38033/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 860, \"height\": 983, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38033/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1839, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38033/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1837, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38033/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 688, \"height\": 188, \"label\": \"Table\"}]"
motivation: 显式特征对齐会破坏模态间的互补性。
method: 提出互感知单元，通过窗口式跨模态交互实现隐式内容对齐。
result: 在多种模态组合下取得鲁棒的分割性能，优于现有方法。
conclusion: CHARM为模态无关语义分割提供了有效的协作调和框架。
---

## Abstract
Modality-agnostic Semantic Segmentation (MaSS) aims to achieve robust scene understanding across arbitrary combinations of input modality. Existing methods typically rely on explicit feature alignment to achieve modal homogenization, which dilutes the distinctive strengths of each modality and destroys their inherent complementarity. To achieve cooperative harmonization rather than homogenization, we propose CHARM, a novel complementary learning framework designed to implicitly align content while preserving modality-specific advantages through two components: (1) Mutual Perception Unit (MPU), enabling implicit alignment through window-based cross-modal interaction, where modalities serve as both queries and contexts for each other to discover modality-interactive correspondences; (2) A dual-path optimization strategy that decouples training into Collaborative Learning Strategy (CoL) for complementary fusion learning and Individual Enhancement Strategy (InE) for protected modality-specific optimization. Experiments across multiple datasets and backbones indicate that CHARM consistently outperform the baselines, with significant increment on the fragile modalities. This work shifts the focus from model homogenization to harmonization, enabling cross-modal complementarity for true harmony in diversity.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：模态无关语义分割（MaSS）旨在处理任意输入模态组合下的鲁棒场景理解。现有方法大多依赖显式特征对齐（如KL散度损失）实现模态同质化，但这会稀释各模态的独特优势，破坏其固有互补性。例如，RGB的丰富纹理信息被稀释以匹配LiDAR的无彩色模式，而LiDAR的精确空间线索被抑制。
- **整体含义**：本文提出从“同质化”转向“协作调和”（harmonization），即通过隐式对齐保留模态特定优势，同时实现有效协作。关键原则是：模态应通过相互理解来协调，且每个模态的互补特征应被主动激发而非被统一对齐约束压制。

## 2. 方法论

### 核心思想
- **互补学习框架**：CHARM通过两个核心组件实现隐式对齐与模态特异性保留：
  1. **互感知单元（MPU）**：基于窗口的跨模态注意力，每个模态同时作为查询（Query）和上下文（Key/Value）为其他模态服务，发现模态间交互对应关系。
  2. **双路径优化策略**：
     - **协作学习策略（CoL）**：所有模态通过MPU联合学习，利用鲁棒性评估器（RE）计算逐像素鲁棒性得分，加权融合得到初始语义特征，然后通过MPU迭代细化，实现互补融合。
     - **个体增强策略（InE）**：基于软最小化（SoftMin）采样概率，优先采样脆弱模态的完整特征，通过MPU进行保护性学习，激发每个模态的潜力。

### 关键技术细节
- **MPU结构**：将模态特征和语义特征各划分为窗口，每个窗口内，模态特征生成K和V，语义特征生成Q，进行窗口多头注意力（W-MHA），并通过移位窗口实现跨窗口连接。多个MPU块堆叠实现逐步精炼。
- **语义投影器（SP）**：每个模态特有的模块，由三层深度卷积（卷积核11×11、7×7、3×3）和一层1×1逐点卷积组成，将模态特征投影到共享语义空间。
- **鲁棒性评估器（RE）**：一个1×1逐点卷积，输出每个模态在每个像素的鲁棒性得分。
- **损失函数**：CoL和InE分别使用交叉熵损失，总损失为二者加权和。训练时这两个路径成对运行。

### 推理流程
- 仅使用CoL路径，将模态特征通过SP和RE得到初始语义特征，再经MPU迭代处理，最终由SegHead输出预测。

## 3. 实验设计

### 数据集
- **DELIVER**：通用场景，包含RGB、Depth、LiDAR、Event四种模态。
- **MCubeS**：材料分割场景，包含RGB、NIR、DoLP、AoLP四种模态。
- **MUSES**：驾驶场景，包含RGB、Event、LiDAR三种模态。

### Benchmark与对比方法
- 对比方法：CMNeXt（多模态分割基线）、Any2Seg、MAGIC、AnySeg（均为MaSS方法）。
- 骨干网络：Segformer的MiT-B0和MiT-B2，部分实验还使用了PVTv2和Swin Transformer（补充材料中）。
- 评估指标：平均、Top-1、Last-1 mIoU（分别衡量整体性能、最佳互补效果、脆弱模态激活程度）。

## 4. 资源与算力

论文中**未明确说明**使用的GPU型号、数量及训练时长。仅在补充材料中提及部分实验设置，但未给出具体算力信息。

## 5. 实验数量与充分性

- **主实验**：在三个数据集、两种骨干网络上进行了系统对比，包括所有模态组合的详细mIoU结果（见补充材料）。
- **消融实验**：包含5组逐步组件集成分析（从直接相加融合到完整框架）、MPU与显式对齐的对比、InE中不同采样策略对比（Softmax、Uniform、Softmin）。
- **可视化分析**：Grad-CAM特征可视化（图7、图8）验证了MPU对脆弱模态的增强效果。
- **充分性评价**：实验覆盖了多种模态数量和组合类型，消融实验结构清晰，对比方法均为最先进方法，具有客观性和公平性。未进行跨骨干网络的全量对比，但在补充材料中提供了额外骨干结果，总体充分。

## 6. 主要结论与发现

- CHARM在所有数据集和骨干网络上**一致超越**现有方法，尤其显著提升了脆弱模态（Event、LiDAR）的性能。
- 在DELIVER（MiT-B2）上，平均mIoU比Any2Seg提高**9.92%**，Last-1 mIoU提升**28.04%**。
- MPU实现隐式对齐，避免了显式对齐导致的模态特性稀释；CoL和InE双路径平衡了协作学习和个体增强，使脆弱模态得到保护性提升。
- 特征可视化表明，MPU使脆弱模态在浅层减少噪声、在深层聚焦语义区域，而鲁棒模态保留其纹理优势，实现真正的“调和”而非“同质化”。

## 7. 优点

- **方法创新**：首次提出用隐式互感知取代显式对齐，保留模态互补性，概念新颖且有效。
- **双路径设计**：CoL和InE分别针对整体协作和个体保护，逻辑清晰且互补。
- **模块通用性**：MPU可接受任意数量和类型的模态，具有强泛化能力。
- **实验结果充分**：在多个数据集、多种骨干和大量消融实验中均验证了有效性，可视化分析有力支撑了论点。
- **指标选择**：使用Average、Top-1、Last-1分别评估整体、最优和最差组合，全面反映方法性能。

## 8. 不足与局限

- **未报告训练资源**：缺少GPU型号、数量及训练时间等算力信息，不利于实际可行性评估。
- **实验覆盖有限**：仅在三种数据集和两种骨干上进行了主实验，缺乏在更大规模多样场景（如自动驾驶多传感器真实数据）上的验证。
- **未讨论推理速度**：MPU的窗口注意力机制可能带来额外计算开销，但未报告推理延迟或参数量。
- **偏差风险**：SoftMin采样策略虽提升脆弱模态，但可能过度偏向脆弱模态而忽略鲁棒模态的贡献，文中未讨论这种权衡的边界条件。
- **应用限制**：模型假设训练时全部模态可用，仅推理时缺失；实际场景中传感器可能长期缺失，长期缺失的影响未被探索。
- **可复现性**：未提供代码链接，仅依赖论文描述，可能影响其他研究者复现。

（完）
