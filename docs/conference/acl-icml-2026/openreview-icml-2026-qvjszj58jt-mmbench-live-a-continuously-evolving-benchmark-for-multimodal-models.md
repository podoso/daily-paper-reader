---
title: "MMBench-Live: A Continuously Evolving Benchmark for Multimodal Models"
title_zh: MMBench-Live：持续演进的多模态模型基准
authors: "Yuanzhi Liu, Shousheng Zhao, Bo Zhou, Kongming Liang, Zhanyu Ma"
date: 2026-04-30
pdf: "https://openreview.net/pdf/fed7203837051af691dd646ee39581494636abe7.pdf"
tags: ["query:multimodal"]
score: 6.0
evidence: 多模态视觉语言模型基准
tldr: 现有视觉语言模型基准多为静态，易过时且受数据污染。本文提出MMBench-Live，一个持续演进的基准，通过多智能体自动流水线实现任务导向的数据集构建、实时数据采集和可验证问答生成。采用分布一致更新策略保持跨版本可比性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 静态多模态基准面临时间过时和数据污染问题。
method: 设计多智能体驱动的自动化流水线，持续构建新数据并保持分布一致性。
result: MMBench-Live能有效更新基准，减少污染并维持版本间可比性。
conclusion: 持续演进的基准是多模态模型评估的重要发展方向。
---

