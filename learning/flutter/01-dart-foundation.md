---
type: learning-module
area: Flutter
module: 01
status: planned
updated: 2026-08-27
---

# 01：Dart 语言、异步与工程工具链

## 本章目标

能独立阅读、编写、分析和测试 Flutter 业务层常见 Dart 代码，并能管理项目结构与依赖，为后续状态、Repository、序列化和异步 UI 打下基础。

## 教学节点

1. Sound Type System、类型推断、`Object?`、`dynamic`、`Never`；
2. 变量、`final`、`const`、空安全、`late` 与非空断言风险；
3. 函数、命名参数、可选参数、默认值、闭包与函数类型；
4. 类、构造函数、工厂构造、继承、抽象类、接口与类修饰符；
5. Enum、sealed 类型、穷尽 `switch` 与不可变状态建模；
6. Records、Patterns、解构和 JSON 结构校验；
7. 泛型、扩展方法、Mixin、库、导入与下划线可见性；
8. `List`、`Set`、`Map`、`Iterable`、集合转换与复制语义；
9. `Exception`、`Error`、`StackTrace`、`rethrow` 与 `finally`；
10. `Future`、`async/await`、并发等待、超时、异步异常与不可取消边界；
11. `Stream`、单订阅/广播、暂停、恢复、取消和错误事件；
12. isolate、消息隔离、`compute` 与主 isolate 阻塞；
13. Dart/Flutter 包结构、`pubspec.yaml`、Lockfile、依赖与开发依赖；
14. `format`、`analyze`、Lint、基础单元测试和依赖升级检查。

每个节点优先与 Kotlin 对照，但必须指出语义差异，不能只做语法翻译。

## L0 概念门禁

- 能说明 Dart 类型系统、空安全、不可变数据和库级可见性与 Kotlin 的关键差异；
- 能画出同步调用、Future、Stream 和 isolate 的最小执行关系；
- 能解释 `pubspec.yaml`、Lockfile、Analyzer、Lint 和测试各自解决的问题。

## L1 引导实验

实现一个纯 Dart 用户请求程序：

```text
Map 模拟 JSON
→ UserDto 解析
→ sealed Result 与不可变 User
→ FakeUserRepository 返回 Future<Result<User>>
→ 成功 / 业务失败 / 异常
→ Stream 输出请求进度
→ 取消订阅
→ format / analyze / test
```

## L2 半开放任务

- 对可空值错误使用 `!`，观察运行时异常；
- 在 `async` 调用链中遗漏 `await`，解释错误出现的位置；
- 重复监听单订阅 Stream，记录异常并修正。
- 给定包含缺失字段和错误类型的 JSON，只提供失败现象，独立补齐校验与错误映射；
- 给定一个依赖升级后的分析或测试失败，定位版本、API 或约束问题。

## L3 综合实战

独立实现一条“JSON → DTO → Domain Model → Repository → Result/Stream”数据链，覆盖成功、业务失败、格式错误、超时和资源取消，并整理成可直接供后续 Flutter 项目复用的业务层代码。

## 交付物与验收

- 可运行的 Dart 源码与运行命令；
- 一张 Kotlin/Dart 语义差异表；
- 一份成功、失败和异常输出，以及单元测试结果；
- `format`、`analyze`、Lint 和依赖状态无未解释问题；
- 能解释 Future、Stream 与 isolate 的边界，以及异常沿异步链传播的路径。

通过 L0～L3 后进入 [[02-widget-layout-rendering|02：Widget、输入、布局、适配与可访问性]]。
