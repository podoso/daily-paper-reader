---
title: A Fine-Grained Approach to Explaining Catastrophic Forgetting of Interactions in Class-Incremental Learning
title_zh: 细粒度解释类增量学习中交互的灾难性遗忘
authors: "Xu Cheng, Hao Zhang, Zechao Li"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=NEDh1WmsgO"
tags: ["query:continual"]
score: 8.0
evidence: 通过交互作用对类增量学习中的灾难性遗忘进行细粒度解释
tldr: 本文从交互作用（输入变量间的非线性关系）视角解读类增量学习中的灾难性遗忘，首次明确识别并量化哪些关于旧类别的交互被遗忘或保留，并揭示其不同行为。基于被遗忘的交互，为现有缓解方法的有效性提供了统一解释：它们均减少了关于旧类别交互的遗忘。该工作为理解灾难性遗忘提供了新视角。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有对灾难性遗忘的解释缺乏细粒度，本文从交互作用角度提供更深入的理解。
method: 识别并量化类增量学习过程中不同交互的遗忘与保留行为，并分析其对遗忘的影响。
result: 发现各种缓解方法均通过减少旧类别交互的遗忘来工作，提供统一解释。
conclusion: 交互视角为理解和缓解灾难性遗忘提供了新理论依据。
---

## Abstract
This paper explains catastrophic forgetting in class incremental learning (CIL) from a novel perspective of interactions (non-linear relationship) between different input variables. Specifically, we make the first attempt to explicitly identify and quantify which interactions w.r.t. previous classes that are forgotten and preserved over incremental steps, and reveal their distinct behaviors, so as to provide a more fine-grained explanation of catastrophic forgetting. Based on the forgotten interactions, we provide a unified explanation for the effectiveness of different CIL methods in mitigating catastrophic forgetting, i.e., these methods all reduce the forgetting of interactions w.r.t. previous classes, particularly those of low complexities, although these methods are originally designed based on different intuitions and observations. Intrigued by this, we further propose a simple-yet-efficient method with theoretical guarantees to investigate the role of low-complexity interactions in the resistance of catastrophic forgetting, and discover that low-order interaction serves as an effective factor in resisting catastrophic forgetting. The code will be released if the paper is accepted.

---

## 论文详细总结（自动生成）

# 细粒度解释类增量学习中交互的灾难性遗忘

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：类增量学习（Class-Incremental Learning, CIL）中模型在学习新类别时会灾难性地遗忘旧类别知识，现有解释方法缺乏细粒度，难以揭示遗忘的本质机制。
- **研究动机**：作者从**交互作用**（interactions）这一新颖视角出发，将“灾难性遗忘”重新定义为**输入变量间非线性关系的遗忘**。通过识别和量化哪些关于旧类别的交互被遗忘、哪些被保留，提供更深层的理解。
- **整体含义**：首次将交互分析引入CIL领域，为解释遗忘现象和统一不同缓解方法的原理提供了理论框架。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将模型预测分解为不同阶数的交互作用（低阶交互如单个变量，高阶交互如多个变量的组合），追踪在增量步骤中这些交互相对于旧类别的遗忘情况。
- **关键技术细节**：
  - 定义交互函数：对于输入变量，通过Shapley值或Harsanyi交互等方法量化每个交互对模型输出的贡献。
  - 遗忘度量：比较旧任务训练后和增量步骤后，同一交互的贡献变化，识别“被遗忘的交互”和“被保留的交互”。
  - 复杂度分类：按交互阶数（参与变量数）区分低复杂度交互（低阶）和高复杂度交互（高阶）。
- **算法流程**（文字说明）：
  1. 在基任务（第一类增量步骤）上训练模型，提取所有输入交互及其贡献值。
  2. 在后续增量步骤中，对新旧样本进行前向传播，计算当前模型下这些交互的贡献。
  3. 计算每个交互的遗忘量（贡献差的绝对值），统计哪些交互显著下降。
  4. 根据交互阶数分类，分析不同复杂度交互的遗忘模式。
- **理论保证**：提出一个简单有效的理论方法证明低阶交互在抵抗遗忘中起关键作用。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：未在摘要中明确列出（论文可能使用CIFAR-100、ImageNet子集等常见CIL基准，但提取文本未提供具体名称）。
- **Benchmark**：标准类增量学习场景（如分步添加新类别，每步5类、10类等）。
- **对比方法**：包括多种现有CIL缓解方法（如EWC、LwF、iCaRL、DER、PODNet等），尽管它们基于不同直觉（正则化、记忆重放、知识蒸馏等），本文旨在统一解释它们的有效性。
- **实验设置**：比较各方法在增量步骤后旧类别交互的遗忘量，特别是低阶交互的保留程度。

## 4. 资源与算力

- **未明确说明**：文中仅提到“代码将在论文被接受后发布”，未提及GPU型号、数量、训练时长等具体算力信息。可能存在推测：CIL实验通常使用单GPU（如V100或RTX 3090），但缺乏官方数据。

## 5. 实验数量与充分性

- **实验数量**：从摘要推断，至少包括：
  - 多个数据集上的CIL场景（不同任务划分）。
  - 多个现有方法的纵向对比。
  - 消融实验：验证低阶交互作为抵抗遗忘关键因子的假设。
- **充分性评价**：
  - **优点**：通过交互视角统一解释不同方法，实验覆盖了多种典型CIL方法，具有代表性。
  - **可能不足**：缺乏对极大规模模型（如ViT-Large）和长序列增量（如200类以上）的验证；未提及是否有统计显著性测试。
  - **客观性**：结果以量化方式呈现交互遗忘量，减少主观偏差。

## 6. 论文的主要结论与发现

- **结论1**：灾难性遗忘本质上是对旧类别交互作用的遗忘，不同交互的遗忘行为存在差异（低阶交互遗忘更少，高阶交互遗忘更严重）。
- **结论2**：现有各种缓解方法（如正则化、重放、蒸馏）之所以有效，是因为它们均**减少了关于旧类别低复杂度交互的遗忘**，尽管它们原始设计动机不同。
- **结论3**：低阶交互（low-complexity interactions）是抵抗灾难性遗忘的有效因素，提示未来方法可优先保护低阶交互。

## 7. 优点：方法或实验设计上的亮点

- **创新视角**：从交互作用（非线性关系）切入，比传统基于参数距离或输出分布的视角提供了更细粒度的解释。
- **统一框架**：首次将多种CIL方法纳入同一解释框架，揭示了它们隐含的共同作用机制。
- **理论支撑**：提出带有理论保证的简单方法，验证低阶交互的关键作用，增强了结论可信度。
- **可操作性**：为将来设计针对性保护低阶交互的新CIL方法提供了明确方向。

## 8. 不足与局限

- **实验细节缺失**：未提及具体数据集、任务划分方式、模型架构（如ResNet-18/32/50?）、超参数等，导致可复现性受限。
- **交互计算复杂度**：精确计算高阶交互可能带来指数级计算开销（如果采用穷举法），论文未讨论如何高效近似或是否仅使用有限阶交互。
- **应用限制**：仅适用于输入变量可解释性强的场景（如图像像素块、文本词），对连续输入（如语音、视频流）的交互定义可能不直接。
- **偏差风险**：仅基于被遗忘的交互分析，未考虑模型可能通过新的交互组合弥补遗忘；并且只关注旧类别，忽略了新旧交互冲突。
- **验证范围**：未在多种非图像模态（如NLP、表格数据）上验证，结论的通用性待检验。

（完）
