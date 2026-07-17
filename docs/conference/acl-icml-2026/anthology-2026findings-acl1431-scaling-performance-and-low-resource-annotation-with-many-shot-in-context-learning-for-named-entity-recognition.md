---
title: Scaling Performance and Low-Resource Annotation with Many-Shot In-Context Learning for Named Entity Recognition
title_zh: 通过多示例上下文学习扩展命名实体识别的性能与低资源标注
authors: "Qi Zhang, Fangping Lan, Cornelia Caragea, Longin Jan Latecki, Eduard Dragut"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1431.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 多示例上下文学习用于命名实体识别
tldr: 针对命名实体识别任务，该论文深入研究了多示例上下文学习的扩展效果，证明将演示数量扩大到数百个可以显著提升性能，并有效用于低资源标注和数据精炼，为NER提供了一种无需微调的强大替代方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 780, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1660, \"height\": 266, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1635, \"height\": 493, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1638, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 751, \"height\": 932, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 754, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 747, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 750, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 707, \"height\": 1373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1431/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 716, \"height\": 825, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1431/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1492, \"height\": 1103, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1431/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 781, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1431/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 993, \"height\": 2642, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1431/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1600, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1431/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 176, \"label\": \"Table\"}]"
motivation: 先前研究表明LLM在NER上仍落后于微调模型，且ICL研究局限于少样本场景。
method: 系统研究多示例ICL在NER上的扩展性，并利用其进行数据标注和精炼。
result: 多示例ICL在NER上达到竞争性能，并有效用于低资源标注。
conclusion: 多示例ICL是NER的一种高效且无需训练的新范式。
---

## Abstract
In-context learning (ICL) with large language models (LLMs) has emerged as a powerful alternative to fine-tuning for Named Entity Recognition (NER), achieving strong performance with minimal annotation and no additional training. However, prior work has shown that despite their adaptability, LLMs still lag behind fully supervised models such as fine-tuned BERT in structured tasks like NER. While existing studies on ICL for NER have mainly explored few-shot settings, the potential of scaling to hundreds of demonstrations has not been thoroughly investigated. To address this gap, we conduct a comprehensive investigation of many-shot ICL for NER and further explore its effectiveness in annotating and refining data for low-resource NER tasks. Specifically, we evaluate various LLMs across multiple domains using hundreds of ICL examples and then assess the feasibility of using many-shot ICL as a data annotation framework. Our experiments demonstrate that: (1) scaling to hundreds of in-context examples enables LLMs to match or even surpass the performance of fully supervised BERT models; and (2) using about one hundred human-labeled examples as demonstrations, many-shot in-context annotation can generate high-quality labeled data, leading to approximately 10% absolute F1 improvement over existing state-of-the-art approaches when used to fine-tune BERT on low-resource NER.

---

## 论文详细总结（自动生成）

# 论文总结：多示例上下文学习用于命名实体识别的性能扩展与低资源标注

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：尽管大语言模型（LLM）通过上下文学习（ICL）在命名实体识别（NER）上展现出无需微调的潜力，但先前研究表明，在诸如 NER 这样的结构化任务中，LLM 的性能仍落后于全监督的小模型（如微调 BERT）。现有的 ICL 研究主要聚焦于少样本（few-shot）场景，而对于扩展至数百个演示示例（many-shot ICL）的潜力尚未进行系统性探索。
- **整体含义**：本文旨在填补这一空白，首次系统研究多示例 ICL 在 NER 上的扩展效果，并利用其进行低资源数据标注与精炼，从而为 NER 提供一种高效、无需训练的替代范式，降低对大规模人工标注的依赖。

## 2. 论文提出的方法论

- **核心思想**：利用现代 LLM 的长上下文能力，将数百个人工标注示例作为上下文演示，通过 ICL 直接对测试数据进行推理（多示例 ICL），或者作为离线标注器为未标注数据生成高质量标签（In-Context Annotation, ICA），再使用这些标签训练高效的小模型（如 BERT）。
- **关键技术细节**：
  - **多示例 ICL 设置**：使用 XML 风格的标签格式（如 `<entity type="...">...</entity>`）来表示实体边界和类型，替代传统的 BIO 格式，以提高 LLM 的边界敏感度。演示选择策略包括**随机采样**（固定演示集）和**检索式**（基于 BM25 为每个测试样本动态选择最相似的演示）。
  - **ICA 框架**：给定少量（如 100 条）人工标注示例，将其作为固定演示，用 LLM 对 2k 条未标注句子进行一次性标注（离线）。为提升标注质量，引入三种精炼策略：
    - **自一致性（Self-consistency）**：对低置信度样本进行多次采样（改变演示顺序），通过多数投票聚合实体 span 和类型。
    - **自修正（Self-correction）**：通过第二个提示让 LLM 回顾并修正自己的标注，使用少量错误修正示例作为少样本演示。
    - **错误感知自精炼（Error-Aware Refinement, EAR）**：将修正任务分解为三个独立步骤（假阳性、遗漏、类型错误），每个步骤使用专用提示，按序应用。这种分解避免了开放式修正的模糊性。
  - **标注置信度**：通过计算生成实体 token 的平均对数概率来评估每条标注的置信度，仅对底部 50% 的低置信度样本应用精炼。
- **流程**：① 收集少量人工种子标注 → ② 用 LLM 标注大量未标注数据 → ③ 可选精炼 → ④ 将标注转换为 BIO 格式 → ⑤ 微调 BERT 模型 → ⑥ 部署小模型进行推理。

## 3. 实验设计

