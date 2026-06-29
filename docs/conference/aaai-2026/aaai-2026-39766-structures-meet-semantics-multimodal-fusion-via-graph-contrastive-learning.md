---
title: "Structures Meet Semantics: Multimodal Fusion via Graph Contrastive Learning"
title_zh: 结构与语义相遇：基于图对比学习的多模态融合
authors: "Jiangfeng Sun, SiHao He, Zhonghong Ou, Meina Song"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39766/43727"
tags: ["query:multimodal"]
score: 5.0
evidence: 基于图对比学习的多模态融合用于情感分析
tldr: 针对现有方法忽略模态结构依赖和语义对齐的问题，提出SSU框架，通过动态构建语法引导的文本图和文本引导的注意力机制，系统整合模态结构信息和跨模态语义，在多个基准上提升了多模态情感分析的性能与鲁棒性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 876, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1817, \"height\": 866, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 886, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 885, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 884, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 883, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39766/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1841, \"height\": 522, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39766/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1832, \"height\": 806, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39766/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 818, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39766/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 887, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39766/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 873, \"height\": 865, \"label\": \"Table\"}]"
motivation: 现有方法忽略模态特定的结构依赖和语义错位。
method: 提出SSU框架，动态构建模态特定图并利用文本引导注意力实现结构化语义对齐。
result: 在情感分析任务上显著提升性能、可解释性和鲁棒性。
conclusion: SSU为多模态融合提供了结构-语义统一的新范式。
---

## Abstract
Multimodal sentiment analysis (MSA) aims to infer emotional states by effectively integrating textual, acoustic, and visual modalities. Despite notable progress, existing multimodal fusion methods often neglect modality-specific structural dependencies and semantic misalignment, limiting their quality, interpretability, and robustness. To address these challenges, we propose a novel framework called the Structural-Semantic Unifier (SSU), which systematically integrates modality-specific structural information and cross-modal semantic grounding for enhanced multimodal representations. Specifically, SSU dynamically constructs modality-specific graphs by leveraging linguistic syntax for text and a lightweight, text-guided attention mechanism for acoustic and visual modalities, thus capturing detailed intra-modal relationships and semantic interactions. We further introduce a semantic anchor, derived from global textual semantics, that serves as a cross-modal alignment hub, effectively harmonizing heterogeneous semantic spaces across modalities. Additionally, we develop a multi-view contrastive learning objective that promotes discriminability, semantic consistency, and structural coherence across intra- and inter-modal views. Extensive evaluations on two widely-used benchmark datasets, CMU-MOSI and CMU-MOSEI, demonstrate that SSU consistently achieves state-of-the-art performance while significantly reducing computational overhead compared to prior methods. Comprehensive qualitative analyses further validate SSU’s interpretability and its ability to capture nuanced emotional patterns through semantically-grounded interactions.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 核心问题与整体含义（研究动机和背景）
多模态情感分析（MSA）旨在融合文本、语音和视觉三种模态来推断情感状态。现有方法（尤其是基于注意力的融合）通常将每个模态视为简单的特征序列，忽略了模态**内在的结构依赖**（如文本的语法依存、音频/视频的时间连贯性）以及跨模态之间的**语义错位**。这些不足导致表示质量、可解释性和鲁棒性受限。为此，论文提出 **SSU（Structural-Semantic Unifier）** 框架，系统整合**模态特定的结构信息**和**跨模态语义对齐**，以提升多模态情感分析性能。

## 2. 方法论：核心思想、关键技术细节
**核心思想**：通过图结构显式建模每个模态的内部结构，并利用从全局文本语义中提取的“语义锚”作为跨模态对齐枢纽，再配合多视图对比学习目标，实现结构化与语义的统一。

**关键技术细节**：
- **模态特定图构建**：
  - **文本图 G_t**：基于句法依存树构建，每个词为节点，语法关系为有向边。
  - **音频/视觉图 G_a, G_v**：通过文本引导的注意力机制实现。首先使用文本作为查询，通过交叉注意力增强非文本表示（公式1-2）；然后计算模态段与文本之间的语义相似度矩阵 S_m（公式3），经softmax归一化和对称化得到初始邻接矩阵，再通过自适应稀疏化（基于均值和标准差计算动态阈值 τ_m）去除噪声边（公式4-5）。最终得到稀疏、语义相关的图结构。
- **语义锚集成**：
  - 对文本表示 X_t 进行平均池化得到全局语义锚 z_a（公式6）。
  - 将 z_a 作为共享节点加入每个模态图，并通过注意力计算锚节点与各模态节点的边权重 β_mi（公式7），从而将异构模态图统一到同一语义空间。
  - 进一步构建融合图 G_f，包含所有模态节点和锚节点，保留模态内部、锚-模态以及高语义相似度的跨模态边。
