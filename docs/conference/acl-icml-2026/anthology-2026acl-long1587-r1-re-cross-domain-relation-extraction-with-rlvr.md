---
title: "R1-RE: Cross-Domain Relation Extraction with RLVR"
title_zh: R1-RE：基于强化学习与可验证奖励的跨域关系抽取
authors: "Runpeng Dai, Tong Zheng, Run Yang, Kaixian Yu, Hongtu Zhu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1587.pdf"
tags: ["query:ie"]
score: 9.0
evidence: 关系抽取强化学习框架
tldr: "针对关系抽取在域外泛化能力差的问题，提出R1-RE框架，将关系抽取重塑为基于标注指南的推理任务，利用强化学习与可验证奖励激发小语言模型的推理能力。在Sem-2010和MDKG数据集上，R1-RE-7B模型取得了约70%的平均域外准确率，显著提升了鲁棒性。"
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1587/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 707, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1587/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 790, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1587/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1641, \"height\": 840, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1587/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1500, \"height\": 1026, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1587/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1587/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1623, \"height\": 1294, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 733, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 759, \"height\": 528, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1153, \"height\": 1345, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 645, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1587/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1518, \"height\": 512, \"label\": \"Table\"}]"
motivation: 传统关系抽取方法在域外泛化上表现不佳，受人类标注者工作流程启发，将关系抽取视为推理任务。
method: 提出R1-RE框架，首次将强化学习与可验证奖励应用于关系抽取任务。
result: "在Sem-2010和MDKG数据集上，R1-RE-7B模型平均域外准确率约70%。"
conclusion: 该框架有效提升了小语言模型在关系抽取任务上的跨域鲁棒性。
---

## Abstract
Relation extraction (RE) is a core task in natural language processing. Traditional approaches typically frame RE as a supervised learning problem, directly mapping context to labels—an approach that often suffers from poor out-of-domain (OOD) generalization. Inspired by the workflow of human annotators, we reframe RE as a reasoning task guided by annotation guidelines and introduce R1-RE, the first reinforcement learning with verifiable reward (RLVR) framework for RE tasks. Our method elicits the reasoning abilities of small language models for annotation tasks, resulting in significantly improved OOD robustness. We evaluate our approach on the public Sem-2010 dataset and a private MDKG dataset. The R1-RE-7B model attains an average OOD accuracy of approximately 70%, on par with leading proprietary models such as GPT-4o. Additionally, our comprehensive analysis provides novel insights into the training dynamics and emergent reasoning behaviors of the RLVR paradigm for RE.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：传统关系抽取（RE）方法通常视为监督学习任务，直接学习句子到标签的映射，导致域外（OOD）泛化能力差。小型语言模型（7B/8B）在域外场景中表现显著低于大型商业模型（如GPT-4o）。
- **动机**：受人类标注者工作流程启发——人类借助标注指南进行多步推理（假设-验证-结论）而非直接匹配。这种推理技能具有跨域迁移性，因此希望将RE重构为基于指南的推理任务。
- **意义**：本文首次将**强化学习与可验证奖励（RLVR）**应用于RE任务，旨在激发小语言模型的推理能力，实现稳健的跨域关系抽取。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将关系分类（RC）视为一个由**标注指南**驱动的多步推理过程。模型需先分析实体，再逐条比对关系定义，形成推理链并输出最终答案。
- **关键技术细节**：
  - **Prompt设计**：显式嵌入标注指南，要求模型输出<think>...</think>（推理过程）和<answer>...</answer>（最终答案），答案格式为`关系类型(e1,e2)`。
  - **R1-RE框架**：采用**Group Relative Policy Optimization (GRPO)** 算法优化策略πθ，目标函数最大化期望奖励。GRPO对每组G个候选输出的优势值进行归一化，并通过裁剪与KL散度约束稳定训练。
  - **多阶段奖励设计**：
    - 格式奖励（r_format）：响应格式正确得+1，错误得-3。
    - 指标奖励（r_metric）：格式正确后，预测正确得+2，错误得-1.5。
    - 最终奖励：格式错误则r = -3；格式正确则r = 1 + r_metric（正确时总+3，错误时总-0.5）。
  - 对三元组抽取（TE）任务，采用两阶段F1分数作为奖励（实体级F1和三元组级F1加权）。

### 3. 实验设计
- **数据集**：
  - **Sem-2010**：公开的SemEval-2010 Task 8，17类关系，约8,353训练/500测试。
  - **MDKG**：私有精神疾病知识图谱数据集，17类关系，约10,033训练/500测试。
