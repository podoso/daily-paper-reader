---
title: "Imagine with Layout and Sketch: Enhancing Vision-Language Retrieval with Dual-Stream Multi-Modal Query Refinement"
title_zh: 通过布局和素描想象：双流多模态查询细化增强视觉语言检索
authors: "GuangHao Meng, Jinpeng Wang, Qian-Wei Wang, XuDong Ren, Dan Zhao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37742/41704"
tags: ["query:multimodal"]
score: 4.0
evidence: 使用布局和素描多模态查询细化的视觉语言检索
tldr: 传统视觉语言检索方法对多实体布局和困难实体理解不足。本文提出LASE框架，通过多模态布局和素描知识细化查询表示。布局编码空间排列，素描捕获实体本质形状。在多个基准上显示该方法在复杂查询中显著提升检索精度。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37742/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1822, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37742/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1718, \"height\": 851, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37742/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 859, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37742/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 847, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37742/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1757, \"height\": 698, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37742/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1619, \"height\": 1033, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37742/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 873, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37742/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 766, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37742/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 878, \"height\": 235, \"label\": \"Table\"}]"
motivation: 传统方法缺乏对多实体布局和困难实体特征的深层理解。
method: 引入布局和素描两种多模态知识，通过双流网络细化查询表示。
result: 在多实体和挑战性查询上显著提升检索性能。
conclusion: 多模态查询细化有效增强视觉语言检索的细粒度理解。
---

## Abstract
Vision-Language Retrieval (VLR) aims to retrieve relevant visual or textual information from multimodal data using language or image queries. However, traditional VLR methods often rely on data-driven shallow semantic alignment and fail to understand the deeper structural and fine-grained entity features of queries, resulting in poor performance on multi-entity layouts and challenging entities. In this paper, we propose the Layout-Aware and Sketch-Enhanced (LASE) VLR framework, which refines query representations by incorporating multimodal layout and sketch knowledge. Specifically, layout knowledge encodes the spatial arrangement of entities, while sketch knowledge refines entity perception by capturing essential structural details. To extract these knowledge representations, we leverage Large Language Models' (LLMs) powerful semantic understanding for layout generation, and Diffusion Models' (DMs) fine-grained cross-modal generative capabilities for sketch generation. However, integrating  knowledge into queries may introduce biases and query-specific preferences due to varying visual content and knowledge demands. To address this, we propose the Gated Dual-Stream Knowledge Module (GDKM), which consists of a multi-instance fusion network with a sample-aware gating network. The fusion network aggregates diverse knowledge using multi-head attention to reduce bias, while the gating network adjusts knowledge weights based on query characteristics. Extensive experiments demonstrate that the LASE significantly enhances VLR performance across multiple benchmarks, with superior generalization and transferability.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：传统视觉语言检索（VLR）方法大多依赖数据驱动的浅层语义对齐，忽视查询中潜在的深层结构知识和细粒度实体特征，导致面对**多实体布局**（如复杂空间关系）和**跨模态实体对齐**（如区分相似实体）时性能显著下降。
- **具体挑战**：
  - 多实体布局：模糊的空间描述和有限的空间推理能力使检索器难以正确理解实体间的布局关系。
  - 跨模态实体对齐：检索器难以将文本实体与对应的视觉实体精准匹配，易混淆相似实体（如“自行车”与“摩托车”）。
- **研究动机**：探索额外引入多模态知识（布局和素描）来增强查询表示，从而提升VLR在复杂场景下的对齐能力。

## 2. 方法论

### 2.1 核心思想
提出**LASE（Layout-Aware and Sketch-Enhanced）** 框架，通过双流多模态查询细化，将**布局知识**（实体空间排列）和**素描知识**（实体本质结构细节）融入查询表示，弥补传统方法的不足。

### 2.2 关键技术细节
- **知识生成**：
  - **布局生成**：利用LLM（如Llama3-7B）根据查询生成布局信息（实体名称、边界框坐标、背景描述），每个查询生成多个布局实例以降低偏差。
  - **素描生成**：利用扩散模型（如DALL-E 3）基于查询+布局引导生成高保真素描，同样生成多个实例。
- **知识融合模块（GDKM）**：
  - **多实例融合网络**：分别对布局和素描实例使用多头交叉注意力机制，以查询嵌入为查询、多实例嵌入为键值，融合得到布局增强嵌入和素描增强嵌入。
  - **样本感知门控网络**：将查询嵌入、布局增强嵌入、素描增强嵌入拼接后经MLP+Sigmoid输出权重β（布局权重），素描权重为1-β，最终加权求和得到增强查询表示。
