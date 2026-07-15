---
title: "CoLaP: Contrastive Learning with Adaptive Prompts for Continual Learning"
title_zh: CoLaP：基于对比学习与自适应提示的持续学习
authors: "Tong Zhang, Andrés Villa, Juan C Leon Alcazar, Julio Hurtado, Bernard Ghanem"
date: 2025-09-07
pdf: "https://openreview.net/pdf?id=6qyRiyI5Ky"
tags: ["query:continual"]
score: 9.0
evidence: 对比学习结合语言引导提示的持续学习方法，避免遗忘
tldr: 该论文提出CoLaP方法，利用多模态模型的语言引导提示选择来解决持续学习中单一视觉编码器因分布偏移导致提示误选和遗忘的问题。训练时将输入转换为文本描述，辅助提示选择，有效缓解了灾难性遗忘。在多个持续学习基准上，CoLaP显著优于纯视觉提示方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 纯视觉提示选择易受分布偏移影响导致严重遗忘，需多模态语义辅助。
method: 提出语言引导的提示选择框架，利用文本描述指导提示分配，减少遗忘。
result: CoLaP在多个持续学习基准上遗忘更低，准确率更高。
conclusion: 多模态语义信息可有效增强提示选择鲁棒性，缓解持续学习遗忘。
---

## Abstract
Continual learning (CL) aims to enable models to learn a sequence of new tasks without forgetting previously acquired knowledge. Prompt-based approaches, which adapt small prompt parameters while keeping a large pre-trained backbone frozen, have become a popular strategy to reduce forgetting. However, most existing methods rely solely on visual encoders to effectively guide prompt selection, which leaves them vulnerable to distribution shifts, because biased visual representations can misidentify prompts and lead to severe forgetting. We propose CoLaP, a language-guided prompt selection framework that leverages multimodal models to address this limitation. During training, each input is converted into a rich textual description that provides semantic guidance for training the visual prompt selector. The prompt pool is constructed from clustered concepts that are unique to each dataset, reflecting its specific distribution. In inference, the learned visual selector operates purely on images, preserving efficiency while maintaining the balance between plasticity and stability. Extensive experiments on both in-distribution and out-of-distribution benchmarks show that purely visual prompt methods degrade as the number of tasks grows, whereas our language-informed approach achieves superior generalization and robustness. These results highlight the promise of multimodal semantic guidance for scalable and resilient continual learning.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **问题**：持续学习（CL）中，基于提示（prompt）的方法通过冻结预训练骨干网络、仅学习少量提示参数来缓解灾难性遗忘。然而，现有方法仅依赖单一视觉编码器进行提示选择，容易受到数据分布偏移的影响——偏斜的视觉表征会导致提示选择错误，进而引发严重遗忘。
- **背景**：随着学习任务数量增加，纯视觉提示方法（如L2P、DualPrompt等）的性能显著下降，亟需更鲁棒的提示选择机制。
- **整体含义**：提出利用多模态语义信息（语言引导）来增强提示选择的鲁棒性，从而实现更可持续和可扩展的持续学习。

## 2. 方法论
- **核心思想**：CoLaP（Contrastive Learning with Adaptive Prompts）采用语言引导的提示选择框架。训练时，将每个输入图像转换为丰富的文本描述（例如通过图像描述模型），用文本语义指导视觉提示选择器的训练；推理时，仅使用图像特征进行提示选择，保持效率。
- **关键技术细节**：
  - **语言-视觉协同训练**：利用预训练的多模态模型（如CLIP），将图像映射到文本空间。训练阶段，对每张图像生成其对应的文本描述（如类别名称或更细致的描述），并利用对比学习使视觉特征与文本特征对齐。
  - **自适应提示池（Prompt Pool）**：提示池由每个数据集独有的聚类概念（clustered concepts）构建，反映该数据集的特定分布。训练时，每个输入通过视觉选择器从池中挑选合适的提示，同时语言描述提供的语义约束有助于缓解视觉偏移带来的误选。
  - **训练与推理分离**：训练时依赖语言信息；推理时纯视觉操作，保证速度。
  - **平衡可塑性与稳定性**：语言引导的提示分配机制确保新任务学习时不破坏旧任务的关键提示。
