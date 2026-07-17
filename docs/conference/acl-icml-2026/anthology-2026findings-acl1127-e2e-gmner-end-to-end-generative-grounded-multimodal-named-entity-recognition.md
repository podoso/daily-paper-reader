---
title: "E2E-GMNER: End-to-End Generative Grounded Multimodal Named Entity Recognition"
title_zh: E2E-GMNER：端到端生成式接地多模态命名实体识别
authors: "Meng Zhang, Jinzhong Ning, Xiaolong Wu, Hongfei Lin (林鸿飞), Yijia Zhang (张益嘉)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1127.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 多模态命名实体识别的端到端生成式模型
tldr: 现有接地多模态命名实体识别方法采用流水线架构，导致误差累积和次优优化。本文提出E2E-GMNER，一个完全端到端的生成式框架，在单个多模态大语言模型中统一实体识别、语义类型预测、视觉定位和隐式知识推理，并通过指令微调和思维链推理增强性能。实验表明该方法在GMNER基准上显著优于流水线方法。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1127/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 733, \"height\": 789, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1127/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1407, \"height\": 698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1127/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1594, \"height\": 373, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1127/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1418, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1127/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 711, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1127/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 775, \"height\": 266, \"label\": \"Table\"}]"
motivation: 流水线方法在多模态NER中导致误差累积，需要端到端联合优化。
method: 构建基于多模态大语言模型的单阶段生成框架，将任务形式化为指令微调条件生成，融入思维链推理。
result: 在GMNER基准上取得领先性能，有效缓解误差传播。
conclusion: 端到端生成式框架是解决多模态NER流水线问题的有效途径。
---

## Abstract
Grounded Multimodal Named Entity Recognition (GMNER) aims to jointly identify named entity mentions in text, predict their semantic types, and ground each entity to a corresponding visual region in an associated image. Existing approaches predominantly adopt pipeline-based architectures that decouple textual entity recognition and visual grounding, leading to error accumulation and suboptimal joint optimization. In this paper, we propose E2E-GMNER, a fully end-to-end generative framework that unifies entity recognition, semantic typing, visual grounding, and implicit knowledge reasoning within a single multimodal large language model. We formulate GMNER as an instruction-tuned conditional generation task and incorporate chain-of-thought reasoning to enable the model to adaptively determine when visual evidence or background knowledge is informative, reducing reliance on noisy cues. To further address the instability of generative bounding box prediction, we introduce Gaussian Risk-Aware Box Perturbation (GRBP), which replaces hard box supervision with probabilistically perturbed soft targets to improve robustness against annotation noise and discretization errors. Extensive experiments on the Twitter-GMNER and Twitter-FMNERG benchmarks demonstrate that E2E-GMNER achieves highly competitive performance compared with state of the art methods, validating the effectiveness of unified end-to-end optimization and noise-aware grounding supervision.

---

## 论文详细总结（自动生成）

# 论文总结：E2E-GMNER: End-to-End Generative Grounded Multimodal Named Entity Recognition

## 1. 核心问题与整体含义

- **问题背景**：接地多模态命名实体识别（GMNER）任务要求同时识别文本中的实体提及、预测其语义类型，并将每个实体与相关图像中的对应视觉区域（边界框）对齐。
- **现有方法弊端**：绝大多数现有方法采用流水线架构，将文本实体识别和视觉定位解耦为独立模块（如独立的NER标签器、外部目标检测器），导致误差累积且无法联合优化。
- **研究意义**：本文首次提出完全端到端的生成式框架E2E-GMNER，统一了实体识别、语义类型预测、视觉定位和隐式知识推理，旨在消除流水线误差并实现联合优化，提升GMNER整体性能。

## 2. 方法论

- **核心思想**：将GMNER形式化为一个基于多模态大语言模型（MLLM）的指令微调条件生成任务，通过单次自回归生成直接输出实体跨度、类型和边界框。
- **关键技术细节**：
  - **指令微调生成**：输入为任务指令+图像+文本，输出为推理序列（CoT）和结构化实体记录，格式为 `ei | ci | [x1, y1, x2, y2]`。
  - **Chain-of-Thought (CoT) 推理**：在训练时利用更强的教师模型（如Qwen2.5-VL-72B）生成推理序列作为监督信号，使模型学会自适应判断何时视觉证据或背景知识有效，减少对噪声线索的依赖；推理时无需外部模型。
  - **高斯风险感知边界框扰动 (GRBP)**：为解决生成式边界框预测对标注噪声和离散化误差敏感的问题，对真实边界框施加高斯扰动（中心偏移和尺度缩放），并引入IoU守卫（IoU≥τ才接受），将硬监督替换为概率性软目标，提高鲁棒性。算法流程：中心扰动→尺度扰动→IoU检查→重复最多T次，否则回退原始框。
