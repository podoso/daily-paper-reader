---
title: Discovering Latent Facts from Context to Construct Richer Open Knowledge Graphs
title_zh: 从上下文中发现潜在事实以构建更丰富的开放知识图谱
authors: "Jinpeng Li, Hang Yu, Ziqi Ma, Peng Qi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38998/42960"
tags: ["query:ie"]
score: 9.0
evidence: 提出开放知识图谱构建方法，属于核心信息抽取任务
tldr: 本文针对基于LLM的知识图谱构建无法发现跨文本潜在事实的问题，提出KG-DLF方法。通过增强上下文逻辑一致性，从多个文本中挖掘潜在新事实，构建更丰富的开放知识图谱。该方法突破了LLM输入长度限制，有效提升了知识图谱的覆盖面和准确性。实验证明KG-DLF在开放知识图谱构建任务上优于现有方法，推动了信息抽取技术的发展。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于LLM的知识图谱构建方法受限于输入长度，仅能抽取单文本内知识，缺乏跨文本发现能力。
method: 设计新颖的开放知识图谱构建方法，通过逻辑一致性约束发现跨文本潜在新事实。
result: 在多个开放知识图谱构建数据集上，生成的知识图谱覆盖更广且更准确。
conclusion: 为信息抽取中的知识图谱构建提供了一种跨文本挖掘新途径。
---

## Abstract
Knowledge graph construction (KGC) aims to extract valuable information from text and organize it into structured knowledge graphs (KGs). Recent methods have leveraged the strong generative capabilities of large language models (LLMs) to improve the generalization and reduce the labor costs. However, constrained by the input length of LLMs, existing methods mainly focus on extracting knowledge within individual texts and lack the capability to discover latent knowledge across texts. To fill this gap, we propose a novel method for open knowledge graph construction, termed KG-DLF. The core idea of this method is to enhance the knowledge graph construction process by discovering new facts that are consistent with the underlying contextual logic. Specifically, we first design a knowledge extractor to extract knowledge from the text. Then, a knowledge normalizer performs schema alignment on the extracted knowledge. Next, we explore a knowledge discoverer based on a clue search strategy, which leverages the logical consistency of context to mine latent facts. Finally, we design a counterfactual-based knowledge corrector, enabling the model to purify knowledge and reduce factual errors. Experimental results show that KG-DLF is capable of extracting comprehensive knowledge in open-world scenarios across three KGC benchmarks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有基于大语言模型（LLM）的知识图谱构建（KGC）方法受限于LLM的单次输入长度，通常采用文本分片策略，独立处理每个文本片段。这导致抽取的知识是碎片化的，缺乏跨文本的语义关联，无法发现隐藏在多个文本之间的潜在事实，从而使得构建的知识图谱结构不连续、不完整。
- **背景**：传统KGC依赖多步骤流水线（实体识别、关系抽取、知识融合），泛化能力差、错误传播严重、成本高。LLM的出现将KGC统一为文本到文本的生成任务，但输入长度限制造成了上述知识碎片化问题。
- **整体意义**：本文首次提出通过发现与上下文逻辑一致的潜在事实来增强KGC过程，突破输入长度限制，构建更丰富、更连贯的开放知识图谱。

## 2. 方法论：核心思想、关键技术细节、公式/算法流程
- **核心思想**：KG-DLF（Knowledge Graph construction by Discovering Latent Facts）包含四个模块：知识抽取器、知识标准化器、知识发现器、知识纠正器。核心在于利用LLM的常识和线索检索策略，从跨文本实体对中推理出符合上下文的潜在关系，并通过反事实比较进行自动纠错。
- **关键技术细节**：
  - **知识抽取器**：使用少样本提示（ICL）引导LLM从文本中抽取事实三元组（主语, 关系, 宾语），并定义每个元素的模式（schema）描述。
  - **知识标准化器**：基于BERT的嵌入模型Φ(·)计算新抽取模式与预定义模式集的余弦相似度，选择最相似的模式进行对齐（相似度阈值λ）。使用对比损失（margin α=0.2）训练嵌入模型。
    - 公式：`s* = argmax_{si∈S} sim(ŝ, si)`，其中 `sim(ŝ, si) = cos(ĥ_s, h_{si})`。
  - **知识发现器**：首先让LLM判断两个实体在现实中是否有关联。若有关联，则通过**线索检索策略**：对每个实体对(s,o)，在对方实体的l跳邻域内（l=2）取实体，用LLM评分函数ψ(·)计算路径平均置信度，选择Top-k路径作为上下文线索，最后引导LLM推断关系。
    - 公式：`conf_X(p_i) = (1/l) Σ_{j=1}^l ψ(X, e_j)`，`P_X^{(k)} = Top-k({conf_X(p_i) | p_i ∈ P_X})`。
  - **知识纠正器**：受反事实思维启发，为每个事实构造一组反事实（替换关系），通过LLM比较原始事实与反事实的合理性（选择最合理的一个）。若原始事实的合理性最高则保留，否则被修正。