- **多视图对比学习目标**：
  - **原始视图**（结构感知）：使用共享GAT对每个模态图G_m编码得到 z_ori。
  - **增强视图**：对原始图施加随机扰动（边增删），再经同一GAT得到 z_aug。
  - **融合视图**：使用另一GAT对融合图G_f编码得到 z_fuse。
  - 三个损失：
    - 监督区分损失 L_sup：对 z_ori 进行情感分类的交叉熵（公式8）。
    - 结构一致性损失 L_self：z_ori 与 z_aug 之间的对比学习（公式9）。
    - 语义对齐损失 L_align：z_fuse 与 z_ori 的均方误差（公式10）。
  - 总损失：L = L_reg + λ_sup L_sup + λ_self L_self + λ_align L_align（公式11），其中 L_reg 为回归损失。

## 3. 实验设计
- **数据集**：
  - **CMU-MOSI**：2,199个话语（来自93个视频），情感得分范围[-3,3]。
  - **CMU-MOSEI**：23,453个话语（来自1,000+说话人）。
- **评估指标**：二分类准确率（ACC2）、F1分数、七分类准确率（ACC7）、平均绝对误差（MAE）。
- **对比方法**：
  - **基于注意力的方法**：CIA、MAT、TBJE、GATE、MPT、UniMSE、SPECTRA、MMML+FusionNet、CMPT。
  - **基于图的方法**：MMGraph、GraphCAGE、CJTF-BERT、MoSARe。
  - **大语言模型（LLM）基的图构造**：LLaMA-3.1-8B、Qwen-2.5-7B、Mistral-7B、Gemma-2B（均为8-bit量化，用离线提示构造图）。
- **训练细节**：固定种子68，batch size 128，序列长度128，隐藏大小128，学习率1e-5。

## 4. 资源与算力
- **硬件**：8块 NVIDIA A100 GPU（共512 GB RAM）。
- **软件**：PyTorch 1.8.2，CUDA 11.1，spaCy 3.5.0。
- **模型参数**：SSU仅0.3B参数（约3亿）。
- **训练时长**：论文未明确给出具体训练时长，但报告了每批次的图构造时间：SSU约0.015秒/批次，远快于LLM基方法（如LLaMA-3.1-8B需8.45秒/批次）。

## 5. 实验数量与充分性
论文进行了多组实验，覆盖：
- **主结果比较**：在CMU-MOSI和CMU-MOSEI上与12种代表性方法对比（表1）。
- **与LLM基图构造对比**：在相同数据集上与4种LLM对比（表2）。
- **消融研究**：
  - 移除语义锚（表3）。
  - 不同对比损失组合（表4）。
  - 损失面可视化（图5）。
- **案例研究**：预测可视化（图6）和跨模态注意力图（图7）。
- **模型效率对比**：参数量和构建时间（图4）。

实验设计较为充分，主表对比了两种主流范式（注意力和图方法），消融从不同组件到不同损失逐一验证，且与LLM进行了公平比较（相同输入配置）。结论具有较高可信度。

## 6. 主要结论与发现
- SSU在所有指标上均达到**新SOTA**：在MOSI上ACC2达89.32%，MOSEI上ACC2达87.93%，MAE显著降低。
- **语义锚**对性能至关重要，移除后MOSI上F1下降2.42%，并导致损失面更尖锐（优化不稳定）。
- **多视图对比损失**各组件互补：L_align增强跨模态一致，L_sup提升类别可分性，L_self提高结构鲁棒性；完整组合最优。
- SSU比LLM基方法**快两个数量级**（0.015s vs 8.45s），且参数少得多（0.3B vs 7B+），但性能更优。
- 案例研究表明SSU能聚焦情感关键词并正确对齐非语言信号，具备**可解释性**。

## 7. 优点
- **结构-语义统一**：首次在同一框架内显式建模模态内部结构并实现跨模态语义对齐，切入点新颖。
- **轻量高效**：仅0.3B参数，图构建在线完成且耗时极短，适合实际部署。
- **动态与鲁棒**：图结构非静态，采用自适应稀疏化与语义锚，抵抗噪声。
- **可解释性强**：注意力可视化清晰显示跨模态对齐效果，有助于理解模型行为。
- **消融全面**：逐项验证了各模块和损失函数的必要性。

## 8. 不足与局限
- **数据集通用性**：仅在两个英文情感数据集（CMU-MOSI/MOSEI）上验证，缺乏对其他语言、场景（如多模态讽刺检测、视频对话）的测试。
- **图构建对文本质量的依赖**：音频/视频图依赖文本引导，若文本转录有误或简短，可能影响图质量。
- **未考虑模态缺失**：论文假设所有模态完整，未讨论实际中常见的一种或多种模态缺失的情况（该方向已有相关工作，如Lin & Hu 2023）。
- **超参数敏感性**：对比损失权重 λ_sup、λ_self、λ_align 需调参，论文未提供详细敏感性分析。
- **无跨文化/跨语言验证**：情感表达存在文化差异，当前模型可能对非英语或非西方文化数据泛化不足。
- **仅二维情感**：关注情感分类（正/负/1-7等级），未涉及复杂情感（如混合情绪、细粒度情绪类别）。

（完）
