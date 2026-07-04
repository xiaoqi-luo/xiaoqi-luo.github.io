---
layout: page
title: 安克创新 — 具身闭环
description: 四足 VLA 部署、多模态数据产线、遥操作采集与 VLM 自动标注
img: assets/img/2.jpg # TODO: 替换为 Go2 / 机械臂采集场景真实效果图
importance: 2
category: 工作
related_publications: false
---

2025.10 – 2026.03 在**安克创新**担任**具身闭环算法实习生**，负责 VLA 模型部署、四足机器狗多模态数据产线、机械臂数据采集与 VLM 自动标注工具链。

## VLA 复现与验证
复现 **ACT**、**pi0.5**、**Diffusion Policy**，完成 **Franka 方块插入凹槽**端到端验证；将 **InternVLA-N1** 以 client/server 架构部署至 **Unitree Go2**：
- **RTX 4090** 侧：运行 HTTP 推理 server
- **Jetson Orin** 侧：部署 D435i 采集与 ROS2/UDP 控制桥接
- 经局域网 HTTP 回传轨迹，实现语言指令导航

## 四足多模态数据产线
构建 **8 路传感器时空对齐**链路：
- 三路 LiDAR 外参标定、坐标系变换与点云融合
- 5 路鱼眼相机标定去畸变
- 在 Kubernetes 上部署 MCAP 切片/解包/对齐服务并通过任务队列异步调度

累计处理**数十 TB** 原始机器人数据。

## 机械臂数据采集
搭建 **UMI 与 teleop** 数据采集 pipeline，覆盖局域网组网、NTP 时钟同步、站点接收上传、**rerun** 回放、多模态对齐与 **WebDataset/lerobot** 格式转换；调研数据质量评估方法，设计 **5 维端侧质量规则校验**与云端湖仓打分算法。

## VLM 预标注与工具链
搭建基于 **Qwen-VL 与 GroundingDINO** 的视频理解数据生产链路（场景描述、目标定位、区域标注），通过 **vLLM** 高并发推理、多机并行与队列负载均衡，将端到端生产吞吐提升约 **30%**。

## 演示：InternVLA-N1 推理部署
InternVLA-N1 的推理部署与实机运行演示。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/anker_internvla.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">InternVLA-N1 推理部署实机演示。</div>
