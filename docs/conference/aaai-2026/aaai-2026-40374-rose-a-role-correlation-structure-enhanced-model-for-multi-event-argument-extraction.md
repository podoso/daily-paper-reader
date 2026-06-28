---
title: "RoSE: A Role Correlation Structure-Enhanced Model for Multi-Event Argument Extraction"
title_zh: RoSE：增强角色相关结构的多事件论元抽取模型
authors: "Geting Huang, Jilong Zhang, Kai Zhou, Zhang Yi, Xiuyuan Xu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40374/44335"
tags: ["query:ie"]
score: 10.0
evidence: 多事件论元抽取，建模角色关联
tldr: 针对多事件论元抽取中事件结构异质性和重叠带来的挑战，以及以往工作忽视角色间关联的问题，本文提出角色相关结构增强模型（RoSE）。RoSE通过联合上下文提示输入、以角色为中心的图引导编码器和角色特定信息融合，有效捕获事件内和事件间的角色关联，提升论元抽取精度。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有事件论元抽取方法未充分利用角色间关联，难以处理事件结构异质性和重叠。
method: 构建角色为中心的图引导编码器和角色特定信息融合模块，建模角色关联。
result: 在多个事件论元抽取基准上取得最优结果。
conclusion: 显式建模角色关联是应对多事件结构异质性的有效手段。
---

## Abstract
Event co-occurrences have been proven effective for event argument extraction (EAE) in previous studies; 
however, few have considered intra- and inter-event role correlations. Since role varies among different event types, event structure heterogeneity and overlap pose significant challenges to EAE. To address this issue, we propose a Role Correlation Structure-Enhanced model for Multi-Event Argument Extraction (RoSE), capable of capturing both heterogeneity and overlap of event structures through modeling role correlations. The proposed RoSE model employs a joint context-prompts input, role-centric graph-guided encoder (RoGE), and role-specific information fusion (RoIF). The RoGE is designed to enhance the intra- and inter-event role correlation between prompts and their corresponding event contexts. The RoIF module utilizes intra-event role information to improve multi-event arguments extraction.
Extensive experiments on four widely-used benchmarks (RAMS, WikiEvents, MLEE, and ACE05) demonstrate that our proposed approach achieves state-of-the-art performance, validating the effectiveness of incorporating both intra- and inter-event role correlations.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究任务**：多事件论元抽取（Multi-Event Argument Extraction, Multi-EAE），即从一段文本中同时提取多个事件的所有论元及其角色。
- **现有挑战**：
  - 事件结构**异质性**：不同事件类型拥有不同的角色集合，角色间关系复杂，导致事件结构各不相同。
  - 事件结构**重叠**：不同事件可能共享相同的实体作为论元（例如同一实体同时是“受害者和“攻击目标”），产生角色间的共指。
  - 以往工作（包括单事件和多事件方法）未显式建模**事件内角色共现**和**事件间角色共指**，限制了模型对结构异质性与重叠的捕获能力。
- **研究意义**：显式利用角色关联结构，提升多事件论元抽取的准确性和鲁棒性，是事件抽取领域的重要进展。

## 2. 方法论

### 核心思想
提出 **RoSE（Role Correlation Structure-Enhanced model）**，通过显式建模事件内和事件间的角色关联，增强预训练语言模型对多事件结构的理解与抽取能力。关键模块包括：
- 联合上下文-提示输入（Joint Context-Prompts Input）
- 以角色为中心的图引导编码器（Role-centric Graph-based Encoder, RoGE）
- 角色特定信息融合（Role-specific Information Fusion, RoIF）

### 关键技术细节

#### （1）联合上下文-提示输入
- 将上下文文本中的每个触发词插入标记 `<ti>...</ti>`，并拼接多个事件提示（每个提示包含事件类型描述 `Ei` 和角色列表 `Pi`），形如：  
  `...<t0>killed</t0>...<e0>Life.Die</e0> Agent Victim Instrument Place...`
- 利用预训练语言模型同时处理多个提示，实现并行抽取。

#### （2）角色中心图构建（Role-centric Graph Construction）
- **事件内共现图（Intra-event Co-occurrence）**：针对每个事件类型，统计训练集中角色对共现频率，构建局部邻接矩阵，捕获事件内部角色关系。
- **事件间共指图（Inter-event Co-reference）**：统计不同事件角色间共享相同论元的频率，构建全局邻接矩阵，捕获事件间结构重叠。
- **上下文自适应融合（Context-Adaptive Fusion）**：使用图注意力网络（GAT）从输入中学习软结构，并与上述先验图加权融合（权重γ可学习），得到最终图结构 \( G = (1-\gamma) \cdot \text{GAT}(S) + \gamma \cdot P \)。

#### （3）以角色为中心的图引导编码器（RoGE）
- 基于Transformer编码器，引入**双重自注意力**：
  - 语义自注意力（Semantic Self-attention）：标准点积注意力，捕获上下文语义。
  - 结构自注意力（Structural Self-attention）：利用图结构 \( G_{ij} \) 调整注意力权重，显式注入角色关联信息。
- 最终注意力分数为两者之和，应用于所有层。

