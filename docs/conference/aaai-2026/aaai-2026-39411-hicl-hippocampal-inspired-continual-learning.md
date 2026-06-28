---
title: "HiCL: Hippocampal-Inspired Continual Learning"
title_zh: HiCL：海马体启发的持续学习
authors: "Kushal Kapoor, Wyatt Mackey, Yiannis Aloimonos, Xiaomin Lin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39411/43372"
tags: ["query:continual"]
score: 9.0
evidence: 基于海马记忆机制的持续学习
tldr: 受海马体回路启发，提出HiCL双记忆持续学习架构，通过网格细胞编码、齿状回模式分离、CA3自关联记忆和DG门控专家混合机制有效缓解灾难性遗忘，在多个持续学习基准上显著优于现有方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续学习方法缺乏生物可解释性，且遗忘缓解效果有限。
method: 模仿海马电路，包括网格细胞编码、齿状回稀疏模式分离、CA3自关联记忆和DG门控混合专家。
result: 在多个持续学习基准上显著优于现有方法，验证了生物启发架构的有效性。
conclusion: 生物启发的双记忆架构为持续学习提供了有效且可解释的解决方案。
---

## Abstract
We propose HiCL, a novel hippocampal-inspired dual-memory continual learning architecture designed to mitigate catastrophic forgetting by using elements inspired by the hippocampal circuitry. Our system encodes inputs through a grid-cell-like layer, followed by sparse pattern separation using a dentate gyrus-inspired module with top-k sparsity. Episodic memory traces are maintained in a CA3-like autoassociative memory. Task-specific processing is dynamically managed via a DG-gated mixture-of-experts mechanism, wherein inputs are routed to experts based on cosine similarity between their normalized sparse DG representations and learned task-specific DG prototypes computed through online exponential moving averages. This biologically grounded yet mathematically principled gating strategy enables differentiable, scalable task-routing without relying on a separate gating network, and enhances the model's adaptability and efficiency in learning multiple sequential tasks. Cortical outputs are consolidated using Elastic Weight Consolidation weighted by inter-task similarity. Crucially, we incorporate prioritized replay of stored patterns to reinforce essential past experiences. Evaluations on standard continual learning benchmarks demonstrate the effectiveness of our architecture in reducing task interference, achieving near state-of-the-art results in continual learning tasks at lower computational costs.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
人工神经网络在顺序学习多个任务时，存在严重的**灾难性遗忘**——新知识会覆盖旧知识。相比之下，人脑依赖海马体实现终身学习，能够快速编码独特经历并长期保存。  
本文提出**HiCL**（Hippocampal-Inspired Continual Learning），一个受海马体三突触回路（DG → CA3 → CA1）启发的双记忆持续学习架构，旨在通过模拟生物记忆机制缓解灾难性遗忘，同时保持计算效率。

## 2. 论文提出的方法论

### 核心思想
将海马体的关键计算原理抽象为可训练的神经网络模块：
- **网格细胞编码**（Grid‑Cell Encoding）：通过4个并行的1×1卷积（带正弦激活和相位偏移）为输入特征添加结构化关系先验。
- **齿状回（DG）模式分离**：对编码后的特征施加 **Top‑k 稀疏化**（k=5%），产生准正交的稀疏码，减少任务间干扰。
- **CA3 模式补全**：用一个两层 MLP 对稀疏码进行非线性映射，近似吸引子网络的模式补全功能。
- **CA1 整合**：将 DG 稀疏码与 CA3 输出拼接，形成最终表示。
- **DG 门控混合专家（MoE）**：每个专家拥有独立的 DG 模块，输入经所有 DG 模块并行处理后，计算每个专家的稀疏码与其**原型**（通过指数移动平均 EMA 更新）的余弦相似度，作为路由得分。支持 soft / hard / top‑2 等多种门控方式。
- **两阶段训练**：
  - **Phase I（专门化）**：分类损失 + 类内/类间对比损失（L_intra）+ 特征蒸馏 + EWC + 稀疏正则 + 重放损失。
  - **Phase II（巩固）**：冻结非 DG 参数，使用原型对比损失进一步拉大同任务/异任务表示的差异。

### 关键技术细节
- Grid‑Cell 层：\( g_m = \sin(W_m f + \phi_m) \)，M=4。
- DG 层：\( z = \text{ReLU}(W_{DG}g + b_{DG}) \)，然后 LayerNorm + TopK（k=5%）。
- CA3：两层 MLP，输入 DG 稀疏码，输出模式补全后的表示。
- 原型更新：\( u_i \leftarrow (1-\mu)u_i + \mu p^{(i)}_{\text{sep}} \)，\(\mu=0.01\)。
- 训练使用 Adam，CIFAR‑10 每任务训练 10 epochs，Tiny‑ImageNet 每任务 20 epochs。

