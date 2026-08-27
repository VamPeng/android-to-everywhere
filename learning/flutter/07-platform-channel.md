---
type: learning-module
area: Flutter
module: 07
status: planned
updated: 2026-08-26
---

# 07：Platform Channel 与基础原生桥接

## 本章目标

能判断何时需要原生桥接，并实现 Dart 与 Android/iOS 之间可靠的请求响应和连续事件通信。

## 教学节点

1. Dart、Flutter Framework、Engine、Embedder 和平台代码的边界；
2. `MethodChannel`、`EventChannel`、`BasicMessageChannel`；
3. Codec、参数类型、错误码和异常映射；
4. Flutter 调用原生方法并接收结果；
5. 原生向 Flutter 推送连续事件；
6. 主线程、Activity/Context 和生命周期；
7. 订阅取消、资源释放和重复注册；
8. 项目内桥接与独立 Flutter Plugin 的选择；
9. 平台接口统一与 Android/iOS 差异实现。

## L1 引导实验

先通过 `MethodChannel` 获取原生设备信息，再通过 `EventChannel` 接收原生计时或状态事件，并在页面销毁时释放订阅。

## 故障任务

- Dart 与 Kotlin 使用不一致的 Channel 名称；
- 返回无法编码的参数类型；
- 重复注册监听导致事件重复；
- 在错误线程调用要求主线程的原生 API。

## 交付物与验收

- Dart 与 Kotlin 双端带注释代码；
- 方法调用和事件流执行链；
- 成功、原生失败、参数错误和取消证据；
- 能区分 Channel、插件和 FFI 的适用范围。

通过后进入 [[08-quality-diagnostics|08：质量与问题定位]]。
