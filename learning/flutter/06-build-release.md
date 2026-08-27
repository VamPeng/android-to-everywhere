---
type: learning-module
area: Flutter
module: 06
status: planned
updated: 2026-08-26
---

# 06：Android/iOS 构建、签名与发布

## 本章目标

能配置多环境项目，独立完成 Android/iOS 的 Debug、Profile 和 Release 构建，并分层定位常见构建问题。

## 教学节点

1. Flutter SDK、项目结构与版本约束；
2. Debug、Profile、Release 的差异；
3. Flavor、入口文件与环境配置；
4. Android Gradle、SDK 版本、APK/AAB 和签名；
5. 混淆、资源压缩和敏感配置；
6. iOS Runner、Bundle ID、Certificate、Provisioning Profile 和 Archive；
7. 插件原生依赖与最低系统版本；
8. Dart、Flutter、Gradle/Xcode、签名环境的分层排查；
9. 最小 CI 构建与产物留存。

## L1 引导实验

为同一项目建立 dev/prod 两套配置，分别完成 Android Debug、Android Release 和 iOS 模拟器构建。

## 故障任务

- 制造 SDK 或插件版本冲突；
- 使用错误签名配置；
- 遗漏某个环境变量并从构建日志定位。

## 交付物与验收

- 可复现构建命令；
- Android Release 产物与签名检查结果；
- iOS 构建结果；
- 一份构建故障分层排查记录。

通过后进入 [[07-platform-channel|07：原生桥接]]。
