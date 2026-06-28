---
title: PANDA – Patch and Distribution-Aware Augmentation for Long-Tailed Exemplar-Free Continual Learning
title_zh: PANDA – 面向长尾无样本持续学习的补丁与分布感知增强
authors: "Siddeshwar Raghavan, Jiangpeng He, Fengqing Zhu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39694/43655"
tags: ["query:continual"]
score: 8.0
evidence: 无样本持续学习中缓解灾难性遗忘的技术
tldr: 无样本持续学习因不能存储旧任务数据极易发生灾难性遗忘，且真实数据流存在数据集级和任务内的双重不平衡。本文提出PANDA框架，结合补丁感知和分布感知数据增强，无缝集成现有基于预训练模型的无样本持续学习方法。实验表明，PANDA能有效缓解双重不平衡造成的遗忘，在长尾分布下性能显著提升。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 真实世界数据流存在数据集级和任务内双重不平衡，加剧了无样本持续学习中的灾难性遗忘。
method: 提出补丁感知和分布感知数据增强框架，与现有预训练模型结合以缓解不平衡导致的遗忘。
result: 在多个长尾持续学习基准上，PANDA显著降低了遗忘率并提高了平均准确率。
conclusion: PANDA通过针对性增强有效应对了长尾分布下的灾难性遗忘问题。
---

## Abstract
Exemplar-Free Continual Learning (EFCL) restricts the storage of previous task data and is highly susceptible to catastrophic forgetting. While pre-trained models (PTMs) are increasingly leveraged for EFCL, existing methods often overlook the inherent imbalance of real-world data distributions. We discovered that real-world data streams commonly exhibit dual-level imbalances, dataset-level distributions combined with extreme or reversed skews within individual tasks, creating both intra-task and inter-task disparities that hinder effective learning and generalization. To address these challenges, we propose PANDA, a Patch-and-Distribution-Aware Augmentation framework that integrates seamlessly with existing PTM-based EFCL methods. PANDA amplifies low-frequency classes by using a CLIP encoder to identify representative regions and transplanting those into frequent-class samples within each task. Furthermore, PANDA incorporates an adaptive balancing strategy that leverages prior task distributions to smooth inter-task imbalances, reducing the overall gap between average samples across tasks and enabling fairer learning with frozen PTMs. Extensive experiments and ablation studies demonstrate PANDA's capability to work with existing PTM-based CL methods, improving accuracy and reducing catastrophic forgetting.

---

## 论文详细总结（自动生成）

# 论文总结：PANDA – 面向长尾无样本持续学习的补丁与分布感知增强

## 1. 核心问题与研究动机

- **背景**：无样本持续学习（Exemplar-Free Continual Learning, EFCL）因无法存储旧任务数据，极易发生灾难性遗忘。近年来，基于预训练模型（PTM）的方法虽取得进展，但大多假设任务内类分布平衡，忽视了真实数据流中普遍存在的**双重不平衡**。
- **核心问题**：真实数据流同时存在**数据集级不平衡**（全局长尾）和**任务级不平衡**（任务内极端偏斜或反向偏斜），导致类间与任务间差异加剧，严重限制学习与泛化。
- **目标**：提出一种可无缝集成到现有 PTM 型 EFCL 方法的增强框架，缓解双重不平衡引起的灾难性遗忘。

## 2. 方法论：PANDA 框架

### 核心思想
PANDA 通过两种互补机制实现双重不平衡下的公平学习：
1. **任务内平衡（Intra-task Balancing）**：利用冻结的 CLIP 编码器识别尾类（低频类）图像中最具语义代表性的图像块（patch），将其转移到头类（高频类）样本的对应区域，合成新的尾类训练样本，从而增加尾类有效数量，减少头类偏置。
2. **任务间平滑（Inter-task Smoothing）**：通过可学习参数 β 融合先前任务与当前任务的分布极值（min/max），自适应校准分类器阈值，缓解任务间分布偏移导致的决策偏差。

### 关键技术细节
- **补丁选择**：每张图像分割为 N×N 非重叠块；利用冻结 CLIP 计算文本嵌入（如“Image of a {label}”）与各图像块嵌入的余弦相似度，选取 Top N/2 的高置信度补丁（阈值 0.45），生成二值掩码。
- **合成图像**：将尾类补丁掩码区域粘贴到头类图像背景中（保留头类背景），标签保持为尾类；再应用标准图像增强（翻转、裁剪、色彩抖动、高斯模糊）以防止过拟合。
- **迭代平衡**：重复上述过程，直到头类与尾类平均样本数之差 ≤ q。
- **自适应分布平滑**：维护先前任务的最大/最小值向量，通过 β 加权当前任务对应的值；β 根据任务性能变化动态调整（性能下降则降低 β 以快速适应，性能提升则增大 β 以保持稳定）。

