---
title: "Bring Your Dreams to Life: Continual Text-to-Video Customization"
title_zh: 将梦想变为现实：连续文本到视频定制
authors: "Jiahua Dong, Xudong Wang, Wenqi Liang, Zongyan Han, Meng Cao, Duzhen Zhang, Hanbin Zhao, Zhi Han, Salman Khan, Fahad Shahbaz Khan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37361/41323"
tags: ["query:continual"]
score: 9.0
evidence: 持续学习灾难性遗忘文本到视频定制
tldr: 针对持续学习新概念时出现的遗忘和概念忽视问题，本文提出连续定制视频扩散模型（CCVD），通过概念特定属性保留模块和任务感知概念聚合机制，在文本到视频生成中实现连续学习新概念的同时保持旧概念，有效缓解了灾难性遗忘。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有文本到视频定制方法假设概念静态不变，无法连续学习新概念，且存在遗忘问题。
method: 提出CCVD模型，包含概念特定属性保留模块和任务感知概念聚合模块，在扩散模型中实现连续学习。
result: 在多个视频生成任务上证明能连续学习新概念并保持旧概念性能。
conclusion: 为文本到视频定制提供了有效的持续学习方案，缓解了灾难性遗忘。
---

## Abstract
Customized text-to-video generation (CTVG) has recently witnessed great progress in generating tailored videos from user-specific text. However, most CTVG methods assume that personalized concepts remain static and do not expand incrementally over time. Additionally, they struggle with forgetting and concept neglect when continuously learning new concepts, including subjects and motions. To resolve the above challenges, we develop a novel Continual Customized Video Diffusion (CCVD) model, which can continuously learn new concepts to generate videos across various text-to-video generation tasks by tackling forgetting and concept neglect. To address catastrophic forgetting, we introduce a concept-specific attribute retention module and a task-aware concept aggregation strategy. They can capture the unique characteristics and identities of old concepts during training, while combining all subject and motion adapters of old concepts based on their relevance during testing. Besides, to tackle concept neglect, we develop a controllable conditional synthesis to enhance regional features and align video contexts with user conditions, by incorporating layer-specific region attention-guided noise estimation. Extensive experimental comparisons demonstrate that our CCVD outperforms existing CTVG models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：定制化文本到视频生成（CTVG）技术能够根据用户指定的文本描述生成个性化视频。现有方法通常假设用户定义的概念（如主体、动作）是静态的，且不会随时间增量扩充。然而，在实际场景中，用户往往希望持续学习新概念来生成视频。
- **核心问题**：当连续学习新概念（包括新主体和新运动模式）时，现有 CTVG 方法面临两大挑战：
  - **灾难性遗忘**：模型在学习新概念后会丢失先前学习的概念的独特身份和特征。
  - **概念忽视**：在多概念视频定制中，某些旧概念（主体或运动）在生成结果中被忽略或未对齐用户指定的条件（如边界框）。
- **论文贡献**：提出一个新的问题定义——连续文本到视频定制（Continual Text-to-Video Customization, CTVC），并设计首个解决该问题的模型 CCVD，旨在克服遗忘和概念忽视。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **整体架构**：基于 DreamVideo 基线，模型 CCVD 包含三个核心模块：
  1. **概念特定属性保留模块（CAR）**：用于训练阶段，缓解灾难性遗忘。
     - **层特定概念令牌（Layer-Specific Concept Tokens）**：为每层 UNet 设置独立的文本提示中的概念令牌，以更好地捕捉每个概念的独有特征。
     - **概念正交损失（Concept Orthogonal Loss, COL）**：在训练当前任务时，强制当前任务的概念子空间与所有先前任务的概念子空间正交（通过最小化不同子空间内积的绝对值），从而保持概念间的区分性。损失函数形式为：  
       \[
       \mathcal{L}_{COL} = \mathbb{E}[\|\epsilon - \epsilon_{\theta_u}(z_t, c, t)\|_2^2 + \lambda \sum_{j=1}^{u-1} \sum_{l=1}^L \operatorname{tr}(R_j^l (R_u^l)^\top)]
       \]
  2. **任务感知概念聚合策略（TCA）**：用于测试阶段，动态组合所有已学习任务的概念适配器。
     - 对于测试文本提示，提取其层特定嵌入，与存储的各任务概念令牌嵌入计算相似度并归一化，然后以此作为权重加权求和各任务的适配器权重：  
       \[
       \Delta \hat{W}_l = \sum_{j=1}^u \Delta W_j^l \cdot \zeta(H)_j, \quad H = \max(\hat{c}_l \cdot (\hat{h}_l)^\top)
       \]
  3. **可控条件合成模块（CCS）**：解决多概念定制中的概念忽视问题。
     - **层特定区域注意力（Layer-Specific Region Attention）**：对于用户指定的区域条件（边界框 + 文本），在 UNet 每一层计算区域注意力，提取区域内特征并替换原特征图对应区域。
     - **注意力引导噪声估计（Attention-Guided Noise Estimation）**：基于注意力值的大小动态重新加权区域噪声估计。注意力值小的容易忽视的概念被赋予更大权重，通过公式（7）聚合噪声估计，实现条件控制。

