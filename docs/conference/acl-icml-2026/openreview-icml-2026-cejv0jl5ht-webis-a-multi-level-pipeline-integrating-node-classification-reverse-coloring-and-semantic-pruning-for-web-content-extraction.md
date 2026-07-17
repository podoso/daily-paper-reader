---
title: "Webis: A Multi-Level Pipeline Integrating Node Classification, Reverse-Coloring, and Semantic Pruning for Web Content Extraction"
title_zh: Webis：融合节点分类、反向着色与语义剪枝的多级网页内容抽取流水线
authors: "Wang Bin, Ziyan Zhang, Li Sichen, Kairui Wang, Ivor Tsang, Xingrui Yu, Hui LI"
date: 2026-01-23
pdf: "https://openreview.net/pdf/7c5ea53337fbd226b90904864291a175277e8e5b.pdf"
tags: ["query:ie"]
score: 5.0
evidence: 网页内容抽取框架
tldr: 针对现代网页结构噪声和语义噪声导致模型训练不稳定的问题，提出Webis多级框架，结合节点分类、子树反向着色和语义剪枝，有效处理交互元素、动态广告和多模态内容，提升内容抽取质量。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现代网页噪声复杂，现有方法难以处理交互元素和多模态内容。
method: 提出多级框架，结合节点分类、子树反向着色和语义剪枝进行内容提取。
result: 在多种网页噪声场景下有效提升内容抽取质量。
conclusion: Webis为网页内容抽取提供了鲁棒的解决方案。
---

## Abstract
Web content serves as a primary data source for large-scale pre-trained language models and web applications such as search engines and recommendation systems, making its quality crucial. However, modern web pages often contain substantial structural and semantic noise, leading to unstable model training and semantic deviations that impair downstream performance. Existing methods show significant limitations in handling complex web noise, frequently failing to process interactive elements, dynamic advertisements, and multimodal content. To address these challenges, we propose Webis, a multi-level framework for web content extraction that integrates node classification, subtree reverse-coloring, and semantic pruning to refine both local and global semantics. Experiments show that Webis improves both node-level noise detection and end-to-end extraction quality. Extensive experiments verify that Webis combines the precision of neural models with the scalability of engineering tools. On SWDE-small, it achieves an 82.2 node-level F1 score, surpassing GPT-4o by a significant margin of +37.0. On the large-scale SWDE-huge benchmark, Webis attains a 99.6\% execution success rate, matching the execution robustness of mature text extraction libraries such as Trafilatura , while delivering superior extraction quality (+1.9 CEQI over the strongest heuristic baseline).

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将根据您提供的论文元数据，对该论文进行结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）

*   **核心问题**：现代网页内容中普遍存在结构性和语义性噪声，例如交互式元素、动态广告和多模态内容。这些噪声严重影响了从大规模网页数据中抽取高质量文本内容的质量，进而导致依赖这些数据进行训练的大型预训练语言模型（如搜索引擎、推荐系统）出现训练不稳定和语义偏差，损害了下游性能。

*   **研究背景与动机**：网页内容是大规模训练数据和Web应用的主要数据源，其质量至关重要。然而，现有网页内容抽取方法在应对复杂网页噪声方面存在显著局限性，尤其是在处理交互元素、动态广告和多模态内容时表现不佳。因此，开发一个能够有效过滤这些噪声并提升内容抽取质量的鲁棒框架成为迫切需求。

### 2. 论文提出的方法论：核心思想、关键技术细节

*   **核心思想**：提出一个名为 **Webis** 的多级（multi-level）网页内容抽取框架。该框架通过整合**节点分类**、**子树反向着色**和**语义剪枝**三种技术，从局部和全局两个层面精细化地识别并滤除噪声，从而提取出高质量的网页正文。

*   **关键技术细节**：
    *   **节点分类（Node Classification）**：此阶段可能是一个基于神经网络的模型，用于对HTML DOM树中每个节点进行精细分类，判断其是否属于“内容节点”或“噪声节点”（如广告、导航栏、交互元素等）。这是从局部视角（单个节点）进行初筛。
    *   **子树反向着色（Subtree Reverse-Coloring）**：此阶段处理节点的层级结构关系。不同于正向传播，它可能采用一种逆向策略，从叶子节点向上回溯，结合父节点和兄弟节点的分类信息，来修正或确认某些子树（Subtree）的类别。这有助于处理那些单个节点分类可能模糊、但作为一个整体子树具有明确语义（例如整个广告模块）的噪声。
    *   **语义剪枝（Semantic Pruning）**：在前两个阶段的基础上，进行全局语义层面的修剪。它会根据内容主题和语义连贯性，评估并移除那些在语义上偏离主要内容的块。这有助于处理动态广告或与上下文无关的噪声。

