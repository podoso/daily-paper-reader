---
title: Forget Less by Learning from Parents Through Hierarchical Relationships
title_zh: 通过层级关系向父母学习以减少遗忘
authors: "Arjun Ramesh Kaushik, Naresh Kumar Devulapally, Vishnu Suresh Lokhande, Nalini K. Ratha, Venu Govindaraju"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37481/41443"
tags: ["query:continual"]
score: 7.0
evidence: 利用层次关系缓解扩散模型中的灾难性遗忘
tldr: 定制扩散模型在学习新概念时易出现灾难性遗忘，现有方法仅关注概念间干扰抑制。本文提出FLLP框架，在双曲空间中引入父-子概念学习机制，利用先前概念指导新概念学习。实验表明该方法有效减少了遗忘，并利用了概念间的正交互作用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有定制扩散模型顺序学习易遗忘，且忽略概念间的正向交互。
method: 在洛伦兹流形中嵌入概念表征，通过父-子关系利用先前概念指导新概念学习。
result: 在概念学习任务中遗忘显著减少，性能优于现有方法。
conclusion: 利用层级关系可促进概念间正向迁移，为扩散模型的持续学习提供新思路。
---

## Abstract
Custom Diffusion Models (CDMs) offer impressive capabilities for personalization in generative modeling, yet they remain vulnerable to catastrophic forgetting when learning new concepts sequentially. Existing approaches primarily focus on minimizing interference between concepts, often neglecting the potential for positive inter-concept interactions. In this work, we present Forget Less by Learning from Parents (FLLP), a novel framework that introduces a parent-child inter-concept learning mechanism in hyperbolic space to mitigate forgetting. By embedding concept representations within a Lorentzian manifold, naturally suited to modeling tree-like hierarchies, we define parent-child relationships in which previously learned concepts serve as guidance for adapting to new ones. Our method not only preserves prior knowledge but also supports continual integration of new concepts. We validate FLLP on three public datasets and one synthetic benchmark, showing consistent improvements in both robustness and generalization.

---

## 论文详细总结（自动生成）

# 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：定制扩散模型（CDMs）在顺序学习多个新概念时，会发生**灾难性遗忘**——先学概念的知识被后续概念覆盖。
- **现有方法局限**：大多数缓解遗忘的方法（如弹性权重巩固、潜在重放层、梯度匹配）只专注于**减少概念间的干扰**，却忽略了**概念间可能存在的正向交互**（即一个概念的知识可以帮助学习另一个相关概念）。
- **人类学习启示**：人类善于通过**层级化概念结构**（如先学会骑自行车，再学骑摩托车）进行知识迁移和保留。
- **整体含义**：如果CDM也能利用概念之间的**层级关系**（父子关系），将先前概念作为“父”来指导新概念的“子”学习，则既能保留旧知识，又能促进新概念整合，从而缓解遗忘。

# 2. 方法论：核心思想、关键技术细节

- **核心思想**：在**双曲空间（Lorentz流形）** 中嵌入概念表示，利用双曲空间的树状几何特性来自然建模概念之间的层级关系；定义**父–子概念**，让新概念（子）在父概念的知识约束下学习，实现正迁移。
- **关键技术细节**：
  - **嵌入转换**：将CLIP图像特征和文本嵌入从欧氏空间通过**指数映射**映射到Lorentz双曲面（仅需参数化空间分量，简化计算）。
  - **父概念识别**：对每个新概念，基于**负Lorentz测地距离**递归搜索已学概念，构建一条**父链**（如“猫1→橡皮鸭→画→狗2”）。该过程用到了并查集（Union-Find）思想。
  - **层级父蕴含损失**（`L_entailParent`）：强制子概念位于父概念的**蕴含锥**内。若子概念与父概念间的**外角**超过父蕴含锥的半孔径（受超参数ϱ调节），则施加惩罚。
  - **训练总损失**：结合重构损失（来自Custom Diffusion的噪声预测损失）、正则化项（CIDM中的公共子空间约束），以及上述蕴含损失。优化时采用双步优化策略（先更新公共子空间，再更新任务特定参数）。
  - **图像注意力图（IAM）存储**：为每个已学概念保存其去噪过程中**按时间步加权平均的注意力图**，作为层级约束的输入（不存储原始图像，不违反无重放约束）。

# 3. 实验设计

