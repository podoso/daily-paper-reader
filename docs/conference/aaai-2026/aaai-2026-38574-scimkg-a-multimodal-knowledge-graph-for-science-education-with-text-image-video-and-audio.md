---
title: "SciMKG: A Multimodal Knowledge Graph for Science Education with Text, Image, Video and Audio"
title_zh: SciMKG：面向科学教育的多模态知识图谱（文本、图像、视频、音频）
authors: "Tong Lu, Zhichun Wang, Yaoyu Zhou, Yiming Guan, Zhiyong Bai, Junsheng Du"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38574/42536"
tags: ["query:multimodal"]
score: 6.0
evidence: 利用LLM构建多模态知识图谱，包含文本、图像、视频、音频
tldr: 针对多模态教育知识图谱构建依赖昂贵人工标注和多模态整合困难的问题，提出自动化框架，利用大语言模型从开放课程中增量提取和精炼学科概念，并通过验证-整合-增强流水线融合文本、图像、视频、音频，构建了首个大规模科学教育多模态知识图谱。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38574/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38574/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 790, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38574/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 621, \"height\": 228, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38574/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1413, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38574/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 605, \"height\": 484, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1849, \"height\": 693, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 817, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1424, \"height\": 631, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 460, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 864, \"height\": 109, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38574/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1205, \"height\": 533, \"label\": \"Table\"}]"
motivation: 构建多模态教育知识图谱需要大量人工标注且缺乏多模态整合。
method: 提出基于LLM的自动化框架，包含提取-验证-整合-增强流水线，融合多模态资源。
result: 构建了高质量的多模态教育知识图谱。
conclusion: 该方法为智能教育提供了结构化多模态知识表示。
---

## Abstract
Knowledge graphs (KGs) play a vital role in intelligent education by offering structured representations of educational content. However, constructing multimodal educational knowledge graphs (EKGs) from diverse open educational resources remains a challenge due to the reliance on costly manual annotations and the lack of multimodal integration. In this work, we propose an automated framework that harnesses the reasoning capabilities of large language models (LLMs) to construct multimodal EKGs from open courses efficiently. In our framework, an Extraction-Verification-Integration-Augmentation pipeline is designed to incrementally extract and refine disciplinary concepts from learning resources. Texts, images, videos and audios are aligned with their corresponding concepts. To ensure semantic consistency across modalities, we propose a cross-modal alignment method based on shared structural and semantic features. Using our framework, we build SciMKG, a large-scale multimodal EKG for Chinese K12 education in sciences (biology, physics, and chemistry), encompassing 1,356 knowledge points, 34,630 multimodal concepts, and 403,400 relational triples. Experimental results show that our method improves concept extraction F1 score by 9 % over state-of-the-art baselines; both automatic and human evaluations confirm the robustness of our multimodal alignment method. SciMKG and our construction toolkit will be publicly released to support further research and applications in AI-driven education.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，现根据您提供的论文内容，进行如下结构化、深入、客观的总结。

## 论文分析总结：SciMKG：面向科学教育的多模态知识图谱

### 1. 核心问题与整体含义（研究动机和背景）

*   **研究动机**：知识图谱（KGs）在智能教育中至关重要，但现有教育知识图谱（EKGs）的构建存在两大关键挑战：
    1.  **依赖昂贵的人工标注**：传统EKGs严重依赖人工标注数据和训练的深度学习模型，成本高、适应性差、存在主观偏差。
    2.  **模态不完整**：大多数EKGs仅基于文本，无法有效支持多模态教育应用（如基于图、视频、音频的问答）。尽管有工作尝试整合多模态，但通常将多模态知识转为文本，或依赖人工标注进行对齐，且局限于通用领域。
*   **整体含义**：本文旨在解决自动化构建大规模、高质量、多模态EKGs的难题，通过利用大语言模型（LLM）的强大推理能力，提出一个端到端的自动化框架，并构建了首个覆盖文本、图像、视频和音频四种模态的科学教育知识图谱 **SciMKG**，以推动AI驱动教育的发展。

### 2. 方法论：核心思想与关键技术细节

