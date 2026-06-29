---
title: "ICLR: Iterative Optimization for Information Extraction on In-Context Learning via Rule Filtering"
title_zh: ICLR：基于规则过滤的上下文学习信息抽取迭代优化
authors: "Haoliang Liu, Chengkun Cai, Xu Zhao, Han Zhu, Shizhou Huang, Xinglin Zhang, Tao Chen, Jenq-Neng Hwang, Lei Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=3bfseFWNUH"
tags: ["query:ie"]
score: 9.0
evidence: 基于上下文学习和规则过滤的信息抽取
tldr: 该论文提出ICLR框架，将规则优化建模为自适应滤波问题，通过迭代优化上下文规则来提升信息抽取（包括命名实体识别和关系抽取）的性能。方法直接针对IE任务，并利用大语言模型的上下文学习能力，属于信息抽取领域的前沿工作。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 654, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 542, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1308, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1360, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1295, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1288, \"height\": 694, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3bfsefwnuh/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1300, \"height\": 786, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-3bfsefwnuh/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1175, \"height\": 782, \"label\": \"Table\"}]"
motivation: 上下文学习中规则的选择和优化对于不同IE任务至关重要，但现有方法缺乏系统性。
method: 将规则优化视为控制理论中的自适应滤波问题，迭代更新规则。
result: 在NER和RE任务上取得了优于基线的方法，具体指标未在摘要中给出。
conclusion: 迭代规则优化能有效提升上下文学习在IE任务中的效果。
---

## Abstract
Existing information extraction (IE) tasks, such as named entity recognition (NER) and relation extraction (RE), typically rely on fine-tuning or few-shot learning methods. In few-shot learning, large language models (LLMs) demonstrate excellent performance through in-context learning (ICL), which involves guiding the model by providing a few examples or rules in the prompt. However, a major challenge with this approach is the selection and optimization of contextual information for diverse IE tasks. In this work, we introduce ICLR (Iterative Context Learning Rule), a control-theoretic framework that models rule optimization as an adaptive filtering problem for comprehensive information extraction. We treat rules as controllable state variables and design an observer system to monitor and control LLM behavior indirectly, without modifying model parameters. Our method iteratively estimates and updates the optimal rule combinations using performance feedback, thereby reformulating the traditionally complex problem of LLM control into a well-defined state-space optimization that generalizes across multiple IE tasks. We evaluate ICLR on both NER datasets (CoNLL03, ACE05, GENIA) and RE datasets (NYT, CoNLL04), demonstrating rapid convergence and superior performance with minimal training data requirements. Our approach achieves up to 10\% performance improvement over state-of-the-art ICL methods while requiring no additional model training and ICLR provides the first control-theoretic foundation for understanding and optimizing in-context learning behavior in information extraction.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：当前信息抽取（IE）任务（如命名实体识别NER、关系抽取RE）广泛采用大型语言模型（LLM）的上下文学习（ICL）范式。但ICL面临核心挑战：如何有效选择并优化提供给模型的上下文信息（如示例或规则），以在不同IE任务上取得稳定高性能。现有方法（如GuideNER）依赖启发式频率过滤选择规则，无法捕获规则间的复杂依赖性，且仅适用于NER任务，缺乏系统优化理论。
- **整体含义**：作者提出将规则优化建模为控制理论中的自适应滤波问题，首次为ICL规则选择建立控制理论基础，旨在实现跨NER和RE任务的通用、高效优化，且无需修改模型参数。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 核心思想
- 将规则视为外部可观测、可控的状态变量，通过构建一个**观测器系统**间接监控和调整LLM行为，避免直接操作海量参数空间。
- 将LLM控制问题转化为**状态空间优化**问题，规则具有低维、可解释、可控的优点。

### 关键技术细节与流程（ICLR算法）

#### 问题形式化
- 给定预训练LLM \( M \) 和数据集 \( D \)，目标是找到最优规则列表 \( R^* \) 使模型在测试集上性能最优。
- 规则配置 \( R_t = \{ (p_i^{(t)}, c_i, w_i^{(t)}) \}_{i=1}^N \)，其中 \( p \) 为子类别模式（粒子）、\( c \) 为实体标签、\( w \) 为置信权重。
- 优化目标基于验证集性能最大化，使用F1分数。

#### 自适应滤波算法（四步迭代）

1. **初始化（规则提取）**：使用LLM从训练数据中提取初始粒子（子类别模式），并基于LLM内部信念分配先验权重（softmax归一化）。
2. **评估（ICL观测）**：每个粒子在验证子集上进行ICL推理，通过计算输出序列的token似然积（softmax后）作为观测性能。
3. **权重更新（贝叶斯后验）**：结合先验权重和观测似然 \( \exp(\beta \cdot y_i^{(t)}) \) 更新粒子权重。
4. **多层重采样与规则变异**：
   - **第一层**：基于性能阈值淘汰低权重粒子。
   - **第二层**：对保留粒子进行语义变异（精化、泛化、情境化），生成新粒子，权重基于LLM困惑度（perplexity）赋值。
