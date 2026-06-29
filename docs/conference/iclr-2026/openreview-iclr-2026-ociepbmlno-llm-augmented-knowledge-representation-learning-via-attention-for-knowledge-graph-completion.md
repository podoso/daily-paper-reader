---
title: LLM-AUGMENTED KNOWLEDGE REPRESENTATION LEARNING VIA ATTENTION FOR KNOWLEDGE GRAPH COMPLETION
title_zh: 基于注意力的大语言模型增强知识表示学习
authors: "Mengqing Wang, Peipei Li"
date: 2025-09-11
pdf: "https://openreview.net/pdf?id=OcIepBMLnO"
tags: ["query:llm"]
score: 5.0
evidence: 大语言模型增强知识图谱补全
tldr: 该论文提出LAKRA框架，利用大语言模型主动推理并生成符合模式的优质三元组，缓解知识图谱补全中长尾实体的数据稀疏问题。虽涉及知识图谱和关系表示，但核心是补全而非抽取，且未涉及多模态。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1160, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 962, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1434, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1445, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 833, \"height\": 1177, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 637, \"height\": 926, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 476, \"height\": 868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 567, \"height\": 999, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 545, \"height\": 898, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 572, \"height\": 994, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ociepbmlno/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1427, \"height\": 484, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 873, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 804, \"height\": 140, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1308, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1317, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1308, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1165, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 428, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 546, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 540, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 531, \"height\": 155, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 564, \"height\": 154, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1245, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 543, \"height\": 153, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 615, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ociepbmlno/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 573, \"height\": 298, \"label\": \"Table\"}]"
motivation: 知识图谱中长尾实体数据稀疏，现有隐式增强方法引入噪声。
method: 利用LLM显式生成高质量、符合模式的三元组作为数据增强，结合注意力机制学习表示。
result: 在知识图谱补全基准上缓解了数据稀疏问题，具体提升数值未在摘要中给出。
conclusion: LLM可有效增强知识图谱表示，但任务与实体关系抽取不同。
---

## Abstract
Knowledge Graph Completion (KGC) is a critical task, yet its performance is often hindered by the data sparsity problem arising from the long-tail distribution of entities. While existing works attempt to enrich representations by incorporating auxiliary information like entity descriptions, this kind of implicit learning approaches often proved ineffective due to the introduction of irrelevant noise. To address this, we propose a novel framework LAKRA, which shifts the paradigm from implicit knowledge encoding to explicit data augmentation. LAKRA leverages a Large Language Model (LLM) to proactively reason and generate high-quality, schema-compliant triples for sparse entities, mitigating data sparsity at its source. Besides, we design a powerful encoder-decoder architecture for representation learning, which features a query-aware hybrid attention encoder and a deep feature interaction decoder to capture complex structural and semantic patterns. Experiments conducted on the benchmark datasets demonstrate that LAKRA achieves highly competitive performance on link prediction tasks involving infrequent entities. Our work presents an effective new paradigm for tackling data sparsity in knowledge graphs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：知识图谱补全（KGC）中普遍存在的数据稀疏性问题，源于实体的长尾分布——大部分实体出现频次极低，导致基于嵌入或图神经网络的模型难以学习高质量表示。
- **现有方法局限**：已有工作尝试通过融合实体描述等辅助信息来隐式增强表示，但这类隐式学习方法常因引入无关噪声而效果有限；GNN 模型受限于邻域密度，LLM 直接被用作编码器或推理器时计算成本高且未解决图结构稀疏性本身。
- **本文动机**：将范式从隐式编码转变为显式数据增强，直接为目标稀疏实体生成高质量、符合图模式的新三元组，从根本上缓解数据稀疏问题。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
利用大语言模型（LLM，具体使用 DeepSeek-V3）的推理能力，基于实体类型约束和已有图结构先验，为低频“尾实体”显式生成合理的候选三元组；再通过一个强大的编码器-解码器架构对增强后的图进行表示学习并完成链接预测。

### 关键技术细节（三部分）

#### (1) LLM 驱动的显式数据增强
- **尾实体识别**：计算训练集中每个实体的度数（作为头尾的总次数），选取度最低的 20% 实体作为增强目标（记为 \( E_{\text{tail}} \)）。
- **类型约束候选集构建**：构建两个表：
    - 关系候选表 \( C_{\text{rel}} \)：实体类型 → 该类型作为头/尾时出现的高频关系（频率阈值过滤）。
    - 实体候选表 \( C_{\text{ent}} \)：关系 → 该关系头/尾实体的常见类型。
