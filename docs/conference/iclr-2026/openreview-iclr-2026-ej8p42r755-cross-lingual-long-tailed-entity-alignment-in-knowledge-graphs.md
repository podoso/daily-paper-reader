---
title: Cross Lingual Long-tailed Entity Alignment in Knowledge Graphs
title_zh: 知识图谱中的跨语言长尾实体对齐
authors: "Russa Biswas, Trung Duc Anh Dang, Gerard de Melo, Johannes Bjerva"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=eJ8p42r755"
tags: ["query:ie"]
score: 4.0
evidence: 知识图谱中的实体对齐，使用对比学习
tldr: 知识图谱实体对齐模型在长尾实体上表现不佳。ContrastEA利用预训练语言模型和难负样本挖掘，结合对比学习，提升长尾实体对齐性能，并提供了新的跨语言长尾数据集。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-ej8p42r755/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1430, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ej8p42r755/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1439, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ej8p42r755/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1390, \"height\": 822, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ej8p42r755/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1393, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ej8p42r755/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1382, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-ej8p42r755/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1579, \"height\": 2135, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1134, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1582, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 947, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1306, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1239, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1424, \"height\": 939, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 905, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1482, \"height\": 1156, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 449, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1412, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 959, \"height\": 783, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1589, \"height\": 956, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-ej8p42r755/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1228, \"height\": 302, \"label\": \"Table\"}]"
motivation: 现有实体对齐模型在稀疏连接的长尾实体上性能不佳。
method: 提出ContrastEA，使用预训练语言模型表示实体，结合top-k难负样本与NT-Xent损失。
result: 在长尾实体上显著提升对齐性能，并构建了多语言长尾数据集。
conclusion: 对比学习结合难负样本能有效解决长尾实体对齐问题。
---

## Abstract
Entity alignment (EA) models rely mostly on triples and structural information of Knowledge Graphs (KGs), but underperform on sparsely connected long-tailed entities. We address this gap by proposing a model, \textbf{ContrastEA}, that leverages pre-trained Language Models (LM), e.g. me5, to generate entity representations, followed by a novel contrastive learning approach that incorporates hard-negative mining strategies with \textit{top-k} negatives per entity, alongside NT-Xent loss to separate challenging entity pairs. In addition, to address the under-representation of long-tailed entities in benchmark datasets, we curate a new dataset from DBpedia comprising long-tailed entities per language -- Arabic, German, Portuguese, Italian, Hindi, Russian, and Japanese, each aligned to English (a total of 154,296 cross-lingual entity pairs). Our results demonstrate that ContrastEA outperforms the classic EA models on three benchmark datasets, improving Hits@1 by 6--20 percentage points, and achieves SOTA on the curated dataset over the long-tailed EA models.

---

## 论文详细总结（自动生成）

好的，以下是对论文《Cross-Lingual Long-Tailed Entity Alignment in Knowledge Graphs》的详细中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）

*   **核心问题**：现有知识图谱（KG）实体对齐（EA）方法在稀疏连接、信息匮乏的“长尾实体”上表现不佳。
*   **研究动机**：
    *   **长尾问题普遍存在**：现实世界的知识图谱（如DBpedia）中，超过50%的实体属于长尾实体（连接数≤3），但主流EA基准数据集（如DBP15K）对这类实体的代表性不足，导致模型无法反映真实场景的性能。
    *   **现有方法依赖结构信息**：多数EA模型（基于图神经网络）严重依赖实体间的结构、关系和邻域信息。长尾实体恰恰缺乏这些信息，因此基于结构的模型难以有效对齐它们。
    *   **数据集的局限性**：现有跨语言EA数据集语言覆盖少（主要为中、法、英等），且未包含完全孤立的实体（悬垂实体），无法全面衡量模型在稀疏图上的表现。
*   **整体含义**：论文旨在解决知识图谱中长尾实体对齐这一关键挑战，通过利用预训练语言模型和对比学习范式，提出一种不依赖结构信息的、鲁棒性更强的跨语言实体对齐方法。

### 2. 论文提出的方法论：核心思想、关键技术细节

*   **核心思想**：利用预训练语言模型（PLM）编码实体名称（这是所有实体都具备的、最稳定的特征），结合对比学习框架，将源KG和目标KG的实体对齐到统一的向量空间中。其关键在于通过“硬负样本挖掘”策略，模型能够更好地区分那些名字或语义非常相似的“欺骗性”实体对。

