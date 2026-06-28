---
title: Lifelong Language-Conditioned Robotic Manipulation Learning
title_zh: 终身语言条件机器人操作学习
authors: "Xudong Wang, Zebin Han, Zhiyu Liu, Gan Li, Jiahua Dong, Baichen Liu, Lianqing Liu, Zhi Han"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38930/42892"
tags: ["query:continual"]
score: 6.0
evidence: 机器人操作中的终身学习缓解遗忘
tldr: 针对语言引导机器人操作中连续学习新技能导致旧技能遗忘的问题，提出SkillsCrafter框架，通过操作技能适配保留旧知识，并利用奇异值分解从指令中提取共享语义子空间，减少遗忘。实验表明该方法能有效保持旧技能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 传统语言条件操作代理在适应新技能时会灾难性遗忘旧技能，限制实际部署。
method: 提出SkillsCrafter，包括操作技能适配保留旧知识，以及奇异值分解提取技能语义子空间。
result: 在连续学习场景中，SkillsCrafter显著减少遗忘，保持旧技能性能。
conclusion: 该框架为机器人终身学习提供了一种有效路径，可推广至其他多任务连续学习场景。
---

## Abstract
Traditional language-conditioned manipulation agent adaptation to new manipulation skills leads to catastrophic forgetting of old skills, limiting dynamic scene practical deployment. In this paper, we propose SkillsCrafter, a novel robotic manipulation framework designed to continually learn multiple skills while reducing catastrophic forgetting of old skills. Specifically, we propose a Manipulation Skills Adaptation to retain the old skills knowledge while inheriting the shared knowledge between new and old skills to facilitate learning of new skills. Meanwhile, we perform the singular value decomposition on the diverse skill instructions to obtain common skill semantic subspace projection matrices, thereby recording the essential semantic space of skills. To achieve forget-less and generalization manipulation, we propose a Skills Specialization Aggregation to compute inter-skills similarity in skill semantic subspaces, achieving aggregation of the previously learned skill knowledge for any new or unknown skill. Extensive simulator and real-world experiments demonstrate the effectiveness and superiority of our SkillsCrafter.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：语言条件机器人操作（LCRM）在仿真和真实环境中取得了显著进展，但现有方法在连续学习多个新技能时，会灾难性地遗忘先前学到的旧技能。这种“灾难性遗忘”严重限制了机器人在动态场景中的实际部署。
- **核心问题**：如何在不断学习新操作技能的同时，保持对旧技能的掌握，并能够利用旧知识促进新技能的学习，甚至在开放世界中泛化到未知技能？
- **整体含义**：本文提出了终身语言条件机器人操作（LLCRM）这一新任务，旨在让机器人代理能够终身持续地积累、复用和精炼操作技能，实现“遗忘少、泛化强”的操作能力。

## 2. 方法论：核心思想、关键技术细节
### 2.1 核心思想
- **两大挑战**：
  1. 如何探索和利用不同操作技能之间的共享知识与特有知识？
  2. 如何自适应、灵活地聚合已学知识以应对新技能或未知技能？
- **整体框架**：SkillsCrafter，包含三个模块：操作技能适配（MSkA）、技能专门化聚合（SkSA）、技能指定推理（SkSI）。

### 2.2 关键技术细节
- **操作技能适配（MSkA）**：
  - 基于LoRA微调预训练LLARVA模型，将低秩权重拆分为共享知识矩阵 **A** 和特有知识矩阵 **B**（基于观察3：A倾向于学习共享知识，B倾向于学习特有知识）。
  - **共享知识继承**：对新技能，利用SkSA模块计算当前技能与所有已学技能的语义子空间相似度，得到聚合权重，对历史所有A矩阵进行加权和作为新A的初始化。
  - **特有知识正交约束**：在新技能学习时，令当前B矩阵与所有历史B矩阵正交，以减少干扰，并通过L2归一化防止退化为零矩阵。
  - **动态稀疏LoRA注入**：使用Gumbel-Softmax门控机制自适应地决定在每一层是否注入LoRA，避免固定层数的过拟合或欠拟合，并加入稀疏正则化。
- **技能专门化聚合（SkSA）**：
  - 对每个技能收集多条指令，用CLIP文本编码器提取嵌入，然后进行奇异值分解（SVD）获得技能语义子空间投影矩阵 \(\psi_t\)。
  - 对于任意新指令 \(I_q\)，将其投影到每个已存子空间，计算余弦相似度，经指数变换得到权重 \(\Omega_q\)，从而加权聚合所有已有的LoRA适配器，得到当前技能专用的聚合适配器 \(\Delta \tilde{W}_q\)。
- **技能指定推理（SkSI）**：加载聚合后的适配器，使代理能利用历史知识完成当前技能操作。