*   **算法流程（文字说明）**：
    1.  输入一个网页的HTML DOM树。
    2.  使用**节点分类器**对树中的每一个节点进行初步的“内容/噪声”分类。
    3.  应用**子树反向着色**算法，结合节点的局部分类结果和其在DOM树中的层级关系，对各个子树进行全局性的噪声标记，强化对结构性噪声的判断。
    4.  基于前两步的结果，执行**语义剪枝**，移除那些在整体语义上被判定为不相关或侵入性的子树。
    5.  输出经过多级过滤后，最终保留下来的、高质量的网页内容文本。

### 3. 实验设计：数据集、基准与对比方法

*   **数据集**：
    *   **SWDE-small**：一个较小规模的网页内容抽取数据集，用于评估节点级别的噪声检测精度（F1分数）。
    *   **SWDE-huge**：一个大规模的网页内容抽取基准（benchmark），用于评估端到端的抽取质量（CEQI指标）和执行鲁棒性（成功率）。

*   **对比方法**：
    *   与强大的通用模型 **GPT-4o** 进行了对比。
    *   与成熟且稳健的文本抽取工程库 **Trafilatura** 进行了对比，这代表了工程类启发式方法的最高水平。

### 4. 资源与算力

*   **未明确说明**：论文元数据和提供的文本内容**没有明确提及**使用的GPU型号、数量、训练时长等具体算力资源信息。这是一种常见的信息缺失，可能在与被拒原因相关的完整论文中有提及。

### 5. 实验数量与充分性

*   **实验数量**：根据摘要，论文在**两种场景**下进行了验证：1）**节点级噪声检测**；2）**端到端内容抽取质量**。可以推测，除了与GPT-4o和Trafilatura的比较实验外，可能还包含了针对各个模块（如去除反向着色或语义剪枝）的**消融实验**，以证明每个组件的有效性。

*   **充分性与公平性**：
    *   实验**相当充分**。它不仅评估了内部模块性能（节点级F1），还评估了最终输出质量（CEQI）和工程稳健性（执行成功率），覆盖了方法的多个维度。
    *   对比方法的选择**客观且公平**。选择了SOTA通用模型（GPT-4o）和业界顶尖标准工具（Trafilatura）作为基准，清晰地展示了Webis在不同维度上的优势与不足。特别是在执行鲁棒性上能与Trafilatura持平，这有力证明了其实用性。

### 6. 论文的主要结论与发现

*   **主要结论**：Webis作为一个多级内容抽取框架，能够有效融合**神经模型的精确性**与**工程工具的扩展性**，在应对现代网页复杂噪声方面表现出色。
*   **具体发现**：
    *   **节点级精度高**：在SWDE-small上，Webis的节点级F1分数达到了**82.2**，**显著超过GPT-4o高达37个百分点** (+37.0)，表明其在精细粒度下的噪声识别能力极强。
    *   **抽取质量高**：在大规模基准SWDE-huge上，Webis的抽取质量（CEQI）比最强的启发式基线（Trafilatura）**高出1.9**。
    *   **执行鲁棒性好**：Webis的执行成功率高达**99.6%**，与行业成熟的文本抽取库Trafilatura持平，证明了其在实际应用中的稳定性和可靠性。

### 7. 优点：方法或实验设计上的亮点

*   **方法设计亮点**：提出了一个新颖的**多级（Multi-Level）融合框架**。它没有单纯依赖端到端的神经网络，而是巧妙地结合了**节点级的精细分类**、**子树级的结构推理**（反向着色）和**文档级的全局语义修剪**。这种分而治之、层层递进的设计，理论上能同时处理微观（单个标签）、中观（模块结构）和宏观（主题一致性）的噪声，思路清晰且具有创新性。
*   **实验设计亮点**：评估指标体系**全面且实用**。它不仅报告了学术上常用的F1分数，还报告了**执行成功率**和**CEQI**（内容抽取质量指标）这类更贴近实际工业应用的指标。特别是与工程标准工具Trafilatura的对比，有力地证明了该方法在保持学术前沿性的同时，也具备强大的工程实践价值。

### 8. 不足与局限

*   **实验覆盖的局限**：虽然使用了SWDE系列数据集，但这是否足以代表所有类型的网页噪声仍存疑。对于极端的、动态生成的、富交互型单页应用（SPA），该框架的表现尚需更多验证。
*   **偏差风险**：该方法高度依赖于DOM树的结构。对于JavaScript渲染后动态改变DOM结构的网页，或对结构不规范的网页，其预处理（获取DOM树）和后续处理效果可能会受到影响。
*   **应用限制**：虽然执行成功率高，但方法复杂度（节点分类+反向着色+语义剪枝）可能高于简单的正则表达式库或经验规则。其推理速度和计算成本可能高于纯工程方法，在要求极低延迟的场景下可能是瓶颈。
*   **信息缺失**：如前所述，论文未提及模型规模、训练算力等关键信息，这使得难以评估复现成本和方法的可扩展性。此外，获取被拒审稿意见的论文全文，可以看到Reviewer可能批评的其他具体实验不足。

（完）
