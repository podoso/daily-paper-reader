---
title: "Schema-Guided Event Reasoning: A Plug-and-Play Event Reasoning Framework Based on Large Language Models"
title_zh: 模式引导的事件推理：基于大语言模型的即插即用事件推理框架
authors: "Yuying Liu, Xuechen Zhao, Yanyi Huang, Ye Wang, Xin Song, Yue Zhang, Haiyan Liu, Bin Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40501/44462"
tags: ["query:ie"]
score: 6.0
evidence: 利用LLM进行模式引导的事件推理
tldr: 针对LLM在事件推理中对事件结构建模不足的问题，本文提出即插即用的模式引导事件推理框架（SGER）。该框架在模式抽取阶段将事件描述映射为语义结构表示，实现从实例到模式的抽象转换，从而在不依赖预定义模式库的情况下增强LLM的事件推理能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: LLM对事件结构建模不足，现有方法依赖预定义模式库缺乏可扩展性。
method: 设计即插即用的模式引导框架，在线抽取事件结构模式辅助LLM推理。
result: SGER在事件推理任务上取得良好效果，且无需预定义模式库。
conclusion: 动态模式抽取能有效提升LLM在事件推理中的表现。
---

## Abstract
Recent advancements in Large Language Models have increasingly demonstrated their potential for event reasoning. However, LLMs still struggle with this task due to inadequate modeling of event structures. Although introducing schema knowledge has been shown to improve event reasoning performance, existing methods rely on predefined schema library, compromising their scalability and lightweight deployment. To address these challenges, we propose SGER, a plug-and-play Schema-Guided Event Reasoning framework. In the schema extraction stage, the model maps event descriptions with diverse surface forms to potential semantic structure representations, achieving an abstract transformation from instances to schemas. The schema prediction stage captures the potential associations between historical event schemas to make forward-looking inferences about possible future event schemas. In the event reasoning stage, we integrate historical events and predicted schemas into prompts to guide LLMs in generating specific, contextually consistent predicted events. Experimental evaluations demonstrate that our framework significantly improves event reasoning performance of LLMs.

---

## 论文详细总结（自动生成）

# 论文详细总结：Schema-Guided Event Reasoning: A Plug-and-Play Event Reasoning Framework Based on Large Language Models

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大型语言模型（LLMs）在事件推理任务中表现不足，主要原因是难以显式建模事件结构，无法充分理解事件间的语义关系。
- **现有局限**：虽然引入结构化的事件模式（schema）已被证明能提升推理性能，但现有方法依赖于预定义的事件模式库，这限制了其可扩展性和轻量级部署能力。
- **研究动机**：设计一种不依赖预定义模式库、能够在线自动抽取并利用事件模式来增强LLMs事件推理能力的框架，使LLMs能够在更高抽象层次上捕获事件演化规律。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
提出 **SGER（Schema-Guided Event Reasoning）** 框架，采用“即插即用”的模块化设计，通过一个显式的模式抽象层将事件推理任务分解为三个子任务：模式抽取、模式预测、事件推理。框架不依赖预定义模式库，而是在推理过程中自动识别和生成高质量的事件模式，并用这些模式指导LLMs进行更准确的推理。

### 关键技术细节

#### (1) 模式提取器（Schema Extractor）
- **功能**：将具体的事件描述（实例级别）转化为抽象的事件类型（模式级别）。例如：“Emma felt her awareness on the topic had expanded significantly” → “knowledge increase”。
- **建模**：采用序列到序列的映射函数 \( f_{\text{extract}}: E_I \to E_S \)，其中 \( E_I \) 是实例描述，\( E_S \) 是抽象事件类型。
- **实现**：基于 **BART-large** 模型进行微调，通过最小化交叉熵损失来训练。
- **损失函数**：
  \[
  L_{CE} = \frac{1}{N} \sum_{i=1}^{N} \text{CE loss}(E_S^i \mid f_{\text{extractor}}(E_I^i, \theta_{\text{extractor}}))
  \]

