---
title: "Ground Then Rank: Revisiting Knowledge-Based VQA with Training-Free Entity Identification"
title_zh: 先定位再排序：重新审视基于知识的视觉问答中的无训练实体识别
authors: "Qian Ma, Qiong Wu, Zhengyi Zhou, Yao Ma"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.563.pdf"
tags: ["query:multimodal"]
score: 4.0
evidence: 多模态大语言模型在知识型视觉问答中的实体识别
tldr: 该论文重新审视知识型视觉问答中的多模态检索增强生成方法，提出分阶段的实体级和事实级定位方法，以降低计算成本并提升泛化能力。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 720, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 360, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 248, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 249, \"height\": 242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 249, \"height\": 250, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 254, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 249, \"height\": 252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 253, \"height\": 252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 253, \"height\": 252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 250, \"height\": 248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 253, \"height\": 252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 253, \"height\": 257, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 248, \"height\": 254, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 255, \"height\": 253, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 254, \"height\": 260, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 251, \"height\": 255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 252, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 457, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 461, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 456, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 458, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 461, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.563/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 458, \"height\": 455, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.563/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.563/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 786, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.563/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1394, \"height\": 826, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.563/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 830, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.563/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 822, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.563/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 695, \"height\": 216, \"label\": \"Table\"}]"
motivation: 现有MM-RAG方法将实体区分和证据排序耦合，导致高成本和有限泛化。
method: 将实体级和事实级定位分离，设计无训练的两阶段流程。
result: 所提方法在KB-VQA上实现更高效的实体与证据定位。
conclusion: 分阶段定位是提升多模态RAG效率和泛化性的有效途径。
---

## Abstract
Knowledge-Based Visual Question Answering (KB-VQA) requires grounding visual queries to external knowledge beyond directly observable content in images.While recent multi modal large language models (MLLMs) show strong perceptual abilities, they struggle on KB-VQA tasks requiring groundings from both fine-grained entity and evidence levels.Most existing multi-modal retrieval augmented generation (MM-RAG) methods tightly couple entity discrimination and section-level evidence ranking into a single re-ranking stage, leading to high cost and limited generalization.In this work, we revisit existing MM-RAG solutions from a workflow perspective and argue both entity-level and fact-level groundings are key bottlenecks.We observe that although MLLMs often fail under open-ended entity naming, they can better identify the correct entity when selecting from a small set of candidate names.Based on this insight, we propose a simple and training-free identify-before-answer IBA framework that decouples entity identification from section-level re-ranking.Our approach prompts an MLLM to select high-confidence entities using only candidate names, followed by an off-the-shelf textual re-ranker for evidence selection.Experiments on Encyclopedic-VQA and InfoSeek show that our method consistently outperforms fine-tuned multi-modal re-ranking baselines while reducing training and inference complexity.Additional analyses reveal that the improvements arise not only from better entity identification, but also from selecting more informative evidence once correct entity is fixed.Our implementation is made public to ease reproducibility

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：基于知识的视觉问答（KB-VQA）需要将视觉查询与图像外部的知识（如维基百科实体）进行细粒度定位。当前多模态大语言模型（MLLM）在开放式实体命名任务上表现不佳，难以直接从图像中生成正确的实体名称。
- **现有方法的局限**：主流多模态检索增强生成（MM-RAG）方法将实体区分和段落级证据排序耦合在一个重排序阶段中，导致计算成本高、泛化能力有限。同一评分函数难以同时区分不同实体和选择正确的证据段落。
- **观察与动机**：作者发现，尽管 MLLM 在开放式命名下失败，但当提供候选实体名称列表时，其识别准确率大幅提升（类似人类的“舌尖现象”）。基于此，提出解耦实体识别与证据排序的“先识别再回答”（IBA）框架。

## 2. 论文提出的方法论

- **核心思想**：将 KB-VQA 流程解耦为两个独立阶段：首先利用 MLLM 进行实体级识别（仅基于候选名称），再使用现成的文本重排序器进行段落级证据选择。全程无需训练或微调。
- **关键技术细节**：
  - **初始检索**：使用 EVA-CLIP-8B 进行图像到图像检索，从大型知识库（如 200 万维基百科页面）中获取 Top‑20 候选实体。
  - **实体识别**：将查询图像与候选实体名称（附带初始视觉相似度分数）输入 MLLM（Qwen‑2.5‑VL‑7B‑Instruct），要求其选出 top‑j 个高置信度实体（j < K）。通过约束选择任务激活 MLLM 的潜在知识。
  - **段落重排序**：对识别出的每个实体，使用现成的 BGE 文本重排序器计算问题与每个段落的相关性分数。
  - **最终评分公式**：`score = α·ID(P_i) + β·V(I, I_i) + γ·T(S_{i,j})`，其中 ID 为识别置信度，V 为视觉相似度，T 为文本相关性。超参数（α, β, γ）在数据集上微调，但敏感性分析显示设为 1 时性能下降微小。
  - **答案生成**：选择最高分段落作为上下文，使用 Llama‑3.1‑8B‑Instruct 或 Qwen‑2.5‑VL‑7B‑Instruct 生成最终答案。
- **流程文字描述**：输入图像 → 图像检索得 Top‑20 候选 → MLLM 识别出 top‑3 实体 → 仅对 3 个实体的所有段落进行文本重排序 → 选出最相关段落 → LLM 生成答案。

## 3. 实验设计

