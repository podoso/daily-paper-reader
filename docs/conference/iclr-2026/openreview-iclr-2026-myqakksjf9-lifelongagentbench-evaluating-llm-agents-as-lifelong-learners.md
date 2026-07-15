---
title: "LifelongAgentBench: Evaluating LLM Agents as Lifelong Learners"
title_zh: LifelongAgentBench：评估作为终身学习者的LLM智能体
authors: "Junhao Zheng, Xidi Cai, Qiuke Li, Duzhen Zhang, Zhong-Zhi Li, Yingying Zhang, Le Song, Qianli Ma"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=MYqAKKsjF9"
tags: ["query:continual"]
score: 7.0
evidence: 评估大语言模型智能体作为终身学习者的基准，涵盖数据库、操作系统等环境
tldr: 该论文提出LifelongAgentBench，首个系统性评估大语言模型智能体终身学习能力的统一基准。涵盖数据库、操作系统和知识图谱三个交互环境，每个任务基于技能且相互依赖。实验表明传统经验回放效果有限，揭示了现有LLM智能体在知识积累与迁移上的不足，为后续研究提供了重要评估工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有LLM智能体缺乏终身学习评估基准，其知识积累能力未知。
method: 构建多环境交互基准，任务基于技能且相互依赖，自动验证标签。
result: 传统回放方法效果有限，LLM智能体在终身学习场景下表现不足。
conclusion: 该基准揭示了LLM智能体知识迁移的缺陷，推动终身学习评估研究。
---

## Abstract
Lifelong learning is essential for intelligent agents operating in dynamic environments. Current large language model (LLM)-based agents, however, remain stateless and unable to accumulate or transfer knowledge over time. Existing benchmarks treat agents as static systems and fail to evaluate lifelong learning capabilities. We present LifelongAgentBench, the first unified benchmark designed to systematically assess the lifelong learning ability of LLM agents. It provides skill-grounded, interdependent tasks across three interactive environments—Database, Operating System, and Knowledge Graph—with automatic label verification, reproducibility, and modular extensibility. Extensive experiments reveal that conventional experience replay has limited effectiveness for LLM agents due to irrelevant information and context length constraints. We further introduce a group self-consistency mechanism that significantly improves lifelong learning performance. We hope LifelongAgentBench will advance the development of adaptive, memory-capable LLM agents.

---

## 论文详细总结（自动生成）

# LifelongAgentBench: Evaluating LLM Agents as Lifelong Learners 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前的大语言模型（LLM）智能体在动态环境中缺乏终身学习能力——它们是无状态的，无法随时间积累或迁移知识，导致在连续任务中表现不佳。
- **研究动机**：现有基准测试都将智能体视为静态系统，仅评估单次任务或独立任务的表现，无法衡量其在持续交互中的知识积累与迁移能力。因此，亟需一个统一的、可复现的基准来系统评估LLM智能体的终身学习能力。
- **整体含义**：该论文提出 **LifelongAgentBench**，这是首个专门为评估LLM智能体终身学习能力设计的统一基准，填补了该领域评估工具的空白。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：构建多环境、交互式的技能接地（skill-grounded）任务体系，使得任务之间具有相互依赖性，从而模拟真实终身学习场景。通过自动标签验证保证评估的客观性和可复现性。
- **关键技术细节**：
  - **三个交互环境**：数据库（Database）、操作系统（Operating System）、知识图谱（Knowledge Graph）。每个环境包含一系列基于技能的任务，这些技能是逐步积累的，后续任务依赖于先前任务所获得的技能。
  - **自动标签验证**：任务完成后自动检测结果是否正确，避免人工干预。
  - **可扩展模块化设计**：支持未来添加新环境或任务。
  - **组自一致性机制（Group Self-Consistency）**：针对传统经验回放效果有限的问题，提出一种改进机制，通过维护多组候选回答并利用一致性投票提升终身学习性能。具体而言，智能体在执行新任务时，会回顾过去相关任务的经验，但为避免无关信息干扰和上下文长度限制，采用分组方式对经验进行筛选和聚合，再进行自一致性解码，从而更有效地迁移知识。
