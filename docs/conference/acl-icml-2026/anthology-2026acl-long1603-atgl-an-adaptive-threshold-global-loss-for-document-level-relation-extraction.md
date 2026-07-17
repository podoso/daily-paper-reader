---
title: "ATGL: An Adaptive-Threshold Global Loss for Document-level Relation Extraction"
title_zh: ATGL：面向文档级关系抽取的自适应阈值全局损失
authors: "Huangming Xu, Fu Zhang, Zhixuan Yang, Lu Zhang, Jingwei Cheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1603.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 文档级关系抽取，自适应阈值损失
tldr: 文档级关系抽取作为多标签分类任务，现有解耦损失导致阈值不稳定和优化偏差。本文提出自适应阈值全局损失ATGL，通过联合优化正负类与阈值，克服了梯度冲突和样本不平衡问题。在多个DocRE数据集上，ATGL有效提升了关系抽取性能。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1603/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1316, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1603/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 725, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1603/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 715, \"height\": 347, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1603/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 785, \"height\": 920, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 722, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 575, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1651, \"height\": 1402, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 500, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1316, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 799, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1603/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1152, \"height\": 271, \"label\": \"Table\"}]"
motivation: 现有解耦损失在文档级关系抽取中导致阈值不稳和优化偏差。
method: 提出自适应阈值全局损失函数，统一优化正负类和阈值，缓解梯度冲突。
result: 在多个文档级关系抽取基准上取得最优结果。
conclusion: 联合优化阈值和损失可有效提升多标签关系抽取的稳定性。
---

## Abstract
Document-level relation extraction (DocRE) aims to determine which relations hold between a given entity pair within a document. As a multi-label classification task, the most commonly adopted paradigm introduces a learnable threshold to distinguish positive and negative classes for an entity pair. Under this paradigm, existing losses decouple the optimization into independent positive and negative losses, which interact solely with a shared threshold. This leads to two inherent limitations: (*i*) threshold instability caused by conflicting gradient updates from the decoupled losses; and (*ii*) optimization bias exacerbated by the severe imbalance between limited positive samples and abundant negative samples inherent in DocRE, which makes the model more likely to predict that no relation exists.To address these issues, we propose the **A**daptive-**T**hreshold **G**lobal **L**oss (ATGL). Unlike prior work, ATGL integrates positive, negative, and threshold optimization into a unified logit space and explicitly enforces ranking constraints on their contributions to the objective. Furthermore, ATGL incorporates an imbalance-aware optimization mechanism, thereby effectively addressing the severe class imbalance in DocRE. Our ATGL serves as a general optimization objective that can be readily applied to different DocRE models. Experiments on four datasets show that ATGL outperforms other DocRE losses and achieves state-of-the-art results, while consistently improving the performance of existing DocRE models. Code is available at https://github.com/xhm-code/ATGL.

---

## 论文详细总结（自动生成）

# 论文总结：ATGL: An Adaptive-Threshold Global Loss for Document-level Relation Extraction

## 1. 核心问题与整体含义（研究动机和背景）
- **研究任务**：文档级关系抽取（DocRE），需判断文档中给定实体对之间存在哪些关系，属于多标签分类任务。
- **现有范式**：主流方法引入可学习阈值（Adaptive Threshold Loss, ATL），将优化分解为独立的正例损失和负例损失，仅通过共享阈值交互。
- **两大根本缺陷**：
  - **阈值不稳定**：正、负损失对阈值产生冲突梯度更新（正损失驱使阈值降低，负损失驱使阈值升高），导致学习到的阈值偏离理想阈值。
  - **优化偏差加剧**：DocRE中负样本（无关系实体对）占绝对多数（如Re-DocRED中94%实体对无关系），主导负损失优化，使模型更倾向预测无关系，正损失难以抗衡。
- **本文目标**：提出统一优化框架，同时解决阈值不稳定和类别不平衡问题，作为通用损失函数适用于各类DocRE模型。

## 2. 方法论：核心思想、关键技术细节
### 2.1 核心思想
- **统一logit空间**：将正类、阈值类、负类的logits纳入同一个softmax，使概率相互依赖且可直接比较。
- **全局排序约束**：通过不同权重编码期望的全局顺序：正类得分 > 阈值 > 负类得分。
- **不平衡感知**：赋予正类更大权重（α>1），阈值权重为1，负类权重为0（仅通过softmax归一化间接贡献），从而抑制负类梯度主导，放大正类信号。

### 2.2 关键技术细节
- **损失函数定义**：
  \[
  L_{ATGL} = -\sum_{r \in \mathcal{R} \cup \{TH\}} w_r \cdot \log\left(\frac{\exp(\text{logit}_r)}{\sum_{r'\in \mathcal{R} \cup \{TH\}} \exp(\text{logit}_{r'})}\right)
  \]
  其中 \( w_r = \begin{cases} \alpha > 1, & r \in \mathcal{P}_T \\ 1, & r = TH \\ 0, & r \in \mathcal{N}_T \end{cases} \)
- **推导与理论分析**（附录A）：
  - 损失函数等价于匹配结构化目标分布，凸性（模平移不变性）保证唯一最优概率分布。
  - 最优解满足严格分组排序：所有正类得分 > 阈值得分 > 所有负类得分。
  - 梯度动态：阈值自校正至目标概率1/W，正类被放大至α/W，负类单调下降。

