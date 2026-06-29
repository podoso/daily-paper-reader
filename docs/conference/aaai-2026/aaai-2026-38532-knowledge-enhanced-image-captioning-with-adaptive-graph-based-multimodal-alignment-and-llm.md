---
title: Knowledge-Enhanced Image Captioning with Adaptive Graph-based Multimodal Alignment and LLM
title_zh: 基于自适应图多模态对齐和LLM的知识增强图像描述
authors: "Guoyi Li, Die Hu, Haozhe Li, Zhongjiang Yao, Wei Mi, Zongzhen Liu, Xiaodan Zhang, Honglei Lyu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38532/42494"
tags: ["query:multimodal"]
score: 9.0
evidence: 图像描述，知识增强，多模态对齐，大语言模型
tldr: 针对大语言模型在开放世界图像描述中遇到未见实体时产生模糊和幻觉的问题，提出AKGMA，通过自适应知识图谱引导的多模态对齐，融合外部知识并利用LLM推理，显著提升描述准确性和知识合理性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38532/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 834, \"height\": 1033, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38532/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38532/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1799, \"height\": 881, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38532/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 837, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38532/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 783, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38532/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1832, \"height\": 744, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38532/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38532/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 855, \"height\": 386, \"label\": \"Table\"}]"
motivation: 现有大语言模型在开放世界场景中面对未见实体时，描述模糊且易产生知识幻觉。
method: 提出AKGMA，利用自适应知识图谱引导的多模态对齐，结合视觉知识推理和LLM增强。
result: 在多个图像描述基准上显著提升准确率，减少幻觉。
conclusion: 该方法有效融合外部知识，提升了开放场景下的图像理解能力。
---

## Abstract
Image captioning is crucial for multimodal understanding, bridging visual content and natural language. Despite recent advancements in Large Multimodal Models (LMMs), when faced with unseen entities or scenes in the open world, even when attempting to leverage learned knowledge, models still struggle with vague and inaccurate descriptions, and may even generate knowledge hallucinations. A key reason is that the model fails to effectively integrate knowledge with visual information, limiting its understanding of visual content. Thus, we propose Adaptive Knowledge Graph-guided Multimodal Alignment (AKGMA) for image captioning, which enhances semantic understanding in open-world scenes through visual knowledge reasoning, reducing knowledge hallucinations and improving caption quality. It consist three key components: Entity-guided Knowledge Aligner (EKA), Adaptive Knowledge Graph Construction (AKGC), and Scene-Context Knowledge Adapter (SCKA). EKA connects visual entities to knowledge graphs, providing structured knowledge to a small language model, which interacts with a visual encoder to acquire visual knowledge. AKGC uses reinforcement learning to build image-relevant subgraphs to optimize knowledge prompts and improve knowledge hallucinations. SCKA leverages scene graph annotations to extract visual contextual knowledge and inject it into Large Language Models (LLMs), ensuring the generated descriptions are consistent with the image's details. Additionally, we introduce UniKnowCap, a new image knowledge description dataset spanning various open-world knowledge domains, designed to evaluate the knowledge accuracy and detail consistency of model-generated descriptions. Extensive experiments show our model outperforms baselines across multiple metrics.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：当前大型多模态模型（LMMs）在开放世界场景中面对未见实体或场景时，即使尝试利用已学知识，仍会生成模糊、不准确的描述，甚至出现**知识幻觉**（knowledge hallucination）。根本原因在于模型未能有效融合知识与视觉信息，对视觉内容的理解受限。
- **核心问题**：如何通过结构化外部知识增强LMMs对图像的理解，减少知识幻觉，同时保证描述与图像细节一致。
- **整体目标**：提出一种自适应知识图谱引导的多模态对齐方法（AKGMA），利用视觉知识推理提升开放世界图像描述的质量，并构建新数据集评估模型在知识密集型场景下的表现。

## 2. 论文提出的方法论

### 核心思想
通过三个模块协同工作，将外部结构化知识（知识图谱）和内部场景知识（场景图）注入LLM，从而提升描述的准确性和语义一致性。

### 关键技术细节

