---
title: Task-Constrained Optimization for Entity-Relation Extraction
title_zh: 面向实体关系抽取的任务约束优化
authors: "xiaojun sheng, Shilong Wei, Wang Yafei, Wenhao Jiang, Minmin Li"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=R900G8z0cm"
tags: ["query:ie"]
score: 9.0
evidence: 基于约束多任务优化的实体关系抽取
tldr: "多任务实体关系抽取中存在任务干扰问题。本文提出基于双曲障碍函数的自适应分层优化框架，将实体识别作为硬约束，关系分类自适应加权，在五个基准上提升三元组F1达6.4%。该方法可推广至结构预测任务。"
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-r900g8z0cm/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1438, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-r900g8z0cm/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1423, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-r900g8z0cm/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1429, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-r900g8z0cm/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 924, \"height\": 571, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1409, \"height\": 1128, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 766, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1117, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1150, \"height\": 406, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1261, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1460, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1067, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-r900g8z0cm/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 709, \"height\": 301, \"label\": \"Table\"}]"
motivation: 多任务学习中的任务干扰缺乏显式结构优先级机制。
method: 提出双曲障碍自适应分层优化，将实体识别设为动态硬约束。
result: "在五个实体关系抽取基准上三元组F1提升高达6.4%。"
conclusion: 该约束优化框架有效缓解任务干扰，可推广至其他结构预测。
---

## Abstract
Multi-task learning for entity-relation extraction often suffers from implicit task interference and lacks explicit mechanisms to enforce structural task prioritization. We propose Hyperbolic Barrier-based Adaptive Hierarchical Optimization, a constraint-driven optimization framework that formulates entity recognition as a dynamic hard constraint via a numerically stable hyperbolic barrier function, while adaptively reweighting relation classification through a curriculum-based thresholding strategy. This principled framework enforces strict task prioritization throughout training, yielding absolute improvements of up to $6.4\%$ in triplet F1 across five entity-relation extraction benchmarks. Furthermore, the proposed method generalizes effectively to structurally divergent domains such as recommender systems. Our findings underscore that explicitly modeling task hierarchies through constrained optimization represents a critical yet underexplored paradigm for achieving stable and effective multi-task learning.

---

## 论文详细总结（自动生成）

# 论文总结：Task-Constrained Optimization for Entity-Relation Extraction

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：实体关系抽取（ERE）是一个多任务学习问题，包含实体识别和关系分类两个子任务。两者存在非对称依赖：关系分类只有在实体边界正确识别时才有意义。现有方法通常平等优化两个任务，导致隐式任务干扰，且缺乏显式的结构优先级机制。
- **背景**：主流多任务学习（如加权求和、梯度平衡、Pareto优化）虽然缓解了梯度冲突，但并未在优化过程中嵌入任务层次依赖。作者认为，关系分类只有在实体识别充分后才能可靠学习，因此需要一种能够强制执行“实体优先”原则的优化框架。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将实体识别视为硬约束，关系分类作为在约束满足后的优化目标。通过双曲障碍函数将约束融入损失函数，实现可微的优先级控制。
- **关键技术细节**：
  - **约束优化问题**：  
    min L_rel(θ)  s.t. L_ent(θ) ≤ ε_t  
    其中ε_t是动态阈值。
  - **双曲障碍函数**：  
    φ(x) = tanh(3x + 1)，x = L_ent - ε_t。  
    该函数单调递增、全局Lipschitz连续（导数为α·sech²，有界于3），避免传统对数/倒数障碍函数在边界附近的梯度爆炸。
  - **最终损失**：  
    L_final = φ(x) * L_ent + (1/(1+φ(x))) * L_rel。  
    当实体损失大于阈值（L_ent > ε_t）时，φ→1，实体项主导；随着约束满足，关系项权重逐渐增加。
  - **自适应阈值调度**（课程学习）：  
    ε_{t+1} = ε_t * 0.95^{δ(L_ent ≤ ε_t)}。  
    仅在约束满足时才衰减阈值，使早期探索宽松，后期收紧。
  - **推广到多级任务**：对于N个有序任务，损失可递归定义为：  
    L_final = φ(L_1-ε_1)L_1 + Σ_{i=2}^N [L_i / (1+φ(L_{i-1}-ε_{i-1}))]。

