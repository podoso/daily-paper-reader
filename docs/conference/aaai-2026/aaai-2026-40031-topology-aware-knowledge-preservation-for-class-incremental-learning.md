---
title: Topology-aware Knowledge Preservation for Class-Incremental Learning
title_zh: 拓扑感知的知识保留用于类增量学习
authors: "Han Zang, Yongfeng Dong, Linhao Li, Liang Yang, Yu Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40031/43992"
tags: ["query:continual"]
score: 8.0
evidence: 通过拓扑感知蒸馏实现类增量学习无遗忘
tldr: 类增量学习中知识蒸馏通常限于成对对齐，未能保持特征空间的全局流形结构导致语义漂移。本文提出拓扑感知蒸馏框架，利用持续同调强制增量阶段间的拓扑对齐，确保结构一致的知识迁移。在多个基准数据集上，该方法有效缓解了灾难性遗忘，并在长序列增量场景下保持鲁棒性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有知识蒸馏方法在类增量学习中仅做两两对齐，忽略了特征空间的全局结构。
method: 利用持续同调捕捉多尺度结构模式，通过拓扑对齐实现结构一致的知识迁移。
result: 在多个类增量学习基准上，该方法在准确率和遗忘率上优于现有蒸馏方法。
conclusion: 拓扑感知蒸馏有效保留了特征空间结构，减轻了语义漂移。
---

## Abstract
Class Incremental Learning (CIL) aims to enable models to continually learn new classes while retaining previously learned knowledge. The principal challenge in CIL is catastrophic forgetting, which prior approaches typically address by distilling knowledge from previous model. However, such way is often limited to pairwise alignment, failing to preserve the underlying global manifold structure of feature space—ultimately resulting in semantic drift over time. To capture multi-scale structural patterns in the feature space, we propose a topology-aware distillation framework that leverages persistent homology. Specifically, by enforcing topological alignment across incremental stages, our method ensures structure-consistent knowledge transfer and robust preservation of old classes. Furthermore, we still devise a dual-branch architecture with an inverse sampling and dynamic reweighting mechanism that addresses the inherent data imbalance in standard replay-based frameworks. These innovations coalesce into TaKP (Topology-aware Knowledge Preservation), a unified framework designed to enhance knowledge preservation in CIL. Extensive experiments demonstrate that TaKP achieves state-of-the-art performance on multiple benchmarks, significantly improving old-class preservation and average accuracy.

---

## 论文详细总结（自动生成）

### 论文详细中文总结

#### 1. 核心问题与整体含义（研究动机和背景）
- **研究问题**：类增量学习（CIL）面临的主要挑战是灾难性遗忘，即学习新类别时严重损害旧类别性能。
- **现有方法局限**：当前主流的知识蒸馏（KD）方法（如基于logits或特征的成对对齐，或基于关系的蒸馏）虽能缓解遗忘，但仅限于局部一致性约束，忽视了特征空间的全局流形结构，导致语义漂移随时间累积。
- **本文动机**：受流形假设和单纯复形同胚思想的启发，提出利用持续同调（Persistent Homology, PH）捕获特征空间的多尺度拓扑结构（如簇、环等），实现全局结构感知的知识迁移，同时设计双分支架构应对数据不平衡。

#### 2. 方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：构建拓扑感知蒸馏框架TaKP，通过强制当前模型与旧模型在特征空间的拓扑结构（以持久图表示）一致，保留全局几何信息；并采用双分支自适应重平衡网络缓解类别不平衡。
- **关键技术细节**：
  - **拓扑知识蒸馏**：
    - 使用RipsNet近似计算每个batch样本嵌入的持久图（PD）和持久图像（PI）。
    - 定义拓扑蒸馏损失 \( L_{\text{TopKD}} = \sum_{(x_1,...,x_i) \in D_m} L_2(\hat{p}_{\text{old}}(f_{\text{old}}(x_1),...), \hat{p}_{\text{new}}(f_{\text{new}}(x_1),...)) \)。
    - 总损失：\( L_{\text{total}} = L_{\text{CE}} + L_{\text{KD}} + L_{\text{TopKD}} \)，其中 \( L_{\text{KD}} \) 是KL散度蒸馏logits。
  - **双分支自适应重平衡**：
    - 常规分支：从原始不平衡分布学习通化特征。
    - 重平衡分支：通过逆采样（\( p_i \propto N_{\max}/N_i \)）提高旧类采样概率，并采用动态权重 \( \alpha = 1 - (T/T_{\max})^2 \) 控制两个分支的贡献，从前期侧重通用表征逐渐转向后期强调旧类保留。
    - 最终输出：\( z = \alpha W_c^\top f_c + (1-\alpha) W_r^\top f_r \)。
