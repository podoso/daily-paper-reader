---
title: "SEAL-RAG: Loop-Adaptive RAG with On-the-Fly Entity Extraction and Fixed-k Gap Repair"
title_zh: "SEAL-RAG: 循环自适应RAG与实时实体抽取及固定k间隙修复"
authors: "Moshe Lahmy, Roi Yozevitch"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=QqjUfdPkkb"
tags: ["query:ie"]
score: 6.0
evidence: RAG中的实时实体与关系抽取
tldr: 当前RAG方法在多跳问答中难以构建精确证据链，SEAL-RAG提出一种无需微调的推理时控制器，在检索循环中执行实体锚定的（头、关系、尾）抽取并维护实体账本，通过范围充分性检查决定停止或修复。实验表明其有效提升了多跳精确度。该方法将实体关系抽取集成于RAG流程，为信息抽取与检索增强生成结合提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-qqjufdpkkb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1441, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-qqjufdpkkb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 832, \"height\": 1163, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-qqjufdpkkb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1460, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-qqjufdpkkb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1461, \"height\": 591, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-qqjufdpkkb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 906, \"height\": 398, \"label\": \"Table\"}]"
motivation: 现有RAG方法在多跳推理中缺失关键实体关系，需要动态修复。
method: 提出SEAL-RAG，在检索循环中实时进行实体关系抽取，构建缺失规范并触发微查询。
result: 实验表明该方法有效提升了多跳问答的精确度。
conclusion: 将实体关系抽取与RAG结合可显著改善多跳推理性能。
---

## Abstract
We propose SEAL-RAG, a training-free, inference-time controller (no fine-tuning
of retriever, reranker, or generator) for retrieval-augmented generation that targets
multi-hop precision. SEAL executes a fixed retrieval depth k (k = number of
passages retrieved per search/micro-query) in a Search → Extract → Assess →
Loop cycle. A scope-aware sufficiency check aggregates coverage, typed bridging,
corroboration/contradiction, and answerability signals to decide stop vs. targeted
repair. At each loop, SEAL performs on-the-fly, entity-anchored (head, relation,
tail) extraction, maintains a live entity ledger, and builds a gap specification (miss-
ing entities/relations) that triggers one micro-query per repair under the same top-k;
new candidates are merged via entity-first ranking (prefers passages anchoring
those entities) before a single final generation step. On a 1,000-example HotpotQA
validation subset in a shared setup, SEAL improves LLM-judged answer correct-
ness by +10–22 pp (k=1) and +3–13 pp (k=3) vs. SELF-RAG across backbones,
and increases evidence precision@k (gold-title precision) by +12–18 pp at k=3.
These gains are statistically significant (chi-square for correctness; paired two-sided
t-tests for precision/recall/F1; p<0.05). By keeping k fixed and bounding repairs
by T (maximum repair iterations), SEAL yields a predictable, bounded cost profile
while replacing distractors rather than broadening context.

---

## 论文详细总结（自动生成）

# SEAL-RAG：循环自适应RAG与实时实体抽取及固定k间隙修复

## 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大型语言模型（LLM）在知识密集型任务中依赖参数化记忆易产生幻觉，检索增强生成（RAG）虽然引入外部证据，但传统流水线在初始检索缺失关键衔接时无法修复，简单增加检索数量（k）或堆叠上下文反而增加干扰信息与成本。
- **核心问题**：多跳（multi-hop）问答中，如何在不增加检索深度（固定k）的前提下，精准定位并修复缺失的实体或关系证据，同时保持可预测的推理成本。
- **整体含义**：提出一种无需训练、仅在推理时运行的控制器SEAL-RAG，通过循环式搜索、实体抽取、充分性评估、定向修复，在固定检索预算下提升多跳精确度，替代了依靠扩宽上下文或依赖模型反思的现有方法。

## 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将RAG流程改造为“搜索→抽取→评估→循环”（Search→Extract→Assess→Loop），保持每次检索的passage数量k固定，通过实时实体锚定（头实体、关系、尾实体）抽取构建“间隙规范”（gap specification），然后发出一个微查询（micro-query）定向修复，并用实体优先排序（entity-first ranking）替换干扰项而非扩宽上下文。
- **关键技术细节**：
  - **循环控制器**：维持固定检索深度k，循环至多T次。初始化时检索k个片段，抽取初始实体，建立阻塞列表（避免冗余）。
  - **范围感知充分性检查**：聚合四个轻量信号：问题属性覆盖度、类型化桥接（多跳链接）、证据间的证实/矛盾、答案可能性。当所有信号超过固定阈值时停止，否则修复。
  - **循环自适应实体抽取**：对检索到的片段执行（头、关系、尾）三元组抽取，并维护实时实体账本，仅存储逐字三元组以稳定接地。
  - **微查询策略**：每个修复循环仅发出一个微查询（仍在相同k下），利用阻塞列表、卡住检测、安全枢轴等机制避免冗余。
  - **实体优先排序**：新候选片段与现有片段合并时，优先选择包含账本中实体且能通过逐字支持解决缺失属性的片段，从而替换干扰项。
- **成本轮廓**：检索/读取预算为O(k·T)，为可预测的有界成本。

## 实验设计：数据集、场景、基准、对比方法

