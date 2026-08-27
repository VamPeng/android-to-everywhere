---
type: learning-module
area: Flutter
module: 02
status: planned
updated: 2026-08-27
---

# 02：Widget、输入、布局、适配与可访问性

## 本章目标

能独立搭建包含输入与滚动的常规页面，理解 Flutter 页面从 Widget 配置到布局、绘制和状态更新的关键链路，并能适配屏幕、平台与辅助技术。

## 教学节点

1. `main()`、`runApp()`、`MaterialApp` 与 `Scaffold`；
2. Widget 的不可变性，`StatelessWidget`、`StatefulWidget` 与 `State`；
3. Widget、Element、RenderObject 的职责和关联；
4. `BuildContext`、父子位置、Inherited 依赖与 `didChangeDependencies`；
5. `build()`、`setState()`、重建范围与 `const`；
6. `Key`、局部状态、节点匹配与状态保留；
7. `initState`、`didUpdateWidget`、`dispose`、`mounted` 与 App 生命周期；
8. `Row`、`Column`、`Stack`、`Expanded`、`Flexible`；
9. Constraints go down、Sizes go up、Parents set positions；
10. `ListView`、`GridView`、ScrollController、惰性列表与 Sliver 基础；
11. `TextField`、`TextFormField`、Form、Controller、Focus、键盘与校验；
12. 点击、拖动等常用手势，以及隐式/显式动画的生命周期边界；
13. `SafeArea`、`MediaQuery`、`LayoutBuilder`、断点与响应式布局；
14. Material/Cupertino 平台适配、Theme、文字缩放与深浅色；
15. Locale、本地化资源、复数/日期格式和 LTR/RTL 基础；
16. Semantics、焦点顺序、触控尺寸、对比度、TalkBack/VoiceOver 基础；
17. Build、Layout、Paint、Compositing 与帧调度的最小渲染链路。

## L0 概念门禁

- 能解释 Widget、Element、RenderObject、BuildContext、State 与帧流水线的关系；
- 能根据约束推导常见布局结果，并说明重建不等于重新布局或重新绘制；
- 能说明输入焦点、资源生命周期、窗口尺寸、平台习惯、本地化和 Semantics 的边界。

## L1 引导实验

实现可交互自适应用户资料页：资料展示与编辑、表单校验、焦点切换、在线状态切换、动态列表增删、窄/宽屏布局和页面进入退出日志。

需要记录：哪些 Widget 重新执行 `build()`、状态是否保留、布局约束如何传递、焦点如何移动、资源何时释放，以及大字体和屏幕阅读器下是否可用。

## L2 半开放任务

- 制造一次 Row overflow 并根据约束修复；
- 修改普通字段但不调用 `setState()`，解释 UI 不更新的原因；
- 给定控制器或 FocusNode 泄漏现象，定位生命周期问题；
- 给定旋转、分屏或大字体后的布局/状态异常，独立修正；
- 给定缺少语义标签或焦点顺序错误的页面，完成无障碍修正。

## L3 综合实战

独立完成登录 UI：表单校验、密码可见性、焦点与键盘流程、加载/错误显示、窄屏与宽屏适配、基础本地化和无障碍行为；本章只处理 UI 与临时状态，业务状态在 03 接入。

## 交付物与验收

- 可运行资料页；
- Build、输入焦点与生命周期日志；
- overflow 修复前后截图；
- 至少一个 Widget Test 和一个无障碍基线检查；
- 能解释 Widget 为什么不是实际渲染对象，以及 `setState()` 后发生的关键步骤。

通过 L0～L3 后进入 [[03-state-routing-architecture|03：状态、导航、依赖与应用架构]]。