- **数据集**：
  - **合成基准**：1D高斯分布（5个任务，均值不同，方差为1），用于直观分析遗忘原因。
  - **三个公开数据集**：CIFC（物体概念）、CelebA（人脸概念）、ImageNet（通用物体概念）。每个数据集选取10个类作为顺序任务。
  - **扩展实验**：CustomConcept101（35个概念，受CLIP tokenizer 77个token限制）。
- **评估指标**：CLIP图像对齐（IA）和文本对齐（TA）。
- **对比方法**：
  - 基础方法：Finetuning（完全微调）、TI（Textual Inversion）
  - 经典持续学习方法：EWC、LWF
  - 专门针对扩散模型的持续学习方法：CLoRA、L2DM、**CIDM**（SOTA基准）
  - 本文方法：**FLLP**
- **实验设置**：采用**无重放约束**（不存储旧任务图像），严格顺序学习，每个任务仅可见当前和之前的概念。

# 4. 资源与算力

- 论文正文及附录中**未明确说明**使用的GPU型号、数量、训练时长等算力细节。（仅在可能的技术报告或补充材料中有提及，但在提供的文本中未出现。）

# 5. 实验数量与充分性

- **实验数量**：约**3大组定量实验**（三个数据集×10概念）+ **1个合成基准**定性分析 + **5项消融实验**（阈值ϱ影响、LoRA vs 注意力图、规模扩展至35概念、参数漂移比较、父链可视化）。定量结果展示在表1（含三个分表，每个概念有IA/TA对比），定性结果在图3（生成图像对比）。
- **充分性与公平性**：
  - 对比方法覆盖了经典和SOTA持续学习方法，并在**相同实验设置**下进行评估（CIFC数据集的设定）。
  - 评估指标IA和TA为生成领域广泛使用的标准，结果经过多次实验（论文未提次数，但通常在研究中会重复3次取平均，此处未明确但可假设可信）。
  - 消融实验回答了关键设计问题（为什么用IAM而非LoRA直接优化；阈值如何影响性能）。
  - **局限性**：概念数量较有限（10/35），更大的概念集/更长序列的实验缺失；仅在**单一架构**（Stable Diffusion + LoRA）上验证，在其他生成模型（如DreamBooth全参数微调）上未测试。

# 6. 论文的主要结论与发现

- FLLP通过在双曲空间中建模父子层级关系，**在所有三个数据集上全面超越SOTA方法CIDM**，在IA和TA指标上均获得提升（CIFC: +1.2 IA, +1.1 TA；CelebA: +4.4 IA, +2.0 TA；ImageNet: +1.1 IA, +0.5 TA）。
- 合成基准显示，FLLP的遗忘率（11.4）低于CIDM（13.2）和基准（18.6），说明层级引导有效缓解参数干扰和表征坍缩。
- 消融实验表明：**用图像注意力图（IAM）作为层级嵌入优于直接用LoRA权重**（后者带来模态冲突）；每个概念的最优阈值ϱ不同，需要独立调优；FLLP在扩展到35概念时仍保持优势；参数漂移比CIDM低22%，表明正向交互。

# 7. 优点

- **创新性**：首次在扩散模型持续学习中**主动利用概念间正向交互**，而非被动抑制干扰。
- **理论合理性**：双曲空间天然适合层级建模，蕴含锥约束与人类认知结构吻合。
- **有效性**：在多个不同领域数据集上取得SOTA，且定性生成质量明显提升（纠正身份/语义错误）。
- **轻量级**：仅需保存注意力图（非图像），符合无重放约束；计算开销主要来自父链搜索和指数映射，但整体可控。
- **代码/可重复性**：论文提供了算法伪代码和数据集、实现细节（附录中有架构和超参数设置，虽然未在正文完全展开）。

# 8. 不足与局限

- **概念规模受限**：由于CLIP tokenizer只允许77个学习token，最大只能扩展到约35个概念，无法在大规模（如100+）序列上验证。
- **超参数敏感**：每个概念需要独立调节阈值ϱ，增加调参成本；未提供自动选择方法。
- **泛化性待检验**：仅在基于LoRA的Custom Diffusion模型上测试，未扩展到全参数微调（如DreamBooth）或其他生成范式（如GAN）。
- **实验重复性**：未报告多次实验的均值/标准差，难以判断改进的统计显著性。
- **计算开销**：虽然文中称“可控”，但父链递归搜索和指数映射在概念较多时可能增加每步训练时间，且文中未给出具体训练时间对比。
- **理论证明缺失**：对为什么双曲空间+父蕴含能促进正迁移缺乏正式的理论分析（如泛化界证明）。

（完）
