---
title: "MPBoCo: Multimodal Prompt-based Boundary-enhanced Continual Framework for Joint Entity and Relation Extraction"
title_zh: "MPBoCo: 基于多模态提示的边界增强持续学习框架用于联合实体与关系抽取"
authors: "Guanglu Sun, Xinyu Liu, Lili Liang, Yang yu, Fei Lang, Suxia Zhu, Ming Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1220.pdf"
tags: ["query:joint-mer"]
score: 9.0
evidence: 持续学习下的多模态实体关系联合抽取
tldr: 针对多模态信息持续演进中实体和关系类型动态更新的问题，提出多模态提示边界增强持续学习框架MPBoCo，通过可学习多模态提示增量存储任务知识，动态匹配相关提示，在冻结主干上实现高效联合抽取，平衡了实时适应性与计算效率。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1220/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 760, \"height\": 958, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1220/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 856, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1220/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 777, \"height\": 311, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1405, \"height\": 668, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 587, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1418, \"height\": 430, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1418, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1220/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 531, \"height\": 205, \"label\": \"Table\"}]"
motivation: 现有方法在多模态持续学习场景下难以平衡实时适应性和计算效率。
method: 提出MPBoCo框架，利用可学习的多模态提示增量存储任务知识，动态匹配相关提示并融合到冻结骨干中。
result: 在联合多模态实体关系抽取任务上实现高效持续学习，适应新类型。
conclusion: MPBoCo有效解决了多模态持续学习中的可塑性与稳定性平衡问题。
---

## Abstract
In real-world scenarios, multimodal information continuously evolves, with new entity and relation types emerging, necessitating timely updates to multimodal knowledge graphs for supporting downstream tasks. However, existing methods struggle to balance real-time adaptability and computational efficiency in continual learning scenarios. To this end, this paper proposes the Continual Multimodal Entity and Relation Joint Extraction (CMERJE) task and a Multimodal Prompt-based Boundary-enhanced Continual (MPBoCo) framework. Specifically, MPBoCo incrementally stores task-specific knowledge via learnable multimodal prompts, dynamically matches relevant prompts for each instance, and fuses them into a frozen backbone model for task-specific reasoning. Subsequently, the boundary-enhanced dual-branch module leverages the auxiliary branch to preserve local syntactic continuity and provide boundary guidance. Experimental results demonstrate that MPBoCo achieves superior performance in real-world scenarios, significantly outperforming baseline methods by 5.5% and 7.2% in 10-task and 5-task settings, respectively.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：在真实世界中，多模态信息（如社交媒体的图文数据）持续演化，新出现的实体和关系类型频繁涌现，需要及时更新多模态知识图谱（MMKGs）以支持下游任务（如多模态推理、问答）。现有方法大多假设静态标签空间和离线训练，难以适应持续学习场景；而传统的持续学习方法（如重放范式）存在存储和隐私问题，且无法平衡实时适应性与计算效率。
- **整体含义**：本文首次提出了**持续多模态实体与关系联合抽取（CMERJE）**任务，旨在让模型在持续学习场景下，从多模态信息中联合抽取实体和关系，并能增量学习新类型而不过度遗忘旧知识。为此，作者设计了**MPBoCo框架**，通过可学习多模态提示（prompt）和边界增强的双分支模块，实现任务知识的有效积累与重用，同时保持对边界语义的精细建模。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：采用**基于提示的持续学习范式**，冻结预训练骨干网络（VLMO），仅通过可学习的多模态提示（key-prompt pairs）存储任务特定知识。针对每个输入实例，通过**类型感知的实例级提示匹配**（Type-aware Instance-level Prompt Matching）动态选择最相关的提示，并通过**层次化提示融合**（Hierarchical Prompt Fusion）注入骨干网络，实现任务特定推理。同时，设计**边界增强的双分支融合模块**（Boundary-enhanced Dual-branch Prompt Fusion），利用辅助文本分支保留局部句法连续性与边界线索，为主分支提供结构化指导。
- **关键技术细节**：
  - **多模态提示池**：为每个任务学习M组key-prompt对，key由类型描述初始化（编码实体、关系、对象类型的描述文本），prompt为可学习向量。训练时仅优化当前任务对应的提示对，完成后冻结并存入池中。
  - **实例级提示匹配**：使用冻结的VLMO提取多模态表示，通过可学习的类型增强组件（Type-aware Enhancement）聚焦于类型相关语义，然后与所有key计算余弦相似度，选择Top-r个最匹配的key-prompt对。
  - **层次化提示融合**：将选中的prompt拼接至Transformer attention的key和value中，而非追加到输入token序列，实现逐层注入。
  - **双分支解码**：主分支使用VLMO的跨模态FFN（VL-FFN）生成多模态表示；辅助分支使用纯文本FFN（T-FFN）生成文本表示，并预测实体边界（BIO标签）。通过任务变换矩阵（WT2VL）将辅助分支的边界预测融入主分支的发射分数，同时将实体表示投影到角色特定空间（主语/宾语），增强关系方向建模。
  - **训练目标**：联合优化CRF负对数似然（主分支+辅助分支）、提示一致性损失（使匹配得分逼近真实提示的one-hot分布）、以及关键正则化损失（约束keys不发生语义漂移）。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：作者构建了**CMERJE数据集**，基于现有的MNER（Twitter-2015、Twitter-2017）和MRE（MNRE）数据集，并补充了MNER-MI的标注以缓解标签不平衡。数据被划分为10个持续任务（按关系类型语义划分，无重叠标签），同时构造了5任务变体以评估不同粒度下的鲁棒性。数据统计见附录表6、7（训练/验证/测试样本数）。