#### (2) 模式预测器（Schema Predictor）
- **功能**：基于上下文中的历史事件模式，预测与当前查询最相关的事件类型（用于CEC任务）或事件关系（用于CRR任务），生成参考模式 \( S_{\text{predict}} \) 或参考关系 \( R_{\text{predict}} \)。
- **建模**：函数 \( f_{\text{predict}}: \text{Input}_S \to (S_{\text{predict}} \lor R_{\text{predict}}) \)，输入为指令、上下文、问题（包含查询事件和关系/事件对）以及候选集合。
- **实现**：基于 **Llama3.2-3B** 模型，使用 **LoRA** 进行参数高效微调，同时引入 **对比学习** 增强判别能力：训练时随机选择负样本，最小化预测与正样本距离、最大化与负样本距离。
- **对比损失**：
  \[
  L_{CL} = \frac{1}{N} \sum_{i=1}^{N} \left[ \text{CE loss}(p_S^i \mid f_{\text{predictor}} (\text{Input}_S^i, \theta_{\text{predictor}})) + \text{CE loss}(n_S^i \mid f_{\text{predictor}} (\text{Input}_S^i, \theta_{\text{predictor}})) \right]
  \]

#### (3) 事件推理器（Event Reasoner）
- **功能**：将历史事件（实例或模式）与预测出的参考模式/关系整合到精心设计的提示模板中，输入任意的LLM，引导其生成符合语义和上下文逻辑的最终预测事件或关系。
- **提示模板构成**：任务指令、上下文信息、模式指导（参考模式或关系）。
- **推理流程**：
  - 实例级任务：先由模式提取器将实例事件转为模式，然后模式预测器生成参考模式/关系，最后事件推理器基于所有信息输出答案。
  - 模式级任务：跳过提取器，直接由预测器生成参考，然后推理器输出。

## 3. 实验设计：数据集、benchmark、对比方法

### 数据集
- **主要数据集**：**EV²**（Tao et al., 2025），包含四个子任务：
  - S-CEC（模式级事件分类）
  - I-CEC（实例级事件分类）
  - S-CRR（模式级关系推理）
  - I-CRR（实例级关系推理）
- **训练集划分**：从I-CEC和I-CRR各取20%样本训练模式提取器；从S-CEC和S-CRR各取20%样本训练模式预测器。测试集为剩余部分。
- **额外泛化性数据集**：**MCNC**（Li, Ding, Liu, 2018），用于评估模型在未见过的、分布外事件上的推理能力（五选一任务，预测结尾事件）。

### Benchmark
- 以各任务准确率（Accuracy）为评价指标。

### 对比方法（Baselines）
- **闭源LLM**：GPT-4o、GPT-3.5
- **开源LLM**：Qwen2-7B、Baichuan2-7B、Orca2-7B、Chatglm2-6B、Internlm2-7B、Llama2-7B、Vicuna-7B、Llama3.2-3B
- 所有对比均使用相同的推理参数（greedy decoding，max new tokens=512）。

### 消融与分析实验
- **消融实验1**：去除模式预测器，仅使用提取器输出的事件类型和关系直接注入提示（E+R配置）。
- **消融实验2**：去除提取器和预测器，训练一个“推理助手”（Reasoning Assistant）同时处理实例和模式数据（RA+R配置），并比较在MCNC上的泛化性。
- **分析实验**：分别使用黄金事件类型（替代提取器输出）和单独评估预测器在模式级任务上的性能，测试各模块的独立上限。

## 4. 资源与算力
论文明确提及：
- **训练环境**：Ubuntu服务器，配备 **Nvidia A800 GPU**，Python 3.10，PyTorch 2.6，CUDA 12.1。
- **模式提取器**（BART-large）：学习率5e-5，线性衰减，batch size=8，训练时长约 **20分钟**。
- **模式预测器**（Llama3.2-3B + LoRA）：LoRA rank=16，scaling factor=32，学习率5e-5，batch size=8，训练时长约 **40分钟**。
- **推理阶段**（以Llama2-7B为例）：单样本推理平均时间 **4.12秒**，额外GPU内存占用约 **34.40 GB**（包含基础模型）。提取器和预测器各自的推理时间分别为0.51秒和0.17秒，内存占用分别为1.38 GB和5.97 GB。
- **总训练时间**：约60分钟（两个模块训练之和）。

## 5. 实验数量与充分性

