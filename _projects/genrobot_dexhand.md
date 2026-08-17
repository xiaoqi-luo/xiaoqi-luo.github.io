---
layout: page
title: 简智新创 — 灵巧手与具身动作算法
description: HKT 异构重定向、Dex 遥操、Ego-SMPL 纯视觉跨本体控制、MANUS+VIVE 手—臂遥操作与 HORA Sim-to-Real
img: assets/img/logo_genrobot.png
brand_label: 简智新创
brand_accent: "#5B84E8"
brand_tint: "#EEF1FF"
importance: 1
category: 工作
related_publications: false
---

<style>
  .genrobot-method-note {
    margin: 1.15rem 0 1.5rem;
    padding: 1rem 1.1rem;
    border: 1px solid color-mix(in srgb, #5b84e8 24%, var(--global-divider-color));
    border-left: 3px solid #5b84e8;
    border-radius: 0.8rem;
    background: linear-gradient(135deg, #eef1ff 0%, var(--global-card-bg-color) 72%);
    box-shadow: 0 10px 26px rgb(35 55 95 / 6%);
  }

  .genrobot-method-kicker {
    display: block;
    margin-bottom: 0.55rem;
    color: #4f73cc;
    font-size: 0.75rem;
    font-weight: 750;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .genrobot-method-note p {
    margin-bottom: 0.75rem;
  }

  .genrobot-pipeline {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 0.38rem;
    color: var(--global-text-color-light);
    font-size: 0.82rem;
  }

  .genrobot-pipeline span {
    padding: 0.22rem 0.52rem;
    border: 1px solid color-mix(in srgb, #5b84e8 20%, var(--global-divider-color));
    border-radius: 0.4rem;
    background: color-mix(in srgb, #5b84e8 7%, var(--global-card-bg-color));
  }

  .genrobot-pipeline b {
    color: #5b84e8;
    font-weight: 700;
  }

  html[data-theme="dark"] .genrobot-method-note {
    background: linear-gradient(
      135deg,
      color-mix(in srgb, #5b84e8 13%, var(--global-card-bg-color)) 0%,
      var(--global-card-bg-color) 76%
    );
    box-shadow: 0 10px 26px rgb(0 0 0 / 22%);
  }
</style>

2026.06 – 2026.09 在**简智新创**担任**灵巧手算法实习生**，聚焦五条技术线：**HKT 异构外骨骼重定向**、**Dex 实时遥操与数据采集**、**Ego-SMPL 纯视觉跨本体控制**、**MANUS+VIVE 手—臂协同遥操作**，以及**密集接触手内操作的 RL Sim-to-Real**。

<span id="exofactor"></span>

## ExoFactor / HKT：异构外骨骼重定向

**ExoFactor: Geometry-Conditioned Cross-Attention for Calibration-Efficient Retargeting of Heterogeneous Hand Exoskeletons**（ICRA-27 在写）。

<div class="genrobot-method-note">
  <span class="genrobot-method-kicker">Method 01 · Heterogeneous Kinematics Transformer</span>
  <p>提出<strong>异构运动学 Transformer（HKT）</strong>：将不同外骨骼的 FK 编译为<strong>拓扑无关的几何 Token</strong>，通过几何条件化跨注意力学习“外骨骼—21 keypoints—灵巧手”的通用映射，支持面向不同机械拓扑的<strong>少样本快速标定</strong>与<strong>高精度遥操</strong>。</p>
  <div class="genrobot-pipeline" aria-label="HKT 方法流程">
    <span>外骨骼 FK</span><b>→</b><span>几何 Token</span><b>→</b><span>Cross-Attention</span><b>→</b><span>21 keypoints</span><b>→</b><span>多平台灵巧手</span>
  </div>
</div>

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_hkt_exoskeleton_retarget_protected.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">异构外骨骼动作到灵巧手的真机重定向与遥操演示（外骨骼结构已作马赛克保密处理）。</div>

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
    {% include video.liquid path="assets/video/genrobot_dex_retarget_protected.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">左：动捕（mocap）驱动的遥操；右：Dex 外骨骼遥操作实机演示（外骨骼结构已作马赛克保密处理）。</div>

### 动捕数据采集与处理

搭建动捕（mocap）数据的采集与处理流程：多源动捕/手部关键点采集、时空对齐与坐标系变换、重定向到机械手关节轨迹，产出可用于模仿/强化学习的高质量演示数据。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_mocap_pipeline.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">动捕数据采集与处理 · 手部动作重定向到灵巧手的采集流程演示。</div>

<span id="cross-embodiment"></span>

## Ego Motion → Cross-Embodiment Control

<div class="genrobot-method-note">
  <span class="genrobot-method-kicker">Method 02 · Unified SMPL Motion Control</span>
  <p>以<strong>人类第一视角 Ego 纯视觉数据</strong>输出的 <strong>SMPL 全身骨架与 Hand21 手部轨迹</strong>作为统一动作表示，使用固定会话坐标变换和相对根节点表征，避免逐帧刚体拟合带来的抖动与尺度漂移；再通过本体适配器将同一段动作分别映射至 <strong>Tianji + Wuji</strong> 与 <strong>Unitree G1</strong>。</p>
  <div class="genrobot-pipeline" aria-label="跨本体动作回放流程">
    <span>Ego MCAP</span><b>→</b><span>SMPL + Hand21</span><b>→</b><span>本体适配器</span><b>→</b><span>Tianji + Wuji</span><b>↔</b><span>Unitree G1 / SONIC</span>
  </div>
</div>

- **Tianji + Wuji**：将上肢运动与 Hand21 分别适配至 Tianji 双臂与 Wuji Hand2 的关节空间；
- **Unitree G1 / SONIC**：将 SMPL-22 扩展为 SMPL-24，并生成 6 维腕部参考，通过 ZMQ Mode-2 接入官方 GEAR-SONIC 编码器/解码器，输出 G1 29-DoF 动作；
- **同步控制**：仅依赖 Ego 纯视觉输入，在统一时间轴下驱动多台异构本体；完成 4,272 帧（85.42 s）闭环验证，ONNX 推理 P95 为 8.82 ms。

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_ego_tianji_wuji_real.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_ego_g1_sonic_real.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">左：Tianji + Wuji 实体平台；右：Ego 动作驱动的 Unitree G1 SONIC 实机演示。</div>

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_cross_embodiment_mujoco.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_ego_multiview_replay.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">左：Tianji + Wuji 与 G1 的 MuJoCo 同步回放；右：Ego 多视角轨迹复核与动作回放。</div>

<p><strong>当前能力：</strong>仅依赖 Ego 纯视觉输入的多本体同步控制。<strong>下一步：</strong>将当前链路进一步改造为实时流式回放，使同一 Ego 动作可低延时驱动多种具身本体。</p>

<span id="manus-vive-teleop"></span>

## MANUS + VIVE：手—臂协同真机遥操作

<div class="genrobot-method-note">
  <span class="genrobot-method-kicker">Method 03 · SE(3)-Referenced Hand–Arm Teleoperation</span>
  <p>构建手指与手臂<strong>解耦</strong>的双链路遥操作：MANUS 左手骨架经 Hand21 与 Wuji retargeting 驱动 <strong>Wuji Hand2</strong>；中心与左腕双 VIVE Tracker 以 <strong>90 Hz 相对 SE(3)</strong> 消除 SteamVR 世界坐标漂移，经 One-Euro 滤波、安装外参与手动零点的 <strong>1:1 末端映射</strong>驱动 <strong>Tianji 左臂</strong>。</p>
  <div class="genrobot-pipeline" aria-label="MANUS 与 VIVE 手臂协同遥操作流程">
    <span>MANUS Skeleton</span><b>→</b><span>Hand21</span><b>→</b><span>Wuji Hand2</span><b>｜</b><span>Dual VIVE SE(3)</span><b>→</b><span>Marvin IK</span><b>→</b><span>Tianji Arm</span>
  </div>
</div>

- **稳定控制语义**：仅在操作者显式捕获零点后开始手臂跟随；Tracker 短时失效、IK 无解或仿真重启均不会静默重置人机对应关系；
- **单一生产运动学链**：采用 Tianji Marvin SDK IK，以当前实测关节保持解的连续性；HL-IK 仅保留为历史实验资产，避免双重 IK 和冗余限幅带来的尾延迟；
- **低延时与可诊断性**：手、臂和仿真独立启停，端到端延迟控制在 **25 ms 以内**；完整记录 90 Hz Tracker、映射目标、IK 输出与实机反馈，便于逐层定位不跟手、漂移与可达域问题。

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_manus_vive_tianji_wuji_teleop.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">MANUS 左手与双 VIVE Tracker 协同驱动 Wuji Hand2 和 Tianji 左臂的实机演示。</div>

## 密集接触任务 Retarget + RL Sim-to-Real

针对**转笔**等密集接触的手内操作任务：

- 保持人手-物体的**任务相关接触拓扑**，生成带**物体位姿**与**手部 21 keypoint** 的 reference 轨迹；
- 在 **Isaac Lab** 中通过 **reference-state initialization**、**residual joint-position action** 与 **PPO** 训练 tracking policy；
- 最终迁移到**真机**完成转笔任务。

### 接触保持转笔（Retarget + Tracking）

<div class="row justify-content-center">
  <div class="col-sm-12 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_pen_spinning_sim.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">接触保持重定向与策略轨迹跟踪的双视角转笔仿真演示。</div>

### Revo3 右手 · HORA 转球（Sim-to-Real）

<div class="genrobot-method-note">
  <span class="genrobot-method-kicker">Method 04 · HORA Sim-to-Real</span>
  <p>搭建“<strong>Stage 1 特权信息条件化 PPO</strong> + <strong>Stage 2 ProprioAdapt 时序蒸馏</strong>”两阶段训练链路。Stage 1 在质量、摩擦、质心与 PD 响应随机化下学习条件控制策略；Stage 2 冻结 Actor，以本体历史预测动力学隐变量。</p>
  <p>针对无触觉 Revo3 真机定位并消除 <strong>contact observation mismatch</strong>，统一训练、ONNX 导出与真机部署的关节位置—目标历史输入；Stage 2 潜变量 MSE 由 <strong>0.47</strong> 收敛至 <strong>0.04–0.05</strong>，完成 Revo3 右手闭环部署与转球验证。</p>
  <div class="genrobot-pipeline" aria-label="HORA 训练与部署流程">
    <span>Privileged PPO</span><b>→</b><span>Dynamics Latent</span><b>→</b><span>ProprioAdapt</span><b>→</b><span>ONNX</span><b>→</b><span>Revo3 闭环</span>
  </div>
</div>

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_hora_revo3_sim.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_hora_revo3_real.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">左：Isaac 仿真中的 HORA 转球策略；右：Revo3 右手 ONNX 真机闭环与转球验证。</div>

## 演示：基于 pi0.5 的 SFT 策略

基于 **pi0.5** 进行监督微调（SFT）的策略实机演示。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/genrobot_pi05_sft.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">基于 pi0.5 的 SFT 策略实机演示。</div>
