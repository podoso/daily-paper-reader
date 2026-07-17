---
title: "SudokuFill: A Multi-Agent Progressive Filling Framework for Document-Level Scientific Information Extraction"
title_zh: SudokuFill：面向文档级科学信息抽取的多智能体渐进填充框架
authors: "Yang Li, Yajiao Wang, Yu Zhang, Yuanzhe Zhang, Maodi Hu, Mengting Zhang, Xi Sun, Hua Yue, Zhixiong Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1657.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 科学信息抽取
tldr: 科学信息抽取（SciIE）中，传统先局部抽取再全局组装的方式丢失全局关联。本文提出SudokuFill，将SciIE视为渐进填充问题，类似数独：高置信度字段作为约束指导后续填充。多智能体协作，在长文档和多模态场景中效果显著。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1657/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 788, \"height\": 813, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1657/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1607, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1657/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 779, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1657/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 766, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1657/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1612, \"height\": 763, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1657/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1593, \"height\": 2115, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1664, \"height\": 1210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1663, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1663, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1664, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 1335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1612, \"height\": 763, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1662, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1662, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1662, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1657/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1339, \"height\": 336, \"label\": \"Table\"}]"
motivation: 现有科学信息抽取方法因局部抽取而破坏全局相关性。
method: 提出SudokuFill框架，将抽取视为渐进填充，利用已抽取的高置信度字段作为约束指导后续抽取。
result: 在科学文献数据集上，SudokuFill优于传统流水线方法。
conclusion: 将信息抽取建模为渐进填充问题能有效利用全局约束。
---

## Abstract
Scientific information extraction (SciIE) is a key bottleneck for turning unstructured papers into computable knowledge bases, yet most existing systems still follow a “local extraction then global assembly” paradigm. This workflow is inherently lossy: by extracting fields in isolation, it breaks global correlations and discards high-confidence signals that could otherwise be reused as internal supervision, forcing systems to repeatedly restart from scratch, especially in long, multimodal scientific documents. In this paper, We propose a different view: SciIE should be solved as a progressive filling problem, similar to solving a Sudoku,once a field is filled with high confidence, it should act as a constraint that guides the remaining uncertain fields. Based on this idea, we introduce SudokuFill, a multi-agent framework that maintains a Global Filling State and performs priority scheduling to establish reliable anchors first, then reuses them as internal supervision for iterative deliberation over harder fields. Evaluated on a specialized document-level adjuvant dataset, our framework achieves a SOTA score of 51.83% on our benchmark. Crucially, SudokuFill enables a 7B model to outperform the vanilla GPT-4o, proving that structured architectural reasoning can effectively compensate for parameter scale.

---

## 论文详细总结（自动生成）

# 论文《SudokuFill：面向文档级科学信息抽取的多智能体渐进填充框架》详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：科学信息抽取（SciIE）旨在将非结构化的学术论文转化为可计算的知识库，是AI for Science的基础瓶颈。现有主流方法遵循“局部抽取→全局组装”范式：先将目标模式分解为独立的字段级子任务，逐字段从句子/段落中抽取候选值，再通过后处理组装成结构化记录。
- **缺陷**：该流程本质上有损——（1）人为割裂了字段间的全局相关性（如蛋白质功能注释中，结构域类型对活性位点有约束）；（2）丢弃了先前高置信度抽取结果作为内部监督的潜力，导致每字段、每文档从零开始，尤其面对长文档、多模态科学论文时错误率高。
- **动机**：作者将SciIE重新定义为类似数独的“渐进填充”问题：一旦某个字段被高置信度填充，它应作为约束指导后续不确定字段，从而利用结构化推理弥补模型参数规模的不足。

## 2. 方法论：核心思想、关键技术细节与流程

### 2.1 核心思想
- **SudokuFill**：一个两阶段多智能体框架，以全局填充状态为核心，通过优先级调度先建立可靠锚点，再迭代重用这些锚点作为内部监督，通过多轮辩论逐步填充较难字段。

### 2.2 关键技术细节

