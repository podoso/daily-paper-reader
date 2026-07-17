---
title: "A Survey on MLLM-based Visually Rich Document Understanding: Methods, Challenges, and Emerging Trends"
title_zh: 基于多模态大语言模型的视觉丰富文档理解综述：方法、挑战与新兴趋势
authors: "Yihao Ding, Siwen Luo, Yue Dai, Yanbei Jiang, Zechuan Li, Qiang Sun, Geoffrey Martin, Wei Liu, Yifan Peng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.652.pdf"
tags: ["query:ie"]
score: 8.0
evidence: 基于多模态大语言模型的视觉丰富文档理解综述，涵盖信息抽取
tldr: 该综述全面回顾了基于多模态大语言模型的视觉丰富文档理解进展，涵盖基于OCR和无OCR的信息抽取方法、文本视觉布局特征融合技术、预训练与指令微调等训练范式，并展望未来研究方向。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.652/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.652/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1655, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.652/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 697, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 1286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1576, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1248, \"height\": 1646, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1091, \"height\": 1330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1656, \"height\": 600, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1656, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1656, \"height\": 591, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1674, \"height\": 1179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1447, \"height\": 1787, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.652/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1388, \"height\": 535, \"label\": \"Table\"}]"
motivation: VRDU需要自动解释包含复杂视觉、文本和结构元素的文档。
method: 综述MLLM在VRDU中的应用，聚焦特征集成和训练范式。
result: 系统总结了当前方法和挑战，指出未来方向。
conclusion: MLLM在VRDU中展现出巨大潜力，但仍需解决多模态融合等挑战。
---

## Abstract
Visually Rich Document Understanding (VRDU) has become a pivotal area of research, driven by the need to automatically interpret documents that contain intricate visual, textual, and structural elements. Recently, Multimodal Large Language Models (MLLMs) have demonstrated significant promise in this domain, including both OCR-based and OCR-free approaches for information extraction from document images. This survey reviews recent advances in MLLM-based VRDU, highlighting emerging trends and promising research directions with a focus on two key aspects: (1) techniques for representing and integrating textual, visual, and layout features; (2) training paradigms, including pretraining, instruction tuning, and training strategies. Moreover, we address challenges such as data scarcity, handling multi-page and multilingual documents, and integrating emerging trends such as Retrieval-Augmented Generation and agentic frameworks. Our analysis offers a roadmap for advancing MLLM-based VRDU toward more scalable, reliable, and adaptable systems.

---

## 论文详细总结（自动生成）

# 基于多模态大语言模型的视觉丰富文档理解综述：方法、挑战与新兴趋势

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：如何利用多模态大语言模型（MLLM）自动理解视觉丰富文档（VRDU），这类文档包含复杂的视觉、文本和布局结构（如发票、表格、学术论文等）。传统方法依赖手工规则或浅层深度学习，难以跨域泛化；多模态预训练模型虽有所改进，但受限于数据规模和多样性。
- **整体含义**：MLLM（如GPT-4V、LLaVA系列）凭借强大的视觉-语言联合表征能力和世界知识，在VRDU任务上展现出显著潜力。本文系统梳理了基于MLLM的VRDU框架，聚焦于两个方面：① 文本、视觉、布局特征的表示与集成技术；② 预训练、指令微调及训练策略。同时分析了数据稀缺、多页/多语言文档处理、RAG与Agent框架等挑战与趋势，为构建更可扩展、可靠、自适应的VRDU系统提供路线图。

## 2. 论文提出的方法论（核心思想、关键技术）

> 本文是综述，并非提出全新方法，而是系统归纳现有MLLM-based VRDU框架的技术路线。核心框架分为两大类：

### 2.1 框架架构
- **OCR-Dependent框架**：依赖外部OCR工具提取文本和布局信息（如边界框），典型模型包括DocLLM、LayoutLLM、LMDX等。优点是可利用预训练LLM直接处理结构化文本；缺点是OCR误差累积，且低分辨率输入可能限制表达能力。
- **OCR-Free框架**：端到端直接处理文档图像（如mPLUG-DocOwl、UReader、TextMonkey）。需高分辨率图像和视觉压缩模块（如Q-Former、Resampler、内容检测器）来保持细粒度特征；依赖大规模预训练/指令微调来学习文本识别，计算成本高。

### 2.2 多模态表示
- **文本模态**：OCR-Dependent方式将OCR文本直接嵌入LLM提示（如ICL-D3IE），或通过辅助编码器（如LayoutLMv3）增强表示；OCR-Free方式则通过训练文本识别/检测等目标从图像中隐式学习文本。
- **视觉模态**：低分辨率输入直接经视觉编码器提取嵌入；高分辨率输入需切分（如UReader的Shape-Adaptive Cropping）或双编码器设计。视觉特征压缩是关键挑战（如Token Filtering、聚类聚合）。
- **布局模态**：通过位置编码（2D PE）、提示内嵌（如量化坐标）、或训练任务（视觉定位、表格重建）来编码布局。
- **多模态融合**：包括神经融合（交叉注意力、LoRA）、目标导向融合（如文本识别+定位联合训练）、提示融合（如LayoutCoT链式推理）。

### 2.3 训练范式
- **预训练**：采用掩码建模、跨模态对齐、文本识别/检测/字幕等自监督任务；多数框架基于IIT-CDIP、RVL-CDIP等大规模数据集。
- **指令微调**：将VRDU任务（KIE、QA、分类）转化为指令-响应对，提升指令跟随能力和零样本泛化；常合成大规模数据集（如OCR+LLM生成）。
- **训练策略**：逐步训练，常见为冻结LLM/视觉编码器仅训练适配器，或逐步解冻；LoRA等轻量调优广泛使用。

