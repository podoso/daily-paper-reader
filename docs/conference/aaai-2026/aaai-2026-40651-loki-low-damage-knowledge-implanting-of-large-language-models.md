---
title: "LoKI: Low-Damage Knowledge Implanting of Large Language Models"
title_zh: LoKI：大语言模型的低损伤知识植入
authors: "Runyu Wang, Peng Ping, Zhengyu Guo, Xiaoye Zhang, Quan Shi, Liting Zhou, Tianbo Ji"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40651/44612"
tags: ["query:continual"]
score: 9.0
evidence: 灾难性遗忘微调大模型低损伤知识植入
tldr: 针对微调大模型时灾难性遗忘导致预训练知识丢失的问题，提出LoKI方法，利用Transformer中知识存储的机制理解，实现参数高效微调，在保持任务性能的同时显著保留通用能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 微调大模型时容易丢失预训练知识，即灾难性遗忘。
method: 基于Transformer知识存储机制，设计低损伤知识植入参数高效微调方法。
result: 与现有方法相比，在保留通用能力和任务性能之间取得更好平衡。
conclusion: 为微调大模型时防止灾难性遗忘提供了有效方案。
---

## Abstract
Fine-tuning adapts pretrained models for specific tasks but poses the risk of catastrophic forgetting (CF), where critical knowledge from pretraining is overwritten. To address the issue of CF in a general-purpose framework, we propose Low-damage Knowledge Implanting (LoKI), a parameter-efficient fine-tuning (PEFT) technique that utilizes recent mechanistic understanding of how knowledge is stored in transformer architectures. We compare LoKI against state-of-the-art PEFT methods in two real-world fine-tuning scenarios. The results show that LoKI demonstrates significantly better preservation of general capabilities. At the same time, its task-specific performance is comparable to or even surpasses that of full parameter fine-tuning and these PEFT methods across various model architectures. Our work bridges the mechanistic insights of LLMs' knowledge storage with practical fine-tuning objectives, enabling an effective balance between task-specific adaptation and the retention of general-purpose capabilities.

---

## 论文详细总结（自动生成）

# LoKI: 低损伤知识植入——大语言模型的参数高效微调方法

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）在预训练中积累了广泛的世界知识，微调这些模型以适应下游任务时，常发生「灾难性遗忘」（Catastrophic Forgetting, CF），即预训练的关键知识被覆盖。
- **问题**：现有PEFT方法（如LoRA、DoRA、PiSSA等）虽减少参数量，但大多未考虑模型内部知识存储的结构，更新参数时缺乏选择性，导致通用能力退化。
- **目标**：提出一种既能高效微调、又能最大限度保留预训练通用能力的框架，实现任务适配与知识保护的最佳平衡。

## 2. 方法论：LoKI 框架

LoKI由三个阶段组成：**分析（Analyzing）→ 选择（Selecting）→ 植入（Implanting）**。

### 2.1 核心思想
利用Transformer中知识存储在FFN（前馈网络）的**down-projection矩阵（W_down）** 中的机制，识别出对通用任务贡献最低的“知识向量”，只更新这些低贡献向量以植入新知识，从而对原有知识造成最小扰动。

### 2.2 关键技术细节

#### (1) 分析阶段：知识向量归因（KVA）
- 基于**积分梯度（Integrated Gradients, IG）** 方法，计算每个知识向量（即W_down的每一行）对模型最终输出的贡献。
- 定义单个向量j的归因值：  
  \[
  \text{Attr}_{l,j}(x) \approx \frac{1}{m} \sum_{k=1}^{m} \frac{\partial L(\frac{k}{m} z_{l,j})}{\partial z_{l,j}}
  \]
  其中 \(z_{l,j}\) 为第l层第j个FFN中间节点的预激活值，m为Riemann近似步数（固定为7）。
- 对MMLU数据集（57个学科）的每个样本计算归因值，统计出每个向量在全体数据上的高频低贡献频率。

#### (2) 选择阶段：层平衡策略（Layer-Balanced Strategy）
- 发现：模型内高贡献与低贡献知识向量均**集中在相似的层**（即分布不均匀）。
- 策略：为每一层分配相等的可训练参数配额（\(k_l = T/L\)），确保更新不影响知识的层次结构。
- 流程：
  1. 设定可训练比例q%（总可训练槽位T = q% × L × D）。
  2. 每层按KVA值选择**最低贡献**的k_l个向量（每层独立）。
  3. 跨样本聚合出现频率，最终每层取频率最高的k_l个向量作为可训练集S。

#### (3) 植入阶段：参数高效微调
- 冻结所有其他参数，仅更新选中的低贡献子集W_S（即W_down的部分行）。
- 可进一步结合LoRA：将W_S参数化为 \(W_S = W_S^{(0)} + A B\)，进一步减少参数量（LoKI*）。

## 3. 实验设计

### 3.1 任务与数据集

