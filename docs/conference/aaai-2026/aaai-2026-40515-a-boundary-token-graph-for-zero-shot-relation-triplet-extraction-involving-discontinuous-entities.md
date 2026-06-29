---
title: A Boundary Token Graph for Zero-Shot Relation Triplet Extraction Involving Discontinuous Entities
title_zh: 面向含不连续实体的零样本关系三元组提取的边界令牌图
authors: "Kailun Lyu, Zehan Li, Fu Zhang, Jingwei Cheng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40515/44476"
tags: ["query:joint-mer"]
score: 8.0
evidence: 零样本关系三元组提取，处理不连续实体
tldr: 现有关系三元组提取方法假设实体连续，忽略了不连续实体情况。本文首次研究含不连续实体的零样本关系三元组提取，提出边界令牌图（BoG）框架。通过预测边界令牌间边构建图结构，将提取转化为路径预测问题。实验表明在不连续实体场景下大幅超越基线。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40515/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 880, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40515/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1799, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40515/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 845, \"height\": 395, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1745, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 801, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1847, \"height\": 1209, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1836, \"height\": 675, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 444, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1626, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40515/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 838, \"height\": 297, \"label\": \"Table\"}]"
motivation: 零样本关系提取中现有方法无法处理不连续实体。
method: 构建边界令牌图，通过边预测连接实体边界，并转化为路径预测。
result: 在含不连续实体的数据集上取得显著提升。
conclusion: 首次解决了不连续实体下的零样本关系提取问题，拓展了任务边界。
---

## Abstract
Zero-Shot Relation Triplet Extraction (ZSRTE) aims to extract head-tail entity pairs and their corresponding relations from sentences, where the relations available during inference are not seen during training. Existing methods typically assume that entities are continuous; however, in practice, entities can be discontinuous, which poses challenges to these approaches. To address this issue, we are the first to discuss and study the ZSRTE task involving discontinuous entities, and propose an innovative BoG framework, which is based on our proposed Boundary Token Graph structure. This method first predicts and adds edges between boundary tokens of (dis)continuous entities to construct a token graph, and then innovatively transforms the relation triplet extraction task into a process of finding paths in the graph. Additionally, we design a Boundary Token-Aware Prompt for each relation to further enhance the interaction between boundary tokens and relation semantics. Experimental results on four ZSRTE datasets—with or without discontinuous entities—consistently demonstrate that our method outperforms previous approaches, achieving state-of-the-art results.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）
- **研究问题**：零样本关系三元组抽取（Zero-Shot Relation Triplet Extraction, ZSRTE）旨在从句子中提取头尾实体对及其对应关系，且推理阶段的关系在训练阶段未见过。现有方法普遍假设实体是连续的，但在实际场景（如医疗、生物领域）中，实体常由多个不连续片段组成（例如“pain, particularly in head”中的实体“pain in head”），导致现有方法无法处理此类情况。
- **研究动机**：首次系统研究包含非连续实体的零样本关系三元组抽取任务，填补该方向空白。
- **整体含义**：通过提出新的图结构将三元组抽取转化为图路径搜索，为处理非连续实体提供了有效解决方案，显著提升了零样本设置下的泛化能力。

### 2. 论文提出的方法论
- **核心思想**：构建一个“边界令牌图”（Boundary Token Graph），图中顶点为句子中每个令牌与四种边界标记（左/右边界、头/尾实体）组合而成的标记令牌；通过预测顶点之间的有向边（共五类，分为Span-内部边和Span-间边），将关系三元组抽取转化为从源节点[CLS]到汇节点[SEP]的路径搜索问题。
- **关键技术细节**：
  1. **边界令牌感知提示（Boundary Token-Aware Prompt）**：为每个关系r设计包含关系描述和四个可学习边界令牌标记（[H], [/H], [T], [/T]）的提示，增强边界令牌与关系语义的交互。
  2. **编码**：将句子S与提示τr拼接，通过BERT-base编码获得令牌嵌入H_S和边界标记嵌入H_M。
  3. **顶点构造**：对句子中每个令牌t与四个标记m拼接，得到顶点集合V = {t ⊗ m}，并分为四个子集V[H], V[/H], V[T], V[/T]。
  4. **边预测**：对任意两个顶点vi, vj，使用两层FFN和sigmoid计算有向边概率pij = σ(FFN(vi)^T FFN(vj))，若pij ≥ 阈值δ则添加边。边类型包括Span-内部边（连接同一实体的左右边界）和Span-间边（连接同实体不同片段、或头尾实体之间）。
  5. **路径搜索**：使用BFS/DFS枚举所有从[CLS]（标记为[/H]）到[SEP]（标记为[T]）的路径，每条路径对应一个三元组。对于单三元组场景，选择平均概率最高的路径。
- **训练目标**：采用二元交叉熵损失，对Span-内部边和Span-间边分别计算后加权求和（α=0.5）。

