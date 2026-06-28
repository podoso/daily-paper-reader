---
title: Unifying Locality of KANs and Feature Drift Compensation Projection for Data-Free Replay Based Continual Face Forgery Detection
title_zh: 融合KAN局部性与特征漂移补偿投影的无数据回放持续人脸伪造检测
authors: "Tianshuo Zhang, Siran Peng, Li Gao, Haoyuan Zhang, Xiangyu Zhu, Zhen Lei"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38274/42236"
tags: ["query:continual"]
score: 9.0
evidence: 持续学习灾难性遗忘KAN网络
tldr: 针对连续学习场景下新伪造方法导致旧知识遗忘的问题，本文利用KAN网络的局部可塑性特性，结合特征漂移补偿投影，提出无需数据回放的持续学习框架，在保留旧任务性能的同时学习新伪造类型。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 人脸伪造检测需持续适应新伪造方法，但存在灾难性遗忘问题。
method: 利用KAN网络的局部可塑性学习新任务，并设计特征漂移补偿投影缓解遗忘。
result: 在无数据回放条件下实现了对新旧伪造类型的有效检测。
conclusion: 展示了KAN在持续学习中的潜力，为无数据回放场景提供了新思路。
---

## Abstract
The rapid advancements in face forgery techniques necessitate that detectors continuously adapt to new forgery methods, thus situating face forgery detection within a continual learning paradigm. However, when detectors learn new forgery types, their performance on previous types often degrades rapidly, a phenomenon known as catastrophic forgetting. Kolmogorov-Arnold Networks (KANs) utilize locally plastic splines as their activation functions, enabling them to learn new tasks by modifying only local regions of the functions while leaving other areas unaffected. Therefore, they are naturally suitable for addressing catastrophic forgetting. However, KANs have two significant limitations: 1) the splines are ineffective for modeling high-dimensional images, while alternative activation functions that are suitable for images lack the essential property of locality; 2) in continual learning, when features from different domains overlap, the mapping of different domains to distinct curve regions always collapses due to repeated modifications of the same regions. In this paper, we propose a KAN-based Continual Face Forgery Detection (KAN-CFD) framework, which includes a Domain-Group KAN Detector (DG-KD) and a data-free replay Feature Separation strategy via KAN Drift Compensation Projection (FS-KDCP). DG-KD enables KANs to fit high-dimensional image inputs while preserving locality and local plasticity. FS-KDCP avoids the overlap of the KAN input spaces without using data from prior tasks. Experimental results demonstrate that the proposed method achieves superior performance while notably reducing forgetting.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：随着AI生成内容（AIGC）快速发展，人脸伪造技术不断迭代，检测器需要持续适应新型伪造方法，传统静态模型泛化能力不足。持续学习（Continual Learning）被视为解决方案，但现有模型在学新任务时往往对旧任务性能急剧下降，即灾难性遗忘（Catastrophic Forgetting）。
- **背景创新点**：Kolmogorov-Arnold Networks（KANs）因采用局部可塑样条作为激活函数，理论上天然适合持续学习——通过修改局部曲线区域来学习新任务，同时保持其他区域稳定。然而，KANs应用于视觉持续性学习存在两大限制：1）B样条不擅长高维图像建模，而替代的激活函数（如有理函数）又缺乏局部性；2）不同任务的输入特征空间重叠会导致同一曲线区域被反复修改，使得旧知识被覆盖。本文旨在同时解决这两个问题，实现无需原始数据的无数据回放持续伪造检测。

## 2. 方法论：核心思想、关键技术细节

- **整体框架**：提出KAN-CFD，由两个核心模块组成：
  1. **Domain-Group KAN Detector（DG-KD）**：为每个域（任务）分配一组独立的、基于径向基函数（RBF）的激活函数矩阵（称为DG-Layer），再将所有DG-Layer求和得到最终检测器。RBF具有局部非零响应特性，保证了局部性和局部可塑性；同时通过分组共享参数（将输入维度分为g组，每组共享同一RBF基函数），解决KAN在高维视觉输入上的计算冗余和拟合困难。
  2. **Feature Separation by KAN Drift Compensation Projection（FS-KDCP）**：无数据回放的分布分离策略。仅存储每个旧任务选出的代表性特征（通过SUR方法选取），而非原始数据。然而，随着骨干网络不断更新，存储的特征会产生语义漂移（feature drift）。为此，训练一个由单层DG-Layer构成的KAN投影模块（KDCP），用于将旧任务特征映射到当前特征空间，补偿漂移。然后，使用监督对比损失（L_SC）将新旧任务的特征分布拉开，同时使用特征级知识蒸馏损失（L_KD）约束骨干网络变化不要过大。最终整体损失为 L_Overall = L_CLS + λ1 L_SC + λ2 L_KD。投影模块通过最小化当前骨干提取特征与映射后的旧骨干特征之间的MSE对齐损失（L_Align）进行训练。

- **公式/算法流程（文字说明）**：
  - DG-Layer：输入x，维度din，输出dout，经分组后每个组共享一个加权RBF：ˆφ_{⌊i/dg⌋,t}(xi) = ω_{i,t} · φ_{⌊i/dg⌋,t}(xi)。DG-KD(t) = Σ_{k=1..t} DG-Layer_k(x)。
  - 特征选择：f_{t-1→t-1} = SUR( f^{t-1}_θ (X_{t-1}) )。
  - 漂移补偿：f_{t-1→t} = p^t_KAN( f_{t-1→t-1} )，p^t_KAN为单层DG-Layer。
  - 分离损失L_SC：对2T个类（T个域的real/fake）进行对比学习。
  - 蒸馏损失L_KD：MSE( f^{t-1}_θ(x_i), f^t_θ(x_i) )。
  - 对齐损失L_Align：MSE( p^t_KAN( f^{t-1}_θ(x_i) ), f^t_θ(x_i) )。

