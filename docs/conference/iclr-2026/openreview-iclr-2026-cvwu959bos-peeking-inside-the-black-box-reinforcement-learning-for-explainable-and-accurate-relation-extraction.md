---
title: "Peeking inside the Black-Box: Reinforcement Learning for Explainable and Accurate Relation Extraction"
title_zh: 窥视黑箱：基于强化学习的可解释且准确的关系抽取
authors: "Xinyu Guo, Zhengliang Shi, Minglai Yang, Mahdi Rahimi, Mihai Surdeanu"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Cvwu959bOs"
tags: ["query:ie"]
score: 9.0
evidence: 使用强化学习进行可解释关系抽取
tldr: 关系抽取缺乏解释性监督。本文提出CogRE，将关系抽取建模为一系列文本处理步骤，并利用强化学习优化准确性和解释质量。自动构建高质量关键字字典，生成包含关系关键词的解释，在多个RE基准上取得高精度。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-cvwu959bos/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1393, \"height\": 1250, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-cvwu959bos/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1421, \"height\": 717, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-cvwu959bos/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1580, \"height\": 1009, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1438, \"height\": 1076, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 735, \"height\": 146, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 733, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1063, \"height\": 1006, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 995, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1000, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 900, \"height\": 833, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 829, \"height\": 1203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1110, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1105, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1020, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 899, \"height\": 505, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-cvwu959bos/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1228, \"height\": 1030, \"label\": \"Table\"}]"
motivation: 传统关系抽取缺乏可解释的语言监督。
method: 提出CogRE，将RE分解为推理步骤，用RL优化准确性和解释质量。
result: 在多个RE基准上取得高精度，同时生成高质量解释。
conclusion: RL可有效平衡关系抽取的准确性和可解释性。
---

## Abstract
This paper introduces a framework for relation extraction (RE) that enhances both accuracy and explainability. The framework has two key components: (i) a reasoning mechanism that formulates relation extraction as a series of text-processing steps inspired by cognitive science, and (ii) an optimization process driven by reinforcement learning (RL) with a novel reward function designed to improve both task accuracy and explanation quality. We call our approach CogRE. Our framework addresses the lack of supervision for language-based explanations in traditional RE by promoting outputs that include important relation keywords. These keywords are drawn from a high-quality dictionary that is automatically constructed using an LLM. We evaluate our approach for the task of one-shot RE using two LLMs and two RE datasets. Our experiments show that CogRE improves explanation quality by addressing two common failure patterns in one-shot RE: poor attention focus and limited one-shot learning capability. For example, our cognitive-structured reasoning with Qwen2.5-15B-Instruct on One-shot NYT29 achieves 24.65\% F1, surpassing prior reasoning-based designs. Optimizing this approach with RL using our reward further improves performance by +23.46\% (absolute). Finally, human evaluation shows that our best model generates relational keywords closely aligned with gold labels, increasing human explanation quality ratings by 54\% (relative).

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

关系抽取（Relation Extraction, RE）是 NLP 的基础任务，广泛应用于医疗、法律、金融等高风险领域，这些领域对模型的可解释性有很高要求。然而，传统 RE 方法（基于特征、神经网络、预训练小语言模型）存在两个主要局限：
- **可解释性有限**：难以提供自然语言形式的解释，仅能通过注意力权重或事后分析提供粗略解释；
- **依赖大量人工标注**：构建大规模标注数据集成本高昂，影响快速定制与部署。

本文研究 **one-shot RE** 的变体：给定每个关系仅一个支持句子，模型不仅需要正确抽取关系，还需要生成解释。尽管大语言模型（LLM）在语言理解和推理上表现出色，但其解释往往不忠实于决策（“LLMs do not say what they think”）。因此，论文旨在构建一个**同时提升准确性与可解释性**的 RE 系统。

## 2. 方法论：核心思想、关键技术细节

### 2.1 认知结构化推理框架（CogRE）
受认知科学中的 **建构-整合模型**（Kintsch, 1988）启发，将 RE 分解为三个步骤：
1. **语义分块**：将每个句子压缩为关系性命题（Proposition Chunking）；
2. **关键词锚定**：在原始句子和命题中锚定关系关键词（Keywords Anchoring）；
3. **整合推理**：结合命题和关键词生成连贯的逻辑链，并输出最终标签（Integrative Reasoning）。