#### Stage I：字段优先级调度（Field Priority Scheduling）
- **输入**：原始PDF文档和预定义模式字段集。
- **过程**：
  1. **查询实例化**：将每个模式字段 \( f \) 转化为查询单元 \( q = \langle f, \phi(f) \rangle \)，包含字段定义和抽取约束。
  2. **页面探针**：基于MLLM的页面智能体并行扫描各页，对每个查询输出三元组（候选值V，置信度C，证据定位E），形成页面-查询矩阵M。
  3. **排序**：排名智能体根据三个信号输出执行顺序π：MaxConf(q)（页级最大置信度）、Part(q)（有效参与页数，C>0.5）、模式隐含字段依赖关系，实现“从易到难”调度。
- **输出**：优先查询序列及初始候选池，为Stage II提供热启动。

#### Stage II：多智能体辩论抽取（Multi-Agent Debate Extraction）
- **角色定义**：
  - **页面智能体**：基于自己分配的页面提出或修订候选值，输出(V, C, E)。
  - **行约束智能体**：查阅全局填充状态G，从已有候选中选择支持或挑战的值（不引入新值）。
  - **列约束智能体**：相似地提供列级结构信号（格式、别名、单位一致性等）。
  - **协调智能体**：不直接预测值，负责汇聚证据、跟踪支持/反对、更新候选池和历史记忆，并选择下一轮辩论模式。
- **迭代协议**：每轮中协调器构建上下文（当前查询q、候选池、历史摘要H、全局状态G），各智能体并行响应。约束智能体仅对现有候选发表意见。协调器更新候选池和历史记忆，实现跨轮重用（同一查询历史）和跨查询重用（高置信度结果写入G）。
- **自适应辩论模式**（防止过早偏见）：
  - **常规辩论**：默认模式，所有智能体参与。
  - **反偏见辩论**：当主导候选反复被支持但存在持久的、有证据支持的异议时，优先直接处理异议。
  - **重新思考**：当主导候选仅来自单一页面或单一智能体时，要求其他页面智能体查证/反驳。
- **收敛判据**：基于时间趋势而非跨智能体置信度比较——主导候选连续多轮不变、各智能体自身置信度更新趋于零、无未解决异议。

### 2.3 算法流程（文字说明）
1. Stage I：对每个文档，为每个字段创建查询，并行执行页面探针，构建矩阵M；计算每查询的MaxConf和Part；排名智能体根据这些信号和依赖关系输出调度序列π，同时初始化候选池。
2. Stage II：按顺序处理每个查询q∈π。初始化候选池为Stage I的热启动候选。每轮：协调器构建上下文→所有智能体并行输出→协调器汇聚更新候选池和历史→根据历史选择下一轮模式→检查收敛。收敛后输出最终值并写回全局状态G，约束后续字段。

## 3. 实验设计

### 3.1 数据集与基准
- **疫苗佐剂基准（Vaccine Adjuvant Benchmark）**：首个文档级佐剂信息抽取基准，包含250篇科学论文、超过1000条注释记录，10个异构字段（Adjuvant_Name, Category, Sub_type, Composition, Morphology, Particle_Size, Particle_Structure, Target, Target_Cell, Combination_mode）。输入为原始PDF，需要多页综合和多模态信号（表格、图片）集成。
- 与其他数据集对比（表C.1）：本数据集在文档级别、测试样本数和字段数上具有竞争力。

### 3.2 对比方法
- **闭源多模态大模型**：GPT-4o, GPT-5 Nano, Gemini-1.5 Flash, Claude-3 Haiku。
- **开源多模态大模型**：Qwen2-VL (72B), Intern-VL2 (40B/8B), LLaVA-v1.5 (7B), Qwen-VL-Chat (7B), Qwen2.5-VL (7B), DeepSeek-VL-Chat (7B), Phi3-Vision (7B)等。
- **SciIE相关专用模型**：LLM-NERRE, Eunomia, BioWorkflow（均基于7B模型）。
- **基线实现**：所有MLLM基线采用固定顺序的串行抽取策略（无优先级调度），专用模型遵循原始协议。

### 3.3 评价指标
- **实体级**：Precision, Recall, Micro F1。
- **行级**：Row-level Accuracy, Row-level F1（要求核心属性正确分组）。
- **总体**：实体级F1和行级F1的算术平均。

## 4. 资源与算力

- **未明确说明**：论文中未提供具体的GPU型号、数量、训练时长或推理基础设施细节。仅提及使用了不同参数规模的模型（如7B、GPT-5 Nano等），但未披露实验的硬件配置。因此无法评估计算成本。后续研究者需依据自身资源复现。