### 实验组数
- **主实验**：在EV²的四个任务上，对11个LLM（3个闭源+8个开源）分别测试了原始模型和SGER增强模型，共4×11×2 = 88组结果（表2）。
- **消融实验**：在Llama2-7B上进行了4个配置（Van, E+R, RA+R, SGER）在四个任务上的对比（表3），共16组结果。另外在MCNC上对8个模型进行了Vanilla、SGER、RA+R的对比（表4），共8×3=24组结果。
- **分析实验**：在EV²上使用黄金类型（表5）和单独预测器，共4组（模块独立上限）。
- **资源与速度分析**（表6）：一个对比表格。

### 充分性与公平性
- **充分性**：涵盖实例级和模式级、分类和关系推理两大类任务；在多个开源和闭源模型上进行验证；做了消融、泛化、模块上限等多种分析，实验设计较为全面。
- **公平性**：所有LLM推理使用相同参数（greedy decoding、相同max tokens）；对比模型包括不同规模的模型；训练数据划分比例明确；但需要注意，主实验中对GPT-3.5等闭源模型的API调用细节未完全公开，可能存在微小差异（如随机性）。整体实验设计客观，对比基准合理。

## 6. 论文的主要结论与发现
- SGER框架显著提升了LLMs在事件推理任务上的性能，特别是在基线较低的模型上提升巨大（如Llama2-7B在S-CEC上提升26.55%）。
- 闭源模型（GPT-4o、GPT-3.5）在SGER下也获得提升，但幅度较小（GPT-4o在大部分任务上提升1-3%，但I-CEC上仅提升0.38%）。
- 直接引入原始事件类型（不经过预测）反而损害性能（E+R配置准确率下降），突显了模式预测环节的必要性。
- 混合训练的“推理助手”（RA+R）虽然在实例级训练集上表现不错，但在分布外数据集MCNC上泛化性差，而SGER保持了较好的泛化能力，说明分步抽象-预测的流程更优。
- 模式提取器和预测器单独使用黄金数据时能达到接近或优于完整框架的性能，证明了各模块的有效性；同时提示了事件推理器并未完全采纳预测器的建议，存在指令遵循问题。

## 7. 优点
- **即插即用设计**：模式提取器和预测器可作为独立模块无缝集成到任何闭源或开源LLM中，无需修改模型结构，可扩展性强。
- **不依赖预定义模式库**：自动在线提取模式，解决了传统方法需要手动构建模式库的瓶颈，提高了实际部署的灵活性。
- **多级抽象提升泛化**：通过将实例抽象为模式，在高层次捕获事件演化规律，增强了对分布外事件的推理能力。
- **轻量高效**：两个小模型（BART-large + 3B LLM）即可提供有效指导，训练总时间约1小时，推理额外开销较小（4秒/样本），资源占用可接受。
- **消融与分析实验充分**：不仅验证了框架整体有效性，还深入分析了各模块的独立贡献和局限性，为后续改进提供了方向。

## 8. 不足与局限
- **指令遵循问题**：事件推理器（LLM）未能完全采纳模式预测器的正确建议，导致部分任务性能低于预测器单独上限（如S-CEC上66.24% vs 预测器71.91%）。论文指出这可能是LLM的指令遵循限制，但未提出有效解决方案。
- **GPT-3.5在I-CEC上性能下降**：闭源模型的API行为不可控，可能导致负面效果，表明框架对不同模型的鲁棒性仍需验证。
- **数据集规模有限**：EV²数据集大小未明确给出，但训练集仅为各任务20%的样本（I-CEC 98/393，I-CRR 147/588，S-CEC 98/388，S-CRR 146/584），数据量较小，可能限制模型泛化性评估的可靠性。
- **关系类型有限**：仅考虑6种预定义关系（Causes, IsResult, Before, After, IsSubevent, HasSubevent），未能覆盖更复杂或细粒度的事件关系。
- **实验覆盖偏差**：主实验主要在EV²上进行，虽然增加了MCNC泛化测试，但MCNC仅涉及I-CEC类似任务，未对关系推理进行跨域验证。
- **计算资源报告不完全**：虽然给出训练和推理时间，但未提供详细的总能耗或更细粒度的算力需求（如GPU内存峰值等）。另外，所有实验在单一GPU型号（A800）上进行，不同硬件下性能可能变化。
- **应用限制**：框架依赖一个额外的小型提取器和预测器，增加了系统复杂度和部署成本，对于资源极度受限的场景可能不够轻量。

（完）