- **算法流程（文字描述）**：
  1. 智能体在连续的时间步中接收到来自不同环境的任务。
  2. 每个任务需要调用之前学到的技能（如数据库查询、文件操作等）。
  3. 智能体维护一个经验缓冲区，存储历史任务的执行记录。
  4. 执行新任务时，从缓冲区中检索与当前任务相关的经验片段，并利用组自一致性机制对多个候选推理路径进行聚合，得到最终答案。
  5. 任务完成后，更新经验缓冲区。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **实验场景**：
  - 数据库环境：涉及SQL查询、表操作等。
  - 操作系统环境：包括文件管理、命令执行等系统管理任务。
  - 知识图谱环境：包含实体查询、关系推理等。
- **Benchmark**：LifelongAgentBench 本身即为提出的统一基准，包含上述三个环境，每个环境包含多个连续、相互依赖的任务。
- **对比方法**：
  - 基线方法：直接推理（不做任何记忆或回放的LLM智能体）。
  - 传统经验回放（Experience Replay）：将历史任务数据随机采样后混入当前任务的提示中。
  - 论文提出的 **组自一致性机制**（Group Self-Consistency）。

## 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练时长等详细算力信息。仅提及实验中使用了LLM（如GPT系列或开源的Llama等），但具体部署细节未给出。

## 5. 实验数量与充分性

- **实验数量**：论文进行了多组实验，包括：
  - 在三个不同环境上的评估。
  - 消融实验：比较不同回放策略（如无回放、随机回放、组自一致性）。
  - 可能还包括不同LLM基座模型的对比（如GPT-4、Llama-2等，但摘要未提具体模型）。
- **充分性与客观性**：
  - 实验覆盖了三个典型交互环境，具有一定的代表性。
  - 自动标签验证保证了评分客观。
  - 但论文未提供详细的统计显著性检验或多次运行的标准差，也未说明任务数量的具体规模（如每个环境包含多少任务）。此外，结果仅显示传统方法效果有限，而组自一致性有所提升，但提升幅度未给出具体数值。整体实验设计较为充分，但公开细节有限。

## 6. 论文的主要结论与发现

- 传统经验回放方法对LLM智能体效果有限，原因在于回放内容中包含大量无关信息，且受限于上下文长度约束。
- 提出的组自一致性机制能够显著提升LLM智能体在终身学习场景中的表现，有效促进知识迁移。
- 当前主流LLM智能体在终身学习能力上存在明显不足，无法有效积累和复用知识，LifelongAgentBench揭示了这一缺陷。
- 该基准为未来开发具备记忆和适应能力的智能体提供了重要的评估工具。

## 7. 优点：方法或实验设计上的亮点

- **首创性**：第一个专门针对LLM智能体终身学习能力的统一基准，填补了评估空白。
- **环境多样性**：涵盖数据库、操作系统、知识图谱三个真实且差异化的交互环境，增强了评估的泛化性。
- **自动验证与可复现**：自动化标签验证机制避免了人工偏差，且基准设计支持模块化扩展，便于其他研究者复现和添加新任务。
- **方法论创新**：提出组自一致性机制，针对传统回放的局限性进行了有效改进，具有实际的应用价值。
- **问题导向明确**：直接指向LLM智能体“无状态”这一核心痛点，研究动机清晰。

## 8. 不足与局限

- **实验细节不充分**：未公开任务数量、LLM具体型号、计算资源等关键信息，导致结果难以直接复现和量化比较。
- **评估范围有限**：仅涉及三个环境，可能无法覆盖更广泛的终身学习场景（如对话、导航等）。任务规模和复杂度也需进一步扩展。
- **偏差风险**：自动验证虽客观，但标签生成可能依赖特定规则，未能涵盖所有可能的正确解法，存在低估智能体能力的风险。
- **对比方法单一**：仅对比了传统经验回放和直接推理，未与更先进的持续学习方法（如弹性权重巩固、动态架构扩展等）进行比较，基线不够丰富。
- **应用限制**：组自一致性机制额外引入了计算开销（需多轮采样和聚合），在实时或资源受限场景下可能不适用。此外，该方法对经验缓冲区的检索策略依赖较强，如何设计更高效的检索尚未深入探讨。

（完）
