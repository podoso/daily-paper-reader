---
title: A Reasoning Paradigm for Named Entity Recognition
title_zh: 一种面向命名实体识别的推理范式
authors: "Hui Huang, Yanping Chen, Ruizhang Huang, Chuan Lin, Yongbin Qin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40375/44336"
tags: ["query:ie"]
score: 9.0
evidence: 命名实体识别，推理范式，思维链
tldr: 针对生成式LLM在命名实体识别中缺乏显式可验证推理机制的问题，提出一个包含思维链生成、思维链微调和推理增强的三阶段推理框架，将NER范式从隐式模式匹配转变为显式推理，在零样本和低资源场景下显著提升性能和泛化能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM通过指令调优进行NER时缺乏显式推理，导致零样本和低资源场景下性能不佳。
method: 构建面向NER的思维链数据集，通过思维链生成、微调和推理增强三阶段框架实现显式推理。
result: 在多个标准NER数据集上，该推理范式显著优于传统指令调优方法，尤其在零样本设置下。
conclusion: 显式推理机制可有效提升NER的泛化能力，为信息抽取提供了新范式。
---

## Abstract
Generative LLMs typically improve Named Entity Recognition (NER) performance through instruction tuning. They excel at generating entities by semantic pattern matching but lack an explicit, verifiable reasoning mechanism. This "cognitive shortcutting" leads to suboptimal performance and weak generalization,  especially in zero-shot and low-resource scenarios where reasoning from limited contextual cues is crucial.
To address this issue, a reasoning framework is proposed for NER, which shifts the extraction paradigm from implicit pattern matching to explicit reasoning. This framework consists of three stages: Chain of Thought (CoT) generation, CoT tuning, and reasoning enhancement. First, a dataset annotated with NER-oriented CoTs is generated, which contain task-relevant reasoning chains. Then, they are used to tune the NER model to generate coherent rationales before deriving the final answer. Finally, a reasoning enhancement stage is implemented to optimize the reasoning process using a comprehensive reward signal. This stage ensures explicit and verifiable extractions.
Experiments show that ReasoningNER demonstrates impressive cognitive ability in the NER task, achieving competitive performance. In zero-shot settings, it achieves SoTA performance, outperforming GPT-4 by 12.3 percentage points on the F1 score. Analytical results  demonstrate its great potential to advance research in reasoning-oriented information extraction.

---

## 论文详细总结（自动生成）

# 论文总结：A Reasoning Paradigm for Named Entity Recognition

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前基于生成式大语言模型（LLM）的命名实体识别（NER）方法主要依赖指令调优，通过语义模式匹配直接生成实体标签，缺乏显式、可验证的推理机制。这种“认知捷径”导致模型在零样本和低资源场景下泛化能力差，难以利用有限的上下文线索进行逻辑推断。
- **整体含义**：论文旨在将NER从隐式模式匹配范式转变为显式推理范式，从而提升模型的可解释性、泛化能力和数据效率。通过引入链式推理（Chain of Thought, CoT），使模型在预测前先生成逐步推理过程，最终实现更鲁棒的实体识别。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **范式转变**：将NER视为一个显式推理过程，而非直接的输入-输出映射。模型需先生成关于实体识别逻辑的思维链（CoT），再输出最终实体列表。
- **三阶段框架**：
  1. **CoT生成（CoT Generation, CG）**：基于现有NER数据集（如Pile-NER）构建具有高质量CoT标注的NER-CoT数据集。通过重标注、结构验证和语义一致性筛选三步生成。
  2. **CoT微调（CoT Tuning, CT）**：使用NER-CoT数据集对基础LLM进行监督微调，最大化条件概率 \( \log p(Y|X, S) \)，其中Y = (CoT, 实体列表)。
  3. **推理增强（Reasoning Enhancement, RE）**：采用GRPO（Group Relative Policy Optimization）算法，结合两种奖励函数（span-level F1奖励和格式一致性奖励）优化推理策略，避免分布漂移。

### 关键技术细节
- **NER-CoT数据集**：由45,787个样本组成，每个样本包含输入文本X、实体模式S、推理链C和实体列表E。
- **奖励函数**：组合奖励 \( R(o_i) = \lambda_{F1} R_{F1}(o_i) + \lambda_{schema} R_{schema}(o_i) \)，其中 \( \lambda_{F1}=10, \lambda_{schema}=1 \)。
- **GRPO更新**：使用组内平均奖励作为基线计算优势，并引入KL散度正则化防止策略偏离参考模型。

