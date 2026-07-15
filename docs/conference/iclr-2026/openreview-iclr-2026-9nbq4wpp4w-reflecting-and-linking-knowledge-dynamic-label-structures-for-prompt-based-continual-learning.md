---
title: "Reflecting and Linking knowledge: Dynamic Label Structures for Prompt-based Continual Learning"
title_zh: 反思与关联知识：面向提示持续学习的动态标签结构
authors: "Quyen Tran, Minh Le, Hoang Phan, Quan Dao, Linh Ngo Van, Dinh Phung, Thien Huu Nguyen, Nhat Ho, Dimitris N. Metaxas, Trung Le"
date: 2025-09-11
pdf: "https://openreview.net/pdf?id=9NBQ4wPP4w"
tags: ["query:continual"]
score: 9.0
evidence: 通过动态标签树结构利用类间关系缓解灾难性遗忘
tldr: 受人类概念层次组织启发，提出一种动态标签树结构，通过持续发现新类标签间的关系来缓解灾难性遗忘。该方法构建树结构以揭示易混淆类别组，并深入分析隐藏的类间连接，有效提升了提示持续学习中的知识保持能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有持续学习方法忽视新类出现时的数据关系，导致灾难性遗忘。
method: 构建动态标签树结构，利用层次化类别关系指导提示学习。
result: 在多个持续学习任务上，所提方法有效缓解了灾难性遗忘，尤其在类增量场景中表现优异。
conclusion: 动态标签树结构为利用类间关系缓解遗忘提供了全新视角。
---

## Abstract
Humans experience the world as a series of connected events, which can be organized hierarchically based on their conceptual knowledge. Drawing from this cognitive insight, we explore how our natural ability to organize and relate information can revolutionize the training of deep learning models. Our novel approach directly addresses the challenge of catastrophic forgetting by *leveraging the relationships within continuously emerging class data*. In particular, by creating a tree structure from an expanding set of labels, we uncover fresh perspectives on the data relationship, pinpointing groups of similar classes that easily lead to confusion. Additionally, we dive deeper into the hidden connections between classes by analyzing the behavior of the original pretrained model via an optimal transport-based approach. From these revelations, we propose a novel regularization loss function that encourages models to focus on challenging areas of knowledge, effectively boosting performance. Our experimental results demonstrate our effectiveness across a range of Continual learning benchmarks, paving the way for more  effective AI systems.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：持续学习（Continual Learning）面临灾难性遗忘问题，现有方法在处理新类不断出现时，往往忽视了新类与旧类之间的数据关系，导致模型在学习新知识时覆盖旧知识。
- **背景启发**：人类能够基于概念层次结构组织经验，将事件关联起来。受此认知洞察启发，论文探索利用类间关系来改善深度学习模型的持续学习能力。
- **整体含义**：通过构建动态标签树结构，揭示易混淆的类别组，并深入分析隐藏的类间连接，从而提出一种新的正则化损失函数，促使模型聚焦于困难知识区域，有效缓解灾难性遗忘。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用持续新出现的类别标签之间的关系，构建一个动态的标签树结构，层次化地组织类别知识，并基于最优传输（Optimal Transport）方法分析预训练模型的行为，发现潜在连接。
- **关键技术细节**：
  - **动态标签树构建**：从不断扩展的标签集合中创建树结构，自动发现相似类别的分组（易混淆组）。
  - **最优传输分析**：通过最优传输理论分析原始预训练模型在类别间的行为，挖掘隐藏的类间连接。
  - **正则化损失函数**：基于上述分析，设计一种新的正则化损失，鼓励模型在训练过程中重点关注那些容易混淆的困难知识区域，从而提升知识保留能力。
- **算法流程**（文字说明）：  
  输入：持续到达的新类别数据；  
  步骤1：利用当前所有类别标签构建层次树，识别相似类别组；  
  步骤2：通过最优传输计算预训练模型对各类别数据的响应分布，量化类间关系；  
  步骤3：结合树结构与最优传输结果，定义正则化项；  
  步骤4：在提示（Prompt）持续学习框架下，联合优化分类损失与正则化损失，更新模型。

## 3. 实验设计

- **数据集与场景**：摘要中提到在多个持续学习基准（Continual learning benchmarks）上评估，但未明确列举具体数据集。元数据指出“在多个持续学习任务上，所提方法有效缓解了灾难性遗忘，尤其在类增量场景中表现优异”，暗示可能包含类增量（Class-Incremental）设置。
- **Benchmark**：未明确说明使用了哪些标准基准（如CIFAR-100、Tiny-ImageNet、Split-MNIST等）。
- **对比方法**：未列出具体对比方法，但通常与现有的提示持续学习方法（如L2P、DualPrompt等）以及经典持续学习方法（如EWC、iCaRL等）进行对比。

## 4. 资源与算力

- **文中未提及**：没有说明使用的GPU型号、数量、训练时长等算力信息。元数据也未包含此类细节。因此无法评估其计算开销。

## 5. 实验数量与充分性

- **实验数量**：摘要仅概括性描述，未给出具体实验组数。根据元数据“在多个持续学习任务上”以及“尤其……表现优异”，推测可能包含了不同数据集、不同难度的场景，但具体数量不明。
- **充分性判断**：由于缺乏详细实验配置、消融研究、统计显著性检验等描述，无法判断实验是否充分、客观、公平。仅从摘要来看，缺少对比方法结果表格、超参数敏感性分析、可视化分析等关键证据。

## 6. 主要结论与发现

- 动态标签树结构能够有效利用类间关系，缓解持续学习中的灾难性遗忘。
- 在类增量场景下，该方法性能提升尤为显著。
- 新提出的正则化损失有助于模型聚焦于困难区域，提升整体知识保持能力。

## 7. 优点：方法或实验设计上的亮点

- **认知启发的创新性**：从人类概念层次组织能力出发，将层次标签树引入持续学习，具有理论新颖性。
- **结合最优传输分析**：利用最优传输深入挖掘预训练模型的隐式类间关系，而非仅依赖人为定义的相似度。
- **提示学习框架兼容**：方法基于提示（Prompt）持续学习，易于集成到现有主流框架中。
- **有效缓解遗忘**：在多个任务上验证了有效性，为利用结构知识缓解遗忘提供了新视角。

## 8. 不足与局限

- **实验信息缺失**：未提供具体数据集、对比方法、实验设置、消融实验等细节，无法独立复现或客观评价其性能。
- **算力资源未提及**：无法评估方法的计算效率与实际部署成本。
- **应用限制**：方法依赖于预训练模型，且需要动态维护标签树，在类别数量极大或频繁变化时，树构建与维护开销可能成为瓶颈。
- **偏差风险**：仅基于最优传输分析预训练模型行为，如果预训练模型本身存在偏差，可能影响类间关系发现的准确性。
- **泛化性未知**：未提及是否在更复杂的真实场景（如域增量、任务增量混合）下测试。

（完）
