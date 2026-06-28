---
title: "URaG: Unified Retrieval and Generation in Multimodal LLMs for Efficient Long Document Understanding"
title_zh: "URaG: 多模态大语言模型中统一检索与生成以实现高效长文档理解"
authors: "Yongxin Shi, Jiapeng Wang, Zeyu Shan, Dezhi Peng, Zening Lin, Lianwen Jin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39729/43690"
tags: ["query:multimodal"]
score: 7.0
evidence: 多模态大语言模型用于长文档理解，检索与生成
tldr: 多模态大语言模型在处理长文档时面临信息干扰和二次计算成本问题。本文发现MLLM具有从粗到细的推理模式，早期层广泛关注文档，深层聚焦相关证据。基于此提出URaG框架，统一检索与生成过程，避免外部检索器增加复杂度。实验证明URaG在多个长文档理解任务上取得了高效且准确的结果。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多模态大语言模型在处理长文档时存在信息干扰和二次计算成本两大挑战。
method: 利用MLLM的粗到细推理模式，统一检索与生成过程实现端到端优化。
result: 在多个长文档理解基准上，URaG在准确率和效率上均优于现有方法。
conclusion: 统一检索与生成可有效提升多模态大语言模型长文档理解性能。
---

## Abstract
Recent multimodal large language models (MLLMs) still struggle with long document understanding due to two fundamental challenges: information interference from abundant irrelevant content, and the quadratic computational cost of Transformer-based architectures. Existing approaches primarily fall into two categories: token compression, which sacrifices fine-grained details; and introducing external retrievers, which increase system complexity and prevent end-to-end optimization. To address these issues, we conduct an in-depth analysis and observe that MLLMs exhibit a human-like coarse-to-fine reasoning pattern: early Transformer layers attend broadly across the document, while deeper layers focus on relevant evidence pages. Motivated by this insight, we posit that the inherent evidence localization capabilities of MLLMs can be explicitly leveraged to perform retrieval during the reasoning process, facilitating efficient long document understanding. To this end, we propose URaG, a simple-yet-effective framework that Unifies Retrieval and Generation within a single MLLM. URaG introduces a lightweight cross-modal retrieval module that converts the early Transformer layers into an efficient evidence selector, identifying and preserving the most relevant pages while discarding irrelevant content. This design enables the deeper layers to concentrate computational resources on pertinent information, improving both accuracy and efficiency. Extensive experiments demonstrate that URaG achieves state-of-the-art performance while reducing computational overhead by 44-56%.

---

## 论文详细总结（自动生成）

# URaG 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：多模态大语言模型（MLLM）在处理长文档时面临两大挑战：① 大量无关内容导致**信息干扰**（information interference）；② Transformer 架构的**二次计算复杂度**（quadratic computational cost），使长序列处理成本过高。
- **现有方法的局限性**：
  - **Token 压缩**（如 mPLUG-DocOwl2）：牺牲细粒度细节。
  - **引入外部检索器**（如 SV-RAG、CREAM）：增加系统复杂度，无法端到端优化，存在子优协调和错误传播。
- **关键洞察**：作者通过实证分析发现，MLLM 具有**类人粗到细推理模式**（coarse-to-fine reasoning pattern）：早期 Transformer 层均匀关注所有页面，深层逐渐聚焦到证据页面。这启发作者利用 MLLM 固有的证据定位能力，在推理过程中完成检索。

## 2. 论文提出的方法论

- **核心思想**：**统一检索与生成**（Unified Retrieval and Generation, URaG），在一个 MLLM 内部完成检索和生成，无需外部检索器。
- **框架结构**（见图3）：
  1. **基础 MLLM**：采用 Qwen2.5-VL（3B/7B）。
  2. **轻量跨模态检索模块**（Cross-modal Retrieval Module）：由两个线性层（含 GELU 激活）组成，参数极少（仅占模型参数的 0.05%~0.07%）。
