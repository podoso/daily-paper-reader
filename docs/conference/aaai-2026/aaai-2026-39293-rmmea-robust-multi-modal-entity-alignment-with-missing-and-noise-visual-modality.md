---
title: "rMMEA: Robust Multi-Modal Entity Alignment with Missing and Noise Visual Modality"
title_zh: rMMEA：鲁棒的多模态实体对齐方法，处理缺失和噪声视觉模态
authors: "Lingbing Guo, Zhuo Chen, Yichi Zhang, Wenbin Guo, Haonan Yang, Zhao Li, Zirui Chen, Xin Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39293/43254"
tags: ["query:multimodal"]
score: 6.0
evidence: 处理视觉模态缺失的多模态实体对齐方法
tldr: 针对多模态实体对齐中视觉模态缺失和噪声这一关键挑战，现有方法简单使用虚拟向量导致性能下降。本文提出rMMEA，通过基于排名的知识蒸馏和互信息估计来恢复缺失视觉信息并增强噪声鲁棒性。实验结果表明，在多个实体对齐基准上，rMMEA显著优于先前方法，尤其在不完整模态场景下表现突出。该工作为多模态表示学习中缺失模态问题提供了一种有效且鲁棒的解决方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多模态实体对齐中视觉模态常缺失，现有方法用虚拟向量导致训练和推理受损。
method: 提出rMMEA，利用基于排名的知识蒸馏优化缺失模态表示，并结合互信息估计增强对噪声的鲁棒性。
result: 在标准实体对齐数据集上，rMMEA在处理视觉缺失和噪声时显著优于基线方法。
conclusion: rMMEA有效提升了多模态实体对齐在现实不完整数据场景下的鲁棒性和准确性。
---

## Abstract
Recently, multi-modal embedding methods have flourished in entity alignment. As state-of-the-art approaches evolve rapidly, visual modality (i.e., images) missing emerges as a critical challenge. While visual modality typically offers the most informative signals in multi-modal entity alignment (MMEA), it is frequently unavailable for many entities. The existing methods commonly use dummy vectors to represent visual-missing embeddings, which negatively impacts both model training and inference. In this paper, we propose robust multi-modal entity alignment (rMMEA), which leverages ranking-based knowledge distillation and mutual information (MI) estimation to address missing modalities while enhancing noise robustness. Unlike conventional teacher-student distillation that requires the student to replicate teacher outputs, our rMMEA learns soft rankings from pure and complete modality sides while capturing implicit key semantics of teacher embeddings through mutual information maximization, allowing rMMEA to avoid strict point-to-point alignment. The experimental results across multiple benchmarks and settings demonstrate that rMMEA significantly outperforms the state-of-the-art anti-modality-missing methods in terms of effectiveness and efficiency.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：多模态实体对齐（MMEA）中，视觉模态（图像）经常缺失或含有噪声。现有方法通常使用零向量或随机向量作为缺失视觉实体的嵌入，导致模型训练和推理质量下降，降低实体对判别能力。
- **研究动机**：真实知识图谱（如DBPedia）中超过20%的实体缺乏图像链接；现有生成式抗缺失方法（如UMAEA）需要多阶段训练和额外参数，效率低；传统知识蒸馏方法强制学生模仿教师点对点输出，面临学习鸿沟（如从0.36到0.87的差距）。
- **整体含义**：提出一种鲁棒、高效、无需外部数据和多阶段训练的MMEA方法，同时处理模态缺失和噪声，提升实体对齐的准确性和鲁棒性。

## 2. 论文提出的方法论

### 核心思想
- 采用**自蒸馏**（self-distillation）框架，教师模型为完整模态（含视觉）的输出，学生模型为视觉缺失时的输出，但避免点对点匹配。
- 提出**基于排名的知识蒸馏**（Ranking-based Knowledge Distillation），让学生学习实体候选的相对排名关系，而非精确概率值。
- 结合**互信息估计**（Mutual Information Estimation），捕获教师嵌入中的隐式语义，而非直接对齐维度。

### 关键技术细节
#### (1) 基于排名的知识蒸馏
- 给定源实体 \(e_i^1\)，其与目标候选实体 \(e_j^2\) 的相似度分数 \(S(e_i^1, e_j^2)\)，定义排名函数：
  \[
  r(e_j^2 | e_i^1) = 1 + \sum_{e_k \in \mathcal{N}_i^2} \sigma(S(e_i^1, e_k^2) - S(e_i^1, e_j^2))
  \]
  其中 \(\sigma(x) = \frac{1}{1 + \beta e^{-\min(\alpha x, x)}}\)，\(\alpha, \beta\) 控制温度，使排名函数可微。
- 蒸馏损失：最小化学生排名 \(r_s\) 与教师排名 \(r_t\) 的绝对差：
  \[
  L_{rd} = \sum_{e_j^2 \in \mathcal{N}_i^2 \cup \{e_i^2\}} |r_s(e_j^2|e_i^1) - r_t(e_j^2|e_i^1)|
  \]

#### (2) 互信息估计
- 使用对比学习框架，将学生嵌入 \(e_{i,s}\) 和教师嵌入 \(e_{i,t}\) 视为正对，负样本从教师嵌入的负集合 \(\mathcal{N}_{i,t}\) 中采样。
- 损失函数（InfoNCE形式）：
  \[
  L_{mi} = -\log \frac{f_{mi}(e_{i,s}, e_{i,t})}{f_{mi}(e_{i,s}, e_{i,t}) + \sum_{e_{j,t} \in \mathcal{N}_{i,t}} f_{mi}(e_{i,s}, e_{j,t})}
  \]
  其中 \(f_{mi}(e_s, e_t) = \exp(e_s^T W_m e_t + b_m)\)。