- **两阶段生成**：
    - 阶段1（关系生成）：给定尾实体 \( e_{\text{tail}} \)，利用 prompt 从 \( C_{\text{rel}} \) 中选取最可能的关系子集 \( R_{\text{pred}} \)。
    - 阶段2（实体生成）：对每个预测关系 \( r_{\text{pred}} \)，利用 prompt 从 \( C_{\text{ent}} \) 的候选实体池中选取最合适的实体 \( t_{\text{pred}} \)，构成完整三元组。
- **后过滤**：移除已存在于训练集的三元组；额外增加关系特定的启发式规则以降低噪声。

#### (2) 查询感知图注意力编码器（Hybrid Attention）
设计了一种混合注意力机制，使邻域聚合与特定查询关系相关：
- **查询感知多头交叉注意力**：从中心实体和查询关系生成 Q，从邻居实体和关系生成 K，并加入可学习的偏置项 \( b_{r_{ij}} \)。
- **MLP 加性注意力**：将中心实体、邻居实体、关系嵌入拼接后通过 MLP 非线性变换。
- **动态门控融合**：通过门控权重 \( g_{ij} \)（基于中心与邻居实体嵌入自适应计算）融合两种注意力分数。
- **消息聚合**：使用循环互相关（circular cross-correlation）函数融合邻居实体和关系，再用注意力加权求和更新实体表示。
- **残差连接**避免梯度消失和过平滑。

#### (3) 3D 深度特征交互解码器
- **高斯特征增强**：将原始实体/关系嵌入通过一组可学习高斯核映射到高维空间，得到非线性的增强表示 \( x^\Phi \)。
- **3D 卷积解码**：
    - 构造 5 层 3D 特征栈：\([\rho(r), \rho(e_h), \rho(r^\Phi), \rho(e_h^\Phi), \rho(r)]\)。
    - 使用 3D 卷积核同时处理相邻两层，捕捉原始-原始、原始-增强、增强-增强、增强-原始四种交互。
    - 输出交互向量 \( v_{hr} \)，与候选尾实体 \( e_t \) 计算余弦相似度作为预测得分。

#### 训练目标
- 主损失：标准交叉熵损失（正负采样）。
- 总损失：\( L_{\text{total}} = L_{\text{orig}} + \lambda L_{\text{aug}} \)，其中 \( L_{\text{aug}} \) 仅基于 LLM 生成的三元组计算，\(\lambda\) 为超参数。

## 3. 实验设计

### 数据集与场景
- **主数据集**：FB15k-237（14,541 实体，237 关系，272,115 训练三元组）和 WN18RR（40,493 实体，11 关系，86,835 训练三元组）。
- **补充数据集**：UMLS（小规模生物医学，135 实体，46 关系）和 FB15K（14,951 实体，1,345 关系）——用于验证泛化性。

### 评价指标：MRR、Hits@1、Hits@3、Hits@10（过滤设置）。

### 对比方法
- 嵌入型：TransE、RotatE、HAKE、QuatRE、CompilE。
- GNN 型：R-GCN、ConvE、InteractE、BiGAT、RHKH。
- PLM/LLM 型：KG-BERT、KG-R3、iHT、RAA-KGC、KICGPT。
- 共计约 15 种基线。

### 实验组数
- 主实验结果（Table 2）：在两个数据集上对比所有基线，报告 4 个指标。
- 解码器与消息函数消融（Table 3）：3 种消息函数 × 3 种解码器 = 9 种组合。
- 注意力机制消融（Table 4）：混合注意力 vs. 仅交叉注意力 vs. 仅 MLP 注意力，在 FB15k-237 的 4 种关系模式上评估。
- 组件消融（Table 5）：移除 LLM 增强、3D 卷积、MLP 注意力、交叉注意力、高斯增强、测试集重叠三元组后，共 6 项。
- 附加数据集实验：UMLS（Table 13）和 FB15K（Table 14）。
- 稀疏实体性能对比（Table 10）：增强前后对比。
- 生成三元组统计分析（Table 9、图 9-13）。

## 4. 资源与算力（文中说明）

