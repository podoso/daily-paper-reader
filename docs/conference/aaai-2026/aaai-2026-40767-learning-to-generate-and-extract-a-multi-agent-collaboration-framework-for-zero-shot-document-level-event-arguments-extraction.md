---
title: "Learning to Generate and Extract: A Multi-Agent Collaboration Framework for Zero-Shot Document-Level Event Arguments Extraction"
title_zh: 学习生成与提取：零样本文档级事件论元抽取的多智能体协作框架
authors: "Guangjun Zhang, Hu Zhang, Yazhou Han, Yue Fan, Yuhang Shao, Hongye Tan, Ru Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40767/44728"
tags: ["query:ie"]
score: 9.0
evidence: 事件论元抽取框架
tldr: 针对零样本文档级事件论元抽取中合成数据质量难以保证的问题，提出多智能体协作框架，利用大语言模型生成数据并通过质量评估机制提升可靠性，实验表明该方法在多个基准上显著优于现有方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有零样本事件论元抽取方法依赖事件类型提示，难以捕捉未见事件的结构关系，且合成数据缺乏质量评估。
method: 提出多智能体协作框架，包括生成、评估和提取智能体，协同完成零样本事件论元抽取。
result: 在多个基准数据集上取得最优性能，验证了框架的有效性。
conclusion: 多智能体协作能有效提升零样本事件论元抽取的准确性和鲁棒性。
---

## Abstract
Document-level event argument extraction (DEAE) is essential for knowledge acquisition, aiming to extract participants of events from documents. In the zero-shot setting, existing methods employ LLMs to generate synthetic data to address the challenge posed by the scarcity of annotated data. However, relying solely on Event-type-only prompts makes it difficult for the generated content to accurately capture the contextual and structural relationships of unseen events. Moreover, ensuring the reliability and usability of synthetic data remains a significant challenge due to the absence of quality evaluation mechanisms. To this end, we introduce a multi-agent collaboration framework for zero-shot document-level event argument extraction (ZS-DEAE), which simulates the human collaborative cognitive process of “Propose–Evaluate–Revise.” Specifically, the framework comprises a generation agent and an evaluation agent. The generation agent synthesizes data for unseen events by leveraging knowledge from seen events, while the evaluation agent extracts arguments from the synthetic data and assesses their semantic consistency with the context. The evaluation results are subsequently converted into reward signals, with event structure constraints incorporated into the reward design to enable iterative optimization of both agents via reinforcement learning. In three zero-shot scenarios constructed from the RAMS and WikiEvents datasets, our method achieves improvements both in data generation quality and argument extraction performance, while the generated data also effectively enhances the zero-shot performance of other DEAE models.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **任务**：零样本文档级事件论元抽取（ZS-DEAE），即在没有未见事件类型标注数据的情况下，从文档中抽取事件参与者。
- **现有挑战**：
  - 使用LLM生成合成数据时，仅依赖事件类型提示，难以准确捕捉未见事件的上下文和结构关系。
  - 缺乏有效的质量评估机制，生成的合成数据可靠性不足，可能引入噪声，反而降低下游抽取性能。
- **研究动机**：模拟人类“提出-评估-修正”的协作认知过程，通过多智能体协同提升合成数据质量与抽取性能。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：构建一个多智能体协作框架，包含**生成代理**和**评估代理**，通过强化学习迭代优化，实现“Propose–Evaluate–Revise”循环。
- **关键技术细节**：
  - **生成代理**（基于LLaMA3.1-8B / Qwen2.5-7B）：给定未见事件类型和角色集合，生成文档级上下文、事件触发词和角色-论元对。使用自回归目标在已见事件数据上微调。
  - **评估代理**（基于Bart-Gen，即BART-large）：从生成的数据中提取论元，并评估语义一致性。输入为上下文和含占位符的模板，输出为填充后的模板。通过计算对数似然作为质量指标。
  - **事件结构约束**：为避免生成大量空论元（None）的倾向，引入结构完整性惩罚项，使样本中空论元比例接近训练数据分布。
  - **强化学习优化**：将归一化后的对数似然减去惩罚项作为奖励信号，通过策略梯度更新两个代理的参数，使高质量样本获得更高奖励。
- **算法流程**（文字说明）：
  1. 生成代理为每个未见事件类型生成K个候选样本。
  2. 评估代理对每个样本计算对数似然，应用结构约束得到最终质量分数。
  3. 将分数作为奖励，通过梯度上升更新生成代理和评估代理的参数。
  4. 重复多轮直至收敛（论文中为5轮）。

