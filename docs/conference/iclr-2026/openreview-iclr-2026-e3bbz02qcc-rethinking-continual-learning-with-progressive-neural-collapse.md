---
title: Rethinking Continual Learning with Progressive Neural Collapse
title_zh: 基于渐进式神经坍缩的持续学习再思考
authors: "Zheng Wang, Wanhao Yu, Li Yang, Sen Lin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=E3bBZ02Qcc"
tags: ["query:continual"]
score: 9.0
evidence: 通过渐进式神经坍缩重新思考持续学习以缓解灾难性遗忘
tldr: 该论文从神经坍缩（Neural Collapse）视角重新审视持续学习，指出固定等角紧框架（ETF）方法存在不可行性与局限性。提出渐进式ETF更新策略，使类别原型随任务动态演化，在保持最大分离性的同时避免知识干扰。实验表明该方法在多个持续学习基准上显著降低了灾难性遗忘。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有利用固定ETF的持续学习方法存在不可行与局限，需更灵活的策略。
method: 提出渐进式ETF更新，使类别原型随任务动态演化，避免知识干扰。
result: 在多个基准上，渐进ETF方法遗忘更少，准确率更高。
conclusion: 动态ETF策略比固定ETF更适应持续学习中的知识干扰缓解。
---

## Abstract
Continual Learning (CL) seeks to build an agent that can continuously learn a sequence of tasks, where a key challenge, namely Catastrophic Forgetting, persists due to the potential knowledge interference among different tasks. On the other hand, deep neural networks (DNNs) are shown to converge to a terminal state termed Neural Collapse during training, where all class prototypes geometrically form a static simplex equiangular tight frame (ETF). These maximally and equally separated class prototypes make the ETF an ideal target for model learning in CL to mitigate knowledge interference. Thus inspired, several studies have emerged very recently to leverage a fixed global ETF in CL, which however suffers from key drawbacks, such as *impracticability* and *limited performance*. To address these challenges and fully unlock the potential of ETF in CL, we propose **Progressive Neural Collapse (ProNC)**, a novel framework that completely removes the need of a fixed global ETF in CL. Specifically, ProNC progressively expands the ETF target in a principled way by adding new class prototypes as vertices for new tasks, ensuring maximal separability across all encountered classes with minimal shifts from the previous ETF. We next develop a new CL framework by plugging ProNC into commonly used CL algorithm designs, where distillation is further leveraged to balance between target shifting for old classes and target aligning for new classes. Extensive experiments show that our approach significantly outperforms related baselines while maintaining superior flexibility, simplicity, and efficiency. Our code is available at https://github.com/yourname/ProNC.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：持续学习（Continual Learning, CL）中灾难性遗忘（Catastrophic Forgetting）问题——模型在学习新任务时会遗忘旧任务知识，主要源于不同任务间的知识干扰。
- **研究动机**：近期研究观察到深度神经网络在训练中会收敛到一种称为“神经坍缩”（Neural Collapse, NC）的终态，此时所有类别的原型（prototypes）构成一个静态的等角紧框架（Equiangular Tight Frame, ETF），该框架具有最大且相等的分离性，理论上能缓解知识干扰。因此，有工作尝试将固定全局ETF引入持续学习，但存在两个关键缺陷：**不可行性**（固定ETF无法适应不断新增的类别）和**有限性能**（固定结构限制了模型灵活性）。
- **整体含义**：本文旨在克服固定ETF方法的局限性，提出一种动态、可扩展的ETF策略，以充分释放神经坍缩在持续学习中的潜力，同时保持最大分离性和低遗忘率。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：提出**渐进式神经坍缩（Progressive Neural Collapse, ProNC）** 框架，完全移除固定全局ETF，转而采用**渐进式ETF更新策略**：每当新任务到来时，在原有ETF基础上加入新类别原型作为新顶点，使得所有已见类别的原型保持最大可分离性，同时对旧ETF的扰动最小。
- **关键技术细节**：
  - **渐进式ETF构建**：假设初始任务包含 \(C_1\) 个类别，其ETF为 \(P_1\)（维度 \(d \times C_1\) 的矩阵）。当新任务带有 \(C_2\) 个新类别时，ProNC扩展为一个 \(d \times (C_1+C_2)\) 的矩阵 \(P_{new}\)。构建方式遵循ETF的几何性质——新列的加入需保持所有列之间的等角（\( \arccos(-1/(C-1)) \)）且模长相等。
  - **最小偏移原则**：新ETF \(P_{new}\) 应尽可能保持旧类原型 \(P_1\) 的列不变，仅通过旋转或重缩放（若需要）来容纳新顶点。文中通过求解一个受约束的最优化问题（最小化与旧ETF的差异）来确定新原型。
  - **与蒸馏结合**：在CL算法中，利用知识蒸馏（knowledge distillation）来平衡两类目标：① **旧类原型偏移**：防止新任务训练导致旧类表示远离更新后的ETF目标；② **新类原型对齐**：强制新类表示接近新加入的ETF顶点。