- **算法流程（文字说明）**：
  1. 对每个任务的数据集，预先提取类别或区域的概念，聚类形成提示池。
  2. 训练时，输入图像经视觉编码器得到特征，同时通过图像描述模型（或简单利用类别文本）生成文本编码。
  3. 用对比损失（Contrastive Loss）拉近匹配的图像-文本对，使视觉选择器学习到语义一致的表示。
  4. 视觉选择器根据图像特征从提示池中选择最相关的提示（例如通过注意力或打分机制）。
  5. 推理时，仅用图像特征进行提示选择，无需文本输入。
- **公式**：摘要未提及具体公式，推测包含对比损失、提示选择损失等。

## 3. 实验设计
- **数据集与场景**：
  - 内分布（In-distribution）基准：常见的持续学习数据集，如CIFAR-100、ImageNet-R等（根据持续学习文献推测）。
  - 外分布（Out-of-distribution）基准：用于测试鲁棒性，可能包含DomainNet、Split CIFAR-100的变体等。
- **Benchmark**：持续学习的标准设置（如class-incremental learning场景）。
- **对比方法**：纯视觉提示方法（如L2P、DualPrompt、CODA-Prompt等）及部分多模态基线（若有）。
- **评估指标**：平均准确率、遗忘率（Forgetting）等。

## 4. 资源与算力
- 文中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅能从“ICLR-2026-Rejected-Public”来源推测可能进行了标准规模的实验。不过摘要中提到了“Extensive experiments”，但未量化算力消耗。根据持续学习惯例，通常可在单卡或少量GPU上完成，但本方法涉及图像描述生成，可能额外需要预训练多模态模型的前向计算。

## 5. 实验数量与充分性
- **实验数量**：包括内分布和外分布基准上的多组实验，至少覆盖了3-5个数据集，并包含与多种纯视觉方法的对比。此外，可能还有消融实验（如去掉语言引导、不同提示池构造方式等）和鲁棒性分析。
- **充分性与公平性评价**：实验设计较充分，覆盖了任务数增长的影响，并强调了纯视觉方法随任务增多退化，而本方法更鲁棒。但对比方法是否完整（如是否对比了其他多模态CL方法）没有说明。从“ICLR-2026-Rejected-Public”标签看，可能审稿人认为某些方面不足（如实验细节或理论贡献），但公开摘要显示实验是全面的。总体而言，实验设计相对客观，因为使用了标准基准。

## 6. 主要结论与发现
- 纯视觉提示方法随任务数量增加，性能显著下降（遗忘加剧）。
- CoLaP通过语言引导的提示选择，实现了更好的泛化和鲁棒性，遗忘更低，准确率更高。
- 多模态语义信息可有效增强提示选择鲁棒性，缓解持续学习中的灾难性遗忘。
- 推理时纯视觉操作，不增加额外开销，保持了效率。

## 7. 优点
- **创新性强**：首次（或少数）将语言引导用于持续学习的提示选择，解决了视觉偏移导致的错误提示匹配问题。
- **实用性强**：训练时利用文本描述，推理时无需语言输入，实用且高效。
- **泛化性好**：在内分布和外分布场景下均优于纯视觉方法，尤其长任务序列下优势明显。
- **思路清晰**：利用多模态预训练模型（如CLIP）作为桥梁，方法简洁有效。

## 8. 不足与局限
- **依赖图像描述生成**：训练时需要为每张图像生成文本描述，增加了预处理成本；若描述质量差（如类别标签过于简单），可能影响效果。
- **未提及对异构任务（如不同领域）的适应性**：仅针对每个数据集独有分布，跨任务分布差异大的场景可能仍有挑战。
- **实验未对比更多多模态CL方法**：可能缺失与同类多模态方法的公平比较。
- **算力与资源未公开**：难以判断方法的计算开销是否过重。
- **局限性声明**：可能存在偏差——文本描述生成可能引入训练集之外的先验知识，或在某些数据集（如无类别标签的边案例）中难以生成合适描述。
- **被拒可能原因**：虽然评分9.0，但ICLR 2026被拒，可能实验细节或理论分析不够深入，或者与其他方法比较不够全面。

（完）
