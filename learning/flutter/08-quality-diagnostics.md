---
type: learning-module
area: Flutter
module: 08
status: planned
updated: 2026-08-26
---

# 08：性能、日志、测试与问题定位

## 本章目标

能为 Flutter 项目建立基本质量闭环，并使用日志、测试和 DevTools 证据定位常见业务、渲染、插件和平台问题。

## 教学节点

1. Debug/Profile/Release 性能差异与 Flutter DevTools；
2. UI、Raster、帧预算和 Janky Frame；
3. 不必要重建、长列表、图片内存和主 isolate 阻塞；
4. 分层日志、状态日志、网络日志、原生日志与脱敏；
5. Dart 单元测试、Widget Test、Integration Test；
6. Fake、依赖替换、状态流测试和关键路径回归；
7. Dart、Widget、插件、Engine、Android/iOS 的问题分层；
8. 复现、采证、假设、验证、根因、修复和回归。

## L1 引导实验

在既有项目中加入状态日志和关键测试，再使用 DevTools 观察一次不必要重建、一次长任务阻塞和一次图片内存压力。

## 故障任务

至少主动制造并定位：

- 一次无效或重复状态更新；
- 一次页面销毁后的异步回调；
- 一次布局或列表性能问题；
- 一次网络、缓存或序列化错误；
- 一次 Platform Channel 错误；
- 一次 Android/iOS 构建错误。

## 交付物与验收

- 单元、Widget 和关键流程测试；
- DevTools 截图或性能数据；
- 分层日志样例；
- 至少一份完整故障案例：现象 → 复现 → 证据 → 根因 → 修复 → 回归；
- 能在未知问题出现时先判断所属层级，再选择证据工具。

完成本章后，依据 [[../../skills/flutter|Flutter 领域]] 的中级标准进行综合验收，不能仅凭章节阅读记录升级能力。
