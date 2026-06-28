---
title: "LLaVA-MS-PIT: Multi-Modal Schema-Guided Progressive Instruction Tuning for Multi-Modal Event Extraction"
title_zh: LLaVA-MS-PIT：多模态模式引导的渐进式指令微调用于多模态事件抽取
authors: "Hui Zhang, Po Hu, Wei Emma Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40770/44731"
tags: ["query:ie"]
score: 10.0
evidence: 多模态事件抽取，结合模式引导和指令微调
tldr: 针对现有跨模态事件抽取模型缺乏显式事件模式指导、多模态对齐策略粗糙且依赖异构不匹配数据集的问题，本文提出LLaVA-MS-PIT框架。该框架在多模态事件抽取前显式注入结构化多模态事件模式知识，通过渐进式指令微调实现对齐，显著提升了跨文本和视觉模态的事件抽取效果。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有跨模态事件抽取模型缺乏事件模式指导，多模态对齐不足且数据集异质错配。
method: 设计多模态模式引导的渐进式指令微调，显式注入结构化事件模式知识。
result: 在多个多模态事件抽取基准上取得最优性能。
conclusion: 显式引入事件模式知识能有效提升跨模态事件抽取的准确性和鲁棒性。
---

## Abstract
The proliferation of multi-modal data on the internet has intensified the need for structured event understanding across textual and visual modalities. However, existing multi-modal event extraction models suffer from three major limitations: the absence of explicit event schema guidance, coarse-grained multi-modal alignment strategies, and reliance on heterogeneous, misaligned multi-modal training datasets. To address these issues, we propose LLaVA-MS-PIT, a Multi-modal Schema-Guided Progressive Instruction Tuning Framework that explicitly injects structured multi-modal event schema knowledge into the model before event extraction. Specifically, we introduce the textual event schema to establish the model’s prior knowledge of event concepts and enhance its ability to reason about event structures, while the visual event schema is employed to bridge the representation gap between textual and visual modalities at the event level, enabling unified and semantically aligned event representations across modalities. Moreover, to alleviate data scarcity and modality misalignment inherent in current benchmarks, we construct imSitu-MEE, a high-quality multi-modal parallel dataset generated and annotated through schema-guided procedures. Extensive experiments demonstrate that LLaVA-MS-PIT achieves competitive performance on multi-modal event extraction benchmarks, underscoring the effectiveness and necessity of schema-guided progressive instruction tuning.

---

## 论文详细总结（自动生成）

# LLaVA-MS-PIT：多模态模式引导的渐进式指令微调用于多模态事件抽取

## 1. 论文的核心问题与整体含义（研究动机和背景）

随着互联网上多模态数据的激增，从文本和图像中提取结构化事件信息（即多模态事件抽取，MEE）变得日益重要。然而，现有方法存在三大瓶颈：
- **缺乏显式事件模式（Event Schema）指导**：模型无法内化事件的语义结构和跨模态一致性约束。
- **粗粒度的多模态对齐策略**：仅进行整体特征对齐，缺乏事件级别的语义对齐。
- **依赖异构且标注不对齐的数据集**：如ACE 2005（纯文本）、imSitu（图像）与VOA（字幕）拼接使用，存在语义鸿沟、跨模态漂移和训练冗余。

本文旨在通过显式注入结构化多模态事件模式知识，并采用渐进式指令微调，来解决上述问题，从而提升多模态事件抽取的准确性和鲁棒性。

## 2. 论文提出的方法论

### 核心思想
在事件抽取之前，先让模型通过两阶段渐进式微调学习并内化多模态事件模式知识（文本模式+视觉模式），再执行事件抽取任务。同时，通过模式引导方式构建高质量平行多模态数据集，缓解数据稀缺与模态错配。

### 关键技术细节
#### （1）多模态事件模式构建
- **文本事件模式（Textual Event Schema, TES）**：将静态的事件模式转化为动态的多轮渐进式问答对，模拟人类认知过程，包括四个子任务：
  - 事件检测（识别事件类型）
  - 事件类型分析（理解上下文语义触发原因）
  - 事件论元角色填充（定位并分类论元）
  - 事件结构推理（整合信息，推断完整结构）
- **视觉事件模式（Visual Event Schema, VES）**：将图像分解为与事件语义同构的结构化表示，包括：
  - 核心视觉实体（O）
  - 实体属性（A_attr）与动作（A_action）
  - 实体间关系（R）
  - 场景上下文（C）
  - 形式化定义：VES = {O, {A_attr(oi), A_action(oi)}, R, C}

#### （2）两阶段渐进式微调框架
- **第一阶段：事件模式感知微调（Event Schema-Aware Fine-tuning）**
  - 子阶段1（文本模式微调）：冻结视觉编码器和投影器，仅用LoRA微调语言模型，目标是最大化 log p(atext | x, stext)。使用PESD指令数据。
  - 子阶段2（视觉模式对齐微调）：仅更新多模态投影器，将视觉特征映射到事件语义空间，最大化 log p(aimg | I, simg)。
- **第二阶段：模式引导的事件抽取微调（Schema-Guided Event Extraction Instruction Tuning）**
  - 基于构建的平行数据集imSitu-MEE，设计端到端抽取指令，联合微调语言模型和投影器，模式作为隐式约束。

