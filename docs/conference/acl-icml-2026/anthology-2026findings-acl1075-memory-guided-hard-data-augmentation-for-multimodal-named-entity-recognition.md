---
title: Memory-Guided Hard Data Augmentation for Multimodal Named Entity Recognition
title_zh: 记忆引导的硬数据增强用于多模态命名实体识别
authors: "Xinyu Liu, Kai fu, Yinghan Shi, Quanyou Chu, Ming Du, Hongya Wang, Xiaojun Meng, Jiansheng Wei, Yanghua Xiao, Bo Xu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1075.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 多模态命名实体识别，结合记忆引导的数据增强
tldr: "多模态命名实体识别中现有数据增强方法忽视模型内部状态。本文通过定量分析发现超30%错误是模型特有的，提出记忆引导的硬数据增强框架：用K折交叉验证识别模型特定的困难样本，并构造针对性增强。实验表明该方法显著修复模型缺陷，提升NER鲁棒性。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 731, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1644, \"height\": 737, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 284, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 784, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1623, \"height\": 74, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1075/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1545, \"height\": 1150, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 639, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1303, \"height\": 1238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 744, \"height\": 187, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 144, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1075/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1261, \"height\": 505, \"label\": \"Table\"}]"
motivation: 现有数据增强方法忽略模型自身偏差，导致错误修复低效。
method: 采用K折交叉验证识别模型特有的困难样本，并构建记忆引导的硬数据增强策略。
result: 在多个MNER基准上显著降低模型特定错误，提升识别准确率。
conclusion: 模型感知的数据增强能有效修复架构特定偏差，提高多模态NER泛化性。
---

## Abstract
Multimodal Named Entity Recognition relies on visual context to resolve textual ambiguities. To mitigate data scarcity, Data Augmentation (DA) has become a standard practice; however, existing methods predominantly adopt a one-size-fits-all and random perturbation paradigm, ignoring the internal state of the target model. In this paper, we first conduct a quantitative analysis, revealing that a significant portion of errors (over 30%) are model-specific, stemming from the unique biases of different architectures. To address this, we propose Memory-Guided Hard Data Augmentation, a framework designed to systematically repair these specific defects. First, we employ K-fold cross-validation to identify model-specific Hard Data. Second, we construct a Memory Tree and utilize Large Language Models (LLMs) with a clustering mechanism to induce macro-level error patterns from micro-level failures. This facilitates a paradigm shift from stateless instance-driven augmentation to a logical pattern-driven approach. Finally, we introduce an iterative augmentation mechanism that triggers recursive generation for stubborn instances that fail initial quality filters. Extensive experiments on Twitter-2015 and Twitter-2017 benchmarks demonstrate that our framework consistently yields significant performance gains across various MNER backbones.

---

## 论文详细总结（自动生成）

# Memory-Guided Hard Data Augmentation for Multimodal Named Entity Recognition 论文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有数据增强（DA）方法在 Multimodal NER 中采用“一刀切”的随机扰动范式，忽略目标模型的内部状态，导致大量模型特有的错误（超过30%）未被修复。
- **动机**：不同架构（如 HVPNeT、MKGformer、AMNet）具有独特的盲区（图1维恩图显示各模型特有困难样本占30%以上，共同错误交集很小），因此需要模型感知的、针对性的增强策略。

## 2. 方法论
### 核心思想
- 从“无状态实例驱动增强”转向“逻辑模式驱动的修复”：识别模型特有困难样本，抽象出宏观错误模式，并基于模式生成定制化增强数据。

### 关键技术细节
1. **Model-Aware Hard Data Mining**（阶段1）  
   - 使用K折交叉验证（K=10）划分训练集，训练临时模型并预测，将预测与标签不一致的样本定义为困难集 \( D_{\text{hard}} \)（公式1）。
2. **Memory Tree Construction**（阶段2）  
   - 先进行粗粒度分类（实体幻觉、边界检测失败、遗漏、类型混淆），再通过LLM进行根因分析，并利用层次聚类（局部归纳+全局合并）构建四层记忆树（根→粗粒度→细粒度模式→实例）。
3. **Data Generation**（阶段3）  
   - 基于记忆树中的错误模式，为每个模式生成通用增强策略，再对簇内实例应用策略生成原始增强样本（文本+图像）。