| 任务 | 数据集 | 用途 |
|------|--------|------|
| 函数调用 | ToolACE Function-Calling数据集（26,507个API） | 增强LLM的函数调用能力 |
| 检索重排序 | LB Reranker数据集（228万问答对，1-7分相关性标注） | 训练多语言检索模型 |

### 3.2 评估基准
- **灾难性遗忘测量**：在6个通用基准上评测：TriviaQA（知识）、GSM8K（数学）、HellaSwag（常识）、WinoGrande（常识）、HumanEval（代码）、IFEval（指令遵循）。定义平均遗忘率 Avg = 100/N × Σ((S_o - S_t)/S_o)。
- **任务性能**：函数调用任务使用Berkeley Function Calling Leaderboard V3（BFCL）；检索任务使用BEIR基准（MAP@1, Recall@1, NDCG@1, P@1）。

### 3.3 对比方法
- 全参数微调（Full FT）
- LoRA
- DoRA
- PiSSA
- CorDA（仅检索任务）

### 3.4 模型规模
- Llama3.1-8B-Instruct（函数调用任务）
- Qwen2.5-0.5B-Instruct（检索任务）

## 4. 资源与算力

- **显式说明**：论文提到KVA分析阶段在单张RTX4090 GPU上运行，对Llama3.1-8B-Instruct每个样本平均耗时9.69秒。
- **分析数据**：使用MMLU完整数据集或采样版本（采样后与全量选择结果重叠率97.57%）。
- **训练资源**：未详细说明微调阶段的GPU数量与时长，仅指出分析阶段的计算是一次性的（per model）。

## 5. 实验数量与充分性

### 实验组数概览
- **主要实验**：两个不同任务（函数调用、检索）× 多种q值（10/20/30；检索还包含q=5）→ 约6组对比实验。
- **消融实验**：
  - 验证KVA有效性：抑制高贡献 vs 低贡献向量（S-H vs S-L），结果差异显著（Avg: 36.73% vs 11.35%）。
  - 验证层平衡策略：全局高贡献（G-H） vs 全局低贡献（G-L） vs LoKI，结果LoKI远优于两者（Avg: 8.86% vs 39.04%/30.48%）。
- **组合实验**：LoKI+LoRA（LoKI*）在函数调用任务上测试。
- **超参数研究**：讨论了学习率与q值的相互作用（检索任务）。

### 充分性评价
- **客观公平**：使用相同基座模型、相同评估工具（OpenCompass、BFCL官方测试集），对比方法采用官方或标准实现。
- **局限**：仅测试了两个模型（Llama3.1-8B和Qwen2.5-0.5B），且仅做两类下游任务（函数调用和检索），覆盖广度有限；未在更大规模模型（如70B）或更多任务（如文本分类、对话）上验证。

## 6. 主要结论与发现

- LoKI在所有配置下**显著降低灾难性遗忘**（平均遗忘率最低0.34%~1.23%，远低于DoRA的4.92%和PiSSA的48.93%）。
- 在任务性能上，LoKI（q=30）在BFCL上达到最高总体准确率（58.93%），接近或超越全参数微调。
- 检索任务中，LoKI甚至以更少的遗忘取得了**正面增益**（q=30时MAP@1提升+1.0%）。
- 验证了**知识向量分布不均匀**（高、低贡献向量均密集于相似层），以及**层平衡策略**的重要性。
- LoKI可无缝集成LoRA，进一步降低参数量（97%减少）而不显著损害抗遗忘能力。

## 7. 优点与亮点

- **方法创新**：首次将机制可解释性（知识定位与归因）与PEFT系统结合，实现针对性的低损伤更新。
- **工程实用**：KVA仅需一次预计算（per model），可离线完成；选择策略简单有效。
- **灵活性**：支持参数比例控制，并可与LoRA等低秩方法协同，适用于不同算力场景。
- **实证充分**：通过两种不同的抑制实验和层平衡消融，充分验证了KVA和层平衡策略的必要性。

## 8. 不足与局限

- **模型规模有限**：仅测试了8B和0.5B两个模型，未在更大模型（如70B）或更小模型（如1B以下）上验证，泛化性待确认。
- **任务覆盖窄**：仅涉及函数调用和检索两类任务，未覆盖文本分类、生成、对话等常见微调场景。
- **计算开销**：KVA需要运行前向-反向传播并计算积分梯度，对MMLU全量数据（57学科）仍需一定计算成本（虽然一次完成）。
- **可解释性不足**：KVA基于积分梯度，其归因结果受到基线选择和积分步数影响，论文未对m=7的选择进行充分敏感性分析。
- **与LoRA结合的优化**：LoKI*（LoKI+LoRA）在参数量减少时任务性能略有下降（BFCL整体准确率56.76→57.16），可能需更细的超参数调优。
- **学习率依赖**：在检索任务实验中，发现不同q值需配合不同学习率，增加调参成本。

（完）