- **算法流程**：预训练RipsNet（仅一次）→ 每个增量阶段：使用双分支网络训练，同时计算 \( L_{\text{TopKD}} \) 对齐当前与旧模型的持久图像，联合优化 \( L_{\text{total}} \)。

#### 3. 实验设计
- **数据集与场景**：
  - CIFAR-100（32×32，100类）和 ImageNet-100（256×256，100类）。
  - 两种增量协议：B0 Inc10（10个任务，每任务10类）和 B0 Inc20（5个任务，每任务20类）。每旧类保留20个样本（记忆缓冲区）。
- **基准（Baseline）**：包括iCaRL、PodNet、Foster、MTD、DSGD、PsHD、LKD、CREATE等蒸馏方法，以及CLAD、RNKS、DBL等类别重平衡方法。
- **对比方法**：共13种方法，覆盖logits蒸馏、特征蒸馏、关系蒸馏、拓扑蒸馏及显式重平衡。

#### 4. 资源与算力
- **文中明确说明**：使用Nvidia 4090 GPU（24GB显存），训练每个任务80个epoch，batch size 64。但未给出GPU数量、总训练时长（仅提到RipsNet预训练需额外1.3小时，总训练时间与PsHD相近，约8.1小时）。参数数量：4.8M（TaKP），内存占用46.7MB（含RipsNet）。

#### 5. 实验数量与充分性
- **实验数量**：
  - 主表（Table 1）对比了4个协议（CIFAR100×2 + ImageNet100×2）×13种方法。
  - 消融实验（Table 3）在iCaRL和PodNet上分析拓扑蒸馏和重平衡的贡献。
  - 额外实验（Table 2）探究同调维度（0维、1维、0&1维）的影响。
  - 图6(b)分析PCD点数（batch size）。
  - 图7展示不同增量协议下的准确率曲线。
  - 图8-9可视化持久图像一致性。
  - Table 4与PsHD进行效率和精度对比。
- **充分性评估**：实验覆盖多个数据集、多种协议、充分的消融和可视化，结论客观。但未报告标准差或多次运行结果，可能存在随机性偏差；且仅在两个中等规模数据集上验证，未在更大规模（如ImageNet-1K）上测试。

#### 6. 主要结论与发现
- TaKP在CIFAR-100和ImageNet-100上均取得最优平均准确率（如CIFAR-100 B0 Inc10：74.32%，ImageNet-100 B0 Inc20：79.15%），且遗忘程度最低（BWT=14.67）。
- 拓扑蒸馏有效保持特征空间全局结构，持久图像在增量阶段高度一致（图8-9），证明其稳定性。
- 双分支重平衡（逆采样+动态权重）显著缓解数据不平衡，对旧类保护效果突出。
- 0维持久图（连接分量）比1维（环）更适合分类任务，因包含聚类信息。

#### 7. 优点
- **方法创新**：首次将持续同调直接嵌入CIL蒸馏框架，实现多尺度全局结构对齐，超越局部蒸馏。
- **结构完备**：同时解决知识遗忘（拓扑蒸馏）和数据不平衡（双分支重平衡）两大CIL核心问题，形成统一框架。
- **实验严谨**：在多个协议和数据集上全面对比，消融实验验证各组件贡献，可视化证明拓扑稳定性。
- **效率可控**：RipsNet仅预训练一次，后续蒸馏计算开销可接受，优于CPU依赖的PsHD。

#### 8. 不足与局限
- **计算开销**：需额外预训练RipsNet，且内存占用略高（46.7MB vs PsHD 22.1MB），推理延迟未报告，可能在小规模设备上受限。
- **实验覆盖不足**：仅在CIFAR-100和ImageNet-100上测试，未在ImageNet-1K或更大规模、更长序列（如100任务）上验证；未报告多次运行的标准差。
- **数据假设**：基于replay（每类20样本），若记忆极度有限（如每类1样本）时性能如何未分析。
- **可重复性风险**：代码已开源，但未说明随机种子设置，且依赖RipsNet的近似可能引入微小偏差。
- **理论分析缺失**：未从理论上证明拓扑对齐为何比局部对齐更能缓解语义漂移，仅通过实验验证。

（完）