- 迭代直到收敛，最终输出最优规则组合。

#### 关键公式（文字描述）
- 规则演化方程：\( R_{t+1} = f(R_t, u_t) \)，其中 \( u_t \) 为控制动作。
- 性能观测方程：\( y_t = h(R_t) \)。
- 权重更新：\( w_i^{(t)} \propto w_i^{(t-1)} \cdot \exp(\beta \cdot y_i^{(t)}) \)。
- 变异：使用LLM生成新的子类别模式，通过困惑度计算权重。

## 3. 实验设计

### 数据集
- **NER**：CoNLL-2003（新闻）、ACE05（新闻和对话）、GENIA（生物医学）
- **RE**：NYT（远程监督新闻）、CoNLL04（手动标注实体和关系）

### Benchmark与对比方法
- 基线方法：
  - **IO**：直接在原始LLM上运行，无任何示例或规则。
  - **CodeIE**：基于代码生成的示例选择方法。
  - **GuideNER**：当前NER SOTA，使用LLM生成的注释指南（仅限NER任务）。
- 所有方法均使用**纯上下文学习**，不涉及微调或链式思维。

### 模型与配置
- 四种LLM：Qwen2.5-3B、Qwen2.5-7B、Llama3.1-8B、Pixtral-12B
- 温度设为0.0，随机种子42，评估模式（eval mode）确保确定性。

## 4. 资源与算力
- 论文提到实验在配备**H100 GPU**的计算集群上进行，使用PyTorch 2.6.0和transformers 4.51.3。
- **未明确说明GPU具体数量、训练时长、总计算开销**。仅提到使用了集群进行加速，未提供详细资源统计。

## 5. 实验数量与充分性
- 实验涵盖5个数据集（3个NER + 2个RE）、4种不同规模/架构的LLM，共20组主实验结果（Table 1）。
- 参数敏感性分析：探索了上下文窗口长度（1-15句子）和训练数据量（100-5000样本）对性能的影响（图4）。
- 文中提到由于ICLR各组件紧密耦合，无法进行传统消融实验，因此用参数分析替代。
- **充分性评价**：总体实验覆盖面较广，对比方法包括当前主流ICL基线（IO、CodeIE、GuideNER）。但缺少与更多先进IE方法（如微调模型、基于检索的ICL）的对比，且无消融研究，对方法各贡献的分离验证不足。此外，评估指标仅为F1，未报告精确率、召回率或方差。

## 6. 主要结论与发现
- ICLR在所有任务上均优于基线方法，NER任务相对提升7.7%~18.1%，RE任务提升显著（最高达87%）。
- 参数规模不直接决定性能：Pixtral-12B性能不如Qwen2.5-7B，暗示训练数据质量和架构更重要。
- ICLR在训练数据量较小时即可快速收敛（100样本即达接近最优性能），资源效率高。
- 上下文窗口长度以4-9句子为佳，过长导致权重平均化，性能下降。
- 与GuideNER相比，ICLR可适用于RE任务，而GuideNER仅限NER。

## 7. 优点
- **理论创新**：首次将控制理论引入ICL规则优化，提供系统化框架。
- **通用性**：方法同时适用于NER和RE，无需针对不同任务调整。
- **数据效率**：仅需少量训练样本即可达到高性能（如100样本即接近饱和）。
- **计算友好**：无需额外模型训练，token消耗与GuideNER相近（~500 tokens），远低于CodeIE（~1172）。
- **快速收敛**：参数分析显示性能在迭代中快速稳定。

## 8. 不足与局限
- **消融缺失**：由于组件耦合，未提供消融实验，难以评估各步骤的独立贡献。
- **评价指标单一**：仅报告F1，无精确率/召回率、方差、统计显著性（仅在表格中标注p<0.05，但未详细说明）。
- **基线覆盖有限**：未与近期其他ICL优化方法（如基于检索的、基于强化学习的）或微调模型对比；也未与基于规则的传统方法比较。
- **实验规模**：仅测试了四种模型，且均为开源模型；未在更大规模（如GPT-4级别）或不同语言上验证。
- **资源细节不清**：未提供GPU数量、训练时间、总能耗等，可复现性受限。
- **收敛速度假设**：尽管声称快速收敛，但未给出具体迭代次数或收敛曲线（仅参数分析片段）。
- **应用限制**：方法依赖LLM生成初始规则和变异，可能受LLM自身偏见和知识边界影响。

（完）
