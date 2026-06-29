---
title: Subspace-Aware Graph Construction and Contrastive Alignment for Multimodal Recommendation with Large Language Models
title_zh: 基于子空间感知图构建和对比对齐的多模态推荐与大语言模型
authors: "Haodong Li, Lianyong Qi, Weiming Liu, Fan Wang, Chong Li, Shengye Pang, Wenwen Gong, Yanwei Xu, Xiaoxiao Chi, Yang Zhang, Xiaokang Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38533/42495"
tags: ["query:multimodal"]
score: 7.0
evidence: 多模态推荐，使用大语言模型进行图和对比对齐
tldr: 针对多模态推荐中模型仅捕获浅层语义、难以建模复杂跨实体关系的问题，提出SCALE框架，结合子空间感知图构建和对比对齐，利用大语言模型增强表示学习，有效融合多模态信息并抑制协同信号主导，提升了推荐性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38533/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 870, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38533/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1830, \"height\": 867, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38533/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 886, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38533/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 760, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38533/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 765, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38533/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38533/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1773, \"height\": 656, \"label\": \"Table\"}]"
motivation: 现有方法仅捕获浅层语义，难以建模复杂跨实体关系，且协同信号抑制语义知识。
method: 提出SCALE框架，结合子空间感知图构建和对比对齐，利用大语言模型增强多模态表示。
result: 在多个数据集上验证了框架的有效性，显著提升了推荐精度。
conclusion: 该方法有效融合多模态信息，为推荐系统提供了更丰富的语义理解。
---

## Abstract
Multimedia content offers additional context for recommender systems to better understand user interests. Existing studies on multimodal recommendation primarily focus on constructing item-item semantic graphs. However, most of these methods capture only shallow semantic structures based on feature similarity and struggle to model more complex or cross-entity semantic relationships (e.g., user-item). Moreover, in these methods, collaborative signals often dominate and suppress semantic knowledge, which limits its role in representation learning. To address these issues, we propose SCALE, a novel framework that combines subspace-aware graph construction and contrastive alignment for multimodal recommendation with large language models. Specifically, we first use large language models and encoders to extract user and item features. Following the subspace clustering assumption, we apply the Orthogonal Matching Pursuit algorithm to mine complex semantic structures within the item-item, user-user, and user-item spaces, and integrate them into a unified semantic graph. We then perform graph convolution on both the semantic and interaction graphs, and aggregate the results for recommendation. Furthermore, contrastive losses are employed to enhance semantic fusion and alignment. Extensive experiments on five real-world datasets demonstrate that SCALE significantly outperforms state-of-the-art multimodal recommendation models, highlighting its effectiveness in modeling complex relationships and integrating semantic knowledge with collaborative signals.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：多模态推荐系统（MRS）面临两个关键挑战：  
  - 挑战1：如何从多模态内容中有效提取全面的语义知识？  
  - 挑战2：如何适当地将语义知识与协同信号（用户-物品交互）整合？  
- **现有方法的不足**：  
  - 大多数方法仅基于特征相似性构建物品-物品语义图，捕获的是浅层语义结构，难以建模更复杂的跨实体语义关系（如用户-物品）。  
  - 协同信号往往主导并压制语义知识，限制了语义在表示学习中的作用（例如，FREEDOM等方法中语义区分度不足）。  
- **论文目标**：提出一种新框架，能够同时捕获复杂、跨实体的语义关系，并有效融合语义知识与协同信号，提升推荐性能。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：  
  - 利用大语言模型（LLM）生成用户和物品的语义档案；  
  - 基于子空间聚类假设，使用正交匹配追踪（OMP）算法挖掘物品-物品、用户-用户、用户-物品空间中的复杂语义结构，构建子空间感知图（SAG）；  
  - 同时构建特征相似图（FSG）以捕获浅层成对关系；  
  - 将SAG与FSG融合为统一语义图；  
  - 分别在交互图和语义图上进行图卷积；  
  - 引入对比损失实现语义对齐和关系对齐，使得语义知识在最终表示中发挥更大作用。

- **关键技术细节**：  
  1. **档案生成与多模态编码**：  
     - 使用LLM（如Llama-3.2-3B）和提示（prompt）生成物品档案 \(F_i\) 和用户档案 \(F_u\)；  
     - 文本编码器（如Izacard et al. 2022）提取文本特征 \(x^t\)，视觉编码器（He & McAuley 2016a）提取图像特征 \(x^v\)。  
  2. **子空间感知图（SAG）构建**：  
     - 对每个用户 \(u\)，假设其表示可由字典（相似用户特征）稀疏重构，使用OMP优化 \(\min \|c_u\|_1\) s.t. \(x^t_u = D_u c_u\)，得到稀疏系数 \(c_u\)，形成用户-用户图 \(C_U\)；  
     - 类似地构建物品-物品图 \(C_I\) 和用户-物品图 \(C_{UI}\)。  
     - 算法1描述了OMP：初始化残差，迭代选取最相关原子，更新支持集，求解最小二乘，更新残差，最后将系数二值化。  
  3. **特征相似图（FSG）构建**：  
     - 使用余弦相似度，top-\(k_f\) 最近邻构建稀疏邻接矩阵 \(G\)；  
     - 分别构建用户-用户、物品-物品（视觉和文本）、用户-物品相似图。  
  4. **语义图融合**：  
     - 对每对实体，SAG和FSG进行元素级逻辑与（\(\oplus\)）得到最终语义图 \(\hat{G}\)。  
  5. **双图卷积**：  
     - 交互图上 \(L_I\) 层GCN（LightGCN风格），取各层平均得到 \(\tilde{H}\)；  
     - 语义图上 \(L_S\) 层GCN，取最后一层得到 \(\hat{H}\)。  
  6. **对比对齐**：  
     - **语义对齐损失** \(L_{align}^s\)：拉近交互表示 \(\tilde{h}\) 与语义表示 \(\hat{h}\) 对应实体（公式8）；  
     - **关系对齐损失** \(L_{align}^r\)：在最终表示 \(H = \tilde{H} + \hat{H}\) 上，将SAG中连接的实体（正对）拉近，无连接实体（负对）推远（公式10，包括用户-用户、物品-物品、用户-物品）。  
  7. **优化**：  
     - BPR损失 \(L_{bpr}\)，总损失 \(L = L_{bpr} + \lambda_s L_{align}^s + \lambda_r L_{align}^r\)。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**（共5个真实数据集）：  
  - Amazon子集：Baby、Sports、Clothing（包含文本和图像）  
  - Book、Yelp（用于与LLM增强模型的对比）  
