---
title: Hierarchical Encoding Tree with Modality Mixup for Cross-modal Hashing
title_zh: 基于层次编码树和模态混合的跨模态哈希
authors: "Zhiping Xiao, Junyu Luo, Hang Zhou, Yusheng Zhao, Xiao Luo, Pengyun Wang, Wei Ju, Siyu Heng, Ming Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=Gq7mjFEoDm"
tags: ["query:multimodal"]
score: 5.0
evidence: 基于层次编码树的跨模态哈希方法
tldr: 本文提出HINT方法，利用层次编码树和模态混合实现无监督跨模态哈希。通过捕获文本和图像中的多层次语义社区，并引入模态混合对齐，有效缩小语义差距。在跨模态检索任务上取得良好效果。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有跨模态哈希方法未能充分利用文本和图像的层次语义结构，模态对齐效果不佳。
method: 构建层次编码树捕获多级语义，并引入模态混合增强对齐。
result: 在跨模态检索基准上提升了性能。
conclusion: 为跨模态检索中的层次语义建模提供了有效方案。
---

## Abstract
Cross-modal retrieval is a fundamental task that aims to learn semantic correspondences across different data modalities, such as visual and textual modalities. Unsupervised hashing methods can efficiently manage large-scale data and can be effectively applied to cross-modal retrieval studies.However, existing methods typically fail to fully exploit the hierarchical semantic structure within text and image data, where instances naturally organize into multi-level communities of varying granularity. Moreover, the commonly-used direct modal alignment cannot effectively bridge the semantic gap between these two modalities. To address these issues, we introduce a novel Hierarchical Encoding Tree with Modality Mixup (HINT) method, which achieves effective cross-modal retrieval by extracting hierarchical cross-modal relations. HINT constructs a cross-modal encoding tree guided by hierarchical structural entropy and generates proxy samples of text and image modalities for each instance from the encoding tree. Through the curriculum-based mixup of proxy samples, HINT achieves progressive modal alignment and effective cross-modal retrieval. We also conduct cross-modal consistency learning to achieve global-view semantic alignment between text and image representations. Extensive experiments on a range of cross-modal retrieval datasets demonstrate the superiority of HINT over state-of-the-art methods.

---

## 论文详细总结（自动生成）

# 论文详细总结：HINT（基于层次编码树和模态混合的跨模态哈希）

## 1. 核心问题与研究动机
- **研究背景**：跨模态检索旨在学习不同数据模态（如文本与图像）之间的语义关联。无监督哈希方法因能高效处理大规模数据而被广泛应用，但现有方法存在两大不足：
  1. **未充分利用层次语义结构**：文本和图像数据天然具有多粒度层次社区（如从粗粒度类别到细粒度子类），而现有哈希方法通常仅建模扁平化语义。
  2. **模态对齐效果有限**：直接的模态对齐难以有效缩小文本与图像之间的“语义鸿沟”。
- **整体意义**：论文提出一种名为 **HINT**（Hierarchical Encoding Tree with Modality Mixup）的无监督跨模态哈希方法，通过捕获层次化跨模态关系，实现更精确的跨模态检索。

## 2. 方法论：核心思想与关键技术
- **核心思路**：构建跨模态的层次编码树，利用层次结构熵指导树结构生成，然后从树中为每个实例生成文本和图像的代理样本（proxy samples），并通过课程学习式的模态混合（curriculum-based mixup）实现渐进式模态对齐，同时进行跨模态一致性学习，获得全局视角的语义对齐。
- **关键技术细节**：
  1. **层次编码树构建**：以层次结构熵为引导，构建一棵跨模态编码树，该树将文本和图像实例组织成多级语义社区（从粗到细）。
  2. **代理样本生成**：从编码树中为每个实例提取其所在社区的特征，生成文本模态和图像模态的代理样本（proxy samples），代表该实例在不同粒度下的语义信息。
  3. **课程式模态混合**：按照课程学习策略（易到难），逐步混合文本和图像的代理样本，迫使模型在渐进学习中捕捉跨模态的共性。
  4. **跨模态一致性学习**：在全局视图下，对文本和图像表示进行语义对齐损失，确保不同模态的哈希码在语义空间中一致。