#### (3) 联合训练
- 总损失：\(L = L_{main} + L_{rd} + L_{mi}\)，所有目标联合优化，无需多阶段。
- 通过随机采样训练集中部分实体构造“缺失模态”数据，实现自监督。

#### (4) 噪声鲁棒性
- 可扩展到其他模态缺失或噪声（如属性、关系等），通过随机替换特征（零向量或随机向量）模拟混乱数据。

## 3. 实验设计

### 数据集与场景
- **DBP15K**（中文-英文、日文-英文、法文-英文）和 **OpenEA**（法文-英文、德文-英文、跨知识图谱D-W-V1和D-W-V2）。
- 主要场景：视觉缺失比例 \(r_{vm} \in \{0.4, 0.6, 0.8, 0.95\}\)；以及混合混乱数据（多模态缺失+噪声，比例0%~80%）。

### 基准方法
- 常规MMEA：EVA、MSNEA、MCLEA。
- 抗缺失MMEA：UMAEA（生成式）、GEEA（生成式）。

### 评估指标
- Hits@1、Hits@10、MRR（Mean Reciprocal Rank）。

## 4. 资源与算力

- 论文中提及使用**单块H100 GPU**进行效率对比（图4）。
- 模型参数：rMMEA约**1026.4万**参数（与UMAEA的2542.8万相比显著更少）。
- 训练总时间：rMMEA约**997.3秒**（UMAEA需2542.8秒，因多阶段训练）。
- 每轮训练时间：约13-14秒，与基线相近。
- 未明确说明使用的GPU数量、内存、CPU等细节。

## 5. 实验数量与充分性

### 实验组数
- **主实验**：7个数据集 × 4种缺失比例（共28个设置），表1-2。
- **消融实验**：DBP15K ZH-EN和OpenEA EN-FR上5种变体（表3）。
- **效率对比**：单数据集（DBP15K ZH-EN）综合图（图4）。
- **混乱数据实验**：4个数据集 × 5种混乱比例（共20个设置），图5。
- **不同缺失比例趋势**：2个数据集（图3）。

### 充分性判断
- 数据集覆盖跨语言和跨知识图谱场景，多种缺失比例，对比了当前所有主流抗缺失方法。
- 消融实验验证了排名蒸馏和互信息估计的贡献，以及与其他蒸馏方式的比较。
- 但仅在此7个数据集上测试，未涵盖更多跨领域（如社交网络、电商）的真实图谱；所有实验均为离线评估，未进行在线或人工验证。
- 未报告统计显著性检验（如t检验），但结果差异明显。

## 6. 论文的主要结论与发现

- rMMEA在**所有7个数据集、所有缺失比例**下显著优于现有抗缺失方法（UMAEA、GEEA）和常规方法。
- 在**高缺失比例（0.95）**下，rMMEA的Hits@1比UMAEA高约2~4个百分点，MRR高约2~3个百分点。
- 在**混乱数据**（多模态缺失+噪声）场景下，rMMEA性能退化更平缓，相对提升随混乱比例增加（从7.2%升至27.9%），显示更强鲁棒性。
- **效率优势**：参数更少、训练时间仅为UMAEA的约40%，无需多阶段训练。
- 排名蒸馏比传统KL散度蒸馏更有效（替换为KLD后MRR下降约1.5~2%）。

## 7. 优点

- **方法设计创新**：将排名信息纳入蒸馏，避免点对点匹配带来的学习鸿沟，更符合实体对齐的排序本质。
- **互信息估计**：弥补了单纯排名蒸馏无法捕获嵌入语义的不足，提升嵌入质量。
- **自蒸馏框架**：无需额外教师模型或外部数据，可在主模型内联合训练。
- **高效性**：单阶段、参数少、训练快，适合实际部署。
- **噪声鲁棒性**：在混合模态缺失和噪声下性能下降最慢，具有实际价值。
- **实验全面**：覆盖多种缺失比例、混乱程度、跨语言和跨知识图谱场景。

## 8. 不足与局限

- **基准局限性**：仅在DBP15K和OpenEA两个基准（各含2-3个子集）上测试，缺乏更多真实世界多模态知识图谱（如Wikidata多模态扩展、电商商品图谱）的验证。
- **视觉缺失假设**：仅处理完全缺失（无图像），未考虑部分缺失（如低质量图像、分辨率差异）或图像内容噪声（如无关图片）。
- **生成式方法的对比**：虽然效率更高，但生成式方法（如UMAEA）在高缺失时Hits@10可能更好（论文提及“outline of vision information”），说明rMMEA在召回率方面可能还有提升空间。
- **未涉及其他模态缺失**：论文虽声称可推广，但实验仅聚焦视觉模态缺失，对其他模态（如文本、属性）缺失未单独实验。
- **超参数依赖**：排名蒸馏中的\(\alpha, \beta\)需要调节，虽在附录给出设置，但对不同数据集可能需要微调，未见详细鲁棒性分析。
- **未与近期LLM基方法对比**：文中提到未来计划与LLM结合，但未与当前基于大语言模型的实体对齐方法（如ChatEA等）对比，可能不够前沿。

（完）
