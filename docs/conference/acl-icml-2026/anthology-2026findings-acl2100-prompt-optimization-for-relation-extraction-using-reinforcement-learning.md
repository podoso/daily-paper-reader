---
title: Prompt Optimization for Relation Extraction using Reinforcement Learning
title_zh: 基于强化学习的关系抽取提示优化
authors: "Ying Liu (刘颖), Dong Shuai, Cui Zibo, TengQi Ye, Gang Wu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2100.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 关系抽取提示优化强化学习
tldr: 针对提示设计依赖领域专家经验和试错的问题，提出REPO框架，使用强化学习自动优化关系抽取的提示。将提示构建建模为结构化序列决策问题，通过与黑盒LLM交互优化提示质量，在低资源领域取得显著提升。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2100/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1338, \"height\": 712, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2100/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1775, \"height\": 739, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2100/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1366, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2100/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1184, \"height\": 901, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2100/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 590, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2100/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1304, \"height\": 787, \"label\": \"Table\"}]"
motivation: 提示设计在低资源关系抽取中至关重要但需要大量人工尝试。
method: 提出REPO框架，将提示构造建模为序列决策问题，用强化学习优化。
result: 在多个领域低资源场景下，自动化提示优于人工设计。
conclusion: REPO有效降低了关系抽取对人工提示设计的依赖。
---

## Abstract
Relation extraction is a fundamental task in information extraction. Still, existing supervised approaches rely heavily on large-scale annotated data, limiting their applicability in domain-specific and low-resource scenarios. Prompt-based methods with large language models provide a parameter-efficient alternative; however, their performance is susceptible to prompt design, which often requires extensive domain expertise and heuristic trial-and-error. We propose REPO, a reinforcement learning-based automated prompt optimization framework for domain relation extraction. REPO formulates prompt construction as a structured, sequential decision-making problem, optimizing prompt quality through interaction with a black-box LLM. To enable efficient and stable optimization, we introduce a two-stage framework comprising an initial prompt-construction stage that generates semantically grounded candidates and a DRL-based refinement stage that iteratively improves prompts within a constrained, domain-aware action space. We further design a composite evaluation metric that integrates extraction accuracy and semantic consistency to serve as a dense reward signal. Extensive experiments on multiple relation extraction datasets across medical, financial, legal, and news domains demonstrate that REPO consistently outperforms existing prompt-based methods and supervised baselines. Ablation studies further confirm the effectiveness and robustness of the proposed DRL-based prompt optimization strategy. Our code is available at https://github.com/dddong2-star/REPO .

---

## 论文详细总结（自动生成）

# 基于强化学习的关系抽取提示优化（REPO）—— 中文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

关系抽取（Relation Extraction, RE）是信息抽取的核心任务，广泛应用于知识图谱构建、问答系统等。然而，传统监督方法严重依赖大规模、高质量标注数据，在医学、金融、法律等低资源或领域特定场景下扩展性差。基于大语言模型（LLM）的提示（Prompt）方法提供了一种参数高效的替代方案，但提示设计高度依赖领域专家知识和人工试错，且LLM对提示措辞、结构、示例顺序极为敏感，微小的变化会导致性能大幅波动。现有自动提示生成方法缺乏对关系语义的显式建模，且采用无结构搜索策略，难以高效探索组合空间。因此，**需要一种结构化的、可控制的自动提示优化方法，以降低手工成本并提高领域关系抽取的鲁棒性**。

## 2. 方法论

### 核心思想
将关系抽取的提示构建建模为**结构化序列决策问题**，通过深度强化学习（DRL）与黑盒LLM交互，自动优化提示。提出两阶段框架REPO：
- **第一阶段：提示初始化（Prompt Initialization）** —— 利用LLM从示例中生成语义合理的候选种子提示，并通过复合指标REPQS筛选高质量提示，缩小搜索空间。
- **第二阶段：基于强化学习的提示优化（Prompt Optimization using RL）** —— 使用Double Deep Q-Network (DDQN)在受限的、领域感知的动作空间中迭代优化提示。

### 关键技术细节
- **马尔可夫决策过程（MDP）建模**：状态 \( s_t \) 由BERT编码当前提示的语义嵌入表示；动作空间 \( A \) 包含11种预定义的提示编辑操作（如添加实体类型、调整关系描述、增强输出格式等），分为7个类别；奖励 \( r_t \) 采用平均REPQS（\( M\text{-}REPQS \)），即多个样本上的平均评分。
- **复合奖励信号（REPQS）**：
  \[
  REPQS(p) = \alpha \cdot F1(y, y^*) + \beta \cdot Sim(y, y^*)
  \]
  其中 \( \alpha=5, \beta=1 \)。F1基于精确三元组（头实体、关系、尾实体）完全匹配计算；语义相似度 \( Sim \) 使用SBERT将实体和关系编码为向量，计算余弦相似度的最大值并平均。
- **DDQN优化**：采用双重Q网络缓解Q值过估计；经验回放池存储转移；ϵ-贪婪策略线性衰减（0.95→0.05）；在线网络和目标网络周期同步。
- **算法流程**：第一阶段使用启发式算法（Algorithm 1）迭代重写种子提示，每5轮重采样以保持多样性，当平均REPQS连续三轮变化小于0.05时早停。第二阶段DRL基于第一阶段输出的最佳种子提示进行精细化编辑。

## 3. 实验设计

