---
title: "Fourier Minds, Forget Less: Discrete Fourier Transform for Fast and Robust Continual Learning in LLMs"
title_zh: 傅里叶心智，遗忘更少：面向LLM快速鲁棒持续学习的离散傅里叶变换
authors: "Haokun Lin, Shujun Xia, Haobo Xu, Teng Wang, Jingyi Su, Yinan Zhou, Kaijie Zhu, Yichen Wu, Renzhen Wang, Ying Shan, Zhenan Sun"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=cQ8VPIMbfN"
tags: ["query:llm"]
score: 7.0
evidence: 利用稀疏傅里叶变换实现LLM的高效持续学习，减少遗忘
tldr: 本文针对LLM持续学习中灾难性遗忘和参数预算累积的问题，探索稀疏傅里叶变换（SFT）的应用。初步实验发现直接使用SFT会导致时间不稳定和遗忘，进而提出改进方案，在保持参数高效的同时有效缓解遗忘。该工作为LLM持续学习提供了新的频域视角。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LoRA方法在持续学习中累积参数预算，且存在遗忘问题，需要更高效的方法。
method: 研究稀疏傅里叶变换在持续学习中的潜力，并针对其不稳定性提出改进。
result: 改进后的SFT方法在LLM序列任务上实现更快、更鲁棒的持续学习，减少参数开销。
conclusion: 频域方法为LLM持续学习提供了一条有前景的路径。
---

## Abstract
Continual learning (CL) for large language models (LLMs) is challenged by both catastrophic forgetting and efficiency constraints when facing long sequential tasks. While low-rank adaptation in LoRA-based approaches reduces per-task trainable parameters, the cumulative parameter budget grows with stream length and can be substantial. This limits their applicability in lifelong learning scenarios, especially under strict resource constraints. In this work, we explore the potential of the parameter-efficient Sparse Fourier Transform (SFT) in the context of continual learning. Our preliminary experiments reveal that directly applying SFT in CL settings leads to temporal instability and forgetting.  Motivated by this finding, we propose Discrete Fourier Continual Learning (DF-CL), which leverages a spectral decomposition strategy to disentangle shared and task-specific knowledge components, facilitating more stable continual learning. By leveraging the orthogonality properties inherent to the SFT bases, DF-CL ensures that task-specific knowledge is encoded within its own dedicated parameter space, minimizing interference between tasks. Furthermore, we introduce a max-magnitude task-weight merging strategy, which enables efficient knowledge consolidation and transfer across sequential tasks. Extensive experiments on both T5-Large and LLaMA2-7B demonstrate the scalability, efficiency, and effectiveness of DF-CL.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLM）在持续学习（Continual Learning, CL）场景下面临两大挑战：灾难性遗忘（catastrophic forgetting）和参数效率问题。现有基于LoRA的方法虽然通过低秩适配减少了每任务的训练参数，但随着任务序列增长，累积的参数预算会显著增加，限制了其在资源严格受限的终身学习场景中的适用性。
- **研究动机**：探索一种参数更高效且能缓解遗忘的持续学习方法。作者注意到稀疏傅里叶变换（Sparse Fourier Transform, SFT）在参数效率上的潜力，但直接将其应用于持续学习会导致时间不稳定和遗忘问题。因此，需要改进SFT以适应持续学习的稳定性和知识保留需求。
- **整体含义**：本文提出从频域视角解决LLM持续学习瓶颈，通过离散傅里叶变换（DFT）实现任务特定知识与共享知识的解耦，在保持参数高效的同时减少遗忘，为LLM持续学习开辟了新路径。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：利用稀疏傅里叶变换（SFT）的正交性，将任务特定知识与共享知识分别编码到独立的参数空间中，以减少任务间干扰，并通过最大幅值任务权重合并策略实现高效知识整合与迁移。
- **关键技术细节**：
  - **Discrete Fourier Continual Learning (DF-CL)**：基于离散傅里叶变换的持续学习框架。
  - **谱分解策略**（spectral decomposition）：将知识分解为共享组件和任务特定组件，利用SFT基函数的正交性，确保任务特定知识被编码到专属参数空间，从而最小化任务间干扰。
  - **最大幅值任务权重合并策略**（max-magnitude task-weight merging）：在序列任务处理过程中，通过选择每个频率分量上幅值最大的权重进行合并，实现高效的知识巩固与跨任务迁移（无需参数预算随任务数线性增长）。
