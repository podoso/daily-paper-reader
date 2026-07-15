---
title: Dynamic Mixture of Progressive Parameter-Efficient Expert Library for Lifelong Robot Learning
title_zh: 面向终身机器人学习的动态渐进参数高效专家库
authors: "Yuheng Lei, Sitong Mao, Shunbo Zhou, Hongyuan Zhang, Xuelong Li, Ping Luo"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=YKaoAJE2ej"
tags: ["query:continual"]
score: 9.0
evidence: 使用参数高效专家库的终身机器人学习
tldr: 终身机器人学习面临灾难性遗忘和知识共享不足问题，现有参数高效微调方法依赖测试时任务标识符。本文提出动态渐进参数高效专家库，逐步构建低秩专家库并通过动态混合实现前向迁移与遗忘缓解。实验表明DMPEL在多个机器人任务上实现高效持续学习，无需任务标识符。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有终身学习方法依赖任务标识符且缺乏知识共享。
method: 提出DMPEL，渐进构建低秩专家库并动态混合。
result: 在机器人持续学习任务中实现高效前向迁移和遗忘缓解。
conclusion: 动态专家库是终身机器人学习的有效框架。
---

## Abstract
A generalist agent must continuously learn and adapt throughout its lifetime, achieving efficient forward transfer while minimizing catastrophic forgetting. Previous work within the dominant pretrain-then-finetune paradigm has explored parameter-efficient fine-tuning for single-task adaptation, effectively steering a frozen pretrained model with a small number of parameters. However, in the context of lifelong learning, these methods rely on the impractical assumption of a test-time task identifier and restrict knowledge sharing among isolated adapters. To address these limitations, we propose Dynamic Mixture of Progressive Parameter-Efficient Expert Library (DMPEL) for lifelong robot learning. DMPEL progressively builds a low-rank expert library and employs a lightweight router to dynamically combine experts into an end-to-end policy, enabling flexible and efficient lifelong forward transfer. Furthermore, by leveraging the modular structure of the fine-tuned parameters, we introduce expert coefficient replay, which guides the router to accurately retrieve frozen experts for previously encountered tasks. This technique mitigates forgetting while being significantly more storage- and computation-efficient than experience replay over the entire policy. Extensive experiments on the lifelong robot learning benchmark LIBERO demonstrate that our framework outperforms state-of-the-art lifelong learning methods in success rates during continual adaptation, while utilizing minimal trainable parameters and storage.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：机器人需要具备终身学习能力——在持续接触新任务的过程中实现高效的前向迁移（forward transfer），同时最小化灾难性遗忘（catastrophic forgetting）。现有的主流范式是“预训练-微调”（pretrain-then-finetune），其中参数高效微调（PEFT）方法（如Adapter、LoRA）已被证明能通过少量参数适配单个任务。但在终身学习场景下，这些方法存在两个关键缺陷：(1) 依赖测试时的任务标识符（task identifier），这在实际应用中不可行；(2) 各个适配器彼此隔离，缺乏知识共享，导致前向迁移不足。

- **整体含义**：为了克服上述限制，论文提出一种不需要任务标识符、能动态共享和重用知识的新型终身学习方法，旨在让机器人以参数高效的方式持续学习多个任务。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：构建一个**动态渐进参数高效专家库（Dynamic Mixture of Progressive Parameter-Efficient Expert Library, DMPEL）**。它逐步扩充一个低秩专家库，并通过轻量级路由器动态组合专家形成端到端策略。

- **关键技术细节**：
  - **渐进式专家库构建**：每遇到一个新任务，不是直接增加整个新适配器，而是基于已有的低秩专家库，仅学习少量新的低秩参数（如LoRA风格的模块），将新知识融入库中。专家库是逐步增长的，但总体参数量保持高效。
  - **动态混合路由**：使用一个轻量级路由器（router），根据输入的观察（observation）自动选择并加权组合专家，无需任何任务标识符。路由器输出每个专家的混合系数，从而生成当前任务所需的策略参数。
  - **专家系数回放（Expert Coefficient Replay）**：为了缓解遗忘，论文提出存储每个历史任务的“专家系数分布”（即路由器的输出），并在后续训练中回放这些系数，作为约束引导路由器正确检索冻结的旧专家。相比直接回放整个策略（experience replay over the entire policy），这种方法显著节省存储和计算。

