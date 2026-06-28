---
title: Continual Out-of-Distribution Detection with Analytic Neural Collapse
title_zh: 基于解析神经坍缩的连续分布外检测
authors: "Saleh Momeni, Changnan Xiao, Bing Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38585/42547"
tags: ["query:continual"]
score: 9.0
evidence: 持续学习方法避免灾难性遗忘
tldr: 现有持续学习方法多关注闭集场景，忽略了开放世界的分布外检测需求。本文利用解析神经坍缩现象，提出基于原型策略的持续分布外检测方法，在持续学习过程中有效缓解灾难性遗忘。实验表明，该方法在多个基准上取得了优异的检测性能，为持续学习与分布外检测的融合提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续学习方法主要关注闭集场景，无法有效应对包含分布外样本的开放世界环境。
method: 利用神经坍缩现象，采用基于原型的最近类均值策略同时处理分类与分布外检测。
result: 在多个持续学习基准上，该方法在分布外检测和分类任务中均达到先进水平。
conclusion: 提出的方法有效结合了持续学习与分布外检测，缓解了灾难性遗忘问题。
---

## Abstract
Continual learning (CL) aims to enable models to incrementally learn from a sequence of tasks without forgetting previously acquired knowledge. While most prior work focuses on closed-world settings, where all test instances are assumed from the set of learned classes, real-world applications require models to handle both CL and out-of-distribution (OOD) samples. A key insight from recent studies on deep neural networks is the phenomenon of Neural Collapse (NC), which occurs in the terminal phase of training when the loss approaches zero. Under NC, class features collapse to their means, and classifier weights align with these means, enabling effective prototype-based strategies such as nearest class mean, for both classification and OOD detection. However, in CL, catastrophic forgetting (CF) prevents the model from naturally reaching this desirable regime. In this paper, we propose a novel method called Analytic Neural Collapse (AnaNC) that analytically creates the NC properties in the feature space of a frozen pre-trained model with no training, overcoming CF. Extensive experiments demonstrate that our approach outperforms state-of-the-art methods in continual OOD detection and learning, highlighting the effectiveness of our method in this challenging scenario.

---

## 论文详细总结（自动生成）

### 论文详细中文总结

#### 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：现有持续学习（CL）方法主要关注闭集场景，即假设所有测试样本都属于已学习的类别。然而，实际应用（如自动驾驶、医疗诊断）中模型必须同时处理持续学习与分布外（OOD）检测，即识别从未见过的类别。
- **背景**：神经坍缩（Neural Collapse, NC）现象在深度网络训练到损失接近于零的终端阶段出现，其性质（NC1～NC4）使得基于原型的最近类均值（NCM）策略对分类和OOD检测都非常有效。但在持续学习中，灾难性遗忘（CF）阻止模型自然达到NC，因此需要一种人工构造NC的方法。

#### 2. 方法论：核心思想、关键技术细节
- **核心思想**：利用冻结的预训练模型（PTM）提取特征，然后通过解析投影（无需训练）在特征空间中人为创建NC1（类内方差坍缩）和NC2（类均值构成等角紧框架ETF），从而支持基于NCM的持续学习和OOD检测，完全避免CF。
- **关键技术细节**：
  1. **特征增强**：在PTM特征后添加一层随机投影（RP），使用随机权重矩阵 \(W_{rp} \in \mathbb{R}^{d \times D}\) 和GELU非线性激活，将特征映射到更高维空间（默认D=5000），增强表达能力。
  2. **解析学习输出层**：采用极限学习机（ELM）框架，通过脊回归（Ridge Regression）求解输出层权重 \(W = (Z^TZ + \lambda I)^{-1} Z^T Y\)。其中目标矩阵 \(Y\) 定义了每个类应坍缩到的目标均值 \(\tilde{\mu}_c\)。该解可增量更新（通过维护Gram矩阵和Cross矩阵）。
  3. **实现NC1**：将所有属于同一类的样本映射到同一个目标点 \(\tilde{\mu}_c\)，使得类内方差消失。
  4. **实现NC2**：将目标均值 \(\tilde{\mu}_c\) 排列成ETF结构（满足 \(\tilde{M}\tilde{M}^T = S\)，其中 \(S = I - \frac{1}{C-1}(11^T - I)\)）。通过求解正交Procrustes问题（SVD分解）找到最接近原始类均值 \(M\) 的ETF目标均值 \(\tilde{M}_{\text{ETF}}\)，平衡了ETF约束与原始几何。
  5. **分类与OOD检测**：在构造好的NC特征空间中，使用余弦相似度（等价于归一化后的欧氏距离）进行NCM分类和OOD评分。

