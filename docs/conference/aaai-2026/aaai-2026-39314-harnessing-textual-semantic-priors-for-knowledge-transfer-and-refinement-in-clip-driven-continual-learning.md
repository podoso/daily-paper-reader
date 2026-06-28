---
title: Harnessing Textual Semantic Priors for Knowledge Transfer and Refinement in CLIP-Driven Continual Learning
title_zh: 利用文本语义先验实现CLIP驱动的持续学习中的知识迁移与细化
authors: "Lingfeng He, De Cheng, Di Xu, Huaijie Wang, Nannan Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39314/43275"
tags: ["query:continual"]
score: 8.0
evidence: 利用文本语义先验的CLIP驱动持续学习
tldr: 视觉语言模型的持续学习面临稳定性-可塑性困境。本文利用CLIP中的丰富文本语义先验，进行语义相关的知识迁移和细化，避免无关任务干扰。在多个持续学习基准上，该方法有效平衡了稳定性和可塑性，优于忽略语义相关性的方法。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有CLIP持续学习方法在骨干训练时忽视语义相关性，导致任务干扰破坏稳定性-可塑性平衡。
method: 基于CLIP文本语义先验，按语义相关性进行知识迁移和特征细化。
result: 在多个持续学习基准上取得更优的稳定性和可塑性平衡。
conclusion: 文本语义先验能有效指导视觉模型的持续学习。
---

## Abstract
Continual learning (CL) aims to equip models with the ability to learn from a stream of tasks without forgetting previous knowledge. With the progress of vision-language models like Contrastive Language-Image Pre-training (CLIP), their promise for CL has attracted increasing attention due to their strong generalizability. However, the potential of rich textual semantic priors in CLIP in addressing the stability–plasticity dilemma remains underexplored. During backbone training, most approaches transfer past knowledge without considering semantic relevance, leading to interference from unrelated tasks that disrupt the balance between stability and plasticity. Besides, while text-based classifiers provide strong generalization, they suffer from limited plasticity due to the inherent modality gap in CLIP. Visual classifiers help bridge this gap, but their prototypes lack rich and precise semantics. To address these challenges, we propose Semantic-Enriched Continual Adaptation (SECA), a unified framework that harnesses the anti-forgetting and structured nature of textual priors to guide semantic-aware knowledge transfer in the backbone and reinforce the semantic structure of the visual classifier. Specifically, a Semantic-Guided Adaptive Knowledge Transfer (SG-AKT) module is proposed to assess new images' relevance to diverse historical visual knowledge via textual cues, and aggregate relevant knowledge in an instance-adaptive manner as distillation signals. Moreover, a Semantic-Enhanced Visual Prototype Refinement (SE-VPR) module is introduced to refine visual prototypes using inter-class semantic relations captured in class-wise textual embeddings. Extensive experiments on multiple benchmarks validate the effectiveness of our approach.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：持续学习（Continual Learning, CL）旨在让模型从连续的任务流中学习而不遗忘先前知识。现有基于CLIP（对比语言-图像预训练）的持续学习方法虽然利用其强泛化能力，但未能充分发挥CLIP中**丰富的文本语义先验**来解决稳定性-可塑性难题。
- **核心挑战**：
  - **骨干网络训练中的语义干扰**：大多数方法在迁移过去知识时不考虑语义相关性，导致无关任务的知识干扰当前学习，破坏稳定性-可塑性平衡。
  - **分类器中的模态鸿沟**：纯文本分类器泛化强但可塑性有限，因为CLIP存在固有的模态鸿沟（视觉与文本特征在嵌入空间分离）；视觉分类器可帮助桥接鸿沟，但其原型缺乏丰富精确的语义。
