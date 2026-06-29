---
title: "FuseMine: Robust Multi-Modal Compound-Protein Interaction Prediction via Differential Attention Feature Mining"
title_zh: FuseMine：基于差分注意力特征挖掘的鲁棒多模态化合物-蛋白质相互作用预测
authors: "Junlin Xu, Zhuang Zhang, Zhenghang Gong, Jincan Li, Pan Zeng, Zilong Zhang, Xiong Li, Shuting Jin, Haowen Chen, Yajie Meng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39944/43905"
tags: ["query:multimodal"]
score: 4.0
evidence: 多模态深度学习用于化合物-蛋白质相互作用预测
tldr: 针对现有方法存在隐偏差和跨域泛化差的问题，提出FuseMine多模态框架，采用双表示策略，结合卷积编码器和预训练大语言模型提取分子结构和序列语义，有效提升CPI预测的准确性和鲁棒性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39944/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1823, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39944/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 879, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39944/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 889, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39944/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 849, \"height\": 302, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39944/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1723, \"height\": 563, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39944/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 881, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39944/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 880, \"height\": 473, \"label\": \"Table\"}]"
motivation: 现有方法存在隐偏差和跨域泛化能力差的问题。
method: 提出多模态深度学习框架，联合分子结构卷积特征和大语言模型语义特征进行CPI预测。
result: 在多个基准上取得鲁棒的预测性能，优于现有方法。
conclusion: FuseMine为药物发现提供了可靠的多模态预测工具。
---

## Abstract
Accurate prediction of compound protein interactions (CPIs) is crucial for drug discovery. 
However, existing deep learning-based methods suffer from hidden biases and poor cross-domain generalization, leading to spurious correlations and inadequate representation of unseen compound-protein pairs. 
To address these limitations, we propose FuseMine, a multimodal deep learning framework that jointly leverages molecular structures and biological sequences for reliable CPI prediction.
Specifically, FuseMine adopts a dual-representation strategy for each molecule. It employs a convolutional encoder to capture structural features, combined with pretrained large language models for extracting semantic information from sequences. We propose a novel Multi-modal Feature Orchestration Aggregation (MFOA) module that enables deep and synergistic fusion between the structural features and the sequential semantics of molecules, effectively capturing the complementary patterns across modalities. Additionally, we design a Reduction Differential Feature Mining (RDFM) module to further enhance the representation of discriminative features, thereby improving the model’s generalization capability. Extensive experiments on multiple benchmark datasets demonstrate that our framework consistently outperforms state-of-the-art methods in both intra-domain and cross-domain scenarios. These results highlight the synergistic value of combining structural and sequential data for CPIs.

---

## 论文详细总结（自动生成）

# FuseMine: 基于差分注意力特征挖掘的鲁棒多模态化合物-蛋白质相互作用预测

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：化合物-蛋白质相互作用（CPI）预测是药物发现的关键步骤。现有深度学习方法存在两大缺陷：
  - **隐偏差**：模型容易学到统计伪影而非生物上有意义的模式，导致对未见过的化合物-蛋白对预测效果差。
  - **跨域泛化能力弱**：在训练分布与测试分布不同（如跨域场景）时性能急剧下降，限制了在实际药物筛选中的应用。
- **背景**：传统机器学习依赖手工特征，深度学习虽能自动提取特征，但受限于高质量标注数据稀缺。近期多模态融合（结合分子结构与序列语义）有潜力提升表现，但现有融合方式多为简单拼接，未能实现深度协同。
- **整体含义**：本文提出FuseMine框架，通过联合分子图结构特征、蛋白质序列局部模式以及预训练大语言模型（LLM）的全局语义信息，实现鲁棒的CPI预测，尤其强调跨域泛化能力的提升。

## 2. 方法论

### 核心思想
采用“双表示策略”：对每个分子（化合物和蛋白质）分别提取结构特征和序列语义特征，然后通过精心设计的模块进行深度融合与判别特征挖掘，最后用双向交叉注意力建模交互。

### 关键技术细节

- **双编码器（Dual Molecular Encoder）**：
  - 化合物：3层GNN处理分子图，得到结构特征 H_ct；ChemBERTa-MTR编码SMILES序列，得到序列特征 H_cs。
  - 蛋白质：3层CNN处理氨基酸序列，得到结构特征 H_pt；ESM-2编码蛋白质序列，得到序列特征 H_ps。

- **多模态特征编排聚合（MFOA）模块**：
  - 三阶段：① 初步融合（矩阵乘法 + 卷积）；② 编排分区（按3:4:1比例分割）；③ 协调聚合（用SiLU激活、卷积、元素积，加入结构特征作为引导项）。
  - 输出融合表示 Z_cst, Z_pst。