- **数据集**：Encyclopedic‑VQA（E‑VQA，约 22 万对，单跳问题）和 InfoSeek（约 130 万对，涵盖 1.1 万个视觉实体）。知识库为 200 万/10 万维基百科页面。
- **基准方法**：
  - 需微调的 MM‑RAG：EchoSight（训练多模态重排序器）、ReflectiVA（基于自反射令牌的微调 MLLM）。
  - 零样本变体：Para（无外部证据）、Article（直接使用 Top‑5 文章）、1Stage（单提示隐式重排序）、2Stage（两提示显式分解）。
- **评估指标**：
  - 检索：Recall@K（实体级）。
  - 答案生成：E‑VQA 用 BEM 分数（基于 BERT 的语义等价性），InfoSeek 对于时间/数字问题用 VQA 准确率，字符串问题用 BEM。
- **对比设置**：均使用相同的初始检索（EVA‑CLIP‑8B，Top‑20）和相同的生成骨干（Llama‑3.1‑8B 或 Qwen‑2.5‑VL‑7B），保证公平。

## 4. 资源与算力

- 论文**未明确说明**所使用的 GPU 型号、数量、训练时长等具体算力资源。
- 作者强调所有组件均为**训练无关**（training‑free）的现成模型（EVA‑CLIP‑8B、Qwen‑2.5‑VL‑7B、BGE reranker），无需额外微调，因此训练算力成本为零。仅推理阶段需要运行这些模型。
- 附录 G 和 H 提供了 FLOPs 的大致估算，显示 IBA 的总计算量（约 6.35×10¹² FLOPs）远低于 EchoSight 的重排序部分（约 4.8×10¹⁴ FLOPs），效率提升近两个数量级。

## 5. 实验数量与充分性

- **实验组数**：包含 6 张表格和多个定性示例：
  - 表 1‑2：检索 Recall@K 对比（E‑VQA 和 InfoSeek）。
  - 表 3：答案生成分数对比，涵盖 2 个数据集 × 2 个骨干 × 大量零样本基线，以及缺失值拆分（未见过问题/实体）。
  - 表 4：消融实验（在 E‑VQA 有前提子集上替换重排序器）。
  - 表 5：分解分析（按双方是否识别正确分类）。
  - 表 6：直接证据命中率对比。
  - 附录中还有敏感性分析、token 预算分析、FLOPs 对比。
- **充分性评价**：
  - **优点**：覆盖了多个数据集、多种基线（零样本 vs 微调）、多种消融设置，并分析了证据质量而非仅仅实体召回。实验设计客观，控制初始检索和生成骨干一致。
  - **局限**：主要在两个基准上进行，未在更广泛或真实场景测试。部分消融实验仅基于 E‑VQA 的有前提子集（约 2322 个问题），样本量可能偏低。

## 6. 论文的主要结论与发现

1. **“舌尖效应”确认**：提供候选实体名称可显著提升 MLLM 的实体识别能力（E‑VQA 从 25.5% 升至 40.2%，InfoSeek 从 45.8% 升至 73.2%），且 GPT‑5.2 也验证该现象。
2. **分离实体识别与证据排序是关键**：IBA 在多数指标上超过需微调的 EchoSight 和 ReflectiVA，同时降低计算成本。
3. **提升不仅来自实体识别，更来自更优的证据段落选择**：即使双方均识别出正确实体，IBA 选出的段落更直接包含答案（表 5 中“Both ✓”列 IBA 得分 88.2 vs EchoSight 79.6）。直接证据命中率也更高（表 6，33.8% vs 30.2%）。
4. **现成的文本重排序器效果优于多模态重排序器**：在识别正确实体后，使用多模态重排序器反而降低答案质量（表 4）。
5. **简单零样本提示（如 1Stage/2Stage）不可靠**：MLLM 无法在长上下文中可靠地隐式重排序，导致性能下降。

## 7. 优点

- **训练无关**：所有组件均为现成模型，无需任何微调，通用性和可复现性强。
- **高效**：通过先识别实体（仅看名称+图像）大幅减少重排序段落数（从 165 段降至约 25 段），总 FLOPs 降低约两个数量级。
- **可解释性**：实体识别、视觉相似度、文本相关性各自独立贡献分数，可单独分析每个环节的影响。
- **鲁棒性**：超参数敏感性低（统一设为 1 时性能仅下降 0.6%~2.1%），无需复杂调参。
- **洞察深刻**：首次系统揭示 MLLM 在 KB‑VQA 中的“舌尖现象”，并证明分离实体级和事实级定位是更合理的范式。

## 8. 不足与局限

- **依赖知识库质量**：假设知识库已包含全部必要知识，在真实场景中知识库可能不完整（作者在局限性中承认）。
- **实验覆盖有限**：仅在两个基准上评估，未涉及更多实体类别或开放端到端搜索环境（如利用互联网的智能体流程）。
- **潜在偏差**：使用的候选名称列表来自图像检索，若检索遗漏正确实体则无法恢复；实体识别可能偏向高频或视觉相似的实体。
- **泛化性验证不足**：主要实验集中于英语和维基百科知识，对其他语言和知识源的有效性未讨论。
- **计算分析基于 FLOPs 估计**：实际硬件上的延迟差异未测量，且 FLOPs 估计本身依赖特定近似（附录 H），可能不完全准确。
- **消融实验规模偏小**：部分分析仅基于 1000 个采样问题（InfoSeek）或 2322 个有前提问题（E‑VQA），统计稳定性需进一步验证。

（完）