*   **关键技术细节**：
    1.  **实体表示**：
        *   使用多语言预训练语言模型 **mE5-base** 将实体名称编码为向量。
        *   采用**掩码平均池化**得到实体`e`的最终嵌入向量`e_i`。
        *   公式：`e_i = (Σ_j M_{i,j} H_{i,j}) / (Σ_j M_{i,j})`
        *   其中`H`是模型输出的隐藏状态，`M`是掩码矩阵。

    2.  **对比学习框架（ContrastEA）**：
        *   核心是三种对比损失函数的变体，训练目标是将源实体（查询，`f_θ(s_i)`）与对应的目标实体（正样本，`f_θ(t_i)`）拉近，与不相关实体（负样本）推远。
        *   **变体1：Top-k硬负样本对比损失**：
            *   **硬负样本选择**：计算一个批次内所有源实体与目标实体之间的相似度矩阵`A`。对于每个源实体`i`，从`A`中选择与其相似度最高的`k`个错误目标实体（排除正样本`j=i`）作为“硬负样本”。
            *   **损失函数**：仅在正样本和选出的 `k` 个硬负样本之间计算交叉熵损失。
            *   公式：`ℓ^{TopK}_{i,j} = -log( exp(sim(zs_i, zt_i)/τ) / (exp(sim(zs_i, zt_i)/τ) + Σ_{j∈Ni} exp(sim(zs_i, zt_j)/τ) )`
        *   **变体2：聚合Top-k硬负样本对比损失**：
            *   在选出`k`个硬负样本后，计算它们的平均相似度，得到一个聚合的负分数。
            *   这种方式将多个负样本的信息合并，可能会提供更稳定的梯度。
        *   **变体3：带批次内负样本的 NT-Xent 损失**：
            *   将批次内所有其他目标实体都作为负样本（In-batch negatives）。
            *   使用标准的 NT-Xent 损失函数，最大化正样本对的相似度，同时最小化所有负样本对的相似度。
        *   **为什么硬负样本重要？**：
            *   论文通过梯度分析指出，对于 NT-Xent 损失，相似度越大的负样本（硬负样本）对梯度的贡献也越大。然而，大量“简单负样本”的总和可能会淹没少数硬负样本的作用。
            *   **Top-k 损失通过限制分母仅为硬负样本，将梯度集中到这些最有信息量的样本上，显著提高了训练效率和效果。**

### 3. 实验设计：数据集、基准测试与对比方法

*   **数据集**：
    1.  **基准数据集**：
        *   **DBP15K**（ZH-EN, JA-EN, FR-EN）：广泛使用的EA基准。
        *   **SRPRS**（EN-DE, EN-FR）：更侧重于包含更多长尾实体的基准。
        *   **DBP5L**（EL, EN, ES, FR, JA 五语言组合）：多语言EA基准。
    2.  **新构建的数据集 LT-EA-25K**：
        *   **目的**：填补现有基准对长尾和悬垂实体代表性不足的空白。
        *   **来源**：来自DBpedia的7种语言（阿拉伯语、德语、葡萄牙语、意大利语、北印度语、俄语、日语）与英语的对齐，共154,296对跨语言实体对。
        *   **特点**：通过分层抽样确保实体度分布与真实KG一致，包含大量度≤3的实体，甚至包括约1400个阿拉伯语中的孤立（度=0）实体，真实反映了现实世界的稀疏性。

*   **对比方法**：范围广泛，包括基于翻译嵌入的（**MTransE, IPTransE**）、基于图神经网络的（**GCN-Align, RDGCN, HGCN, AliNet**）、基于属性和文本的（**JAPE, BERT-INT**）以及专门针对长尾的（**DAT**）等数十种经典和最新模型。

*   **评价指标**：Hits@1（精确匹配）和 Hits@10（前10命中率），严格遵循EA领域惯例。

### 4. 资源与算力

*   **文中说明**：论文明确提到实验在**一块NVIDIA Tesla A100 GPU（80GB内存）** 上完成。但未明确说明训练轮次的执行时间和总GPU小时数。
*   **总结**：算力资源较为充沛（A100是高性能GPU），但与文章结论相关性不大。模型本身是轻量化、基于预训练的编码器，无需从头训练PLM。

### 5. 实验数量与充分性

*   **实验数量**：论文进行了大量的实验，覆盖了：
    *   **3个现有基准数据集**（DBP15K、SRPRS、DBP5L）上的全面对比（表3、4、5）。
    *   **1个自建数据集**（LT-EA-25K）上的对比和深入分析（表6、图2）。
    *   **多种特征组合**的对比实验（仅名称、仅描述、名称+描述）。
    *   **消融实验**：分析了不同对比损失函数的影响、不同Top-k值对性能的影响、不同批次大小的敏感性。
    *   **按实体度分布的详细性能分析**（图2，表7）。
    *   与Zero-shot LLM（DeepSeek-R1-70bn）的对比（表11）。
    *   **超参数敏感性分析**：对学习率、批次大小、温度、Top-k值等进行了网格搜索。