4. **Data Filtering**（阶段4）  
   - 三级过滤：标签验证（BIO合规性）、文本逻辑一致性（微调LLM判断标签是否被文本支持）、文本-图像语义一致性（图像描述与原始描述余弦相似度≥0.5）。
5. **Iterative Augmentation**（阶段5）  
   - 对过滤后仍无保留候选的“顽固”实例，递归调用对应模式的生成策略，直至获得合格样本。

### 关键算法流程
- 算法1：LLM驱动的全局模式合并——逐模式与已有模式比较语义，合并相同模式，否则新增。

## 3. 实验设计
- **数据集**：Twitter-2015 和 Twitter-2017（社交媒体图像-文本对，含PER/LOC/ORG/MISC四类实体，BIO标注）。
- **基准模型（Backbone）**：HVPNeT、AMNet、MKGformer。
- **对比方法**：
  - Vanilla LLM Augmentation（随机选择样本，LLM+SD生成）
  - GMDA（两阶段生成，LLM+SD）
  - AMIA（自适应混合图像增强）
- **评估指标**：Precision、Recall、F1。

## 4. 资源与算力
- **本地计算**：单张 NVIDIA H100 GPU，用于微调过滤模型（Meta-Llama-3-8B-Instruct）和图像合成（Stable-Diffusion-3.5-Large 推理）。
- **API调用**：超大模型 Qwen3-235B-A22B、Qwen2.5-VL-72B-Instruct、Qwen3-30B-A3B 通过API访问。
- **时间成本**（表1）：总离线耗时约6小时，其中图像合成占5小时，其余步骤（挖掘15min+记忆树20min+过滤30min）开销较小。

## 5. 实验数量与充分性
- **主实验**（表2）：3个backbone × 2个数据集 × 4种对比方法，共12组对比，结果一致显示本方法提升F1。
- **消融实验**（表5）：5个变体（去除模型感知挖掘、记忆树、迭代增强、过滤），验证各组件贡献。
- **模型规模对比**（表3）：Qwen3-30B vs 235B，30B仅差0.11% F1，说明框架对LLM规模不敏感。
- **过滤模型验证**（表4）：微调后的Llama-3-8B在验证集上F1=83.35%，证明过滤有效性。
- **案例研究**：展示了错误抽象（图5）和逻辑驱动修复（图4）的具体过程。
- **充分性评价**：实验设计全面，覆盖多个架构、数据集、消融和案例分析，对比基线包括最先进的生成式和混合式方法，固定划分、标准标注，结果客观。

## 6. 主要结论与发现
- 框架在 HVPNeT 上提升 F1 达 0.92%（Twitter-2015）和 1.54%（Twitter-2017），优于所有对比方法。
- 模型感知的困难样本挖掘比随机采样更关键（去除后F1下降至86.52%，接近Vanilla方法）。
- 记忆树和迭代增强机制显著提升稳健性（去除后F1分别下降0.30%和0.71%）。
- 数据过滤至关重要（去除后精度从87.58%降至83.49%）。
- 即使使用较小的30B模型也能达到接近235B的效果，实现性能与效率的平衡。

## 7. 优点
- **方法论创新**：从模型感知角度设计增强，突破“一刀切”范式，首次系统利用LLM归纳错误模式。
- **可解释性强**：记忆树结构层次清晰，错误模式可追溯，增强策略可理解。
- **模块化设计**：五个阶段独立可替换，便于扩展和适配不同模型。
- **鲁棒性强**：迭代增强解决顽固样本，过滤机制保证数据质量，增强效果稳定。
- **效率良好**：离线自动诊断修复，不影响训练/推理时延；小LLM即可有效工作。

## 8. 不足与局限
- **领域覆盖有限**：仅验证社交媒体数据集（Twitter），图像-文本关系松散耦合；在严格对齐领域（如医疗影像报告、产品说明书）的效果未知。
- **生成式模型依赖**：框架性能受LLM/Diffusion Models的幻觉和噪声影响，虽然过滤缓解，但细微语义不一致（如隐喻误解、视觉伪影）仍可能传播。
- **资源需求仍高**：尽管通过API降低本地负担，但大规模LLM调用和扩散模型合成仍需要可观计算资源，对普通研究者不够友好。
- **理论分析较浅**：未深入探讨模式归纳的理论保证，聚类合并依赖LLM判决的稳定性。
- **未对比最新SOTA**：论文明确声明不追求绝对SOTA，但缺少与更近期的MNER专用增强方法（如有）的对比。

（完）
