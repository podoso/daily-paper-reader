---
title: Transfer between Modalities with MetaQueries
title_zh: 通过MetaQueries进行模态间的迁移
authors: "Xichen Pan, Satya Narayan Shukla, Aashu Singh, Zhuokai Zhao, Shlok Kumar Mishra, Jialiang Wang, Zhiyang Xu, Jiuhai Chen, Kunpeng Li, Felix Juefei-Xu, Ji Hou, Saining Xie"
date: 2025-09-06
pdf: "https://openreview.net/pdf?id=4AEivvf9uv"
tags: ["query:multimodal"]
score: 7.0
evidence: 多模态大语言模型与扩散模型之间的接口
tldr: 统一多模态模型需要复杂训练。MetaQueries通过一组可学习查询作为MLLM和扩散模型的高效接口，利用MLLM的推理能力增强图像生成，且MLLM可冻结，简化训练。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1434, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 518, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1443, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1430, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1162, \"height\": 881, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1574, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1532, \"height\": 1680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aeivvf9uv/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1444, \"height\": 800, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1302, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1002, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1441, \"height\": 586, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1299, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1451, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1096, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1282, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1177, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1256, \"height\": 486, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aeivvf9uv/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1172, \"height\": 299, \"label\": \"Table\"}]"
motivation: 统一多模态模型训练复杂，需要仔细的数据平衡。
method: 提出MetaQueries，一组可学习查询连接自回归MLLM与扩散解码器。
result: 仅需图像-标题对和标准扩散目标即可有效训练，甚至冻结MLLM。
conclusion: MetaQueries为多模态生成提供了简化的迁移方法。
---

## Abstract
Unified multimodal models aim to integrate understanding (text output) and generation (pixel output), but aligning these different modalities within a single architecture often demands complex training recipes and careful data balancing. We introduce MetaQueries, a set of learnable queries that act as an efficient interface between autoregressive multimodal LLMs (MLLMs) and diffusion models. MetaQueries connects the MLLM's latents to the diffusion decoder, enabling knowledge-augmented image generation by leveraging the MLLM's deep understanding and reasoning capabilities. Our method simplifies training, requiring only paired image-caption data and standard diffusion objectives. Notably, this transfer is effective even when the MLLM backbone remains frozen, thereby preserving its state-of-the-art multimodal understanding capabilities while achieving strong generative performance. Additionally, our method is flexible and can be easily instruction-tuned for advanced applications such as image editing and subject-driven generation.

---

## 论文详细总结（自动生成）

以下是对论文《Transfer between Modalities with MetaQueries》的详细中文总结：

### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：统一多模态模型（同时支持文本理解和图像生成）通常需要复杂的训练流程和数据平衡，难以同时优化理解和生成能力。
- **动机**：作者提出“让扩散模型做生成，让大语言模型做理解”的简化哲学，希望在不牺牲各自专长的情况下实现模态间高效迁移。
- **背景**：现有统一模型（如Emu、SEED-X、Janus等）多采用全参数训练或共享骨干，代价高昂且容易造成性能权衡。

### 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：使用一组可学习的**MetaQueries**作为冻结多模态大语言模型（MLLM）与条件扩散模型之间的接口，从MLLM中提取用于图像生成的多模态条件。
- **关键技术细节**：
  - **MetaQueries**：一组随机初始化的可学习查询 `Q ∈ R^{N×D}`（`N`为令牌数，`D`为MLLM隐藏维度），直接输入冻结的MLLM，利用其因果注意力获取条件向量 `C`。
  - **连接器**：条件 `C` 通过一个可训练连接器（采用编码器-投影结构，在MLLM隐藏维度先对齐再投影到扩散模型输入空间）映射到扩散解码器。
  - **训练目标**：仅使用标准扩散去噪损失（配对的图像-标题数据），不修改MLLM参数。
  - **灵活扩展**：MLLM可冻结也可微调；扩散模型可替换（实验中使用了SD v1.5和Sana-1.6B）。
- **算法流程**（文字描述）：
  1. 输入图像-标题对，将标题和可选的图像编码送入冻结MLLM。
  2. 在MLLM中插入MetaQueries，得到查询后的条件表示。
  3. 通过连接器将条件投影到扩散模型条件空间。
  4. 对扩散模型输入噪声图像，以条件为引导进行去噪训练（或推理）。