*   **充分性与公平性**：
    *   实验设计**非常充分**，从多个维度证明了方法的有效性。
    *   **对比方法选择全面且具有代表性**，包括经典模型和最新的SOTA方法（如DAT）。
    *   自建数据集有助于弥补现有基准的不足，验证了模型在稀疏场景下的鲁棒性，设计很合理。
    *   **潜在不足**：对比方法多数是依赖结构信息的，也许可以包括一些纯粹的基于文本匹配的模型来作为更直接的基线。

### 6. 论文的主要结论与发现

1.  **SOTA性能**：提出的 **ContrastEA** 在三个现有基准数据集（DBP15K, SRPRS, DBP5L）和自建数据集 **LT-EA-25K** 上均取得了最先进的性能。
2.  **显著提升**：在 **SRPRS**（长尾更严重的基准）上，**Hits@1 提升高达20个百分点**（EN-FR）；在 DBP15K 上，对 FR-EN 提升显著。这证明其**长尾对齐能力极强**。
3.  **强鲁棒性**：
    *   不仅对长尾实体（度1-3）有效，对**孤立悬垂实体（度=0）** 也表现出良好性能（阿拉伯语 Hits@1=81.42%）。
    *   在**低资源语言**（如印地语 HI-EN）和**复杂语系**（如日语 JA-EN）上也表现强劲。
4.  **结构信息非必须**：实验证明，仅依赖实体名称信息，不依赖任何结构或邻域信息，即可达到甚至超越依赖结构信息的模型，这颠覆了传统EA领域的认知。
5.  **硬负样本挖掘有效**：Top-k硬负采样策略是提升模型区分能力的关键，显着优于简单的批次内负样本或聚合负样本方法。

### 7. 优点：方法或实验设计上的亮点

*   **方法创新**：首次将**硬负样本挖掘**策略与**对比学习**、**预训练语言模型**相结合，专门用于解决跨语言长尾实体对齐问题。这种组合设计非常巧妙且有效。
*   **数据贡献**：构建的 **LT-EA-25K 数据集** 是多语言、长尾EA领域的宝贵资源，填补了现有基准在稀疏性和语言多样性上的空白，对推动该领域研究具有重要价值。
*   **实验设计严谨**：进行了极为详尽的实验，从多个维度（数据集、特征、损失函数、度分布、超参数、LLM对比）进行了验证，结论（主要基于SOTA结果）可靠性强。
*   **实践价值高**：模型仅需实体名称，无需昂贵的图计算或规则，因此**易于实现和部署**，对低资源KG的融合非常有好处。
*   **深入分析**：对“为什么硬负样本重要”给出了直观的数学解释（梯度分析），并系统分析了不同特征（名称vs描述）在不同语言下的效果，以及长尾实体对齐性能与实体度的关系，具有深刻的洞察力。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

*   **依赖PLM**：最终性能高度依赖于所使用的预训练语言模型（mE5-base）的质量和覆盖范围。对于极度低资源、PLM训练数据中很少出现或完全没有的语言，性能可能会下降。
*   **仅限名称特征**：虽然名称是直接可用的特征，但在某些情况下，名称本身可能不具区分性或存在歧义（例如，简单的等价名称对必须很接近，但误解名称造成的错误匹配也会难以纠正）。
*   **数据集局限于DBpedia**：新数据集和部分基准数据（DBP15K、SRPRS、DBP5L）均来源于DBpedia。虽然具有一定的代表性，但**缺乏跨不同知识库**（如YAGO、Wikidata）或不同类型图谱（如来自文本构建的异构KG）的验证，可能存在**偏差风险**。论文在附录中也承认了这一点，并提到未在跨KG基准上测试。
*   **对比样本**：论文生成的负样本（硬负样本）原本只是基于相似度的最近邻。在某些场景下，可能存在更隐蔽的负样本（如同义词、近义词），该方法可能无法捕捉。
*   **系统偏差**：对比学习通过最大化正负样本差异来学习，如果训练数据中的名称本身就包含某种系统性偏差（如某些文化或领域名称更多更相似），模型可能会放大这些偏差。
*   **未提及跨KG场景验证**：论文提到未在DBP-YAGO等跨KG基准上测试，这限制了方法在更通用KG集成任务中的适用性。

（完）
