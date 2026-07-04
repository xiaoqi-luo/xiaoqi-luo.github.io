---
layout: page
title: 西湖大学 CenBRAIN — 侵入式脑机接口语音解码
description: 基于 sEEG 的侵入式脑机接口中文语音解码
img: assets/img/logo_cenbrain.png
importance: 3
category: 研究
related_publications: false
---

2025.06 – 2025.09 在**西湖大学 CenBRAIN 实验室**担任**算法工程师实习生**，从事**侵入式脑机接口（iBCI）语音解码**，基于临床 sEEG 信号实现中文句子级输出。

## sEEG 数据采集与预处理
搭建临床 sEEG 数据流水线：
- 低通滤波、工频陷波、下采样
- 通道选择与差分参考
- 基于 **MFA**、**pyPinyin** 与 **IPA** 映射生成字级时间边界及**声母 / 韵母 / 声调**标签

## 声学启发的分层解码架构
设计面向中文句子解码的分层架构：
- 共享 **1D-CNN / RNN** 时序骨干编码 `C × T` sEEG 片段
- **Initial、Tone、Final** 三路并行解码器
- 通过 **Beam Search**、**pinyin-to-char** 映射与 **LLM 重排序**恢复句子级中文输出

## 演示
侵入式脑机接口语音解码演示。

<div class="row justify-content-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include video.liquid path="assets/video/cenbrain_ibci.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
  </div>
</div>
<div class="caption">西湖大学 CenBRAIN 实验室 · 侵入式脑机接口语音解码演示。</div>
