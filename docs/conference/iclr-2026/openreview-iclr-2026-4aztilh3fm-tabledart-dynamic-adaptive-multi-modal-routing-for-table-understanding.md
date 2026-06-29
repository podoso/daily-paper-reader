---
title: "TableDART: Dynamic Adaptive Multi-Modal Routing for Table Understanding"
title_zh: TableDART：面向表格理解的动态自适应多模态路由
authors: "Xiaobo Xing, Wei Yuan, Tong Chen, Quoc Viet Hung Nguyen, Xiangliang Zhang, Hongzhi Yin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4aZTiLH3fm"
tags: ["query:multimodal"]
score: 4.0
evidence: 动态自适应多模态路由
tldr: 该论文提出TableDART，一个训练高效的表格理解框架，通过复用预训练单模态模型并动态路由文本和图像模态，避免冗余和冲突。虽涉及多模态，但专注于表格，与实体关系抽取不直接相关。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1410, \"height\": 726, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1302, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1299, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1410, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1256, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1438, \"height\": 768, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1445, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1452, \"height\": 849, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1154, \"height\": 859, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1432, \"height\": 856, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-4aztilh3fm/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1408, \"height\": 1045, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1459, \"height\": 931, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1152, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 971, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1439, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1027, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 969, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1329, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 947, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 964, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 603, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-4aztilh3fm/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 643, \"height\": 302, \"label\": \"Table\"}]"
motivation: 现有表格多模态方法静态处理两种模态，导致冗余冲突且需昂贵微调。
method: 复用预训练单模态模型，根据查询-表格对动态选择最优模态路径，避免全部处理。
result: 在表格理解任务上效率提升，但未报告实体关系抽取的结果。
conclusion: 动态路由策略可推广至其他多模态任务，但非关系抽取。
---

## Abstract
Modeling semantic and structural information from tabular data remains a core challenge for effective table understanding. Existing Table-as-Text approaches flatten tables for large language models (LLMs), but lose crucial structural cues, while Table-as-Image methods preserve structure yet struggle with precise semantics. Recent Table-as-Multimodality strategies attempt to combine textual and visual views, but they (1) statically process both modalities for every query-table pair within large multimodal LLMs (MLLMs), inevitably introducing redundancy and even conflicts, and (2) depend on costly fine-tuning of MLLMs.  In light of this, we propose TableDART, a training-efficient framework that integrates multimodal views by reusing pretrained single-modality models. TableDART introduces a lightweight 2.59M-parameter MLP gating network that dynamically selects the optimal path (Text-only, Image-only, or Fusion) for each table–query pair, reducing redundancy and avoiding conflicts that arise when textual and visual views of the same table provide inconsistent cues. By routing to the most appropriate view, our framework improves both accuracy and efficiency. In addition, we propose a novel agent to mediate cross-modal knowledge integration by analyzing outputs from text- and image-based models, either selecting the best result or synthesizing a new answer through reasoning. This design avoids the prohibitive costs of full MLLM fine-tuning. Extensive experiments on seven benchmarks show that TableDART establishes new state-of-the-art performance among open-source models, surpassing the strongest baseline by an average of 4.02%. The code is available at: https://github.com/xiaobo-xing/TableDART.

---

## 论文详细总结（自动生成）

