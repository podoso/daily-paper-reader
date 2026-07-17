---
title: "From Recognition to Reasoning: Benchmarking and Enhancing MLLMs on Real-World Receipt Document Understanding"
title_zh: 从识别到推理：基于真实世界收据文档理解的MLLM基准测试与增强
authors: "Yandi Wang, Libin Zhan, Ziwei Huang, Tiancheng Luo, Yuxuan Jiang, Wang Dong, Leilei Gan, Jun Chen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2135.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 面向收据文档理解的视觉信息抽取基准
tldr: 现有视觉信息抽取基准在规模、真实性和语义粒度上不足。本文构建ReceiptBench，包含一万张多样化收据，组织四个层次子任务：基础感知、格式标准化、语义推理和隐含推断。评估发现多模态大模型在推理任务上仍存局限，本基准推动更全面的文档理解研究。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2135/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1640, \"height\": 888, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2135/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 794, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2135/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 199, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2135/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.2135/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1640, \"height\": 641, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1660, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 572, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 713, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 848, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 610, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1662, \"height\": 741, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 811, \"height\": 151, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 813, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 809, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 807, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.2135/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 810, \"height\": 204, \"label\": \"Table\"}]"
motivation: 现有VIE基准规模小、缺乏真实性和语义层次。
method: 构建大规模人工标注收据基准，包含四个递进子任务评估MLLM。
result: 揭示了MLLM在语义推理和隐含推断上的不足。
conclusion: 为视觉信息抽取提供了更贴近真实场景的评测基准和洞察。
---

## Abstract
Extracting structured information from visual documents (Visual Information Extraction, VIE) is a cornerstone of business automation. While recent Multimodal Large Language Models (MLLMs) have shown promising capabilities, existing benchmarks suffer from critical limitations in scale and realism, lack semantic granularity, and fail to cover diverse document types. To bridge this gap, we introduce ReceiptBench, a large-scale, human-annotated benchmark consisting of 10k diverse receipts, organizing information extraction into four hierarchical sub-tasks: (1) Basic Perception for raw text spotting, (2) Format Normalization for strictly following standardization instructions, (3) Semantic Reasoning for inferring implicit attributes from context, and (4) Structure Parsing for handling nested line items. Furthermore, we propose a two-stage training framework incorporating Metric-Aware Group Relative Policy Optimization (GRPO), which translates rigorous evaluation constraints into reinforcement learning signals to enhance structural consistency. Extensive experiments demonstrate that our method yields state-of-the-art performance, surpassing leading proprietary models on complex reasoning tasks. We release our datasets and code at https://github.com/wwwT0ri/ReceiptBench.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）
- **问题**：视觉信息抽取（VIE）是业务流程自动化的基础，但现有基准存在三大缺陷：
  - **规模与真实性不足**：早期数据集（如SROIE、CORD）小于2000张，且仅为零售或餐饮领域的简单单据；合成数据集（如FATURA）模板有限，缺乏真实语义逻辑。
  - **语义粒度欠缺**：大多数基准仅关注显式文本提取（浅层感知），忽略了真实财务处理中所需的格式规范化、隐式推理和结构化解析。
  - **文档类型单一**：缺乏多语言、多布局（如酒店账单、交通票据）的复杂文档。
- **整体含义**：推动VIE从“文字识别”迈向“认知推理”，为多模态大模型（MLLM）在真实财务审计场景中的能力评估提供标准化测试平台。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：构建大规模、高真实性、多层次的收据理解基准，并提出结合监督微调（SFT）与指标感知GRPO的对齐训练框架，将严格的评估规则转化为强化学习奖励，提升模型的结构化输出一致性。
- **关键技术细节**：
  - **基准构建（ReceiptBench）**：
    - 收集10,656张真实收据图像（网络爬取+众包），覆盖10类文档（酒店、交通、购物等），98%为英文，含2%多语言长尾样本。
    - 定义19个字段，按认知需求分为4个子任务：
      1. **基础感知（8字段）**：OCR识别显式文本（如发票号、原始时间）。
      2. **格式规范化（4字段）**：将原始文本转为标准格式（如日期YYYY-MM-DD）。
      3. **语义推理（6字段）**：从上下文推断隐含属性（如从地址推断货币代码）。
      4. **结构解析（1字段）**：解析嵌套表格为列表（商品明细、金额、是否为税款）。
  - **混合评估协议**：
    - 精确匹配字段、数值容差、LLM语义判断（Qwen3-4B作判官）、“结构化列表”用匈牙利算法匹配（考虑列维斯坦、词序、LCS、语义嵌入加权相似度，并施加强约束：金额差异>0.05则代价无穷）。
    - 主报告F1分数，显式包含真阴性（正确输出空字符串）以避免惩罚。
  - **两阶段训练框架**：
    - **阶段1：SFT**——用严格指令格式（含系统提示、字段约束、负约束）训练模型遵循JSON schema。
    - **阶段2：Metric-Aware GRPO**——设计基于混淆矩阵的奖励函数：
      - TP：对齐分数S∈[0,1]（语义字段由LLM Judge提供）；
      - TN：λ_TN=0.3（鼓励正确识空，但防模式崩溃）；
      - FP：λ_FP=-0.5（显式惩罚幻觉）；
      - FN：λ_FN=0。
      - 最终奖励为19个字段的平均奖励，用于组相对策略优化（GRPO），KL系数0.01，每提示采样16个。

