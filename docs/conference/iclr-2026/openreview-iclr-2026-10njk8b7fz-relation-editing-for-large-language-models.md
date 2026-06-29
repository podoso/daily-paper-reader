---
title: Relation Editing for Large Language Models
title_zh: 面向大语言模型的关系编辑
authors: "Xu Cao, Qing Liu, Mengyang Li, Xinrui Chen, Ou Wu, Yi Du"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=10nJk8B7FZ"
tags: ["query:llm"]
score: 4.0
evidence: 面向大语言模型的关系编辑
tldr: "该论文提出关系编辑任务，为大型语言模型中的关系知识更新构建专用数据集，并发现现有编辑方法存在高达98.20%的过时信息残留。虽涉及关系概念，但属于模型编辑而非信息抽取中的关系抽取。"
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1438, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 568, \"height\": 493, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1381, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1450, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1446, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1425, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1413, \"height\": 724, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1448, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1436, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1146, \"height\": 798, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-10njk8b7fz/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1498, \"height\": 1914, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 698, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1450, \"height\": 804, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 727, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1451, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1447, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1452, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1460, \"height\": 625, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1138, \"height\": 462, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1420, \"height\": 730, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1408, \"height\": 852, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-10njk8b7fz/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1424, \"height\": 830, \"label\": \"Table\"}]"
motivation: 现有知识编辑仅关注修改对象，忽略了关系本身的更新需求。
method: 构建关系编辑数据集，评估现有算法并分析失败原因。
result: 揭示当前方法在关系编辑中严重保留过时信息。
conclusion: 关系编辑是值得探索的新方向，但与实体关系抽取任务不同。
---

## Abstract
Knowledge editing is a critical technique for the routine updating and maintenance of LLMs. Existing research predominantly assumes changes only to the object within subject-relation-object triples, with minimal exploration into techniques for editing the relation. We term this task Relation Editing(distinct from the established "Object Editing" paradigm). We first construct a dedicated relation editing dataset and benchmark existing algorithms, revealing a critical flaw: even with successful edits, prominent methods suffer from the persistent retention of outdated information, with rates reaching as high as 98.20\%. Editing failures stem primarily from two sources: the persistent retention of outdated relationships and the presence of challenging editing samples. To address the first issue, we propose a novel relation editing framework called Forgetting-and-Editing (FE). We theoretically show that existing forgetting methods (i.e., model unlearning) are unsuitable for this purpose and, to this end, introduce a new target assignment strategy within our framework. To mitigate the second challenge, we introduce a self-paced learning strategy, instantiated in a new algorithm named self-paced AlphaEdit(SPaEdit). We conduct extensive experiments on both our compiled relation-editing dataset and established object-editing benchmarks. Results demonstrate that our proposed relation editing strategy achieves satisfactory performance on the relation editing task. In addition, SPaEdit outperforms existing SOTA methods on object-editing benchmarks. Our research also suggests further study is warranted in relation editing, particularly on forgetting existing relations.

---

## 论文详细总结（自动生成）

# 论文总结：Relation Editing for Large Language Models

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现有知识编辑研究主要关注修改三元组中的**对象**（Object Editing），即 `(s, r, o) → (s, r, o*)`，但忽略了修改**关系**（Relation Editing）的需求，即 `(s, r, o) → (s, r*, o)`。例如，将“齐达内是皇马的球员”改为“齐达内是皇马的教练”需要更新关系而非对象。这种实际场景非常常见，但现有方法尚未专门研究。
- **核心问题**：直接应用现有对象编辑方法进行关系编辑存在两大缺陷：① 旧知识保留率极高（高达98.20%），编辑只是“附加”而非“覆盖”；② 对困难样本（计算残差大）编辑成功率低。
- **贡献**：本文首次系统定义关系编辑任务，构建专用数据集 ReEditBench，并提出 Forgetting-and-Editing (FE) 和 Self-paced AlphaEdit (SPaEdit) 方法，显著提升关系编辑性能，同时在对象编辑任务上也达到 SOTA。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 2.1 Forgetting-and-Editing (FE) 框架
- **核心思想**：先“忘记”旧关系，再“编辑”新关系。直接使用现有模型遗忘策略（如将目标设为“I don't know”或随机答案）在基于线性回归的编辑方法中会导致系统性偏差，使正常知识也被扭曲。
- **关键技术**：提出**目标平滑 (Target Smoothing)** 策略，为待遗忘的三元组 `(s, r, o)` 生成中间目标向量：
  ```
  v(ô) = v(o) + γ * [v(IDK) - v(o)] , γ ∈ (0,1)
  ```
  该策略满足：非恒定、非随机、与原始目标向量相近，从而抑制系统性偏差，提升遗忘效果，同时减小对正常知识的扰动。
