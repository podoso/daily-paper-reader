---
title: Modal Dependency Parsing as Structured Prediction over Source-Cue Scope
title_zh: 模态依赖解析：基于源-线索作用域的结构化预测
authors: "Jayeol Chun, Nianwen Xue"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1362.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 事件中心的来源归因与模态作用域预测
tldr: 现有工作仅识别事件来源，忽略了线索表达和模态覆盖。本文提出结构化预测框架，利用大语言模型显式识别源-线索对及其作用域，从而决定事件级来源归因。该方法在源定位和事件决策上取得更精确的模态上下文建模。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1362/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 732, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1362/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1583, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1362/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1640, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1362/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 770, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1362/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 744, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1362/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 1039, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1362/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1613, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1362/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1483, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1362/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 562, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1362/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 1128, \"label\": \"Table\"}]"
motivation: 现有事件来源识别方法忽略线索表达和模态覆盖，导致归因不完整。
method: 提出基于大语言模型的结构化预测框架，识别源-线索对及其作用域。
result: 在事件级来源归因任务上优于仅识别来源的基线方法。
conclusion: 显式建模源-线索作用域可提升事件模态解析的准确性。
---

## Abstract
Modal dependency parsing-the task of identifying a semantic graph that represents who is responsible for an event-centered claim and with what degree of certainty-relies on recognizing source-introducing cues and correctly linking them to their associated content. However, prior work has largely focused on identifying sources only, treating cue expressions and their modal coverage as auxiliary signals. In this work, we propose a structured prediction framework that leverages large language models (LLMs) to explicitly identify source-cue pairs as well as their respective scope, which together define the modal contexts governing downstream source attribution for events. By concentrating learning at the source-cue level and constraining event-level decisions to a small, scope-defined candidate set, our top-down approach enables more efficient inference in long, event-rich documents. Experiments show this approach surpasses prior state-of-the-art results by 3 and 4% for English and Chinese datasets, respectively.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

模态依赖解析（Modal Dependency Parsing, MDP）旨在构建一种语义图，表示谁对事件中心的声明负责（来源），以及负责的确定性程度。传统方法主要集中于识别事件来源（conceiver），而将线索表达（cue，如“said”、“claimed”）及其模态覆盖范围视为辅助信号。这导致对模态上下文的建模不完整，尤其在嵌套归因和隐含来源的场景中表现不佳。本文立足于“先识别来源-线索对及其作用域，再约束事件级归因”的认知语言学直觉，提出一种结构化预测框架，显式建模源-线索-作用域三元组，从而提升整个MDP任务的准确性和鲁棒性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将MDP分解为两层结构化预测：  
  1）识别文档中的**源-线索-作用域**三元组（每个三元组由一个来源span、一个线索span和该线索引入的模态作用域span组成）；  
  2）根据作用域包含关系，将检测到的事件和来源节点**约束地**连接到最具体的覆盖作用域对应的来源节点，或默认连接到抽象节点AUTHOR/NULL。  
  这种自顶向下（top-down）的方式大幅缩小了事件级归因的候选空间。

- **关键技术细节**：
  - **银注释生成**：利用DeepSeek离线为原MDG语料添加缺失的线索和作用域span，得到`scope_min`（最紧边界）和`scope_max`（较宽边界）两种版本。
  - **监督微调（SFT）**：基于DeepSeek-R1-Distill-Qwen-7B模型，使用QLoRA参数高效微调，训练输入为token-indexed文本（每个句子前缀全局token索引），输出为结构化JSON，包含事件span、源-线索-作用域span以及目标（事件和来源）的归因边和标签。
  - **训练目标**：联合优化span预测损失和归因边预测损失，边预测受作用域包含约束引导，但仍作为学习目标以捕捉注释约定。
  - **跨语言统一**：单个模型同时处理英、中文，采用双语基座模型。

### 3. 实验设计：数据集 / 场景、基准、对比方法