### 3. 实验设计
- **数据集**：
  - **标准ZSRTE数据集**（无非连续实体）：Wiki-ZSL、FewRel。测试集设m ∈ {5,10,15}个未见关系，验证集固定m=5；使用5个随机种子划分，报告平均结果。
  - **含非连续实体的ZSRTE数据集**：人工构建的Disc-Wiki-ZSL、Disc-FewRel（约15%三元组含非连续实体）。另外从这些数据集中提取“仅含非连续实体”的子集（Only Disc）进行单独评估。
  - **非连续NER数据集**：ShARe 14（用于辅助验证非连续实体识别能力）。
- **基准方法（baselines）**：
  - 判别式方法：DSP、RSED、ZS-SKA、Re-Cent。
  - 生成式方法：TableSequence、RelationPrompt、ZETT、TAG。
  - 基于LLM的方法：MICRE（T5-3B、LLaMA-7B）、ChatIE（GPT-3.5-turbo、GPT-4o、DeepSeek-R1）等。
  - 非连续NER方法：Comb、Trans E、BART-based、MAC、W2NER、RerankNER等。
- **评估指标**：
  - 单三元组场景：准确率（Accuracy）。
  - 多三元组场景：微平均精确率（P）、召回率（R）、F1值。
  - 非连续NER任务：P、R、F1。

### 4. 资源与算力
- **论文未明确说明**使用的GPU型号、数量及训练时长。仅提到采用BERT-base（110M参数）作为骨干模型，未涉及更大的模型或分布式训练细节。因此无法定量总结算力消耗。

### 5. 实验数量与充分性
- **实验数量**：共开展以下实验组：
  - 在4个ZSRTE数据集（2个标准+2个人工构造）上进行m=5/10/15三个设置下的单/多三元组对比。
  - 在含非连续实体的子集（Only Disc）上进行单独评估。
  - 在ShARe 14上进行非连续NER任务对比。
  - 与8种LLM方法进行对比。
  - 在FewRel和Disc-FewRel上进行消融实验（5种变体）。
- **充分性与公平性**：实验覆盖了多种场景（无/有非连续实体、单/多三元组），对比了当前主流方法，消融实验验证了各组件的必要性。但人工构造的非连续数据集可能存在一定偏差；所有基线结果（除特别标注外）均使用原论文设置复现，尽量保证公平。整体而言实验设计较为充分，但仅限于英文数据集，未在中文或其他语言上验证。

### 6. 论文的主要结论与发现
- 所提出的BoG框架在四个ZSRTE数据集上均取得最佳性能，尤其是在含非连续实体的数据集上显著优于基线（如Disc-Wiki-ZSL的F1提升13~14个百分点）。
- 边界令牌感知提示和边界令牌标记对性能至关重要（消融后F1下降12~17个百分点）。
- Span-内部边和Span-间边分别对实体识别和关系确定起关键作用，缺失会导致性能严重下降。
- BoG在计算效率上优于生成式方法（如RelationPrompt、TAG、ZETT），可处理更多句子/秒。
- 即使在不含非连续实体的标准数据集上，BoG也达到或超越了SOTA（如FewRel m=15时Accuracy 32.89 vs 第二27.06）。

### 7. 优点
- **创新性**：首次将非连续实体纳入零样本关系三元组抽取任务，并创新性地将其转化为图路径搜索问题，避免了传统序列标注对连续性的强假设。
- **模块化设计**：边界令牌感知提示可灵活适应不同关系语义，图结构天然支持三元组的联合解码。
- **有效性**：在多个数据集上一致领先，尤其对非连续实体处理效果显著。
- **计算效率**：采用判别式方法，推理速度优于生成式方法，且参数量小（110M），适合实际部署。
- **消融充分**：通过细致的消融实验验证了各设计组件的必要性。

### 8. 不足与局限
- **实验局限性**：人工构造的非连续实体数据集（Disc-Wiki-ZSL/Disc-FewRel）仅近似真实场景，可能存在人工偏差；仅在英文数据集上测试，未覆盖多语言或跨领域场景。
- **未报告算力细节**：缺乏GPU型号、训练时间等资源使用信息，影响可复现性和效率对比。
- **阈值敏感性**：边预测阈值δ（intra=0.4, inter=0.3）需手动设定，未讨论其敏感性或自适应方法。
- **非连续NER任务表现**：在ShARe 14上略低于专门NER方法（如MAC、W2NER），说明图结构在纯粹识别任务上仍有改进空间。
- **模型规模单一**：仅使用BERT-base，未探索更大模型（如BERT-large、RoBERTa）或不同预训练策略对性能的影响。
- **应用限制**：当前方法假设单句子内的三元组提取，未考虑跨句或文档级关系；且零样本能力依赖于关系语义描述的质量。

（完）