## 3. 实验设计
- **数据集与场景**：
  - 使用RAMS和WikiEvents构建三种零样本场景：`RAMS2RAMS`、`RAMS2Wiki`、`Wiki2Wiki`。
  - 每种场景中，训练集和测试集的事件类型不重叠，角色可共享。
- **基准方法**：
  - **DEAE模型**：PAIE、TabEAE、DEEIA、HMPEAE、TSAR、SCPRG（部分适配为零样本）。
  - **零样本模型**：EEQA、ZSTL、Bart-Gen、Distar（改造为文档级）。
  - **大语言模型**：Phi-4、Gemma-1.1、Mixtral、LLaMA3.1、GPT-4o、DS-V3、DS-R1（使用零样本和Chain-of-Thought提示）。
- **评价指标**：Span-F1（严格边界匹配）。

## 4. 资源与算力
- 论文中**未明确说明**使用的GPU型号、数量和总训练时长。
- 仅提及：生成代理使用LLaMA3.1-8B和Qwen2.5-7B，通过LoRA（秩8，缩放因子32，dropout 0.05）进行参数高效微调；评估代理使用Bart-large。运行了5轮代理交互优化，使用3个不同随机种子报告平均结果。
- 算力消耗较高，但未提供具体量化数据。

## 5. 实验数量与充分性
- **主要实验**：表1展示了三种场景下与12种以上基线的对比，每个场景报告了可见角色、不可见角色和总体F1。
- **消融实验**：表2分别移除RL奖励和结构约束，验证各组件贡献。
- **分析实验**：
  - 交互轮次影响（图4a损失曲线，图4b F1趋势）。
  - 合成数据质量提升效果（表3：将合成数据加入其他模型训练集）。
  - 评估代理的区分能力（图5：对正常/缺失/错配数据给出不同似然）。
  - 合成数据多样性分析（图6：四个维度随轮次变化）。
  - 案例分析（图7：与GPT-4o、LLaMA3.1-70B生成样本对比）。
- **充分性评估**：实验较为充分，覆盖多种基线、多场景、消融和分析，对比公平（统一数据集、指标）。但仅使用Span-F1一个指标，未采用更灵活的边界宽松度量，可能对LLM类方法不公平。总体设计合理。

## 6. 论文的主要结论与发现
- 所提多智能体协作框架在所有三个零样本场景中均取得最优或次优结果，显著优于现有DEAE模型和主流LLM。
- 合成数据不仅能提升自身性能（通过强化学习迭代），还能有效增强其他DEAE模型（如TabEAE、Bart-Gen）的零样本能力。
- 结构约束有效降低了空论元比例，提升了合成数据完整性。
- 随着交互轮次增加，合成数据多样性在词汇、语义、句法维度下降，导致后期性能略有退化，但逻辑多样性保持稳定。

## 7. 优点
- **创新性**：首次将多智能体协作机制引入零样本DEAE，模拟人类“提出-评估-修正”认知过程，框架设计直观且有效。
- **完备性**：引入事件结构约束和强化学习奖励设计，解决了合成数据中空论元偏好和缺乏评估的痛点。
- **通用性**：生成的合成数据可即插即用，增强其他模型性能，说明其高质量和泛化能力。
- **实验扎实**：多场景、多基线、多轮次分析，消融和案例分析全面，结果可复现（提供代码链接）。
- **稳定性**：损失曲线显示代理训练过程收敛良好。

## 8. 不足与局限
- **多样性退化**：后期交互导致词汇、语义、句法多样性下降，可能限制模型对未见数据的泛化，论文承认这是性能下降的原因之一，但未提出有效缓解策略。
- **指标单一**：仅使用Span-F1，严格边界匹配可能低估LLM的能力（LLM往往能识别正确语义但边界不精确），建议补充宽松F1或语义匹配评估。
- **算力成本**：需微调两个大模型并执行多轮交互优化，资源消耗较高，论文未给出具体量化，不利于实际部署评估。
- **数据集局限**：仅在RAMS和WikiEvents上评估，未涉及更多领域（如金融、医疗）或更大规模数据集，跨领域零样本泛化能力未知。
- **结构约束的设计**：仅基于训练数据中空论元比例的均值和标准差，对分布变化敏感，可能不适用于角色分布差异大的事件类型。
- **缺乏理论分析**：强化学习优化的收敛性、最优轮次选择等缺乏理论支撑，主要依赖经验设定。

（完）
