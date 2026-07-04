---
layout: page
title: 普渡机器人 — VLA 基座模型
description: 模型复现与本体适配、评测、推理加速与强化学习后训练
img: assets/img/logo_pudu.png
importance: 1
category: 工作
related_publications: false
---

2026.03 – 2026.06 在**普渡机器人**担任 **VLA 算法实习生**，围绕自研轮式双臂机器人开展视觉-语言-动作基座模型的复现、适配、评测、推理加速与强化学习后训练，共四条工作线。

## 模型复现与本体适配
复现 **GR00T-N1**、**DM0**，基于自研轮式双臂本体的搬箱子和生产任务数据做 SFT，适配动作表征与 infer config，并记录训练踩坑与效果归因。

## 自研基模 RoboChallenge 评测
打通官方 **RoboChallenge** 评测链路：部署自研基模 HTTP 推理服务、ClientAPI 对接与本地 Mock 闭环，实现 **20 维模型动作 → Franka 控制接口**的映射，并在 Table 30 上微调。

## 推理速度优化
参考 **Realtime-VLA** 优化端到端在线推理：
- **CUDA Graph** 消除 CPU 调度开销
- 客户端预 resize、图像编解码 **WebP95 → JPEG90**
- 通信 **WebSocket → ZMQ**

效果：端到端单轮推理时延降低约 **50ms**。

## RL 后训练
在 FlowerVLA SFT 权重后接 **ConRFT** 强化学习微调，设计人在环路流程（**SFT → 离线 RL → 在线 RL**），结合 BC 与 Q-learning 双重 loss、人类干预与稀疏奖励，构建 reward model 与真机 rollout 评测闭环，显著提升抓取/推动任务成功率与错误恢复能力。

## 演示：宇树 G1（基于 GR00T）
在宇树 G1 人形机器人上基于 GR00T 进行策略推理的实机演示。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/pudu_g1_groot.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">宇树 G1 · 基于 GR00T 的策略推理实机演示。</div>
