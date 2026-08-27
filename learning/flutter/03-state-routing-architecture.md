---
type: learning-module
area: Flutter
module: 03
status: planned
updated: 2026-08-27
---

# 03：状态、导航、依赖与应用架构

## 本章目标

能把页面状态、业务操作、数据访问和导航拆成可解释、可测试、可替换的结构。

## 教学节点

1. 临时 UI 状态、页面业务状态、共享会话状态和持久状态；
2. 不可变 UI State、sealed 状态、`idle/loading/success/error` 与穷尽渲染；
3. 用户事件、Command、一次性副作用与单向数据流；
4. `setState`、`ValueNotifier`、`ChangeNotifier` 的机制与边界；
5. 选择一个项目级状态方案，并解释订阅、选择性重建和资源释放；
6. 异步竞态、重复提交、取消、幂等操作和页面销毁后的结果处理；
7. Navigator 路由栈、参数传递、返回结果、系统返回与 Predictive Back；
8. Router/声明式路由（如 `go_router`）、Deep Link、登录重定向和嵌套路由基础；
9. 页面恢复与 Restoration 的适用范围；
10. 构造注入、接口注入、Composition Root、Scope 与对象生命周期；
11. View、ViewModel、Repository、Service 组成的 UI/Data 主分层；
12. Domain/Use Case 仅在复杂或重复业务逻辑下引入；
13. Repository 抽象、Fake/真实实现替换与单一事实来源；
14. 按 Feature 组织代码、依赖方向和避免过度分层的判断标准。

## L0 概念门禁

- 能画出用户事件 → Command/ViewModel → Repository → UI State → View 的单向链路；
- 能解释临时状态、业务状态、共享会话状态和持久状态分别应由谁持有；
- 能比较 Navigator 与 Router，并说明 Deep Link、返回栈、状态恢复和依赖 Scope 的风险。

## L1 引导实验

先实现不可变的用户加载状态流，再把 Repository 替换为 Fake，覆盖成功、失败、超时和重复触发；最后接入两个页面的声明式路由、参数、结果返回和一个 Deep Link。

## L2 半开放任务

- 页面销毁后异步结果尝试更新状态；
- 重复提交产生竞态；
- 错误的依赖 Scope 导致状态意外共享或提前释放；
- Deep Link、系统返回或登录重定向产生错误页面栈；
- View 直接依赖 Service，导致测试无法替换依赖。

## L3 综合实战

将 02 的登录 UI 接入真实状态、Fake Repository、路由和依赖装配，完成校验、加载、错误、超时、防重复提交、成功跳转、返回栈和冷启动 Deep Link；真实鉴权会话在 04 接入。

```text
LoginPage
→ LoginController / ViewModel
→ Immutable LoginState
→ LoginRepository
→ FakeLoginRepository
→ 成功 / 失败 / 超时
→ 防重复提交与一次性副作用
→ 登录成功后导航 / 登录重定向
```

## 交付物与验收

- 登录项目代码和结构说明；
- 状态逻辑、路由和依赖替换测试；
- 状态转换记录；
- 手动修改一次校验或异常需求，不整页重新生成；
- 能解释每层职责、依赖方向和一次完整登录状态流。

通过 L0～L3 后进入 [[04-data-network-storage|04：网络、会话、存储、缓存与实时数据]]。