#### （4）角色特定信息融合（RoIF）
- 针对每个事件-角色槽位，通过注意力机制聚合触发词与对应角色提示的上下文信息，得到增强向量 \( \tilde{h}_{s_{i,k}} \)。
- 使用门控融合（gated fusion）将角色表示与上下文增强向量结合，用于后续论元跨度选择。

#### （5）角色跨度选择器（Role Span Selector）
- 将融合后的角色表示通过两个线性层得到开始/结束跨度选择器，使用二分匹配损失（Bipartite Matching Loss）进行训练。

## 3. 实验设计

### 数据集
- **ACE05**：句子级，新闻领域。
- **RAMS**：文档级，新闻领域。
- **WikiEvents**：文档级，新闻领域。
- **MLEE**：文档级，生物医学领域（包含嵌套事件）。

### 评估指标
- **Arg-I（论元识别）**：预测论元跨度与任何黄金论元完全匹配。
- **Arg-C（论元分类）**：跨度 + 角色类型完全匹配。

### 对比方法
- **Single-EAE**：EEQA、BART-Gen、PAIE、TabEAE（单事件模式）、DEGAP、ERCL。
- **Multi-EAE**：PAIE-multi、TabEAE-multi、DEEIA。
- **大语言模型**：ChatGPT、ChatGLM2-6B、LLaMA2-7b-chat。

## 4. 资源与算力

论文明确说明：
- **GPU**：单块 NVIDIA GeForce RTX 4090 GPU。
- **框架**：PyTorch。
- **预训练模型**：RoBERTa-large（24层），使用前17层作为编码器，后7层作为解码器。
- 解码器交叉注意力模块随机初始化，学习率设为其他参数的1.5倍。
- 优化器：AdamW，配合线性学习率调度。
- **未提及**：具体训练时长、批次大小、迭代轮次。属常见省略，不影响可复现性。

## 5. 实验数量与充分性

### 实验配置
- **主实验**：在4个数据集上报告Arg-I和Arg-C F1分数（表1）。
- **消融实验**：依次移除RoGE、RG（角色-角色关系，含intra/inter）、CAF、RoIF，在4个数据集上报告Arg-C（表2），共8组变体，每组6个随机种子取平均。
- **角色关联分析**：按事件数量（E=1 vs E>1）拆分子集测试（表3），并进一步按事件数量分段（图3）。
- **RoIF可视化**：对特定样本展示注意力权重热图（图4）。
- **与LLM对比**：在RAMS和WikiEvents上对比（表5）。
- **错误分析**：在WikiEvents上分类错误类型（表4）。
- **案例研究**：展示多事件示例（图5）。

### 充分性与公平性
- **充分性**：覆盖4个领域、句子/文档级别、嵌套/非嵌套事件；消融全面；多角度分析（数量、错误、可视化、LLM对比）。实验设计丰富，结论可信。
- **公平性**：所有对比方法均使用相同预训练模型（RoBERTa-large/BART-large）；Multi-EAE基线采用相同输入格式（提示模板复用DEEIA）；统计6次随机种子平均值，降低随机波动影响。整体客观公平。

## 6. 主要结论与发现

- **RoSE在所有四个基准上均取得最优结果**：相比DEEIA（原SOTA），ACE05上Arg-C提升1.7，RAMS提升1.0，WikiEvents提升0.5，MLEE提升0.3（表1）。
- **显式建模角色关联有效**：消融实验显示移除RoGE或RoIF均导致显著性能下降（表2），证明结构异质性和重叠信息的关键作用。
- **事件间共指对多事件场景尤其重要**：当事件数>1时，移除inter-event co-reference导致更大性能下降（表3）。
- **RoIF帮助模型区分边界**：可视化显示RoIF使注意力更集中于正确的论元跨度，避免冗余实体干扰。
- **与LLM相比优势明显**：RoSE在RAMS和WikiEvents上远超ChatGPT、ChatGLM、LLaMA（表5），证明在监督场景下，专门设计的模型效率与精度更优。

## 7. 优点

- **方法创新性**：首次系统性地利用事件内共现和事件间共指两种角色关联，通过图引导编码融合到Transformer中，结构新颖且理论扎实。
- **实验完整**：覆盖多领域、多基准，消融详细，错误分析及案例可视化增强了说服力。
- **效率与精度兼顾**：相比单事件循环提取，并行提取多个事件显著提高推理效率，且性能领先。
- **可复现性**：代码已开源。
- **泛化性强**：在生物医学领域（MLEE）也取得SOTA，验证跨领域有效性。

## 8. 不足与局限

- **依赖先验统计图**：角色共现/共指图基于训练集统计构建，对于低频事件或新领域，先验可能不准确甚至无法构建，限制了零样本或少样本场景的适用性。
- **未探索动态图构建**：论文提及未来方向“自动构建图”，说明静态图是当前局限。
- **MLEE提升较小**：作者分析认为MLEE中角色共指关系较少，导致RoSE的优势不突出。这表明方法对重叠程度敏感，并非所有场景都适用。
- **未在更大规模或更多样化的语料上验证**：仅使用4个基准，且大多为新闻领域（MLEE除外）。对于社交媒体、对话等噪声大、事件密集的场景未评测。
- **计算开销**：虽然推理效率优于单事件方法，但引入了图注意力、双重自注意力等模块，相比基线可能增加训练复杂度。论文未报告训练/推理时间比较。

（完）
