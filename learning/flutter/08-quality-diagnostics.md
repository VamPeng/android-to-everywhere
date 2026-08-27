---
type: learning-module
area: Flutter
module: 08
status: planned
updated: 2026-08-27
---

# 08：测试、性能、可观测性、安全与故障定位

## 本章目标

能为 Flutter 项目建立可重复、可回归、可发布的质量闭环，并使用静态检查、测试、运行时观测和 DevTools 证据定位常见业务、渲染、插件和平台问题。

## 教学节点

1. Format、Analyzer、Lint、依赖/安全检查和 CI 阻断规则；
2. Dart 单元测试、Widget Test、Integration Test、覆盖率与测试分层；
3. Fake、依赖替换、状态/路由/缓存测试和关键路径回归；
4. Golden Test 的适用边界，以及 Semantics、对比度、触控尺寸和大字体测试；
5. Debug/Profile/Release 性能差异与 Flutter DevTools；
6. UI/Raster、帧预算、Janky Frame、Timeline 和渲染问题；
7. CPU、内存/GC、网络、启动、App Size 和主 isolate 阻塞分析；
8. 不必要重建、长列表、图片内存、动画和平台视图成本；
9. 分层日志、状态/导航/网络/原生日志、关联 ID 与脱敏；
10. Flutter 未捕获错误、Platform 错误、Crash、版本维度、Breadcrumb 和符号化；
11. 生产监控、关键业务指标、告警、灰度观察和回滚触发条件；
12. 密钥、Token、用户数据、权限、日志和依赖的安全/隐私检查；
13. Dart、Widget、插件、Engine、Android/iOS 的问题分层；
14. 复现、采证、假设、验证、根因、修复、回归和复盘。

## L0 概念门禁

- 能为静态检查、单元、Widget、集成、无障碍和性能测试划分职责；
- 能根据现象选择日志、测试、Timeline、CPU、Memory、Network、App Size 或原生工具；
- 能画出线上错误从版本/用户操作到 Crash、符号文件、根因和回滚的证据链。

## L1 引导实验

在既有项目中建立 format/analyze/test 门禁，加入脱敏状态日志、错误捕获和关键测试，再使用 DevTools 观察一次不必要重建、一次长任务阻塞、一次图片内存压力和一次启动/包体指标。

## L2 半开放任务

从以下故障池抽取至少三项；任务只提供现象、复现入口和验收条件，不提供根因：

- 一次无效或重复状态更新；
- 一次页面销毁后的异步回调；
- 一次布局或列表性能问题；
- 一次网络、缓存或序列化错误；
- 一次 Platform Channel 错误；
- 一次 Android/iOS 构建错误；
- 一次只有线上脱敏日志、Crash 或性能数据的未知问题。

## L3 综合实战

从主项目选择一个未知故障或隐藏故障分支，独立完成“现象 → 稳定复现 → 分层采证 → 假设排除 → 根因 → 最小修复 → 自动回归 → 发布/监控结论”，并将质量门禁接入 CI。

## 交付物与验收

- format/analyze/依赖检查、单元、Widget 和关键流程测试；
- DevTools 截图或性能数据；
- 分层脱敏日志、Crash/符号化或生产观测样例；
- 无障碍检查和安全/隐私清单；
- 至少一份完整故障案例：现象 → 复现 → 证据 → 根因 → 修复 → 回归；
- 能在未知问题出现时先判断所属层级，再选择证据工具。

完成本章后，依据 [[../../skills/flutter|Flutter 领域]] 的中级标准进行综合验收，不能仅凭章节阅读记录升级能力。
