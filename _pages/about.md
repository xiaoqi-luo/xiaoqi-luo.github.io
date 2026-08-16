---
layout: about
title: 关于
permalink: /
subtitle: 杭州电子科技大学 · 具身智能 / 多模态学习 / 脑机接口

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>控制工程 · 硕士在读</p>
    <p>自动化（人工智能）学院</p>
    <p>杭州电子科技大学</p>

selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

我是**杭州电子科技大学自动化（人工智能）学院控制工程专业**的硕士研究生，导师为**高云园教授**，研究方向为多模态时序信号建模与解码。作为**学生作者**参与多篇 EEG 解码相关论文（**1 篇已发表 + 6 篇在审**），代表性工作如下（完整列表见[论文页面](/publications/)）：

- [**NeuralIntent**](/publications/#luo2027neuralintent) · *AAAI-27*（第一作者，投稿在审，Submission 37074）：将非侵入式 EEG 对齐至 Qwen3-VL 中间语义空间，形成连续 **Neural Intent Token**，经校准桥与本体适配器接入 GR00T N1.7-DROID；提出 **EIG-Bench**，在多目标场景中解耦评估神经目标选择与机器人操作执行。
- [**PCMAN**](/publications/#gao2026pcman) · *Applied Soft Computing*（IF≈7.8 · JCR Q1 · 中科院计算机 2区 TOP；第二作者（导师一作），已发表）：提出**渐进式跨模态对齐网络**，以"物理 → 语义 → 任务"三层渐进机制融合 EEG 与 fNIRS——用滑动窗口建模血流动力学延迟、以 fNIRS 空间注意力增强 EEG，系统性缓解两种信号的时空异质性。
- [**PhysioSync**](/publications/#gao2026physiosync) · *IEEE T-AFFC*（IF≈9.8 · JCR Q1 · 中科院计算机 1区 TOP；第二作者（导师一作），小修返修在审）：面向**连续情绪回归**，在多模态融合**之前**先做 **HRF 式神经血管对齐**（可学习双伽马核），并把对齐残差转化为**可靠性门控**抑制不可靠的血流动力学证据，配合线性复杂度 Mamba 编码长程 EEG。

此外，拥有**发明专利 3 项**：作为第一发明人的神经血管耦合对齐与残差可靠性融合脑电近红外情绪回归方法，以及两项处于初稿审核阶段的 AI 策略计算平台专利；并拥有软件著作权一项（大宗商品 AI 分析系统 V1.0，登记号 2026SR0328287）。详见[简历](/cv/)。

除此之外，我主要从事**具身智能**方向的研究（点击单位名可跳转对应[项目](/projects/)）：曾在 [**简智新创**](/projects/genrobot_dexhand/) 实习，担任灵巧手算法实习生，覆盖 HKT 异构外骨骼重定向、Ego-SMPL 跨本体回放、MANUS+VIVE 手—臂协同遥操作与接触式手内操作 Sim-to-Real；[**宇树科技**](/projects/unitree_g1/) 实习，开展基于 G1 人形的 loco-manipulation 人在环强化学习；[**普渡机器人**](/projects/pudu_vla/) 实习，开展 VLA 基座模型复现、自研本体适配、推理加速与人在环机械臂真机强化学习后训练；[**安克创新**](/projects/anker_embodied/) 实习，开展模型部署、四足多模态数据产线、遥操作数据采集与 VLM 自动标注产线；以及 [**西湖大学 CenBRAIN 实验室**](/projects/cenbrain_ibci/) 实习，开展侵入式脑机接口的 sEEG 语音解码。

我关注如何打通感知、语言与行动的闭环——构建能够“看见、理解并在物理世界中行动”的机器人与神经接口。

我**正在积极寻找 2027 年秋季入学的博士机会**，可在此下载我的 [简历（PDF）](/assets/pdf/cv_xiaoqi_luo.pdf)。
