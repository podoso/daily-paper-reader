---
title: "GSAP-ERE: Fine-Grained Scholarly Entity and Relation Extraction Focused on Machine Learning"
title_zh: GSAP-ERE：面向机器学习的细粒度学术实体与关系抽取
authors: "Wolfgang Otto, Lu Gan, Sharmila Upadhyaya, Saurav Karmakar, Stefan Dietze"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40537/44498"
tags: ["query:ie"]
score: 9.0
evidence: 从科学出版物中进行命名实体识别和关系抽取
tldr: 信息抽取有助于理解机器学习的可复现性，但缺乏细粒度数据集。本文构建了GSAP-ERE数据集，包含63K实体和35K关系，涵盖10种实体类型和18种关系类型，源自100篇ML论文全文。实验表明该数据集能够支持精细训练的信息抽取模型，推动科学文献IE研究。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 机器学习研究发展迅速，从科学文献中抽取细粒度信息对理解和复现研究至关重要。
method: 人工标注100篇ML论文全文，构建包含10种实体类型和18种关系类型的细粒度数据集。
result: 微调后的模型在实体识别和关系抽取任务上表现良好，验证了数据集的实用性。
conclusion: 该数据集为科学领域的信息抽取提供了高质量资源，促进了ML研究的可复现性。
---

## Abstract
Research in Machine Learning (ML) and AI evolves rapidly. Information Extraction (IE) from scientific publications enables to identify information about research concepts and resources on a large scale and therefore is a pathway to improve understanding and reproducibility of ML-related research. To training and testing of IE models focused on fine-grained information in ML-related research, e.g. method training and data usage, we introduce GSAP-ERE. It is a manually curated fine-grained dataset of mentions of 63K ML-related entities and 35K relations distributed across 10 entity types and 18 semantically categorized relation types annoated in the full text of 100 ML publications. We show that our dataset enables fine-tuned models to automatically extract ML-related information that facilitate knowledge graph (KG) construction from scholarly papers or monitoring of computational reproducibility of AI research at scale. Additionally, we use our dataset as a test suite to explore prompting strategies for
IE using Large Language Models (LLM). We observe that the performance of state-of-the-art LLM prompting methods is largely outperformed by our best fine-tuned baseline model (NER: 80.6%, RE: 54.0% for the fine-tuned model vs. NER: 44.4%, RE: 10.1% for the LLM). This disparity of performance between supervised models and unsupervised usage of LLMs suggests datasets like GSAP-ERE are needed to advance research in the domain of scholarly information extraction.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：机器学习（ML）和人工智能研究快速发展，但存在严重的可复现性问题——仅4%的ML相关论文可在原作者未回应澄清请求的情况下被复现。同时，确定特定任务的最新模型和数据集越来越困难。这些问题源于不良的基准测试实践和日益增多的研究文献。
- **解决思路**：从科学出版物中进行信息抽取（IE），特别是命名实体识别（NER）和关系抽取（RE），可以大规模识别研究概念和资源，从而提升对ML研究的理解和可复现性。
- **现有不足**：现有IE数据集多为粗粒度（如只有3-6种实体类型）、基于摘要或选定的段落，缺乏覆盖全文、细粒度的实体和关系标注，且未经监督微调的大语言模型（LLM）在细粒度领域IE任务上表现远不如微调模型。
- **本文贡献**：构建GSAP-ERE数据集——人工标注的100篇ML论文全文，含63K实体和35K关系，覆盖10种实体类型和18种关系类型。通过实验证明该数据集能支持高质量IE模型训练，并揭示LLM在领域特定IE任务上的局限性。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：扩展已有的GSAP-NER实体标注数据集，在其基础上添加关系标注，形成端到端的实体与关系抽取（ERE）数据集。明确形式化定义NER和RE子任务，采用跨文档的句子级标注。
- **形式化定义**：
  - NER：给定句子token序列，识别连续词序列（span）并赋予实体标签（共10类）。
  - RE：对每对实体预测关系标签（共18类，包含NIL表示无关系）。
  - ERE：联合完成NER和RE任务。
- **标注方案**：
  - 实体类型：ML模型相关（MLModel, ModelArchitecture, MLModelGeneric, Method, Task）、数据集相关（Dataset, DatasetGeneric, DataSource）、其他（ReferenceLink, URL）。
  - 关系类型：分为7个语义组——模型设计（usedFor, architecture, isBasedOn）、任务绑定（appliedTo, benchmarkFor）、数据使用（trainedOn, evaluatedOn）、数据溯源（transformedFrom, generatedBy, sourcedFrom）、数据属性（size, hasInstanceType）、同类关系（coreference, sameAs, isPartOf, isHyponymOf, isComparedTo）、引用（citation, url）。
