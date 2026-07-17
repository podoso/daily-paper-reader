---
title: ToMMeR - Efficient Entity Mention Detection from Large Language Models
title_zh: ToMMeR：从大语言模型中高效检测实体提及
authors: "Victor Morand, Nadi Tomeh, Josiane Mothe, Benjamin Piwowarski"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1268.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 命名实体识别：提及检测
tldr: "实体提及检测是信息抽取的基础瓶颈。本文提出ToMMeR，一个轻量级模型（<300K参数），从大语言模型早期层提取提及检测能力。在13个NER基准上零样本召回率达93%，并发现不同架构的LLM在提及边界上高度一致，表明提及检测是语言建模的自然涌现能力。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 790, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 703, \"height\": 1013, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 851, \"height\": 699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1270, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 751, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 653, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 786, \"height\": 653, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 821, \"height\": 670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 770, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 767, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1535, \"height\": 1485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1436, \"height\": 1065, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 605, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1672, \"height\": 944, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1268/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1645, \"height\": 1067, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1429, \"height\": 959, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 727, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1540, \"height\": 382, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1433, \"height\": 850, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1432, \"height\": 850, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1336, \"height\": 917, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1328, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1268/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 810, \"height\": 205, \"label\": \"Table\"}]"
motivation: 实体提及检测是信息抽取的性能瓶颈，现有方法效率低且依赖标注。
method: 设计轻量模型ToMMeR，从LLM早期层抽取提及检测信号，结合LLM法官协议提升精确率。
result: "零样本下在13个NER基准上实现93%召回率，扩展为分类头后达到竞争性性能。"
conclusion: 提及检测能力自然涌现于语言模型，可通过轻量模型高效利用。
---

## Abstract
Identifying which text spans refer to entities - mention detection- is both foundational for information extraction and a known performance bottleneck. We introduce ToMMeR, a lightweight model (<300K parameters) probing mention detection capabilities from early LLM layers. Across 13 NER benchmarks, ToMMeR achieves 93% recall zero-shot, with an estimated 90% precision under a human-calibrated LLM-judge protocol, showing that ToMMeR rarely produces spurious predictions despite high recall. Cross-model analysis reveals that diverse architectures (14M-15B parameters) converge on similar mention boundaries (DICE >75%), confirming that mention detection emerges naturally from language modeling. When extended with span classification heads, ToMMeR achieves competitive NER performance (80-87% F1 on standard benchmarks). Our work provides evidence that structured entity representations exist in early transformer layers and can be efficiently recovered with minimal parameters.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- 实体提及检测（Mention Detection）是信息抽取（IE）管线的基础任务，但已知是性能瓶颈（Popovic and Färber, 2024）。传统NER系统将提及检测与实体类型联合学习，导致检测与类型化耦合，限制了跨数据集的迁移能力。
- 已有证据表明，大语言模型（LLM）在预训练过程中可能隐式编码了实体跨度信息（Feng & Steinhardt, 2024; Geva et al., 2023; Morand et al., 2025）。因此，本文核心假设：**提及检测能力是语言建模目标的自然涌现产物，可以通过轻量探针从LLM的早期层中恢复，且无需微调整个模型**。
- 本文提出ToMMeR（Token Matching for Mention Recognition），一个参数不足300K的轻量模型，仅使用LLM单个前向传递中早期层的表示，即可高效、高召回地检测实体提及，并且天然支持零样本迁移。

## 2. 方法论

### 2.1 核心思想
- 基于**Binding ID**理论（Feng & Steinhardt, 2024）：LLM在内部通过类似注意力机制的信号将相关token动态绑定，实体提及的token间存在强绑定信号。
- ToMMeR学习一个轻量分类器，从LLM的隐藏状态中提取这些绑定信号，输出每个连续跨度是否为有效提及。

### 2.2 关键技术细节
- **输入**：冻结LLM某层的token表示序列 $[z^\ell_1, \dots, z^\ell_n]$。
- **匹配分数** $m_{ij}$：采用查询-键投影（$W_Q, W_K \in \mathbb{R}^{r \times d}$），对每对token $(i,j)$ 计算余弦相似度（替代传统softmax），以捕捉token间绑定强度。
  $$m_{ij} = \cos(W_Q z^\ell_i, W_K z^\ell_j) \in [0,1]$$
- **Token值** $v_i$：额外线性层 $W_V$ 输出标量，提供边界及锚点信息（尤其对自回归模型，最后一个token常集中实体信息）。
- **跨度概率**：利用 logistic 模型聚合以下特征：匹配分数 $m_{ij}$、跨度内部最大/最小匹配分数、最后token值 $v_j$ 及其下一个token值 $v_{j+1}$。共5个特征。
  $$\hat{p}_{ij} = \theta \cdot [m_{ij}, \max\{m_{kj}\}, \min\{m_{kj}\}, v_j, v_{j+1}]$$
- **损失函数**：平衡二元交叉熵（BBCE），通过动态类权重 $\alpha = \#Neg/\#Pos$ 处理严重类别不平衡。
- **两阶段训练**：1) 在Pile-NER标注数据上训练；2) **自蒸馏**：用当前模型预测未标注的提及（减少假阴性），再重新训练。

### 2.3 与现有方法的区别
- 不依赖提示或文本生成，仅需一次前向传递，比提示方法快42倍。
- 不要求输入schema，零样本迁移；而GLiNER需要推理时指定类型，EMBERT需要每个数据集有标注。

## 3. 实验设计

### 3.1 数据集与场景
- **主实验（零样本提及检测）**：13个英文NER基准，涵盖新闻、维基百科、科学/生物医学、工业等多领域：
  - MultiNERD, CoNLL 2003, CrossNER (5个领域), NCBI, FabNER, WikiNeural, OntoNotes, ACE 2005, GENIA NER。
