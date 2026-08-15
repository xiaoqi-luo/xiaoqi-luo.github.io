---
layout: page
title: 宇树科技 — G1 人形 Loco-Manipulation
description: G1 人形 loco-manipulation · 人在环强化学习（HIL-RL）思路 + 全身遥操作数据采集系统（XR/PICO + WBC + 灵巧手 + MCAP）
img: assets/img/logo_unitree.png
brand_label: 宇树科技
brand_accent: "#17191C"
brand_tint: "#F2F0ED"
importance: 2
category: 工作
related_publications: false
---

2026.06 在**宇树科技**担任**算法实习生**（约一周），围绕 **G1 人形机器人**的 **loco-manipulation**（移动-操作一体），设计**人在环强化学习（HIL-RL）**后训练思路，并搭建配套的**全身遥操作数据采集系统**。

## 算法思路：人在环强化学习（HIL-RL）
面向 G1 人形的**接触密集 / 精细操作**任务，采用人在环的"部署 → 接管 → 后训练"闭环：

- 每条 episode 以策略**自主 rollout** 开始；当**接近失败**时，由操作者通过**全身 + 灵巧手遥操作**接管纠正；
- 将轨迹按 **rollout / 纠正（adaptation）/ 恢复（recovery）** 分阶段打标，并**保守设置失败边界**，避免把犹豫、低效的接管动作误标为高质量恢复；
- 以**价值 / 优势（advantage）估计**从混合质量轨迹中甄别高价值行为，使策略**聚焦高价值动作**而非无差别模仿全部接管数据，从而在多轮"部署—接管"迭代中稳定提升成功率与失败恢复能力。

## 全身遥操作数据采集系统
为支撑上述人在环采集，搭建了一套 **G1 全身遥操作 + 多模态同步录制** pipeline：

- **XR / PICO 三点遥操作**：读取 XR 头显与双手柄的 3 点位姿，结合 SMPL 人体关节估计映射到 G1 全身，驱动上肢末端位姿与身体朝向。
- **全身控制（WBC）**：基于 Unitree G1 `LocoClient` 与 FSM（遥操 / 行走模式切换），订阅 29 维关节角 + IMU 低层状态，做 yaw 连续化与末端位姿控制，实现移动与操作的协同。
- **Inspire 双手灵巧手**：接入灵巧手 SDK 遥操双手动作。
- **多相机图像服务**：多路相机采集与时间对齐。
- **MCAP 录制**：30 Hz 录制状态机（生命周期管理、坐标系变换、异步写入线程、暂停 / 恢复），产出 MCAP 轨迹并支持 meshcat 回放复核。

<div class="row justify-content-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    <img src="{{ '/assets/img/unitree_teleop_arch.svg' | relative_url }}" class="img-fluid rounded z-depth-1" alt="G1 全身遥操作数据采集系统架构" />
  </div>
</div>
<div class="caption">系统架构：XR/PICO 遥操 → SMPL 映射 → WBC 控制 → G1（低层状态反馈）；多相机与机器人状态经 30 Hz MCAP 录制，服务下游 HIL-RL 后训练。</div>

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/unitree_g1.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">宇树 G1 人形机器人 · loco-manipulation 策略推理实机演示。</div>
