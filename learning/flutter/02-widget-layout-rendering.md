---
type: learning-module
area: Flutter
module: 02
status: planned
updated: 2026-08-26
---

# 02：Widget、布局、生命周期与渲染更新

## 本章目标

能独立搭建常规页面，理解 Flutter 页面从 Widget 配置到布局、绘制和状态更新的关键链路。

## 教学节点

1. `main()`、`runApp()`、`MaterialApp` 与 `Scaffold`；
2. Widget 的不可变性，`StatelessWidget`、`StatefulWidget` 与 `State`；
3. Widget、Element、RenderObject 的职责和关联；
4. `BuildContext`、父子位置与依赖查找；
5. `build()`、`setState()`、重建范围与 `const`；
6. `Row`、`Column`、`Stack`、`Expanded`、`Flexible`；
7. Constraints go down、Sizes go up、Parents set positions；
8. `ListView`、`GridView` 与惰性列表；
9. `Key` 在节点匹配和状态保留中的作用；
10. `initState`、`didUpdateWidget`、`dispose` 与 `mounted`；
11. Build、Layout、Paint 的最小渲染链路。

## L1 引导实验

实现可交互用户资料页：资料展示、在线状态切换、动态列表增删、页面进入退出日志。

需要记录：哪些 Widget 重新执行 `build()`、状态是否保留、布局约束如何传递、资源何时释放。

## 故障任务

- 制造一次 Row overflow 并根据约束修复；
- 修改普通字段但不调用 `setState()`，解释 UI 不更新的原因；
- 故意遗漏控制器释放，说明生命周期风险。

## 交付物与验收

- 可运行资料页；
- Build 与生命周期日志；
- overflow 修复前后截图；
- 能解释 Widget 为什么不是实际渲染对象，以及 `setState()` 后发生的关键步骤。

通过后进入 [[03-state-routing-architecture|03：状态与工程组织]]。
