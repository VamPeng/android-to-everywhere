---
type: learning-track
area: Android Performance
updated: 2026-08-23
---

# Android 性能与疑难排查学习路线

目标不是记住优化清单，而是形成固定的证据链分析能力：

```text
确定症状
→ 选择正确工具
→ 找到异常时间段
→ 判断线程/进程/渲染阶段
→ 建立代码与系统行为的关联
→ 验证根因
→ 修复并量化回归
```

## 模块顺序

| 模块 | 学习重点 | 主要工具 | 状态 |
|---|---|---|---|
| 01 UI 卡顿 | 帧超时、Main/RenderThread/GPU、线程状态、自定义 Trace | Android Studio System Trace、Perfetto | 当前 |
| 02 ANR | ANR 类型、主线程栈、锁竞争、Binder 等待、输入超时 | traces、bugreport、Perfetto | 计划 |
| 03 内存 | 泄漏、内存增长、Bitmap、Java/Native Heap、GC | Memory Profiler、Heap Dump、Perfetto | 计划 |
| 04 启动 | 冷/温/热启动、初始化、主线程 I/O、类加载 | Macrobenchmark、Perfetto | 计划 |
| 05 I/O 与数据库 | 主线程 I/O、事务、锁、索引、文件读写 | StrictMode、Trace、SQLite 工具 | 计划 |
| 06 性能回归 | 可重复基准、稳定采样、自动化门禁 | Macrobenchmark、CI | 计划 |

## 当前入口

先完成：[[01-ui-jank-guided-lab|01：UI 卡顿 Trace 引导实验]]。

第一轮不要求你面对一个未知线上问题。先通过 `sleep` 与 CPU 忙循环两个已知故障，学习如何从 Trace 中区分：

```text
耗时很长但没有占用 CPU
vs
耗时很长并持续占用 CPU
```

掌握工具后，再进入只给现象、不告知根因的半开放案例。