- **数据集**：
  - **多示例 ICL 评估**：MIT-Restaurant（8 种实体）、MIT-Movie（12 种）、WNUT2017（社交媒体噪声文本）、CoNLL2003（新闻领域标准 NER）。
  - **低资源标注评估（ICA）**：CrossNER 基准，包含五个领域：AI、Literature、Music、Politics、Science。每个领域仅提供 100 或 200 个人工标注训练样本。
- **Benchmark**：对于 ICA，对比了三大类方法：
  - **传统数据增强**：DAGA、NERDA、GPDA。
  - **LLM 数据增强**：ProgGen。
  - **SOTA 低资源/跨域 NER 方法**：LST-NER、DoSEA、DTrans-SMix、DH-GAT、B2NER、GLiNER、Three-KPNs、PromptNER、IF-WRANER、DTrans-MPrompt 等。
  - **直接 ICL 推理**：零样本 ICL（ICL-ZS）和 100 样本 ICL（ICL-MS），以及带精炼的 ICL-MS。
- **对比方式**：所有 ICA 变体（ICA、ICA+自一致性、ICA+自修正、ICA+EAR）与基线在 CrossNER 五个领域上报告平均 micro-F1（精确 span 匹配），使用 5 次不同随机种子的平均值和标准差。
- **LLM 评估**：评估了 GPT-4o、DeepSeekV3、Qwen2.5（7B/32B/72B）、LLaMA3.1（8B/70B）共 7 种模型，涵盖闭源和开源。

## 4. 资源与算力

- 多示例 ICL 实验：开源模型（Qwen、LLaMA）使用 vLLM 部署在 **4 块 A100 GPU** 上；闭源模型（DeepSeekV3、GPT-4o）通过官方 API 调用。
- BERT 微调：使用单张 A100 GPU，PyTorch 2.7.0，训练超参数为学习率 1e-5、batch size 16、5 epochs。在 CoNLL03 上每个 epoch 约 **34 秒**。
- 文中未详细说明总计算量（如 GPU 小时数），仅描述了硬件配置和单次训练时长。

## 5. 实验数量与充分性

- **实验组数**：论文包含大量实验：
  - 多示例 ICL：4 个数据集 × 7 种模型 × 2 种演示选择策略 × 约 11 个示例数量梯度（0~500）= 超过 600 组性能记录。
  - ICA 框架：5 个低资源领域 × 4 种 ICA 变体 × 5 次随机种子 × 约 15 种对比基线 = 大量消融与对比。
  - 附加分析：数据量缩放实验（0.5k~5k）、种子集大小实验（0~300）、LLM 选择比较等。
- **充分性与公平性**：实验充分覆盖多种场景和模型，结果以平均和标准差报告，对比基线采用原论文结果或公开最佳配置（如 ProgGen、GLiNER）。基线包括直接 ICL 推理、传统数据增强和最新 SOTA，对比公平。消融实验验证了每种精炼策略的贡献。此外，还进行了成本分析（附录 B.5）。

## 6. 论文的主要结论与发现

1. **多示例 ICL 可匹配或超越全监督模型**：在四个数据集上，当演示数量达到约 100~500 时，LLM 的性能可与微调在全部训练集上的 BERT 相当甚至更优，且随机采样与检索式采样的差距随演示数量增加而缩小。
2. **ICA 框架显著提升低资源 NER**：使用 100 个人工标注演示，ICA 生成的 2k 标注数据训练的 BERT 模型，在 CrossNER 上平均 F1 达到 84.80，比之前 SOTA（DTrans-MPrompt）提升约 10 个绝对百分点。
3. **EAR 精炼策略最佳**：错误感知自精炼（EAR）在所有领域上一致优于自一致性和自修正，平均提升 1.79 F1 点。EAR 通过分解错误类型、提供针对性示例，有效修正常见 NER 错误（假阳性、遗漏、类型错误）。
4. **种子集规模影响**：约 75~100 个人工标注示例即可达到 ICA 性能饱和，更多的种子收益递减。
5. **LLM 选择至关重要**：大型闭源模型（GPT-4o）和强开源模型（DeepSeekV3、Qwen-72B）显著优于小模型（Qwen-7B），但开源模型在足够大时可接近闭源水平。

## 7. 优点

- **首次系统研究**：首次全面探索多示例 ICL 在 NER 上的扩展行为，揭示了单调提升趋势。
- **实用框架 ICA**：将 LLM 用作离线标注器，解耦 LLM 推理与下游部署，既利用了 LLM 的泛化能力，又通过小模型实现低成本推理，具有实际应用价值。
- **精炼策略设计精巧**：EAR 方法针对 NER 常见错误设计，分解提示、提供针对性示例，避免了通用自修正的过度纠正问题（如 sycophancy），实验证明有效。
- **实验覆盖全面**：涵盖多领域、多模型、多策略，消融和附加分析深入，结论可靠。
- **可复现性**：公开代码和数据。

## 8. 不足与局限

- **仍需一定人工标注**：框架依然需要约 100 条高质量种子标签，对于完全零资源场景不适用。
- **计算开销**：LLM 标注过程虽然离线，但重复推理（特别是精炼阶段）仍然需要较多算力和 API 成本；精炼仅对低置信度样本应用，部分缓解但未消除。
- **可解释性差**：ICL 的内部工作机制不透明，难以调试或审计模型在特定用例中的行为。
- **实验覆盖面有限**：仅使用英语 NER 数据，未评估多语言、嵌套实体、不连续实体等更复杂标注方案；领域仅限于新闻、社交媒体、学术等领域。
- **潜在偏差风险**：LLM 标注可能继承预训练数据中的偏见或对特定表面模式（如大小写）过度敏感，文中虽提到但未深入分析。
- **精炼策略依赖人工设计**：EAR 的分解和示例构建需要领域知识和人工检查，自动化程度有限。

（完）
