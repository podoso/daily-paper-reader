---
title: "SEFEL: A Simple Yet Effective Framework for Fast Event Linking"
title_zh: SEFEL：快速事件链接的简洁有效框架
authors: "Yinan Liu, Ziyang Zhang, Bin Wang, Xiaochun Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38564/42526"
tags: ["query:ie"]
score: 8.0
evidence: 事件链接框架用于事件抽取
tldr: 事件链接旨在将文本事件提及关联到知识库，现有方法计算成本高且泛化受限。本文提出SEFEL框架，利用端到端的事件表示和论元感知机制，统一处理知识库内外事件。实验表明SEFEL在速度和准确率上均优于传统检索排序方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有事件链接方法依赖手工规则且计算开销大，实体链接直接应用效果不佳。
method: 构建端到端论元感知事件表示模型，统一处理知识库内外事件链接。
result: 在多个事件链接数据集上取得更快速度和更高准确率。
conclusion: SEFEL为事件抽取下游任务提供了高效的事件链接方案。
---

## Abstract
Event linking aims to associate event mentions in text with their corresponding entries in a knowledge base (KB). This task can help text understanding to benefit downstream tasks (e.g., question answering) and expand the KB through new event knowledge mentioned in the text. Existing event linking approaches usually adopt a retrieve-and-rank framework, which suffers from high computational costs and relies on hand-crafted rules, thereby limiting generalization. Additionally, it is found that some entity linking methods can be used to solve this task directly. However, they also perform not well. In this paper, we propose SEFEL, an end-to-end, argument-aware event representation-based event linking framework to unify the modeling of both in-KB and out-of-KB scenarios. To further enhance the linking performance, we propose a contrastive learning module to refine the learned embeddings of events and event mentions. Experimental results demonstrate that SEFEL improves accuracy by at least 3.59 (in-KB) and 21.5 (out-of-KB) compared with baselines, while its inference speed is more than 38 times faster than baselines, showcasing its accuracy and efficiency.

---

## 论文详细总结（自动生成）

# 论文总结：SEFEL: A Simple Yet Effective Framework for Fast Event Linking

## 1. 核心问题与整体含义（研究动机和背景）
- **任务定义**：事件链接（Event Linking）旨在将文本中的事件提及（event mention）关联到知识库（KB）中对应的事件条目，同时处理知识库外（out-of-KB）事件。
- **现有挑战**：
  - 事件表达多样化，同一事件可能有不同描述，导致词汇重叠度低。
  - 事件论元（如时间、地点、参与者）常跨句子分布，难以捕获。
  - 知识库覆盖有限，需同时处理 in-KB 和 out-of-KB 事件。
- **现有方法局限**：
  - 主流方法采用“检索-重排序”框架（如 BLINK），计算成本高（需为每个提及与多个候选事件进行交叉编码）。
  - 依赖手工规则提取事件论元（如 ArgEveLink），泛化能力差，且对 out-of-KB 事件识别效果不佳。
  - 实体链接方法直接用于事件链接效果较差（实验验证）。
- **研究动机**：提出一种高效、准确、可统一处理 in-KB 和 out-of-KB 事件的端到端事件链接框架。

## 2. 方法论：核心思想、关键技术细节
### 2.1 总体架构：SEFEL
- **四部分构成**：
  1. **Out-of-KB 事件样本生成**：利用 LLM（LLaMA-3.1-70B-Instruct）提取事件论元，并通过对论元进行替换、重写生成 out-of-KB 事件训练样本，增强模型对 unseen 事件的判别能力。
  2. **事件链接基础模块**：双塔 Transformer 架构，分别编码候选事件描述和论元感知的事件提及表示，并引入可学习的 NIL 嵌入统一处理 out-of-KB 事件。
  3. **对比学习模块**：从“提及-提及”和“提及-候选”两个视角进行对比学习，提升嵌入质量。
  4. **优化与推理**：联合优化多个损失函数，推理时直接通过相似度计算完成链接。

### 2.2 关键技术细节
- **论元感知事件提及表示**：
  - 对每个事件提及 m 及其提取的论元集合 A_m，构造 M = m ∪ A_m，并通过平均池化融合嵌入：h_M = (h_m + Σ h_a) / (|A_m|+1)。
  - 候选事件集通过字典检索从 m 和 A_m 中合并得到，并加入 NIL 候选。
- **损失函数**：
  - **基础损失** L_base = α·L_ce + β·L_fuse，其中 L_ce 为描述相似性交叉熵，L_fuse 为融合事件流行度（Wikipedia 锚链接统计）和描述相似性的线性层后的交叉熵。
  - **对比损失** L_ct = γ·L_mm + δ·L_mc，其中 L_mm 为提及-提及对比（使用动量更新记忆库），L_mc 为提及-候选对比。
  - 联合优化：L = Σ ζ·L_base + η·L_ct。
- **事件流行度**：基于 Wikipedia 锚链接统计先验概率，辅助判断候选事件可能性，特别有利于 out-of-KB 检测。