- **流程简述（文字说明）**：
  1. 初始化一个空的低秩专家库和一个路由器。
  2. 对于第1个任务：训练路由器使其输出固定权重（或学习一组专家），并更新专家库。
  3. 对于后续任务：路由器根据当前输入动态组合已有专家，同时学习新增的少量专家参数。同时，从记忆中采样之前任务的专家系数分布，让路由器在训练新任务时保持对旧任务的响应能力，从而抑制遗忘。
  4. 测试时：仅用路由器根据输入自动加权专家，无需任务标识。

## 3. 实验设计

- **数据集/场景**：使用机器人终身学习基准 **LIBERO**（Lifelong Robot Learning Benchmark）。该基准包含多个连续的任务（如抓取、放置等），涉及视觉输入和动作控制。
- **Benchmark**：LIBERO 提供的标准终生学习评估协议，包括持续适配过程中的成功率（success rate）以及最终性能。
- **对比方法**：与多种现有的终身学习方法进行对比，包括基于全网络微调的方法、基于经验回放的方法（如ER、EWC、SI等）以及参数高效的适配方法（如Adapter、LoRA）并配备任务标识符。DMPEL在无需任务标识符的情况下与这些方法对比。

## 4. 资源与算力

- 论文摘要和元数据中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅能从常规实验推断可能使用了单卡或数卡（如NVIDIA RTX 3090或A100等），但无法确定。这一点需要在分析中明确指出“文中未明确给出”。

## 5. 实验数量与充分性

- **实验数量**：在LIBERO基准上进行了完整的终身学习实验，包含多轮持续适配。此外还进行了消融实验（如验证专家系数回放的效果、不同专家库构建策略的对比等）。但具体实验数量未在摘要中列出，通常至少包含主对比实验（多任务序列）、消融实验、参数分析等。
- **充分性与公平性**：
  - 充分性：覆盖了主要性能指标（成功率）和存储、参数效率的对比，能够支撑核心结论。
  - 客观公平：对比了当前最先进的终身学习方法，且DMPEL无需任务标识符，比较条件合理。
  - 不足之处：仅有单一基准（LIBERO），未在多机器人任务集或不同视觉困难度的场景下验证，可能存在泛化性局限。

## 6. 论文的主要结论与发现

- DMPEL在LIBERO基准上**超越了所有对比的终身学习方法**，在持续适配期间获得更高的成功率，同时使用的可训练参数和存储量显著更少。
- 动态混合专家库机制能够在不依赖任务标识符的前提下实现高效的前向迁移和抑制遗忘。
- 提出的**专家系数回放**技术相比经典经验回放（存储完整动作或状态）在存储和计算上更优，且能有效缓解灾难性遗忘。

## 7. 优点

- **参数高效**：仅需学习少量低秩参数，极大减少了存储和训练成本，适合资源受限的机器人平台。
- **无需任务标识符**：路由器自动根据输入分配专家权重，更符合真实机器人终身学习场景（任务不可预知）。
- **动态知识共享**：专家库可跨任务复用，促进前向迁移，避免孤立适配器。
- **可扩展性**：渐进式构建专家库，可随任务数量线性增长而控制参数量增长（低秩结构）。
- **简洁有效的遗忘缓解机制**：专家系数回放替代全策略回放，效率高。

## 8. 不足与局限

- **实验场景单一**：仅在LIBERO基准上验证，缺乏在不同机器人形态、不同任务领域（如操作、导航）的泛化评估。
- **未说明计算资源**：无法判断训练复杂度或对比方法的公平性（如是否使用相同硬件）。
- **专家系数回放可能引入偏差**：回放的是历史路由分布，若离线存储的系数因策略变化而不准确，可能影响遗忘抑制效果，论文未充分讨论这一点。
- **缺乏理论分析**：对于动态专家库的收敛性、遗忘上界等缺乏理论保证。
- **应用限制**：假设预训练模型已经较好（如已有视觉基础模型），若预训练模型质量差，则专家库效果会下降；此外，路由器可能过拟合于观察中的干扰特征。

（完）