### 算法流程（文字描述）
1. 当前任务 T_k 中，将样本分为头类集合 X_h 和尾类集合 X_t。
2. 对每个头类样本 x_h 和尾类样本 x_t，冻结 CLIP 提取图像块特征，选择语义相似度最高的补丁，生成掩码 M_h, M_t。
3. 合成新图像 x‘ = (M_h)‘ ⊙ x_h + M_t ⊙ x_t，标签为 y_t。
4. 应用增强后输入主干网络训练。
5. 通过自适应分布平滑调整当前任务分类阈值。

## 3. 实验设计

### 数据集与场景
- **CIFAR-100-LT**：通过指数衰减因子 ρ=0.01 生成长尾版本，任务数 10。
- **iNaturalist (100 classes)**：天然长尾分布，随机选取 100 类，任务数 10。
- **双级不平衡（DLI）设置**：在数据集级不平衡基础上，对特定任务施加更极端的任务级不平衡（ρ* = 0.05，作用于任务 2/3/4）。

### Benchmark 与对比方法
- **提示方法**：L2P、CodaPrompt、DualPrompt、DAP
- **基于表示的方法**：SimpleCIL、Adam w/ SSF、RanPAC、EASE、CoFiMA、SLCA、FeCAM、APART、APER、MOS
- **消融对比**：CutMix、Mixup、Remix、Contrastive CutMix；注意力亲和掩码（Attention Affinity Masking）

### 评估指标
- 平均准确率（Average Accuracy）
- 平均遗忘率（Average Forgetting）

## 4. 资源与算力

- **硬件**：单块 NVIDIA A40 GPU（未明确说明使用数量）
- **训练时间**：表 5 显示了各方法及其 +PANDA 的运行时（小时）。例如 RanPAC 基线 0.33h，+PANDA 0.42h；CoFiMA 基线 1.20h，+PANDA 1.43h。增加幅度较小（0.09~0.46h）。
- **GPU 显存**：如 L2P 基线 2994MB，+PANDA 3282MB（+288MB）；RanPAC 基线 5052MB，+PANDA 5517MB（+465MB）。整体资源增量有限。

> 注意：论文未给出总训练 GPU 数或全部实验的总算力，仅提供了单次运行的资源数据。

## 5. 实验数量与充分性

- **主实验**：在 CIFAR-100-LT 和 iNaturalist 上分别进行单级不平衡（SLI）和双级不平衡（DLI）共约 6 组场景，每组对比 15~20 种方法（基线 + PANDA），结果由 10 次重复取平均。
- **消融实验**：
  - 与其他长尾增强方法比较（表 3）：4 种增强 vs PANDA，在 SLI 和 DLI 下各 1 组。
  - 掩码策略对比（表 4）：注意力亲和掩码 vs PANDA 的 CLIP 掩码。
  - 资源用量（表 5）：6 种方法的 GPU 占用和运行时对比。
- **充分性评价**：实验覆盖了主流 PTM-EFCL 方法（提示类、表示类、定制类），涵盖两种数据集、两种不平衡模式、多种消融，统计上采用多重复平均，结果客观。但 DLI 场景仅选了 4 种 top 方法进行对比（表 2），缺少所有方法在 DLI 下的完整结果，覆盖稍显不足。

## 6. 主要结论与发现

1. 现有 EFCL 方法在单级不平衡下准确率显著下降，双级不平衡下退化更严重；PANDA 可稳定提升所有对比方法的平均准确率（1~8%）并降低遗忘率（0.2~2.6%）。
2. PANDA 的任务内平衡（CLIP 补丁迁移）优于传统增强（CutMix/Mixup/Remix/Contrastive CutMix），尤其在 DLI 下优势明显。
3. 基于 CLIP 语义的掩码选择优于基于注意力的亲和掩码，避免了关键特征丢失或背景混淆。
4. PANDA 资源开销适中，可实际部署。

## 7. 优点

- **创新性**：首次形式化 EFCL 中的双级不平衡问题，并提出兼具补丁级语义增强与分布级平滑的统一框架。
- **通用性**：PANDA 是训练无关（training-free）模块，可即插即用集成到任意 PTM-EFCL 方法，无需修改原有学习算法。
- **低资源需求**：运行时与显存增加很少，适合实际应用。
- **实验设计合理**：对比了多种主流基线，进行了消融和鲁棒性分析，10 次重复平均保证可靠性。

## 8. 不足与局限

- **依赖 CLIP 质量**：补丁选择完全依赖冻结 CLIP 的对齐能力，若 CLIP 在特定领域（如医学图像）表现差，PANDA 效果可能受限。
- **场景覆盖不全**：DLI 实验仅选用了 4 种代表性方法，缺乏对全部基线的对比，且未验证不同任务数（如 5 或 20 任务）下的表现。
- **未考虑更复杂的任务序列**：论文仅对任务级不平衡进行单任务扰动（* = 2,3,4），未研究连续多任务均不平衡的设定。
- **存储与计算假设**：尽管无需旧样本，但 PANDA 在训练时需要 CLIP 模型常驻显存，对极端边缘设备仍有压力。
- **缺乏理论分析**：未从理论上解释补丁迁移为何能改善双级不平衡下的泛化边界。

（完）
