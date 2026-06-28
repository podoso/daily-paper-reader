---
title: "ConSurv: Multimodal Continual Learning for Survival Analysis"
title_zh: "ConSurv: 面向生存分析的多模态持续学习"
authors: "Dianzhi Yu, Conghao Xiong, Yankai Chen, Wenqian Cui, Xinni Zhang, Yifei Zhang, Hao Chen, Joseph J. Y. Sung, Irwin King"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40013/43974"
tags: ["query:continual"]
score: 7.0
evidence: 多模态持续学习用于生存分析，解决灾难性遗忘
tldr: 生存预测中静态模型无法适应动态临床环境，现有持续学习方法多局限于单模态且遗忘严重。本文提出ConSurv框架，针对癌症生存分析，同时利用全切片图像和基因组等多模态数据，通过设计多模态持续学习策略缓解灾难性遗忘。实验表明，ConSurv在多模态持续生存预测任务中显著优于基线方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 静态生存预测模型无法适应临床持续数据流，且现有持续学习方法忽略多模态关联与灾难性遗忘。
method: 设计多模态持续学习框架，利用全切片图像和基因组数据进行联合建模并缓解遗忘。
result: 在多个癌症生存数据集上，ConSurv准确率优于单模态及非持续学习方法。
conclusion: 多模态持续学习可提升生存预测模型的适应性和准确性。
---

## Abstract
Survival prediction of cancers is crucial for clinical practice, as it informs mortality risks and influences treatment plans. However, a static model trained on a single dataset fails to adapt to the dynamically evolving clinical environment and continuous data streams, limiting its practical utility. While continual learning (CL) offers a solution to learn dynamically from new datasets, existing CL methods primarily focus on unimodal inputs and suffer from severe catastrophic forgetting in survival prediction. In real-world scenarios, multimodal inputs often provide comprehensive and complementary information, such as whole slide images and genomics; and neglecting inter-modal correlations negatively impacts the performance. To address the two challenges of catastrophic forgetting and complex inter-modal interactions between gigapixel whole slide images and genomics, we propose ConSurv, the first multimodal continual learning (MMCL) method for survival analysis. ConSurv incorporates two key components: Multi-staged Mixture of Experts (MS-MoE) and Feature Constrained Replay (FCR). MS-MoE captures both task-shared and task-specific knowledge at different learning stages of the network, including two modality encoders and the modality fusion component, learning inter-modal relationships. FCR further enhances learned knowledge and mitigates forgetting by restricting feature deviation of previous data at different levels, including encoder-level features of two modalities and the fusion-level representations. Additionally, we introduce a new benchmark integrating four datasets, Multimodal Survival Analysis Incremental Learning (MSAIL), for comprehensive evaluation in the CL setting. Extensive experiments demonstrate that ConSurv outperforms competing methods across multiple metrics.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机

- **背景**：癌症生存预测对临床决策至关重要，但现有模型多为静态训练，难以适应持续变化的数据流（如新医院、新批次数据）。多模态数据（全切片图像WSI和基因组）能提供互补信息，但现有持续学习（CL）方法主要针对单模态，且存在严重的**灾难性遗忘**。
- **关键挑战**：
  - **灾难性遗忘**：在新数据集上微调会导致旧任务性能急剧下降。
  - **复杂跨模态交互**：WSI与基因组之间的关联随不同癌症类型变化，现有CL方法忽略了这种动态相关性。
- **目标**：首次提出面向生存分析的多模态持续学习方法 **ConSurv**，在多个癌症数据集上顺序学习时既能获取新知识，又能保留旧知识，同时有效建模跨模态关系。

### 2. 方法论

- **核心思想**：采用**任务增量学习**设定，结合可扩展的混合专家结构（MS-MoE）和特征约束回放（FCR），平衡稳定性与可塑性。
- **MS-MoE（多阶段混合专家）**：
  - 在WSI编码器、基因组编码器和模态融合组件三个关键位置插入MoE模块。
  - 保持固定的专家集合（nE=8），每遇到新任务添加一个线性层路由器，采用**稀疏共享策略**：一个共享专家始终激活，其余专家中选Top-k（k=1）。
  - 路由器输出权重：\( W^{(k)} = \text{Softmax}(\text{TopK-S}(R_k(x^{(k)}))) \)，输出为 \( y^{(k)} = \sum_i W_i^{(k)} E_i(x^{(k)}) \)。
  - 集成方式：若目标位置为FFN则替换，否则采用残差附加。这使模型在保留原有骨干能力的同时学习任务特定和共享知识。