## 3. 实验设计（数据集、基准、对比方法）

- **作为综述，本文未进行新实验，但系统收集并对比了多个已有模型的benchmark表现**。
- **数据集**：
  - **KIE基准**：FUNSD、CORD、SROIE、DocILE、XFUND、KVP10k等，覆盖单/多页、单/多语言、开放类别。
  - **VQA基准**：DocVQA、ChartVQA、InfoVQA、MPDocVQA、DUDE、MMLongBench-Doc等，包含单/多页、多模态推理、长上下文。
- **对比方法**：表格9和10展示了通用MLLM（GPT-4V、Claude-3.5、InternVL2）、OCR-Dependent模型（DocLLM、LAPDoc、DoCo、LayoutLLM、PDF-WuKong等）、OCR-Free模型（KOSMOS-2.5、mPLUG-DocOwl系列、TextMonkey、Marten、PP-DocBee等）在多个基准上的性能（ANLS、F1等）。
- **主要发现**：
  - OCR-Dependent模型在FUNSD、CORD等结构清晰的数据集上仍占优（>80% F1）。
  - OCR-Free模型在DocVQA、ChartVQA等复杂视觉任务上快速追赶，最新模型（如Marten、TokenFD）已超越部分OCR-Dependent方法。
  - 多页任务（MPDocVQA、DUDE）上，OCR-Dependent方法（如GRAM、PDF-WuKong）仍领先，但OCR-Free方法（mPLUG-DocOwl2）进步显著。

## 4. 资源与算力

- **文中未明确提及具体GPU型号、数量或训练时长**，因为综述聚焦于方法分类而非复现实验。
- 但在部分框架描述中暗示：OCR-Free框架需要高分辨率图像+大量视觉token，导致更大计算开销；大规模指令微调（如使用LLM合成数据）和预训练（IIT-CDIP百万级）需要显著算力资源。

## 5. 实验数量与充分性

- **作为综述，验证了40+模型在10+基准上的性能**，对比范围广泛，覆盖单/多页、单/多语言、KIE/VQA任务。
- **充分性分析**：
  - **优点**：对比了不同技术路线（OCR-D vs OCR-Free）及不同LLM骨干（GPT、LLaMA、Qwen等）的表现，表格清晰，趋势明显。
  - **不足**：各模型训练设置（预训练数据、分辨率、优化器、batch size）未统一，直接对比存在不公平性（如有些模型报告了多模型集成结果）。部分模型仅在特定数据集上报告，缺失跨基准全覆盖。作者也承认这是定性分析，缺乏严格的消融和统计测试。
  - **结论**：实验覆盖全面但深度有限，更适合作为趋势概览而非严格竞技。

## 6. 论文的主要结论与发现

- **MLLM在VRDU上展示出强大潜力**，尤其OCR-Free方法通过端到端学习避免了OCR误差，在复杂场景（图表、手写）上更具优势。
- **多模态融合仍是核心挑战**，当前方法仍依赖启发式或粗粒度融合，缺乏对层级布局和空间关系的显式建模。
- **数据瓶颈突出**：合成数据虽降低人工成本，但存在噪声和分布不匹配问题；多页/多语言场景的数据标注和评估仍不足。
- **RAG和Agent框架是新兴趋势**：通过检索增强和工具调用（如PDF解析器、检索器）可提升准确性和可解释性，但当前检索-推理解耦、多智能体协调等问题亟待解决。
- **未来方向**：更高效的高分辨率处理、多页长期依赖建模、语言无关表示学习、强化学习与人类反馈、闭环推理与证据验证。

## 7. 优点（方法或实验设计的亮点）

- **系统全面性**：首次从框架架构、多模态表示、训练范式、推理提示、挑战趋势等维度完整梳理MLLM-based VRDU，覆盖OCR-D/OCR-Free两条路线。
- **分类清晰**：对文本/视觉/布局表示方法进行了细致分类（如布局的三种编码方式），便于读者快速定位技术差异。
- **数据集和基准的详尽罗列**：附录中给出了几乎所有主流KIE/VQA数据集的属性（语言、是否多页、标注格式等），极具参考价值。
- **趋势分析前瞻**：明确指出RAG、Agent、合成数据、多页等方向，并给出建设性挑战分析，对后续研究有指导意义。

## 8. 不足与局限

- **定性为主，缺乏严格定量比较**：未提供所有模型在统一设置下的复现结果，性能对比表中部分指标缺失（如表格9中很多模型未报告FUNSD或CORD分数），难以公平评判。
- **工业部署讨论缺失**：未涉及推理速度、内存占用、隐私合规等实际应用问题；多数讨论集中于学术基准。
- **时效性局限**：综述截至2026年，技术演进迅速（如更多OCR-Free模型发布），需持续更新。
- **多模态融合机制分析较浅**：仅列举了融合类型，未深入分析不同机制的优劣势和适用场景（如何时用LayoutCoT更好）。
- **未讨论模型幻觉问题**：MLLM在文本密集区域可能产生位置融合错位或内容虚构，文中未专门分析。
- **实验充分性受限**：部分模型仅基于单数据点报告，消融实验缺失，无法评估设计选择的贡献。

（完）