- **算法流程**：
  1. 编码文档，计算实体损失L_ent和关系损失L_rel。
  2. 计算约束违反x = L_ent - ε_t。
  3. 计算障碍函数φ(x) = tanh(3x+1)。
  4. 计算最终损失L_final。
  5. 反向传播，更新模型参数。
  6. 若L_ent ≤ ε_t，则衰减ε_t：ε_{t+1} = ε_t * 0.95。
  7. 重复直至收敛或早停。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：五个ERE基准，涵盖不同领域和粒度：
  - 句子级：NYT（新闻）、WebNLG（维基百科）。
  - 文档级：DocRED（维基百科）、CDR（生物医学）、GDA（生物医学）。
  另在推荐数据集KuaiRand1k（八种用户行为，形成决策层次）上评估跨域泛化。
- **基准（基线）**：
  - ERE基线：BADS, SPN4RE, ERFD-RTE, ERGM, MFSF。
  - 多任务优化对比方法：PCGrad, IMTL-GG, AdaTask, NMT, DRGrad。
- **评估指标**：关系F1、实体F1、三元组F1。

## 4. 资源与算力
- **文中提及**：使用NVIDIA RTX 4090 GPU，训练100个epoch，batch size为4，早停基于验证集三元组F1（连续10个epoch无提升则停止）。
- **未明确说明**：具体GPU数量、总训练时长、各实验的随机种子次数等。

## 5. 实验数量与充分性
- **实验数量**：
  - 主表：5个模型 × 5个数据集 = 25组对比，每组报告加/不加HB-AHO的结果。
  - 与MTL方法对比：在DocRED上与5种方法比较。
  - 消融实验：阈值ε敏感性（7个值）、障碍函数类型（9种）、课程衰减因子γ（5个值）。
  - 跨域泛化：在KuaiRand1k上测试6个骨干模型，共48个结果。
- **充分性**：覆盖了多种架构、多种任务粒度、参数敏感性和域迁移，实验设计较广泛。但缺少多次随机重复实验的报告（如标准差），以及统计显著性检验。

## 6. 主要结论与发现
- HB-AHO在五个ERE基准上一致提升三元组F1，最大绝对增益达6.4%（BADS on NYT）。
- 在文档级数据集（DocRED, CDR, GDA）上增益更为显著，因为实体错误会扩散到跨句推理中。
- 相比PCGrad、IMTL-GG等MTL方法，HB-AHO在DocRED上三元组F1高出约2-4%，表明显式层次约束优于梯度平衡。
- 障碍函数消融显示：双曲函数（tanh）优于多项式、sigmoid、softplus等，因其兼具单调性、有界梯度和平滑过渡。
- 跨域泛化验证：在推荐系统上平均AUC提升2.1-2.6%，说明该方法可推广至其他层次依赖任务。

## 7. 优点
- **创新性**：将约束优化思想引入多任务层次学习，设计了数值稳定的双曲障碍函数，并辅以课程调度，克服了传统障碍函数的梯度不稳定问题。
- **理论上**：证明了单调性、Lipschitz连续性、KKT等价性、渐近可行性，以及Lyapunov稳定性。
- **实验覆盖**：跨越句子级、文档级ERE及推荐域，对比多种骨干和MTL方法，消融充分。
- **实用性**：即插即用，无需修改模型架构；对超参数（初始阈值、衰减因子）鲁棒性强，简化调参。
- **跨域迁移**：展示了方法在非NLP任务上的有效性，增强了泛化主张。

## 8. 不足与局限
- **实验局限**：
  - 仅报告单次结果，未提供多次运行的均值和方差，无法评估统计显著性。
  - 在饱和句子级数据集上，关系F1偶有下降（如SPN4RE在NYT上-0.8%），可能增加应用风险。
  - 未在更多样化的层次任务（如视觉-语言、多步推理）上验证。
- **理论假设**：理论分析假设任务损失光滑且凸，但实际深度模型损失非凸，KKT条件的严格适用性存疑。
- **计算成本**：虽然声称复杂度优于Pareto方法，但未提供实际训练时间对比。
- **依赖预训练编码器**：实验基于DeBERTa-v3，方法对编码器是否敏感未探讨。
- **阈值初始化**：初始ε设为0.05，虽鲁棒但未提供选择依据；在极端任务不平衡下可能需要调整。

（完）