### 数据集与场景
四个中文领域数据集：
- **CMeIE**（医疗）：864例，关系类型——病因、药物治疗、临床表现。
- **FinCUGE**（金融）：1,219例，关系——合作、拥有。
- **LexEval**（法律）：497例，关系——贩毒、贩卖人口、非法窝藏、持有。
- **LCN**（新闻）：1,953例，关系——供应商、生产、构成。

所有数据集按 **1:1:8** 划分为训练、验证、测试集（低资源设置）。

### Benchmark与对比方法
- **提示基线**：APE（自动模板生成）、OPRO（LLM作为优化器）、SPO（自监督提示优化）——均基于GPT-4o。
- **监督基线**：CasRel（基于级联和残差的神经关系抽取模型）——基于BERT。
- **REPO变体**：REPO（GPT-4o）、REPO-FT（对Qwen2.5-7B-Instruct-1M进行LoRA微调）。

### 评估指标
精确率（P）、召回率（R）、F1分数（基于三元组精确匹配）。

## 4. 资源与算力

论文中未明确声明使用的GPU型号和数量。但提供了成本与时间数据（见表5）：
- **主实验（GPT-4o）**：第一阶段使用GPT-3.5-turbo（约2.7~3.4M tokens，3,000~4,500 API调用），第二阶段使用GPT-4o（约0.5~1.5M tokens，476~1,008 API调用）。总成本不超过50美元（实际$16~$41）。时间约20~30小时。
- **REPO-FT**：未报告具体GPU成本，但LoRA微调通常需要单GPU数小时。

总体而言，计算开销较小，**强调成本高效**。

## 5. 实验数量与充分性

- **主实验**：在4个领域数据集上对比了3个提示基线+1个监督基线+REPO两个变体，共计10个实验配置。
- **消融实验**（表4）：对比完整REPO与“Only Init”（移除RL阶段）和“Only RL”（移除初始化阶段），在4个数据集上均报告F1，共12个消融实验。
- **附加分析**：对LCN数据集进行了案例研究（附录A.1），跟踪提示变化过程；提供了成本分析（表5）。
- **公平性**：所有方法使用相同的数据划分和LLM（GPT-4o）评估；超参数固定。监督方法CasRel使用BERT，但标注数据量少，公平对比了低资源场景。

**评价**：实验较充分，覆盖多领域和多基线，消融验证了两阶段互补性。但存在局限（见第8点）。

## 6. 主要结论与发现

- **REPO在所有数据集上取得最佳F1**：LexEval 0.72、FinCUGE 0.60、CMeIE 0.58、LCN 0.56，比最佳提示基线（OPRO）高4~8%绝对值。
- **REPO平衡了精确率和召回率**，而OPRO/SPO往往高召回低精确。
- **两阶段互补**：初始化阶段提供好的起点，RL阶段进一步精细优化，缺一不可（消融实验F1下降0.02~0.07）。
- **低资源下优于监督方法**：CasRel在数据丰富时（LexEval）表现好（F1=0.64），但在其他数据集下降严重（0.32~0.45）；REPO性能更稳定。
- **REPO-FT（LoRA微调）进一步提升了F1**（平均提高4.7%），说明任务自适应参数调整可增强RL优化效果。
- **成本极低**：总API成本<$50，适合实际部署。

## 7. 优点

1. **创新性**：首次将强化学习系统应用于关系抽取的提示优化，将提示构建建模为结构化决策问题。
2. **方法设计合理**：两阶段框架有效缩小搜索空间、避免语义漂移；结构化动作空间（11种操作）结合领域知识，提高可解释性和稳定性；复合奖励REPQS结合精确匹配和语义相似度，提供密集信号。
3. **实验覆盖全面**：涵盖医疗、金融、法律、新闻四个差异大的领域，验证了跨域泛化性。
4. **成本效益显著**：极低的API调用量和成本（<$50），实用性强。
5. **开源代码**：提供GitHub仓库，可复现。
6. **鲁棒性分析**：消融实验和案例研究充分证明了各组件贡献。

## 8. 不足与局限

1. **模型泛化性有限**：主实验仅使用GPT-4o作为黑盒LLM，REPO-FT仅使用Qwen2.5-7B，未测试其他主流LLM（如Claude、LLaMA等），结论可能受单一模型影响。
2. **动作空间设计可能不完整**：11种编辑操作虽覆盖常见修改，但可能无法适应所有关系类型的特定需求，尤其高度复杂的领域（如法律中的嵌套关系）。
3. **数据集规模较小且均为中文**：最大数据集仅1953例，且全部为中文，未验证英文或其他语言场景。英文领域（如ACE、TACRED）的测试缺乏。
4. **基线对比的局限性**：监督基线仅采用了CasRel，未与更多现代监督方法（如Span-based、Seq2Seq）对比；提示基线只包括APE/OPRO/SPO，缺少对DPR、RLcf等最新方法的对比。
5. **奖励设计依赖SBERT**：语义相似度部分依赖于SBERT的质量，且固定权重α=5, β=1可能不是最优，未进行灵敏性分析。
6. **未进行统计显著性检验**：报告了数值优势，但未提供置信区间或p值，难以判断改进是否统计显著。
7. **低资源划分有意使训练集很小（10%数据）**，但未探索不同资源比例下的性能变化。
8. **REPO-FT的对比不公平**：REPO-FT使用了额外微调（LoRA），而基线提示方法未进行微调，直接比较可能高估其优势。论文也未比较REPO-FT与直接微调LLM而不使用REPO的效果。

（完）