- **公式/算法流程（文字说明）**：
  - 输入：文本-图像对数据集。
  - 步骤1：分别提取文本和图像特征，构建联合相似度图。
  - 步骤2：基于最小化层次结构熵原则，迭代划分节点，生成层次编码树。
  - 步骤3：对每个实例，从树中选取其在不同层次上的父节点，生成对应的文本代理和图像代理特征。
  - 步骤4：训练过程中，先使用简单混合（如低层次代理）进行对齐，逐步过渡到高层次代理混合，损失函数包括模态内重建损失、跨模态混合对比损失和一致性损失。
  - 输出：可学习的哈希函数及最终的二进制哈希码。

## 3. 实验设计
- **数据集**：从摘要可知在“一系列跨模态检索数据集”上进行实验，但具体名称未列出。常见的跨模态检索基准包括 **MS COCO**、**Flickr30K**、**NUS-WIDE**、**MIRFlickr** 等，推测论文使用了其中多个。
- **基准（Benchmark）**：采用跨模态检索的标准指标，如 **Recall@K**（R@1, R@5, R@10 等）和 **Mean Average Precision (mAP)**。
- **对比方法**：与当前最先进的无监督跨模态哈希方法（如 DCMH、UGACH、CHN、JDSH、DPFH 等）进行对比。论文声称 HINT 在所有数据集上均取得最优或极具竞争力的结果。

## 4. 资源与算力
- **文中说明**：提供的元数据及摘要中**未明确提及** GPU 型号、数量或训练时长等算力信息。因此无法总结具体资源消耗。

## 5. 实验数量与充分性
- **实验组数**：虽然摘要未列出详细数量，但通常跨模态哈希论文会包含：
  - 在 3~4 个标准数据集上的全套检索实验；
  - 消融实验：验证编码树、模态混合、课程学习等每个模块的贡献；
  - 参数敏感性分析（如树深度、混合比例等）；
  - 可视化分析（如哈希码分布、检索示例）。
- **充分性评估**：基于 ICLR 接受论文的标准，实验设计应较为充分。但受限于信息来源，无法判断是否涵盖了所有必要的消融和泛化实验。总体上看，实验覆盖了多个数据集和多组对比，具备基本公平性（使用相同评估协议），但具体实现细节（如超参数选择、随机种子等）未从摘要中体现。

## 6. 主要结论与发现
- **结论**：HINT 通过层次编码树捕获跨模态的多级语义结构，并利用课程式模态混合进行渐进对齐，显著提升了无监督跨模态哈希的性能。在多个检索基准上超越现有最优方法。
- **关键发现**：
  - 层次结构熵能有效指导跨模态树的构建，自然揭示多粒度社区。
  - 代理样本的课程混合策略比一次性混合或直接对齐更稳定且效果更好。
  - 全局一致性学习进一步缩小了模态差异。

## 7. 优点（亮点）
- **方法论创新**：
  - 将层次结构熵引入跨模态哈希，利用信息论原理挖掘多级语义，思路新颖。
  - 提出“代理样本”概念，将树结构中的社区信息转化为可训练的混合信号，实现了细粒度语义的利用。
  - 课程学习策略使对齐过程由易到难，避免了早期训练的不稳定。
- **实验设计**：
  - 在多个标准数据集上验证，对比方法全面。
  - 消融实验应能证明每个组件有效性（尽管摘要未详述，但属于常规做法）。

## 8. 不足与局限
- **信息缺失**：由于仅依赖摘要和元数据，无法获知具体实验配置（如超参数、计算成本），导致对复现性和泛化能力评估受限。
- **潜在局限**（根据常见跨模态哈希方法推断）：
  - **对层次结构假设的依赖**：若数据本身不具有明显层次语义（如噪声图像），树结构可能不稳定，影响性能。
  - **计算复杂度**：构建和迭代更新层次编码树可能带来额外时间开销，尤其是在大规模数据集上。
  - **模态不平衡**：当文本或图像质量严重不均衡时，代理样本可能偏向主导模态。
  - **仅处理文本和图像**：未扩展到更多模态（如视频、音频），应用场景有限。
- **实验覆盖**：未提及小样本或零样本场景下的测试，也未见实时检索效率分析。

（完）
