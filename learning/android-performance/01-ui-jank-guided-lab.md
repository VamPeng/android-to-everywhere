---
type: guided-lab
area: Android Performance
level: L1
status: ready
updated: 2026-08-23
---

# 01：UI 卡顿 Trace 引导实验

## 本节目标

完成后，你需要能独立回答：

1. 哪一帧错过了渲染期限；
2. 问题主要发生在 Main Thread、RenderThread 还是 GPU；
3. 主线程在异常区间是占用 CPU、等待、休眠还是被阻塞；
4. 哪一段应用代码与异常时间区间重合；
5. 修复后如何证明问题确实消失或明显减轻。

这不是“会写一个 `Thread.sleep()`”的任务。`sleep` 只是已知答案的教学样本，用来学习 Trace 的阅读方式。

---

## 一、先建立最小概念

### 1. 帧预算不是固定的 16 ms

60 Hz 屏幕一帧约为 16.67 ms；90 Hz、120 Hz 的可用时间更短。实际分析时不要只背 16 ms，应以 Trace 中该帧的 deadline 和 FrameTimeline/Janky frames 结果为准。

### 2. 卡顿排查的第一工具是 System Trace

System Trace 能同时看到：

- 帧是否超时；
- 主线程和 RenderThread 的时间线；
- 线程何时真正运行在 CPU 上；
- 调度、锁、I/O、Binder、GC 等系统事件；
- 自定义 Trace 区间。

方法级 Profiler 可以辅助寻找耗时方法，但会引入额外开销，也不能像 System Trace 一样完整表达线程是运行还是等待。因此本实验先用 System Trace，再根据需要补方法分析。

### 3. 自定义 Trace 的作用

系统只能告诉你某段时间主线程很忙或被阻塞。自定义 Trace 把应用代码区间标记到同一条时间轴上，建立：

```text
异常帧时间
↔ 线程状态
↔ 应用方法
```

---

## 二、实验准备

### 推荐环境

- 真实 Android 设备优先；
- Android 12 及以上最容易直接看到 `Janky frames`；
- 当前 Android 14 设备可以直接使用；
- 使用 Android Studio 的 **System Trace**；
- 第一次实验允许使用 Debug 构建，正式对比再切换到更接近 Release 的可分析构建。

### 创建一个最小页面

页面放两个按钮：

```text
按钮 A：Sleep 80 ms
按钮 B：CPU Busy 80 ms
```

代码只用于实验，禁止进入生产代码。

```kotlin
import android.os.SystemClock
import android.os.Trace

private var blackHole: Long = 0L

private fun sleepOnMainThread() {
    Trace.beginSection("JankLab#sleep80ms")
    try {
        Thread.sleep(80)
    } finally {
        Trace.endSection()
    }
}

private fun cpuBusyOnMainThread() {
    Trace.beginSection("JankLab#cpuBusy80ms")
    try {
        val deadline = SystemClock.elapsedRealtimeNanos() + 80_000_000L
        var value = 0L
        while (SystemClock.elapsedRealtimeNanos() < deadline) {
            value = value xor System.nanoTime()
        }
        blackHole = value
    } finally {
        Trace.endSection()
    }
}
```

分别从按钮点击回调直接调用这两个方法，确保它们运行在主线程。

---

## 三、第一次采集：Sleep 80 ms

### 操作步骤

```text
Android Studio
→ View
→ Tool Windows
→ Profiler
→ 选择目标进程
→ CPU / System Trace
→ Record
→ 点击 Sleep 80 ms 一次
→ 再等待 1～2 秒
→ Stop
```

不要连续狂点。单次触发更容易建立时间对应关系。

### 在 Trace 中按这个顺序查看

#### 1. 先找异常帧

Android 12+：

```text
Display
→ Janky frames
→ 选择包含红色超时区间的帧
```

选择后重点线程通常会被关联高亮：

```text
Main Thread
RenderThread
GPU completion
```

如果没有直接显示候选帧，打开 `All Frames` 或 `Lifecycle`，并检查是否确实在录制期间触发了按钮。

#### 2. 判断是哪一层拖慢

先不要急着找你的方法名，先回答：

```text
Main Thread 是否出现覆盖异常帧的长区间？
RenderThread 是否长时间工作或等待？
GPU completion 是否明显晚于应用侧？
```

本实验预期瓶颈在 Main Thread。

#### 3. 找自定义区间

展开应用进程的主线程，查找：

```text
JankLab#sleep80ms
```

它应该与异常帧的时间区间明显重合。

#### 4. 判断是否真的占用 CPU

观察同一时间段的 CPU core、线程调度和主线程状态：

- 自定义区间持续约 80 ms；
- 但主线程并不会在这 80 ms 内持续占用 CPU；
- 它主要是在休眠，无法继续处理消息和绘制下一帧。

这说明：

> “主线程被阻塞了 80 ms”不等于“主线程消耗了 80 ms CPU 时间”。

