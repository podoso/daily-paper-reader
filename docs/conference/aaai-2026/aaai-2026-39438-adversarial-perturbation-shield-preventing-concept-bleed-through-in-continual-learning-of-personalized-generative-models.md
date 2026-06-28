---
title: "Adversarial Perturbation Shield: Preventing Concept Bleed-through in Continual Learning of Personalized Generative Models"
title_zh: 对抗扰动盾：防止持续学习中个性化生成模型的概念渗漏
authors: "Ziwen Lan, Keisuke Maeda, Takahiro Ogawa, Miki Haseyama"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39438/43399"
tags: ["query:continual"]
score: 7.0
evidence: 对抗扰动防止持续学习中的概念渗漏
tldr: 个性化文本到图像扩散模型在持续学习中面临概念渗漏问题，新概念覆盖旧概念。本文提出对抗扰动训练策略，在潜在空间维护语义表征的独特性。该方法有效减少概念干扰，适用于持续学习的个性化生成场景。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 持续学习场景下，新概念覆盖旧概念导致概念渗漏，现有模型级方法无法完全保留语义。
method: 在潜在空间添加对抗扰动以强化旧概念表征，防止被新概念干扰。
result: 在个性化扩散模型持续学习中有效降低概念渗漏，保持生成质量。
conclusion: 对抗扰动策略为持续生成学习提供有效保护机制。
---

## Abstract
Personalized text-to-image diffusion models have gained increasing attention because they can generate images that contain unique concepts based on limited training data. However, in continual learning scenarios, these models suffer from concept bleed-through, where newly introduced concepts frequently overwrite or interfere with the previously learned concepts. Previous studies have attempted to mitigate this issue at the model adaptation level; however, they failed to fully preserve the distinct semantic representations in the latent space. Thus, this paper proposes an adversarial perturbation-based training strategy to address concept bleed-through in continual learning for personalized diffusion models. The proposed method introduces adversarial perturbations into the training images, which strategically shifts their semantic representations in the latent space to ensure that the newly learned concepts remain distinct and do not interfere with the previously acquired knowledge. Unlike structural modifications to the model, the proposed method operates at the data level, which makes it broadly applicable to existing continual personalization frameworks without increasing model complexity. Experimental results demonstrate that the proposed method significantly improves concept separation while maintaining high image fidelity, offering a solution to enhance the reliability of continual learning in personalized generative models.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

个性化文本到图像扩散模型（如 DreamBooth、LoRA）能够基于少量参考图像学习用户提供的独特概念（如特定物体、风格）。然而，在实际应用中，模型需要**持续学习**一系列新概念，即按顺序学习多个概念而无法访问之前的训练数据。这带来了两个关键问题：
- **灾难性遗忘**：学习新概念时覆盖旧概念；
- **概念渗漏（Concept Bleed-through）**：新概念干扰旧概念的生成，导致生成图像出现意外的混合或错误输出（例如，学习“小狗”后，生成“哈士奇”时却混入了“小狗”的特征）。

现有方法（如 C-LoRA、CIDM）在模型结构层面进行改进，但未能完全保留潜在空间中不同概念的语义独特性，且增加了模型复杂度，兼容性有限。本文旨在解决概念渗漏问题，提出一种**基于对抗扰动的数据级训练策略**，在不修改模型结构的前提下，通过在训练图像中添加精心设计的对抗扰动，将新概念的潜在表征“推离”旧概念区域，从而实现清晰的概念分离。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 核心思想
在持续学习每个新概念时，对其训练图像施加微小的人眼不可见的对抗扰动，使得扰动后的图像在扩散模型的潜在空间中的嵌入朝着一个**语义不相似的目标图像**方向偏移。这样，新概念的潜在表征区域与先前概念的潜在区域在空间中拉开距离，从而避免新学习的概念干扰旧概念的生成。

