---
title: Catastrophic Forgetting in Kolmogorov-Arnold Networks
title_zh: Kolmogorov-Arnold网络中的灾难性遗忘
authors: "Mohammad Marufur Rahman, Guanchu Wang, Kaixiong Zhou, Minghan Chen, Fan Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39697/43658"
tags: ["query:continual"]
score: 8.0
evidence: 持续学习中的灾难性遗忘
tldr: 该论文系统研究了KAN网络中的灾难性遗忘现象，提出了一个新的理论框架将遗忘与激活支持重叠和数据内在维度联系起来，并通过实验验证了该框架的解释力，为设计更具鲁棒性的持续学习架构提供了理论指导。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: KAN网络声称具有抗遗忘能力，但其实际持续学习行为尚不明确，缺乏理论理解。
method: 构建理论框架，分析激活支持重叠和数据内在维度对遗忘的影响，并进行实验验证。
result: 揭示了KAN网络在持续学习中的遗忘机制，验证了理论框架的有效性。
conclusion: 为理解KAN网络的遗忘特性提供了理论基础，并指导未来抗遗忘架构设计。
---

## Abstract
Catastrophic forgetting is a longstanding challenge in continual learning, where models lose knowledge from earlier tasks when learning new ones. While various mitigation strategies have been proposed for Multi-Layer Perceptrons (MLPs), recent architectural advances like Kolmogorov-Arnold Networks (KANs) have been suggested to offer intrinsic resistance to forgetting by leveraging localized spline-based activations. However, the practical behavior of KANs under continual learning remains unclear, and their limitations are not well understood. To address this, we present a comprehensive study of catastrophic forgetting in KANs and develop a theoretical framework that links forgetting to activation support overlap and intrinsic data dimension. We validate these analyses through systematic experiments on synthetic and vision tasks, measuring forgetting dynamics under varying model configurations and data complexity. Further, we introduce KAN-LoRA, a novel adapter design for parameter-efficient continual fine-tuning of language models, and evaluate its effectiveness in knowledge editing tasks. Our findings reveal that while KANs exhibit promising retention in low-dimensional algorithmic settings, they remain vulnerable to forgetting in high-dimensional domains such as image classification and language modeling. These results advance the understanding of KANs’ strengths and limitations, offering practical insights for continual learning system design.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：灾难性遗忘是持续学习中的长期挑战，即模型在学习新任务时丢失旧任务知识。尽管MLP中已有多种缓解策略，但近年来提出的Kolmogorov-Arnold Networks（KANs）因其基于局部样条的可学习激活函数，被认为可能天然抵抗遗忘。然而，KANs在持续学习中的实际行为尚不明确，其局限性也未被充分理解。
- **研究动机**：填补理论空白，系统研究KANs的灾难性遗忘现象，建立理论框架解释遗忘机制，并通过实验验证。
- **整体含义**：揭示KANs在低维任务中保留能力强，但在高维任务中仍易遗忘，为设计抗遗忘架构提供理论指导。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：遗忘与KANs中样条激活函数的局部支持重叠（activation support overlap）以及任务数据的内在维度（intrinsic data dimension）相关。
- **关键技术细节**：
  - 定义遗忘度量 \( F_i = \mathcal{L}(f^{(T)}, D_i) - \mathcal{L}(f^{(i)}, D_i) \)。
  - 定义激活支持 \( S^{(i)}_{\ell,p,q} \) 为分支函数非零的输入子集，用勒贝格测度量化大小。
  - 定义最大一维重叠 \( \Delta_{i,j} = \max_{\ell,p,q} \mu(S^{(i)}_{\ell,p,q} \cap S^{(j)}_{\ell,p,q}) \)。
  - **引理1（零重叠保留）**：若 \( \Delta_{i,j}=0 \)，则 \( F_i=0 \)。
  - **定理1（保留边界）**：在Lipschitz和有界损失假设下，\( F_i \leq C \sum_{\ell} N_\ell L_\ell \Delta_{i,j} \)，遗忘与重叠线性相关。
  - **定理2（分支累积遗忘）**：遗忘受分支在所有后续任务中累积重叠的驱动。
  - **推论1（随机支持期望）**：期望遗忘与支持大小乘积 \( s_i s_j \) 相关。
  - **推论2（饱和边界）**：当分支整个支持被覆盖后，遗忘饱和。
  - **定理3（内在维度遗忘率）**：任务内在维度 \( d_t \) 越高，期望重叠 \( O(r^{d_i+d_j}) \) 越大，遗忘 \( O(\sum N_{tot} \bar{L} r^{d_i+d_j}) \) 呈指数增长。
  - **推论3**：低维任务遗忘可忽略。
  - **推论4**：支持碎片化可缓解高维遗忘。
- **算法流程**：无具体算法，但理论分析指导了实验设计。

## 3. 实验设计：数据集、基准、对比方法

