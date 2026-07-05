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

我是**杭州电子科技大学自动化（人工智能）学院控制工程专业**的硕士研究生，研究方向为多模态时序信号建模与解码。作为**学生作者**参与多篇 EEG 解码相关论文（**1 篇已发表 + 3 篇在审**），核心创新如下（点击可跳转至[论文页面](/publications/)）：

- [**PCMAN**](/publications/#gao2026pcman) · *Applied Soft Computing*（第二作者（导师一作），已发表）：提出**渐进式跨模态对齐网络**，以"物理 → 语义 → 任务"三层渐进机制融合 EEG 与 fNIRS——用滑动窗口建模血流动力学延迟、以 fNIRS 空间注意力增强 EEG，系统性缓解两种信号的时空异质性。
- [**PhysioSync**](/publications/#gao2026physiosync) · *IEEE T-AFFC*（第二作者（导师一作），大修已返修）：面向**连续情绪回归**，在多模态融合**之前**先做 **HRF 式神经血管对齐**（可学习双伽马核），并把对齐残差转化为**可靠性门控**抑制不可靠的血流动力学证据，配合线性复杂度 Mamba 编码长程 EEG。
- [**Neuro-SSCL**](/publications/#lu2026neurosscl) · *IEEE JBHI*（第二作者，初审中）：将**神经科学先验**（容积传导的局部空间相关 + 全局功能连接拓扑）注入**半监督对比学习**，并以谱自适应多尺度图对比与多域自适应，缓解跨被试 EEG 情绪识别的**标签稀缺**问题。
- [**AG-LRTD**](/publications/#wu2026aglrtd) · *IEEE TETCI*（第三作者，初审中）：提出**注意力引导的低秩张量分解**，把 MI-EEG 组织为"通道 × 时间 × 频带 × 试次"四阶张量，用卷积注意力引导张量积低秩分解，并以 tubal-rank 约束 + 残差稠密隐式正则兼顾判别力与**可解释性**。

除此之外，我主要从事**具身智能**方向的研究：曾在**简智新创**实习，担任灵巧手算法实习生（Dex 外骨骼摇操作 Retarget，密集接触任务 Retarget + RL Sim-to-Real）；**宇树科技**实习，担任算法实习生（基于 G1 人形的 loco-manipulation 的 HIL-RL）；**普渡机器人**实习（VLA 基座模型复现、自研本体适配、推理加速与人在环的机械臂真机强化学习后训练 RFT）；**安克创新**实习（模型部署、四足多模态数据产线、遥操作数据采集与 VLM 自动标注产线）；以及**西湖大学 CenBRAIN 实验室**实习（侵入式脑机接口的 sEEG 语音解码）。

我关注如何打通感知、语言与行动的闭环——构建能够“看见、理解并在物理世界中行动”的机器人与神经接口。

我**正在积极寻找 2027 年秋季入学的博士机会**，可在此下载我的 [简历（PDF）](/assets/pdf/cv_xiaoqi_luo.pdf)。
