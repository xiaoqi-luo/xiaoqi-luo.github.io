---
layout: page
title: 普渡机器人 — VLA 基座模型
description: VLA 基座模型复现、自研本体适配、评测、推理加速与人在环真机 RL 后训练（RFT）
img: assets/img/logo_pudu.png
importance: 3
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

## HIL-SERL 真机强化学习复现（Franka 圆柱抓取-插孔）
复现 **HIL-SERL**（Human-in-the-Loop 样本高效强化学习）框架，在 **Franka** 机械臂上完成圆柱**抓取-插孔**任务的真机人在环训练：

- **圆柱插孔成功率 97/106（≈90%+）**，单任务训练总耗时约 2.5–3 h（60k+ 步）。
- 系统研究 **critic/actor 更新频率**、**人工干预时机与强度**对 Q 值收敛、熵坍塌与泛化的影响；发现"前期多给成功干预、正确引导 critic"是稳定收敛的关键。
- 关键结论：**人在环干预能有效提升成功率**——对未见情形只需多示教几次即可转为无需干预；**模型具备从失败中学习、二次尝试自主纠正**的能力。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/hilserl_insertion_demo.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">Franka 圆柱抓取-插孔 · HIL-SERL 真机演示（成功率 97/106，≈90%+）。</div>

### 泛化性对比实验
在其它孔位塞入圆柱/连接件、封孔、更换背景等干扰下测试策略泛化性：

<div class="row mt-2">
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_2holes.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>间隔两孔插入干扰柱 · ✅ 100%</small></p>
  </div>
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_thirdhole.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>封住第三孔 · ✅ 100%</small></p>
  </div>
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_horiz.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>隔壁槽横卡连接件 · ✅ 100%</small></p>
  </div>
</div>
<div class="row mt-2">
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_adjacent.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>目标隔壁孔放圆柱 · ❌ 0%</small></p>
  </div>
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_two_cyl.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>同时放绿、黄两柱 · ❌ 0%</small></p>
  </div>
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_vert.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>隔壁槽竖卡连接件 · ❌ 0%</small></p>
  </div>
</div>
<div class="row justify-content-center mt-2">
  <div class="col-md-4 mt-3">
    {% include video.liquid path="assets/video/hilserl_gen_bg.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
    <p class="text-center mt-1"><small>更换工作台背景 · ❌ 0%</small></p>
  </div>
</div>
<div class="caption">结论：仅当"第一个孔"（疑似被作为目标参考物）被干扰、或工作台背景改变时成功率显著下降；其余干扰下策略保持稳健。</div>
