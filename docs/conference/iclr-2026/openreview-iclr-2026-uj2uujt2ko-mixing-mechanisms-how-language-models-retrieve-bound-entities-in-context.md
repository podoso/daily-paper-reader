---
title: "Mixing Mechanisms: How Language Models Retrieve Bound Entities In-Context"
title_zh: 混合机制：语言模型如何检索上下文绑定的实体
authors: "Yoav Gur-Arieh, Mor Geva, Atticus Geiger"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=UJ2UUjT2ko"
tags: ["query:llm"]
score: 5.0
evidence: 研究语言模型如何检索上下文绑定的实体
tldr: 本文研究语言模型在上下文推理中如何检索绑定的实体。发现当上下文中的绑定实体数量增加时，基于位置的检索机制变得不可靠，模型会补充使用基于内容的机制。该工作揭示了语言模型内部工作机制，但对实际方法贡献有限。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1275, \"height\": 1255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1427, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1435, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1441, \"height\": 348, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 590, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1424, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1397, \"height\": 742, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1409, \"height\": 1170, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1409, \"height\": 1168, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1427, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1419, \"height\": 1089, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1427, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1415, \"height\": 872, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1436, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1437, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1438, \"height\": 595, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1436, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1398, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1408, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1376, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1430, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1427, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1402, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1439, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1439, \"height\": 636, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1442, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1412, \"height\": 583, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1401, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1443, \"height\": 665, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1400, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uj2uujt2ko/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 1435, \"height\": 610, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 776, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1453, \"height\": 1484, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 1268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1458, \"height\": 813, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1458, \"height\": 850, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1458, \"height\": 852, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uj2uujt2ko/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1460, \"height\": 849, \"label\": \"Table\"}]"
motivation: 探索语言模型在上下文推理中绑定并检索实体的具体机制，特别是处理大量绑定实体时的局限性。
method: 通过实验分析语言模型在检索绑定实体时采用的机制，包括位置机制和内容机制。
result: 发现位置机制在少量实体时有效，但在实体增多时变得不可靠，模型转而依赖内容机制。
conclusion: 揭示了语言模型在复杂上下文中的实体检索机制，为理解其推理过程提供了新视角。
---

## Abstract
A key component of in-context reasoning is the ability of language models (LMs) to bind entities for later retrieval.
For example, an LM might represent *Ann loves pie* by binding *Ann* to *pie*, allowing it to later retrieve *Ann* when asked *Who loves pie?* 
Prior research on short lists of bound entities found strong evidence that LMs implement such retrieval 
via a **positional mechanism**, where *Ann* is retrieved based on its position in context.
In this work, we find that this mechanism generalizes poorly to more complex settings; as the number of bound entities in context increases, the positional mechanism becomes noisy and unreliable in middle positions.
To compensate for this, we find that LMs supplement the positional mechanism with a **lexical mechanism** (retrieving *Ann* using its bound counterpart *pie*) and a **reflexive mechanism** (retrieving *Ann* through a direct pointer). 
Through extensive experiments on nine models and ten binding tasks, we uncover a consistent pattern in how LMs mix these mechanisms to drive model behavior.
We leverage these insights to develop a causal model combining all three mechanisms that estimates next token distributions with 95\% agreement.
Finally, we show that our model generalizes to substantially longer inputs of open-ended text interleaved with entity groups, further demonstrating the robustness of our findings in more natural settings.
Overall, our study establishes a more complete picture of how LMs bind and retrieve entities in-context.

---

## 论文详细总结（自动生成）

### 论文详细中文总结

#### 1. 论文的核心问题与整体含义
- **研究动机**：语言模型（LM）在上下文推理中需要绑定实体（如“Ann loves pie”中绑定 Ann 和 pie）以便后续检索（如回答“Who loves pie?”）。先前研究认为 LM 主要依赖**位置机制**（根据实体在上下文中的位置进行检索），但该机制在实体数量增多时表现不佳，尤其对中间位置的实体检索不可靠。
- **整体含义**：本文旨在揭示 LM 在复杂上下文（更多绑定实体）中如何实现实体检索，发现 LM 实际混合使用了三种机制：位置机制、**词汇机制**（通过绑定对象实体检索，如用 pie 检索 Ann）和**反射机制**（通过直接指针检索自身实体）。该发现修正了先前单一位置机制的观点，为理解 LM 的长上下文推理能力提供了更完整的因果解释。

#### 2. 论文提出的方法论
- **核心思想**：通过机制解剖（mechanistic interpretability）和因果抽象（causal abstraction），将 LM 的实体检索行为建模为三种机制的加权混合，并学习各机制的权重与分布参数。
- **关键技术细节**：
  - **三类机制定义**：
    - 位置机制 P：根据查询实体的组索引（群组位置）检索目标实体。
    - 词汇机制 L：根据查询实体的标识（如单词本身）检索其绑定伙伴。
    - 反射机制 R：通过直接指向目标实体的指针进行检索（指针被复制到绑定实体，再传递到最后一个 token）。
  - **因果模型 M**：将机制表示为可学习参数，用 logits 线性组合模拟 LM 的下一个 token 概率分布。公式为：
    - `Yi = w_pos * N(i | iP, σ(iP)^2) + w_lex[iL] * 1{i = iL} + w_ref[iR] * 1{i = iR}`
    - 其中 `σ(iP) = α(iP/n)^2 + β(iP/n) + γ`，`w_pos`、`w_lex`、`w_ref`、`α`、`β`、`γ` 从数据中学习。
  - **反事实干预设计**：构造成对的原始输入与反事实输入，使三种机制在干预下产生不同预测，从而分离并测量各机制的影响。例如，通过交换绑定矩阵中的实体或位置，使位置、词汇、反射机制分别指向不同的实体。
  - **干预位置**：通过逐层 patching（替换残差流向量）定位到最后一层的最后一个 token 位置（累积绑定信息的层），称为 `ℓ`（不同模型不同）。