### 2.3 算法流程
- 前向传播：计算每个候选关系及阈值类的logit → 计算带权softmax交叉熵。
- 反向传播：按式(20)-(21)更新，负类始终被抑制，阈值自稳态调整。
- 推理：对每个实体对，将logit高于阈值的关系预测为存在。

## 3. 实验设计：数据集、基准、对比方法
### 3.1 数据集
- **四个DocRE数据集**：CDR（生物医学，二元任务）、DWIE（通用领域）、Re-DocRED（大规模，修正版）、DocGNRE（Re-DocRED增强版）。统计见表1。

### 3.2 基准与评估
- **Backbone模型**：ATLOP、DocuNet、KD-DocRE、DREEAM、TTM-RE、VaeDiff-DocRE。
- **编码器**：BERT-base 和 RoBERTa-large。
- **对比损失**：ATL、Balanced-Softmax、AML、AFL、NCRL、PEMSCL、HingeABL（含SAT/MeanSAT变体）、AMTL、ARPDL、CMM。
- **评估指标**：F1 和 Ign F1（去除训练集重叠事实）。

### 3.3 主要实验设置
- 多次随机种子取平均，使用GeForce RTX 3090 GPU。

## 4. 资源与算力
- **明确提及的硬件**：GeForce RTX 3090 GPU。
- **训练时间**：在表8中报告了各损失在ATLOP+BERT-base模型上训练30个epoch（batch size=4）的时间，ATGL约为40.71分钟，与基线相近。未说明GPU数量、总计算量或具体训练配置细节。论文未提供详细的资源消耗（如显存占用、总GPU小时数）。

## 5. 实验数量与充分性
- **大量系统性实验**：
  - **模型泛化实验**（表2）：6种不同DocRE模型×4个数据集×2种编码器，共48组对比，均显示ATGL带来一致提升（平均+2.80 F1）。
  - **损失对比实验**（表3）：在Re-DocRED、DocGNRE、DWIE、CDR上对比13种损失函数，ATGL全面最优。
  - **消融与深入分析**：
    - 阈值稳定性量化（RO分布，图2）：ATGL标准差最小（0.098）。
    - 全局排序一致性（OVR，图3）：ATGL违反率最低（0.259）。
    - 类别不平衡缓解分析（表4）：FN_NA和FN显著降低。
    - 假阳性归因分析（表5）。
    - 超参数α分析（图4，表10）。
    - 与LLM模型对比（表9）。
    - 计算开销对比（表8）。
    - 案例研究（表7）。
- **充分性评估**：实验覆盖多模型、多数据集、多编码器、多损失、多维度分析，设计公平（复现时统一框架），结论稳健。但未在更多多标签任务（如文本分类、图像标注）上验证通用性。

## 6. 主要结论与发现
- **ATGL在所有四个数据集上达到SOTA**：如Re-DocRED上F1 77.26，Ign-F1 76.05，超越之前最佳损失CMM分别+1.14和+1.29。
- **作为通用损失**，替换不同DocRE模型原有损失后，性能一致提升（平均+2.80 F1）。
- **有效解决阈值不稳定**：RO标准差从0.167（ATL）降至0.098（ATGL）。
- **有效缓解类别不平衡**：FN_NA和FN显著减少，FN/(FP+FN)从76.82%（ATL）降至58.06%。
- **计算成本与基线相当**，不引入额外负担。
- **理论保证**：损失函数凸性、唯一最优解、严格全局排序、稳定梯度动态。

## 7. 优点
1. **创新性**：首次将正、阈值、负类纳入统一logit空间并显式施加全局排序，从根本上解决ATL解耦优化导致的阈值不稳定。
2. **不平衡处理巧妙**：负类权重设为0，仅通过softmax分母影响，避免负类梯度主导；同时放大正类权重（α>1），在不引入复杂重采样或焦点损失机制下有效缓解类别不平衡。
3. **理论完备**：提供严格凸性证明、唯一最优解、全局排序推导、梯度动态分析，有较强数学依据。
4. **通用性强**：仅改变损失函数，不依赖特定模型结构，可即插即用，提升多种现有DocRE模型。
5. **计算效率高**：与标准ATL几乎相同的训练时间（40.71 vs 40.37分钟），无额外开销。
6. **实验充分公正**：多个数据集、多个模型、多个基线损失、多角度消融，结果一致且可复现（开源代码）。

## 8. 不足与局限
1. **假阳性率上升**：虽然FN大幅下降，但FP增加（表4）。作者通过归因分析发现额外FP集中在少数高频关系且多为类型一致的近误，但实际应用中高FP可能降低精确率，需要权衡。
2. **超参数α敏感度**：α取值依赖标签空间大小，不同数据集最佳α不同（表10），虽给出了粗略指导，但仍需在开发集上调优。
3. **实验覆盖范围有限**：仅在DocRE四个数据集上验证，未在更广泛的多标签分类任务（如文本分类、多标签图像识别）上测试通用性。
4. **理论假设的局限性**：最优解要求负类logit趋于负无穷（在softmax中），实际只能逼近，且极低logit可能影响数值稳定性。
5. **未探索多阈值机制**：ATGL采用单一阈值类，而某些复杂场景可能需要多个阈值或动态阈值。
6. **与LLM对比不够深入**：表9仅与有限LLM方法对比，且ATGL基于的预训练模型较小（BERT base/RoBERTa large），与8B参数的Llama3相比不公平，但作者仅作参照而非竞争。

（完）