本文的核心思想是**利用大语言模型（LLMs）的推理能力，设计一个自动化流水线，从多模态教育资源中提取、精炼并整合学科概念，并实现跨模态语义对齐**。

*   **整体框架（四步流水线）**：
    1.  **数据采集与预处理**：从MOOC等开放教育平台获取视频、幻灯片、习题等资源。从视频字幕中提取文本，从幻灯片中提取图像，并利用多模态大语言模型（MLLMs）对文本进行重写并生成对应的音频。
    2.  **概念提取（核心）**：提出“**提取-验证-整合-增强**”流水线。
        *   **提取**：引导LLMs理解文本语法结构，识别名词和名词短语作为候选学科概念。
        *   **验证**：采用迭代的**SELF-REFINE**策略，让LLMs自我检查和修正，剔除学科歧义的概念。
        *   **整合**：设计了一个基于投票的**自洽性（Self-Consistency, SC）** 机制，整合多个LLMs（如GPT-4o, Gemini-1.5-flash, DeepSeek-V3）的输出。一个概念只有当其`SC-Score G(ci)`（即所有LLM投票分数的总和）超过设定的置信度阈值α时，才被视为有效概念。公式为：
            `SC-Score G(ci) = Σ SC-Score (ci, LLM i)`
        *   **增强**：将提取的概念链接到外部知识库**ConceptNet**和**Wikipedia**，以扩展学科概念并获取文本解释，再将其转化为音频。
    3.  **多模态对齐**：
        *   **概念-图像对齐**：利用MLLMs为每个图像生成语义描述，并让另一个模型验证对齐的置信度（仅保留置信度 > 0.8的对齐）。
        *   **概念-视频对齐**：基于视频片段的语义特征与时间戳，将其与对应的概念对齐。
        *   **概念-音频对齐**：基于用LLMs重写的文本解释，通过**TTS（文本转语音）** 技术生成音频。
    4.  **知识组织与存储**：
        *   采用三级层次结构（**学科 -> 知识点 -> 概念**）。知识点依据课程标准和MOOC大纲组织。
        *   采用JSON格式的**符号化存储**，为学科、知识点、习题、多模态概念分配唯一ID，并通过交叉索引表进行互联，确保知识的连通性和可扩展性。同时提供RDF格式。

### 3. 实验设计：数据集、基准与方法对比

*   **数据集**：从**SciMKG**数据集中随机选取一个**子图**作为评估数据集。该子图包含来自生物、物理、化学三门学科的100节课的知识点，覆盖4,479个概念及对应的四种模态数据。
*   **基准（Baselines）**：对比了多种 **SOTA（最先进）** 的概念提取方法：
    *   **LLM-based**：Decomposed-QA, GPT-NER, LinkNER, UniversalNER, Self-Improving
    *   **Non-LLM traditional methods**: 文中未列出具体non-LLM方法作为baseline，但表格比较中包含了多种基于不同LLM的方法。
*   **对比方法**：
    *   **本文方法（Ours）**：完整的“提取-验证-整合-增强”流水线。
    *   **不同规模LLM的变体**：使用不同参数量级的LLM组合进行对比。
    *   **消融实验的变体**：分别移除“多个LLM”（w/o MLs）和“自反馈机制”（w/o SF-FD）。
*   **评估指标**：
    *   **概念提取**：**Precision, Recall, F1-score, ACC, MCC, AUC**。
    *   **多模态对齐**：**CLIP Score, BLIP ITM Score, X-VLM ITM Score, VQA Score** 和**人工评估**。

### 4. 资源与算力

*   **计算平台**：一台搭载 **Ubuntu 22.04 LTS** 系统的服务器，配备 **Intel Xeon E5-2686 v4 CPU**， **128GB RAM**，和一张 **NVIDIA GeForce RTX 3090 GPU**（24GB显存）。软件环境基于 **Python 3.7** 和 **PyTorch 2.4.0**。
*   **算力使用**：文章未明确提及完整的模型训练或推理所需的**具体GPU数量、总训练时长或总计算量**（如GPU-hours）。实验环境描述仅用于复现，并未提供大规模训练的算力开销分析。评估环节也仅使用了一张RTX 3090。

### 5. 实验数量与充分性

