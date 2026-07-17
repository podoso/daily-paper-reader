---
title: "ReCoT-NER: Enhancing Zero-Shot Named Entity Recognition through Chain-of-Thought Prompting and Recall-Oriented Loss Optimization"
title_zh: ReCoT-NER：通过思维链提示和面向召回率损失优化增强零样本命名实体识别
authors: "Dabin Fu, Fanghong Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.227.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 零样本命名实体识别与思维链提示
tldr: 针对零样本命名实体识别检测不全和边界不稳定问题，提出ReCoT-NER框架，通过思维链提示将NER分解为跨度检测和类型分类两个推理阶段，并引入面向召回率的损失优化。在风电故障诊断等专业领域取得优异效果。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.227/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.227/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 659, \"height\": 788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.227/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 775, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.227/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 494, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.227/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 766, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.227/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 594, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.227/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1347, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.227/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1228, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.227/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1137, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.227/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1654, \"height\": 454, \"label\": \"Table\"}]"
motivation: 零样本NER在专业领域面临实体检测不全和生成边界不稳定的挑战。
method: 提出ReCoT-NER框架，结合思维链提示进行两阶段推理，并采用面向召回率的损失优化。
result: 在风电故障诊断等领域有效提升了零样本NER的准确率和召回率。
conclusion: 推理增强和损失优化显著改善了零样本NER在专业领域的效果。
---

## Abstract
Named Entity Recognition (NER) plays a fundamental role in information extraction and domain knowledge construction. However, in specialized domains such as wind power fault diagnosis, the scarcity of labeled data makes supervised approaches impractical. Zero-shot NER provides a promising alternative but still struggles with incomplete entity detection and unstable generation boundaries. To address these challenges, we propose ReCoT-NER, a reasoning-enhanced generative framework that integrates Chain-of-Thought (CoT) prompting and recall-oriented loss optimization. The proposed CoT instruction design explicitly decomposes NER into two reasoning stages: entity span detection and entity type classification. This enables the model to follow a structured inference process. In addition, we introduce a recall-oriented loss function that reweights entity and non-entity tokens to mitigate false negatives, encouraging more inclusive entity coverage. Experiments on CrossNER, MIT, and a newly constructed wind-power NER dataset demonstrate that ReCoT-NER consistently improves recall and overall F1 performance across both general and industrial domains. Notably, ReCoT-NER achieves competitive results with just a 77M-parameter model, making it well-suited for low-resource zero-shot settings. The code for our method is publicly available at https://github.com/10637409100/RECOTNER.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究问题**：在零样本（zero-shot）命名实体识别（NER）任务中，现有方法存在实体检测不完整（低召回率）和生成边界不稳定的问题，尤其是在风电故障诊断等专业领域，标注数据稀缺使得监督方法不实用。
- **背景意义**：NER是信息抽取和领域知识构建的基础。零样本NER通过指令微调等方式无需目标域标注数据即可工作，但在复杂领域表现不佳，需要提升实体覆盖率和分类准确性。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 **ReCoT-NER** 框架，将思维链（Chain-of-Thought, CoT）提示与面向召回率的损失优化（RCLoss）结合，增强生成式NER的推理能力和实体召回。
- **关键技术细节**：
  - **CoT指令设计**：将NER显式分解为两个推理阶段：① 实体跨度检测（entity span detection）；② 实体类型分类（entity type classification）。模型按BIO格式输出带标签的词序列。
  - **面向召回率的损失函数（RCLoss）**：基于BIO标记结构，对 **B-token**（实体起始标记）赋予更高权重（α > β），并引入置信度因子 (1-p_t) 以聚焦低置信度预测。公式：
    - L_recall = w_t · (-log p_t)
    - 其中 w_t = α(1-p_t) （若为B token），否则 w_t = β(1-p_t) （α > β > 0）。
  - **算法流程**：训练阶段使用Pile-NER数据集进行指令微调，采用标准生成负对数似然损失（结合RCLoss）。推理时直接使用CoT引导的两步推理。