- **数据集**：HotpotQA验证集（fullwiki设置），随机种子采样1,000个问题（包含桥接和比较类型）。
- **场景**：多跳开放域问答，要求短答案（2-4词）并引用支持信息，否则输出“I don’t know”。
- **基准对比方法**：主要对比SELF-RAG（一种领先的反射式控制器）。两者在相同环境（相同LLM backbone、相同密集检索器、相同解码参数、相同评价指标）下比较，并控制检索深度k和循环预算一致。
- **其他对比**：论文在相关工作中提及CRAG、Adaptive-RAG、ReAct等，但未在实验中直接对比（仅与SELF-RAG并列），实验聚焦于SEAL-RAG与SELF-RAG的差异。

## 资源与算力

- **论文未明确说明**：文中未提及使用的GPU型号、数量、训练时长等信息。由于SEAL-RAG是无需训练的推理时控制器，其计算开销主要体现在LLM推理和检索上。作者仅在实验设置中指出使用“identical LLM backbones”（如gpt-4o等）和“cosine-similarity vector index with 1536-d embedding”，但未给出具体硬件配置或运行时间。因此无法评估资源需求。

## 实验数量与充分性

- **实验组数**：
  - 主实验：分别在k=1和k=3下，使用4个LLM backbone（gpt-4o-mini、gpt-4o、gpt-4.1-mini、gpt-4.1），共8组结果（每个表格8行，含SELF-RAG和SEAL-RAG的对比）。
  - 消融实验：在固定k=1下，改变循环预算L∈{0,1,3,5}，在4个backbone上报告Judge-EM，共16个数据点（含L=0基线）。
  - 统计显著性测试：对主结果进行卡方检验（Judge-EM）和配对t检验（精确率/召回率/F1），并采用Holm-Bonferroni校正（α=0.05），验证差异显著。
- **充分性评价**：实验设计较为充分：
  - 控制了所有共享变量（backbone、检索器、索引、解码、评价指标），仅改变控制逻辑，确保公平比较。
  - 覆盖了不同LLM容量（小型和大型）和不同检索深度（k=1和k=3）。
  - 消融实验有效隔离了循环预算的影响，揭示了从L=0到L=1的巨大跳跃及后续递减收益。
  - 提供了定性案例和失败模式分析，增强了结果解释力。
  - 局限：仅在一个数据集（HotpotQA）上验证，且仅对比SELF-RAG一个强基线，未与更多方法（如CRAG、Adaptive-RAG、IRCoT等）比较，可能遗漏其他更优方案。另外，实验基于1k子集而非全验证集，泛化性需关注。

## 论文的主要结论与发现

- **主要结论**：SEAL-RAG在固定k下，通过实体锚定的间隙修复，在HotpotQA上显著优于SELF-RAG：
  - 在k=1时，Judge-EM提高+10~22个百分点，证据精确率提高+11~25个百分点。
  - 在k=3时，Judge-EM提高+3~13个百分点，证据精确率提高+12~18个百分点。
  - 所有差异在统计上显著（p<0.05）。
- **其他发现**：
  - 循环预算L从0到1带来最大收益（平均+35pp），之后收益递减，提示大部分增益来源于首次替换。
  - 当检索深度k增大或backbone更强时，SEAL的边际收益缩小，但始终为正。
  - 精确率的提升是核心驱动力：即使召回率偶有下降（如小模型在k=3），Judge-EM仍能上升，因为替换了更关键的缺失页面。

## 优点

1. **无需微调**：控制器完全在推理时运行，不修改任何模型参数，可直接应用于已有LLM和检索器。
2. **固定预算**：通过保持k固定并限制循环次数T，推理成本可预测，避免传统多跳检索的路径爆炸。
3. **精确修复**：实体锚定的抽取与间隙规范提供了明确的修补目标，而非模糊的上下文扩充，从而提高精确率并减少干扰。
4. **可解释性**：实时实体账本和逐字三元组存储使证据链清晰，便于验证。
5. **实验设计严谨**：共享环境、配对统计检验、消融实验和定性分析确保了结论的可信度。

## 不足与局限

1. **LLM评价偏差**：使用固定LLM评判最终答案的正确性（Judge-EM），而LLM评判可能存在位置偏好、措辞偏差等，论文虽通过固定解码、配对检验、提供逐项判断结果来缓解，但仍需谨慎解读小幅度差异。
2. **任务耦合限制**：实验限定于短答案（2-4词）的HotpotQA，不适用于需要长理由或开放式生成的场景，泛化性存疑。
3. **固定k策略**：实验仅在k∈{1,3}下进行，未探索动态k或更大k，虽然这是设计使然，但实际应用可能需要更灵活的预算分配。
4. **领域偏移**：仅在HotpotQA（Wikipedia域）验证，未在新闻、生物医学、法律等其他语料或BEIR基准上测试，结果可能不通用。
5. **Prompt敏感性**：系统依赖多组提示（充分性检查、抽取、微查询、排序、答案生成），更改模型或调整提示可能改变性能，论文虽固定了prompt并开源，但可迁移性需进一步检验。
6. **只对比一个基线**：虽SELF-RAG是强基线，但未对比更多同类方法（如CRAG、Adaptive-RAG、MAIN-RAG等），可能无法全面反映SEAL-RAG的相对优势。

（完）