- **多语言迁移**：WikiANN 涵盖英、西、法、德、中（拉丁语系转移良好，中文较差）。
- **LLM法官评估精度**：对MultiNERD和GENIA，使用gpt-4.1-mini判定ToMMeR预测跨度是否为合法实体，并标记人机一致性。
- **完整NER（外延实验）**：在CoNLL 2003, GENIA, MultiNERD, OntoNotes, NCBI 上添加分类头。

### 3.2 基准与对比方法
- 零样本提及检测：未直接对比（因为本文是首个做通用零样本提及检测的），但提供与标注集的对齐性能。
- 完整NER对比：GLiNER (2023)，EMBER (2024)（基于GPT2-xl），以及不同骨干的ToMMeR变体（LLaMA-3.2-1B/3B/8B, RoBERTa-base, BERT-base）。

### 3.3 评估指标
- 提及检测：Recall, Precision, F1（报告阈值解码和贪婪扁平解码两种模式）。
- 完整NER：微F1。

## 4. 资源与算力

- **训练**：在 Pile-NER 上训练ToMMeR（274K参数）使用单块 NVIDIA H100-80GB GPU，耗时约4小时（峰值显存6GB）。
- **评估与推理**：也使用 NVIDIA V100-32GB 进行。
- **多骨干实验**：训练了约20个不同LLM的ToMMeR模型（14M~15B参数），每个训练4小时，总GPU时数约80小时。
- **LLM法官**：使用gpt-4.1-mini API，消费约10k个跨度（$0.01级别）。
- **人类标注**：5名NLP领域研究者对1800个跨度进行标注，总耗时数人天。

## 5. 实验数量与充分性

- **实验数量**：非常丰富。
  - 零样本提及检测：13个英文基准 + WikiANN多语言（5种语言） + 2个LLM法官数据集，共约20个测试集。
  - 跨模型DICE分析：19个LLM，涵盖Pythia全系列、LLaMA、Mistral、Phi、BERT、RoBERTa、ModernBERT。
  - 层级分析：在Llama3.2-1B上每个16层分别训练模型并比较。
  - 消融实验：不同秩（rank 4~128）、不同架构变体（LTQK, LCAttn）。
  - 完整NER：5个基准 × 5个骨干（共25个配置）。
- **充分性**：实验设计系统，覆盖了多种规模、架构、领域、编码器-解码器及自回归/双向模型。消融分析充分。
- **客观性**：在零样本设置下，用LLM法官并配合人类标注进行PPI校正，有效避免了因基准标注不完整而低估精度的偏差。但是仅针对两个数据集做了人机校正，其他数据集仍存在低估精度的风险。整体实验设计公平、透明。

## 6. 主要结论与发现

- **高召回零样本**：ToMMeR在13个英文NER基准上平均召回率88.2%（阈值解码），其中MultiNERD达98.6%；使用贪婪扁平解码后平均召回率75.3%但精度提升至41.3%。
- **真实精度高**：LLM法官校正后精度约90%，证实绝大部分被基准标注为“负例”的预测实际上是合法实体（超出了原标注范围）。
- **跨架构收敛**：不同规模、家族的自回归模型（≥160M参数）在提及边界上达到DICE>75%，说明提及检测是语言建模的共享涌现能力。编码器模型（BERT等）略有不同，推测因双向注意力机制抑制了嵌套跨度。
- **早期层提取**：性能在LLM的第1层即接近最优，并保持稳定直至最后几层下降，表明实体信号在模型早期计算中已出现。
- **完整NER竞争力**：将ToMMeR扩展为分类头后，在CoNLL 2003达到84.8% (1B)~87.3% (RoBERTa)，接近SOTA（GLiNER 88.7%），而参数少得多。
- **效率**：推理速度比提示方法快42倍，适合实时流处理。

## 7. 优点

- **方法优雅简洁**：仅用<300K参数、单层线性变换，即可从任意识别器LLM中提取通用提及检测能力，无需prompting、生成或微调主干。
- **极强迁移性**：零样本跨领域、跨基准、跨语言（拉丁语系）表现优异；且能通过与标注的少量微调快速适应特定schema（如ACE 2005）。
- **评估严谨**：直面基准不完整问题，采用LLM法官+PPI校正+人类标注的三级验证，对真正精度有可靠估计。
- **实验覆盖广**：从14M至15B参数、从自回归到编码器、从通用到领域数据，全面验证了假设的普适性。

## 8. 不足与局限

- **基准不完整问题**：虽然使用LLM法官校正，但仅对两个数据集做了人类验证，其他11个基准的真实精度仍可能被低估。此外，Wikipedia的实体定义边界模糊，LLM法官存在positive bias（人类验证显示偏正）。
- **连续跨度假设**：模型仅检测连续token序列，无法处理不连续实体（如“New York ... City”分隔），这在某些语言现象和专门领域（如化学）中可能发生。
- **自回归模型无右侧上下文**：基于Llama等自回归骨干无法访问未来token，可能损失边界信息，尽管完整NER结果不错。
- **训练数据偏差**：Pile-NER来自GPT-3.5标注，继承了其标注偏好（如不包含代词、定冠词等），导致ACE 2005上召回率仅42%（ACE包含代词、 nominal mention）。虽可通过微调缓解，但零样本时对特殊schema不适应。
- **多语言中效果差**：对中文（非拉丁语系）仅41%召回，主要源于英语主导的tokenizer和预训练分布。
- **人类标注局限性**：GENIA领域（生物医学）专家知识不足，人机一致率偏低（κ=0.239），表明医学实体定义有歧义，影响了PPI置信区间的宽度。

（完）