## 3. 实验设计

- **数据集**：
  - 数据集增量协议：FaceForensics++ (FF++)、DFDC-P、DFD、Celeb-DF v2 (CDF2)。
  - 伪造类型增量协议：从DF40选取Hybrid（FF++混合）、Face-Reenactment (FR, MCNet)、Face-Swapping (FS, BlendFace)、Entire Face Synthesis (EFS, StyleGAN3)。
  - 长序列实验：从DF40中选10个任务，覆盖FR、FS、EFS三大类。

- **Benchmark**：遵循DFIL和SUR-LID设立的标准协议。

- **对比方法**：
  - 数据集增量：LWF (TPAMI’17)，CoReD (MM’21)，DFIL (MM’23)，DMP (MM’24)，SUR-LID (CVPR’25)。
  - 伪造类型增量：额外对比HDP (IJCV’25)。
  - 长序列：对比DFIL和KAC (CVPR’25)。

- **评价指标**：准确率（Acc）、曲线下面积（AUC）、平均遗忘率（AF）。

## 4. 资源与算力

- 文中明确说明：**所有实验在两张Nvidia A6000 GPU上进行**。
- 训练时长未单独给出，但可能通过补充材料提供，本文未提及具体时长。
- 使用的骨干网络为ConvNeXt-B，优化器为Adam（lr=2e-4），投影模块优化器为Adam（lr=5e-4）。特征记忆大小为500，批次大小64。

## 5. 实验数量与充分性

- **主要实验**：两张大表（表1、表2）分别对应数据集增量和伪造类型增量协议，包含7种以上的对比方法，每个任务后报告准确率、平均准确率、遗忘率。
- **长序列实验**：图5展示了10个任务的结果，对比DFIL和KAC。
- **消融实验**：
  - 表3：损失函数消融（L_CLS、L_CLS+L_KD、L_CLS+L_SC、完整损失）。
  - 表4：特征分离模块消融（Baseline、FS w/o KDCP、完整Ours、Ours+数据回放上界）。
  - 表5：检测器结构消融（MLP、GroupKAN、KAC、DG-KD）。
  - 图4：UMAP可视化特征空间分离效果。
- **充分性与公平性**：
  - 实验覆盖多个数据集、多种伪造类型、长序列场景，对比方法包括通用持续学习方法和专用持续伪造检测方法，且部分方法带有数据回放（本文无数据回放），结果以粗体标出最优、下划线标出次优，客观性较好。
  - 实验中提及“aligned backbones”在补充材料中提供，本文未详细展开；所有对比结果取自官方发表论文的最佳值，可能存在实现差异，但已尽力公平。
  - 总体实验设计较为充分，消融验证了各部分有效性。

## 6. 主要结论与发现

- 提出的KAN-CFD框架在两个协议上均取得新SOTA：数据集增量协议下平均Acc达91.64%，平均AF仅4.08%；伪造类型增量协议下平均AUC达94.40%，平均AF仅2.60%，均优于带数据回放的方法。
- DG-KD相比普通MLP、GroupKAN、KAC具有更低的遗忘率，并且能保持零激活基线（图3玩具实验）。
- FS-KDCP通过投影补偿漂移，几乎达到数据回放上界的性能，且缓存大小节省99.48%。
- 长序列实验（10任务）中，本方法平均准确率最高、遗忘率最低。

## 7. 优点

- **无数据回放**：仅存储少量代表性特征，避免了隐私风险，缓存节省巨大（声称99.48%）。
- **独特结合KAN局部性**：首次将KAN的局部可塑性与视觉持续检测相结合，提出分组RBF设计解决高维输入瓶颈；DG-KD保留了KAN的理想性质并适配图像。
- **漂移补偿投影**：利用KAN投影模块（KDCP）有效补偿特征语义漂移，使得旧分布能在当前空间准确保留，无需旧数据即可实现分布分离。
- **设计简洁有效**：损失函数组合（分类损失+对比分离损失+蒸馏损失）轻量且效果显著；消融实验验证了各组件必要性。
- **实验全面**：涵盖数据集增量、伪造类型增量、长序列，以及多组消融和可视化，充分验证方法鲁棒性。

## 8. 不足与局限

- **实验范围局限**：仅在人脸伪造检测领域验证，模型通用性未在其他持续学习任务（如图像分类、目标检测）中测试。
- **对比方法选择**：无数据回放的方法仅对比了LWF，缺乏与其他无数据回放持续学习方法的比较（如ER、GDumb、DER等），可能影响“无数据回放领域SOTA”的宣称强度。
- **计算开销**：KAN网络（尤其是分段RBF动态调整）可能带来额外推理/训练开销，论文未汇报训练时间或参数量对比，也未对效率做详细分析。
- **特征选择依赖**：FS-KDCP依赖SUR方法进行特征选择，SUR的选择质量可能影响最终效果，未探讨不同选择策略的影响。
- **序列长度**：长序列实验仅10任务，仍有待更大规模（如20+任务）验证遗忘极限。
- **理论分析有限**：未严格证明分组RBF能完全模拟B样条局部性，仅通过实验验证；漂移补偿的收敛性未提供理论保证。
- **领域漂移假设**：假设不同任务的骨干变化可被一层DG-Layer投影近似，可能对剧烈骨干变化无效（如更换架构）。

（完）