#### 3. 实验设计
- **数据集与场景**：
  - 设计了 10 个模板化绑定任务（如 `boxes`、`music`、`filling liquids` 等），每个任务包含实体角色集（如人名、物品名）、实体组（如 `(Pete, jam)`）、模板（如“Pete loves jam”）。
  - 实体组数量 `n` 从 3 到 20 变化；组内实体数 `m` 为 2 或 3。
  - 还测试了含填充句（free-form filler sentences）的更自然文本，以及随机语言变体任务。
- **基准方法与对比**：
  - 对比方法：纯位置机制（prevailing view）、统一分布（uniform）、因果模型的各种消融版本（去除某类机制、将位置机制建模为 one-hot 而非高斯等）。
  - 评估指标：Jensen–Shannon 相似度（JSS）、KL 散度。
- **对比方法**：所有对比均在相同反事实干预设置下进行，包括消融实验和 oracle 上界（用实际 logits 代替位置高斯）。

#### 4. 资源与算力
- 论文未明确说明使用的 GPU 型号、数量及训练时长。仅提及在多种模型（2B–72B 参数）上运行实验，但未提供算力细节。

#### 5. 实验数量与充分性
- **实验数量**：相当充分。涵盖：
  - 9 个不同规模的模型（Gemma-2、Qwen2.5、Llama-3.1 家族，2B–72B）。
  - 10 个绑定任务，每个任务测试不同 `tentity`（目标位置）和 `n`。
  - 主要交换干预实验在所有模型和任务上重复，并使用多种反事实数据集。
  - 消融实验：训练并比较了 9 种因果模型变体（含全模型、去某机制、替换分布形式等）。
  - 附加实验：注意力 knockout、实体不存在性检验、填充文本、语言变体、正交实验（机制同意、移除目标实体等）。
- **充分性与公平性**：实验设计系统全面，覆盖了不同模型家族、规模、任务复杂度、上下文长度和噪声水平；使用了标准化指标（JSS、KL）；所有干预和对比均在同一数据生成流程下进行，结果一致且可复现。结论稳健。

#### 6. 论文的主要结论与发现
- **位置机制仅在首尾位置有效**：当实体组数量增加（如 `n=20`），位置机制对中间位置的预测变得模糊、不可靠。其 logit 分布从首尾的尖锐高斯变成宽广弥散的分布。
- **词汇机制和反射机制补充位置机制**：在中间位置，位置信号弱时，词汇机制（尤其当目标实体在组末尾 `tentity=3` 时）和反射机制（目标在组首 `tentity=1` 时）发挥主导作用；当目标在中间 `tentity=2` 时两者混合。
- **反射机制是一个独立机制**：通过将反事实答案实体移除（不在原始输入中），证实 patching 的是指向实体的指针而非答案本身，且模型无法“无视”指针（即不能直接输出答案实体），验证了反射指针的存在。
- **因果模型高精度匹配 LM 行为**：提出的混合模型在 20 个实体组、3 个目标位置上达到 0.95 JSS（接近 oracle 0.96），远超纯位置机制（0.44）和均匀基线（0.50）。
- **推广性**：填充自然文本后，模型行为模式保持不变（但随着填充增多，词汇机制减弱，位置机制增强但更弥散，部分解释了“lost-in-the-middle”效应）。不同语言变体下结论一致。
- **机制混合受目标位置调节**：位置机制与词汇/反射机制之间存在竞争性协同：当词汇与位置索引接近时词汇增强；当词汇与反射接近时词汇被抑制。

#### 7. 优点
- **方法创新**：首次系统提出并验证了三种实体检索机制（位置、词汇、反射），修正了“单一位置机制”的主流观点。
- **实验设计严谨**：利用反事实干预和因果抽象方法论，精心设计配对数据以分离机制；通过“实体不存在”实验、注意力 knockout 等辅助验证反射机制，排除替代解释。
- **规模与多样性**：覆盖 9 个不同规模模型、10 个任务、多种上下文长度和噪声，结论具有高度泛化性。
- **可复现性**：提供了代码和数据，详细描述了任务生成和模型训练的超参数。
- **工程价值**：混合因果模型能够高精度模拟 LM 行为，可应用于提升长上下文推理性能。

#### 8. 不足与局限
- **任务模板化**：所有绑定任务均为模板生成的自然语言，与真实世界中的自由文本仍有差距，可能遗漏其他潜在机制。
- **模型范围**：虽然测试了 9 个模型，但仅涵盖 3 个架构家族（Gemma、Qwen、Llama），未探索编码器-解码器或非 transformer 架构。
- **未报告算力消耗**：未提供 GPU 型号、数量、训练时间，不利于成本估算和复现。
- **机械主义分析局限性**：因果模型假设机制可完美分离，但实际中可能存在依赖高维交互的微小额外机制（如“mixed”效应被归因于位置噪声，但可能包含更复杂的混合）。
- **实际应用限制**：实验仅在受控任务上进行，未在开放领域问答或对话系统中验证，对“lost-in-the-middle”的因果解释仅基于填充实验，需要更多直接证据。

（完）