- **训练目标**：标准自回归最大似然，对扰动后的边界框（软监督）进行token级预测。
- **推理**：完全端到端，无需外部知识或教师模型，模型自主生成CoT推理和结构化预测。

## 3. 实验设计

- **数据集**：Twitter-GMNER（4种粗粒度类型）和 Twitter-FMNERG（8种粗粒度+51种细粒度子类型），两个社交媒体GMNER基准。
- **评估指标**：整体GMNER F1、子任务MNER F1（识别+类型）、EEG F1（识别+定位，IoU≥0.5），以及Acc@0.5、MeanIoU等辅助指标。
- **对比方法**：
  - 知识增强方法：GMDA†、GEM†、RiVEG†、MAKAR†（使用额外数据或外部知识）。
  - 流水线方法（MNER-first类）：GPT4o、GVATT-OD-EVG、UMT-OD-EVG、UMGF-OD-EVG、ITA-OD-EVG、MMT5/BARTMNER-OD-EVG。
  - 流水线方法（特征融合类）：H-Index、TIGER、MQSPN、UnCo。
- **实验组**：主实验结果（表1）、消融实验（表2：去掉CoT、去掉GRBP）、教师模型影响（表3：不同教师生成CoT数据）、扰动强度分析（图3：β/γ从0到0.05变化）。

## 4. 资源与算力

- 文中附录B明确说明：所有实验在单个NVIDIA RTX 5090 GPU上进行。
- 使用Qwen2.5-VL-7B作为基础模型，采用LoRA（低秩适应）微调以减少显存占用。
- 优化器：AdamW，学习率4×10⁻⁵，weight decay 1×10⁻³，per-device batch size=2，梯度累积8步，有效batch size=16，最大输入序列长度2048 tokens。
- 教师模型生成CoT数据使用了更大的模型（如Qwen2.5-VL-72B、GPT-4o），但推理时不依赖它们。

## 5. 实验数量与充分性

- **实验数量**：至少包含4组正式实验（主结果表1、消融表2、教师对比表3、扰动分析图3），覆盖两个数据集和多个指标。
- **充分性**：
  - 主结果对比了所有主流方法（包括知识增强和流水线），公平全面。
  - 消融实验验证了两个核心组件（CoT、GRBP）的必要性，结果清晰。
  - 教师模型对比表明方法对教师选择具有鲁棒性。
  - 扰动强度分析揭示了最佳超参数范围，并分析了召回与精度的权衡。
- **客观性**：实验设计合理，指标标准（F1、IoU等），未发现明显偏差。

## 6. 主要结论与发现

- E2E-GMNER在Twitter-GMNER和Twitter-FMNERG上均优于所有不依赖外部知识的流水线方法，整体GMNER F1分别达到63.94和54.32。
- 即使与知识增强方法（如MAKAR†）相比，也取得了极具竞争力的结果，表明端到端统一优化可有效利用MLLM的隐式知识。
- CoT推理显著提升性能（去掉后GMNER F1下降约1.4-0.4），GRBP同样有效（去掉后下降约2.4-1.4）。
- GRBP主要通过提升定位召回（Acc@0.5）改善整体性能，尽管MeanIoU略有下降（召回-精度权衡）。
- 中等扰动强度（β=γ=0.03）表现最佳。

## 7. 优点

- **首次端到端**：第一个完全端到端生成式GMNER框架，消除了流水线误差累积，实现实体识别、类型分类、视觉定位和知识推理的联合优化。
- **噪声鲁棒定位**：提出GRBP，通过概率性软监督有效缓解了生成式边界框预测对标注噪声和离散化误差的敏感问题。
- **自适应推理**：融入CoT指令微调，使模型学会自主判断何时利用视觉/知识线索，而非被动依赖外部知识源。
- **高效推理**：推理时无需任何外部模型或API调用，单次生成即输出完整结构，成本低。
- **实验充分**：对比全面，消融严谨，参数分析细致。

## 8. 不足与局限

- **任务覆盖有限**：框架专为GMNER设计，尚未适配其他多模态信息抽取任务（如关系抽取、事件抽取），泛化能力未验证。
- **教师模型依赖**：CoT训练数据生成需要强教师模型（如72B级），引入了额外成本和注释工作量。
- **计算资源**：虽然推理高效，但训练仍需单张高端GPU（RTX 5090），对小规模实验室可能门槛高。
- **潜在过拟合**：扰动策略虽提升召回，但MeanIoU略降，在某些高精度定位场景下可能不够理想。
- **语言与领域**：仅在英语社交媒体数据上评估，对其他语言或专业领域（如医疗、遥感）的迁移效果未知。

（完）