这降低了 LLM 的处理负担，减少复杂句子中的推理幻觉。

### 2.2 强化学习与 HIT@DICT 奖励
使用 **Group Relative Policy Optimization**（GRPO）进行优化。奖励函数由两部分组成：
- **准确性奖励（\(R_{Acc}\)）**：针对 one-shot 中正负样本不平衡（1:K）设计权重，正确 Yes 得 3.0，正确 No 得 1.0，错误 Yes 扣 3.0，错误 No 扣 1.0。
- **解释质量奖励（\(R_{HIT@DICT}\)）**：通过一个自动构建的**关系关键词字典**评估解释中对关键词的覆盖。字典构建流程：
  1. 从训练集中收集正样本对（相同关系标签）；
  2. 用“普通”LLM 推理获得正确预测项的解释；
  3. 使用 GPT-4o 从这些解释中提取关系关键词，再结合关系标签本身分词得到最终字典；
  4. 奖励计算：分别统计实体关键词和关系关键词在解释中的命中次数，加权求和后按长度归一化。

最终奖励：\(R = R_{Acc} + R_{HIT@DICT}\)。GRPO 优化目标包含组内优势归一化和 KL 散度惩罚。

## 3. 实验设计

### 3.1 数据集与场景
- **数据集**：Few-shot TACRED 和 NYT29（来自 Alam et al., 2024），均为 one-shot 设置。
  - 训练集和测试集的关系标签**分布外**（out-of-distribution）。
  - 每个数据集随机采样约 1000 个 episode，保持原始关系比例。
- **任务**：给定支持句子和测试句子，判断它们是否表达相同的关系，并生成解释。

### 3.2 Benchmarks 与对比方法
- **基于提示的 LLM 基线**：
  - **SUMASK**（Li et al., 2023）：多轮问答形式，使用单提示变体。
  - **Direct Matching**：直接输出 Yes/No。
  - **Simple Reasoning**：先推理后回答。
- **传统监督方法**：
  - **Semantic Rule Matcher**（Vacareanu et al., 2024b）：结合神经网络分类器和规则，是 Few-Shot TACRED 和 NYT29 的 SOTA。
- **CogRE 的不同变体**：
  - 无强化学习（vanilla）；
  - 仅用准确性奖励；
  - 用 HIT@DICT + 准确性奖励。

### 3.3 评估指标
- **自动评估**：F1 分数（Precision/Recall）。
- **人工评估**：对解释质量采用 3 点 Likert 量表（两点评分：正确性和简洁性，一票判断是否与 RE 标注抽象级别对齐），由两名 NLP 背景标注员独立评估，Cohen's κ = 0.693（高度一致）。

## 4. 资源与算力
论文明确说明：
- **硬件**：4×NVIDIA H100-80GB GPU。
- **模型规模**：14B–15B 参数（Qwen2.5-14B-Instruct 和 Phi-4）。
- **训练时长**：约 **20 GPU 小时** 完成一次完整训练（使用 Verl 框架，actor 学习率 1e-6，KL 正则系数 0.01，熵正则系数 0.001）。
- 字典构建使用 GPT-4o API，不依赖人工标注。

**注意**：未提及推理阶段的具体计算开销，但字典是离线构建的，推理时仅需匹配，开销很小。

## 5. 实验数量与充分性
论文进行了以下实验：
- **主实验**（Table 1）：两个数据集 × 两个模型 × 六种方法（基线 + 三种推理变体 × 两种训练设置），共约 24 个 F1 值。
- **消融实验**（Table 3）：Phi-4 模型上移除三个推理步骤之一，共 8 个配置。
- **训练动态分析**（Figure 2）：对比仅 Acc 与 HIT@DICT+Acc 的奖励、KL、响应长度曲线。
- **人工评估**（Table 4）：两个模型 × 两个数据集 × 三个训练阶段，每个阶段 40 个解释（10 个 TP/TN/FP/FN），共 96 组评分。
- **模型规模/家族泛化实验**（Table 13，附录）：Qwen2.5-7B/3B、Phi-4-mini、Llama-3.2-8B、Mistral-7B 等共 15 个配置。