- **基准（benchmark）**：非持续方法包括Vanilla BERT（每次在新任务上微调）、以及三个多模态联合抽取模型（UMT、UMGF、HiTIMI），并在它们基础上扩展了随机重放（RR）和影响重放（IR）策略。持续学习方法包括EWC（弹性权重巩固）和RP-CRE（基于重放的持续关系抽取）。对比方法涵盖单模态、多模态、重放型等多种范式。
- **评估指标**：平均F1（AF1），即对已学过的所有任务测试集F1取平均。

### 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及使用Adam优化器、余弦学习率调度和热重启，但未报告硬件配置或训练代价。因此无法评估其计算资源需求。

### 5. 实验数量与充分性

- **实验组数**：论文进行了多组实验，包括：
  - 主实验：在10任务和5任务两种设定下，对比9种基线方法（表1、表3），报告每个任务的F1和平均AF1。
  - 消融实验（表2）：移除关键组件（key正则化、类型增强、辅助文本分支、任务变换矩阵、主语/宾语分离）的5组变体。
  - 鲁棒性分析：提示层数敏感性实验（表4、表5），比较不同数量的单模态/多模态专家层配置。
  - 进一步分析：冻结骨干 vs. 不冻结骨干的性能对比（图3）、与联合训练（上限）的对比。
- **充分性评估**：实验设计较为充分。覆盖了多种基线（包括非持续、重放型、正则化型），并在不同任务粒度下验证。消融实验针对每个关键模块进行了独立验证，分析合理。灵敏度实验探索了提示层数的影响。但缺少与更多最新持续学习方法的比较（如L2P、DualPrompt等），且仅在单个数据集（CMERJE）上评估，未在其他多模态持续数据集上验证泛化性。实验公平性方面：基线方法均采用了与MPBoCo相同的骨干（VLMO）或报告了最佳配置，但部分基线（如EWC）未针对多模态进行优化，可能处于劣势。

### 6. 论文的主要结论与发现

- MPBoCo在所有持续设置下均显著优于基线方法：在10任务设置下平均AF1为28.5%，比最佳重放基线HiTIMI-IR（23.0%）高出5.5%；在5任务设置下平均AF1为42.5%，比HiTIMI-IR（35.3%）高出7.2%。
- 冻结骨干网络有效平衡可塑性与稳定性：不冻结骨干导致新任务适应性强但遗忘加剧。
- 每个关键组件（key正则化、类型增强、辅助分支、变换矩阵、角色分离）都对性能有贡献，其中类型增强（TAE）的移除导致性能大幅下降（AF1从28.5%降至17.9%），说明类型感知匹配的重要性。
- 提示层数存在最优配置：8个单模态 + 2个多模态专家层效果最佳；过多或过少均降低性能。
- MPBoCo接近联合训练（所有数据可访问）的性能上限，证明了其知识保留能力。

### 7. 优点：方法或实验设计上的亮点

- **任务创新**：首次提出CMERJE任务，填补了多模态联合抽取与持续学习之间的空白，并构建了专门的基准数据集。
- **方法创新**：将提示学习成功应用于持续序列标注任务，解决了传统提示范式无法捕获细粒度边界语义的问题；边界增强双分支模块巧妙利用了辅助文本分支的句法连续性信息，不增加额外存储。
- **训练高效**：仅优化提示参数和解码器，参数高效，避免重放带来的存储和隐私问题。
- **实验设计完整**：包含多任务粒度、消融、灵敏度分析、与联合训练上限对比，验证了方法的鲁棒性和有效性。
- **代码与数据开放潜力**：论文未明确提及代码开源，但提供了详细数据集构建过程，便于复现。

### 8. 不足与局限

- **实验覆盖有限**：仅在自建的CMERJE数据集上评估，未在更多公开多模态持续学习数据集（如Twitter-MNER+持续版）上测试，泛化性有待验证。
- **基线覆盖不全**：缺少与最新提示型持续学习方法（如L2P、DualPrompt、Coda-Prompt）的对比，这些方法在单模态持续学习上表现优异，但未在本文中比较其在多模态序列标注上的适配。
- **计算资源未报告**：缺少GPU型号、训练时长等信息，无法评估实际部署成本。
- **数据集人工构建**：CMERJE由现有数据集拼接并补充标注，可能存在标注噪声或任务划分的任意性，影响结论的普适性。
- **模型依赖特定骨干**：使用VLMO，其专家层覆盖文本和视觉，若涉及其他模态（如音频）需重新预训练专家层，扩展性受限。
- **边界识别仍有局限**：尽管设计了辅助分支，但作者自述在细粒度边界识别上仍有提升空间，未来可考虑引入更多结构约束（如词法特征）。
- **未讨论隐私与安全**：虽然提示范式规避了存储旧样本的隐私问题，但未分析提示中是否可能泄露任务信息或遭受对抗攻击。

（完）