- **基准与对比方法**：  
  - 传统推荐：BPR、LightGCN、LayerGCN  
  - 多模态推荐：VBPR、LATTICE、SLMRec、BM3、FREEDOM、MGCN、LGMRec、DiffMM、MENTOR  
  - LLM增强推荐：KAR、RLMRec（在Book和Yelp上对比）  
- **评估指标**：Recall@10, Recall@20, NDCG@10, NDCG@20  
- **实现细节**：  
  - LLM使用Llama-3.2-3B  
  - 文本特征维度768，图像特征维度4096  
  - 嵌入维度d=64，batch size=2048，学习率1e-3，Adam优化器  
  - 损失权重 \(\lambda_s=1e-2\)，\(\lambda_r=5e-2\)，温度 \(\tau_s=0.6,\tau_r=0.2\)  
  - 稀疏度 \(k_o\) 从{2,5,10,12,15}选择，\(k_s=800,k_f=5\)  
  - 交互图层数 \(L_I\) 和语义图层数 \(L_S\) 从1到5选择  
  - 采用早期停止，基于验证集Recall@20

## 4. 资源与算力

- 文中未明确说明使用的GPU型号、数量以及训练时长。  
- 仅提及使用Llama-3.2-3B作为LLM生成档案，未提供计算资源细节。

## 5. 实验数量与充分性

- **实验数量**：  
  - 在5个数据集上进行主实验（表1、表2）  
  - 消融实验（图4a）：逐一移除子组件（LLMs、SAG、FSG、语义对齐损失、关系对齐损失、跨实体关系等）  
  - 可视化分析（图1、图3、图4b-c）：t-SNE显示表示分布  
  - 敏感性分析（图5）：对齐损失权重、负样本大小、稀疏度、图卷积层数  
- **充分性评估**：  
  - 实验设计较为全面，覆盖了主要性能对比、组件贡献、超参数影响和可视化解释。  
  - 公平性：与SOTA模型在同一设置下比较，采用公开基准和常见协议。  
  - 但缺少对不同LLM选择、更大规模数据集、冷启动或跨域场景的实验。

## 6. 论文的主要结论与发现

- SCALE在所有5个数据集上均显著优于SOTA多模态推荐模型（表1），在Recall@20上相对最强基线提升7.68%~27.96%。  
- 与LLM增强模型（KAR、RLMRec）对比，SCALE也取得更好结果（表2），原因是其避免了直接引入文本特征带来的噪声，保持协同信号和语义知识的独立性。  
- 消融研究凸显了每个组件的必要性，尤其是LLM档案生成、SAG、FSG以及两种对齐损失。  
- 关系对齐损失（\(L_{align}^r\)）有效增强了类别间区分度（图4c）。  
- 超参数分析给出了合理的取值范围（如稀疏度 \(k_o=10\)，交互图层数 \(L_I=2\) 或5最优）。

## 7. 优点

- **方法论创新**：  
  - 首次将子空间聚类假设和OMP应用于多模态推荐语义图构建，能够捕获复杂组合关系和跨实体联系。  
  - 双图卷积结构并配合两种对比对齐损失，实现了语义知识与协同信号的有效分离与融合。  
- **实验充分**：覆盖多个数据集、多种基线，对模型各组件和超参数做了深入分析。  
- **可视化**：t-SNE直观展示了表示空间的改善，增强说服力。  
- **代码与框架**：基于MMRec实现，便于复现与扩展。

## 8. 不足与局限

- **依赖文本质量**：如Clothing数据集存在大量缺失描述（93.83%）和文本冗余（94.10%），导致性能提升有限；模型高度依赖LLM生成档案的准确性。  
- **计算资源未公布**：缺乏训练时间、GPU型号等信息，不利于评估实际部署成本。  
- **实验覆盖有限**：未测试跨域推荐、冷启动用户/物品等更具挑战的场景；未与更多类型LLM（如GPT-4）对比。  
- **潜在偏差风险**：仅使用单一LLM（Llama-3.2-3B），不同LLM生成质量可能影响结果；数据集多来自亚马逊，领域多样性不足。  
- **关系对齐负采样**：仅随机采样1个负例，文中表明对性能不敏感但可能不是最优策略；大负样本增加内存且收益有限。

（完）
