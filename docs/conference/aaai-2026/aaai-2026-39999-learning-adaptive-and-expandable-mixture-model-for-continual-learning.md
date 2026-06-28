---
title: Learning Adaptive and Expandable Mixture Model for Continual Learning
title_zh: 学习自适应可扩展混合模型用于持续学习
authors: "Fei Ye, YongCheng Zhong, Qihe Liu, Adrian G. Bors, JingLing Sun, Jinyu Guo, ShiJie Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39999/43960"
tags: ["query:continual"]
score: 9.0
evidence: 持续学习方法避免灾难性遗忘
tldr: 针对持续学习中灾难性遗忘问题，现有方法依赖单一预训练模型且冻结参数，限制了新任务适应性。本文提出基于预训练模型的双表征骨干架构，结合不变与演化表征网络，同时捕获静态和动态特征，实现灵活扩展与遗忘缓解。实验表明该方法在多个持续学习基准上取得优异性能，为类人持续学习提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续学习方法依赖单一预训练骨干并冻结参数，限制了模型对新任务的适应性。
method: 提出双表征骨干架构，包含不变表征网络和演化表征网络，分别捕获静态和动态特征。
result: 在多个持续学习基准数据集上取得领先性能，有效缓解灾难性遗忘。
conclusion: 所提方法通过动态与静态特征分离，平衡了知识保留与任务适应，推动了持续学习发展。
---

## Abstract
Continuous learning constitutes a fundamental capability of artificial intelligence systems, enabling them to incrementally assimilate novel information without succumbing to catastrophic forgetting. Recent research has leveraged Pre-Trained Models (PTMs) to enhance continual learning efficacy. Nevertheless, prevailing methodologies typically depend on a singular pre-trained backbone and freeze all pre-trained parameters to mitigate network forgetting, thereby constraining adaptability to emerging tasks. In this study, we introduce an innovative PTM-based framework featuring a Dual-Representation Backbone Architecture (DRBA), which integrates both invariant and evolved representation networks to concurrently capture static and dynamic features. Building upon DRBA, we propose an Adaptive and Expandable Mixture Model (AEMM) that incrementally incorporates new expert modules with minimal parameter overhead to accommodate the learning of each novel task. To further augment adaptability, we develop a Dynamic Adaptive Representation Fusion Mechanism (DARFM) that processes outputs from both representation networks and autonomously generates data-driven adaptive weights, optimizing the contribution of each representation. This mechanism yields an adaptive, semantically enriched composite representation, thereby maximizing positive knowledge transfer. Additionally, we propose a Dynamic Knowledge Calibration Mechanism (DKCM), comprising prediction and representation calibration processes, to ensure consistency in both predictions and feature representations. This approach achieves a balance between stability and plasticity, even when learning complex datasets. Empirical evaluations substantiate that the proposed approach attains state-of-the-art performance.

---

## 论文详细总结（自动生成）

# 论文总结：Learning Adaptive and Expandable Mixture Model for Continual Learning

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：持续学习（Continual Learning, CL）中，模型在学习新任务时会发生灾难性遗忘（catastrophic forgetting），即对旧任务的性能显著下降。
- **现有方法局限**：当前基于预训练模型（PTM）的方法通常使用单一预训练骨干（如ViT），并冻结所有预训练参数以避免遗忘，但这严重限制了模型对新任务的适应性（plasticity不足）。特别是面对多领域任务（Multi-Domain Task-Incremental Learning, MTIL）时，静态表征难以应对分布漂移。
- **研究动机**：借鉴生物 hippocampus 和 neocortex 的双系统记忆机制（缓慢变化信息 vs. 快速进化信息），本文提出动态捕获静态与动态特征的方法，以平衡稳定性（stability）和可塑性（plasticity）。

## 2. 方法论

### 核心思想
提出 **双表征骨干架构（Dual-Representation Backbone Architecture, DRBA）**，包含：
- **不变表征网络（invariant representation network）**：编码稳定、缓慢变化的信息。
- **演化表征网络（evolved representation network）**：编码随任务动态进化的信息。
两者共享大部分参数，仅演化网络的最后 L 层可训练，减少参数冗余。

基于DRBA，构建**自适应可扩展混合模型（Adaptive and Expandable Mixture Model, AEMM）**：
- 为每个新任务增量添加轻量级专家模块（特征变换层 + 线性分类器）。
- 通过**动态自适应表征融合机制（DARFM）** 自动生成数据驱动的自适应权重，调节不变和演化表征的贡献，实现更鲁棒的融合表示。
- 通过**动态知识校准机制（DKCM）** 校准预测和表征，包括：
  - **预测校准过程（PCP）**：最小化当前专家与历史专家预测分布的KL散度。
  - **表征校准过程（RCP）**：使用MMD或MSE对齐当前与辅助（之前）演化网络各层的特征分布，保持稳定性。

