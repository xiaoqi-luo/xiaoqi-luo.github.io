---
layout: page
permalink: /cv/
title: 简历
nav: true
nav_order: 3
description: 罗骁齐的简历 — 教育、实习、项目、论文与技能。
toc:
  sidebar: left
---

<div class="text-right">
  <a href="/assets/pdf/cv_xiaoqi_luo.pdf" class="btn btn-sm btn-outline-primary" target="_blank">下载简历 PDF</a>
</div>

# 罗骁齐 {#top}

**控制工程 · 硕士在读** ｜ 杭州 ｜ 2496998324@qq.com ｜ (+86)132-3796-1369

研究方向：多模态时序信号建模与解码、视觉-语言-动作（VLA）模型、具身智能、脑机接口

---

## 教育经历

### 杭州电子科技大学 — 硕士研究生 ｜ 2024.09 – 至今
自动化（人工智能）学院 · 控制工程 ｜ **GPA 4.05/4.5** ｜ 导师：**高云园 教授**

- 研究方向：多模态时序信号建模与解码、视觉—语言—动作模型及具身智能。
- 已发表/接收 SCI 论文 2 篇；以第一作者投稿 *AAAI-27* 的 NeuralIntent，另有 ExoFactor（ICRA-27）在写。
- 获学院羽毛球男子单打第一。

### 华东交通大学 — 工学学士 ｜ 2020.09 – 2024.06
电气与自动化工程学院 · 自动化 ｜ **GPA 3.34/4.0（专业前 30%）**

- 多次获得学业奖学金。

---

## 实习经历

### 简智新创（Genrobot.ai）— 灵巧手算法实习生 ｜ 2026.06 – 2026.09
围绕灵巧手遥操作、异构运动重定向、跨本体动作回放与密集接触手内操作的 RL Sim-to-Real 开展工作。

- **ExoFactor / HKT 异构外骨骼重定向**：将异构外骨骼 FK 编译为拓扑无关的几何 Token，以几何条件化跨注意力学习“外骨骼—21 keypoints—灵巧手”通用映射，支持少样本快速标定与高精度遥操作。
- **接触保持 Retarget + RL Sim-to-Real**：针对转笔等密集接触任务保持手—物接触拓扑，生成物体位姿与 Hand21 参考轨迹；在 Isaac Lab 中以 reference-state initialization、residual joint-position action 与 PPO 训练 tracking policy，完成 Wuji Hand2 迁移验证；并在 Revo3 上完成 HORA 两阶段策略的真机手内转球部署。
- **Ego 动作跨本体控制**：将人类第一视角 Ego 数据输出的 SMPL 骨架与 Hand21 统一重定向至 Tianji–Wuji 与 Unitree G1（SONIC）等异构本体，仅依赖 Ego 纯视觉输入完成多本体同步控制。
- **MANUS+VIVE 手—臂协同遥操作**：以 MANUS 驱动 Wuji Hand2，双 VIVE Tracker 经相对 SE(3)、零点 1:1 映射与 One-Euro 滤波驱动 Tianji 左臂；接入 Marvin SDK IK 实现协同真机遥操作，端到端延迟控制在 **25 ms 以内**。

### 宇树科技 — 人形算法实习生 ｜ 2026.06（约一周）
基于 **G1 人形机器人**的 **loco-manipulation**（移动-操作一体）开展**人在环强化学习（HIL-RL）**：协同下半身运动控制与上半身抓取，通过人在环迭代提升策略在真机上的稳定性与任务成功率。

### 普渡机器人 — VLA 算法实习生 ｜ 2026.03 – 2026.06
为自研轮式双臂机器人开展视觉-语言-动作基座模型的复现、适配、评测、推理加速与强化学习后训练。

- **模型复现与本体适配**：复现并部署 GR00T-N1.5，面向自研轮式双臂平台的搬箱任务完成数据 SFT、动作空间适配与推理配置开发。
- **自研基模 RoboChallenge 评测**：打通官方评测链路，部署自研基模 HTTP 推理服务、ClientAPI 对接与本地 Mock 闭环，实现 20 维模型动作到 Franka 控制接口的映射，在 Table 30 上微调。
- **推理速度优化**：参考 Realtime-VLA，用 CUDA Graph 消除 CPU 调度开销，客户端预 resize、图像编解码 WebP95→JPEG90、通信 WebSocket→ZMQ，端到端单轮推理时延降低约 50ms。
- **RL 后训练**：在 FlowerVLA SFT 权重后接 ConRFT 强化学习微调，设计 HIL 人在环路（SFT→离线 RL→在线 RL）流程，结合 BC 与 Q-learning 双重 loss、人类干预与稀疏奖励，构建 reward model 与真机 rollout 评测闭环，显著提升抓取/推动任务成功率与错误恢复能力。

