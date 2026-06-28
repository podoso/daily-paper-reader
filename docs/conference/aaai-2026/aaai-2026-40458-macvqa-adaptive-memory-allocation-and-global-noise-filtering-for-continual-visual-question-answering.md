---
title: "MacVQA: Adaptive Memory Allocation and Global Noise Filtering for Continual Visual Question Answering"
title_zh: MacVQA：用于持续视觉问答的自适应内存分配与全局噪声过滤
authors: "Zhifei Li, Yiran Wang, Chenyi Xiong, Yujing Xia, Xiaoju Hou, Yue Zhao, Miao Zhang, Kui Xiao, Bing Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40458/44419"
tags: ["query:continual"]
score: 7.0
evidence: 结合记忆机制的持续学习方法应用于视觉问答
tldr: 持续视觉问答面临知识保留与适应新信息的平衡难题。本文提出MacVQA框架，通过自适应内存分配与全局噪声过滤融合视觉与文本信息，并采用原型记忆分配优化特征质量。实验证明该方法在持续VQA任务中有效缓解灾难性遗忘，为多模态持续学习提供了可借鉴方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有持续VQA方法难以平衡知识保留、新信息适应与鲁棒特征表示。
method: 设计自适应内存分配与全局噪声过滤模块，融合视觉与问题信息，并利用原型记忆分配优化特征。
result: 在持续VQA基准上实现更优的知识保留与任务适应平衡。
conclusion: 该方法通过噪声过滤与自适应记忆机制提升了持续VQA的鲁棒性与可扩展性。
---

## Abstract
Visual Question Answering (VQA) requires models to reason over multimodal information, combining visual and textual data. With the development of continual learning, significant progress has been made in retaining knowledge and adapting to new information in the VQA domain. However, current methods often struggle with balancing knowledge retention, adaptation, and robust feature representation. To address these challenges, we propose a novel framework with adaptive memory allocation and global noise filtering called MacVQA for visual question answering. MacVQA fuses visual and question information while filtering noise to ensure robust representations, and employs prototype-based memory allocation to optimize feature quality and memory usage. These designs enable MacVQA to balance knowledge acquisition, retention, and compositional generalization in continual VQA learning. Experiments on ten continual VQA tasks show that MacVQA outperforms existing baselines, achieving 43.38% average accuracy and 2.32% average forgetting on standard tasks, and 42.53% average accuracy and 3.60% average forgetting on novel composition tasks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究对象**：持续视觉问答（Continual VQA），即模型在顺序学习多个视觉问答任务时，需要在吸收新知识的同时保留先前学到的知识。
- **核心挑战**：现有方法（如正则化、重放）难以同时平衡知识保留、新任务适应和鲁棒特征表示；尤其在多模态场景下，视觉噪声和动态任务分布会加剧灾难性遗忘。
- **论文目标**：设计一个能有效过滤视觉噪声、并动态优化内存资源分配的框架，以提升持续 VQA 的准确率和抗遗忘能力。

## 2. 论文提出的方法论