- **算法流程**：对于每个关系编辑样本，构造两组键值对：遗忘对 (k_old, v(ô)) 和编辑对 (k_new, v(o))，将两者拼接后作为完整训练集输入基准编辑方法（如 AlphaEdit 或 SPaEdit）进行联合优化。

### 2.2 Self-paced AlphaEdit (SPaEdit)
- **核心思想**：引入自步学习 (Self-Paced Learning)，按照“从易到难”的顺序进行编辑，先学习简单样本，再逐步纳入困难样本，迭代优化。
- **关键技术细节**：
  - 在 AlphaEdit 原始目标函数中引入二进制选择变量 z_i ∈ {0,1}，表示样本是否被当前迭代选中：
    ```
    min_{Δ,z} ∑ z_i * ℓ_i(Δ) + α||ΔP||²_F + β||ΔP K_p||²_F - λ ∑ z_i
    ```
  - 固定 z 时，求解 Δ 的闭式解为：
    ```
    ΔSPaEdit = (V1 - WK1) Z K1^T P (K1 Z K1^T P + β Kp Kp^T P + αI)^{-1}
    ```
  - 固定 Δ 时，根据损失 ℓ_i(Δ) 与阈值 λ 更新 z_i：ℓ_i < λ 时 z_i=1，否则 0。
  - 迭代过程中 λ 逐步增大（λ ← μλ），使更多困难样本被纳入。通过验证集选择最优模型（早期停止策略，patience=3）。
- **算法流程**（算法1）：
  1. 初始化 λ = λ0；
  2. 对于 t=1 到 T：
     - 计算每个样本的损失 ℓ_i；
     - 根据阈值 λ 更新选择矩阵 Z；
     - 计算当前 ΔP 闭式解；
     - 更新权重 W(t)，并增大 λ；
  3. 返回最优 W(t)。

## 3. 实验设计

### 3.1 数据集
- **关系编辑数据集 ReEditBench**：新建专用基准，包含 7,918 个实例，来自 ZsRE 和 Wikidata，经过四阶段构建（知识收集、LLM生成、自动过滤、人工验证），质量高达 98.5%。
- **对象编辑基准**：标准 ZsRE 和 CounterFact 数据集（使用困难子集进行重点评估）。

### 3.2 基础模型与基线方法
- **模型**：LLaMA3-8B、GPT-J-6B、GPT2-XL。
- **基线方法**：MEMIT、RECT、NSE、ROME、Fine-Tuning (FT)、PRUNE、AlphaEdit（共7种参数编辑方法）。特别对比了 FE 策略与无遗忘、IDK遗忘、随机遗忘的变体。

### 3.3 实验设置
- 关系编辑：顺序编辑设置，每次编辑100个样本，共2000个样本，遗忘参数 γ 设为0.6，α=10，β=1。
- 对象编辑：使用困难子集（100个样本），并报告全数据集结果。

### 3.4 评估指标
- **关系编辑**：Success（整体替换）、Retention（遗忘）、Efficacy（新知识获取）、Generalization（泛化）。
- **对象编辑**：Efficacy、Generalization、Specificity，以及 Fluency、Consistency（CounterFact）。

## 4. 资源与算力