## 3. 实验设计

### 数据集与场景
- **训练数据**：
  - CoT微调：自建的NER-CoT数据集（45,787样本）。
  - 推理增强：从InstructUIE（20个NER数据集）中分层采样4,703样本。
- **评估数据集**：
  - **跨域（out-of-domain）**：CrossNER（5个子域：AI、文学、音乐、政治、科学）+ MIT-Movie、MIT-Restaurant（共7个数据集）。
  - **零样本**：20个标准NER基准（包括ACE05、CoNLL03、OntoNotes等）。
  - **低资源**：CoNLL03训练集按1%、5%、10%随机下采样。
  - **监督评估**：20个NER基准的全监督设置。

### 对比方法
- **非推理模型**：ChatGPT-3.5、UniNER、InstructUIE、GoLLIE、KnowCoder、GPT-4、GLiNER-L、B2NER等。
- **推理模型**：DeepSeek-R1（8B/32B）、Qwen3（4B/8B）、ReasoningNER（1.7B/8B）。

### 评价指标
- span-based Micro-F1。

## 4. 资源与算力

- **基础模型**：Qwen3-8B（主实验），也测试了InternLM2-7B、Llama2-7B等。
- **训练细节**：
  - SFT：5 epoch，序列长度8192，学习率2e-5（余弦调度），batch size 256。
  - GRPO：1 epoch，clip阈值0.2，KL系数0.04，batch size 384。
  - 优化器：AdamW。
  - 加速技术：bfloat16混合精度、梯度检查点、FlashAttention-2、Liger-kernel。
- **算力信息**：**未明确说明** GPU型号、数量及训练时长，仅提及使用了上述优化技术提升计算效率。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验（表1）：在7个数据集上对比15+方法。
  - 消融实验（表2）：逐步分析4个组件的影响。
  - 监督评估（表3）：20个数据集全监督设置，对比4个基线。
  - 零样本评估（表4）：20个数据集零样本设置，对比3个基线。
  - 低资源实验（图3）：3种数据比例，2个基线。
  - 骨干LLM对比（表5）：7种基础模型，1个基线对比。
- **充分性**：实验覆盖了跨域、零样本、低资源、全监督等多种场景，并通过消融实验验证各组件贡献，实验设计全面且对比公平（相同评估指标、一致测试集）。结论稳健。

## 6. 主要结论与发现

- **跨域零样本**：ReasoningNER 8B平均F1=72.4，超越GPT-4（60.1）12.3个点，超越B2NER（64.6）7.8个点。
- **推理模型对比**：ReasoningNER 8B优于DeepSeek-R1 8B（70.2 vs 54.6），且超过DeepSeek-R1 32B（64.0），表明任务特定推理优化有效。
- **消融分析**：NER-CoT数据质量（+20.3 F1）、CoT推理（+2.4 F1）、RE阶段（+2.1 F1）均带来显著提升。
- **低资源**：在仅1%数据时F1=87.1%，比KnowCoder高7.9个点，证明推理有效地提升样本效率。
- **骨干无关性**：多种LLM上均取得显著提升，方法具有通用性。

## 7. 优点

- **范式创新**：首次将NER任务系统性地重构为显式推理过程，弥补了现有生成式NER缺乏推理机制的短板。
- **数据高效**：NER-CoT数据集仅45,787样本，远小于KnowCoder（4.59M）等，但性能更优。
- **泛化能力强**：在零样本、跨域、低资源场景下均大幅超越现有方法，尤其是零样本提升明显。
- **可解释性**：推理链使实体识别过程透明，便于人类验证和模型修正。
- **实验严谨**：多角度、多场景的评估设置，消融实验清晰展示各阶段贡献，对比公平。

## 8. 不足与局限

- **推理延迟**：生成CoT增加了推理时间，实际应用效率下降。论文承认这是主要局限。
- **算力细节缺失**：未报告具体GPU型号、数量及训练时长，影响可复现性。
- **GRPO训练规模较小**：RE阶段仅用4,703样本，可能未充分利用全部训练数据。
- **CoT数据集构建依赖多个LLM**（DeepSeek-R1、Qwen3 32B），质量受限于辅助模型能力。
- **低资源实验仅基于CoNLL03**，未在更多数据集上验证样本效率。
- **潜在偏差**：NER-CoT数据集主要基于Pile-NER，其领域分布可能影响泛化。

（完）
