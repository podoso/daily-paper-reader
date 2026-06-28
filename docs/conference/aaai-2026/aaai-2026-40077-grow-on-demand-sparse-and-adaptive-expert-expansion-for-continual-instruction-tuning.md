---
title: "Grow-on-Demand: Sparse and Adaptive Expert Expansion for Continual Instruction Tuning"
title_zh: 按需增长：持续指令微调的稀疏自适应专家扩展方法
authors: "Ying Zhang, Xingyue Guo, Yu Zhao, Xuhui Sui, Baohang Zhou, Xinying Qian, Xiaojie Yuan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40077/44038"
tags: ["query:continual"]
score: 9.0
evidence: 解决大语言模型持续指令微调中的灾难性遗忘
tldr: 本文针对持续指令微调中的灾难性遗忘问题，提出GoD-MoE框架。通过稀疏自适应的专家模块扩展策略，在相似任务间共享参数，仅在必要时扩展，无需数据重放即可平衡可塑性与稳定性。实验表明GoD-MoE在多个持续微调任务上显著减少遗忘并保持高性能，同时参数量增长可控。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续指令微调方法在平衡可塑性与稳定性时面临重放隐私问题或参数过度增长。
method: 设计基于MoE的按需增长框架，通过稀疏专家模块共享和自适应扩展避免数据重放。
result: 在多个持续指令调优基准上，该方法在防止遗忘的同时保持参数高效。
conclusion: 为LLM的持续学习提供了一种隐私友好且参数高效的解决方案。
---

## Abstract
Continual instruction tuning aims to incrementally adapt large language models to new tasks without forgetting previously acquired knowledge. Existing approaches often struggle to balance plasticity and stability. Replay-based methods retrain on historical data, which raises privacy concerns. Architecture-based methods allocate task-specific components, resulting in significant parameter growth. To address this, we consider a structure-sharing strategy that enables parameter reuse across similar tasks and expands only when necessary, avoiding any data replay. Specifically, we introduce Grow-on-Demand (GoD-MoE), a parameter-efficient framework that is based on sparse and adaptive expert module expansion for continual instruction tuning. GoD-MoE inserts multiple LoRA-based experts into attention layers and dynamically activates a small subset of experts for each task. To avoid redundant parameter growth, we develop an Expert Demand Detector that determines whether new experts are added, facilitating adaptive structural sharing and minimizing parameter overhead. We conduct comprehensive experiments on the TRACE benchmark, demonstrating that GoD-MoE achieves state-of-the-art performance. Furthermore, it effectively mitigates catastrophic forgetting and even outperforms several advanced replay-based baselines.

---

## 论文详细总结（自动生成）

# 论文《Grow-on-Demand: Sparse and Adaptive Expert Expansion for Continual Instruction Tuning》详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）在持续指令微调中会遭遇**灾难性遗忘**——学习新任务时遗忘先前学过的知识。现有方法在平衡**可塑性（学习新知识）** 与**稳定性（保持旧知识）** 上存在不足：
  - 基于重放的方法（replay-based）需要存储历史数据，引发**隐私风险**和存储开销；
  - 基于架构的方法（architecture-based）为每个任务分配独立组件，导致**参数爆炸**，训练效率降低。
- **整体意义**：本文提出一种无需数据重放、参数高效的持续指令微调框架 GoD-MoE，通过**稀疏且自适应的专家模块扩展**，在相似任务间共享参数，仅在必要时扩展新专家，从而实现可塑性、稳定性与隐私性的平衡。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
- 基于**Mixture-of-Experts (MoE)** 结构，将LoRA低秩矩阵拆分为多个专家，每个任务动态激活少量专家。
- 训练完当前任务后，冻结最活跃的专家以保留知识；新任务到来时，通过**专家需求检测器**判断是否需要新增专家，实现**按需增长**，避免冗余参数。

### 关键技术细节
1. **稀疏自适应专家扩展**：
   - 在每个注意力层的Q和V权重上插入多个LoRA专家（初始为4个）。
   - 前向传播时，通过门控函数选择top-2专家激活（公式2~3）。
   - 每任务训练后，冻结最活跃的2个专家；之后每新增任务，每层最多允许增加1个冻结专家。
   - 新专家初始化：权重矩阵取现有专家参数的平均值，路由向量取均值加高斯噪声。

2. **专家需求检测器**：
   - 基于新任务1%的样本，执行前向/反向传播，计算冻结专家和可训练专家的激活分布。
   - 将激活分布与三种原型模式（高匹配、部分匹配、低匹配）比较，使用**蒙特卡洛Dropout**进行M次随机前向传播，得到相似度均值和方差。
   - 采用**上置信界（UCB）准则**选择最匹配的模式，决定添加0、1或2个新专家（公式6~7）。
   - 超参数λ控制不确定性权重（实验中固定为1）。