- 论文明确说明：**所有实验可在单张 NVIDIA L40S (48GB) 上完整复现**。
- 未提供具体训练时长或 GPU 数量，仅提及“可以从头到尾在单张L40S上完成”。SPaEdit 的迭代过程会随困难样本增加而逐渐增加计算时间（见附录C.8）。

## 5. 实验数量与充分性

- **主要实验**：
  - 关系编辑主表（表2）：3种模型 × 8种方法 × 两个设置（Original vs +FE），共48组结果。
  - 对象编辑主表（表3）：3种模型 × 4种方法，12组结果；附录中还有全数据集结果（表7）和 CounterFact 结果（表6）。
  - 消融实验：遗忘策略对比（图4、表5），敏感性分析（λ 参数），语义相似度分析（附录C.5），鲁棒性分析（表层编辑攻击，附录C.6），稳定性分析（图10），通用能力影响（附录C.4）。
  - 算力与时间分析（图11）。
- **充分性**：实验覆盖了多种模型、多种基线、多个数据集，并对遗忘策略进行了深入消融；还分析了困难样本分布、语义相似度影响、对抗攻击鲁棒性、通用能力保持等，较为全面。实验设计公平（使用相同训练/测试划分，报告均值等）。

## 6. 主要结论与发现

1. **直接应用对象编辑方法进行关系编辑会严重保留旧知识**（保留率高达98.20%），且对困难样本编辑失败。
2. **Forgetting-and-Editing (FE) 策略显著改善关系编辑**：在所有模型和方法上提升 Success 平均 10.07%（最高 34.49%），同时降低 Retention。
3. **SPaEdit 在关系编辑和对象编辑上均达到 SOTA**：在 ZsRE 困难子集上，SPaEdit 在 LLaMA3 上 Efficacy 达 92.32%（AlphaEdit 81.87%），在 GPT-J 上近乎完美 99.97%。在 CounterFact 困难子集上也全面领先。
4. **目标平滑策略优于固定目标（IDK/随机）**：理论分析和实验均证明固定/随机目标会导致系统性偏差，而插值策略能更干净地遗忘。
5. **自步学习有效解决困难样本**：从易到难的课程学习使模型逐步适应，最终在困难样本上表现优异。

## 7. 优点

- **任务定义创新**：首次系统定义关系编辑任务，填补空白。
- **基准构建高质量**：ReEditBench 经过多轮过滤和人工验证（98.5%有效），公开代码。
- **理论分析深入**：对现有遗忘策略在知识编辑中的理论缺陷进行了严谨数学推导，为设计新策略提供依据。
- **方法设计合理**：FE 策略简单有效，SPaEdit 将自步学习与 AlphaEdit 的零空间约束相结合，迭代增强而不影响全局稳定性（通用能力实验证明几乎不下降）。
- **实验全面**：不仅评估关系编辑，还在传统对象编辑基准上验证泛化性，并进行了多种消融、鲁棒性和稳定性测试。
- **可复现性**：提供匿名代码和数据链接，单卡L40S即可复现所有实验。

## 8. 不足与局限

- **遗忘仍不完美**：尽管 FE 显著降低 Retention，但在某些困难设置下保留率仍约 50%，完全干净的遗忘仍是开放问题。
- **关系编辑仅考虑关系变化**：未考虑同时更改关系和对象的复杂场景（用户可能指定新对象）。
- **数据集规模有限**：ReEditBench 仅约 8k 实例，且来自单一语言（英语），需扩展至更多语言和领域。
- **通用能力评估仅做小规模实验**：通用能力测试仅使用 LLaMA3-8B 进行顺序编辑（附录C.4），未在其他模型上验证长期稳定性。
- **计算代价**：SPaEdit 的迭代过程比单步方法（如 AlphaEdit）更耗时，尽管在可接受范围内，但对大规模编辑可能成为瓶颈。
- **风险声明**：虽然论文提及伦理风险，但未提供实际防御机制（如对抗恶意编辑）。

（完）