- **FCR（特征约束回放）**：
  - 维护一个固定大小的回放缓冲区，使用水库抽样存储已处理实例的三种特征：WSI patch特征 \(f_P\)、基因组特征 \(f_G\)、最终融合特征 \(f_F\)。
  - 训练时增加三项L2约束损失：\( L_P + L_G + L_F \)，以限制旧任务特征偏移。
  - 同时使用标准回放损失 \( L_R \)（监督损失）。
  - 总体损失：\( L_{CL}^{(k)} = L_s(D_k; \theta) + \alpha L_{FC} + \beta L_R \)。
- **算法流程**：顺序训练四个癌症数据集，每个数据集训练后更新缓冲区，使用上述损失更新模型参数。

### 3. 实验设计

- **数据集与基准**：构建 **MSAIL** 基准，整合TCGA中四个癌症数据集：BLCA（膀胱癌，373例）、UCEC（子宫内膜癌，480例）、LUAD（肺腺癌，453例）、BRCA（乳腺癌，955例）。顺序为BLCA→UCEC→LUAD→BRCA。
- **对比方法**：
  - 基线：联合训练、直接微调。
  - 正则化方法：EWC、LwF。
  - 架构方法：T-LoRA。
  - 回放方法：ER、DER、DER++。
  - 基于MoE的CL方法：MOSE、MOE-MOSE、IMEX-Reg。
- **评估指标**：主要指标为平均C-index和平均C-index IPCW；辅助指标：Forgetting、BWT、FWT。

### 4. 资源与算力

- 论文**未明确说明**使用的GPU型号、数量及训练时长。仅在代码仓库中可查询实现细节，但正文未提供具体硬件配置与耗时信息。

### 5. 实验数量与充分性

- **实验数量**：主实验对比了11种方法在4个数据集上的表现，每个方法在5次随机种子下运行，报告均值和标准差。
- **消融实验**：对MS-MoE、FCR及其变体进行了系统消融（共5行），验证各组件贡献。
- **额外分析**：Kaplan-Meier曲线及log-rank检验（图3）、MS-MoE路由专家选择比例分析（图4），以及替代任务顺序实验（附录C.4）。
- **评价**：实验覆盖了主流CL方法，消融设计完整，统计显著性通过多次运行体现，结果客观公平。

### 6. 主要结论与发现

- 静态模型在新数据集上表现较差（正向迁移有限），直接微调导致严重灾难性遗忘（BLCA性能从0.607降至0.531），证实CL必要性。
- ConSurv在平均C-index（0.601）和平均C-index IPCW（0.597）上均优于所有对比方法，同时保持了较低的遗忘度。
- MS-MoE通过专家选择实现了任务特定与共享知识学习，FCR通过多级特征约束有效缓解遗忘。
- Kaplan-Meier分析显示ConSurv能在所有四个癌种上显著区分高低风险组（p<0.05）。

### 7. 优点

- **首次**将多模态持续学习应用于生存分析，填补了WSI+基因组连续学习的空白。
- 方法设计巧妙：MS-MoE的稀疏共享策略在保留跨任务共享知识的同时控制参数增长；FCR仅存储特征而非原始数据，节省存储。
- 实验全面：包含多种基线、消融、可视化分析，并在替代任务顺序上验证鲁棒性。
- 代码开源，便于复现。

### 8. 不足与局限

- **算力消耗未报告**：缺乏GPU型号、训练时间等细节，难以评估计算成本。
- **仅考虑四种癌症**：更广泛的癌种（如肾癌、结直肠癌）未纳入，泛化性待验证。
- **任务增量设定假设明确**：推理时需提供任务ID，这在真实临床系统中可能不易获得。
- **缓冲区大小固定**：未探讨不同缓冲区大小对性能的影响，可能对极长序列有局限。
- **未与全监督多模态迁移学习方法对比**：如联合训练后微调，但联合训练本身计算成本高，作者未讨论其效率权衡。

（完）