### 第一次观察表

完成后填写：

```text
触发动作：
异常帧开始时间：
异常帧/区间持续时间：
主要瓶颈线程：
自定义 Trace 名称：
自定义区间是否与异常帧重合：
该区间是否持续占用 CPU：
为什么 UI 仍然会卡顿：
```

---

## 四、第二次采集：CPU Busy 80 ms

使用同样流程重新录制，只点击 `CPU Busy 80 ms`。

### 重点不是再次找到 80 ms，而是做对照

预期观察：

```text
Sleep 80 ms
→ 墙上时间很长
→ 主线程无法处理下一帧
→ 但不持续消耗 CPU

CPU Busy 80 ms
→ 墙上时间很长
→ 主线程无法处理下一帧
→ 同时持续获得 CPU 时间执行计算
```

### 第二次观察表

```text
自定义 Trace 名称：
异常帧是否仍由 Main Thread 导致：
主线程在 CPU 轨道上的表现：
与 Sleep 案例最大的区别：
两者为什么都会错过帧期限：
后续选择 Dispatcher 时应如何区分：
```

---

## 五、建立第一次排查决策树

```text
发现 Janky Frame
│
├─ Main Thread 覆盖了异常区间？
│  ├─ 是：检查自定义 Trace、消息、Binder、GC、I/O、锁与线程状态
│  │  ├─ 持续 Running：CPU 计算、布局、绘制、序列化等
│  │  ├─ Sleeping/Waiting：人为等待、条件等待、错误同步
│  │  └─ Blocked：锁竞争、Binder/I/O 等待，继续找唤醒方或持锁方
│  └─ 否：继续检查 RenderThread / GPU / SurfaceFlinger
│
├─ RenderThread 时间过长？
│  └─ 检查绘制命令、复杂阴影、图片、图层与同步点
│
└─ GPU completion 过晚？
   └─ 进入 GPU/图形专项，不直接归因于主线程业务代码
```

第一轮只要求你熟练走 Main Thread 分支，不要求一次掌握 GPU 分析。

---

## 六、修复实验

### CPU 工作

把纯计算移出主线程：

```kotlin
lifecycleScope.launch {
    val result = withContext(Dispatchers.Default) {
        Trace.beginSection("JankLab#cpuBusyBackground")
        try {
            runCpuWork()
        } finally {
            Trace.endSection()
        }
    }

    render(result)
}
```

要求：`runCpuWork()` 内不要操作 View，也不要在中途切回主线程。

### I/O 工作

真实文件、数据库或阻塞网络 I/O 应放到适合阻塞任务的执行环境，例如 `Dispatchers.IO`。不要把“所有耗时都切到 IO”作为结论；CPU 计算与阻塞 I/O 的资源约束不同。

### 再次采集

修复后重新录制相同操作，比较：

```text
异常帧数量
帧超时时长
Main Thread 是否仍被长区间占据
后台线程是否出现对应 Trace
页面交互是否仍被阻塞
```

---

## 七、本实验真正的验收问题

你需要脱离文档回答：

1. 为什么 `sleep 80 ms` 和忙循环 80 ms 都会造成卡顿？
2. 为什么两者的 CPU 行为不同？
3. 如何从 Trace 判断瓶颈先发生在 Main、RenderThread 还是 GPU？
4. 自定义 Trace 解决了系统 Trace 的什么信息缺口？
5. 为什么不应该一开始只看方法耗时 Profiler？
6. 修复后为什么必须重新录制，而不能只凭肉眼感觉？

如果其中任意一项无法回答，把对应 Trace 截图或 `.perfetto-trace` 的关键区间交给 AI 逐项讲解，不需要自己猜。

---

## 八、提交给 AI 的最小材料

```text
设备与 Android 版本：
屏幕刷新率：
Sleep Trace 截图/文件：
CPU Busy Trace 截图/文件：
两份观察表：
我的初步结论：
看不懂的轨道或字段：
```

AI 下一步应做的是：

```text
核对你选择的异常帧
→ 核对线程与 CPU 判断
→ 修正错误解释
→ 再决定是否进入半开放案例
```

不会直接把“成功制造卡顿”判定为完成。

---

## 九、官方资料

按本实验需要阅读，不要求一次通读全部：

1. UI jank detection  
   https://developer.android.com/studio/profile/jank-detection
2. Record a system trace  
   https://developer.android.com/studio/profile/cpu-profiler
3. Slow rendering  
   https://developer.android.com/topic/performance/vitals/render
4. Overview of system tracing  
   https://developer.android.com/topic/performance/tracing
5. Perfetto system tracing  
   https://perfetto.dev/docs/getting-started/system-tracing
6. `android.os.Trace` API  
   https://developer.android.com/reference/android/os/Trace

本实验暂不引入 Macrobenchmark。先学会正确阅读一次人工触发的 System Trace，再进入可重复基准和性能回归。