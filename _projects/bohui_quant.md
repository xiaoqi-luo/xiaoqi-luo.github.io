---
layout: page
title: 原油市场数据与智能投研平台
description: 多资产行情数据、低延迟流式链路与 DAG 策略编排
img: assets/img/4.jpg # TODO: 替换为仪表盘 / 架构图真实截图
importance: 4
category: 工作
related_publications: false
---

2025.10 – 2026.04 为**宁波博汇化工科技股份有限公司**做后端开发，建设原油市场数据与 AI 量化策略投研平台。

## AI 量化策略工作台
使用 **Codex** 与 **Claude Code** 设计工作台，构建策略因子 **Workflow** 与 **DAG 可视化编排**，接入交易所实时行情，搭建 **CTP → Kafka → ClickHouse** 低延迟流式链路。

## 多资产行情与回测数据链路
接入 **FMP**、**TradingView**、**PostgreSQL hot DB**、**OSS 历史归档**与实时指标服务，覆盖**期货、美股、A股**；设计**主站 + Mac worker + OSS** 架构，将计算任务从主链路解耦。