### 安克创新 — 具身闭环算法实习生 ｜ 2025.10 – 2026.03
负责 VLA 模型部署、四足机器狗多模态数据产线、机械臂数据采集与 VLM 自动标注工具链。

- **VLA 复现与验证**：复现 ACT、pi0.5 与 Diffusion Policy，完成 Franka 方块插入凹槽端到端验证；将 InternVLA-N1 以 client/server 架构部署至 Unitree Go2，RTX 4090 运行 HTTP 推理 server，Jetson Orin 部署 D435i 采集与 ROS2/UDP 控制桥接，经局域网 HTTP 回传轨迹实现语言指令导航。
- **四足多模态数据产线**：构建 8 路传感器时空对齐链路，完成三路 LiDAR 外参标定、坐标系变换与点云融合，以及 5 路鱼眼相机标定去畸变；在 Kubernetes 上部署 MCAP 切片/解包/对齐服务并通过任务队列异步调度，累计处理数十 TB 原始数据。
- **机械臂数据采集**：搭建 UMI 与 teleop 数据采集 pipeline，覆盖局域网组网、NTP 时钟同步、站点接收上传、rerun 回放、多模态对齐与 WebDataset/lerobot 格式转换；调研数据质量评估方法，设计 5 维端侧质量规则校验与云端湖仓打分算法。
- **VLM 预标注与工具链**：搭建基于 Qwen-VL 与 GroundingDINO 的视频理解数据生产链路，通过 vLLM 高并发推理、多机并行与队列负载均衡，将端到端生产吞吐提升约 30%。

### 西湖大学 CenBRAIN 实验室 — 算法实习生 ｜ 2025.06 – 2025.09
侵入式脑机接口语音解码。

- 搭建临床 sEEG 数据采集与预处理流水线：低通滤波、工频陷波、下采样、通道选择与差分参考；基于 MFA、pyPinyin 与 IPA 映射生成字级时间边界及声母/韵母/声调标签。
- 设计声学启发的分层解码架构：以共享 1D-CNN/RNN 时序骨干编码 C×T sEEG 片段，训练 Initial、Tone、Final 三路解码器，通过 Beam Search、pinyin-to-char 映射与 LLM 重排序恢复句子级中文输出。

---

## 论文

