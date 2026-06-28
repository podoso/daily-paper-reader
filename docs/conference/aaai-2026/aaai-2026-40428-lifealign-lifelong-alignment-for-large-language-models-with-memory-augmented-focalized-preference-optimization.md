---
title: "LifeAlign: Lifelong Alignment for Large Language Models with Memory-Augmented Focalized Preference Optimization"
title_zh: LifeAlign：利用记忆增强聚焦偏好优化实现大语言模型终身对齐
authors: "Junsong Li, Jie Zhou, Bihao Zhan, Yutao Yang, Qianjun Pan, Shilian Chen, Tianyu Huai, Xin Li, Qin Chen, Liang He"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40428/44389"
tags: ["query:continual"]
score: 8.0
evidence: 基于记忆增强偏好优化的终身对齐
tldr: 针对LLM顺序对齐任务中遗忘已学偏好值的问题，提出LifeAlign框架，采用聚焦偏好优化策略和记忆机制保留旧知识，实现终身对齐而不遗忘。实验表明该方法在连续对齐场景下稳定保持一致性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 传统对齐方法在适应新领域或偏好时会灾难性遗忘之前学到的价值观。
method: 提出聚焦偏好优化策略，结合记忆模块存储旧偏好样本，在优化新偏好时约束旧知识不丢失。
result: 在多个连续对齐任务上，LifeAlign保持了对齐质量，有效克服了遗忘。
conclusion: 该工作为LLM的安全持续部署提供了可行方案，实用性强。
---

## Abstract
Alignment plays a crucial role in Large Language Models (LLMs) in aligning with human preferences on a specific task/domain. Traditional alignment methods suffer from catastrophic forgetting, where models lose previously learned values when adapting to new preferences or domains. We introduce LifeAlign, a novel framework for lifelong alignment that enables LLMs to maintain consistent human preference alignment across sequential learning tasks without forgetting previously learned values. Our approach consists of two key innovations. First, we propose a focalized preference optimization strategy that aligns LLMs with new preferences while preventing the erosion of alignment acquired from previous tasks. Second, we develop a short-to-long memory consolidation mechanism that merges denoised short-term preference representations into stable long-term memory using intrinsic dimensionality reduction, enabling efficient storage and retrieval of alignment patterns across diverse domains. We evaluate LifeAlign across multiple sequential alignment tasks spanning different domains and preference types. Experimental results demonstrate that our method achieves superior performance in maintaining both preference alignment quality and knowledge retention compared to existing lifelong learning approaches.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大型语言模型（LLM）在对齐人类偏好时，若按顺序学习多个不同领域或偏好任务，会产生**灾难性遗忘**——即学习新偏好的同时丢失之前学到的对齐知识。
- **研究背景**：现有对齐方法（如RLHF、DPO、Constitutional AI）通常只在单一静态任务上优化，无法适应偏好的持续演化；而传统的持续学习方法（如正则化、回放、参数隔离）大多针对监督学习设计，不适用于偏好优化的比较性学习信号和非平稳偏好分布。
- **整体含义**：本文提出**终身对齐（Lifelong Alignment）**范式，使LLM能够在不断变化的人类偏好和任务中持续学习、更新对齐知识，同时不遗忘先前学到的价值观，对可信AI的长期部署至关重要。

## 2. 方法论：核心思想、关键技术细节
### 核心思想
- 融合两种创新：**聚焦偏好优化（Focalized Preference Optimization, FPO）** 和 **短到长记忆巩固（Short-to-Long Memory Consolidation, SLMC）**，分别从损失函数层面和参数更新层面抵抗遗忘。

### 关键技术细节
- **FPO（聚焦偏好优化）**：
  - 基于DPO的隐式奖励 \( r = \beta [\log\frac{\pi_\theta(y_p|x)}{\pi_{\text{ref}}(y_p|x)} - \log\frac{\pi_\theta(y_d|x)}{\pi_{\text{ref}}(y_d|x)}] \)。
  - 定义损失函数：\( \mathcal{L}_{\text{FPO}} = -(1 - \sigma(r))^2 \log \sigma(r) \)。
  - 自适应门控：当样本已被模型熟练掌握（\( r > 0 \)）时，\( (1-\sigma(r))^2 \) 缩小，梯度被抑制；当样本新或不确定（\( r \leq 0 \)）时，门控接近1，全量更新。从而保护已学偏好、聚焦新知识。
  - 配合固定大小的回放缓冲区（replay buffer），每个任务结束后随机保留20%新数据并入缓冲区，与当前数据联合训练。