- **技术细节**：
  - **特征提取**：取早期层（默认第6层）的隐藏状态 \( H \in \mathbb{R}^{L \times D} \)，通过特征映射层降维至 \( \mathbb{R}^{L \times D'} \)，再经 L2 归一化。
  - **相似度计算**：采用**上下文延迟交互**（contextualized late interaction）公式：
    \[
    s_{q,v}(p) = \sum_{i \in |E_q|} \max_{j \in |E_v^{(p)}|} \mathbf{E}_q^i \cdot (\mathbf{E}_v^{(p)})_j^{\mathsf{T}}
    \]
    计算查询文本与每页的相似度。
  - **页面选择**：保留 top-k 页（默认 k=5），丢弃其余页面的视觉 token。
  - **推理**：深层 Transformer 层仅处理保留页，生成答案。
- **训练策略**（两阶段）：
  - **阶段一：检索预训练**。冻结除检索模块外的所有参数，优化检索损失（ListNet 风格）：
    \[
    L_{\text{retrieval}} = \log(1 + \exp(S_{\text{neg}} - S_{\text{pos}}))
    \]
    其中 \( S_{\text{pos}} \) 为正样本分数和，\( S_{\text{neg}} \) 为负样本分数和（若负样本过多则取 top-P 个负样本）。
  - **阶段二：联合微调**。添加 LoRA 适配器（rank=32, alpha=64, dropout=0.1）到 LLM 和检索模块，联合优化检索损失和生成损失（交叉熵）：
    \[
    L_{\text{total}} = L_{\text{retrieval}} + L_{\text{generation}}
    \]
    训练时保证 ground-truth 证据页始终保留，其余由最高检索分数补充（最多保留5页）。

## 3. 实验设计

- **数据集**：
  - **检索评估**：MPDocVQA、DUDE、SlideVQA、MMLongBench-Doc。
  - **生成评估**：MPDocVQA、DUDE、SlideVQA、LongDocURL、MMLongBench-Doc。
- **基准对比方法**：
  - **文本检索**：BM25、SBERT、BGE-M3、BGE-large、NV-Embed-v2。
  - **视觉检索**：CLIP、SigLIP、ColPali、MM-Embed、SV-RAG。
  - **长文档理解方法**：LayoutLMv3、Hi-VT5、DocFormerv2、GRAM、Llama-3.2、LLaVA-Next-Interleave、Idefics3、mPLUG-DocOwl2、CREAM、Qwen2-VL、InternVL2.5/3、PDF-WuKong、Qwen2.5-VL（baseline）等。
- **评估指标**：
  - **检索**：Top1、Top5 准确率。
  - **生成**：ANLS（MPDocVQA、DUDE）、EM（SlideVQA）、Generalized Accuracy 和 F1（MMLongBench-Doc）、Generalized Accuracy（LongDocURL）。

## 4. 资源与算力

- **GPU 型号与数量**：4 块 NVIDIA A6000 GPU。
- **训练时长**：检索预训练和联合微调**各 1 个 epoch**（未给出具体小时数）。
- **模型规模**：URaG-3B 和 URaG-7B，均基于 Qwen2.5-VL。
- **检索模块参数量**：仅占总参数的 0.05%~0.07%，计算开销可忽略。

## 5. 实验数量与充分性

- **实验数量**：
  - **检索评估**：4 个数据集 × 2 指标，对比 11 种检索方法。
  - **生成评估**（表2）：4 个数据集，对比约 15 种方法。
  - **生成评估**（表3 MMLongBench-Doc）：按证据模态（TX/LAY/CHA/TAB/IMG）和证据数量（单页/多页/不可回答）细分，对比约 15 种方法。
  - **消融实验**：3 组（检索模块位置、两阶段训练策略、与 baseline 对比）。
  - **计算效率实验**（表7）：FLOPs 对比，3 种页数（20/60/100）。
- **充分性评价**：
  - **充分**：覆盖了主流长文档理解和检索基准，对比了多种类型的基线（纯文本、视觉、混合方法）。
  - **客观公平**：与 baseline（Qwen2.5-VL）使用相同训练数据、相同设置微调，且给出了无微调版本（URaG w/o finetune）的对比。
  - **消融覆盖关键设计**：验证了检索模块插入层、两阶段训练的必要性。

## 6. 论文的主要结论与发现

1. MLLM 在处理长文档时确实表现出**类人粗到细推理模式**：早期层注意力均匀，深层聚焦证据页。
2. URaG 在**检索**上全面超越所有纯文本和纯视觉检索器（见表1）。
3. 在**生成任务**上，URaG 在所有五个基准上均达到 **SOTA**（见表2、3），尤其在长文档（SlideVQA 平均20页，MMLongBench-Doc 平均47.5页）上提升显著。
4. **计算效率**：相比 baseline，FLOPs 减少 **44%~56%**（20页→100页）。
5. **无需外部检索器**，且仅需极少额外参数（0.05%），实现**端到端优化**。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次在 MLLM 内部统一检索与生成，利用模型自身的注意力模式进行证据定位，无需额外检索系统。
- **轻量化**：检索模块仅两个线性层，参数极少，几乎不增加模型规模。
- **高效性**：通过丢弃无关页面显著降低计算成本，同时提升准确率（减少信息干扰）。
- **实证分析充分**：通过注意力熵、检索准确率等指标验证了“粗到细”推理模式，为方法设计提供扎实依据。
- **公平对比**：严格控制训练数据、超参数，与 baseline 进行同设置微调对比，且报告了无微调版本，避免过拟合争议。
- **跨数据集验证**：覆盖 VQA、长文档定位、多跳推理等任务，证据类型涵盖文本、表格、图表、图片等。

## 8. 不足与局限

- **实验覆盖**：
  - 未在更多领域（如法律文档、医学报告）或非英语文档上进行测试，可能存在语言/领域偏差。
  - 计算效率实验仅基于 SlideVQA 并重复页面，未在真实长文档（如100页以上）上验证检索和生成的联合效果。
- **偏差风险**：
  - 训练数据仅来自 MPDocVQA、DUDE、SlideVQA，其分布可能偏向某些页面布局或问题类型，存在过拟合风险。
  - 消融实验显示，在 LongDocURL 上微调后性能下降，说明可能存在**域偏移**或过拟合。
- **应用限制**：
  - top-k 固定为5，对于需要大量跨页证据的问题（如 >5 页），可能丢失关键信息。
  - 依赖 MLLM 早期层表征质量，若基础模型较弱，检索模块可能失效。
  - 未讨论检索错误（当 top-5 未包含证据页）对最终答案的灾难性影响。

（完）