## 3. 实验设计
- **数据集**：ReceiptBench（10,656张），分层采样保留2,000张为测试集，其余训练。
- **Benchmark**：整体F1和4个子任务F1。
- **对比方法**：三类：
  1. **专有闭源**：GPT-5、Gemini-3-Pro、InternVL3.5-241B、Qwen3-VL-Plus。
  2. **开源通用MLLM**：InternVL3（2B/8B/78B）、Qwen3-VL（4B/8B/32B）。
  3. **专用文档模型**：DianJin-OCR-R1、DeepSeek-OCR-small、olmOCR-7B、PaddleOCR-VL 0.9B。
- **实现细节**：基于LLaMA-Factory框架，SFT：2 epoch，batch size=16（梯度累积8），学习率1e-5余弦衰减，BF16混合精度，最大上下文5120 tokens。GRPO：KL系数0.01，每提示16样本。全部实验在4×NVIDIA A800 GPU上运行。

## 4. 资源与算力
- 文中明确说明：**所有实验在4×NVIDIA A800 GPU上完成**。SFT阶段使用每卡batch size 2，梯度累积8达到全局batch 16。GRPO阶段未提具体时长，但提到“计算成本高于标准SFT”。未提供训练总时长。

## 5. 实验数量与充分性
- **主要实验结果**（表3）：包含20+种模型的整体及子任务F1。
- **消融实验**（表4）：SFT vs GRPO vs 组合，验证各阶段贡献。
- **错误分析**（图3）：对比Qwen3-VL-4B与Gemini-3-Pro的错误类型分布（漏检、幻觉、感知错误等）和字段难度排名。
- **鲁棒性分析**（附录D.1）：在类别平衡测试集（1387样本）和非英语子集（213样本）上验证排名一致性。
- **幻觉抑制定量证明**（附录D.2）：比较SFT与SFT+GRPO的精确率和FP绝对数下降（如invoice_number FP减少64.3%）。
- **超参数敏感性分析**（附录D.3）：在4组不同相似度权重配置下重排名，模型相对顺序严格一致。
- **定性案例**（附录D.4）：单张酒店收据的对比输出。
- **总体评价**：实验设计充分、多角度，涵盖了不同模型规模、不同子任务、消融、鲁棒性、错误分析，客观公平。但未在多种随机种子下重复实验（单次运行），也未报告方差。

## 6. 主要结论与发现
- **领域特定对齐比参数规模更重要**：微调后的Qwen3-VL-8B（0.7950）全面超越GPT-5（0.7076）和Gemini-3-Pro（0.7373）。
- **Metric-Aware GRPO有效提升感知和推理，但小模型（2B）存在稳定性问题**（reward collapse）。
- **结构解析是所有模型的瓶颈**，但SFT显著改善（GPT-5仅0.4893，微调后Qwen3-VL-4B达0.6478）。
- **专有模型倾向幻觉（过度自信生成）**，而微调模型倾向保守（漏检），GRPO能显著抑制FP（最高减少68.8%）。
- **SFT建立基础，GRPO进一步优化逻辑一致性**，但单独使用GRPO会弱化视觉接地。

## 7. 优点
- **基准质量高**：10k真实多样收据，严格三阶段验证（人工+自动逻辑+迭代修正），最终标注准确率98.7%。
- **任务层次合理**：从感知到结构解析，对应真实财务处理需求，且字段定义符合GAAP和税务法规。
- **评估协议创新**：混合精确匹配、语义LLM判官、匈牙利算法，并正确处理空字段（TN），避免偏差。
- **奖励设计巧妙**：基于混淆矩阵的显式惩罚幻觉（FP），并给予空字段适当奖励（避免模式崩溃），将评估标准直接转化为RL信号。
- **实验全面**：覆盖多族模型、消融、鲁棒性、误差分析、超参敏感性，结论可信。
- **开源代码和数据**：促进后续研究。

## 8. 不足与局限
- **数据语言偏差**：98%为英文，多语言仅213样本，跨语言泛化性有限。
- **隐私掩码影响**：所有PII被遮挡，可能改变文档视觉分布，与内部企业数据存在差距。
- **未系统做视觉数据增强**：未测试旋转、模糊、噪音等对模型鲁棒性的影响。
- **GRPO训练成本高**：相比标准SFT需要更多采样和计算，缺乏效率改进。
- **小模型不稳定**：2B模型在GRPO阶段出现奖励崩溃，提示模型容量阈值问题。
- **未在多种子下重复实验**：缺乏统计显著性测试，可能受单次运行随机性影响。
- **应用限制**：仅覆盖收据/发票领域，其他文档（如合同、报告）未涉及。

（完）
