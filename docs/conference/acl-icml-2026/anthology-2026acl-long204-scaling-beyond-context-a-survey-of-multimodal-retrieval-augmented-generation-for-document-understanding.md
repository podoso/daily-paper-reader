---
title: "Scaling Beyond Context: A Survey of Multimodal Retrieval-Augmented Generation for Document Understanding"
title_zh: 超越上下文：面向文档理解的多模态检索增强生成综述
authors: "Sensen Gao, Shanshan Zhao, Xu Jiang, Lunhao Duan, Yong Xien Chng, Qing-Guo Chen, Weihua Luo, Kaifu Zhang, Jia-Wang Bian, Mingming Gong"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.204.pdf"
tags: ["query:multimodal"]
score: 6.0
evidence: 多模态检索增强生成用于文档理解的综述
tldr: 文档理解面临OCR流水线丢失结构细节和原生多模态大模型上下文建模困难等问题。本文系统综述了多模态检索增强生成（Multimodal RAG）范式，涵盖其架构设计、关键挑战和未来方向，为多模态文档智能提供了全面参考。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.204/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 700, \"height\": 1167, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.204/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 762, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.204/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 757, \"height\": 585, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.204/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 753, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.204/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 768, \"height\": 711, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 1488, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 813, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1659, \"height\": 1563, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1638, \"height\": 514, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1641, \"height\": 2302, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1638, \"height\": 2425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.204/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1639, \"height\": 2177, \"label\": \"Table\"}]"
motivation: 文档理解需要超越单一模态，多模态RAG是重要但缺乏系统梳理的方向。
method: 全面综述多模态RAG在文档理解中的应用，分析代表性方法和数据集。
result: 系统梳理了现有方法并指出开放问题。
conclusion: 多模态RAG是推动文档理解发展的关键范式。
---

## Abstract
Document understanding is critical for applications from financial analysis to scientific discovery. Current approaches, whether OCR-based pipelines feeding Large Language Models (LLMs) or native Multimodal LLMs (MLLMs), face key limitations: the former loses structural detail, while the latter struggles with context modeling. Retrieval-Augmented Generation (RAG) helps ground models in external data, but documents’ multimodal nature, i.e., combining text, tables, charts, and layout, demands a more advanced paradigm: Multimodal RAG. This approach enables holistic retrieval and reasoning across all modalities, unlocking comprehensive document intelligence. Recognizing its importance, this paper presents a systematic survey of Multimodal RAG for document understanding. We propose a taxonomy based on domain, retrieval modality, and granularity, and review advances involving graph structures and agentic frameworks. We also summarize key datasets, benchmarks, and applications, and highlight open challenges in efficiency, fine-grained representation, and robustness, providing a roadmap for future progress in document AI.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：文档理解在金融分析、科学发现等领域至关重要，但现有方法存在明显不足：基于OCR的流水线会丢失结构细节，而原生多模态大模型（MLLM）在处理超长文档（数百上千页）时受限于上下文窗口，易产生幻觉。检索增强生成（RAG）虽能利用外部知识，但文档的多模态特性（文本、表格、图表、布局等）要求更高级的范式——多模态RAG，以实现跨模态的统一检索与推理。
- **整体含义**：本文是第一篇系统连接多模态RAG与文档理解的综述，旨在通过构建分类体系、汇总方法、数据集、评价指标，为文档AI的未来发展提供路线图。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出基于三个维度的分类法——**领域开放性**（开放域 vs 封闭域）、**检索模态**（仅图像 vs 图像+文本）、**检索粒度**（页面级 vs 元素级），并分析图结构增强和智能体增强两类混合范式。
- **关键技术细节**：
  - **封闭域多模态RAG**：从单个文档中检索最相关页面，减少输入长度、缓解幻觉（如SV-RAG、FRAG）。
  - **开放域多模态RAG**：从大规模文档库中检索，构建知识库（如M3DocRAG、VDocRAG）。
  - **检索模态**：
    - 图像级检索：VLMs直接编码页面图像（如ColPali、VisRAG）。
    - 图像+文本级检索：结合OCR或摘要注释，通过置信度加权或模态联合选取得分融合（如ViDoRAG、SimpleDoc）。
  - **检索粒度**：
    - 页面级：整页作为一个单位（多数早期方法）。
    - 元素级：细粒度到表格、图表、文本块等，通过层次索引或两阶段流水线实现（如MG-RAG、VRAG-RL、RegionRAG）。
  - **混合增强**：
    - **图结构增强**：将文档建模为图（节点为模态/元素，边为语义/空间关系），通过图遍历检索（如HM-RAG、mKG-RAG、RECON）。
    - **智能体增强**：使用自主智能体分解查询、选择检索策略、融合证据并验证（如ViDoRAG、HM-RAG、Patho-AgenticRAG）。
