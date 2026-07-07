---
layout: page
title: 简智新创（Genrobot.ai）— 灵巧手算法
description: 自研 Dex 遥操 / 控制适配（DexPilot / Key-Objectives / Topo Retarget + SDK）与密集接触手内操作的 RL Sim-to-Real
img: assets/img/logo_genrobot.png
importance: 1
category: 工作
related_publications: false
---

2026.06 – 2026.09 在**简智新创（Genrobot.ai）**担任**灵巧手算法实习生**，围绕灵巧手遥操作 Retarget 与密集接触手内操作的强化学习 Sim-to-Real 开展工作。

## 自研 Dex 遥操 / 控制适配（Retarget）
目标：让自研 Dex 手套**高精度、低延时**地遥操机械手，支持手机端 App 遥操，并采集高质量数据用于强化 / 模仿学习。以 **DexPilot** 为 baseline，在 **DexYCB** 上做离线 retargeting 误差与实时仿真评测（指尖误差、关节角误差、手-物碰撞、轨迹平滑性），实现 **Dex 外骨骼 / 动捕 / 视觉输入 → Wuji Hand2 20-DoF 关节轨迹**的稳定映射。

<div class="row justify-content-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_dex_sim21.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">人手 21 关键点 → Wuji Hand2 的仿真 retarget 可视化。</div>

### Key-Objectives Retargeting（DexPilot V2）
用**多目标重定向**替换 DexPilot 的目标函数，显式建模整体手型、指尖相对关系、指尖方向、掌心姿态、关节正则与速度平滑等关键目标。相较 V1（DexYCB 评测）：

- **指尖方向误差 ↓27.6%**（mean）、对指（thumb 相对）误差 ↓10.3%；
- 关节速度 / 加速度 / jerk 的 mean 与 P95 **均 ↓约 10%**（更平滑、更机械友好）；
- 关节 near-limit 率 **↓65.2%**（安全性提升），实时性 P95 仍在 30 Hz 帧预算内。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_dex_retarget_compare.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">DexPilot V1（左）vs Key-Objectives Retargeting V2（右）多视角对比。</div>

### Topo Retargeting 与实时性优化
引入 **Topo 重定向**进一步把**指尖全局误差从 0.99 cm 降到 0.57 cm**；针对其高延迟做了一系列工程优化——Jacobian 加速（约 **1633 ms → 112 ms/帧**）、warm-start gate、Laplacian 向量化、solver 重构与 verified fast path、residual/Jacobian 热路径压缩，**端到端时延 mean 28.4 → 21.3 ms**（满足 30 Hz 实时控制）。

### SDK 工程交付与真机遥操
补充 SDK 左右手支持，并用 **C 重新实现原 Python SDK 逻辑**（Android SDK / Flutter），与 Python 版精度基本一致、**Apple M5 双手串行 mean 8.3 ms**；打通 **Dex 真机 → sim**（磁编码器 raw 数据后处理、量纲统一与零位校准），推进 Wuji / 强脑机械手的真机遥操。

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_dex_mocap.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_dex_retarget.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">左：动捕（mocap）驱动的遥操；右：Dex 外骨骼遥操作实机演示。</div>

### 动捕数据采集与处理
搭建动捕（mocap）数据的采集与处理流程：多源动捕/手部关键点采集、时空对齐与坐标系变换、重定向到机械手关节轨迹，产出可用于模仿/强化学习的高质量演示数据。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_mocap_pipeline.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">动捕数据采集与处理 · 手部动作重定向到灵巧手的采集流程演示。</div>

## 密集接触任务 Retarget + RL Sim-to-Real
针对**转笔**等密集接触的手内操作任务：

- 保持人手-物体的**任务相关接触拓扑**，生成带**物体位姿**与**手部 21 keypoint** 的 reference 轨迹；
- 在 **Isaac Lab** 中通过 **reference-state initialization**、**residual joint-position action** 与 **PPO** 训练 tracking policy；
- 最终迁移到**真机**完成转笔任务。

## 演示：基于 pi0.5 的 SFT 策略
基于 **pi0.5** 进行监督微调（SFT）的策略实机演示。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_pi05_sft.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">基于 pi0.5 的 SFT 策略实机演示。</div>
