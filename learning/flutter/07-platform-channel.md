---
type: learning-module
area: Flutter
module: 07
status: planned
updated: 2026-08-27
---

# 07：Platform Channel、Plugin、Pigeon 与 FFI 边界

## 本章目标

能判断何时使用现有插件、自建 Channel、Pigeon、Platform View 或 FFI，并实现 Dart 与 Android/iOS 之间可靠、可测试、可演进的请求响应和连续事件通信。

## 教学节点

1. Dart、Flutter Framework、Engine、Embedder 和平台代码的边界；
2. 优先评估官方/社区插件，以及对第三方插件做业务接口封装；
3. `MethodChannel`、`EventChannel`、`BasicMessageChannel` 的语义；
4. Codec、支持类型、空值、错误码、异常映射和协议版本；
5. Pigeon 生成类型安全的 Dart/Kotlin/Swift 接口；
6. Flutter 调用原生方法、超时、取消边界和结果返回；
7. 原生向 Flutter 推送事件流、背压边界和订阅状态；
8. Flutter 主 isolate、Android 主线程/Task Queue 与 iOS 主线程；
9. Activity/Context、UIViewController、Engine 和 App 生命周期；
10. 订阅取消、资源释放、热重载/Engine 重建与重复注册；
11. 项目内桥接、独立 Plugin、Federated Plugin 与平台接口包；
12. Mock Channel、Dart 测试、原生单测与双端集成测试；
13. Platform View 的渲染/手势成本、后台 isolate channel 和 FFI 的适用边界；
14. 通知、App/Universal Link、后台执行等平台能力的接入与生命周期通法；
15. 统一 Dart 能力接口与 Android/iOS 差异实现。

## L0 概念门禁

- 能根据能力来源选择插件、Channel、Pigeon、Platform View 或 FFI；
- 能画出 Dart → Codec/Pigeon → Android/iOS → Result/Event 的双向执行链；
- 能说明线程、Engine、Activity/UIViewController、订阅和错误协议的生命周期。

## L1 引导实验

先在 Android 使用 `MethodChannel` 获取原生设备信息，再通过 `EventChannel` 接收原生计时或状态事件，并在页面销毁时释放订阅；随后使用 Pigeon 重写一个带结构化参数和错误结果的方法。

## L2 半开放任务

- Dart 与 Kotlin 使用不一致的 Channel 名称；
- 返回无法编码的参数类型；
- 重复注册监听导致事件重复；
- 在错误线程调用要求主线程的原生 API；
- Engine/Activity 重建后仍持有旧引用；
- Dart、Android、iOS 协议版本不一致。

## L3 综合实战

以统一 Dart 接口接入同一项 Android/iOS 原生能力：Android 使用 Kotlin、iOS 使用 Swift，支持请求响应、连续事件、错误映射、取消和资源释放；至少一个复杂消息使用 Pigeon，并为 Dart、原生侧和集成链路建立测试。

## 交付物与验收

- Dart、Kotlin 与 Swift 三端带注释代码；
- 方法调用和事件流执行链；
- 成功、原生失败、参数错误、取消和生命周期恢复证据；
- Dart Mock、Android/iOS 原生测试或双端集成测试；
- 能区分 Channel、插件和 FFI 的适用范围。

通过 L0～L3 后进入 [[08-quality-diagnostics|08：测试、性能、可观测性、安全与故障定位]]。
