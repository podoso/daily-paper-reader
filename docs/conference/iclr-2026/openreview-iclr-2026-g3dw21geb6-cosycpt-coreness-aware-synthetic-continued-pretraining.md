---
title: "CosyCPT: Coreness-Aware Synthetic Continued Pretraining"
title_zh: CosyCPT：核心度感知的合成持续预训练
authors: "Wenlong Zhao, Shuang Yang, Abhishek Bhandwaldar, Eshwar Prasad Sivaramakrishnan, Seungwook Han, Shivchander Sudalairaj, Aldo Pareja, Krishnateja Killamsetty, Elvira Rui Xiong, Hao Wang, Kai Xu, Akash Srivastava, Andrew McCallum"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=G3dW21Geb6"
tags: ["query:llm"]
score: 6.0
evidence: 利用实体关系图核心度引导合成数据实现LLM高效微调
tldr: 针对合成持续预训练数据效率低的问题，本文提出CosyCPT，构建文档实体关系图并计算核心度，用于引导合成数据采样和增强，提升LLM领域适配效率。实验证明该方法在多个领域数据集上优于基线。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-g3dw21geb6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1445, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-g3dw21geb6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1370, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-g3dw21geb6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1450, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-g3dw21geb6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1558, \"height\": 1302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-g3dw21geb6/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1515, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-g3dw21geb6/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1279, \"height\": 507, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-g3dw21geb6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1451, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-g3dw21geb6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 995, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-g3dw21geb6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1236, \"height\": 246, \"label\": \"Table\"}]"
motivation: 现有合成持续预训练数据效率低，未考虑不同实体关系的重要性差异。
method: 构建实体关系图，计算核心度得分，指导合成数据采样和增强。
result: 在多个领域数据集上，所需合成数据量大幅减少，下游任务性能提升。
conclusion: 利用关系图核心度能有效提升合成持续预训练的数据效率。
---

## Abstract
Synthetic continued pretraining adapts LLMs to specific domains by fine-tuning them on synthetic data that augments real domain data. However, existing methods are often data-inefficient (requiring massive synthetic corpora to enumerate all relational facts) and fail to account for the relative importance of different entity relationships. In this paper, we propose coreness-aware synthetic continued pretraining (CosyCPT), a systematic pipeline that addresses both limitations. Our method (1) constructs a graph representation of entity relations in a document, (2) quantifies relation importance via coreness scores derived from the graph, and (3) leverages these scores to guide synthetic data sampling and augmentation for continued pretraining. We investigate four definitions of entity coreness and four formulations of relation coreness, verifying that multiple variants of coreness-aware sampling can outperform random sampling of augmented data for synthetic continued pretraining. We offer a mathematical analysis, proving that (1) given a learning budget, maximizing the expected accuracy on a query set about relational knowledge in a document collection is an NP-complete problem, (2) coreness-aware sampling is the optimal solution when each query examines one entity pair, and (3) coreness-aware sampling has a better upper bound for expected accuray than random sampling.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的中文总结。

### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：大型语言模型（LLM）在特定领域应用时，需通过“合成持续预训练”（Synthetic Continued Pretraining）来注入领域知识。现有方法（如EntiGraph）会穷举所有实体对来生成合成数据，导致数据效率低下，且忽略了不同实体关系在领域知识中的重要性差异。
- **动机**：现实领域中，实体关系的贡献不均（例如金融领域公司间的交易链路比总部位置更重要）。若统一采样，会浪费合成 token 并稀释训练信号。
- **整体含义**：本文旨在回答“如何根据实体关系对下游性能的贡献程度来更高效地采样合成数据”，从而提升域适应效率。

### 2. 论文提出的方法论：核心思想、关键技术细节与算法流程
- **核心思想**：利用图论中的“核心度”（coreness）概念，量化实体及实体关系的重要性，并以此指导合成数据的采样和增强，将训练聚焦于领域知识的结构核心。
- **关键技术细节**：
  - **实体关系图构建**：从源文档 \( D_{source} \) 中提取实体集 \( E \)，并通过 LLM 判断实体间是否存在显式关系，构建无向图 \( G=(V,E) \)。
  - **核心度挖掘**：
    - 计算**实体中心性**：采用度中心性、介数中心性、接近中心性、PageRank 中心性四种指标（见表1）。
    - 计算**距离**：通过 BFS 获取任意两实体间的最短路径距离 \( Dis(v_i, v_j) \)。
    - **聚合函数模拟关系核心度**：将实体中心性和距离组合成关系得分 \( S_{i,j} \)，探索四种聚合方式（见表2）：吸引力模型（中心性乘积/距离平方）、三元积（中心性*接近度开三次方）、调和平均与距离（2*距离/(1/中心+1/中心)）、最大中心性/距离。
  - **核心度感知采样**：根据 \( S_{i,j} \) 降序排列实体对，优先采样高得分对，并由 LLM 生成描述其关系的合成文本，直到达到 token 预算 \( B \)。
