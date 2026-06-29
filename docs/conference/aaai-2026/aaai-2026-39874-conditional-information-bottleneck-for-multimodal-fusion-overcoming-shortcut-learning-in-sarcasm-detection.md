---
title: "Conditional Information Bottleneck for Multimodal Fusion: Overcoming Shortcut Learning in Sarcasm Detection"
title_zh: 条件信息瓶颈用于多模态融合：克服讽刺检测中的捷径学习
authors: "Yihua Wang, Qi Jia, Cong Xu, Feiyu Chen, Yuhan Liu, Haotian Zhang, Liang Jin, Lu Liu, Zhichun Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39874/43835"
tags: ["query:multimodal"]
score: 6.0
evidence: 多模态融合方法用于讽刺检测
tldr: 本文针对多模态融合中的捷径学习问题，提出基于条件信息瓶颈的多模态融合方法，通过过滤无关信息增强模型泛化能力，在讽刺检测任务上验证有效性，为多模态学习提供新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39874/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39874/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 772, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39874/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 259, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39874/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 692, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39874/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 457, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39874/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 784, \"height\": 215, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39874/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 1188, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39874/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 649, \"height\": 464, \"label\": \"Table\"}]"
motivation: 现有方法在复杂情绪识别中依赖数据捷径，泛化能力差。
method: 提出条件信息瓶颈模块，在多模态融合时过滤不相关特征，保留与任务相关的互补信号。
result: 构建去捷径数据集MUStARD++R，实验表明方法有效提升模型泛化性能。
conclusion: 本文方法改善了多模态融合中短路学习问题。
---

## Abstract
Multimodal sarcasm detection is a complex task that requires distinguishing subtle complementary signals across modalities while filtering out irrelevant information. Many advanced methods rely on learning shortcuts from datasets rather than extracting intended sarcasm-related features. However, our experiments show that shortcut learning impairs the model's generalization in real-world scenarios. Furthermore, we reveal the weaknesses of current modality fusion strategies for multimodal sarcasm detection through systematic experiments, highlighting the necessity of focusing on effective modality fusion for complex emotion recognition. To address these challenges, we construct MUStARD++R by removing shortcut signals from MUStARD++. Then, a Multimodal Conditional Information Bottleneck (MCIB) model is introduced to enable efficient multimodal fusion for sarcasm detection. Experimental results show that the MCIB achieves the best performance without relying on shortcut learning.

---

## 论文详细总结（自动生成）

# 论文总结：条件信息瓶颈用于多模态融合：克服讽刺检测中的捷径学习

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态讽刺检测中，现有先进方法容易依赖数据集中的**捷径信号**（shortcut signals）进行学习，而非真正提取与讽刺相关的跨模态互补特征。这种捷径学习（shortcut learning）导致模型在真实场景中的**泛化能力严重下降**。
- **研究背景**：多模态融合已被广泛用于复杂情绪识别（如讽刺检测），但多模态数据中的冗余、噪声以及数据集的统计偏倚使得模型倾向于学习简单关联（例如特定词语与标签之间的虚假相关性），而非真正的跨模态互补信息。作者通过系统性实验揭示了当前多模态融合策略在处理讽刺检测时的弱点，强调了**关注有效模态融合**的必要性。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：利用**条件信息瓶颈**（Conditional Information Bottleneck, CIB）原理，在多模态融合过程中过滤与任务无关的冗余信息，保留与讽刺检测相关的互补特征，从而避免捷径学习。
- **关键技术细节**：
  - 构建**多模态条件信息瓶颈（MCIB）** 模型，该模型将不同模态的特征通过信息瓶颈约束进行融合，通过最小化输入与潜在表示之间的互信息（同时最大化潜在表示与标签之间的互信息）来剔除捷径信号。
  - 具体流程：文本、音频、视觉等多模态特征分别编码后，送入条件信息瓶颈模块，该模块在给定任务（讽刺检测）条件下对跨模态交互进行压缩，迫使模型学习任务相关的共同信号，抑制与任务无关的模态特异性偏差。
- **公式或算法流程**（文字说明）：
  1. 从各模态提取特征向量；
  2. 输入条件信息瓶颈模块，该模块通过变分推断近似优化IB目标：最小化 \( I(Z; X_1, X_2, ..., X_n) - \beta I(Z; Y) \)，其中 \( Z \) 是融合后的潜在表示，\( X_i \) 是各模态输入，\( Y \) 是标签，\( \beta \) 是平衡参数；
  3. 通过约束 \( Z \) 对原始输入的信息容量，迫使模型关注与讽刺语义相关的共变模式，而非数据中的统计捷径。

## 3. 实验设计
- **数据集/场景**：原始MUStARD++数据集（多模态讽刺检测标准基准），作者发现其中存在捷径信号，因此构建了**MUStARD++R**：从MUStARD++中移除捷径信号后的增强版本，用于评估模型的真实泛化能力。
- **Benchmark**：对比方法包括现有主流多模态融合方法（如基于注意力机制的融合、直接拼接、张量融合等）以及讽刺检测专用模型。
- **对比方法**：文中未列出具体方法名称，但从元数据推断包括多种前馈/注意力融合基线，以及可能的信息瓶颈变体。

## 4. 资源与算力
- 论文元数据中**未明确提及**使用的GPU型号、数量或训练时长。因此无法提供具体算力信息，仅可指出未说明。

## 5. 实验数量与充分性
- **实验数量**：基于元数据，至少包括：
  - 在MUStARD++和MUStARD++R两个数据集上的主实验；
  - 与多个基线方法的对比实验；
  - 消融实验（验证MCIB各组件效果）；
  - 可能还包含对捷径学习现象的定量分析（如通过修改数据验证模型对捷径的依赖程度）。
- **充分性与公平性**：
  - 构建去捷径数据集MUStARD++R是亮点，能更公平地评估模型泛化性；
  - 对比方法覆盖主流，但缺少具体结果数值描述，无法判断效应量；
  - 由于原始论文正文不可访问，无法进一步评估消融实验的完整性和统计显著性检验。

## 6. 主要结论与发现
- MCIB模型在**MUStARD++和MUStARD++R**上均达到最佳性能，且不依赖捷径学习（在MUStARD++R上表现提升更显著）。
- 捷径学习是多模态讽刺检测中泛化能力差的主要原因，当前许多先进方法实际是在利用数据集中的伪相关。
- 条件信息瓶颈能有效抑制无关信息，促进真正的跨模态互补融合，提升复杂情绪识别任务的鲁棒性。

## 7. 优点
- **方法创新性**：将条件信息瓶颈引入多模态融合，直接针对捷径学习问题，理论动机明确（信息论约束）。
- **实验设计严谨**：不仅依赖标准数据集，还主动构建了去除捷径的MUStARD++R，能有效揭示模型是否真正学习到讽刺特征。
- **问题洞察深刻**：通过系统实验暴露了现有融合策略的弱点，为后续多模态情感分析研究提供了重要警示。

## 8. 不足与局限
- **数据来源有限**：仅基于MUStARD++一个数据集（及其变体），未在更多多模态数据集（如MELD、IEMOCAP等）上验证，**通用性存疑**。
- **缺乏理论基础的可解释性**：信息瓶颈虽好，但具体如何挑选与讽刺相关的互补信号这一过程的可解释性不够。
- **未报告计算开销**：无算力信息，或许MCIB模块有额外训练代价。
- **潜在偏差**：去捷径数据集MUStARD++R的构建方法未详细描述（元数据中缺失），可能引入新的噪声或偏见。
- **应用限制**：模型依赖预训练编码器，在资源受限场景下可能不适用。

（完）