- **整体目标**：提出一个统一框架，利用文本语义先验的**抗遗忘性**和**结构化特性**，实现语义感知的知识迁移和视觉分类器的语义增强，从而平衡稳定性与可塑性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用CLIP文本分支提供的稳定语义指导选择性知识迁移，并通过文本语义关系细化视觉原型，构建混合分类范式桥接模态鸿沟。
- **整体框架（SECA）**：基于CLIP（视觉编码器 \(F_V\)、文本编码器 \(F_T\)），包含两个核心模块：
  1. **语义引导的自适应知识迁移（SG-AKT）**
     - 为新图像提取**语义向量**（通过文本编码器结合当前及历史任务的文本提示获得）。
     - 维护一个**历史适配器池**（Adapter Pool），存储先前任务的轻量适配器（每个适配器对应一个历史模型）。
     - 计算新图像与每个历史适配器视觉表示的**语义相关性**（通过两个可学习的语义投影器 \(W_S, W_V\) 将文本和视觉特征映射到共享空间，计算余弦相似度）。
     - 根据相关性分数对池中适配器输出的视觉知识进行**实例自适应聚合**（加权求和），得到聚合特征 \(V_{agg}\)。
     - 以 \(V_{agg}\) 作为教师信号，通过KL散度损失（\(L_{SG-AKT}\)）蒸馏当前模型，优先学习相关历史知识，抑制无关知识。
     - 适配器池管理：采用基于相关性分数的**效用评分**和动量更新策略，移除效用最高的旧适配器（即知识已被充分迁移的），保持池大小固定。
  2. **语义增强的视觉原型细化（SE-VPR）**
     - 对于每个可见类，从文本编码器获得**类级文本嵌入**，并通过可学习投影器 \(H_{proj}\) 建模类间语义**亲和度矩阵**。
     - 利用亲和度分数对粗视觉原型（由CLIP视觉编码器在任务开始时提取的平均特征）进行**加权细化**，得到语义增强的视觉原型 \(\hat{c}_{V,k}\)。
     - 训练时使用交叉熵损失 \(L_{ce-V}\) 和原型一致性正则化 \(L_{reg}\)（保持旧类原型稳定），使视觉分类器继承文本语义结构。
     - 推理时采用**混合分类**：结合所有任务文本分类器预测和细化后的视觉分类器预测，取平均后输出最高分数类别。
- **训练目标**：总损失 \(L = L_{ce-T} + L_{agg} + \beta L_{SG-AKT} + L_{ce-V} + L_{reg}\)，其中 \(\beta\) 随任务增加而增大。

### 3. 实验设计

- **数据集**：三个代表性CIL基准：
  - **ImageNet-R**（30,000张图像，200类，含多种视觉风格）
  - **ImageNet-A**（7,500张挑战性对抗样本，200类）
  - **CIFAR-100**（60,000张32×32图像，100类）
- **任务设置**：两种增量设置——**10-split**（10个任务）和**20-split**（20个任务），采用无重放（rehearsal-free）类增量学习（Class-Incremental Learning）。
- **评价指标**：
  - **Last session accuracy (Last)**：最后任务完成后所有类的准确率。
  - **Average accuracy (Avg)**：所有增量任务的平均准确率。
- **对比方法**：包括多种PEFT-based持续学习方法：
  - Prompt-based：L2P, DualPrompt, CODA-Prompt, VPT-NSP等
  - Adapter-based：RAPF, CLAP, PROOF, DIA, SSIAT等
  - 基线：Zero-shot CLIP, 以及基于ViT-21K或CLIP骨干的模型
  - 特别地，对比了RAPF和VPT-NSP的无重放版本（RAPF†, VPT-NSP†）及有重放版本。
