---
title: Efficient Discriminative Joint Encoders for Large Scale Vision-Language Reranking
title_zh: 面向大规模视觉语言重排序的高效判别式联合编码器
authors: "Mitchell Keren Taraday, Shahaf Wagner, Chaim Baskin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=UXtTBAyqVB"
tags: ["query:multimodal"]
score: 6.0
evidence: 视觉语言联合编码器重排序
tldr: 该论文提出高效判别式联合编码器EDJE，用于大规模视觉语言重排序。通过离线预计算视觉令牌并利用轻量适配器压缩，显著降低在线推理成本。虽涉及多模态联合编码，但任务为检索重排序，而非实体关系抽取。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1367, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1405, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 619, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 572, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1436, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1440, \"height\": 1267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1438, \"height\": 1285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1098, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-uxttbayqvb/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1006, \"height\": 599, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1400, \"height\": 951, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1456, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 897, \"height\": 855, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 561, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 387, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1383, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1420, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1074, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1078, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1348, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-uxttbayqvb/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1249, \"height\": 245, \"label\": \"Table\"}]"
motivation: 现有视觉语言重排序依赖昂贵视觉特征提取，无法大规模部署。
method: 离线预计算视觉令牌，通过轻量注意力适配器压缩，在线仅运行紧凑联合编码器。
result: 在保持强检索性能的同时大幅提升推理效率，具体指标未详述。
conclusion: EDJE为多模态联合编码的实用化提供了可行方案，但未涉及实体关系抽取。
---

## Abstract
Multimodal retrieval still leans on embedding-based models like CLIP for fast
vector search over pre-computed image embeddings. Yet, unlike text retrieval
where joint-encoder rerankers are standard, comparable vision–language rerankers
are largely absent. We find that seminal joint encoders such as BLIP are severely
bottlenecked by an expensive visual feature-extraction stage, preventing practical deployment at scale.
Motivated by this bottleneck, we introduce EDJE , an
Efficient Discriminative Joint Encoder that precomputes vision tokens offline and
compresses them via a lightweight attention-based adapter, so online inference runs
only a compact joint encoder over a small set of visual tokens plus the text. EDJE
preserves strong retrieval performance while drastically reducing storage and online
compute, enabling high-throughput inference. Specifically, EDJE processes 50k
image–text pairs/second while requiring 49kB of disk storage per image, matching
prior art on Flickr (zero-shot) and COCO (fine-tuned) retrieval.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：当前多模态检索主要依赖基于嵌入的模型（如CLIP），通过向量相似性搜索实现高效检索，但这类“晚交互”方式限制了细粒度的跨模态交互。另一方面，已有联合编码器（如BLIP、BLIP-2）虽然能通过重排序显著提升检索性能，但其在线推理时视觉特征提取极为昂贵（ViT-B编码64张图像约需400ms，ViT-L需1400ms），占推理时间80%以上，导致无法在大规模检索场景中实际部署。该领域缺少像文本检索中cross-encoder那样高效的多模态重排序器。
- **整体含义**：本文旨在将联合编码器的优势引入大规模检索，提出一种在保持强检索性能的同时大幅降低在线计算和存储成本的方案，使重排序成为可行。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **视觉特征离线预计算**：将视觉编码器作为预处理阶段，图像令牌（tokens）离线计算并存放到磁盘，在线推理时仅运行一个紧凑的联合编码器（小型语言模型）联合处理视觉令牌和文本，避免重复提取视觉特征。
- **令牌压缩适配器**：为了降低存储开销，设计轻量级注意力适配器，将长序列视觉令牌压缩为一小组富含语义的令牌（如64个）。

### 关键技术细节
1. **架构**：采用视觉语言模型（VLM）的范式——将视觉令牌投影到语言模型嵌入空间，并与文本令牌拼接，由自注意力层处理跨模态交互。但用小型语言模型（如MiniLM）替代大语言模型，保证快速推理。
2. **离线阶段**：图像经ViT编码器提取特征后，通过压缩适配器投影为m个压缩令牌（m<<原始令牌数），以FP16存储（约49kB/图）。
3. **在线阶段**：小型语言模型接收压缩视觉令牌和文本令牌，输出重排序分数。
4. **令牌压缩适配器细节**：引入m个可学习查询令牌（queries），通过交叉注意力与视觉编码器输出的n个视觉令牌交互，经MLP和线性投影映射到语言模型嵌入空间。该策略可视为特征选择，适应不同分辨率和骨架。
5. **训练**：联合优化三个目标：
   - 图像-文本匹配（ITM）：二元分类，负例通过嵌入模型的批内硬负挖掘获得。
   - 掩码语言建模（MLM）：掩码50%的文本令牌，根据视觉和未掩码文本预测。
   - 文本嵌入恢复（ITC）：鼓励[CLS]令牌逼近文本编码器输出。
   - 对于压缩变体，还使用局部模型（无压缩）作为教师，进行logit级知识蒸馏。

## 3. 实验设计