- **数据集/场景**：
  - **低维合成任务**：二进制加法（5个任务：1's addition 到5's addition）；十进制加法（相同构造）。
  - **高维图像分类**：CIFAR-10（5个任务，每任务2类）、Tiny-ImageNet（5个任务，10类）、MNIST（5个任务）。
  - **语言模型知识编辑**：使用CounterFact和ZsRE基准，构建5个连续编辑任务。
- **基准**：
  - 对于图像分类，构建MLP-Transformer + EWC作为基线。
  - 对于语言模型，构建MLP-LoRA（相同EWC设置）作为基线。
- **对比方法**：
  - KAN-Transformer vs MLP-Transformer（图像分类）。
  - KAN-LoRA vs MLP-LoRA（语言模型）。
  - 还对比了专门的MLP架构（二进制加法）。

## 4. 资源与算力

- **文中未明确说明GPU型号、数量、训练时长等具体算力信息**。仅提供了KAN-LoRA和MLP-LoRA的训练时间和推理时间（见表5，单位：秒/epoch和秒/sample），但未给出训练总时长或硬件细节。因此无法总结完整算力开销。

## 5. 实验数量与充分性

- **实验数量**：
  - 合成任务：二进制加法、十进制加法（不同网格大小5/10/15/20）。
  - 图像分类：在CIFAR-10、Tiny-ImageNet、MNIST上测试，并改变任务数量（2~5）、样本数（每任务1~20）、模型配置（编码器块数、注意力头数、分类层数）。还进行了支持重叠与遗忘的定量比较（表1、表2），以及内在维度与遗忘率的对数关系（表3）。
  - 语言模型知识编辑：在Llama2-7B和Llama2-13B上测试KAN-LoRA和MLP-LoRA，改变适配器秩（8和16）、每任务样本数（100个样本？实际表4中显示每任务100个样本），但文中提到“low-sample per task”，具体数值未完全一致。涉及多个数据集。
- **充分性**：整体实验设计较为系统，覆盖低维和高维任务，验证了理论预测（线性关系、指数关系、饱和效应）。但图像分类实验仅在CIFAR-10、Tiny-ImageNet、MNIST上进行，未涉及更大规模或更复杂的持续学习基准（如CIFAR-100、ImageNet-1000、5-Datasets等）。消融实验较充分（网格大小、任务数、样本数、模型深度等）。
- **公平性**：对比时使用了相同的EWC正则化，架构上尽量对等（Transformer基础），但KAN-Transformer与MLP-Transformer的参数量可能存在差异（未明确说明，但表5显示KAN-LoRA参数量约是MLP-LoRA的10倍）。这可能导致比较不公平。作者在表5中承认KAN引入更多参数，但未讨论是否通过调整容量使对比公平。

## 6. 论文的主要结论与发现

- 遗忘与激活支持重叠线性相关（验证了定理1、2）。
- 遗忘随内在维度指数增长（验证了定理3）。
- 增加网格大小（更细的样条分辨率）可降低重叠，缓解遗忘。
- 在低维合成任务（二进制加法）中KAN几乎不遗忘，性能优于专门MLP；但在高维图像任务（Tiny-ImageNet）中KAN不如MLP+EWC。
- KAN-LoRA在高秩和少样本场景下优于MLP-LoRA，但参数量更大。
- 遗忘存在饱和效应（推论2）。
- 提出将遗忘视为可塑造的性质，而非必须消除的缺陷。

## 7. 优点

- **理论创新**：首次为KANs的灾难性遗忘建立严格理论框架，连接激活局部性、支持重叠、内在维度，推导定量边界。
- **实验验证充分**：通过多种任务类型（合成、图像、语言）和参数变化（网格大小、模型深度、任务数量）验证理论。
- **应用拓展**：提出KAN-LoRA适配器，用于语言模型持续知识编辑，展示了KAN在参数高效微调中的潜力。
- **视角新颖**：指出遗忘可能作为有益归纳偏置，提出未来研究方向。
- **开源贡献**：提供代码链接。

## 8. 不足与局限

- **实验覆盖有限**：图像分类仅在CIFAR-10、Tiny-ImageNet、MNIST上测试，未在更复杂的持续学习基准（如CIFAR-100、ImageNet-1000、5-Datasets、Split SVHN等）上评估。语言模型知识编辑仅使用CounterFact和ZsRE，缺乏对更广泛编辑场景的测试。
- **公平性风险**：KAN-Transformer参数量可能显著大于MLP-Transformer（未控制变量），导致比较不公平。表5显示KAN-LoRA参数量约为MLP-LoRA的10倍，但未讨论是否因参数增加导致性能优势。
- **理论假设限制**：定理1-3依赖于Lipschitz和有界损失等假设，实际中可能不严格成立。
- **未考虑其他持续学习方法**：仅与EWC比较，未对比其他主流方法（如GDumb、Experience Replay、Packing等）。
- **代码可用性声明**：虽提供GitHub链接，但论文未验证代码是否可复现全部结果。
- **泛化性疑问**：KAN在低维任务表现优异，但在高维任务中反而较差，实际应用场景中多数任务为高维，限制了KAN在持续学习中的实用性。

（完）