1. **Entity-guided Knowledge Aligner (EKA)**  
   - **实体链接**：使用Mask R-CNN检测图像中的物体，通过文本查询在Wikipedia中检索对应实体，再链接到知识图谱（KG）。  
   - **视觉-知识对齐**：利用CLIP提取图像特征，使用一个小语言模型（如OPT-1.3B）作为视觉知识生成器，通过交叉注意力层将图像特征与知识三元组提示对齐，最终通过线性投影层映射到LLM的语言空间。  
   - **公式**：$h_{vk} = \text{EKA}([h_{kp} || h_{kl}], h_I)$，$h_{ko} = W_k h_{vk} + b$。  
   - **训练数据**：从WIT数据集构建VKPairs（视觉-知识对），用于对齐视觉知识与结构化知识。

2. **Adaptive Knowledge Graph Construction (AKGC)**  
   - **动机**：知识图谱过大，无法将所有实体纳入提示。  
   - **方法**：将知识子图构建建模为**马尔可夫决策过程（MDP）**，使用强化学习（actor-critic）动态选择与图像最相关的实体和关系。  
   - **关键组成**：状态（图像、已选实体、已吸收实体、关系）、动作（从当前实体出发的所有出边）、转移、奖励函数（包括图像相关性奖励 $R_B$ 和终端奖励 $R_T$）。  
   - **奖励**：$R_B$ 基于CLIP多模态表示的余弦相似度；$R_T$ 结合CLIP对比损失和CIDEr分数。总奖励 $R(t) = \lambda R_B(t) + (1-\lambda) R_T(t)$。  
   - **策略网络**：使用图注意力机制和图像引导的实体相似度计算，输出动作概率。

3. **Scene-Context Knowledge Adapter (SCKA)**  
   - **动机**：仅依靠外部知识不够，还需利用图像内部物体之间的关系（空间、动作、交互）。  
   - **方法**：用预训练场景图生成器提取场景图 $G_c$，转换为场景图提示，通过自注意力、交叉注意力和MLP生成场景上下文向量，并注入LLM的每一层。  
   - **注入方式**：将SCKA的输出拼接至每层输入序列头部，逐步融合场景知识。

### 优化框架
- **多任务训练**：同时优化知识对齐损失（VKPairs上的交叉熵）和图像描述损失（MSCOCO上的交叉熵）。总损失：$L_{AKGMA} = \psi L_{s1} + L_{s2}$。  
- **Actor-Critic优化**：critic网络估计Q值，使用TD学习；actor通过策略梯度最大化期望奖励。

## 3. 实验设计

### 数据集
- **训练集**：MSCOCO训练集（通用图像描述） + VKPairs（从WIT构建的2M Wikipedia图像-描述-背景文本对，用于训练EKA）。  
- **测试集**：  
  - 内域：**MSCOCO Test**（标准benchmark）  
  - 外域：**KnowCap Test**、**NoCaps val**、**Flickr30k Test**  
  - 新数据集：**UniKnowCap**（5,873张图片，超26k描述，涵盖医学、科技、历史、美食等8个领域，每个图像5个人工标注参考描述）。

### 对比方法
- **零样本LLM方法**：OFA、CapDec、MiniGPT4、Qwen2.5-VL。  
- **微调方法**：ClipCap、SmallCap、FuseCap、ViECap、EVCap、Qwen2.5-VL†（同等指令微调）、BLIP K-Replay、OFA K-Replay。  
- **消融变体**：w/o KG（无外部知识）、w/o (SCKA&AKGC)、w/o AKGC、w/o VKPairs、w/o SCKA（即LD=0）、Static 1-order/2-order（固定一跳/两跳邻居替换AKGC）。

### 评价指标
- **传统指标**：BLEU-4 (B@4)、METEOR (M)、ROUGE (R)、CIDEr (C)、SPICE (S)。  
- **知识专用指标**：Knowledge Recognition Accuracy (RecogAcc)、CHAIRs/CHAIRi（物体幻觉率）、CLIP-Score (CLIP-S)。  
- **自然度评分**：使用GPT-4V对UniKnowCap随机500张图片进行1-10评分（Natural），关注物体、颜色、位置、关系错误。  
- **NoCaps**：分“近处 / 近域 / 远处”（In/Near/Out）报告CIDEr。

## 4. 资源与算力

- **论文中未明确说明**使用的GPU型号、数量及训练时长。仅提及采用CLIP、OPT-1.3B、Llama-2/Vicuna-7B、Qwen2.5-7B等模型，以及Mask R-CNN进行物体检测。训练规模包括VKPairs（2M图像-文本对）和MSCOCO，但具体的计算资源需求未披露。