- **数据集**：英、中文MDG语料库（Yao et al., 2021；Liu and Xue, 2023），均来自newswire领域。英文约6,825训练句，中文约3,187训练句。
- **基准（Baselines）**：
  - **Biaffine**：基于双仿射注意力的依赖解析器（Chun and Xue, 2025），使用双语翻译数据增强。
  - **Biaffine+Silver**：在Biaffine基础上加入银注释。
  - **Our Baseline**：相同LLM但直接生成完整MDG JSON，无结构化分解。
  - **Ours w/ Src-Cue-Scope**：本文提出的结构化预测方法。
- **评价指标**：事件识别（Event）、来源识别（Conceiver）、整体解析（Parsing）的micro F1分数。
- **结果**：
  - 英文测试集Parsing F1：Biaffine+Silver 73.5 → Ours **76.2**（+2.7%）
  - 中文测试集Parsing F1：Biaffine+Silver 67.3 → Ours **71.1**（+3.8%）
  - 在Conceiver识别上提升更明显，英文76.3%，中文88.0%。

### 4. 资源与算力

论文明确说明所有实验在**单张NVIDIA RTX A6000 GPU**上完成。采用QLoRA配置，可训练参数为161,480,704（约占总参数7,777,097,216的2.1%）。训练超参数包括：学习率2×10⁻⁵，4-bit量化，LoRA秩64，10个epoch，梯度累积4，批量大小4。但**未明确给出单次训练的具体时长**（如小时数）。

### 5. 实验数量与充分性

共进行以下比较实验：
- 四种方法（Biaffine、Biaffine+Silver、Our Baseline、Ours w/ Src-Cue-Scope）在英、中文dev/test上的结果（表2）。
- 对英文语料进行语料清理（去除媒体无关内容）后的额外实验（表3），观察清理效果。
- 作用域边界选择敏感性分析（`scope_min` vs `scope_max`），对比79%与75%的目标包含率。
- 跨语言对比分析（中文受益更大等定性分析）。

实验覆盖了主要消融（结构化分解、银注释、语料质量），并报告单次最佳运行结果。虽然未列出多轮平均或方差，但对比基线均为公开SOTA，设置公平客观。整体充分性较好。

### 6. 论文的主要结论与发现

1. 显式建模源-线索-作用域可显著提升MDP性能，与仅预测来源的方法相比，英中Parsing F1分别提高3%和4%。
2. 中文受益更大，原因在于中文更依赖隐式归因，作用域建模有助于揭示隐含的语篇级归因。
3. 语料清理（去除标题、图片说明等）主要改善归因一致性，对节点识别影响较小。
4. 作用域选择偏好紧边界（`scope_min`）能更好地对齐黄金归因。
5. 直接生成完整MDG JSON的基线表现最差，说明无约束序列生成不适合图结构输出。

### 7. 优点：方法或实验设计上的亮点

- **新颖的自顶向下分解**：将复杂图预测简化为先识别作用域再约束归因，符合人类认知处理模式，降低搜索空间。
- **跨语言统一建模**：单一模型同时处理英语和汉语，无需语言特定架构。
- **银注释增强**：利用大型LLM为原语料补充缺失的线索和作用域，提升监督信号密度。
- **实验设计合理**：对比了现有SOTA（Biaffine）和公平的LLM基线，并做了语料质量控制和作用域敏感性分析，结论可信。
- **参数高效微调**：仅更新2.1%参数即达到SOTA，计算开销可控。

### 8. 不足与局限

- **领域限制**：仅使用newswire语料，未验证其他领域（如社交媒体、对话、医学）的泛化能力。
- **语种覆盖**：仅英、中文，未测试其他语言（如德语、日语），跨语言泛化性未知。
- **输入依赖性**：依赖预tokenization和句子分段，实际部署需预处理管线，误差可能传播。
- **作用域连续性假设**：假设模态作用域为连续span，无法处理中断引用（如“The plan,” he said, “will fail.”），虽声称可被吸收但未定量分析。
- **银注释质量风险**：从DeepSeek生成的银注释可能引入噪声，未进行人工校验或误差传播分析。
- **实验统计**：仅报告单次运行最佳结果，缺乏多次运行的均值和方差，不确定性未量化。

（完）