| 项目 | 说明 |
|------|------|
| GPU | 单张 3060（对比基线中 KG-R3 使用 2×A6000，iHT 使用 V100/16） |
| 模型参数量 | 约 1930 万（不含高斯增强模块约 1510 万） |
| 训练时间 | ~37 小时（300 个 epoch 内） |
| 推理时间 | 10.8 秒（FB15k-237 测试集） |
| LLM 增强耗时 | FB15k-237 约 14 小时，WN18RR 约 13 小时 |
| 说明 | 文中明确给出了上述 GPU 型号、数量、训练时长和参数规模，对比了 PLM 类基线的计算开销。 |

## 5. 实验数量与充分性

- **数量**：共包含 6 个主要表格和多个图表，覆盖主对比、组件消融、注意力机制消融、解码器/消息函数消融、附加数据集、稀疏实体细粒度分析、生成质量分析。
- **充分性评价**：
    - 主对比覆盖了三类主流方法（嵌入/GNN/PLM），且包含 2024–2025 年新方法（CompilE、RAA-KGC、KICGPT），对比相对全面。
    - 消融实验设计良好，逐一验证了 LLM 增强、3D 卷积、混合注意力、高斯增强等关键组件的贡献。
    - 额外在 UMLS 和 FB15K 上测试，增强了泛化性论证。
    - 对生成三元组与测试集重叠情况做了敏感性分析，排除了“记忆测试集”的嫌疑。
- **可能的不足**：缺乏在更大规模 KG（如 YAGO、Wikidata）上的实验；未与所有最新的 LLM-for-KGC 方法（如 KoPA、GPT-KGC）详细比较；未跨不同 LLM 评估增强效果（仅使用 DeepSeek-V3）。

## 6. 主要结论与发现

1. **显式 LLM 数据增强有效性**：去除 LLM 增强后，性能下降最大（MRR 从 0.396 降至 0.364，降幅 8.1%），表明显式生成是 LAKRA 成功的基石。
2. **混合注意力优于单一机制**：混合注意力在复杂关系模式（1-1、1-N、N-N）上表现最佳，而交叉注意力在 N-1 上略优，说明动态融合适应性强。
3. **3D 卷积解码器优于 2D（ConvE）和 Transformer**：在 FB15k-237 和 WN18RR 上均获得更高 MRR 和 Hits@K，归因于其多级特征交互。
4. **循环互相关消息函数最优**：比简单减法和乘法效果更好。
5. **增强收益并非源自测试集泄露**：即使移除与测试集重叠的三元组，性能仍显著高于无增强的版本（MRR 0.375 vs. 0.364）。
6. **稀疏实体提升显著**：对底层 20% 稀疏实体，增强后 MRR 从 0.427 提升至 0.695，涨幅 63%。

## 7. 优点（方法或实验设计亮点）

- **范式创新**：从隐式学习转向显式数据增强，直接干预数据稀疏性的根源，灵活可重复。
- **LLM 增强设计精细**：利用类型约束候选集降低 LLM 幻觉风险，两阶段方式使生成更可控；后过滤和启发式规则进一步提高质量。
- **编码器查询感知**：混合注意力机制使邻域聚合与查询关系相关，打破传统 GNN 的无差别聚合。
- **解码器 3D 卷积**：通过多维特征栈同时建模四种交互，表达能力比 2D 更强。
- **实验客观性**：
    - 消融实验覆盖所有模块。
    - 额外验证了测试集重叠影响（w/o llm test），避免了数据泄露疑虑。
    - 补充了 UMLS 和 FB15K 实验，展示泛化性。
    - 显式报告了计算资源（单卡 3060）并与其他方法比较，显示较低开销。

## 8. 不足与局限

- **实验覆盖不足**：仅使用了 FB15k-237、WN18RR、UMLS、FB15K 四个数据集，未在更大规模或更稀疏的 KG（如 YAGO3-10、DBpedia）上验证。
- **LLM 增强通用性未充分研究**：仅使用了 DeepSeek-V3，未评测不同 LLM（如 GPT-4、Llama 系列）对结果的影响；也未探讨 LLM 规模与生成质量的关联。
- **幻觉风险未完全消除**：文中承认 LLM 仍会产生噪声三元组（图 13 举例），但未定量分析噪声比例及对性能的负面作用。
- **基线对比不完整**：缺少与近两年所有基于 LLM 的 KGC 方法（如 KoPA、GPT-KGC、LLaMA-KGC 等）的对比；在 UMLS 和 FB15K 上仅对比了少量基线。
- **超参数敏感性**：未讨论 \(\lambda\) 等超参数的敏感性及调参过程。
- **可重复性**：代码未发布、LLM prompt 详细内容在附录中给出，但实验环境的完整复现细节可能不足。

（完）
