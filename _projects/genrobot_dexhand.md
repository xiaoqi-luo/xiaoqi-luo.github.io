---
layout: page
title: 简智新创（Genrobot.ai）— 灵巧手算法
description: Dex 外骨骼遥操作 Retarget 与接触式手内操作的 RL Sim-to-Real
img: assets/img/genrobot.jpg # TODO: 替换为灵巧手 / 转笔任务真实效果图
importance: 0
category: 工作
related_publications: false
---

2026.06 – 2026.09 在**简智新创（Genrobot.ai）**担任**灵巧手算法实习生**，围绕灵巧手遥操作 Retarget 与接触式手内操作的强化学习 Sim-to-Real 开展工作。

## Dex 外骨骼遥操作 Retarget
基于 **DexPilot** 算法改进实时 retarget 框架：在机器人手可执行约束下，自适应选择**整体手型、指尖相对关系、指尖方向、掌心姿态、关节正则与速度平滑**等关键目标，实现 **Dex 外骨骼 / 动捕 / 视觉输入 → Wuji Hand2 20-DoF 关节轨迹**的稳定映射。

## 接触 Retarget + RL Sim-to-Real
针对**转笔**等存在物体接触的手内操作任务：

- 保持人手-物体的**任务相关接触拓扑**，生成带**物体位姿**与**手部 21 keypoint** 的 reference 轨迹；
- 在 **Isaac Lab** 中通过 **reference-state initialization**、**residual joint-position action** 与 **PPO** 训练 tracking policy；
- 最终迁移到**真机**完成转笔任务。
