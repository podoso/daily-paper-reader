---
title: "Beyond Unimodal Shortcuts: MLLMs as Cross-Modal Reasoners for Grounded Named Entity Recognition"
title_zh: 超越单模态捷径：多模态大语言模型作为接地命名实体识别的跨模态推理器
authors: "Jinlong Ma, Yu Zhang, Xuefeng Bai (白雪峰), Kehai Chen (陈科海), Yuwei Wang, Zeming Liu, Jun Yu, Min Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2162.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 多模态接地命名实体识别与跨模态推理
tldr: 该论文探索利用多模态大语言模型以端到端方式执行接地多模态NER，揭示模态偏差问题，并提出模态感知一致性推理（MCR）方法，通过结构化跨模态推理提升准确性和鲁棒性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1626, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 347, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 782, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1574, \"height\": 1864, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2162/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1609, \"height\": 986, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1591, \"height\": 1318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 732, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 649, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 806, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 654, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 808, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 605, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 666, \"height\": 940, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 803, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2162/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 730, \"height\": 429, \"label\": \"Table\"}]"
motivation: MLLM在执行接地多模态NER时存在模态偏差，倾向于走单模态捷径。
method: 提出模态感知一致性推理（MCR），强制进行结构化跨模态验证。
result: MCR有效缓解模态偏差，提升接地NER性能。
conclusion: 结构化跨模态推理是提升MLLM在多模态NER中表现的关键。
---

## Abstract
Grounded Multimodal Named Entity Recognition (GMNER) aims to extract text-based entities, assign them semantic categories, and ground them to corresponding visual regions. In this work, we explore the potential of Multimodal Large Language Models (MLLMs) to perform GMNER in an end-to-end manner, moving beyond their typical role as auxiliary tools within cascaded pipelines.Crucially, our investigation reveals a fundamental challenge: MLLMs exhibit modality bias , including visual bias and textual bias, which stems from their tendency to take unimodal shortcuts rather than rigorous cross-modal verification.To address this, we propose Modality-aware Consistency Reasoning ( MCR ), which enforces structured cross-modal reasoning through Multi-style Reasoning Schema Injection (MRSI) and Constraint-guided Verifiable Optimization (CVO). MRSI transforms abstract constraints into executable reasoning chains, while CVO empowers the model to dynamically align its reasoning trajectories with Group Relative Policy Optimization (GRPO).Experiments on GMNER and visual grounding tasks demonstrate that MCR effectively mitigates modality bias and achieves superior performance compared to existing baselines.

---

## 论文详细总结（自动生成）

# 论文中文学术总结

## 1. 论文的核心问题与整体含义

- **研究动机**：Grounded Multimodal Named Entity Recognition (GMNER) 任务要求从文本中提取命名实体、分类并定位到图像中的对应区域。现有方法通常将多模态大语言模型（MLLM）作为辅助工具嵌入级联管道中，这不仅引入累积误差，还增加计算成本。本文首次探索以端到端方式利用 MLLM 执行 GMNER。
- **核心问题**：直接应用 MLLM 进行 GMNER 时存在**模态偏差（modality bias）**，包括：
  - **文本偏差（textual bias）**：模型忽略视觉证据，将文本实体错误地定位到图像中其他视觉显著物体上。
  - **视觉偏差（visual bias）**：模型受视觉线索误导，将仅在图像中出现、文本中不存在的实体错误识别为命名实体。
- 根本原因：MLLM 倾向于走单模态认知捷径（unimodal shortcuts），而非进行严格的跨模态验证。

## 2. 论文提出的方法论

- **核心思想**：提出 **Modality-aware Consistency Reasoning (MCR)**，通过结构化跨模态推理强制模型进行一致性验证，从而缓解模态偏差。
- **关键技术细节**：
  - **Multi-style Reasoning Schema Injection (MRSI)**：
    - 定义四类核心约束：实体识别（C_s）、类型分类（C_t）、视觉蕴含（C_e）、视觉定位（C_u）。
    - 利用模板、LLM 或 MLLM 将标注数据转化为多样化的推理链（reasoning chains），构建训练集 D_R。
    - 通过监督微调（SFT）将推理模式注入 MLLM，使模型在预测前先生成逐步推理路径。
  - **Constraint-guided Verifiable Optimization (CVO)**：
    - 基于上述约束设计可验证奖励函数：实体数量奖励（R_c）、实体跨度奖励（R_s）、实体类型奖励（R_t）、定位奖励（R_u，基于 IoU）、蕴含奖励（R_e）。
    - 总奖励：R = λ1R_c + λ2R_s + λ3R_t + λ4R_u + λ5R_e。
    - 采用 Group Relative Policy Optimization (GRPO) 优化策略，通过组优势估计和裁剪重要率更新策略，提升推理轨迹与约束一致性。
- **算法流程（文字说明）**：
  1. 对每个图像-文本-标签样本，生成多种风格的推理链（DR）。
  2. 将 DR 分为 D1（用于 MRSI 的 SFT 训练）和 D2（用于 CVO 的强化学习训练）。
  3. MRSI 阶段：通过 SFT 使模型学会生成推理链和最终答案。
  4. CVO 阶段：对 D2 中每个查询，模型生成 G 个响应，用奖励函数计算分数，计算组优势，用 GRPO 更新参数，惩罚单模态捷径。