**充分性评估**：实验设计较为全面，覆盖了不同数据集、不同骨干模型、不同变量控制（推理步骤、奖励函数、模型规模）。消融实验证明了三个步骤的必要性。人工评估验证了解释质量提升。但仍存在可改进之处：
- 只测试了 one-shot 场景，未在 few-shot 或多标签设置下验证；
- 未与更多基于 LLM 的推理方法（如 CoT-SC、Self-Consistency）对比；
- 未进行统计显著性检验；
- 附录中的模型变体实验规模较小（仅在 TACRED 上评估）。

总体而言，实验客观且公平，但可进一步扩展。

## 6. 主要结论与发现
1. **CogRE 框架显著提升 RE 准确性**：在 TACRED 和 NYT29 上，CogRE 的 F1 分别达到 31.06% 和 24.65%，超越所有提示基线，并优于传统 SOTA（Semantic Rule Matcher）。
2. **RL 优化进一步提升性能**：使用准确性奖励后，F1 提升 3%–24%；加入 HIT@DICT 奖励后，F1 进一步提升（如 Qwen 在 NYT29 上达 48.11%，相对 +73.74%）。
3. **HIT@DICT 奖励加速收敛并稳定训练**：训练动态显示，使用该奖励时奖励曲线更快攀升，KL 惩罚更早收敛，响应长度压缩到 75–90 词。
4. **改善解释质量**：人工评估显示，HIT@DICT 训练后的模型解释更简洁，更符合关系标签的抽象级别，人类评分相对提高 54%。
5. **误差分析揭示 LLM 在 RE 中的两个关键失败模式**：
   - 关注不相关 token 而非真正传达关系的语义；
   - 无法与人类定义的关系标签抽象级别对齐（如混淆 “city of headquarters” 与 “country of headquarters”）。

## 7. 优点（方法或实验设计亮点）
1. **认知科学启发的推理分解**：将 RE 转化为三个可解释的步骤，降低 LLM 推理负担，且每一步都有独立贡献（消融实验证实）。
2. **自动构建关键词字典**：无需人工标注，采用 LLM 自身的正确预测输出构建，避免了人工偏好偏差。
3. **细粒度解释奖励**：HIT@DICT 是基于规则的轻量奖励，计算高效，且针对实体和关系关键词分别加权，提供比简单格式信号更丰富的信号。
4. **双维评估设计**：同时使用自动 F1 和人工评价，覆盖准确性和可解释性，并给出详细的评分规则和 Cohen's κ 一致性检验。
5. **丰富的训练动态分析**：可视化奖励、KL、响应长度随时间变化，直观展示两种奖励的差异。

## 8. 不足与局限
1. **实验覆盖范围有限**：
   - 仅考虑 one-shot 场景，未扩展到 few-shot（如 5-shot）或标准监督 RE；
   - 仅使用两个数据集（都来自同一基准），泛化性未在更多领域（如生物医学）验证。
2. **未与基于 LLM 的更强推理方法对比**：如 CoT with self-consistency、tree-of-thought、GPT-4 的 direct prompting 等（表1中基线较简单）。
3. **缺少统计显著性检验**：未报告置信区间或重复实验的方差，结果可能受单次实验的随机性影响。
4. **响应长度压缩可能牺牲部分解释完整性**：训练动态显示长度缩短，虽提升简洁性，但可能导致遗漏必要推理步骤（论文也提及某些情况下跳过了 chunking 后的推理）。
5. **字典构建依赖 GPT-4o**：虽然自动化，但引入额外 API 成本和潜在质量不可控性（如不同关系字典质量可能不均）。
6. **奖励超参数需手工设定**：\(w_{entity}=0.4, w_{relation}=1.0, N=5\) 为启发式选择，缺乏敏感性分析。
7. **未讨论模型偏见**：假阳/假阴的错误分布可能影响实用部署，尤其在医疗/法律领域需进一步的错误模式分析。

（完）