## 5. 实验数量与充分性

- **实验丰富**：
  - **主实验结果**（表1）：涵盖19种方法（含3种SudokuFill变体），对比多个维度。
  - **重用与辩论交互分析**（表2）：6种设置，重复3次统计均值与标准差，总共18次运行。
  - **消融实验**（表3）：4类共8种变体（含随机种子和固定顺序），全面测试调度、重用、辩论、约束智能体的影响。
  - **域感知提示 vs 规则无关提示**（表4）：对比两种设置，3种骨干。
  - **测试时扩展分析**（图3）：3种骨干×5个预算水平。
  - **置信度阈值选择**（图4）：9个阈值遍历。
  - **额外验证**：在MaterialIE2数据集上评估（表D.1），弱骨干评估（表D.2），排序稳定性分析（表D.3）。
- **充分性与公平性**：
  - 使用固定种子和多次重复（表2、消融变体）确保统计可靠性。
  - 基线实现标准化（固定顺序、相同骨干对比）以减少偏差。
  - 但数据集仅涵盖疫苗佐剂领域，泛化性有待验证；未在多个不同科学领域（如材料、化学）上大规模验证。

## 6. 主要结论与发现

1. **有效性**：SudokuFill在所有骨干上一致提升性能，特别是7B的Qwen2.5-VL版以48.28%总体F1超越原始GPT-4o（47.72%），证明结构化推理可补偿参数规模。
2. **行级提升显著**：SudokuFill显著缩小了实体级与行级指标间的差距（表1中GPT-5 Nano版行级准确率34.38%，比原始高8.08百分点）。
3. **重用与辩论协同**（表2）：重用有效性依赖于足够强的多轮辩论，单独使用任一组件效果有限。
4. **消融分析**（表3）：优先级调度提供稳健性（整体下降~1.5%），但跨查询重用和多智能体辩论都是关键；同时移除行和列约束智能体影响最大。
5. **域感知提示非必需**（表4）：即使无域特定规则，SudokuFill仍保持竞争力，表明框架可泛化。
6. **测试时扩展**（图3）：增加推理预算（token/智能体调用）单调提升性能，且较小模型通过更多迭代可逼近大模型。
7. **阈值稳健**：置信度阈值0.5为最优，且在0.3~0.9范围内性能相对稳健。

## 7. 优点

- **问题重构创新**：将SciIE重新定义为数独般的渐进填充，抓住了字段间内在依赖和信号重用的本质，突破传统流水线思维。
- **多智能体架构设计精巧**：三角色分工（页面、行约束、列约束）+ 协调器，可自适应切换辩论模式（常规、反偏见、重新思考），避免早期多数偏见和单来源幻觉。
- **全局状态演变**：跨查询、跨文档重用高置信度结果，实现动态约束传播，而非静态知识库。
- **实验全面且可重复**：包含消融、交互分析、阈值分析、测试时扩展、跨骨干验证，并提供详细提示（附录），便于复现。
- **实际价值**：在缺少系统数据库的疫苗佐剂领域构建首个基准，并证明较小模型可通过架构推理超越大型闭源模型，具有成本效益。

## 8. 不足与局限

- **计算开销**：多轮智能体交互和迭代重用导致显著的推理时间增加，不适合低延迟/严格预算的应用场景。
- **错误传播风险**：早期字段的高置信度错误会被强化并传播至后续字段，尽管辩论可缓解但未完全消除。
- **领域单一性**：仅在疫苗佐剂领域评估（虽然附录在MaterialIE2上验证，但仅一个额外数据集），通用性有待验证。不同科学子领域的文献风格、字段特性可能影响框架适用性。
- **基线与公平性**：基线MLLM采用固定顺序串行抽取，可能未充分探索这些模型本身对全局推理的潜力；与SciIE专用模型对比时，未完全对齐参数规模（如Eunomia仅7B，但GPT-4o为一般模型）。
- **缺少资源细节**：未报告GPU型号、训练/推理硬件、成本等，不利于实用性评估。
- **数据标注成本**：基准构建依赖六位博士级领域专家的六个月双盲标注与仲裁，构建成本高，可能限制扩展。

（完）
