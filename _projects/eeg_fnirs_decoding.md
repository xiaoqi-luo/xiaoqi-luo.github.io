---
layout: page
title: EEG–fNIRS 多模态脑信号解码
description: 硕士主研方向 · EEG–fNIRS 多模态解码（PCMAN 已发表 / PhysioSync 在审）
img: assets/img/research_pcman.png
importance: 0
category: 研究
related_publications: true
---

我的硕士主研方向是 **EEG–fNIRS 混合脑机接口的多模态解码**：EEG 具有毫秒级时间分辨率但空间定位有限，fNIRS 空间分辨率更好但存在数秒的血流动力学延迟。二者互补，但直接融合常因**电生理信号与血流动力学信号之间的时空异质性**而失效。围绕这一问题，我作为**第二作者（学生作者）**参与两项工作：一篇已发表于 *Applied Soft Computing*（IF≈6.6），另一篇投稿 *IEEE Transactions on Affective Computing*（大修已返修，在审）。

---

## 工作一：PCMAN — 渐进式跨模态对齐网络（Applied Soft Computing 2026）

针对时空异质性，提出 **渐进式跨模态对齐网络（PCMAN）**，通过三层渐进机制实现 EEG–fNIRS 的深度融合与对齐：

- **物理对齐**：时空相关动态融合框架（SDF），用滑动窗口捕捉血流动力学延迟，并以 fNIRS 驱动的空间注意力增强 EEG 特征。
- **语义对齐**：多维特征增强注意力网络（MDFEA），在保留低层线索的同时学习深层跨模态表示。
- **任务对齐**：跨模态自适应解码网络（CADN），基于前两层进行上下文感知融合与策略自适应。

在心算（MA）、词语生成（WG）、运动想象（MI）三类认知任务上分别取得 **88.18% / 81.93% / 72.94%** 的准确率，优于当时 SOTA 的混合 BCI 方法 {% cite gao2026pcman %}。

<div class="row">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/research_pcman.png" title="PCMAN 整体框架" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">PCMAN 整体框架：物理对齐 → 语义对齐 → 任务对齐 的三层渐进式跨模态融合。</div>

<div class="row">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/research_paradigm.png" title="实验范式与传感器布局" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/research_pcman_results.png" title="三任务性能对比" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">左：实验范式与 EEG/fNIRS 传感器布局；右：三类认知任务上的性能对比。</div>

---

## 工作二：PhysioSync — 神经血管对齐与可靠性感知融合（投稿 IEEE T-AFFC · 大修已返修/在审）

面向**连续情绪回归**（闭环情感脑机接口场景），提出 **PhysioSync**：在多模态融合之前，先做 HRF 式时间对齐与残差感知的可靠性控制。

- **DGamma-HRF-NVC**：可学习双伽马核，将 EEG 驱动通过有限窗因果卷积映射到 fNIRS 时间轴，建模神经血管耦合（NVC）导致的、随被试与脑区变化的延迟。
- **可靠性感知融合**：将对齐残差转化为跨模态一致性线索，在融合时自适应地选取可靠的 fNIRS 证据、抑制局部不可靠成分。
- **线性复杂度 Mamba 编码器**：高效建模高采样率 EEG 的长程上下文。

在 32 被试 REFED 的被试内 3 折基准上，平均 MAE 相较最优融合基线降低 **6.1%**、相较仅用 EEG 降低 **7.5%**，并在 1–3 秒轨迹预测中呈现更小的误差累积 {% cite gao2026physiosync %}。

<div class="row">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/research_physiosync.png" title="PhysioSync 总体框架" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">PhysioSync 总体框架：模态投影与 Mamba 编码 → HRF 式对齐（DGamma-HRF-NVC）→ 可靠性感知融合 → 双任务预测头。</div>

<div class="row">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/research_physiosync_align.png" title="神经血管时间对齐" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">HRF 式时间对齐：将 EEG 驱动映射到 fNIRS 血流动力学时间轴，并将对齐残差作为下游融合的可靠性线索。</div>

---

相关论文详见 [论文页面](/publications/)，可在线阅读摘要并下载 PDF。
