---
type: learning-module
area: Flutter
module: 03
status: planned
updated: 2026-08-26
---

# 03：状态管理、路由、依赖注入与模块边界

## 本章目标

能把页面状态、业务操作、数据访问和导航拆成可解释、可测试、可替换的结构。

## 教学节点

1. 临时 UI 状态、页面业务状态和共享状态；
2. `idle/loading/success/error` 与单向数据流；
3. `setState`、`ValueNotifier`、`ChangeNotifier` 的机制与边界；
4. 选择一个项目级状态方案，并解释为何需要它；
5. Navigator 路由栈、参数传递、返回结果和页面恢复；
6. 命令式路由与声明式路由的适用场景；
7. 构造注入、接口注入与对象生命周期；
8. Presentation、Domain、Data 的职责；
9. Repository 接口、Fake 实现和真实实现的替换；
10. 小项目避免过度分层的判断标准。

## L1 引导实验

先实现一个加载用户状态流，再把 Repository 替换为 Fake，覆盖成功、失败与超时；最后接入两个页面的路由和结果返回。

## 综合验收：登录垂直切片

```text
LoginPage
→ LoginController / ViewModel
→ LoginState
→ LoginRepository
→ FakeLoginRepository
→ 成功 / 失败 / 超时
→ 登录成功后导航
```

## 故障任务

- 页面销毁后异步结果尝试更新状态；
- 重复提交产生竞态；
- 错误的依赖生命周期导致状态意外共享。

## 交付物与验收

- 登录项目代码和结构说明；
- 至少一个状态逻辑测试；
- 状态转换记录；
- 手动修改一次校验或异常需求，不整页重新生成；
- 能解释每层职责、依赖方向和一次完整登录状态流。

通过后进入 [[04-data-network-storage|04：网络与数据]]。