### 关键技术细节
1. **持续学习框架（基于 LoRA）**：
   - 采用 LoRA 技术更新 U-Net 交叉注意力层中的 Key 和 Value 投影矩阵，每次新任务只添加低秩矩阵 \(A_t\) 和 \(B_t\)，增量式累积参数：
     \[
     W_t^{K,V} = W_{t-1}^{K,V} + A_t^{K,V} B_t^{K,V}
     \]
   - 保留预训练权重，保证参数高效。

2. **自正则化损失**：
   - 为了防止新参数与旧参数产生重叠干扰，引入自正则项：
     \[
     L_{\text{forget}} = \left\| \sum_{t'=1}^{t-1} A_{t'}^{K,V} B_{t'}^{K,V} \odot A_t^{K,V} B_t^{K,V} \right\|_F^2
     \]
   - 它惩罚新参数与旧参数的元素乘积的 Frobenius 范数，强制它们在潜在空间中的激活区域不重叠。

3. **对抗扰动优化（核心创新）**：
   - 对于当前新概念的图像 \(x_t\)，从 ImageNet 中选取一张与旧概念语义不相似的目标图像 \(x_t^{\text{pr}}\)。
   - 使用**有目标投影梯度下降（PGD）** 优化扰动 \(\delta\)，满足 \(\|\delta\|_\infty \le \epsilon\)（预算 8/255）：
     \[
     \delta = \arg\min_{\|\delta\|\le\epsilon} \left\| E(x_t^{\text{pr}}) - E(x_t + \delta) \right\|_2^2
     \]
     其中 \(E\) 是扩散模型的编码器。该优化使扰动后图像的潜在编码逼近目标图像编码，从而在潜在空间中将当前概念“拉向”与旧概念无关的区域。

4. **整体训练目标**：
   - 在学习新任务时，最小化总损失：
     \[
     L_{\text{total}} = L_{\text{diff}}(i, \theta) + \lambda L_{\text{forget}}
     \]
     其中 \(L_{\text{diff}}\) 是标准扩散损失。

### 算法流程
1. 对于每个新概念任务 \(t\)，给定该概念的参考图像集；
2. 从 ImageNet 中采样一张与之前所有概念语义不相似的目标图像；
3. 使用 PGD 优化，计算每张参考图像的对抗扰动；
4. 将带扰动的图像用于 LoRA 微调，同时加入自正则损失；
5. 学习完毕后，LoRA 权重累加至模型，用于后续任务和生成。

## 3. 实验设计

### 数据集与场景
- **训练概念数据集**：
  - DreamBooth 官方数据集（30 个概念类，每类 5-6 张图像）
  - CustomConcept101（101 个概念类，每类 3-15 张图像）
- **目标图像来源**：ImageNet（用于扰动优化）
- **评估场景**：持续学习序列，通常依次学习 2 个或 10 个概念，测试生成质量与概念分离度。

### Benchmark 与对比方法
- **单概念基线**：Textual Inversion、DreamBooth、InstantBooth
- **多概念框架**：Custom Diffusion、ED-LoRA
- **持续学习 SOTA**：C-LoRA、STAMINA、CIDM
- **选择性遗忘方法**：Selective Amnesia（SA）

### 评估指标
- **AMMD（平均最大均值差异）**：衡量所有概念生成图像与真实图像的分布差异，越低越好。
- **FMMD（遗忘程度）**：旧概念在学完新任务后 MMD 的增量，越低代表遗忘越少。
- **CLIP Score**：生成图像与文本提示的语义对齐度，越高越好。

### 额外实验
- **概念数量影响**：训练序列包含 10 个概念（如花瓶、猫1、绿植、猫2等），比较基线 STAMINA 与加扰动的版本。
- **目标图像类别影响**：固定学习序列“桌子→椅子”，分别使用五种不同目标图像（花瓶、狗、飞机、面包、微波炉）进行扰动优化，评估生成效果。
- **与选择性遗忘对比**：在“桌子→椅子”任务上，比较 C-LoRA + 我们的方法 vs C-LoRA + Selective Amnesia（遗忘旧概念）。

## 4. 资源与算力

论文**未明确说明**使用的 GPU 型号、数量、训练时长等硬件信息。仅提及：
- 预训练模型：Stable Diffusion v1.5
- LoRA 秩：16
- 学习率：\(2 \times 10^{-6}\)
- 每张图像训练步数：100
- 扰动优化步数：40，批量大小：4

未提供具体算力细节，这对于结果复现和效率评估是不足的。

## 5. 实验数量与充分性

### 主要实验
- 基于 100 种不同的两概念学习序列（随机配对），取平均结果，保证了统计意义。
- 提供了定性结果（图3）展示生成图像，直观体现概念分离效果。

### 额外实验
- **概念数量实验**：单序列 10 个概念，具有挑战性，验证了方法在更长序列下的有效性。
- **目标图像类别实验**：5 种不同语义相似度的目标图像，系统性地探讨了扰动优化的关键因素。
- **与选择性遗忘对比**：1 组专门对比，证明了方法的优势。

### 充分性评价
- 实验覆盖了多种持续学习场景（2 概念、10 概念）、多种基线方法（单概念、多概念、持续学习）、以及消融式分析（目标图像选择）。
- 但缺乏超参数敏感性分析（如扰动预算、正则化系数 λ 的影响），也未在更多扩散模型（如 SDXL）上验证泛化性。总体而言，实验设计比较扎实，结论可信，但细节可进一步补充。

## 6. 主要结论与发现

1. 所提对抗扰动策略显著降低了概念渗漏，相比基线方法（C-LoRA、STAMINA、CIDM）在 **AMMD 和 CLIP Score** 上均有提升（例如，CIDM+Ours 的 AMMD 从 2.11 降至 1.98，CLIP 从 0.85 升至 0.87）。
2. 方法有效缓解了遗忘，FMMD 与最佳基线持平或更优。
3. 在更长序列（10 个概念）下，扰动方法显著减少了语义漂移，生成图像更准确地保留初始概念（花瓶）。
4. **目标图像的选择至关重要**：选择与旧概念语义差异大的目标图像（如狗、面包）效果更好；相似目标（如花瓶、微波炉）则概念分离效果下降。
5. 与选择性遗忘方法相比，本文方法能够在**不主动遗忘旧概念**的前提下达到类似的干扰抑制效果，从而保留对旧概念的生成能力。

## 7. 优点

- **创新性**：首次将对抗扰动引入扩散模型的持续学习，从数据层面解决概念渗漏问题，思路新颖。
- **兼容性**：数据级操作，可直接叠加到现有持续学习框架（C-LoRA、STAMINA、CIDM）上，无需修改模型结构，增加额外复杂度。
- **理论动机清晰**：通过最大化潜在空间中的余弦距离，等效于对比学习，有明确几何解释。
- **实验设计全面**：包含多数据源、多对比方法、多评估指标，并设计了额外消融实验，验证了关键变量（概念数量、目标图像选择）的影响。
- **与选择性遗忘的对比**：展示了方法在保留知识方面的优势，增强了实用性。

## 8. 不足与局限

- **算力资源缺失**：未报告训练耗时、GPU 型号等信息，影响复现和效率评估。
- **超参数未充分探讨**：扰动预算固定为 8/255，未研究其对生成质量与分离效果的影响；自正则系数 λ 仅提及指数搜索，未给出具体值与敏感性分析。
- **目标图像依赖**：方法需要额外选择语义不相似的目标图像，实际应用中若选择不当（如无意中与旧概念相似）会削弱效果。
- **泛化性有限**：仅在 Stable Diffusion v1.5 上验证，未测试其他扩散模型或生成任务（如文本引导编辑、视频生成）。
- **对比基线不够全面**：未与基于回放的持续学习方法（如 A-GEM、GSS）对比，也未与 prompt 无关的方法比较。
- **复杂度考量缺失**：对抗扰动优化需要额外计算开销，论文未分析训练时间增加比例。

（完）