## Abstract
Evaluation benchmarks are essential for assessing vision--language models (VLMs), but most multimodal benchmarks are static, making them vulnerable to temporal staleness, data contamination, and costly maintenance. We present MMBench-Live, a continuously evolving multimodal benchmark built by a multi-agent-driven automated pipeline. Our framework treats benchmark evolution as task-guided dataset construction, integrating structured benchmark specification, feedback-controlled real-time data acquisition, and verifiable QA generation with executable reasoning. To maintain cross-version comparability, we introduce a distribution-consistent update strategy that extracts task-related visual patterns from the original benchmark to guide data collection and filtering. Instantiated from MMBench, MMBench-Live contains 5.9K newly generated evaluation instances with a high answer correctness rate, while each update costs about \$30 and takes 1--2 hours. Extensive evaluations show that MMBench-Live preserves stable model rankings, maintains semantic alignment with the original benchmark, and exhibits weaker contamination-related memorization signals, suggesting a practical and scalable paradigm for sustainable multimodal benchmark evolution. The project is available at \url{https://github.com/PRIS-CV/MMBench-Live}.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：当前大多数多模态视觉语言模型（VLM）评估基准（benchmark）是静态的，存在三大问题：
  - **时间过时**：静态基准无法反映模型在最新任务或场景上的能力。
  - **数据污染**：模型可能在训练过程中“记住”了静态基准的测试样本，导致评估结果虚高。
  - **维护成本高**：定期人工构建新基准费时费力，难以持续。
- **整体目标**：提出一种可持续演进的基准方案，使得基准能够自动更新、保持新鲜度、降低污染风险，同时维持跨版本间的可比性，实现低成本、可扩展的多模态模型评估。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将基准演进视为**任务导向的数据集构建**问题，利用**多智能体自动流水线**持续生成新的评测实例，并通过**分布一致更新策略**保证新版本与旧版本的可比性。
- **关键技术细节**：
  - **多智能体自动化流水线**：包含多个智能体模块（如任务规范理解、实时数据采集、可验证QA生成、数据过滤等），协同完成从定义任务到生成问答对的全过程。
  - **结构化基准规范**：将基准演进行为形式化的数据集构建任务，明确任务类型、评估维度等。
  - **反馈控制的实时数据采集**：根据当前基准的分布特征和任务需求，从真实世界（如新闻、社交媒体、视频流）中动态获取图像/视频数据，并加入质量控制反馈。
  - **可验证问答生成**：生成的每个问答对附带可执行的推理链，支持自动正确性验证，保证答案正确率高。
  - **分布一致更新策略**：
    - 提取原始基准（MMBench）中与任务相关的视觉模式（如图像主题、难度分布、类别比例等）作为指导。
    - 在数据采集和过滤阶段，确保新生成实例的分布与原始基准的分布保持一致，从而新版本的模型排名与旧版本排名具有可比性。
- **算法流程（文字描述）**：
  1. 输入原始基准MMBench及其任务规范。
  2. 利用视觉模式提取模块分析原始基准的分布特征。
  3. 多智能体调度器启动实时数据采集（例如从互联网或特定视频流抓取图片）。
  4. 对采集数据执行过滤（基于分布一致性约束）。
  5. 通过LLM/VLM智能体生成带有可验证推理链的问答对。
  6. 自动验证答案正确性，保留通过验证的实例。
  7. 按照分布一致策略整合新实例到基准中，形成新版本。

## 3. 实验设计：数据集/场景、基准、对比方法
- **基准**：从MMBench实例化，初始版本MMBench-Live包含**5.9K个新生成的评估实例**。
- **实验场景**：
  - 评估多模态视觉语言模型（VLMs）在MMBench-Live上的表现，并与原始MMBench的排名进行对比。
  - 检测数据污染信号（memorization-related signal），比较新基准与原始基准的抗污染能力。
  - 分析跨版本模型排名的稳定性（Spearman相关系数等）。
- **对比方法**：未详细列出具体对比的竞争基准，主要与原始MMBench（静态版本）进行对比，验证新基准是否保持了排名的稳定性并降低了污染风险。

## 4. 资源与算力
- **文中明确说明**：每次更新的成本约为 **30美元**，耗时 **1-2小时**。
- **未说明GPU型号、数量等具体硬件细节**，因此无法推断算力规模，仅知成本极低、耗时短，体现了高效性。

## 5. 实验数量与充分性
- **实验数量**：主要实验围绕：
  - 新基准实例的答案正确率（高正确率）。
  - 模型排名与原始MMBench的一致性（稳定排名）。
  - 语义对齐程度。
  - 污染相关记忆信号（弱于原始基准）。
- **充分性分析**：
  - 实验覆盖了基准的**有效性**（正确率）、**可比性**（排名稳定）、**抗污染性**三个关键维度。
  - 但论文未展示在**多个不同初始基准**上的泛化实验（仅从MMBench实例化），也未提供**长时间多轮更新后的演化效果**的详细数据。
  - 对比方法较少（仅对比静态版本），缺乏与其他持续基准方案（如人工构建更新）的全面对比。
  - 总体而言，实验设计聚焦于验证核心假设，但**覆盖广度一般**，有待更丰富的消融和跨场景验证。

## 6. 论文的主要结论与发现
- **结论**：MMBench-Live能够以低成本、短时间持续生成高质量评测实例（5.9K个，正确率高）。
- **发现**：
  - 新基准与原始MMBench保持稳定的模型排名排序（Spearman相关系数高）。
  - 新基准的语义内容与原始基准对齐。
  - 相较于原始静态基准，新基准表现出更弱的污染相关记忆信号，即**更不易被模型记忆**。
  - 每次更新仅需约30美元和1-2小时，具备可扩展性。
- **总体判断**：持续演进的基准是多模态模型评估的重要发展方向，MMBench-Live提供了可行的实现范式。

## 7. 优点：方法或实验设计上的亮点
- **自动化流水线**：完全多智能体驱动，无需人工标注，实现端到端的基准更新，大幅降低维护成本。
- **分布一致更新策略**：巧妙解决了跨版本可比性问题，使得新老基准评价结果可以公平对比。
- **可验证QA生成**：引入可执行推理链，确保答案正确性，避免自动生成带来的噪声。
- **实时数据采集**：动态从真实世界获取数据，确保基准时效性和抗污染能力。
- **成本极低、速度快**：每次更新30美元/1-2小时，易于长期部署。

## 8. 不足与局限
- **初始依赖单一基准**：仅从MMBench实例化，未验证其通用性（是否可迁移到其他多模态基准，如COCO、Flickr30k等）。
- **长期演化效果未充分验证**：只展示了单次或短期更新结果，未展示多轮更新后分布漂移、排名稳定性变化等长期影响。
- **对比实验不充分**：缺乏与其他持续基准方法（如定期人工重建、基于对抗样本的更新等）的定量比较。
- **抗污染评估维度有限**：仅使用记忆信号指标，未能全面评估数据污染的其他形式（如任务过拟合）。
- **任务范围局限**：当前设计主要适用于视觉问答类任务，未涉及生成、指代、视觉推理等更复杂的评估场景。
- **实验公开性**：项目主页已公开，但论文中未详细列出所有测试的模型种类和数量，透明度有限。

（完）
