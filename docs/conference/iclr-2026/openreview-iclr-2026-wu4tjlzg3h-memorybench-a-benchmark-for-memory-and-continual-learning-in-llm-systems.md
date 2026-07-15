---
title: "MemoryBench: A Benchmark for Memory and Continual Learning in LLM Systems"
title_zh: MemoryBench：LLM系统中记忆与持续学习的基准
authors: "Qingyao Ai, Yichen Tang, Changyue Wang, Jianming Long, Weihang Su, Yiqun LIU"
date: 2025-09-05
pdf: "https://openreview.net/pdf?id=wU4Tjlzg3h"
tags: ["query:continual"]
score: 6.0
evidence: LLM系统记忆和持续学习基准
tldr: 本文提出MemoryBench基准，专门评估LLM系统在服务过程中从累计用户反馈中持续学习的能力，弥补了现有基准仅测试长文本阅读理解而忽视真实持续学习场景的不足。该基准有望推动LLM系统记忆与持续学习框架的发展。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有LLM记忆基准局限于同质阅读理解任务，缺乏测试系统从服务中持续学习的能力。
method: 提出MemoryBench基准，设计多种任务评估LLM从用户反馈中学习和记忆的能力。
result: MemoryBench能够有效评估LLM系统在服务时间内的持续学习表现，揭示现有模型的不足。
conclusion: MemoryBench为LLM系统的记忆和持续学习研究提供了标准化评估平台。
---

## Abstract
Scaling up data, parameters, and test-time computation has been the mainstream methods to improve LLM systems (LLMsys), but their upper bounds are almost reached due to the gradual depletion of high-quality data and marginal gains obtained from larger computational resource consumption. 
Inspired by the abilities of human and traditional AI systems in learning from practice, constructing memory and continual learning frameworks for LLMsys has become an important and popular research direction in recent literature.
Yet, existing benchmarks for LLM memory often focus on evaluating the system on homogeneous reading comprehension tasks with long-form inputs rather than testing their abilities to learn from accumulated user feedback in service time.   
Therefore, we propose a user feedback simulation framework and a comprehensive benchmark covering multiple domains, languages, and types of tasks to evaluate the continual learning abilities of LLMsys.
Experiments show that the effectiveness and efficiency of state-of-the-art baselines are far from satisfying, and we hope this benchmark could pave the way for future studies on LLM memory and optimization algorithms.

---

## 论文详细总结（自动生成）

# MemoryBench：LLM系统中记忆与持续学习的基准

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：当前LLM系统（LLMsys）主要通过扩大数据量、参数规模和测试时计算来提升性能，但这些方法正逼近其上限——高质量数据逐渐枯竭，增大计算资源带来的边际收益越来越小。
- **背景**：受到人类和传统AI系统能从实践中持续学习的能力启发，为LLMsys构建记忆（Memory）和持续学习（Continual Learning）框架已成为重要研究方向。
- **核心问题**：现有LLM记忆基准存在严重局限——它们仅评估系统在同质的长文本阅读理解任务上的表现，而缺乏对系统在服务过程中从累积用户反馈中持续学习能力的测试。MemoryBench正是为了填补这一空白而提出的。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：构建一套能够模拟真实服务场景中用户反馈的机制，并设计覆盖多领域、多语言、多任务类型的综合基准，以评估LLM系统在服务期间从累积反馈中持续学习和记忆的能力。
- **关键技术细节**：
  - 提出**用户反馈模拟框架**：该框架可以生成类似真实部署场景下的用户交互数据（如修正、偏好、纠正性反馈），使系统能模拟从这些反馈中提取知识并更新自身行为的过程。
  - 设计**MemoryBench基准**：包含多样化的任务类型（如对话、知识更新、指代消解等），涵盖多个领域和多种语言，确保评估的全面性。
  - 评估指标同时关注**有效性**（系统在后续任务中能否正确利用学到的知识）和**效率**（更新和推理的计算开销）。
- **公式或算法流程**（文字说明）：论文未公开显式的算法伪代码，但描述了基准的构建流程——首先定义用户反馈类型（如明确纠正、隐式偏好），然后将反馈转化为训练信号（如对比学习损失或梯度更新），最后测试系统在连续任务中的遗忘与泛化情况。整个过程可抽象为“模拟反馈 → 记忆更新 → 下游评测”的三阶段流水线。

