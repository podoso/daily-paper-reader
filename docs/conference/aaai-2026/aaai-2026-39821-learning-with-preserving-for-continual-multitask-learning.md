---
title: Learning with Preserving for Continual Multitask Learning
title_zh: 持续多任务学习中的保留式学习
authors: "Hanchen David Wang, Siwoo Bae, Zirong Chen, Meiyi Ma"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39821/43782"
tags: ["query:continual"]
score: 9.0
evidence: 提出新的持续多任务学习设置并设计防止遗忘的方法
tldr: 本文提出持续多任务学习（CMTL）这一新场景，要求模型在共享数据流上顺序学习多个任务而不遗忘先前能力。为此设计Learning with Preserving（LwP）方法，通过保留任务特定特征间的共享结构来避免干扰。实验证明LwP在自动驾驶等实际场景中有效防止灾难性遗忘，优于现有持续学习方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续学习方法在多任务顺序学习场景下因学习碎片化特征而相互干扰。
method: 提出Learning with Preserving，通过保留共享特征结构避免任务间干扰，同时动态扩展任务特定模块。
result: 在多项持续多任务基准任务上，该方法在保留旧任务性能的同时高效学习新任务。
conclusion: 为持续多任务学习提供了一种无需重放的有效方案。
---

## Abstract
Artificial intelligence systems in critical fields like autonomous driving and medical imaging analysis often continually learn new tasks using a shared stream of input data. For instance, after learning to detect traffic signs, a model may later need to learn to classify traffic lights or different types of vehicles using the same camera feed. This scenario introduces a challenging setting we term Continual Multitask Learning (CMTL), where a model sequentially learns new tasks on an underlying data distribution without forgetting previously learned abilities. Existing continual learning methods often fail in this setting because they learn fragmented, task-specific features that interfere with one another. To address this, we introduce Learning with Preserving (LwP), a novel framework that shifts the focus from preserving task outputs to maintaining the geometric structure of the shared representation space. The core of LwP is a Dynamically Weighted Distance Preservation (DWDP) loss that prevents representation drift by regularizing the pairwise distances between latent data representations. This mechanism of preserving the underlying geometric structure allows the model to retain implicit knowledge and support diverse tasks without requiring a replay buffer, making it suitable for privacy-conscious applications. Extensive evaluations on time-series and image benchmarks show that LwP not only mitigates catastrophic forgetting but also consistently outperforms state-of-the-art baselines in CMTL tasks.

---

## 论文详细总结（自动生成）

# 论文《Learning with Preserving for Continual Multitask Learning》详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：在自动驾驶、医学影像分析等关键领域，AI 系统需要利用**同一数据流**持续学习新任务（例如先学习交通标志检测，再学习交通灯分类）。这一现实场景被定义为**持续多任务学习（CMTL）**，它要求模型顺序学习多个共享输入分布的任务，同时**不遗忘**先前学到的能力。
- **现有方法的不足**：传统持续学习方法（如参数冻结、重放缓冲）设计时侧重于防止灾难性遗忘，但往往**学习碎片化的任务特定特征**，导致特征间相互干扰，无法构建用于多任务的有用共享表示。
- **核心挑战**：CMTL 结合了多任务学习（需要共享表示）和持续学习（需要避免遗忘）的难点，且通常无法同时访问所有任务的标注数据。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出 **Learning with Preserving (LwP)** 框架，将重点从**保留任务输出**转移到**维护共享表示空间的几何结构**。通过保持数据点在潜在空间中的成对距离关系，保留隐式知识，从而支持多个任务。
- **关键技术细节**：
  - **模型架构**：共享特征提取器 \( f_{\theta_s} \) 产生表示 \( z \)，每个任务 \( t \) 有单独的任务头 \( g_{\theta_t} \)（通常是线性层）。
  - **训练流程**（以任务 \( t \) 为例）：
    1. 复制任务 \( t-1 \) 的模型并冻结（作为教师），添加新任务头。
    2. 当前模型使用复合损失函数 \( L_{lwp} = \lambda_c L_{cur} + \lambda_o L_{old} + \lambda_d L_{DWDP} \) 训练。
       - \( L_{cur} \)：当前任务的监督损失。
       - \( L_{old} \)：蒸馏损失，匹配教师模型对旧任务的伪标签。
       - \( L_{DWDP} \)：**动态加权距离保留损失**，核心创新。
  - **DWDP 损失公式**：
    \[
    L_{DWDP} = \frac{1}{N^2} \sum_{i,j} m_{ij} \left( d(z_i^{(t-1)}, z_j^{(t-1)}) - d(z_i^{(t)}, z_j^{(t)}) \right)^2
    \]
    其中 \( d \) 为平方欧氏距离，\( m_{ij} \) 是基于当前任务标签的动态掩码：同类时为1，异类时为0。
  - **理论动机**：保留成对距离等价于保留高斯核 Gram 矩阵，从而在 RKHS 中保持表示的功能等价性，使旧任务上的最优解仍适用于新表示。
  - **无重放缓冲**：LwP 不需要存储样本，适合隐私敏感场景。

