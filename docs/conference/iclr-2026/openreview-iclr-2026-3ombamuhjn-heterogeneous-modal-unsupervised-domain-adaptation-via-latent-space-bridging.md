---
title: Heterogeneous-Modal Unsupervised Domain Adaptation via Latent Space Bridging
title_zh: 基于潜在空间桥接的异质模态无监督域适应
authors: "Jiawen Yang, Shuhao Chen, Shengtao Zhang, Yucong Duan, Ke Tang, Yu Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=3OMBAMuhJn"
tags: ["query:multimodal"]
score: 4.0
evidence: 异质模态域适应
tldr: 该论文提出异质模态无监督域适应（HMUDA）新问题，并设计潜在空间桥接（LSB）框架，通过双分支架构和特征一致性损失实现不同模态间的知识迁移。尽管涉及多模态，但任务为语义分割，与多模态实体关系抽取无直接关联。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 1880, \"height\": 1404}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 537, \"height\": 323}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 674, \"height\": 402}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 686, \"height\": 411}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 628, \"height\": 375}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-006.webp\", \"caption\": \"\", \"page\": 4, \"index\": 6, \"width\": 671, \"height\": 405}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-007.webp\", \"caption\": \"\", \"page\": 4, \"index\": 7, \"width\": 547, \"height\": 320}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-008.webp\", \"caption\": \"\", \"page\": 4, \"index\": 8, \"width\": 495, \"height\": 296}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-3ombamuhjn/fig-009.webp\", \"caption\": \"\", \"page\": 15, \"index\": 9, \"width\": 480, \"height\": 302}]"
motivation: 现有域适应方法无法处理源域和目标域模态完全不同的情况。
method: 引入桥接域包含两种模态的未标记样本，采用双分支架构和特征一致性损失对齐跨模态表示。
result: 在语义分割任务上验证了跨模态迁移的有效性，但未涉及实体关系抽取。
conclusion: LSB框架为跨模态迁移提供了新思路，但应用场景不同。
---

## Abstract
Unsupervised domain adaptation (UDA) methods effectively bridge domain gaps but become struggled when the source and target domains belong to entirely distinct modalities. To address this limitation, we propose a novel setting called Heterogeneous-Modal Unsupervised Domain Adaptation (HMUDA), which enables knowledge transfer between completely different modalities by leveraging a bridge domain containing unlabeled samples from both modalities. 
To learn under the HMUDA setting, we propose Latent Space Bridging (LSB), a specialized framework designed for the semantic segmentation task. 
Specifically, LSB utilizes a dual-branch architecture, incorporating a feature consistency loss to align representations across modalities and a domain alignment loss to reduce discrepancies between class centroids across domains. 
Extensive experiments conducted on six benchmark datasets demonstrate that LSB achieves state-of-the-art performance.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：传统的无监督域适应（UDA）方法能够有效弥合域间差距，但假设源域和目标域属于相同模态。当源域（如2D图像）和目标域（如3D点云）属于完全不同的模态时，现有方法难以直接迁移知识。
- **核心问题**：如何在不依赖目标域标注的情况下，将知识从一种模态（如2D图像）迁移到另一种模态（如3D点云）？实际应用中，3D点云标注昂贵而2D图像标注相对容易，因此迫切需要跨模态的无监督知识迁移方案。
- **整体含义**：论文提出了一个全新的设置——**异质模态无监督域适应（HMUDA）**，并设计了一个名为**潜在空间桥接（LSB）**的框架来解决该问题，主要针对语义分割任务。

## 2. 论文提出的方法论

- **核心思想**：利用一个**桥接域**（bridge domain），其中包含未标注的、来自源模态和目标模态的成对样本（如同时包含2D图像和3D点云的数据）。通过桥接域作为媒介，桥接源域和目标域之间的模态差异。
- **技术架构**：双分支架构：
  - **源网络**（source network）：专为源模态（M1，如2D图像）设计，包含特征提取器 h(·) 和分类器 f(·)。
  - **目标网络**（target network）：专为目标模态（M2，如3D点云）设计，包含特征提取器 ϕ(·) 和分类器 g(·)。
- **关键技术细节**：
  1. **分割损失**：在源域上使用标准交叉熵损失（\(L^s_{seg}\)）训练源网络；在桥接域上使用教师模型（通过EMA更新）生成伪标签，然后用交叉熵损失（\(L^b_{seg}\)）训练目标网络。
  2. **特征一致性损失**（\(L^b_{con}\)）：将源网络和目标网络提取的特征通过可学习的投影（\(p_h, p_ϕ\)）映射到共享潜在空间，然后最小化它们之间的ℓ2距离，同时加入权重衰减正则化。
  3. **域对齐损失**（\(L_{ali}\)）：计算源域和目标域中每类的质心特征（基于伪标签），然后最小化类质心之间的余弦距离，从而减少域间差异。
  4. **联合目标函数**：L = Σ L^s_{seg} + λ_a L_{ali} + Σ ( L^b_{seg} + λ_c L^b_{con} )。
- **教师模型**：通过指数移动平均（EMA）从源网络参数更新，用于生成桥接域的伪标签。
- **理论分析**：提供了一个误差上界，说明目标域误差受源域误差、模态差异、域间差异等影响，而LSB的各损失项与之对应，为方法提供了理论支持。

## 3. 实验设计