### 3. 实验设计
- **数据集**：
  - 预训练：25M公开图像-标题对。
  - 指令微调：从mmc4核心子集挖掘的2.4M自然图像对，使用MLLM生成指令描述。
  - 评估基准：理解（MME-P, MMB, SEED, MMMU, MM-Vet），生成（COCO FID, MJHQ-30K FID, GenEval, DPG-Bench, WISE, CommonsenseT2I）。
- **对比方法**：包括Emu、DreamLLM、SEED-X、Chameleon、Show-o、VILA-U、Emu3、MetaMorph、TokenFlow-XL、Transfusion、LMFusion、Janus系列等18种以上模型。
- **消融实验**：研究了令牌数量（1~1024）、连接器设计（投影-编码器 vs 编码器-投影）、MLLM冻结 vs 全调优、训练目标（文本到图像 vs 图像重建 vs 混合）、不同MLLM骨干（LLaVA-0.5B, Qwen2.5-VL 3B/7B）等。

### 4. 资源与算力
- **提及**：预训练使用全局批次大小4096，学习率1e-4，共8个epoch（约200k步）。指令微调批次2048，3个epoch。
- **未明确说明**：GPU型号、数量、具体训练时长。文本未提供这些细节，需指出这一缺失。

### 5. 实验数量与充分性
- **实验数量丰富**：涵盖理解+生成双任务基准测试（约10项指标）、设计消融（4组表+图2~3）、连接器对比、令牌缩放、训练目标混合、指令微调（主题生成、图像编辑）、知识/推理增强生成（WISE, CommonsenseT2I）等，总计超过10组核心实验。
- **充分性与公平性**：
  - 消融设计系统，控制变量清晰（如对比冻结与调优时控制其他因素）。
  - 对比方法覆盖当时主流统一模型，且给出同等设置下的结果（部分由作者自行测试）。
  - 但部分对比（如GenEval vs Janus-Pro）显示差距，作者承认可能源于扩散模型与自回归模型的固有差异，未在架构上进行公平对齐。

### 6. 主要结论与发现
- **冻结MLLM可匹敌全调优**：MetaQueries在冻结MLLM时，图像生成质量（MJHQ FID 6.02）与全调优相当，且完全保留理解能力（MME 1685, MMB 83.5等）。
- **有效转移推理与知识**：在WISE和CommonsenseT2I上大幅超越所有先前统一模型（WISE 0.55 vs Sana 0.50），证明可激活MLLM的常识和世界知识。
- **可扩展至高级任务**：通过指令微调，零样本实现主题驱动生成、图像编辑、视觉关联和logo设计等。
- **设计选择关键**：可学习查询优于最后一层嵌入；更多令牌持续提升生成质量和对齐；编码器-投影连接器更优。
- **数据高效**：仅25M公开数据即在COCO FID上超越基模型（8.69 vs 9.20）。

### 7. 优点
- **简单高效**：不修改MLLM参数，仅训练轻量MetaQueries和连接器，训练成本低。
- **保持SOTA理解**：冻结MLLM确保理解能力不下降，同时获得强大的生成能力。
- **灵活兼容**：可任意替换MLLM和扩散模型，支持多种下游任务（文本到图、图像编辑、主题生成等）。
- **自然指令数据**：提出从网页图像对自动构建指令数据的方法，避免了人工标注或依赖专家模型的局限。
- **实验设计清晰**：消融实验系统，揭示令牌缩放、连接器结构等重要设计规律。

### 8. 不足与局限
- **生成对齐仍有差距**：在GenEval上与Janus-Pro（自回归方法）存在差距，作者归因于扩散模型与自回归模型的失败模式不同，但未提出解决方案。
- **未披露算力细节**：缺少GPU型号、数量、训练时长等关键资源信息，影响可复现性评估。
- **数据规模有限**：仅用25M数据，推测更大规模数据可进一步提升性能（作者也承认这点），但未在本文验证。
- **图像重建/编辑能力有限**：虽然展示了重建与编辑，但仅基于少量微调步骤（1000步），且未与专用编辑模型全面对比。
- **主题生成评估单一**：仅使用DreamBench，未覆盖复杂场景（多个主体、遮挡等）。
- **推理增强生成仅限文本输入**：实验中的推理示例均为纯文本问题，未涉及多模态推理（如图像+文字）的生成场景。

（完）