## 3. 实验设计
- **数据集**：
  - **Split CIFAR‑10**：10 类分成 5 个任务，每任务 2 类。
  - **Split Tiny‑ImageNet**：200 类分成 10 个任务，每任务 20 类。
- **评测指标**：
  - Task‑IL 准确率 \( A_T \)（给出任务 ID 时的分类准确率）。
  - Class‑IL 准确率 \( A_C \)（无任务 ID，在所有已见类中分类）。
  - 计算效率：单次前向推理的 Mega‑FLOPs。
- **对比方法**：
  - 正则化方法：SGD（Fine‑tuning）、LwF、SI。
  - 重放方法：A‑GEM、ER、DER++。
  - 架构/混合方法：iCaRL、FDR、HAL、E2Net、SparCL。
  - 上界：Joint 训练（所有任务数据一起训练）。
- **设置**：缓冲大小分别为 200 和 500 样本/任务；骨干网络为 LeNet（CIFAR‑10）或 4 层 CNN（Tiny‑ImageNet）；报告均值±标准差。

## 4. 资源与算力
**论文未明确说明**使用的 GPU 型号、数量及总训练时长。仅提及优化器为 Adam，每个任务训练 10 或 20 epochs。这在计算资源透明度上是一个不足。

## 5. 实验数量与充分性
- **主要实验（Table 1）**：在 2 个数据集 × 2 种缓冲大小下，对比了 10 余种基线方法，报告了 Task‑IL、Class‑IL 和 FLOPs。
- **内存鲁棒性实验（Table 2）**：分析了缓冲大小从 100 到 5000 对性能的影响。
- **消融实验（Table 3）**：分别移除对比损失、DG 门控、Top‑k 稀疏、CA1 整合、EMA 更新、CA3 模块、EWC 等关键组件，验证每个成分的必要性。
- **可视化分析（Figure 3–5）**：展示了路由矩阵和 t‑SNE 特征分离效果。
- **评价**：实验覆盖面较广，消融完整，对比基准类型丰富，且结果重复（多次运行取均值与标准差），具备**较高的客观性与公平性**。但仅局限于两个小规模图像分类数据集，缺乏对更大规模图像（如 ImageNet‑Split）或非视觉任务（如 NLP、强化学习）的验证。

## 6. 论文的主要结论与发现
- HiCL 在 Task‑IL 和 Class‑IL 准确率上接近或超越现有方法，同时计算成本（FLOPs）显著更低（例如 Small 模型在 CIFAR‑10 上仅 16.3 MFLOPs）。
- DG 层的**稀疏模式分离**是实现有效路由和抗遗忘的核心：类间余弦相似度显著低于类内（Figure 3）。
- **两阶段训练**（Phase I 专门化 + Phase II 对比巩固）能进一步提升 Class‑IL 性能。
- **记忆鲁棒性**：即使缓冲大小从 500 降至 100，Task‑IL 准确率仅下降 2.7 个百分点，说明 HiCL 对缓冲大小不敏感。

## 7. 优点
- **生物可解释性强**：模块设计紧密映射海马体三突触回路，为持续学习提供了神经科学依据。
- **路由无需独立门控网络**：基于余弦相似度的 DG 门控简洁高效，且可微分。
- **条件计算**：推理时只需激活一个专家（或少数专家），大幅降低计算开销。
- **消融充分**：清晰展示了每个组件（DG 稀疏、CA1、CA3、EWC、对比损失等）的贡献，方法透明。
- **兼容性**：可与 EWC、重放、蒸馏等经典持续学习技术无缝结合。

## 8. 不足与局限
- **依赖任务边界**：Phase I 训练需要任务标签和明确的任务边界，不适用于完全无监督的类增量场景。
- **超参数固定**：稀疏率 \( k=5\% \) 和专家数（5/10）在所有实验中使用相同值，未提供自适应调整机制，可能不适用于异构任务。
- **路由鲁棒性**：约 5% 的样本因 DG 码重叠导致路由混淆，虽影响小但存在改进空间。
- **实验域局限**：仅在两个小规模视觉数据集上评估，未验证在更大规模图像数据集（如完整 ImageNet）、语言或强化学习等领域的有效性。
- **计算资源未报告**：未披露 GPU 型号、数量、总训练时长，影响可复现性评估。
- **骨干网络简单**：实验中仅使用 LeNet 或小型 CNN，未验证在 ResNet / ViT 等现代架构上的表现。

（完）