#### 3. 实验设计
- **数据集**：
  - CIFAR-100（100类），ImageNet-R（200类），CUB（200类），Stanford Cars（196类）。每个数据集随机打乱并分成10个任务。
  - OOD设置：**In-dataset OOD**（未来任务样本作为OOD）、**Cross-dataset OOD**（CIFAR-100为ID，OOD包括CIFAR-10、Tiny ImageNet、Places365、FashionMNIST）。
- **基准方法**：NCM、Mahalanobis Distance (MD)、KLDA、FECAM、Residuals、NECO、CODA-Prompt、SLCA、RanPac等。对于不提供OOD检测的CIL方法，使用最大logit作为OOD分数。
- **评估指标**：AUC（ROC曲线下面积）、FPR95（95% OOD召回率下的误报率）、CIL分类准确率（最后准确率Alast和平均增量准确率Aavg）。

#### 4. 资源与算力
- **硬件**：单张NVIDIA A100 GPU，80GB显存。
- **时间开销**：FSA（第一任务适配）需约6分钟，特征提取约3分钟，而AnaNC的全部训练操作（包括增量更新）少于3秒。总训练时间主要由PTM特征提取主导。
- **未明确**：未报告完整训练时长（如整个10个任务的总时长），也未提及需要多卡或分布式训练。

#### 5. 实验数量与充分性
- **实验组数**：
  - 主表1（In-dataset OOD）：2种PTM（DINO、MOCO）× 4个数据集 × 3种随机种子分任务 → 每个值报告均值和标准差。
  - 表2（消融）：比较Input、RP、NC1、NC1+NC2四种特征，4个数据集。
  - 表3（Cross-dataset OOD）：2种PTM × 4个OOD数据集 × 3种子。
  - 表4（CIL分类性能）：DINO下4个数据集 × 3种子。
  - 图2：RP维度变化对AUC的影响（4个数据集）。
- **充分性评价**：实验设计较为全面，覆盖了多种OOD困难场景（近OOD和远OOD）、多种基线（包括SOTA的CL方法）、两种不同预训练策略（自监督DINO和MOCO）、统计显著性（3次随机分任务）。消融实验清晰地验证了NC1和NC2各自贡献。实验客观公正。

#### 6. 主要结论与发现
- AnaNC在所有设置下（In-dataset和Cross-dataset OOD，以及CIL分类）显著优于现有SOTA方法。例如，In-dataset OOD下使用DINO平均AUC提升2.22%，FPR95降低3.24%；CIL下平均Aavg提升2.45%。
- 仅使用原始PTM特征进行NCM效果有限，加上RP层改进不大，但强制NC1后OOD性能大幅提升，再增加NC2（ETF约束）实现最佳效果。
- 因为无需训练，AnaNC避免了灾难性遗忘，并且计算开销极低。

#### 7. 优点
- **理论启发性**：基于神经坍缩的几何性质，将NC原理成功应用于持续OOD检测，填补了该方向理论空白。
- **无需训练、避免遗忘**：完全解析构造，不需要反向传播或数据回放，从根本上克服CF。
- **高效性**：训练时间几乎可忽略（<3秒），仅依赖于PTM特征提取，易于扩展到更大规模。
- **SOTA性能**：在多个数据集和评估指标上全面领先，且对不同PTM（DINO、MOCO）鲁棒。
- **代码开源**：提供GitHub仓库，可复现。

#### 8. 不足与局限
- **仅覆盖CIL**：方法针对类增量学习（无任务id），未实验域增量学习（DIL）或任务增量学习（TIL）。论文承认对DIL需要额外调整。
- **依赖预训练模型**：假设有一个高质量PTM提供初始特征，若PTM领域不匹配，可能效果下降。
- **RP维度为超参数**：默认D=5000，虽通过消融验证了其影响，但未提供自动选择策略。
- **数据集均为图像**：实验仅涉及视觉任务，未验证文本或其他模态。
- **未考虑内存有限场景**：虽然AnaNC维护的Gram矩阵和随机均值较小，但若类别数极大，ETF的SVD分解（O(C^3)）仍可能成为瓶颈。论文未讨论C非常大时的扩展性。
- **OOD评估仅用阈值无关指标**：在实际部署中需要选择阈值，论文未提供阈值的确定方法或稳定性分析。

（完）