- **数据集**：使用四个公开的多模态自动驾驶数据集：
  - nuScenes-lidarseg（分为USA和Singapore场景、Day和Night光照条件）
  - A2D2（奥迪自动驾驶数据集）
  - SemanticKITTI（简称Sem.）
  - VirtualKITTI（合成数据集，简称Virt.）
- **任务构造**：共构造**6个转移任务**，包括场景布局变化（USA→Sing.）、光照变化（Day→Night）、合成到真实（Virt.→A2D2, Virt.→Sem.）以及不同相机设置（Sem.→A2D2, A2D2→Sem.）。桥接域根据任务选择（Sem.、A2D2、Virt.）。
- **评估维度**：既进行了2D→3D的迁移，也进行了3D→2D的迁移。
- **对比方法**：
  - **Oracle**：目标域有标注的上界。
  - **xMUDA**：多模态UDA方法，视为软上界。
  - **Source-Only**：仅用源域训练源网络，然后用伪标签训练目标网络。
  - **PL（Pseudo-Labeling）**：两阶段伪标签方法。
  - **CDSPP**：异质域适应（HDA）方法，使用约5%的目标标注样本。
- **实现细节**：
  - 2D网络：U-Net + ResNet34（ImageNet预训练）
  - 3D网络：SparseConvNet + U-Net（体素大小5cm）
  - 投影层：线性层
  - 优化器：Adam，batch size=16，学习率0.001，训练50,000步，学习率调度器同xMUDA。
  - 超参数：α初值0.999，λ_w=0.01，λ_c=4.0，λ_a=0.1。

## 4. 资源与算力

- **文中明确提到**：所有实验均在一块**NVIDIA V100（32GB）GPU**上运行。
- **未说明**：没有提及训练总时长、不同任务的具体耗时或多GPU并行情况。因此，算力细节不完全，但可以推断实验规模中等（单卡V100，50,000步训练）。

## 5. 实验数量与充分性

- **实验数量**：
  - 主实验：6个转移任务 × 2个方向（2D→3D和3D→2D） = 12个结果（但在表格中展示为8个任务的结果，因为部分桥接域不同但仍可视为不同设置），每个设置报告mIoU。
  - 消融实验：
    - 不同损失组合（4组）在多个任务上测试。
    - 投影层变体（w/o p_h, w/o p_ϕ）在3个任务上测试。
    - 超参数敏感性：λ_c、λ_a、桥接域样本数量各一个任务。
    - 跨模态对齐位置对比（B vs T）在3个任务上测试。
    - 可视化：定性结果（图6）和t-SNE可视化（图7）。
- **充分性与公平性**：
  - 对比了多种基线（Oracle、xMUDA、Source-Only、PL、CDSPP），覆盖了上界、多模态UDA、传统HDA等方法。
  - 消融实验系统性地验证了每个组件的贡献。
  - 超参数敏感性分析较为详细，给出了合理范围。
  - 仍存在的不足：未在更多下游任务（如物体检测、分类）上验证；理论分析中假设的HΔH距离未实际计算；桥接域的选择是否通用未深入探讨。
- **总体评价**：实验设计较为充分，对比客观，但对手方法的配置（如CDSPP使用5%目标标注）与HMUDA的完全无监督设置略有差异，对比时已注明，较为公平。

## 6. 论文的主要结论与发现

- LSB在**所有2D→3D任务**（除Virt.→Sem.外）和**大多数3D→2D任务**上取得了最高mIoU，显著超越Source-Only、PL和CDSPP。
- 消融实验表明：特征一致性损失和域对齐损失均能有效提升性能，联合使用效果最佳。
- 投影层（p_h, p_ϕ）将特征映射到共享空间比直接在一方空间中对齐更有效。
- 桥接域样本数量达到500后性能趋于稳定，说明少量桥接数据即可支持有效迁移。
- 理论误差界为方法提供了理论保证，实验与理论一致。

## 7. 优点

- **问题新颖**：首次提出HMUDA设置，突破了传统UDA对同模态的依赖，牵引了跨模态无监督迁移的新方向。
- **方法设计简洁有效**：双分支架构+三种损失（分割、特征一致、域对齐）逻辑清晰，且与理论界对应。
- **实验全面**：覆盖了多种场景（城市布局、光照、合成→真实、不同传感器），并进行了正反向迁移（2D↔3D），验证了泛化性。
- **无需额外标注**：完全无监督（目标域），桥接域也无需标注，实用性强。
- **理论支撑**：给出了泛化误差上界，提供了理论解释。

## 8. 不足与局限

- **应用场景局限**：当前仅在语义分割任务上验证，未拓展到图像分类、物体检测等其他任务（作者已在未来工作中提及）。
- **桥接域依赖**：要求存在包含成对跨模态数据的桥接域，在某些场景下可能不易获取（尽管作者指出未标注数据易得）。
- **实验覆盖不完全**：
  - 未与更多最新的UDA/HDA方法（如对抗式、对比式方法）对比。
  - 理论分析中“误差间隙假设”和HΔH距离未在实际中量化。
  - 未进行跨数据集桥接域的泛化实验（如使用不同桥接域对同一任务的影响）。
- **计算资源单一**：仅使用单块V100 GPU，未考察多卡扩展性或更大模型下的表现。
- **偏差风险**：所有数据集均为自动驾驶场景，结果可能受限于特定领域，通用域适应能力未知。

（完）
