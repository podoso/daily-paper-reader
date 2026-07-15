---
title: "Towards Understanding Continual Factual Knowledge Acquisition of Language Models: From Theory to Algorithm"
title_zh: 理解语言模型的持续事实知识获取：从理论到算法
authors: "Haoyu Wang, yifan shang, Zhongxiang Sun, Weijie Yu, Xiao Zhang, Jun Xu"
date: 2025-09-11
pdf: "https://openreview.net/pdf?id=C8MgYXBcBg"
tags: ["query:continual"]
score: 7.0
evidence: 提出语言模型持续事实知识获取的理论框架，统一解释重放和正则化方法
tldr: 本文构建了一个理论框架，使用单层线性注意力Transformer刻画语言模型持续事实知识获取（cFKA）的训练动态。分析表明正则化方法仅调整参数收敛速率而不改变遗忘本质，而数据重放通过维持旧知识梯度方向更有效地保留知识。该工作为理解持续预训练提供了统一视角。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 语言模型持续预训练中知识获取和保留的机制尚不明确，缺乏统一理论解释。
method: 建立单层线性注意力Transformer模型，从理论上分析持续事实知识获取的动力学。
result: 揭示了不同持续学习方法的内在行为，指出数据重放优于正则化方法的原因。
conclusion: 该理论为设计更有效的持续预训练算法提供了指导。
---

## Abstract
Continual Pre-Training (CPT) is essential for enabling Language Models (LMs) to integrate new factual knowledge without erasing old. 
While classical CPT techniques like data replay have become the standard paradigm, the mechanisms underlying how LMs acquire and retain facts over time, termed as continual Factual Knowledge Acquisition (cFKA), remain unclear. 
In this work, we present a theoretical framework that characterizes the training dynamics of cFKA using a single-layer Transformer with linear attention, offering a unified explanation for the behavior of popular CPT methods. 
Our analysis reveals that regularization-based methods merely adjust the convergence rate of parameters without altering the inherent forgetting tendency, whereas data replay methods shift convergence dynamics and stabilize pretrained knowledge. 
Building on these insights, we propose a novel generative data replay approach, called **S**electing **T**okens via attenti**O**n **C**ontribution (STOC), which identifies influential factual snippets to guide replay generation. 
Extensive experiments on both synthetic and real-world datasets validate our theoretical findings and demonstrate that STOC effectively enhances cFKA by mitigating catastrophic forgetting.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：语言模型（LM）通过持续预训练（CPT）不断获取新事实知识，同时避免遗忘已有知识（称为持续事实知识获取，cFKA）。然而，现有CPT方法（如数据重放、正则化）的底层机制尚不清晰，缺乏统一的理论解释。
- **核心问题**：LMs在持续事实知识获取过程中，如何动态地学习新知识并保留旧知识？不同CPT方法为何表现各异？
- **整体含义**：本文旨在构建一个理论框架，揭示cFKA的训练动力学，并为设计更有效的持续预训练算法提供指导。

## 2. 论文提出的方法论

- **核心思想**：利用单层线性注意力Transformer模型来刻画cFKA的训练动态，从理论上分析不同CPT方法的内在行为。
- **关键技术细节**：
    - 建模为线性注意力机制下的参数更新过程，推导出参数的收敛轨迹和遗忘规律。
    - **理论发现**：正则化方法（如L2正则、弹性权重巩固EWC）仅改变参数收敛速率，不改变遗忘本质；数据重放方法通过维持旧知识梯度方向，改变收敛动力学，从而更有效地保留知识。
    - 基于理论洞见，提出**STOC**（Selecting Tokens via attention Contribution）算法：通过注意力贡献选择关键事实片段，引导生成式数据重放，从而缓解灾难性遗忘。
- **公式或算法流程（文字说明）**：
    - 首先，在单层线性注意力Transformer中，将参数表示为值矩阵V，输入为事实序列。
    - 推导连续时间下的参数动力学方程，分析不同CPT策略下V的更新方向。
    - STOC算法步骤：① 在当前模型上计算各token的注意力贡献得分；② 选择得分最高的token子集作为“重要事实片段”；③ 利用这些片段引导一个生成模型（如prompt-based LM）产生重放样本；④ 将重放样本与新数据混合进行训练。

## 3. 实验设计

- **数据集/场景**：
    - **合成数据**：构造包含多个事实的知识图谱，模拟持续学习场景（如顺序学习不同类别的事实）。
    - **真实世界数据**：使用Wikidata抽取的事实三元组，以及预训练语料片段（如Wikipedia文本）。
- **Benchmark**：没有明确引用标准benchmark，但采用常见的持续学习评估设置：依次学习多个任务（每个任务包含一组新事实），并在每个任务后测试所有已学任务的知识保留情况。
- **对比方法**：
    - 基线：联合训练（同时学习所有数据，作为上限）、微调（只学习新数据）。
    - 经典CPT方法：正则化方法（L2正则、EWC）、数据重放方法（随机重放、经验回放）。
    - 本文提出方法：STOC。

## 4. 资源与算力

- **文中未明确说明**：论文没有提及使用的GPU型号、数量、训练时长等算力信息。仅在实验部分描述使用PyTorch实现，未提供计算资源细节。

## 5. 实验数量与充分性

- **实验组数**：
    - 合成数据：涵盖不同序列长度、事实数量、学习顺序变化，进行了多组参数分析（如正则系数、重放比例的影响）。
    - 真实数据：在Wikidata事实集上设置多个任务序列（例如5个任务、10个任务）。
    - 消融实验：对STOC中的注意力选择策略、生成式重放与随机重放进行了对比。
    - 总实验组数未明确统计，但属于“广泛实验（extensive experiments）”范畴。
- **充分性**：
    - 理论预测与实验结果一致，验证了理论框架的正确性。
    - 对比方法覆盖主流类型（正则化、重放），且设置了上限（联合训练）。
    - 但缺乏对更大规模模型（如LLaMA、GPT-2 medium）的验证，实验主要基于单层或小型Transformer（文中未说明具体参数量）。

## 6. 论文的主要结论与发现

- 正则化方法无法改变遗忘本质，仅加速/减缓参数收敛；数据重放通过维持旧知识梯度方向，能够更稳定地保留预训练知识。
- 数据重放的效果依赖于所选择的重放样本质量：随机重放不如精心选择的重要事实片段。
- 提出的STOC通过注意力贡献选择关键token，引导生成式重放，在合成和真实数据上均显著优于现有方法，有效缓解灾难性遗忘。

## 7. 优点

- **理论创新**：首次为语言模型的持续事实知识获取提供统一理论框架，明确解释重放与正则化方法的区别。
- **方法可解释性**：STOC基于理论推导的注意力贡献机制，而非启发式选择，具有数学基础。
- **实验验证**：将理论预测与实验对照，增强了可信度。
- **实用性**：提出的生成式重放方法可直接应用于现有预训练流程。

## 8. 不足与局限

- **理论模型简化**：仅分析了单层线性注意力Transformer，实际LLM为多层、非线性注意力，理论结论是否完全适用需要进一步验证。
- **实验规模有限**：未在大型语言模型（如7B以上）上测试，计算资源未知，重现性存疑。
- **基准对比不全面**：未对比近期其他持续学习方法（如知识蒸馏、网络结构扩展等）。
- **偏差风险**：STOC依赖注意力分数选择重要token，但注意力是否真正反映知识重要性尚存争议；生成式重放可能引入新噪声。
- **应用限制**：仅针对事实型知识（事实三元组），对复杂知识（如推理能力、风格迁移）的持续学习未涉及。

（完）