- **模型架构**：基于Flan-T5系列（small/77M, base/248M, large/783M），采用序列到序列的生成范式。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：
  - **训练集**：Pile-NER（约240K实体，13K类别，由ChatGPT自动标注）。
  - **零样本测试集**：
    - CrossNER（5个领域：AI、文学、音乐、政治、科学）
    - MIT（两个子集：Movie、Restaurant）
    - 自主构建的 **Wind-Power NER**（风电故障诊断领域，1312句，2384实体，11种实体类型，BIO标注）。
- **基准（Benchmark）**：使用标准数据切分和微平均F1指标，同时报告召回率和精确率。
- **对比方法**：InstructUIE（11B）、UniNER（7B/13B）、GoLLIE（7B/13B）、GNER-T5（重实现，与ReCoT-NER相同训练设置），以及ChatGPT（零样本）。

## 4. 资源与算力
- **硬件**：两台NVIDIA RTX 4090 GPU，每张24 GB显存。
- **软件**：PyTorch 2.4.0 + DeepSpeed，混合精度训练（bf16）。
- **超参数**：最大序列长度640 tokens，batch size 16。学习率 5×10⁻⁵，AdamW优化器，无权重衰减，恒学习率调度器。训练轮数：small/base模型20轮，large模型6轮。RCLoss默认α=1.2，β=1.0。

## 5. 实验数量与充分性
- **核心实验**：在CrossNER（5个子域）和MIT（2个子域）上进行了零样本评估，共计7个域；在Wind-Power NER上额外评测；覆盖了3种模型规模（small/base/large）。
- **消融实验**：在Flan-T5-small上对CoT和RCLoss分别进行消融（w/o CoT, w/o RCLoss），同时报告召回率和精确率变化。
- **超参数敏感性**：对RCLoss中α参数（1.0~2.0，步长0.1）进行了分析。
- **稳定性验证**：每个实验重复3次不同随机种子，报告平均F1和标准差（std < 0.005），表明结果可重复。
- **客观性评价**：对比方法均引用自原始论文或按相同设置重实现，基准设置一致。实验覆盖通用域和工业域，数据量适中但具有代表性。

## 6. 论文的主要结论与发现
- ReCoT-NER在所有模型规模上一致优于GNER-T5重实现基线，尤其在平均F1上。
- 仅77M参数的Flan-T5-small即超过多个大模型（如InstructUIE-11B、UniNER-7B），平均F1达53.5。
- 模型规模扩大（77M→783M）带来稳定提升（F1从53.5升至62.5）。
- 在Wind-Power NER上，ReCoT-NER（large）达到61.34 F1，大幅超越基线。
- 消融实验表明CoT和RCLoss均发挥重要作用：CoT提升结构推理和分类准确率，RCLoss显著提升召回率（最高达6.35点），且不影响精确率。

## 7. 优点
- **方法创新**：首次将CoT显式分解为跨度检测+类型分类两阶段用于生成式零样本NER，增强可解释性和推理能力。
- **损失函数设计巧妙**：基于BIO结构对B-token自适应加权，不依赖实体类型信息，符合零样本设定。
- **轻量高效**：77M模型即可达到竞争性结果，适合资源受限场景。
- **领域扩展**：通过构建Wind-Power NER数据集验证了在工业专业领域的有效性，弥补了现有研究在特殊领域验证的不足。
- **实验充分**：涵盖多种模型规模、多个域、消融、超参数灵敏度、稳定性分析，结果可靠。

## 8. 不足与局限
- **CoT推理隐式化**：CoT仅在指令层引导，生成过程中无显式中间步骤监督，难以完全捕捉复杂语义依赖。
- **损失函数未细化类型判别**：RCLoss专注于边界召回，不直接优化细粒度实体类型区分能力。
- **模型规模受限**：由于硬件限制，仅评估到Flan-T5-large（783M），未在更大模型（如数十亿参数）上验证，扩展性未知。
- **领域覆盖有限**：虽然构建了风电数据集，但仅涉及一个工业领域，跨多个专业领域的泛化性有待验证。
- **数据隐私与合规**：Wind-Power NER数据来自真实运维文档，虽已脱敏，但完全公开可能受限。

（完）