- **算法流程**：顺序学习任务，每学习一个新任务，仅存储该任务的适配器权重和概念令牌；测试时使用 TCA 动态融合所有旧适配器，再结合 CCS 模块生成满足条件的视频。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集**：作者新建了持续视频定制（CVC）数据集，包含 35 个顺序的文本到视频定制任务，涵盖不同主体和运动模式。
- **评估场景**：四种视频生成任务：
  - 单概念视频定制（Single-concept video customization）
  - 多概念视频定制（Multi-concept video customization）
  - 风格迁移（Style transfer）
  - 视频编辑（Video editing）
- **对比方法**：包括 Finetuning（直接微调）、EWC、LWF、LoRA-M、CLoRA、L2DM 等。所有方法均使用 DreamVideo 作为基线 backbone。
- **评估指标**：
  - 生成质量：CLIPT（文本-视频一致性）、CLIPI（图像-视频一致性）、DINOI（主体一致性）、TCons（时序一致性）。
  - 遗忘评估：F-CLIPT、F-CLIPI、F-DINOI（指标下降量）。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点
- **文中未明确说明**：实验部分没有提及使用的 GPU 型号、数量、训练时长或显存消耗。仅提到使用 Adam 优化器，学习率 1e-4（文本嵌入）和 1e-5（UNet），视频帧数 nv=32。因此论文在算力资源方面缺乏透明性，可能影响可重复性。

### 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平
- **实验数量**：
  - 定量实验：单概念视频定制任务提供了一张表（Table 1），包含 6 种对比方法和 7 个指标。
  - 消融实验：表 2 逐步消融了层特定概念令牌（LCT）、概念正交损失（COL）、任务感知聚合（TCA），展示了各模块的贡献。
  - 定性实验：图 3-6 分别展示了单概念、多概念、风格迁移、视频编辑下的视觉比较。
- **充分性与客观性**：
  - 实验覆盖了所有定义的四大任务类型，定性结果丰富。
  - 定量实验仅对单概念任务给出了数值，多概念任务没有定量表格，略显不足。
  - 消融实验覆盖了主要模块，但未单独消融 CCS 模块（区域注意力和噪声估计）对多概念任务的影响。
  - 对比方法选择合理，均为增量学习或持续学习领域中代表性方法。
  - 整体实验设计较为充分，但多概念定量的缺失降低了部分说服力。

### 6. 论文的主要结论与发现
- CCVD 在单概念视频定制任务上，所有五项评估指标（CLIPT、CLIPI、DINOI、TCons及其遗忘指标）均优于所有对比方法。
- 通过概念特定属性保留（CAR）和任务感知聚合（TCA），模型能有效缓解灾难性遗忘，保持旧概念的独特属性。
- 通过可控条件合成模块（CCS），模型能够根据用户指定条件（边界框）生成多概念视频，避免概念忽视。
- 定性结果（图 3-6）显示，对比方法在多概念连续学习后出现身份丢失或概念缺失，而 CCVD 生成结果完整且对齐条件。

### 7. 优点：方法或实验设计上有哪些亮点
- **问题新颖性**：首次系统定义连续文本到视频定制（CTVC）问题，具备现实意义。
- **方法创新性**：
  - 使用层特定概念令牌和正交损失保持概念独特性，是针对视频扩散模型持续学习的新探索。
  - 任务感知聚合策略在测试时动态加权，无需重放旧数据，符合隐私和效率需求。
  - 利用注意力值引导噪声估计，自动对易忽视概念给予更多关注，巧妙解决概念忽视。
- **实验覆盖性**：在四种不同视频生成任务（单/多概念、风格迁移、编辑）上均进行了验证，展示通用性。
- **消融实验**：逐步验证了关键模块的有效性（表2），设计合理。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验局限**：
  - 多概念任务缺少定量评估（如指标表格），仅依赖定性图，说服力有限。
  - 未消融 CCS 模块（LRA 和 ANE）的独立贡献。
  - 使用的 CVC 数据集为作者自建，未说明是否公开，可能难以复现。
- **资源与可复现性**：未提供训练所需的 GPU 型号、数量、时间，影响可复现性。
- **潜在偏差风险**：
  - 所有对比方法均基于 DreamVideo，其本身作为基线在持续学习场景下可能有限，未与其他更强的 CTVG 方法（如 VideoBooth、ConceptMaster 等）对比。
  - 正交损失需要存储每个任务的概念子空间（R_u^l），当任务数极大时可能增加内存开销。
- **应用限制**：
  - 模型依赖于逐任务顺序训练，无法应对在线或流式变化。
  - 可控条件合成仅针对多概念定制，对其他任务（如风格迁移）的适用性未明确验证。
  - 对于语义相似度极高的概念，正交性约束可能过于严格，反而影响表达力。

（完）