- **渐进对比损失（PCL）**：分三个阶段逐步引入知识：先基础文本-图像对齐，再单流知识（布局或素描），最后双流知识融合，采用动态执行比例控制学习进程。

### 2.3 公式与流程说明（文字描述）
- 布局嵌入：HLk = φ(Lk)
- 素描嵌入：HSk = ψ(Sk)
- 布局增强：HL = MultiheadAttn(HT, {HLk}, {HLk})
- 素描增强：HS = MultiheadAttn(HT, {HSk}, {HSk})
- 门控权重：β = σ(MLP(concat(HT, HL, HS)))
- 最终增强查询：HT_enhanced = β·HL + (1-β)·HS + HT

## 3. 实验设计

### 3.1 数据集与场景
- **主实验数据集**：Flickr30K (1K test)、MSCOCO (5K test)、Flickr30K-CFQ、Llava23K。
- **泛化性验证**：新闻领域N24News、时尚领域Fashion200K。
- **迁移性验证（零样本）**：WikiDO（含In-Domain和Out-of-Domain）、Urban1K、sDCI7K。

### 3.2 Benchmark与对比方法
- **Baseline检索器**：CLIP (ViT-B/32)、CoCa (ViT-B/32)、EVA-02-CLIP (ViT-B/16)、BLIP2 (ViT-L)、VLM2Vec (LLaVA-1.6)。
- **对比的查询优化方法**：DetCLIP、DesCLIP、CLIP-GPT、LaBo、RACLIP，以及无优化设置（NA）。

## 4. 资源与算力

- 文中**未明确说明**使用的GPU型号、数量及训练时长。
- 仅提及LASE基于预训练CLIP微调，无需重新预训练，过程轻量化。GDKM使用6层交叉注意力块，每个查询生成4个布局和4个素描实例。另外提出了LASE-lite轻量变体以降低推理成本，但具体算力需求未量化。

## 5. 实验数量与充分性

- **实验数量**：涵盖了5种检索器（CLIP、CoCa、EVA-02-CLIP、BLIP2、VLM2Vec）在4个主数据集上的图像→文本和文本→图像检索（共8个评估项），每个评估项报告R@1和R@5；另有2个领域泛化实验和1个零样本迁移实验；消融实验包括知识组件消融（表4）、实例数量影响（图4）、门控网络效果等；定性案例分析（图5）。
- **充分性**：实验设计较为全面：
  - 多检索器、多数据集覆盖不同规模与难度。
  - 与多种现有查询优化方法公平对比。
  - 消融实验验证了每个组件的贡献。
  - 跨域和零样本实验验证泛化性与迁移性。
  - 存在少量主观性（如定性案例选择），但整体客观公平。

## 6. 主要结论与发现

- LASE显著提升VLR性能，尤其在复杂布局和多实体场景下，优于所有对比方法。
- 布局和素描信息互补：布局提升空间对齐，素描增强实体区分。
- 多实例融合降低单实例偏差，门控网络适应查询特性，渐进对比损失稳定训练。
- 在不同检索器（从轻量CLIP到大规模VLM2Vec）上均一致提升，表明知识具有通用性。
- 在未见领域（如新闻、时尚）和零样本任务上表现优异，证明良好泛化与迁移能力。

## 7. 优点

- **创新性**：首次将布局和素描两种多模态知识联合引入查询细化，利用LLM和DM生成知识，思路新颖。
- **鲁棒性**：多实例生成+注意力融合降低偏差；样本感知门控自适应调节知识权重。
- **通用性**：适用于多种主流VLR框架，不依赖特定模型结构。
- **轻量化设计**：LASE-lite为进一步部署提供可能；渐进损失避免训练不稳定。
- **实验充分**：多维度评估验证了方法的有效性和泛化性。

## 8. 不足与局限

- **推理效率**：实时生成布局和素描带来显著延迟，虽提出LASE-lite，但仍需进一步优化。
- **算力未公开**：缺乏具体GPU型号、训练时间等细节，不利于复现和成本评估。
- **依赖外部模型**：依赖LLM和DM生成知识，这些模型的更新或替换可能影响性能，且存在生成偏差风险。
- **知识偏差**：尽管多实例融合缓解了部分偏差，但布局/素描风格与现实图像不完全匹配时仍可能引入噪声。
- **实验覆盖**：主要评估图像-文本检索，未涉及视频-文本检索等更复杂多模态任务。
- **门控网络可解释性有限**：权重β的决策过程缺乏深入分析。

（完）