## 3. 实验设计

- **数据集**：
  - 主数据集：Twitter-GMNER（GMNER 标准 benchmark，7000 训练 / 1500 验证 / 1500 测试）。
  - 额外评估：MNER-MI（多图像 MNER 数据集），GREC（通用视觉指代表达理解数据集，过滤多目标样本后使用 14000 训练）。
  - 总计训练样本：55,712 条带多风格推理标注。
- **基准方法**：
  - 管道方法：ITA-VinVL-EVG、BARTMNER-VinVL-EVG、SCANNER、ReFineG、UnCo。
  - 统一方法：MNER-QG、H-index、TIGER、MQSPN。
  - 端到端 MLLM：GLM4.5VL、Qwen2.5VL-72B、Qwen2.5VL-7B、MimoVL-7B，分别采用直接提示、CoT、CoT+3-Shot、SFT、MCR 等设置。
- **评估指标**：Precision、Recall、F1（GMNER、MNER、EEG 子任务）；对于 VG 使用 N-acc 和 Precision；引入 N-Pre、N-Rec、N-F1 量化文本偏差；N-Count 和 N-Rate 量化视觉偏差。

## 4. 资源与算力

- **硬件**：8 × NVIDIA Tesla L20 GPU（训练和推理）。
- **训练框架**：ms-swift + vLLM（解码与采样），使用 LoRA 微调。
- **MRSI 阶段**：4 张 L20，训练 8 小时（Qwen2.5VL 2  epoch，MimoVL 5 epoch）。
- **CVO 阶段**：4 张 L20，训练 11 小时（2 epoch，batch size 64，8 generations per input）。
- 文中未明确说明总 GPU 卡时数，但可估算 MRSI+CVO 合计约 19 小时。

## 5. 实验数量与充分性

- **主要实验结果**（Table 1）：在 Twitter-GMNER 上对比 12 种以上方法，涵盖管道、统一、端到端三种范式。
- **跨数据集评估**（Table 2）：在 MNER-MI 和 GREC 上验证。
- **消融实验**（Table 3）：去除 MRSI、去除 CVO、去除多样化推理风格、去除指令组件。
- **模态偏差量化**（Table 4 & Figure 3）：分别测量视觉偏差和文本偏差的减少。
- **注意力分析**（Table 5）：对比正常预测、文本偏差、MCR 的注意力分配。
- **训练/推理成本对比**（Table 6）：与 SFT 相比，MCR 的额外开销及效率。
- **敏感性分析**（Table 10）：对 IoU 阈值 σ、奖励权重 λ1、λ5 进行调参。
- **泛化能力与误差传播**（Table 11）：在 Twitter-FMNERG 上对比更多管道方法。
- **单模态主导样本分析**（Table 12）：验证 MCR 在文本主导情况下的表现。
- **实验充分性评价**：实验覆盖多数据集、多方法、多维度（主任务、偏差、成本、注意力、敏感性），消融实验设计合理，统计量丰富，结论具有较强说服力。

## 6. 论文的主要结论与发现

- MLLM 在 GMNER 中存在显著的模态偏差，导致错误定位和实体幻觉。
- 提出的 MCR 框架（MRSI + CVO）能够有效缓解模态偏差，在 GMNER 上 F1 达 70.6%，超越此前最优统一方法 MQSPN（58.8%）和管道方法 SCANNER（68.5%）。
- MRSI 提供必要的推理结构，CVO 进一步优化推理一致性，两者缺一不可。
- 多风格推理模式比单一风格带来更稳定的训练和更高最终性能。
- 注意力分析表明 MCR 通过增强对视觉 token 的关注来纠正文本偏差。

## 7. 优点

- **问题发现新颖**：首次系统诊断 MLLM 在 GMNER 中的模态偏差，归因于单模态认知捷径。
- **方法创新性强**：结合推理模式注入和可验证奖励强化学习，将抽象约束转化为可执行推理。
- **实验全面**：覆盖主任务、子任务、偏差量化、注意力机制、成本效率等多维度，消融设计严谨。
- **开源可用**：代码和数据已公开，便于复现和应用。

## 8. 不足与局限

- **知识依赖**：MCR 仍受底层 MLLM 参数化知识限制，对训练语料中未出现的实体可能泛化不足（文中 Limitation 部分明确指出）。
- **计算成本**：MRSI+CVO 训练时间比基础 SFT 增加约 10 小时，推理时间也略增（但优于管道方法）。
- **基准覆盖**：仅在 Twitter-GMNER、MNER-MI、GREC 三个数据集上评估，未在更多样化的场景（如新闻、医疗图像）中验证。
- **未探讨知识注入**：如何结合外部知识库进一步提升对未知实体的识别能力未涉及。
- **潜在社会风险**：作者提到可能被滥用于监控或产生误导信息，需注意隐私保护。

（完）