- **数据集与场景**：
  - **预训练**：CC12M、CC3M、SBU、Visual Genome、COCO，共约14M图像-文本对（与BLIP小规模数据混合一致）。
  - **零样本评估**：Flickr30k（标准测试集1000张图像，每张5句描述）。
  - **微调评估**：MS-COCO（Karpathy划分）。
  - **全数据集检索**：按LightningDOT设定，检索池包含所有训练/验证图像和描述。
- **Benchmark**：对比ALBEF、BLIP、BLIP-2（基线和大型版本），以及多种嵌入模型（CLIP、DFN、MetaCLIP、SigLIP2）。报告Recall@1/5/10及效率指标。
- **对比方法**：
  - 零样本：与原始嵌入模型对比（CLIP等），以及与联合编码器（ALBEF、BLIP、BLIP-2）对比。
  - 微调：与BLIP系列对比。
  - 效率对比：存储、参数、推理时间。

## 4. 资源与算力

- 论文中未明确说明训练所用的具体GPU型号、数量、总训练时长（如GPU hours）。仅在推理效率实验中提到使用A6000 GPU测量推理时间。
- 预训练使用14M图像-文本对，微调仅COCO，训练细节中给出学习率、批次等，但未提训练周期或总计算量。

## 5. 实验数量与充分性

- **实验数量较多**：包括：
  - 主表（表1）：4种骨干×多种ViT变体，零样本Flickr结果。
  - 表2：与联合编码器对比（零样本+微调）。
  - 消融实验：令牌压缩数（32、64、128、256）与性能（图4）；重排序池大小影响（图5）；训练目标消融（ITM/MLM/ITC）；蒸馏影响（表5）；交叉模型负挖掘（附录E）；全数据集检索（附录F）；令牌压缩基线对比（附录G）；量化效果（附录H）；文本编码器选择（附录J）。
- **充分性**：实验覆盖了核心性能、效率、存储、稳健性，虽然缺少大规模模型训练资源可复现性细节，但实验设计全面，控制变量公平（固定MiniLM、冻结视觉编码器、相同训练数据）。
- **公平性**：与先前方法使用相同或更小训练数据，对比时考虑计算时间、存储等。

## 6. 主要结论与发现

- **EDJE作为重排序器能显著提升各种嵌入模型的检索性能**：例如CLIP ViT-L/14@336的文本→图像Recall@1从67.7%提升至81.9%（+14.2%），SigLIP2也获得提升（82.3%→87.8%）。
- **EDJE在零样本Flickr上匹配/超越BLIP等，但效率高得多**：局部变体ViT-L/16仅33M参数、推理时间4.14ms（BLIP ViT-L/16需101.61ms），存储442kB（压缩后49kB）。64令牌压缩变体在几乎不损失性能情况下进一步降低存储。
- **压缩令牌保留了丰富语义**：可解释性分析显示压缩令牌映射到有意义的概念（如“狗”、“洞穴”、“反光”），而全576令牌很多映射到无效特殊令牌。
- **训练目标均有效**：ITM+MLM+ITC最好；蒸馏对压缩变体有益。
- **对池大小和压缩个数稳健**：64令牌在速度-性能间达极佳平衡。

## 7. 优点

- **创新性方案**：将视觉特征离线化与联合编码相结合，直击现有方法瓶颈（视觉提取昂贵），提出轻量令牌压缩适配器，兼顾性能、存储和速度。
- **模块化与兼容性**：EDJE可作为即插即用重排序器，兼容多种视觉骨干（CLIP、SigLIP2等），语言模型也可替换（MiniLM已足够）。
- **全面实验评估**：覆盖多种骨干、多数据集、多任务（零样本/微调/全数据集检索），消融充分，包含效率、存储、量化分析。
- **可解释性分析**：分析压缩令牌的语义内容，揭示其保留关键信息而过滤冗余，提供了深入理解。
- **实际部署导向**：提供伪代码和磁盘I/O评估，考虑真实部署瓶颈。

## 8. 不足与局限

- **实验计算资源未公开**：未提供训练所需GPU型号、数量、总时长，不利于复现与评估可扩展性。
- **语言模型固定为MiniLM**：虽然是刻意选择的紧凑模型，但未充分探索更优的小型语言模型（仅附录J尝试BERT-Base无显著差异）。
- **训练数据规模较小**：仅14M对，且未使用更大量数据（如LAION-400M）验证扩展性；与BLIP-2（400M）对比时训练数据量差距大。
- **未涉及多语言或视频/音频模态**：论文提及这些作为局限性，未作实验。
- **负采样依赖嵌入模型**：交叉模型负挖掘实验显示若用弱模型（CLIP）给强模型（SigLIP2）采样负例会显著降低性能，需匹配或更强模型。
- **压缩令牌的可解释性分析限于定性**：需要更多定量指标（如下游任务中的利用率）。
- **存储I/O仅测试本地SSD**：网络存储场景未测试，不推荐网络部署。

（完）