- **标注流程**：两阶段——初始标注（2名计算机背景学生，10篇双标+90篇单标），精炼阶段（2名博士生+2名博士后检查对齐，抽取错配模式并修正全部100篇）。
- **人类一致性**：NER宏F1从0.61提升至0.82（精确匹配），关系标注按不同设置评估，加权平均RE+ F1=53.7%，RE≈ F1=62.8%。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：GSAP-ERE（80%训练，10%验证，10%测试）。比较数据集包括ScienceIE、SemEval2018 Task 7、SciERC、SciER。
- **对比方法**：
  - **监督方法**：
    - PL-Marker（流水线方法）：先NER后RE。
    - HGERE（联合方法）：扩展PL-Marker，使用超图神经网络同时处理NER和RE。
  - **无监督LLM方法**：
    - Qwen2.5（32B和72B）和LLaMA 3.1（70B），采用零样本和少样本提示，提示模板包含任务介绍、标签定义、分步指令、示例和输入。
    - 示例选择策略：随机 vs. 相似+多样化动态检索。
- **评价指标**：NER使用精确匹配（NER）和部分匹配（NER≈）；RE使用四种设置：RE+（实体类型和关系标签正确，精确span）、RE（关系标签正确，精确span，实体类型不限）、RE+≈（关系标签正确，部分span）、RE≈（仅关系标签正确，部分span）。报告微平均F1。

## 4. 资源与算力

- **硬件**：服务器运行Ubuntu 22.04.4 LTS，配备2× Intel Xeon 2.1GHz CPU（48核，96线程），1.4 TB RAM，8块GPU（4× RTX 2080 Ti 11GB + 4× A40 48GB）。
- **训练时间**：监督PLM训练单次运行2小时30分钟；推理测试集（10篇文档）监督方法约4分钟，LLM方法需12小时29分钟（慢182倍）。
- **量化模型**：LLM采用Ollama框架加载Qwen2.5和LLaMA3.1的量化版本进行推理。

## 5. 实验数量与充分性

- **总体实验组数**：
  - 监督方法：对HGERE进行了超参数优化（学习率、批量大小、损失权重、epoch数），最终用5个随机种子运行并报告均值±标准差。
  - LLM方法：在验证集上系统测试了不同k-shot（0,1,2,5,10,20）和示例选择策略（随机 vs. 相似+多样化），NER和RE分开优化。
- **充分性评价**：实验设计较充分——覆盖了两种主流监督范式（流水线与联合）、三种不同规模的LLM、多种提示策略和示例数量。但仅有一个数据集（GSAP-ERE自身），未在外部数据集上验证泛化能力；RE评估仅用1-shot LLM，可能不够全面。

## 6. 论文的主要结论与发现

- **监督方法显著优于LLM**：最佳监督联合模型HGERE在NER上F1=80.6%（±0.3%），RE+ F1=46.9%（±0.5%）；最佳LLM（Qwen2.5 72B）NER仅44.4%，RE+仅8.2%，差距达36-39个百分点。
- **联合方法优于流水线**：HGERE在所有设置下均优于PL-Marker（NER高8个百分点，RE高12个百分点以上）。
- **LLM表现普遍低下**：尤其是关系抽取，所有LLM的RE+ F1均低于11%，说明当前LLM在细粒度领域IE上远未成熟。
- **示例选择策略影响**：相似+多样化策略显著优于随机选择，10-shot为NER最优，1-shot为RE最优。
- **数据集价值**：高质量标注数据是监督模型取得良好性能的关键，推动ML研究可复现性。

## 7. 优点

- **细粒度与全面性**：10种实体类型和18种关系类型，覆盖ML研究核心概念及其交互，远超现有数据集（如SciERC仅6种实体、7种关系）。
- **全文标注**：基于全文而非摘要或段落，包含所有句子（含无实体/关系的负样本），更真实反映文献语言多样性。
- **高质量人工标注**：两阶段精炼流程，NER一致性0.82，关系一致性0.53-0.63，确保可靠性。
- **实用导向**：关系类型划分为7个语义组，明确对应模型设计、任务绑定、数据使用等真实研究场景，便于下游应用（知识图谱构建、复现性监测）。
- **实验评价全面**：采用多种严格/宽松的NER和RE指标，并测试LLM多种提示策略，结论客观。
- **开源开放**：代码、数据、标注指南全部公开。

## 8. 不足与局限

- **领域覆盖有限**：仅包含机器学习或应用ML论文，未扩展到其他科学领域（如生物医学、物理），限制了通用性。
- **句子级标注**：仅标注句子内关系，未处理跨句/文档级关系，无法捕获长距离依赖（如方法跨多段描述）。
- **无名实体（泛称）**：虽然保留了MLModelGeneric和DatasetGeneric，但核心指代（coreference）仅在句子内部分标注，未做完整的文档级共指消解。
- **LLM实验不完全公平**：LLM实验仅使用1-shot RE，可能未充分发挥LLM潜力（尽管已给出优化原因）；且仅测试了开源LLM，未涉及GPT-4等闭源模型。
- **基准方法较少**：监督基线仅两种（PL-Marker、HGERE），未与其他更近期的ERE方法（如基于生成的方法）对比。
- **数据规模**：100篇论文，相对于大规模预训练或领域覆盖而言仍较少，样本偏差可能存在。
- **人类一致性在部分关系类型仍较低**：如模型设计组RE+仅38.4%，表明标注难度大，可能影响模型性能的上限。

（完）