#### （3）模式引导的数据集构建（imSitu-MEE）
- **图像筛选**：采用“GPT-4o初步过滤 + 人工审核”两阶段验证，保留与ACE 2005事件类型高度匹配的图像（约53%被丢弃），得到imSitu-Clean。
- **文本生成**：利用GPT-4o，以事件模式和ACE 2005示例作为few-shot提示，为图像生成平行文本描述（imSitu-Clean-Text）。
- **自动标注**：通过模式感知提示，使用GPT-4o自动标注事件类型、触发词和论元角色，最终构建平行多模态数据集imSitu-MEE。

## 3. 实验设计

### 数据集
- **训练数据**：ACE 2005（文本事件抽取）、imSitu-Clean（精炼视觉事件）、imSitu-MEE（模式引导构建的多模态平行数据集）。
- **评估基准**：M²E2（Multi-Modal Event Extraction benchmark，来自Li et al. 2020）。

### 评价指标
- 文本事件抽取：严格模式（事件类型+触发词精确匹配）和宽松模式（仅类型和论元，放松触发词约束）
- 视觉事件抽取：事件类型+论元的准确预测
- 使用Precision、Recall、F1

### 对比方法
WASE_obj、CLIP-Event、UNICL、MGIM、CAMEL、MMUTF、UMIE、X-MTL（8种典型方法）

### 实现细节
- 基础模型：LLaVA-1.5 (7B)
- 训练参数：Schema感知微调时，语言模型学习率2e-4，投影器学习率2e-5，3个epoch，batch size 32；事件抽取微调相同学习率和batch size，1个epoch
- 硬件：NVIDIA A800 GPU（未明确数量）

## 4. 资源与算力

论文提到所有实验在NVIDIA A800 GPU上进行，但**未明确说明所使用的GPU数量**以及具体训练时长。仅给出了学习率、epoch数和batch size等超参数。因此无法精确评估算力消耗，但可以推断使用的是单卡或少量A800 GPU（通常LLaVA-1.5 7B可在单张A800上微调）。

## 5. 实验数量与充分性

论文进行了以下实验：
- **主实验结果**（表1）：在M²E2基准上，对比8种baseline，报告文本/视觉/多模态的事件检测和论元抽取的P/R/F1。
- **消融实验**（表2）：对比4种设置：原始数据微调（ODT）、清洗数据微调（CDT）、仅视觉模式（CDT-VES）、仅文本模式（CDT-TES），验证各模块贡献。
- **进一步分析**（表3、图5）：在ACE 2005和M²E2上进行跨数据集对比，分析对文本模式注入的深入影响，包括匹配/金标/预测数量差异。

**评估**：实验设计较为充分，覆盖了主流baseline、消融分析和跨数据集泛化验证。但存在以下可改进之处：
- 未报告方差或多次运行结果，缺乏统计显著性检验。
- 缺乏在更多样化的多模态事件抽取数据集上的验证（如仅使用M²E2一个基准）。
- 消融实验中CDT-VES和CDT-TES的结果差异不大，可能需要更细粒度的分析。
总体而言，实验基本客观公平，但充分性可进一步通过更多基准和统计增强。

## 6. 论文的主要结论与发现

1. LLaVA-MS-PIT在M²E2基准上取得**最优性能**，在文本事件检测上F1达69.6（宽松模式），视觉事件检测达72.3，多模态事件检测达87.5，显著超越先前最优模型X-MTL（分别提升13.0、0.6、21.3个F1点）。
2. 文本事件模式注入显著提升模型对复杂事件-论元关系的识别能力（ACE 2005上论元F1从55.5提升到58.0）。
3. 视觉事件模式有助于实现事件级跨模态对齐，提升视觉论元抽取（F1从51.9提升到55.7）。
4. 模式引导的数据清洗和构造策略有效降低了imSitu数据集中的噪声，提升了训练数据质量。
5. 模型倾向于预测更多的事件和论元（约1.5-2倍于金标），导致精确率偏低，但召回率更高，且能发现金标中遗漏的合理事件。

## 7. 优点

- **方法论创新**：首次将显式多模态事件模式（文本+视觉）作为知识注入到LLM中，并通过渐进式微调实现结构化学习，具有认知启发意义。
- **数据构造策略**：采用“GPT-4o+人工审核”两阶段清洗和模式引导的文本生成，有效解决了现有数据集不对齐、噪声大的问题，生成的imSitu-MEE为社区提供了高质量基准。
- **实验设计全面**：包含主对比、消融、跨数据集分析，验证了模式知识注入的有效性。
- **代码开源**：提供GitHub代码，促进可复现性。

## 8. 不足与局限

- **计算资源描述不充分**：未注明GPU数量、训练时长，难以评估实际资源需求。
- **基准覆盖有限**：仅在M²E2一个基准上进行评估，缺乏在更多多模态事件抽取数据集（如新发布的）上的验证。
- **缺乏统计显著性**：未报告多次运行的标准差或统计检验结果，无法判断性能提升是否显著。
- **论元抽取精确率偏低**：模型过度预测导致精确率不高，对实际应用中的高精度要求（如安全监控）可能不满足。
- **依赖大规模LLM和GPT-4o**：构建数据时使用GPT-4o产生成本，且基础模型LLaVA-1.5 7B参数规模较大，部署资源需求高。
- **潜在的知识注入偏差**：文本模式采用人工设计的渐进式问答，可能引入设计者的主观偏差；视觉模式定义的元素是否覆盖所有事件类型有待验证。
- **未讨论模型在零样本或跨域场景下的表现**：仅专注于有监督微调，泛化能力评估不足。

（完）