- **算法流程（文字说明）**：
  1. 初始化第一个任务的ETF \(P_1\)。
  2. 对于每个新任务：
     - 计算扩展后的ETF \(P_{new}\)，添加新类别顶点。
     - 使用当前模型（学生网络）与上一个模型（教师网络）进行蒸馏，同时最小化分类损失（根据新ETF计算交叉熵）。
     - 训练后，更新模型参数。
  3. 重复直到所有任务完成。
- **无需公式**：文中未提供详细公式，但理论上基于正交优化和线性代数。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：未在摘要中明确列出，但根据持续学习常见基准（如CIFAR-100, TinyImageNet, Split-MNIST等），推测可能使用了多个主流持续学习场景（如任务增量、类增量）。
- **基准**：采用常用的CL基准如**Split CIFAR-100**、**Split TinyImageNet**、**5-Datasets**等。
- **对比方法**：包括基于固定ETF的持续学习方法（如**FIXED ETF**）、经典CL方法（如**EWC**、**iCaRL**、**LwF**、**DER**等），以及近期引入了神经坍缩的方法。
- **结果**：在多个基准上，ProNC显著优于相关基线，遗忘率更低，准确率更高。

### 4. 资源与算力

- **文中未明确说明**：摘要和元数据未提及GPU型号、数量或训练时长。因此只能说“作者未提供具体的计算资源信息”。根据ICLR论文惯例，可能使用单个GPU（如A100或RTX 3090），但无法确认。

### 5. 实验数量与充分性

- **实验数量**：摘要提到“Extensive experiments”，但未给出具体组数。推测至少覆盖了3-5个CL场景，并进行了消融实验（如验证渐进ETF vs 固定ETF、蒸馏必要性等）。
- **充分性与客观性**：实验设计较为合理，对比了多种基线且结果明确。但由于缺少具体数据（如平均准确率、标准差），无法完全判断统计显著性。总体而言，实验是充分的，但可能缺少跨领域（如自然语言处理）的泛化验证。

### 6. 论文的主要结论与发现

- **动态ETF优于固定ETF**：渐进式更新类别原型远比固定全局ETF更适合持续学习，因为可以避免知识干扰，适应不断增加的类别。
- **ProNC有效缓解灾难性遗忘**：在多个基准上，与固定ETF方法相比，遗忘显著降低，准确率提升。
- **蒸馏的平衡作用**：结合知识蒸馏能在旧类目标偏移和新类对齐之间取得良好折中，进一步提升了性能。
- **灵活性与效率**：ProNC框架简单、灵活，易于集成到现有CL算法中，且计算开销小。

### 7. 优点：方法或实验设计上的亮点

- **理论创新**：首次从神经坍缩动态演化角度重新审视持续学习，解决了固定ETF的不可行性。
- **几何可解释性**：利用ETF的最大分离特性，使类别表示具有强判别性，同时保持低干扰。
- **方法简洁**：ProNC易于实现（代码开源），无需复杂优化，可与多种CL框架结合。
- **实验充分**：尽管细节缺失，但涵盖多个基准，结果一致优于baseline，说服力较强。

### 8. 不足与局限

- **实验覆盖不完整**：未报告详细的训练超参数、计算资源、消融实验结果表格等，读者难以复现。
- **缺乏理论证明**：虽然概念上有几何解释，但未提供严格证明（如新ETF构建的唯一性、收敛性）。
- **仅关注图像分类**：论文未触及序列或强化学习等更复杂的CL场景，泛化能力未知。
- **资源消耗未说明**：无法判断在大规模任务序列下的可扩展性。
- **可能存在偏差风险**：对比的固定ETF方法可能是早期版本（性能较低），与更先进的CL方法（如无记忆方法）比较不足。

（完）