- **算法流程**（见 Algorithm 1）：
  1. 图构建：提取实体，构建图 \( G \)。
  2. 核心度挖掘：计算每个顶点的中心性，通过 BFS 枚举实体对并计算聚合得分，形成列表 \( S_{pairs} \)。
  3. 核心度感知采样：按得分排序，依次从 \( S_{pairs} \) 采样，生成合成文本并拼接成 \( D_{synth} \)。
- **理论证明**：
  - Theorem 1：最大化期望准确率问题是 NP-complete 的（当涉及 ≥3 个实体时）。
  - Theorem 2：当每个问题只涉及一个实体对（\( q_2=1 \)）时，按重要性选择 top-y 实体对是最优的。
  - Theorem 3：核心度采样比随机采样具有更好的期望准确率上界。

### 3. 实验设计
- **数据集**：QuALITY benchmark（长文本多项选择问答数据集），使用 Yang et al. (2024) 划分的数据，共 383,508 tokens，文档平均 4320 词。
- **评测场景**：
  - **闭卷**：模型仅根据文章标题和问题作答。
  - **开卷（RAG）**：检索相关文本片段（4个 passages）后拼接问题作答。
- **基准方法**：
  - Raw Document CPT（直接在原始文档上持续预训练）
  - EntiGraph CPT（随机均匀采样实体对生成合成数据）
  - 直接提示 Llama-3.1-8B-Instruct
- **评估指标**：Exact Match (EM)
- **实现细节**：
  - 教师模型：Qwen-3-32B（用于生成实体对和合成文本）
  - 学生模型：Llama-3.1-8B-Instruct
  - 训练框架：HuggingFace Trainer，超参数沿用 Yang et al. (2024)
- **补充实验**：在 BBH、GPQA、MMLU-Pro 上评估指令遵循能力（闭书设置）。

### 4. 资源与算力
- 文中**未明确说明**使用的 GPU 型号、数量及训练时长。
- 仅提及教师模型为 Qwen-3-32B，学生模型为 Llama-3.1-8B-Instruct，训练使用 HuggingFace Trainer。
- 可推测算力需求适中（8B 模型持续预训练），但具体资源消耗未公开。

### 5. 实验数量与充分性
- **实验数量**：
  - 主要结果（图2）：对比了五种方法在闭卷和开卷下，5 个 token 规模（1×,4×,16×,64×,256×）的准确率。
  - 消融实验（图3）：比较 4 种中心性度量 × 4 种聚合函数（共 16 种组合）相对随机采样的增益。
  - 指令遵循（表3）：在 3 个 benchmark 上对比 4 种方法。
- **充分性**：
  - 消融实验覆盖了主要的可设计空间，系统展示了 PageRank + 调和平均组合的最佳性能。
  - 主要结果在多个规模上稳定，且与随机采样对比公平（使用相同语料生成流程，仅采样策略不同）。
  - 但**仅在一个数据集（QuALITY）上验证**，域外泛化能力未知。指令遵循实验也仅测试闭书场景。
- **客观公平**：遵循公开脚本，控制实验变量，随机采样多次取平均（指令遵循实验）。

### 6. 论文的主要结论与发现
- 核心度感知采样**显著优于**随机采样：在闭卷设置下，CosyCPT 达到最高准确率；在开卷设置下，与 EntiGraph 持平或更优。
- 在多种中心性度量中，**PageRank 中心性**表现最佳且稳定；在聚合函数中，**调和平均与距离**取得最大且最稳定的提升。
- 核心度采样在不损害指令遵循能力的前提下提升了领域知识获取效率。
- 理论证明：最大化期望准确率为 NP-complete；当问题仅涉及一个实体对时，核心度采样最优；核心度采样具有更优的期望准确率上界。

### 7. 优点
- **方法创新**：首次将图论核心度（多个中心性度量）引入合成持续预训练采样，提供了系统理论分析（含 NP-completeness 证明和上界分析）。
- **数据效率提升**：通过聚焦重要关系，减少了冗余合成 token，在同样 token 预算下获得更高准确率（图2显示 4% 提升）。
- **消融实验全面**：广泛探索了中心性度量与聚合函数的组合，为实践提供了清晰的推荐（PageRank + 调和平均）。
- **代码和提示词公开**（将在接受后发布），有利于复现。

### 8. 不足与局限
- **领域覆盖面窄**：仅在一个 QA 数据集（QuALITY）上验证，缺乏对更多领域（如金融、医疗、科学）的评测，泛化性存疑。
- **计算资源未明确**：缺乏 GPU 型号、训练时间等信息，不利于评估实际部署成本。
- **依赖 LLM 提取质量**：实体提取和关系判断均依赖外部 LLM（Qwen-3-32B），该过程可能有噪声或偏差，影响图构建质量。
- **理论假设较强**：理论分析假设问题仅由成对关系组成，且学习是二值的（学会=正确，否则全错），忽略了模型部分学习、推理和猜对的情况。
- **聚合函数为启发式**：采用的四种聚合函数缺乏理论指导，可能不是最优形式，调参空间有限。
- **未与其他结构化合成方法对比**：未与 LinkQA、Active Reading 等工作对比，缺乏与同领域最新方法的横向比较。

（完）