- **Xiaoqi Luo（第一作者）**, Weixiang Gao, Zhengnan Zhang, Taojie Xu, Mo Zhou, Xun Shi, Yunyuan Gao. "[NeuralIntent: Bridging Noninvasive EEG and Embodied Foundation Models with Continuous Neural Intent Tokens](https://openreview.net/forum?id=HD4GoLhMkq)." *The Forty-First AAAI Conference on Artificial Intelligence (AAAI-27)*（**投稿在审 / Under Review**，Submission 37074）。框架 **NeuralIntent**；基准 **EIG-Bench**。
- [Yunyuan Gao（高云园，导师）](https://scholar.google.com/citations?user=fYI7Ic4AAAAJ), **Xiaoqi Luo（第二作者（导师一作））**, Zhengnan Zhang, Xu Shao, Yanhua Qin. "Progressive Cross-Modal Attention Network for Brain–Computer Interface Decoding Using EEG and fNIRS." *Applied Soft Computing*, **199C (2026) 115318**（IF≈7.8 · JCR Q1 · 中科院计算机 2区 TOP）。2026-04-24 接收，2026-06-05 online。[doi:10.1016/j.asoc.2026.115318](https://doi.org/10.1016/j.asoc.2026.115318)。框架 **PCMAN**。
- [Yunyuan Gao（高云园，导师）](https://scholar.google.com/citations?user=fYI7Ic4AAAAJ), **Xiaoqi Luo（第二作者（导师一作））**, Zhengnan Zhang, Jiangwen Lu, Yingchun Zhang, Ruyue Huang. "Neurovascular Alignment and Reliability-Aware Fusion for Continuous EEG–fNIRS Emotion Regression." *IEEE Transactions on Affective Computing*（IF≈9.8 · JCR Q1 · 中科院计算机 1区 TOP；**已接收 / Accepted，2026-08-19**）。框架 **PhysioSync**。
- Zheng Hu, **Xiaoqi Luo（第二作者）**, Xu Shao, [Yunyuan Gao（高云园，导师；通讯作者）](https://scholar.google.com/citations?user=fYI7Ic4AAAAJ), Yanhua Qin. "PSSF: A Phase-Space and State-Space Fusion Method for EEG Source Localization and Feature Decoding." *Journal of Neural Engineering*（IF≈4.0 · JCR Q2；**在审 / Under Review**，JNE-111255）。框架 **PSSF**。
- Jiangwen Lu, **Xiaoqi Luo（第二作者）**, Weixiang Gao, Ruyue Huang, Yunyuan Gao. "Neuro-SSCL: A Neuro-Aware Semi-Supervised Contrastive Learning for Cross-Subject EEG Emotion Recognition." *IEEE Journal of Biomedical and Health Informatics*（IF≈6.8 · JCR Q1 · 中科院医学 2区 TOP；**在审 / Under Review**）。框架 **Neuro-SSCL**。
- Xiao Wu, Weixiang Gao, **Xiaoqi Luo（第三作者）**, Zhengnan Zhang, Yunyuan Gao. "Attention-Guided Low-Rank Tensor Decomposition for Feature Analysis of MI-EEG Signals." *IEEE Transactions on Emerging Topics in Computational Intelligence*（IF≈6.5 · JCR Q1 · 中科院计算机 2区；**在审 / Under Review**）。框架 **AG-LRTD**。
- Weixiang Gao, Yunyuan Gao, **Xiaoqi Luo（第三作者）**, Jiangwen Lu, Zhengnan Zhang, Mo Zhou. "[MSPhys-Diff: Diffusion with Multiscale Physiological Priors for Parkinson's Disease EEG Generation](https://openreview.net/forum?id=dxKopG7EeG)." *The Forty-First AAAI Conference on Artificial Intelligence (AAAI-27)*（**投稿在审 / Under Review**，Submission 46558）。框架 **MSPhys-Diff**。

---

## 专利与软著

- **发明专利（申请中）· 第一发明人**：一种基于神经血管耦合对齐与残差可靠性融合的脑电近红外情绪回归方法及系统。发明人：**罗骁齐**、高伟翔、张政楠、高旭东、高云园、席旭刚、黄如月；申请人：杭州电子科技大学。（对应 **PhysioSync** 工作）
- **发明专利（初稿审核中）**：一种多源策略信号标准化版本化快照与因子复用方法及系统。
- **发明专利（初稿审核中）**：一种策略计算任务的质量门禁异步调度与结果快照同步方法及系统。
- **计算机软件著作权**：大宗商品 AI 分析系统 V1.0。著作权人：冯景禧、**罗骁齐**、蒙奕钢；登记号 2026SR0328287（软著登字第 17542568 号），2026-02。

---

## 技术能力

- **Embodied AI / VLA**：GR00T, π0.5, OpenPI, LeRobot, LIBERO, PPO, SAC；具备 SFT、离线/在线 RL、人类在环训练、价值评估与奖励建模经验。
- **Robotics / Teleoperation**：ROS2, Isaac Lab, MuJoCo、重定向；具备 MANUS、VIVE、灵巧手与外骨骼的手—臂协同遥操作及 Sim-to-Real 经验，覆盖 Unitree G1/Go2、Franka、Tianji、Wuji Hand2、Revo3 等本体。
- **Inference / Deployment**：Python, PyTorch, OpenCV, ONNX, CUDA Graph, vLLM, FastAPI；具备模型服务化、Client/Server 部署、ROS2 控制与实时推理优化经验。
- **Data / Infrastructure**：MCAP, WebDataset, Parquet, Rerun, Docker, Kubernetes, Redis, PostgreSQL, Git/CI/CD；具备多模态数据对齐、轨迹回放与异步流水线建设经验。

---

## 语言

- 中文（母语） ｜ 英文（专业工作水平）
