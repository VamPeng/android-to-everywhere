---
type: learning-module
area: Flutter
module: 01
status: completed
updated: 2026-09-01
---

# 01：Dart 核心基础

## 本章目标

能独立阅读和编写 Flutter 业务层常见 Dart 代码，为后续状态、Repository、序列化和异步 UI 打下语言基础。

## 教学节点

1. 变量、类型推断、`final` 与 `const`；
2. 空安全：可空类型、`?.`、`??`、`!`、`late`；
3. 函数、命名参数、可选参数和默认值；
4. 类、构造函数、工厂构造、继承、抽象类与接口；
5. 泛型、扩展方法与 Mixin 的适用边界；
6. `List`、`Set`、`Map` 与集合转换；
7. `Future`、`async/await` 与异步异常；
8. `Stream`、订阅、取消和错误事件；
9. isolate 的职责与主 isolate 阻塞概念。

每个节点优先与 Kotlin 对照，但必须指出语义差异，不能只做语法翻译。

## L1 引导实验

实现一个纯 Dart 用户请求程序：

```text
Map 模拟 JSON
→ UserDto 解析
→ FakeUserRepository 返回 Future<Result<User>>
→ 成功 / 业务失败 / 异常
→ Stream 输出请求进度
→ 取消订阅
```

## 故障任务

- 对可空值错误使用 `!`，观察运行时异常；
- 在 `async` 调用链中遗漏 `await`，解释错误出现的位置；
- 重复监听单订阅 Stream，记录异常并修正。

## 交付物与验收

- 可运行的 Dart 源码与运行命令；
- 一张 Kotlin/Dart 语义差异表；
- 一份成功、失败和异常输出；
- 能解释 Future 与 Stream 的差别，以及异常沿异步链传播的路径。

快速回顾：[[01-dart-foundation-review|01：Dart 核心基础快速复习]]。

通过后进入 [[02-widget-layout-rendering|02：Widget、布局与渲染更新]]。