## 5. 实验数量与充分性

- **共进行多组实验**：  
  - 在4个标准测试集（MSCOCO Test, KnowCap Test, NoCaps val, Flickr30k) 上对比9+种方法，报告5-8个指标。  
  - 在UniKnowCap上对比8种方法，报告RecogAcc、幻觉、CLIP-S等。  
  - **消融实验**：6种变体（w/o KG, w/o AKGC, w/o VKPairs, w/o SCKA, Static 1-order, Static 2-order），以及SCKA上下文长度LD=2/4/8的对比。  
  - **泛化分析**：按领域（品牌、美食、科技、历史、医学）分析RecogAcc，并关联预训练数据频率。  
  - **案例研究**：展示一张拿破仑图片的推理链。  
- **评估充分性**：实验设计较为全面，覆盖内域/外域、知识准确性、幻觉、语义一致性；消融实验验证了每个模块的必要性；但未涉及更细粒度的参数分析（如RL学习率、奖励权重λ的影响），也未在更多尺度的LLM上验证（仅使用7B规模）。

## 6. 论文的主要结论与发现

1. **AKGMA显著优于现有方法**：在MSCOCO Test上CIDEr达到149.3（Qwen2.5-7B基座），远超OFA K-Replay（138.1）和EVCap（140.1），在KnowCap Test上RecogAcc达81.5%，CHAIRs低至6.9%。  
2. **三个模块均有效**：去除AKGC或SCKA均导致性能下降，尤其使用静态知识子图（Static 1-order/2-order）会引入噪声（CS、CI升高）。  
3. **EKA模块是关键**：即使不使用AKGC和SCKA（w/o AKGC&SCKA），相比直接微调的Qwen2.5-VL†，EKA仍带来RecogAcc提升约(57.4% vs 40.8%)，证实知识对齐的重要性。  
4. **泛化能力强**：在少见的领域（如签名类食品、医学）中，AKGMA的RecogAcc明显高于依赖预训练频率的BLIP K-Replay；且性能受知识频率影响较小。  
5. **UniKnowCap提供了更具挑战的评估基准**，能有效区分模型的知识理解能力。

## 7. 优点（方法或实验设计亮点）

- **模块化设计**：将外部知识对齐、自适应知识子图选择和内部场景注入解耦，各模块可独立训练与替换，灵活性高。  
- **创新的RL子图构建**：采用图强化学习从大型KG中动态选择相关三元组，避免了固定跳数导致的噪声或冗余，且通过图像导向的奖励函数优化选择。  
- **双重知识融合**：既利用结构化的外部KG知识（通过EKA），又利用场景图中的内部关系（通过SCKA），互补性强。  
- **新数据集贡献**：UniKnowCap规模大（5,873图像，超26k描述）、覆盖多领域，且每图5个精心撰写的参考描述，能更好评估模型的跨领域知识推理能力。  
- **充分的消融与泛化分析**：验证了每个组件的贡献，并分析了领域频率对性能的影响，揭示方法对数据偏差的鲁棒性。  
- **实验公平性**：与LLM-based方法对比时，AKGMA使用了同量级的基座模型（Vicuna-7B, Qwen2.5-7B），并标注了“†”表示使用相同指令微调数据。

## 8. 不足与局限

- **工程复杂性高**：需同时维护Mask R-CNN、CLIP、OPT、LLM、场景图生成器、RL策略网络等，训练和推理流水线较长。  
- **资源开销未说明**：未报告训练所需GPU型号/数量/时间，读者难以判断其可重复性和实际部署成本。  
- **依赖外部KG质量**：知识图谱的完整性、实体链接的准确性直接影响EKA和AKGC的效果；若KG缺失目标实体或关系，模型可能退化为基线。  
- **RL训练稳定性**：基于策略梯度的方法可能面临奖励稀疏、训练不稳定等问题，论文未提供reward曲线或超参数调节细节。  
- **评估局限**：UniKnowCap虽大，但仍为人工标注，可能仍存在标注偏差；仅用500张图片进行GPT-4V自然度评分，样本量偏少。  
- **LLM规模局限**：仅测试了7B级别的模型，未探索更大模型（13B/70B）下的表现，可能限制了知识注入的效果上限。  
- **应用限制**：模型针对图像描述任务，未验证在VQA、视觉推理等其他多模态任务上的泛化能力。

（完）
