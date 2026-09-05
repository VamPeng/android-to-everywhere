---
type: learning-path
area: Flutter
priority: P1
status: active
updated: 2026-08-27
---

# Flutter：从 Android 到中级独立开发

## 学习目标

本路径面向具备 Android/Kotlin 经验、但 Flutter 基础尚未建立的开发者。学习过程利用 Android 经验进行迁移，但所有 Flutter 结论都要通过 Dart 代码、运行结果、测试、日志或 DevTools 证据验证。

这不是“先读完全部理论再写项目”，也不是“直接让 AI 生成业务页面”，而是：

```text
核心概念
→ 最小代码
→ 运行观察
→ 手动修改
→ 故障实验
→ 综合实战
```

## 章节顺序

| 章节 | 核心问题 | 引导产出 | 综合验收 |
|---|---|---|---|
| [[01-dart-foundation|01 Dart 语言、异步与工程工具链]]（[[01-dart-foundation-review|快速复习]]） | Flutter 业务代码如何安全表达数据、并发、异常和依赖 | 纯 Dart 用户请求实验 | 为状态、Repository、测试和依赖治理提供基础 |
| [[02-widget-layout-rendering|02 Widget、输入、布局、适配与可访问性]] | 页面如何创建、输入、约束、更新并适配用户与设备 | 可交互自适应用户资料页 | 能独立搭建可测试、可访问的登录 UI |
| [[03-state-routing-architecture|03 状态、导航、依赖与应用架构]] | 状态、事件和依赖如何跨页面与模块流动 | 登录状态流与路由骨架 | 完整登录垂直切片 |
| [[04-data-network-storage|04 网络、会话、存储、缓存与实时数据]] | 远端、本地、会话和实时数据如何可靠协作 | 带会话与缓存的分页列表 | 列表、详情、鉴权、错误恢复与 SSE |
| [[05-media-files-permissions|05 媒体、文件、权限与平台隐私]] | 如何安全访问平台媒体和文件 | 图片选择上传实验 | 权限、内存、进度、取消与失败重试 |
| [[06-build-release|06 环境、构建、签名、交付与依赖治理]] | 如何从开发工程得到可追溯、可回滚的发布产物 | dev/prod 双环境构建 | Android/iOS Release 与发布演练 |
| [[07-platform-channel|07 Platform Channel、Plugin、Pigeon 与 FFI 边界]] | Dart 与原生平台如何可靠、可测试地集成 | 双端方法调用与原生事件流 | Android/iOS 原生能力接入 |
| [[08-quality-diagnostics|08 测试、性能、可观测性、安全与故障定位]] | 如何用工程证据保证质量并定位故障 | 质量门禁、故障注入与修复记录 | Flutter 中级综合验收 |

## 四级门禁

每章必须显式完成四个等级，不能用 L1 的成功运行替代 L2/L3：

| 等级 | 证明内容 |
|---|---|
| L0 概念与对照 | 能解释关键模型、执行链、Android/Kotlin 差异与适用边界 |
| L1 引导实验 | 按指导完成可运行实验，并记录观察证据 |
| L2 半开放任务 | 只给现象和验收条件，能够定位、修改并解释 |
| L3 综合实战 | 将本章能力迁移到主项目或真实故障，完成测试与复盘 |

## 横切质量基线

质量能力从第一章开始累积，第八章只负责综合与未知问题验收：

- 01 起执行格式化、静态分析、Lint、单元测试和依赖记录；
- 02 起执行 Widget Test、输入与生命周期检查、适配和无障碍基线；
- 03～05 为状态、导航、Repository、缓存、权限和取消行为留下测试或日志；
- 04～06 持续检查鉴权、敏感数据、平台隐私、依赖和发布配置；
- 06 留存可追溯产物、符号文件和发布记录；
- 07 对 Dart 与原生两侧分别测试，并至少完成一次端到端桥接验证；
- 08 汇总性能、Crash、日志、回归、可访问性与安全证据。

## 学习节奏

- 一次只推进一个章节节点，不同时铺开八个领域。
- 01～03 完成后立即进行登录实战，不等待全部理论学完。
- 04、05 分别绑定列表/详情与图片上传，避免脱离业务学习。
- 06～08 在已有项目上完成，不重新创建无关 Demo。
- 每章先由用户运行和观察，再由 AI 核对；没有自己的解释就不升级状态。
- 测试、日志、静态检查、安全和可访问性不是第八章才开始的附加项。

## 单章完成定义

```text
能运行最小实验
+ 能解释关键执行链
+ 能手动修改一个需求
+ 能制造并定位一个错误
+ 能完成一个只给现象的半开放任务
+ 能迁移到综合业务或真实故障
+ 有测试、日志、截图或构建结果
+ 能回答验收问题
```

学习笔记只证明“接触”；通过引导实验证明“能操作”；完成半开放任务和综合实战后，才证明“能够独立迁移”。

## AI 教学输出约定

每次请求某一章时，AI 必须按以下顺序教学：

```text
本轮唯一节点
→ Why：为什么需要它
→ Android/Kotlin 对照
→ How：带注释代码与执行链
→ 运行与观察步骤
→ 用户先给出判断
→ AI 核对和纠错
→ 修改任务与故障任务
→ 验收及下一节点
```

不得只罗列 API，不得一次生成整章所有项目代码，也不得因 AI 代码运行成功而直接勾选完成。

## 官方校准入口

- [Dart 语言](https://dart.dev/language)
- [Flutter 学习路径](https://docs.flutter.dev/learn/pathway)
- [Flutter 应用架构](https://docs.flutter.dev/app-architecture)
- [Flutter UI、适配与可访问性](https://docs.flutter.dev/ui)
- [Flutter 数据与后端](https://docs.flutter.dev/data-and-backend)
- [Flutter 测试与调试](https://docs.flutter.dev/testing)
- [Flutter 性能](https://docs.flutter.dev/perf)
- [Flutter 平台集成](https://docs.flutter.dev/platform-integration)
- [Flutter 部署](https://docs.flutter.dev/deployment)