- **整体框架**：MacVQA 包含两个核心模块——Global Noise Filtering (GonF) 和 Adaptive Memory Allocation (AMA)，基于 VL-T5 主干。
- **Global Noise Filtering（GonF）**：
  - **特征评分与加权**：对 Faster R-CNN 提取的每个区域特征计算注意力权重（公式 1），加权求和得到全局特征 \( G \)（公式 2）。
  - **去噪自编码器 (DAE)**：将原始区域特征 \( V \) 输入 DAE 得到去噪特征 \( V' \)。
  - **融合**：全局特征 \( G \) 与去噪特征 \( V' \) 结合得到增强特征 \( V'' \)。
  - **损失函数**（公式 3）：重建误差（MSE）加注意力熵正则化（超参数 \( \theta_1 \)）。
- **Adaptive Memory Allocation（AMA）**：
  - **特征投影**：将多模态编码器输出的隐藏状态 \( H \) 投影到视觉和文本子空间 \( H_v, H_q \)（公式 4）。
  - **原型检索**：维护视觉原型集 \(\{V_m\}\) 和文本原型集 \(\{Q_n\}\)，用余弦相似度（公式 5）选取 top‑k 最相似的原型。
  - **门控融合**：计算门控向量 \( g \)（公式 6），控制视觉和文本原型的贡献；最终特征 \( H' = H + \alpha Q_p + \beta V_p \)（公式 8），其中 \( \alpha, \beta \) 由门控和 softmax 权重决定（公式 9）。
  - **内存更新**：采用时间插值 \( P_i = \lambda P_{i-1} + (1-\lambda)H \)（公式 7），平衡旧记忆与新信息。
  - **损失函数**（公式 10）：包含相似度最大化、门控正则化和特征更新约束（超参数 \( \theta_2, \theta_3 \)）。
- **多模态解码**：将视觉和文本嵌入拼接后通过 Transformer 解码器生成答案，使用负对数似然损失（公式 14）。
- **总损失**：\( L_{total} = \phi_1 L_{GonF} + \phi_2 L_{AMA} + \phi_3 L_{decoder} \)（公式 15），三个超参数和为 1。

## 3. 实验设计

- **数据集**：VQA v2（超过 20 万 COCO 图片，110 万 QA 对），按问题类型分为 10 个连续任务：recognition, location, judge, commonsense, count, action, color, type, subcategory, causal。
- **测试设置**：
  - **Standard Test**：评估在已见过的技能‑概念组合上的性能。
  - **Novel Composition Test**：评估在未见过组合上的泛化能力。
- **对比方法**：Vanilla（无持续学习）、EWC、MAS、ER、DER、VQACL、QUAD、ProtoGroup（共 8 种基线）。
- **评估指标**：Final Average Performance (AP↑) 和 Average Forgetting (AF↓)。
- **实现细节**：所有方法基于预训练 VL‑T5，使用 Adam 优化器，学习率 3e‑5，梯度裁剪 5，warmup 比例 0.1。

## 4. 资源与算力

- **未明确说明**：论文在实现细节中只给出了优化器、学习率等超参数，**未提及所使用的 GPU 型号、数量或训练时长**。因此无法定量评估算力消耗。

## 5. 实验数量与充分性

- **主实验结果**：Table 1 展示了 10 个任务在两种测试设置下的完整对比，共 20 行（9 种方法 × 2 设置）。
- **消融实验**：Table 2 对 GonF 和 AMA 分别进行消融（GonF / AMA / Both / None），验证了各模块的贡献。
- **原型选择策略**：Table 3 对比了 Random 与 Max‑Similarity 两种策略。
- **内存容量敏感性**：Figure 4 展示了不同内存大小（1000‑5000）下 AP 和 AF 的变化。
- **超参数敏感性**：Figure 5 展示了视觉贡献 α 和问题贡献 β 的网格搜索（0.2‑1.0），揭示任务特异性偏好。
- **定性分析**：Figure 3 展示原型相似度雷达图；Figure 6 给出标准与新颖组成测试的示例。
- **评估充分性**：实验覆盖了多个维度（模块、策略、容量、超参数），消融和敏感性分析完整，对比基线全面且为公平设置（相同骨干和协议），结论具有说服力。

## 6. 论文的主要结论与发现

- MacVQA 在标准测试上达到 **43.38% AP** 和 **2.32% AF**，在新型组合测试上达到 **42.53% AP** 和 **3.60% AF**，均优于所有基线。
- 消融实验表明，GonF 主要提升感知类任务（如 recognition, location），AMA 主要辅助记忆敏感的推理任务（如 color, typicality），两者结合互补性明显。
- Max‑Similarity 原型选择策略优于随机，说明选择性检索语义对齐原型对知识保留至关重要。
- 内存容量分析显示 MacVQA 在不同大小下均保持最高 AP 和最低 AF，内存利用效率优于已有方法。
- 超参数敏感性分析表明模型可针对不同任务动态调整视觉/文本权重，具有灵活性。

## 7. 优点

- **方法创新**：将全局噪声过滤与基于原型的自适应内存分配相结合，同时解决视觉鲁棒性和知识保留两个核心问题。
- **实验全面**：包括 10 个任务、两种测试范式、充分消融和超参数分析，对比方法涵盖近年的主流工作。
- **结果显著**：在多个任务上实现明显提升（如 color 提升约 10 个点，action 提升约 8 个点），遗忘率最低。
- **代码开源**：提供了 GitHub 仓库，利于复现和后续研究。

## 8. 不足与局限

- **数据集单一**：仅在 VQA v2 上评估，未在 GQA、Visual7W 等其他 VQA 数据集或更多模态任务（如视频 QA）上验证泛化性。
- **未讨论计算成本**：虽然消融了模块效果，但未报告训练/推理时间、参数增量或 GPU 显存占用，难以评估实际部署负担。
- **内存机制限制**：原型池的大小固定，未来任务数量无限增长时可能饱和，论文未讨论动态扩展策略。
- **基线覆盖有限**：未与最新的基于大语言模型（如 BLIP‑2、LLaVA）的持续学习方法比较（可能因追求公平性仅用 VL‑T5 主干）。
- **超参数依赖性**：GonF 和 AMA 均引入较多超参数（\( \theta_1, \theta_2, \theta_3, \lambda, \phi_1, \phi_2 \) 等），虽然做了敏感性分析，但在实际应用中调参成本较高。

（完）