### 关键技术细节（文字说明）
1. **特征提取**：输入数据经共享网络得到基础表征，再分别经不变和演化网络得到两个特征向量。
2. **融合**：DARFM通过自注意力机制计算两个表征的自适应权重 \(w[0], w[1]\)，将加权后的特征拼接。
3. **任务预测**：拼接后的特征输入当前任务的专家模块（特征变换+线性分类器）。
4. **校准损失**：
   - PCP损失：\(\mathcal{L}_p = \sum_{i=1}^{k-1} D_{KL}(p(Y|Z^{k,i}), p(Y|Z^{k,i}_{\text{his}}))\)
   - RCP损失：\(\mathcal{L}_r = \frac{1}{L}\sum_{i=1}^{L} \text{F}_{\text{measure}}(\tilde{Z}^i, \tilde{Z}^i_{\text{his}})\)，其中 \(\text{F}_{\text{measure}}\) 可选MMD（如式(16)-(18)）或MSE。
5. **总体训练**：联合交叉熵损失与校准损失优化模型。

## 3. 实验设计

### 数据集与场景
- **Multi-Domain Task-Incremental Learning (MTIL) benchmark**：7个不同视觉领域数据集：
  - **自然域**：CIFAR-10, CIFAR-100, Tiny ImageNet (TIN), ImageNet-R (IN-R)
  - **医学域**：CropDiseases (CD)
  - **细粒度域**：CUB-200
  - **遥感域**：RESISC45
- **任务序列**：全部7个数据集按固定顺序（C10→C100→TIN→IN-R→CD→CUB→RESISC45）学习；另设3种3-task排列（TIN→CD→RESISC45、RESISC45→TIN→CD、CD→RESISC45→TIN）验证鲁棒性。

### 对比方法
- **回放类**：DER++, DER++(Re), CLS-ER
- **提示类**：L2P, Dualprompt, CODAPrompt, DAP
- **动态架构类**：Ranpac, SLCA, SEMA
- **本文变体**：AEMM (mmd), AEMM (mse)（RCP分别使用MMD和MSE）

### 评估指标
- **Average Accuracy** (↑)
- **Forgetting Measure** (↓)
- **Learning Accuracy** (↑)
- **Last Accuracy** (↑)
- **Total Average** (↑)

## 4. 资源与算力

论文中**未明确说明**所用GPU型号、数量、训练时长等算力信息。仅提及代码已在GitHub上开源（附录链接），但未提供硬件配置或运行时间。因此无法评估算力需求。

## 5. 实验数量与充分性

- **实验总量**：
  - 表1：在7个数据集上报告了三种指标（Average, Forgetting, Learning），每种重复3次，含标准差。
  - 表2：在3种不同任务排列下比较了11种方法（含两个变体）的Average和Last Accuracy。
  - 图2(a)：展示了RTC序列的遗忘曲线。
  - 图2(b)：超参数敏感性分析（PCP和RCP的权重系数）。
  - 消融研究：去除了PCP和RCP模块（表2中w/o PCP, w/o RCP），另在附录D中有更多消融（论文提及但未在正文全展示）。
- **充分性评价**：
  - **优点**：覆盖了多领域、多指标、多种任务顺序，对比方法全面，消融分析清晰，超参数敏感性验证了稳定性。
  - **不足**：未进行统计显著性检验（如t-test），也未在更大规模数据集（如ImageNet完整版）或类增量场景下评估；缺乏对计算开销和内存增长的量化分析；所有实验均基于固定的预训练ViT，未探究不同预训练模型的影响。

## 6. 主要结论与发现

- **性能领先**：AEMM (mse) 在Total Average Accuracy上达到87.77%，显著优于最强基线CLS-ER（81.00%）和提示方法（DualPrompt 59.35%）。
- **遗忘极低**：AEMM (mmd) 的Forgetting Measure仅0.42%，远低于DER++(Re)（3.92%）和Ranpac（2.65%）。
- **任务顺序鲁棒**：在三种不同任务排列下，AEMM均保持最高Average和Last Accuracy，且遗忘曲线接近零。
- **组件有效性**：单独去除PCP或RCP均导致性能下降，且RCP对稳定性贡献更大（在域漂移下尤为明显）。
- **超参数鲁棒**：PCP和RCP权重在较宽范围内性能稳定。

## 7. 优点

1. **创新架构**：DRBA结合静态和动态表征，灵感来自神经科学，设计新颖且高效（参数共享）。
2. **动态融合机制**：DARFM根据数据自适应调整权重，避免了简单拼接的次优性。
3. **双重校准**：PCP和RCP分别从预测和特征层面保持一致性，有效平衡稳定性和可塑性，无需存储旧样本。
4. **实验全面**：在多领域、多指标、多种任务顺序下验证，消融和敏感性分析完备。
5. **代码开源**：促进可复现性和后续研究。

## 8. 不足与局限

1. **算力信息缺失**：未报告GPU型号、训练时间、显存占用等，难以评估实际资源需求。
2. **场景覆盖有限**：仅在MTIL（任务增量、相同类别集合）下评估，未在类增量（Class-IL）或域增量（Domain-IL）等更常见设置下测试；未使用更大规模的预训练模型（如ViT-L）或不同架构（如CNN）。
3. **统计显著性未说明**：虽然报告了均值和标准差，但未进行假设检验，难以判断性能提升是否显著。
4. **存储与计算开销**：动态添加专家模块虽参数少，但随任务数线性增长，长期扩展性未讨论；DARFM和DKCM在推理时引入额外计算，文中未量化。
5. **依赖预训练质量**：方法有效性高度依赖初始预训练ViT的表征能力，若预训练数据与下游任务域差异极大，可能失效。
6. **实验重复次数较少**：仅3次重复，建议增加重复次数以提高置信度。

（完）