- **算法流程（文字说明）**：
  1. 输入文本→知识抽取器输出初始三元组及模式定义。
  2. 知识标准化器将模式对齐到统一模式集。
  3. 知识发现器跨文本识别相关实体对，检索Top-k线索路径，生成潜在新事实。
  4. 知识纠正器对抽取和发现的事实进行反事实验证，修正错误。
  整个过程无需微调基础LLM。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：
  - **WebNLG***：DBpedia事实与文本配对，1,165个文本-事实对，4,001个事实，345个实体，159个关系（单文本场景）。
  - **REBEL***：复杂长距离依赖关系抽取，从105,516条测试集中随机采样1,000条长文本事实对，包含4,000个事实，3,643个实体，196个关系（长距离依赖场景）。
  - **Wiki-NRE***：维基百科文本与知识图谱关系，随机采样1,000个跨文本实例（由两个以上文本组成），2,335个实体，45个关系（跨文本长尾场景）。
- **基准对比方法**：
  - **通用大模型（GLMs）**：Mistral-7B-Instruct、LLaMA3-8B-Instruct、ChatGPT-3.5、ChatGPT-4.0（通过问答抽取+去重）。
  - **生成式构建方法（GCMs）**：REGEN、GenIE、SAC-KG、EDC+R、AutoSchemaKG。
- **评价指标**：F1、Exact（精确匹配）、Partial（部分匹配）、Strict（严格匹配元素类型），基于token的评估脚本WEBNLG。

## 4. 资源与算力
- 论文明确说明使用22核CPU（AMD EPYC 7T83）和两块RTX-4090 GPU（各24GB内存），基于PyTorch和HuggingFace实现。
- **未明确说明训练时长**（因为KG-DLF无需微调基础LLM，主要耗时为LLM推理时间）。实验报告取三次运行的平均值。

## 5. 实验数量与充分性
- **实验数量**：
  - **主实验**（Table 1）：在三个数据集上对比了5个GLMs和5个GCMs，每个设置三次平均。
  - **消融实验**（Table 2）：对四个模块（KE, KN, KD, KC）进行6种组合，在三个数据集上测试。
  - **参数分析**（Figure 3）：分析了ICL示例数h、线索数k、相似度阈值λ_E和λ_R对F1的影响。
  - **案例研究**（Figure 4）：展示真实场景中潜在事实发现和错误纠正的效果。
- **充分性判断**：实验覆盖了单文本、长距离、跨文本三种典型场景，对比了多种基线和通用模型，进行了详细的消融和参数分析，结论有充分证据支持。实验设计客观、公平。

## 6. 主要结论与发现
- KG-DLF在三个数据集上均取得最优结果：
  - WebNLG*：F1=0.845，比EDC+R提升1.9%（0.826→0.845）。
  - REBEL*：F1=0.648，比EDC+R提升4.6%（0.602→0.648）。
  - Wiki-NRE*：F1=0.800，比AutoSchemaKG提升8.6%（0.714→0.800）。
- 跨文本场景（Wiki-NRE*）提升最大，证实潜在事实发现能有效缓解知识碎片化。
- 知识发现器（KD）和知识纠正器（KC）对结构指标（Strict, Exact）贡献显著，知识标准化器（KN）对语义一致性重要。
- 最优ICL示例数为5，线索数k=3（平衡性能与存储），实体相似度阈值λ_E=0.80，关系相似度阈值λ_R=0.75。
- 案例显示发现器能推断“cooperation”等隐含关系，纠正器能修正如“star”误用为关系的错误。

## 7. 优点（方法或实验设计上的亮点）
- **创新性**：首次提出通过发现跨文本潜在事实来增强KGC，解决LLM输入限制导致的碎片化问题。
- **方法完备性**：设计了从抽取、标准化、发现到纠错的完整流水线，各模块可独立使用或组合。
- **无需微调**：所有模块基于LLM提示和检索实现，无需训练基础模型，易于迁移到不同LLM。
- **反事实纠正器**：新颖的自纠正机制，通过构造反事实比较提高事实正确性，模拟人类反思。
- **实验全面**：覆盖多种场景、多种基线、详细消融和参数分析，案例可视化增强说服力。

## 8. 不足与局限
- **计算成本**：虽然免训练，但多次调用LLM（抽取、标准化、发现、纠正）导致推理开销较大；线索检索需要维护邻域图，存储规模随k增长较快（k=4时平均3.3MB）。
- **依赖LLM质量**：底层LLM（如Mistral-7B）效果差时，KG-DLF提升有限；方法高度依赖LLM的常识推理和评分能力。
- **实验覆盖**：仅测试了三个英文数据集，未覆盖多语言或特定领域（如医学、金融）；未与基于微调的方法（如REBEL原文的微调模型）进行横向比较。
- **发现范围限制**：线索检索仅在l=2跳邻域内进行，可能遗漏更远距离的潜在关联。
- **错误传播**：标准化和发现模块的错误可能影响后续纠正模块，虽然纠正器有一定容错能力。
- **公平性**：对比的GCMs中部分模型（如REGEN、GenIE）使用较老的基座模型，可能未充分代表当前SOTA。

（完）