- **公式与算法流程**（仅文字说明）：论文给出了检索和生成的通用形式化定义，包括图像检索、置信度加权融合、模态特定联合选取得分等公式，但未提供完整算法伪代码。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集与场景**：
  - 列出了24个常用数据集（表3），如DocVQA、InfoVQA、SlideVQA、MMLongBench-Doc、M3DocVQA、VisDoMRAG、OpenDocVQA等，覆盖文本、表格、图表、幻灯片等类型。
  - 四类场景：开放域/封闭域文档理解、单页/多页、视觉丰富文档QA。
- **Benchmark**：
  - 以DocVQA、SlideVQA、InfoVQA、MMLongBench-Doc为主要评测基准。
  - 评估分为检索评价（Top-K、Recall、MRR、nDCG）和生成评价（EM、ANLS、PNLS、G-Acc）。
- **对比方法**：
  - 检索方面：SV-RAG、DSE、VisRAG、CMRAG、ColPali、ColQwen2、VDocRAG、RegionRAG、HKRAG等。
  - 生成方面：VisRAG、FRAG、SV-RAG、CREAM、M3DocRAG、VisDoMRAG、FRAG、VDocRAG、VRAG-RL、SimpleDoc、CMRAG、MoLoRAG等。
  - 表4汇总了各方法在不同基准上的性能，提供了直接对比。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点
- **论文未明确说明训练/推理的GPU型号、数量或时长**。作为综述，它汇总了其他方法的结果，但原始方法论文可能各有不同，本文未进一步整合算力信息。仅提及部分方法使用了“Qwen2-VL-7B”等模型，但无具体资源细节。

### 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平
- **实验数量**：
  - 检索实验：在DocVQA、SlideVQA、InfoVQA、MMLongBench-Doc上进行了多指标对比（表4上部）。
  - 生成实验：在同一基准上对比了10+种方法（表4下部）。
  - 此外，附录A和表6提供了更全面的数据集描述；无单独的消融实验（因是综述）。
- **充分性与公平性**：
  - 覆盖了主流基准和方法，对比较为全面。
  - 评价指标多样（检索和生成），但部分方法使用不同指标（如ANLS vs G-Acc），导致直接比较时需对齐，作者已标注。
  - 原始论文可能存在数据泄露、超参差异等风险，本文未深入控制变量，故公平性受原始研究质量影响。整体上，实验总结具有代表性。

### 6. 论文的主要结论与发现
- 多模态RAG能有效解决OCR流水线丢失结构和MLLM上下文限制问题，在文档理解中展示出显著优势。
- 现有方法的发展趋势：从粗粒度（页面级）向细粒度（元素级）演进，从单模态向多模态融合，从静态检索向图/智能体增强的混合范式发展。
- 当前主要挑战：**效率**（视觉token存储与检索成本）、**细粒度表示**（缺乏对表格、图表等特定结构的专门建模）、**鲁棒性与安全性**（跨模态攻击、数据中毒、幻觉）、**基准与评价**（现有基准易饱和、数据泄露风险）。
- 实际部署中面临工程成本、延迟、数据治理等问题。

### 7. 优点：方法或实验设计上有哪些亮点
- **首次系统性连接**：填补了多模态RAG与文档理解之间综述的空白，此前文献多偏重于其中一方面。
- **多层次分类体系**：从领域、检索模态、检索粒度、混合增强四个维度组织文献，清晰揭示了技术演进路径。
- **全面的数据/基准汇总**：涵盖24个数据集，并提供了最新（2024~2025）方法的对比表，便于研究者快速把握现状。
- **深入讨论开放问题**：不仅总结成功，还专门分析了“OCR-Free vs OCR-Based”悖论、基准饱和、复杂性与实用性权衡等关键矛盾。
- **资源附录丰富**：包含评价指标、损失函数、图/智能体RAG详细讨论、行业部署分析等，极其实用。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验覆盖有限**：作为综述，未进行自身实验，对比结果直接引用原始论文，可能存在超参、训练细节不一致导致的偏差。
- **部署分析仍初步**：虽补充了行业实践，但关于用户中心评估、系统集成、可扩展性等分析不够深入（作者在Limitations中承认）。
- **评价指标不统一**：不同方法使用不同评价指标（如ANLS、G-Acc、EM），导致表4中部分条目无法严格横向比较。
- **数据泄露风险**：文中指出许多公开基准可能被预训练数据污染，影响性能有效性评估，但未提出缓解措施。
- **未涵盖所有最新方法**：领域发展迅速，论文截止于2025年底，部分2026年更前沿的工作可能被遗漏（作者承诺通过开源仓库持续更新）。
- **缺乏实验成本分析**：未讨论不同方法所需的GPU/内存等资源，使得实践者难以权衡精度与开销。

（完）
