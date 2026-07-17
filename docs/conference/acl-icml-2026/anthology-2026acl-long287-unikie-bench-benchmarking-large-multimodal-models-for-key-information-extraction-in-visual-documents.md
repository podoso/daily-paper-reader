---
title: "UNIKIE-BENCH: Benchmarking Large Multimodal Models for Key Information Extraction in Visual Documents"
title_zh: UNIKIE-BENCH：面向视觉文档中关键信息抽取的大型多模态模型基准测试
authors: "Yifan Ji, Zhipeng Xu, Zhenghao Liu (刘正皓), Zulong Chen, Qian Zhang, ZhiBo Yang, Junyang Lin, Yu Gu (谷峪), Ge Yu (于戈), Maosong Sun (孙茂松)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.287.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 使用大型多模态模型的视觉文档关键信息抽取基准
tldr: 该论文提出UNIKIE-BENCH基准测试，用于全面评估大型多模态模型在视觉文档关键信息抽取上的能力。基准包含约束类别和开放类别两大任务，覆盖多种真实应用场景，为多模态信息抽取研究提供了标准化评估平台。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1630, \"height\": 902, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 778, \"height\": 986, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1646, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1520, \"height\": 1169, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1525, \"height\": 1143, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 887, \"height\": 1125, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 790, \"height\": 1121, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 865, \"height\": 1114, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 900, \"height\": 1101, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 673, \"height\": 1099, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.287/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 628, \"height\": 1120, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 815, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1554, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1660, \"height\": 797, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1396, \"height\": 830, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1496, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.287/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1553, \"height\": 776, \"label\": \"Table\"}]"
motivation: 现有视觉文档关键信息抽取缺乏统一的基准评估方法。
method: 构建包含约束和开放类别的多模态关键信息抽取基准。
result: 提供了大型多模态模型在视觉文档KIE上的系统评估。
conclusion: UNIKIE-BENCH推动了多模态信息抽取的评估标准化。
---

## Abstract
Key Information Extraction (KIE) from real-world documents remains challenging due to substantial variations in layout structures, visual quality, and task-specific information requirements. Recent Large Multimodal Models (LMMs) have shown promising potential for performing end-to-end KIE directly from document images. To enable a comprehensive and systematic evaluation across realistic and diverse application scenarios, we introduce UNIKIE-BENCH, a unified benchmark designed to rigorously evaluate the KIE capabilities of LMMs. UNIKIE-BENCH consists of two complementary tracks: a constrained-category KIE track with scenario-predefined schemas that reflect practical application needs, and an open-category KIE track that extracts any key information that is explicitly present in the document. Experiments on 15 state-of-the-art LMMs reveal substantial performance degradation under diverse schema definitions, long-tail key fields, and complex layouts, along with pronounced performance disparities across different document types and scenarios. These findings underscore persistent challenges in grounding accuracy and layout-aware reasoning for LMM-based KIE. All codes and datasets are available at https://github.com/NEUIR/UNIKIE-BENCH.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：从真实世界视觉文档中提取关键信息（Key Information Extraction, KIE）面临布局结构、视觉质量和任务特定信息需求的高度变化，传统方法依赖OCR和模块化流水线，误差易累积。大型多模态模型（LMMs）展现出端到端KIE潜力，但现有基准测试存在评估标准不统一、场景单一、缺乏对开放类别和约束类别同时覆盖等问题，难以系统衡量LMMs的真实KIE能力。
- **动机**：构建一个统一、全面的基准，支持在不同应用场景、文档类型和语言下对LMMs进行系统和公平的KIE能力评估，揭示当前模型的瓶颈与不足。

## 2. 论文提出的方法论

- **核心思想**：采用**schema引导的结构化预测**任务形式化。给定文档图像 \(x\) 和预定义或文档级 \(schema\ s = (F, R)\)（\(F\) 为目标字段集合，\(R\) 为字段间关系），模型一次性生成结构化输出 \(y_{SG} = M(x, s)\)，直接输出与schema对齐的JSON格式结果。
- **关键技术细节**：
  - **两个互补评估轨道**：
    - **约束类别KIE轨道（Constrained-Category KIE Track）**：基于预定义的场景schema，覆盖3个领域、11个真实应用场景（如商业交易、公共服务、受监管记录），每场景文档使用少量固定schema。
    - **开放类别KIE轨道（Open-Category KIE Track）**：无场景假设，每份文档对应自己独特的schema（由OCR结果和人工标注生成），评估模型对任意存在关键信息的抽取能力，覆盖中英文、4种文档类型（收据、表单、发票、合同）。
  - **数据构建**：
    - 约束轨道：从多个公开数据集（如SIBR、DocILE、FUNSD等）收集，经人工映射、修正或重标注确保与schema一致。
    - 开放轨道：通过文档重建流水线生成合成文档，利用GPT-4o及LLM生成HTML代码并渲染为文档图像，施加3D变形、模糊等噪声模拟真实条件，确保隐私且视觉真实。
  - **评估指标**：字段级别F1分数，要求模型预测值与ground truth完全匹配（字符级精确匹配）。
  - **统一提示模板**：所有模型使用相同prompt，要求以给定schema格式输出JSON，禁止额外解释。