### 2.3 推理过程
- 直接计算 z_M 与所有候选事件嵌入（包括 NIL）的点积，取最高分作为预测结果，无需额外重排序。

## 3. 实验设计
- **数据集**：
  - **Wikipedia 数据集**：自动构建，包含 66,425 训练、16,692 验证、19,267 测试（均为 in-KB 样本，按 FIGER schema 中“Event”类别筛选）。
  - **NYT 数据集**：New York Times 标注语料，769 测试（in-KB），993 测试（out-of-KB），包含大量无对应 KB 事件。
- **评价指标**：准确率（Accuracy），按全部、动词、名词分别报告。
- **对比方法**：
  - BM25（词项匹配）、GENRE（生成式）、BLINK（检索+重排序）、EveLink（融入命名实体）、ArgEveLink（融入论元结构）、GPT-4o-mini（指令式重排序）。
  - 基线结果来自原论文（Hsu et al., 2024），GPT-4o-mini 通过 API 运行。
- **环境**：4×RTX A6000 GPU，统一环境对比效率。

## 4. 资源与算力
- 文中明确提及所有效率实验在 **4×RTX A6000 GPU** 上进行。
- **训练时长未明确说明**，但推理时间有详细报告：SEFEL 在 Wikipedia 测试集上耗时 446 秒，NYT 测试集 59 秒，远快于 ArgEveLink（24612/2250 秒）和 GPT-4o-mini（50293/4596 秒）。
- 对比学习需要维护记忆库（大小为 512），动量更新，额外带来一定训练开销但未给出具体训练时间。

## 5. 实验数量与充分性
- **主实验**：在 Wikipedia 和 NYT 两个数据集上，对比 6 种基线，报告全部/动词/名词准确率。
- **消融实验**（Table 5）：去除事件描述、事件流行度、提及-提及对比、提及-候选对比，共 4 组，验证各组件贡献。
- **论元感知表示分析**（Table 4）：对比使用 LLM 提取论元（SEFEL）、传统方法 Uni+Tag、不使用论元（SEFEL-EAE），共 3 组。
- **参数敏感性分析**（Figure 3）：针对温度 τ 在 0.02~0.20 范围变化，观察精度波动（<0.62% on Wikipedia，<0.06% on NYT）。
- **效率对比**：Table 3 报告推理时间，包括并行化 ArgEveLink 的额外实验（72.5% 准确率，6492 秒）。
- **公平性**：所有基线结果来自同一公开论文（Hsu et al., 2024），GPT-4o-mini 自行复现，环境统一。消融实验完整，参数研究合理，实验设计较为充分。

## 6. 主要结论与发现
- SEFEL 在 **in-KB** 场景（Wikipedia）上准确率 **83.64%**，比最佳基线 ArgEveLink（80.05%）提升 **3.59%**；在 **out-KB** 场景（NYT）上准确率 **76.90%**，比 ArgEveLink（55.40%）提升 **21.5%**，提升显著。
- 推理速度比 ArgEveLink 快 **约 38 倍**，比 GPT-4o-mini 快 **约 80 倍**。
- 论元感知表示有效提升性能（SEFEL vs SEFEL-EAE：+1.42% on Wikipedia，+20.37% on NYT）。
- LLM 提取论元优于传统规则提取（SEFEL vs SEFEL_Uni+Tag：+0.36% on Wikipedia，+14.47% on NYT）。
- 事件流行度对 out-of-KB 检测至关重要（去除后 NYT 准确率从 76.90% 降至 56.92%）。
- 对比学习模块进一步改善嵌入质量（去除任一视角均导致性能下降）。

## 7. 优点
- **创新性**：首次提出端到端、论元感知的对比学习事件链接框架，统一处理 in-KB 和 out-of-KB，无需手工规则。
- **效率高**：采用双塔编码，单次前向传播完成推理，避免交叉重排序，速度优势明显。
- **鲁棒性强**：对温度参数 τ 不敏感，性能稳定。
- **实验充分**：包含多层次消融、参数分析、效率对比，结果全面。
- **实用性强**：开源代码，易于复现和应用。

## 8. 不足与局限
- **训练数据依赖**：out-of-KB 样本生成依赖于特定 LLM（LLaMA-3.1-70B），不同 LLM 可能影响生成质量，且生成数据占比仅 1%，对大规模 out-of-KB 场景的泛化性需进一步验证。
- **论元提取依赖 LLM**：虽避免手工规则，但 LLM 调用成本高（尤其大模型），且可能产生幻觉或不完整论元，影响表示质量。
- **数据集规模有限**：Wikipedia 数据集自动构建但仅包含图式过滤后的“事件”类页面，可能遗漏模糊事件；NYT 数据集较小。
- **未对比更多最新事件链接方法**：如基于 LLM 的上下文学习方法等，仅对比了 2024 年之前的基线。
- **缺乏跨领域泛化测试**：实验仅基于新闻和 Wikipedia 领域，未在金融、医疗等专业领域验证。
- **算力需求未完全透明**：训练时长未报告，训练阶段可能仍需较大资源（尽管推理快）。

（完）