```markdown
# 论文结构化中文总结

## 1. 核心问题与研究动机
- **核心挑战**：表格数据理解需要同时建模语义与结构信息。现有方法分为三类：
  - **Table-as-Text**：将表格线性化为文本序列，丢失结构线索。
  - **Table-as-Image**：用视觉模型处理表格截图，保留结构但难以捕捉精确语义。
  - **Table-as-Multimodality**（MLLM-based）：静态地对每个query-table对同时使用文本和图像模态，导致冗余甚至冲突，且需要昂贵的MLLM微调。
- **目标**：提出一种训练高效、动态自适应路由的框架，避免冗余和冲突，同时复用冻结的预训练单模态模型。

## 2. 方法论
- **核心思想**：通过轻量级门控网络（仅2.59M参数）为每个实例动态选择最优处理路径（Text-only、Image-only或Fusion），减少不必要的计算和模态冲突。
- **关键技术细节**：
  - **多模态编码**：并行提取三类特征：
    - 文本表编码：Table-as-Text模型（TableGPT2-7B）的编码器输出，经注意力掩码均值池化得`et`（3584维）。
    - 图像表编码：Table-as-Image模型（Ovis2-8B）的视觉tokenizer输出，经空间均值池化得`ev`（6144维）。
    - 查询编码：使用Sentence-BERT（all-MiniLM-L6-v2）得`eq`（384维）。
    - 拼接得`x = [eq; et; ev]`（10112维）。
  - **门控网络**：2层MLP（隐藏层256维，ReLU，Dropout=0.1），输入`x`输出三个路径的logits `z`。
  - **训练目标**：
    - 任务损失`L_task`：计算每个路径的二进制正确性向量`s`，经温度softmax转化为软目标分布，与门控网络输出分布计算KL散度，鼓励选择所有正确路径。
    - 资源损失`L_resource`：门控网络输出分布与成本向量`c`的点积，惩罚高成本路径。
    - 总损失：`L_total = L_task + λ * L_resource`，其中`λ`控制权衡（实验选0.15）。
  - **推理流程**：
    - 门控网络选择最高logit对应的路径。
    - 若选Text-only或Image-only，则继续对应单模态模型的解码生成。
    - 若选Fusion，则执行两个单模态模型，将输出和表格传给LLM Agent（Gemini 2.0 Flash），Agent作为仲裁者（选择更可靠答案）或救援者（综合推理生成新答案）。
- **算法流程文字说明**：
  1. 输入query和表格，并行提取三类嵌入`eq, et, ev`并拼接。
  2. 门控网络计算路径logits。
  3. 确定路径（Text-only / Image-only / Fusion）。
  4. 执行对应模型生成答案；Fusion路径额外调用LLM Agent。

## 3. 实验设计
- **数据集**：7个基准，覆盖Table Question Answering（TQA）和Table Fact Verification（TFV）：
  - TQA：WTQ（4344测试）、TABMWP（7686）、TAT-QA（772）、HiTab（1586）、FeTaQA（2003，用BLEU评估）。
  - TFV：TabFact（6845）、InfoTabs（5400）。
- **评估指标**：Accuracy（除FeTaQA用BLEU）。
- **对比方法**：
  - Table-as-Text：Llama-2-7B、Llama3-Instruct-8B、TableLlama-7B、TableGPT2-7B。
  - Table-as-Image：MiniGPT-4、mPLUG-Owl、mPLUG-Owl2、LLaVA v1.5、Table-LLaVA、Qwen-VL、InternLM-XComposer2、Monkey、TabPedia、SynTab-LLaVA、MiniCPM-V-2.6、Qwen2.5-VL、Ovis2-8B等。
  - Table-as-Multimodality（MLLM-based）：HIPPO-8B、Google Gemini 2.0 Flash。
  - 基线结果来源：部分从原论文直接引用，部分自己运行。

## 4. 资源与算力
- **硬件**：单张NVIDIA H100 80GB GPU（Bunya超算）。
- **训练时长**：约13.5小时（1个epoch）。
- **可训练参数**：仅门控网络2.59M参数，所有大模型冻结（bf16加载）。
- **其他配置**：有效batch size=32（gradient accumulation=4），学习率1e-4，cosine warmup。

## 5. 实验数量与充分性
- **主要对比实验**：表1（7 benchmark vs. 18+基线）。
- **零样本泛化实验**：表2（训练集未见HiTab和FeTaQA，对比HIPPO，+18.05%准确率）。
- **效率分析**：表3（动态自适应 vs 非自适应融合的延迟和吞吐量）。
- **推理路径贡献分析**：图2（各路径正确分布、互补性、协同救援率）。
- **消融研究**：表4（随机路由 vs 非自适应融合 vs 动态路由）；表5（资源惩罚权重λ的影响）；图3/附录图8（不同λ下各数据集路由分布）；附录图9（启发式对齐度与性能的帕累托前沿）。
- **案例研究**：图4（仲裁者与救援者角色示例）。
- **充分性评价**：实验覆盖全面、对比方法丰富、消融深入（包括路径选择、成本正则化、零样本泛化）、结果具有统计稳定性（重复3次）。公平性较好：基线结果或自己复现或引用原文，且骨干模型一致。

## 6. 主要结论与发现
- **性能SOTA**：TableDART（TableGPT2-7B+Ovis2-8B）在7个基准平均准确率74.86%，超越最强基线HIPPO（70.84%）4.02%；FeTaQA上BLEU+2.93。
- **动态路由有效性**：非自适应融合在某些数据集上不如动态路由（如TABMWP +3.07%，HiTab +1.02%），说明强制融合引入噪声。
- **零样本泛化能力强**：在未见数据集上准确率仅下降0.58%（74.95→74.37），而HIPPO下降9.41%。
- **资源正则化提升泛化**：λ=0.15优于λ=0（纯准确率），表明成本惩罚有正则化作用。
- **Fusion路径补足单模态缺陷**：约14%硬案例中Fusion能救援2.4%（协同成功率平均14%），并化解冲突。

## 7. 优点
- **高效训练**：仅训练2.59M参数的门控网络，大模型冻结，训练成本低（单卡H100约13.5小时）。
- **高效推理**：动态选择路径，相比非自适应融合节省24.5%延迟。
- **模块化与通用性**：可无缝替换不同单模态骨干（验证了TableGPT2+Qwen2.5-VL变体）。
- **创新设计**：门控网络同时考虑任务正确性和资源成本；LLM Agent设计为仲裁/救援模式，无需额外微调。
- **全面实验验证**：7种不同难度数据集、零样本、消融、效率、案例分析。

## 8. 不足与局限
- **Fusion Agent依赖外部LLM API**：使用Gemini 2.0 Flash，带来API延迟和可能的数据隐私问题，且不同API版本可能影响结果。
- **实验范围有限**：仅覆盖表格理解，未验证在一般多模态任务（如图文问答、视觉推理）上的通用性。
- **训练数据偏见**：门控网络训练需预计算每个样本的路径正确性，该过程依赖于所选的单模态模型质量，若单模态模型存在系统性偏差，会传递到门控网络。
- **消融深度**：仅对比了随机路由和非自适应融合两种简单baseline，未与更先进的动态融合方法（如条件计算、软路由）比较。
- **最优配置λ=0.15**：虽然综合表现最好，但准确率仍略低于某些λ值（如λ=0.05时平均75.05% vs 74.86%），说明在效率-准确率权衡上仍有改进空间。
- **部分结果依赖外部引用**：多个基线结果来自原论文，可能因实验环境不同导致微小差异。

（完）
```