## 3. 实验设计

- **使用的数据集与场景**：
  - 约束类别：11个场景（Commercial, Retail, Catering, Accommodation, Administrative, Education, Postal Label, Advertisement, Tax-Compliant, Medical Services, Nutrition Label），共4472份测试文档。
  - 开放类别：中英文各4种文档类型（收据、表单、发票、合同），共1661份文档。
- **Benchmark**：UNIKIE-BENCH本身即为所提基准，与现有基准（OCRBench、OCRBenchV2、DocILE、RealKIE、CC-OCR）进行对比（见表3）。
- **对比方法**（共15个LMMs）：
  - 闭源：GPT-5、GPT-4o、Gemini-3-Pro、Claude-Sonnet-4.5、Qwen3-VL-Plus、Qwen-VL-Max
  - 开源：SmolVLM2-2.2B、Gemma-3-12B、InternVL3.5-8B、Ministral-3-8B、MiniCPM-V4.5-8B、GLM-4.1V-9B、Kimi-VL-A3B、MiMo-VL-7B-RL、Qwen3-VL-8B
- **实验设置**：图像像素总数不超过1,605,632；闭源模型通过官方SDK调用，开源模型使用vLLM+Flash-Attention部署；温度设为0消除采样变异性。

## 4. 资源与算力

- 文中明确提到：所有开源模型**部署在两块NVIDIA A100 GPU**上；闭源模型通过API访问。
- **未说明**：训练时长、具体算力消耗细节（如推理时批次大小、GPU显存使用等）。

## 5. 实验数量与充分性

- **实验数量较多**：包含两个主实验结果表（表4、表5），分别覆盖约束和开放轨道，每表记录了15个模型在多个场景/文档类型下的F1分数。此外还有：
  - faithfulness分析（图2）：统计预测值是否可被OCR结果定位。
  - 典型错误分析（图3）：分类视觉感知失败、布局感知失败、字段解释错误、幻觉预测。
  - 附录中还将Qwen3-VL-8B的注意力层行为进行了可视化分析（图8、图9）。
- **充分性**：覆盖了多种模型类型（闭源/开源、不同规模）、多场景、中英文、多种文档类型，实验设计较为全面。消融实验方面，未有专门针对数据来源或模型组件的消融，但通过将两个轨道分开评估以及错误分类分析，一定程度上提供了解释性。整体而言实验结果客观，指标定义清晰，比较公平。

## 6. 论文的主要结论与发现

- **总体性能差距**：闭源LMMs显著优于开源，Gemini-3-Pro综合最优，Qwen3-VL-8B是最强开源模型。
- **跨语言挑战**：所有模型在中文文档上的表现显著低于英文，表明跨语言鲁棒性不足。
- **布局复杂度影响**：表单文档（Form）因布局碎片化、字段边界灵活，对模型挑战最大；收据文档最简单。
- **faithfulness与性能正相关**：F1分数越高通常伴随更高faithfulness，但高faithfulness并不保证高F1，模型仍需改进字段语义理解和边界定位。
- **典型错误模式**：视觉感知失败（数字混淆）、布局感知失败（错选邻近文本）、字段解释错误（混淆相似字段含义）、幻觉预测（生成不存在内容）。
- **注意力机制分析**：当字段名显式出现时，模型从浅层关注标签转向深层关注值；字段名隐式时，模型在浅层定位近似短语，深层分布到多个候选区，依赖上下文推理。

## 7. 优点

- **统一的任务形式化**：采用schema-guided结构化预测，支持单次推理完成KIE，避免多次独立查询，且能捕获字段间结构关系。
- **双轨道设计**：约束类别模拟实际应用需求，开放类别评估通用抽取能力，互补覆盖。
- **大规模多场景覆盖**：包含3领域11场景的中英文文档，多样性高。
- **合成数据质量保证**：通过真实性分析、语义多样性分析和布局多样性分析验证了合成文档与真实文档的分布接近。
- **详细的错误分析**：分类归纳四种错误类型，揭示了LMMs在布局感知和grounding方面的系统性不足。
- **开放性**：代码和数据集公开，prompt统一，便于复现和公平比较。

## 8. 不足与局限

- **仅限单页/短文档**：不涉及长文档KIE，因为长文档依赖额外组件（页面检索、跨页聚合），难以隔离核心KIE能力。
- **合成数据潜在的分布偏移**：尽管通过多项分析验证真实性，但合成文档的视觉噪声、版面细节与真实扫描/拍照文档仍可能存在差距，可能影响泛化评估的结论。
- **评估指标单一**：采用精确字符串匹配F1，未考虑近似匹配或同义替换，可能低估模型在语义抽取上的部分能力。
- **消融不足**：没有针对不同数据来源、不同schema设计、不同视觉噪声水平进行系统性消融，未能深入解释哪些因素对性能影响最大。
- **建模假设**：schema-guided方式要求每一步都提供完整schema，实际部署中可能无法提供如此详细的schema定义，限制了本基准对无schema场景的评估。

（完）