- **实现细节**：
  - 骨干：CLIP ViT-B/16（OpenAI预训练），优化器Adam，学习率0.001。
  - 训练轮数：ImageNetR/ImageNetA每任务10轮，CIFAR100每任务3轮。
  - 批大小：64（ImageNetR/A）和100（CIFAR100）。
  - 适配器池容量 \(|P|=5\)，温度因子 \(\tau'=0.05\)（训练）和20.0（蒸馏）。

### 4. 资源与算力

- 明确说明：所有实验在**单张NVIDIA RTX 3090 GPU**上完成。
- 未报告总训练时长或单个任务的具体时间，但提到每个任务训练3-10轮，批大小为64-100，因此整体算力需求适中。

### 5. 实验数量与充分性

- **实验数量**：相当充分，包括：
  - 主实验：在3个数据集×2种任务划分（共6种场景）下与10+种SOTA方法对比（Tabel 1 & 2）。
  - 消融实验：
    - 各组件有效性（H-PEFT, SG-AKT, SE-VPR） → Table 3。
    - SG-AKT与四种替代蒸馏策略对比（Seq., CLIP-KD, Vanilla, Avg-KD） → Table 4（含有无SE-VPR两种情况）。
    - SE-VPR与四种分类器设计对比（Only Text, Centroid(CLIP), Centroid(Adapted), Linear） → Table 5。
    - 超参数分析：适配器池大小 \(|P|\) 和温度 \(\tau'\) 的灵敏度 → Figure 3（以曲线图展示）。
- **公平性**：
  - 对比方法中，特意复现了RAPF†和VPT-NSP†的无重放版本，确保与SECA（无重放）公平比较。
  - 报告三次随机种子的平均结果及标准差（Table 3,4,5中标注）。
  - 消融实验中严格控制变量（如SG-AKT与替代方案比较时，均基于相同的H-PEFT基线）。
- **充分性**：实验设计全面，覆盖了方法各模块、不同蒸馏策略、不同分类器设计、关键超参数，以及多数据集多任务划分。统计显著性（标准差）体现结果稳定性。结论具有说服力。

### 6. 论文的主要结论与发现

- **SG-AKT模块有效**：通过文本语义引导选择性知识迁移，相比平均聚合或最近任务蒸馏，在ImageNet-A上Last准确率提升0.77%~1.58%。
- **SE-VPR模块有效**：利用文本语义关系细化视觉原型，相比仅用粗原型或线性分类器，在ImageNet-A上Last准确率提升1.93%以上。
- **整体框架SECA达到SOTA**：在无重放设置下，SECA在10S-ImageNetR/ImageNetA上Last分别达83.18%/65.09%，超过最强对比方法VPT-NSP（有重放）的82.48%/61.42%。增强版SECA++进一步提升。
- **适配器池大小和温度参数鲁棒**：池大小≥5时性能饱和，温度较高的蒸馏更优。
- **文本语义先验是解决稳定性-可塑性难题的有效工具**，能同时改进知识迁移和分类器设计。

### 7. 优点：方法或实验设计上的亮点

- **方法创新性**：
  - 首次系统地将文本语义先验用于指导**选择性知识迁移**（SG-AKT），避免无关干扰。
  - 提出**语义增强的视觉原型细化**（SE-VPR），利用类间语义关系弥补模态鸿沟，与文本分类器形成混合预测。
- **实验设计亮点**：
  - 在多个数据集（含挑战性外分布数据集ImageNet-A）和两种任务划分下全面评估，涵盖无重放和带重放两个场景。
  - 消融实验充分：不仅拆分模块，还深入对比了不同蒸馏策略和分类器设计，验证每个设计的必要性。
  - 对关键超参数（池大小、温度）进行灵敏度分析，并给出推荐值。
  - 代码开源（GitHub），便于复现。
- **性能优势**：在无重放设置下即超越多数有重放方法，且SECA++（加轻量特征重放）进一步拉开差距，证明了框架的强基线和扩展性。

### 8. 不足与局限

- **实验覆盖局限**：
  - 只使用了三个数据集（ImageNet-R, ImageNet-A, CIFAR-100），未在更大规模或更多样化的数据集（如ImageNet-1K全类、DomainNet等）上验证，泛化性有待确认。
  - 任务划分只有10-split和20-split，未测试更细粒度（如5-split, 50-split）或长序列任务。
- **方法限制**：
  - 依赖CLIP预训练模型，可能迁移到其他VLM（如BLIP, ALIGN）时需要调整。
  - 适配器池和投影器增加少量额外参数，虽然算力要求低，但未详细分析参数开销。
  - 温度因子 \(\tau'\) 在训练和推理时分离（训练用0.05，蒸馏用20.0），需要手动调优，未见自适应机制。
- **潜在偏差风险**：
  - 所有实验在单GPU、固定随机种子下进行，未测试不同硬件或随机种子下的波动边界。
  - 未报告CIL场景下任务顺序敏感性（即不同任务顺序的影响），可能存在顺序偏差。
- **应用限制**：
  - 方法针对类增量学习（CIL），未验证其他CL设置（如任务增量、域增量）。
  - 假设任务边界已知且类别不重叠，在完全开放世界场景可能需额外处理。

（完）