*   **实验分组**：
    1.  **主实验**：与6种SOTA LLM-based方法进行全面对比。
    2.  **消融实验**：设计了4组变体（移除MLs、移除SF-FD、同时移除两者）来验证各组件贡献。
    3.  **参数影响实验**：系统分析了**迭代次数（iter）**和**置信度阈值（α）**对性能的影响。
    4.  **LLM规模影响实验**：测试了3种不同参数规模的LLM组合对性能的影响。
    5.  **错误分析**：对提取结果的错误类型（CE, CO, FE, IO, NR）进行分析。
    6.  **多模态对齐评估**：采用4种自动评估指标和1项人工评估。
*   **充分性与客观性**：实验设计较为充分。主实验、消融实验和参数分析相互印证，系统地揭示了各模块和超参数的作用。对比的baseline方法覆盖全面且具有代表性。评估指标包含精确率、召回率等传统指标，也包含AUC等效率指标，较为客观。人工评估的引入增强了可信度。

### 6. 主要结论与发现

1.  **方法有效性**：提出的概念提取方法在所有评估指标（F1, ACC, AUC）上均显著优于所有SOTA基线方法，F1分数提升了**9%**（从0.734到0.803）。
2.  **组件贡献**：消融实验证实，“多个LLMs”（MLs）和“自反馈机制”（SF-FD）是性能提升的关键，两组件协同作用效果最佳。移除任一组件都会导致性能显著下降。
3.  **LLM规模影响**：更大、更先进的LLM（如GPT-4o）结合所提框架能获得最优性能，而中等规模的LLM（如Qwen3-14B+Gemm3-27B+Phi-3-medium组合）也能超越许多基线方法。
4.  **参数鲁棒性**：优化的迭代次数（iter=5）和置信度阈值（α=0.7）能取得最佳性能平衡。
5.  **多模态对齐鲁棒性**：自动评估和人工评估均验证了所提多模态对齐方法的有效性。人工评分为0.73，与自动评估（如CLIP Score=0.83）结果一致，表明对齐质量较高。

### 7. 优点

1.  **方法创新**：
    *   提出了一个**完全自动化**的框架，无需人工标注，极具实用性。
    *   设计了**多LLM协作 + 自洽性投票 的提取-验证-整合机制**，有效利用了不同LLM的语义多样和自我修正能力，显著提升了概念提取的准确性和鲁棒性。
    *   提出了一种**基于MLLM的、基于信心的跨模态对齐方法**，自动化程度高，且自然解决了不同模态间的语义鸿沟。
2.  **贡献显著**：
    *   构建了**SciMKG**，这是**首个同时覆盖文本、图像、视频、音频四种模态的大规模科学教育知识图谱**，填补了领域空白，具有重要应用价值。
    *   数据集及构建工具包将**开源**，可促进相关研究。
3.  **实验严谨**：
    *   进行了详尽的主实验、消融实验、参数分析和错误分析，论证充分。
    *   同时使用了自动化和人工评估，证实了模型在多模态对齐上的有效性。

### 8. 不足与局限

1.  **领域限制**：
    *   仅覆盖了**中国K12阶段**的三门自然科学学科（生物、物理、化学），其方法论在其他人文社科领域的泛化能力未经验证。
2.  **评估范围**：
    *   **多模态对齐评估**仅对**概念-图像**对齐进行了定量分析（因为其最需要语义推理），而未对**概念-视频**和**概念-音频**对齐进行同等深度的定量评估，通过结构对齐的视频和通过TTS生成的音频在评估上可能不够全面。
3.  **资源与可重复性**：
    *   未披露构建SciMKG所需的**总计算量（GPU hours）** 和**成本**，这对其大规模部署的经济可行性评估有影响。
    *   框架依赖于**商业LLM API**（如GPT-4o, Gemini），存在成本、延迟和未来可用性的风险，且其生成结果具有黑箱属性。
4.  **潜在偏差**：
    *   利用LLM进行概念提取和知识增强可能引入**模型自身的知识偏见或幻觉**，尽管通过多LLM投票可以缓解，但无法完全消除。
    *   **音频生成**完全依赖于LLM重写的文本，若重写过程引入错误，会直接导致音频质量下降。

（完）
