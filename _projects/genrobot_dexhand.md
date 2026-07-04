---
layout: page
title: 简智新创（Genrobot.ai）— 灵巧手算法
description: Dex 外骨骼遥操作 Retarget 与接触式手内操作的 RL Sim-to-Real
img: assets/img/logo_genrobot.png
importance: 0
category: 工作
related_publications: false
---

2026.06 – 2026.09 在**简智新创（Genrobot.ai）**担任**灵巧手算法实习生**，围绕灵巧手遥操作 Retarget 与接触式手内操作的强化学习 Sim-to-Real 开展工作。

## Dex 外骨骼遥操作 Retarget
基于 **DexPilot** 算法改进实时 retarget 框架：在机器人手可执行约束下，自适应选择**整体手型、指尖相对关系、指尖方向、掌心姿态、关节正则与速度平滑**等关键目标，实现 **Dex 外骨骼 / 动捕 / 视觉输入 → Wuji Hand2 20-DoF 关节轨迹**的稳定映射。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_dex_retarget.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">Dex 外骨骼遥操作 Retarget 实机演示。</div>

## 接触 Retarget + RL Sim-to-Real
针对**转笔**等存在物体接触的手内操作任务：

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