- **Benchmark对比方法**：
  - **闭源模型**：Claude 3.5 Sonnet、GPT-4o、GPT-4.1-mini。
  - **开源模型**：Qwen2.5-7B/14B/32B/72B-Instruct、Llama-3.1-8B-Instruct。
  - **基线方法**：对Qwen2.5-7B和Llama-3.1-8B进行监督微调（SFT），使用相同prompt模板。
- **评估指标**：Avg@4（四次采样的平均Pass@1准确率）和Pass@4。

### 4. 资源与算力
- **设备**：8张NVIDIA A100（80GB）GPU。
- **训练配置**：全参数、全精度（无LoRA/量化）调优。
  - R1-RE：学习率1e-6，train_batch_size=32，总训练步数400，max_response_length=3K，rollout.n=16。
  - SFT基线：学习率5e-6，batch_size=16，总训练步数600。
- **框架**：R1-RE基于verl训练框架，SFT基于LLaMA-Factory。

### 5. 实验数量与充分性
- **主实验**（表3）：包含3个闭源模型、5个开源模型、4个R1-RE变体（7B/8B分别在MDKG和Sem上训练）及4个SFT基线，共16种对比，覆盖域内和域外准确率。
- **消融与分析实验**：
  - **训练动态可视化**（图6）：追踪奖励、响应长度、域内/域外准确率变化。
  - **案例研究**（图5）：对比基线模型与R1-RE的推理路径。
  - **跨任务泛化测试**（表4）：在MATH-500、IFEval、GPQA上评估，验证RL训练不损害且能提升其他能力。
  - **数据扩充实验**（表5）：加入Sem-2018额外训练数据后，域外准确率提升约4%。
  - **奖励设计鲁棒性**（表6）：替换奖励尺度{−3,−1,3}后性能变化极小（±1.8%内）。
- **充分性**：实验设计较为全面，覆盖域内/域外、不同模型规模、SFT对比、额外数据集、跨任务及奖励消融，且所有评估采用零样本统一prompt，公平性可接受。但三元组抽取任务仅在附录简要提及，主要结论基于关系分类。

### 6. 论文的主要结论与发现
- R1-RE显著提升小语言模型（7B/8B）的关系抽取能力：
  - 域内准确率提升约52~53个百分点，域外提升约28~31个百分点。
  - 相比SFT，域外准确率超越15~16个百分点。
- R1-RE-7B在私有MDKG上的域外性能（约70%）与GPT-4o相当。
- 训练过程中**响应长度自然增长**（从200令牌增至500~1000），体现出真正的多步推理行为，而非简单模式匹配。
- **跨任务泛化**：RL训练未降低MATH-500、IFEval、GPQA性能，反而略有提升；而SFT导致下降。
- 增加额外训练数据（Sem-2018）可进一步提升域外性能约4%。
- 奖励设计对尺度不敏感，鲁棒性良好。

### 7. 优点
- **方法新颖**：首次将RLVR引入关系抽取领域，开创性地将RE视为推理任务。
- **模仿人类标注流程**：prompt设计与奖励机制鼓励模型形成假设-验证的推理链，产出可解释的中间步骤。
- **小模型达到大模型效果**：仅7B参数即可与GPT-4o竞争域外性能，具有显着的成本效益。
- **实验分析深入**：不仅报告准确率，还通过训练动态、案例研究、跨任务评测全面揭示学习机制。
- **奖励设计简洁有效**：基于规则而非训练奖励模型，避免了奖励破解问题，且鲁棒性验证充分。

### 8. 不足与局限
- **任务覆盖不全**：主要验证关系分类（RC），三元组抽取（TE）仅在附录给出初步设计，缺乏与SFT/RL的详细对比实验。
- **模型规模局限**：仅评估7B/8B参数级别，未验证在更大模型（如14B/32B/72B）上的效果。R1-RE在更大模型上的推广性未知。
- **数据偏差风险**：私有MDKG数据集未公开，可复现性受限；Sem-2010上表现与模型规模不成正比，暗示可能存在数据泄漏，影响对比公平性。
- **计算资源与可推广性**：8块A100的算力需求对一般研究群体较高；全参数训练的开销较大，未探索参数高效微调（如LoRA）的效果。
- **实验设计局限性**：仅使用两个数据集（一个公开、一个私有），跨域场景代表性有限。域外定义仅指数据集间的迁移，未测试真实多领域（如生物医学、电商等）。
- **未与现有最强RE方法（如基于检索的RAG+LLM）对比**：基线仅包含直接微调或直接推理的LLM，未与结合知识库的方法比较。

（完）