### 2.3 公式或算法流程（文字说明）
1. 对每个已学技能 \(S_t\)，存储其语义子空间投影矩阵 \(\psi_t\) 和LoRA适配器 \(\{\Delta W^l_t\}\)。
2. 遇到新技能 \(S_q\)，用CLIP编码器得到指令嵌入 \(E_T(I_q)\)，逐一计算与 \(\psi_t\) 的投影余弦相似度。
3. 将相似度通过指数变换归一化得到聚合权重 \(\Omega_q\)。
4. 用 \(\Omega_q\) 对历史所有LoRA适配器进行加权求和，得到聚合后的 \(\Delta \tilde{W}_q\)。
5. 将聚合适配器加载到基础模型，进行前向推理或继续微调（微调时固定其他参数，仅更新当前LoRA，并施加正交约束和稀疏门控）。

## 3. 实验设计：数据集/场景、Benchmark、对比方法
### 3.1 数据集/场景
- **模拟环境**：基于RLBench，构建12种常见机器人操作技能（如开抽屉、推滑块、放钱、扫垃圾、按按钮、转水龙头等）。
- **真实环境**：基于UR-5机械臂和RGB相机，构建6种真实操作技能（如抓瓶子、按按钮、叠块、取肉等）。
- **整体任务设置**：共18项技能，前16项用于训练和测试（连续学习），后2项从未训练，用于开放世界泛化测试。
- **评价指标**：平均成功率（ASR）和遗忘率（FR）。

### 3.2 Benchmark
- 本文首次提出LLCRM任务，并为此构建了包含模拟和真实环境的终身学习基准。

### 3.3 对比方法
- **Seq-FT**：顺序全参数微调
- **LwF-LoRA**：基于知识蒸馏
- **EWC-LoRA**：弹性权重巩固
- **Dense MoLE**、**Sparse MoLE**、**MoLA**、**HydraLoRA**、**BranchLoRA**（均为基于MoE或LoRA的持续学习方法）
- **O-LoRA + SkSA**、**SD-LoRA + SkSA**（本文消融对照）

## 4. 资源与算力
- **文中明确提及**：使用PyTorch 2.1.2 + cu121，在 **八张NVIDIA RTX 6000 Ada Generation GPU** 上进行训练和测试。
- **未说明训练时长**：未提及具体每个技能的微调步数或总训练时间；仅提到学习率1e-4，Adam优化器。

## 5. 实验数量与充分性
- **主要结果**：表1（ASR）和表2（FR）展示了18个技能的详细结果，对比了8种现有方法，并给出了平均值。
- **消融实验**：
  - 表3：对“Gumbel门控（GGM）”“共享知识继承（INA）”“正交项（SOT）”分别移除进行消融，验证各组件贡献。
  - 表4：对四种知识聚合方式（指令匹配IM、视觉匹配VM、平均池化Avg、最相似选取TOP）进行对比，验证SkSA的有效性。
- **实验充分性评价**：实验覆盖了模拟和真实环境，包含多种技能类型，对比了足够多的现有SOTA方法，消融实验设计合理。但由于是持续学习任务，没有使用标准公开数据集（如CL-ImageNet等），而是自建基准，可能影响跨领域泛化性评价。整体来说实验较为充分，结果客观。

## 6. 论文的主要结论与发现
- SkillsCrafter在LLCRM任务上取得了 **最佳平均成功率（ASR 52.0%）**，比次优方法SD-LoRA+SkSA高2.0个百分点。
- 遗忘率最低（**FR 16.0%**），比次优方法低4.8个百分点。
- 在开放世界未知技能（S17、S18）上也表现出更好的泛化能力。
- 三个初步观察（语义子空间与参数子空间相关性一致、不同技能所需层分布不同、共享/特有知识自然解耦）为方法设计提供了有力依据。

## 7. 优点（方法与实验设计亮点）
- **任务创新**：首次提出LLCRM问题定义，并构建了标准基准，推动了机器人持续学习研究。
- **方法创新**：
  - 利用语义子空间关联参数子空间，实现无监督的知识聚合（无需技能ID）。
  - 提出共享知识继承与特有知识正交约束，兼顾新技能学习和旧技能保持。
  - 动态稀疏LoRA注入，适配不同技能复杂度。
- **实验设计**：包含模拟和真实环境，覆盖多种操作技能；对比方法全面；消融实验验证各组件必要性。
- **理论分析**：对共享知识继承策略进行了理论效率分析（文中提及“从理论上分析效率”，但未在摘要中详述）。

## 8. 不足与局限
- **实验覆盖**：未公开代码数据的具体规模（如每个技能的样本数），且没有在更通用的持续学习基准（如CL-ImageNet、CIFAR-100连续学习）上测试，方法对非机器人任务的泛化性未知。
- **偏差风险**：自建基准可能偏向于方法设计，对比方法可能未针对该基准进行超参数优化，存在不公平风险。
- **应用限制**：
  - 依赖预训练视觉语言模型（CLIP、LLaMA），在资源受限设备上部署困难。
  - 需要为每个新技能存储语义子空间投影矩阵和LoRA适配器，存储成本随时间线性增长。
  - 未考虑技能顺序的影响（任务顺序可能对结果有显著影响，本文未探究）。
- **消融实验**：仅做了两种消融，对于动态稀疏门控的稀疏率、正交项权重λ的选择等超参数敏感性未作充分分析。

（完）