- **算法流程（文字说明）**：在持续学习过程中，每个新任务到来时，模型在频域中调整参数：首先通过SFT将当前任务的参数更新映射到频域，利用正交基将其与已有任务的知识空间分离；然后通过最大幅值策略选择保留最重要的频率成分，合并到全局模型参数中，从而实现参数共享与遗忘缓解。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **模型与规模**：在T5-Large和LLaMA2-7B两种不同规模的LLM上进行实验。
- **场景与benchmark**：文中未明确提及具体数据集名称，但提到“long sequential tasks”和“序列任务”，暗示在持续学习标准benchmark（如CIFAR-100、Mini-ImageNet等图像分类任务或文本分类/生成序列任务）上评估。具体数据集需查阅全文，摘要未列出。
- **对比方法**：摘要中明确提到与“LoRA-based approaches”对比（如LoRA的低秩适配方法），未列出其他基线。推测还对比了其他持续学习方法（如EWC、MAS、HAT等常用方法），但摘要未提及。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点。

- **资源说明**：摘要和元数据中均未提及具体GPU型号、数量或训练时长。仅知道在T5-Large和LLaMA2-7B上进行实验，但未给出算力细节。需指出文中未明确说明。

### 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平。

- **实验数量**：基于摘要，至少包含两组规模不同的模型实验（T5-Large和LLaMA2-7B），且提到“extensive experiments”。推测包含：
  - 主要对比实验（任务序列长度、遗忘率、参数效率等）。
  - 消融研究（可能分析了谱分解策略、最大幅值合并策略等的影响）。
- **充分性评估**：两模型规模跨度的实验（大到7B）增强了结论的泛化性。但未提及数据集多样性（如是否覆盖文本分类、问答、生成等），也未展示与其他频域方法的对比。整体实验尚可，但信息不足难以完全判断公平性（如是否采用相同超参数、随机种子等）。

### 6. 论文的主要结论与发现

- **主要结论**：
  - 直接使用SFT进行持续学习会导致时间不稳定和遗忘；而提出的DF-CL通过谱分解和正交性实现了更稳定的持续学习。
  - DF-CL在保持参数高效（参数预算不随任务数线性增长）的同时，有效缓解了灾难性遗忘。
  - 在T5-Large和LLaMA2-7B上的实验证明了DF-CL的可扩展性、效率以及有效性（更快、更鲁棒）。

### 7. 优点：方法或实验设计上有哪些亮点

- **方法亮点**：
  - 创新性地将频域方法（稀疏傅里叶变换）引入LLM持续学习，提供了新视角。
  - 利用SFT基函数的正交性质，天然支持任务特定参数的隔离，减轻干扰。
  - 最大幅值任务权重合并策略实现了参数高效的知识整合，避免参数预算爆炸。
- **实验亮点**：
  - 在两个不同规模模型（大至7B）上验证可扩展性，表明方法对大模型仍有效。
  - 对比了流行的LoRA方法，突出参数效率优势。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **不足与局限**：
  - 摘要中未报告具体数据集和任务类型，实验覆盖范围不透明，可能存在数据集偏置。
  - 仅与LoRA方法对比，缺乏与其他持续学习基线（如EWC、MAS、Progressive Neural Networks等）的系统对比，结论的普适性存疑。
  - 未讨论傅里叶变换的计算开销（虽参数高效，但变换本身的计算成本可能较高，尤其对大模型）。
  - 最大幅值合并策略可能造成信息损失（丢弃幅值较小的频率分量），未分析其负面影响。
  - 未提及在长序列任务（如数十个任务）下的表现，参数预算的实际缩减程度未被量化。
  - 未讨论该方法在非连续任务（如任务顺序变化）或类别不平衡场景下的稳定性。

（完）