- **SLMC（短到长记忆巩固）**：
  - **去噪**：对每轮FPO后得到的LoRA参数更新矩阵 \( SM_t \) 进行SVD分解，保留能量占90%（\( \theta=0.9 \)）的奇异值及其对应分量，重构为去噪后的 \( SM'_t \)。
  - **冲突感知精炼**：将历史所有精炼更新向量 \( RSM_1,...,RSM_{t-1} \) 堆叠并对列进行SVD，得到知识子空间基 \( V_h \)。将 \( SM'_t \) 投影到该子空间，得到冲突分量 \( SM^p_t \)，其正交分量 \( SM^o_t \) 为安全新信息。最终 \( RSM_t = SM^o_t + \lambda SM^p_t \)，其中 \( \lambda \in [0,1] \) 控制对历史冲突的抑制程度（最优 \( \lambda=0.5 \)）。
  - **长期记忆整合**：将 \( RSM_t \) 重塑为矩阵，直接加到当前模型参数 \( LM_{t-1} \) 上，得到 \( LM_t \)，同时将 \( RSM_t \) 存入历史存储 \( H \) 用于下次冲突检测。

### 算法流程（文字说明）
1. 初始化模型参数 \( LM_0 \)，历史记忆集 \( H=\emptyset \)。
2. 对每个任务 \( t=1,...,N \)：
   - 使用当前缓冲区+新任务数据，通过FPO优化模型（LoRA方式更新），得到原始短时记忆 \( SM_t \)。
   - SLMC三阶段：SVD去噪 → 冲突投影与抑制 → 精炼整合。
   - 更新 \( LM_t \) 并存储 \( RSM_t \) 到 \( H \)。
   - 随机抽取新任务数据20%加入缓冲区。

## 3. 实验设计
### 数据集与场景
- 构建**六任务终身对齐基准**，覆盖四类对齐维度：
  1. **人类偏好对齐（HPA）**：HC3、hh-rlhf-helpful
  2. **指令忠诚对齐（IFA）**：Capybara-Preferences
  3. **价值对齐（VA）**：hh-rlhf-harmless、Safe-RLHF
  4. **客观事实对齐（OFA）**：TruthfulQA
- 默认任务顺序：Task1~6对应上述数据集（Capybara → HC3 → hh-rlhf-harmless → hh-rlhf-helpful → Safe-RLHF → TruthfulQA）。另设反向和随机顺序以评估鲁棒性。

### 评价指标
- **Last**：训练完所有任务后，每个任务的最终性能均值。
- **BWT（Backward Transfer）**：衡量旧任务性能相比刚学完时的变化（正越好）。
- **AP（Average Performance）**：渐进平均性能。
- 使用 **BLEU-4、ROUGE-L、LLM-Judge**（基于DeepSeek-Chat API）三种评分。

### 对比方法
- **基线**：SeqFT（顺序微调）、ER（经验回放）、GEM、EWC、O-LoRA、L2P、CPPO（已提出的持续对齐方法）。
- **上界**：单任务学习（STL）、多任务学习（MTL）。

## 4. 资源与算力
- 文中明确说明：在 **8块 A800-80GB GPU** 上训练。
- 使用 **LLaMA-Factory** 框架。
- 训练参数：SFT 3个epoch（学习率1e-4），DPO 3个epoch（学习率5e-6）。
- **未明确给出总训练时长**，但基于GPU数量和数据规模可推测为可接受范围。

## 5. 实验数量与充分性
- **主实验（表1）**：对比10种方法（含LifeAlign）在6个任务上的3个指标，展示整体性能。
- **消融实验（表2）**：4种配置（有无FPO、有无SLMC），验证各自贡献。
- **超参数敏感性（图3）**：对 \( \lambda \)（0~1）和 \( \theta \)（0~1）分别做单变量分析，确定最优值。
- **任务顺序鲁棒性（图4）**：正向、反向、随机三种顺序，对比ER和CPPO。
- **基础模型泛化性（表3）**：在Qwen-2.5-7B、Mistral-7B-v0.3、LLaMA-3.1-8B上验证。

**充分性评价**：实验设计较为全面，覆盖了核心消融、超参数、顺序、模型泛化等方面；对比方法包括最相关的前沿工作（CPPO等）；使用多种自动评价指标和LLM-Judge确保客观性。不足之处在于未在更大参数规模（如13B+）或更多样化任务（如多语言）上测试。

## 6. 主要结论与发现
- **LifeAlign在几乎所有指标上达到最优**，且平均性能（AP）接近多任务学习上界（MTL 38.00 vs LifeAlign 36.43）。
- **BWT为正值**（平均0.91），表明不仅不遗忘，甚至能提升旧任务性能；相比之下所有基线BWT均为负。
- **对超参数较鲁棒**：\( \lambda=0.5, \theta=0.9 \) 为最优，且性能曲线较平滑。
- **对任务顺序不敏感**：在三种顺序下均保持正或近零BWT，而基线顺序波动大。
- **跨模型迁移性好**：在Qwen、Mistral、LLaMA上均显著优于ER和CPPO。

## 7. 优点
- **方法创新性强**：将偏好优化损失设计为自适应聚焦，结合认知启发的记忆巩固，双管齐下解决遗忘。
- **实验设计严谨**：构建了首个覆盖多维度对齐的终身对齐基准，对比方法全面（含专门针对持续对齐的CPPO）。
- **结果显著**：在多项指标上大幅超越现有方法，BWT从负转正，具有实用价值。
- **鲁棒性验证充分**：包括超参数、任务顺序、不同基础模型，证明方法泛化能力。
- **符合实际部署需求**：面向偏好持续演化的真实场景，兼顾知识保留与新知识吸收。

## 8. 不足与局限
- **计算和存储开销**：SLMC需要存储历史精炼更新向量并进行SVD，对大模型或长序列任务可能带来额外内存和时间成本（文中未定量分析）。
- **依赖回放缓冲区**：当前设计在隐私敏感场景（如医疗、金融）下不适用，未来工作虽提及rehearsal-free变体，但尚未实现。
- **模型规模有限**：仅在7B/8B参数级别验证，未测试更大容量模型（如13B/70B），扩展性未知。
- **任务多样性限制**：仅6个英语数据集；未包括多语言、多模态或多轮对话等更复杂场景。
- **评价依赖LLM-Judge**：使用DeepSeek-Chat API可能引入第三方模型偏差，重复性受限。
- **未与最新方法（如CPPO之后的COPR等）全面对比**：论文仅对比了CPPO，而COPR也来自较新工作（Zhang et al. 2025），可能在实验完成时未纳入。

（完）