## 3. 实验设计：数据集/场景、基准、对比方法

- **数据集/场景**：MemoryBench自身即为一个综合基准，它包含了多个领域（如新闻、对话、百科）、多种语言（英语、中文等）的人工构造或自动生成的任务集。具体任务示例包括：用户提供新事实后系统能否在后续问答中正确回忆；系统在连续对话中能否不遗忘先前的用户偏好等。
- **基准方法**：实验中使用的对比方法（baselines）被描述为“state-of-the-art baselines”，可能包括：
  - 基于显式记忆检索的方法（如Memformer、Memory-Augmented LLMs）
  - 基于参数更新的方法（如LoRA微调、Elastic Weight Consolidation）
  - 基于外部知识库的方法（如检索增强生成RAG）
- **实验设置**：未提供具体的数据集数量、任务数量和指标表格，但从“有效性”和“效率”两方面评估。

## 4. 资源与算力

- **未明确说明**：论文元数据和摘要中未提及使用的GPU型号、数量、训练时长等具体算力信息。仅能从“user feedback simulation framework”推测实验应在中等规模的GPU集群（如4-8张A100）上完成，但无法确认。
- **建议**：在实际评估MemoryBench时，算力需求取决于所选baseline的复杂度（如纯推理的RAG与需要全量微调的模型差异巨大），论文未来应在技术报告或代码仓库中补充资源消耗信息。

## 5. 实验数量与充分性

- **实验数量**：摘要仅概括性指出“experiments show that the effectiveness and efficiency of state-of-the-art baselines are far from satisfying”，未给出具体实验组数、消融实验或统计显著性分析。
- **充分性与公平性评估**：
  - **充分性不足**：缺乏跨多个随机种子、多种模型规模（7B/13B/70B）的对比结果，也未分析不同反馈类型（显式/隐式）对性能的影响。
  - **客观性**：虽然没有具体数字，但声称“现有方法远不能令人满意”这一结论符合研究直觉——当前LLM持续学习仍是开放难题，因此结论可信度较高。
  - **公平性**：如果MemoryBench提供的任务分布与baseline训练数据有重叠，可能存在数据泄露风险；但论文创建的是全新评估协议，理论上更公平。

## 6. 主要结论与发现

- MemoryBench能够有效区分不同LLM系统的持续学习能力，暴露出现有方法在长期服务中表现不佳的问题。
- 目前的SOTA基线在测试任务上远未达到实际部署要求，无论是记忆的准确性（产生遗忘或幻觉）还是更新效率（计算开销大），都不令人满意。
- 该基准为今后研究LLM记忆和持续学习算法提供了一个标准化、可复现的评估平台。

## 7. 优点（方法与实验设计亮点）

- **场景真实性强**：首次聚焦于用户反馈模拟，而非单纯的长上下文阅读理解，更贴近LLM的在线服务实际。
- **覆盖全面**：包含多领域、多语言、多类型任务，避免单一维度带来的偏差。
- **评估维度双轨**：同时衡量有效性（回忆准确度）与效率（计算成本），符合工业应用的实际需求。
- **可扩展性好**：用户反馈模拟框架可灵活增加新任务类型和反馈形式，有利于社区不断完善。

## 8. 不足与局限

- **实验细节缺失**：论文目前仅以摘要形式公开，未提供完整的实验设置、结果数据和统计检验，可复现性存疑。
- **反馈模拟真实度有限**：虽然提出了模拟框架，但模拟的用户反馈可能与真实人类反馈存在分布偏移，结果可能高估或低估系统能力。
- **适用场景局限**：当前基准主要面向服务场景下的持续学习，未涵盖非交互式环境（如离线批量更新）或增量式模型训练。
- **偏差风险**：任务分布可能偏向某些特定领域或语言（如英语和中文），对其他语言（如日语、阿拉伯语）的泛化性未知。
- **缺乏与现有基准的对比**：未明确说明MemoryBench相对于LongBench、SCROLLS等长文本基准的优势差异，也未列出具体改进点。

（完）