- ** Reduction Differential Feature Mining (RDFM) 模块**：
  - 对融合特征进行卷积降维（key/value），然后用差分注意力（Differential Attention）计算两个softmax的加权差，抑制冗余噪声，提取判别性特征。
  - 公式：Diff = [softmax(Q1K1^T/√d) - λ·softmax(Q2K2^T/√d)] V，其中λ可学习。

- **交互预测**：
  - 双向交叉注意力：化合物→蛋白质和蛋白质→化合物的多头注意力，通过平均池化得到全局注意力描述子，加残差更新特征，最后MLP输出二分类概率。
  - 损失函数：二元交叉熵。

### 算法流程（文字描述）
输入：化合物C（图+SMILES）和蛋白质P（序列+氨基酸序列）→ 双编码器提取4种特征 → MFOA融合得到Z_cst, Z_pst → RDFM精炼得到Z_c, Z_p → 双向交叉注意力得F_c, F_p → MLP输出预测。

## 3. 实验设计

### 数据集与场景
- **四个基准数据集**：Human, C.elegans（较小）；BindingDB, BioSNAP（较大）。
- **三种分裂协议**：
  1. **域内随机分裂**：8:1:1（小）或7:1:2（大）。
  2. **域内冷对分裂（Cold-Pair）**：70%化合物-蛋白对作为训练，剩余30%中30%验证、70%测试，保证测试集中化合物和蛋白在训练中均未出现。
  3. **跨域分裂**：先用ECFP4指纹聚类化合物、PSC描述子聚类蛋白，60%簇作为源域，40%作为目标域，分布不重叠。

### 对比方法（baselines）
10种：SVM、RF、GraphDTA、DeepConv-DTI、MolTrans、TransformerCPI、HyperattentionDTI、DrugBAN、MlanDTI、LAM-DTI。

### 评价指标
AUC-ROC、AUPR、F1-score（所有结果取5次独立运行平均）。

## 4. 资源与算力

- 文中说明：模型使用PyTorch Lightning实现，在 **NVIDIA A800 GPU** 上训练。
- **未明确**给出GPU数量、训练时长等具体信息。仅提及学习率5e-5，batch size 64，训练100 epochs。

## 5. 实验数量与充分性

- **实验组数**：涵盖三大协议下的4个数据集，共约12组主要实验（表1-3），另加消融实验（图3）和可视化（图4）。
- **充分性**：实验设计较全面，覆盖了随机、冷对、跨域三种难度递增的场景，且与多个SOTA对比。消融实验验证了每个模块的贡献。可视化展示了特征分离过程。
- **公平性**：采用与其他论文相同的数据划分和官方超参数，结果取5次平均。但小数据集（Human, C.elegans）上没有做冷对和跨域，可能因为数据量过小导致结果不可靠。
- **潜在风险**：随机分割可能存在数据泄漏（同一化合物或蛋白出现在训练和测试集），但作者已通过冷对和跨域实验弥补。

## 6. 主要结论与发现

- FuseMine在所有四个数据集上均达到或接近SOTA，尤其在 **冷对场景**（BindingDB AUC 0.745，BioSNAP AUC 0.798）和 **跨域场景**（BindingDB AUC 0.657，BioSNAP AUC 0.765）上提升显著，验证了多模态深度融合和差分特征挖掘的有效性。
- 消融实验表明，MFOA和RDFM模块缺一不可，移除任意一个均导致性能下降。
- 可视化显示，训练过程中正负样本嵌入逐渐分离，表明模型学会了判别性特征。

## 7. 优点

- **创新的模块设计**：MFOA实现了超越简单拼接的深度多模态融合，RDFM借鉴差分放大器思想，有效滤除噪声。
- **鲁棒泛化**：在跨域和冷对场景中表现突出，说明模型能学到基础交互机制而非统计伪影。
- **全面实验**：三种分裂协议、多数据集、多指标、消融、可视化，验证充分。
- **代码开源**：提供了GitHub仓库，可复现。

## 8. 不足与局限

- **小数据集提升有限**：在Human和C.elegans上改进细微（AUC从0.988到0.989），可能因数据量小限制了模型潜力。
- **F1分数不稳定**：在冷对BioSNAP上F1低于MlanDTI（0.611 vs 0.653），说明模型在正负样本不平衡下的分类决策边界仍有优化空间。
- **计算资源未详述**：未给出训练时间、参数规模等，难以评估实际部署成本。
- **仅二分类**：只能判断有无交互，不能预测结合强度（亲和力），适用范围受限。
- **偏差风险**：尽管跨域实验较严格，但基于聚类的域划分可能仍存在领域偏移，且数据集来源为已知相互作用，对全新靶点或化合物的真实外推能力仍需进一步验证。

（完）