## 3. 实验设计

- **数据集与场景**：
  - **图像数据集**：BDD100K（驾驶场景）、CelebA（人脸属性）、FairFace（人脸属性）。
  - **时间序列数据集**：PhysiQ（IMU 运动质量评估）。
  - **非平稳分布场景**：在 BDD100K 上构建天气、场景、时间、组合等移位任务，模拟现实分布变化。
- **对比方法**：
  - 持续学习方法：LwF、oEWC、ER、SI、GSS、FDR、DER、DERPP、DVC、OBC 等。
  - 单任务学习（STL）和朴素微调（FT）作为基线。
  - 部分方法与 MTL 方法对比（附录中另有说明）。
- **评估指标**：平均测试准确率、标准差、后向迁移（BWT）。

## 4. 资源与算力

- 论文**未明确说明**使用的 GPU 型号、数量或训练时长。仅在实验设置中提到每个模型训练 5 次、20 epoch、批量大小 256（图像）或 32（PhysiQ），无具体硬件信息。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验：在 4 个数据集（含非平稳变体共 8 个场景）上对比 11 种基线方法，每组 5 次随机种子。
  - 后向迁移分析：在 3 个数据集上绘制 BWT 柱状图。
  - 非平稳鲁棒性实验：4 种移位场景。
  - 消融实验：在 PhysiQ 上测试动态加权、不同距离度量（Cosine、RBF、Co2L、RKD）、是否包含蒸馏损失等组合。
  - 超参数敏感性分析：在 BDD100K 天气移位场景上展示 LwP 对超参数的稳定性。
  - 模型缩放实验：在 CelebA 上测试 ResNet50/101 以及不同输入尺寸（32×32 vs 224×224）。
- **充分性与公平性**：
  - 实验覆盖多模态（图像、时间序列）、多任务数量（3任务、10任务）、分布偏移场景，较为全面。
  - 对比基线均为公开 SOTA 方法，且 LwP 在大多数场景下显著优于它们，甚至超过 STL 上界，显示了较强说服力。
  - 消融实验验证了每个组件（动态加权、蒸馏、距离选择）的必要性。
  - 不足：未在更大规模模型（如 ViT）或更多任务（如 20+ 任务）上验证；未提供与其他知识蒸馏类方法（如 PODNet）的直接对比；PhysiQ 数据集较小，稳定性略低。

## 6. 主要结论与发现

- LwP 在 **所有 CMTL 基准**上一致优于现有持续学习方法，且是**唯一超过 STL 基线**的方法，表明它能有效缓解任务干扰。
- 通过保持表示空间几何结构，LwP 显著提升**后向迁移（BWT）**，减少灾难性遗忘。
- 在非平稳任务分布（环境移位）下，LwP 的鲁棒性更强，优势更加突出。
- 动态加权避免目标冲突，平方欧氏距离+类内保留是最优配置。
- 方法无重放缓冲，适用于隐私敏感场景。

## 7. 优点

- **创新性强**：明确定义 CMTL 问题，识别现有 CL 方法的弱点，并提出以几何结构保留为核心的解决方案。
- **技术有效**：DWDP 损失在理论和实验上都证明能保持表示功能等价性，同时支持多任务共享。
- **实用性好**：无需重放缓冲，内存高效，便于隐私保护；对超参数不敏感，易于部署。
- **实验充分**：多数据集、多模态、分布偏移、消融、缩放等实验验证了方法的有效性和稳定性。
- **可复现**：提供开源代码和扩展版本。

## 8. 不足与局限

- **复杂度**：DWDP 损失计算成对距离，复杂度为 \( O(N^2) \)，在大批量或大模型上可能成为瓶颈。作者提到未来考虑低秩近似，但当前版本未解决。
- **实验覆盖有限**：
  - 未在更大规模任务序列（如 20+ 任务）上测试。
  - 仅对比了部分持续学习方法，缺少与最新基于记忆的预训练方法（如 EWC+ 变体、Prompt-based 方法）的比较。
  - 未在纯在线（单次遍历）或极度资源受限场景下评估。
- **偏差风险**：仅使用 ResNet/1D-CNN 架构，未测试 Transformer 等现代骨干网络；数据集均为公开学术基准，实际工业场景表现未知。
- **理论深度**：虽提供了 RKHS 等价性的论证，但未给出严格的泛化界或遗忘上界分析。
- **超参数敏感性分析仅在单一场景进行**，在其他数据集上可能略有不同。

（完）