3. **训练与推理协议**：
   - 每任务存储最终层表征的平均向量作为参考向量。
   - 推理时，计算输入的表征与所有参考向量的余弦相似度，选择最相似的任务对应的路由策略（无需任务ID）。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：**TRACE基准**（8个任务，每个任务5000训练样本），顺序为：C-STANCE、FOMC、MeetingBank、Py150、ScienceQA、NumGLUE-cm、NumGLUE-ds、20Minuten。涵盖领域指令、多语言理解、代码补全、数学推理。
- **一般LLM基准**：MMLU、GSM、BBH、BoolQ、PIQA（用于评估持续学习后的通用能力）。
- **对比方法**：
  - 传统方法：EWC（正则化）、L2P、PP（提示方法）。
  - 高级持续指令微调方法：O-LoRA、I-LoRA、PMoE、HiDe-LLaVA（其中PMoE和I-LoRA含重放）。
  - 直接微调方法：Full-FT、LoRA、LoRA-RE（1%重放）、MoE-LoRA。
  - 参考：Few-shot（6-shot）、Multi-task（联合训练作为上界）。
- **评估指标**：Last（最终任务性能）、Avg（平均）、BWT（后向迁移，衡量遗忘）。

## 4. 资源与算力

- 文中提到所有实验在**NVIDIA RTX A6000 GPU（48GB显存）** 上运行。
- 未明确说明GPU数量、训练时长或总参数量，仅给出了模型参数比例（如0.26%等）。
- 总体资源消耗较为合理，但缺乏具体算力统计。

## 5. 实验数量与充分性

- **主要实验**：在TRACE上对比11种baseline，报告Last、Avg、BWT（表1）。
- **通用能力评估**：在5个LLM基准上对比5种方法（表2）。
- **消融分析**：
  - 知识保留与获取曲线（图3、图4）。
  - 相似度得分与专家数量随任务变化（图5）。
  - 专家利用率可视化（图6）。
  - 对比“始终添加专家”变体（表3），验证扩展策略的有效性。
  - 不同任务顺序实验（表4），验证鲁棒性。
- **充分性评价**：实验覆盖主流baseline、多种指标、多角度分析（性能、参数效率、鲁棒性、可视化），设计较为全面，结果客观。但缺乏在更大规模模型（如LLaMA-13B以上）上的验证。

## 6. 论文的主要结论与发现

- GoD-MoE在TRACE上达到**最优平均性能（Avg=55.7）**，BWT=-3.6（仅次于有重放的PMoE的+12.2，但PMoE使用重放）。
- 相比直接LoRA/MoE-LoRA，GoD-MoE显著缓解遗忘，当前任务性能甚至优于单任务训练（图4）。
- 专家需求检测器有效控制扩张：前几个任务扩展较快，后期专家可重用，最终参数量比“总是添加专家”减少35.3%，性能仅下降0.4%（表3）。
- 不同任务顺序下性能稳定（Avg 55.0~56.4，表4），鲁棒性强。
- 专家利用率可视化显示：相似任务（如NumGLUE-cm/ds）激活相似专家，不同任务利用不同的专家组合，说明专家共享有效。

## 7. 优点：方法或实验设计上的亮点

- **无需数据重放**：同时解决隐私和存储问题，更贴合实际场景。
- **参数高效**：按需扩展使参数量增长近似对数/线性，远好于为每个任务分配独立组件。
- **自适应检测**：基于少量样本（1%）的轻量级检测器，避免主观预设专家数量。
- **结构共享**：通过冻结激活频率高的专家保留旧知识，激活可训练专家学习新知识，自然实现可塑性-稳定性平衡。
- **推理无需任务ID**：利用表征相似度自动选择路由策略，实用性强。
- **实验充分**：涵盖多种baseline、多维度分析（性能、遗忘、参数效率、鲁棒性、可视化），结论扎实。

## 8. 不足与局限

- **实验规模有限**：仅基于LLaMA2-7B，未在更大模型或不同架构（如LLaMA2-13B、GPT-like）上验证通用性。
- **基准覆盖**：TRACE虽包含8个任务，但任务类型仍有限（无视觉、多模态任务），且顺序固定，不同顺序实验仅3种。
- **检测器依赖少量样本**：1%样本能否代表任务特性？若任务分布高度异质，可能误判。
- **冻结策略**：每任务冻结top-2专家可能过于刚性，未考虑专家重叠或退化情况。
- **超参数λ（UCB系数）固定为1**：在更复杂场景下可能需要调优，文中未做敏感性分析。
- **隐私风险**：虽然避免数据重放，但存储每任务参考向量（平均表征）可能隐含一些分布信息，严格意义上并非完全隐私。
- **训练效率**：MoE结构引入额外的门控计算和冻结/解冻操作，实际训练开销未与baseline详细对比（如时间/吞吐量）。

（完）
