---
type: learning-module
area: Flutter
module: 06
status: planned
updated: 2026-08-27
---

# 06：环境、构建、签名、交付与依赖治理

## 本章目标

能配置多环境项目，独立完成 Android/iOS 的 Debug、Profile、Release、签名与发布演练，并追溯依赖、版本、产物、符号和回滚路径。

## 教学节点

1. Flutter/Dart SDK、项目结构、版本约束与团队环境复现；
2. `pubspec.yaml`、Lockfile、直接/传递依赖、升级和冲突治理；
3. Debug、Profile、Release 的编译、调试和性能差异；
4. Flavor、入口文件、编译期/运行期配置与 dev/staging/prod 隔离；
5. App Version、Build Number、变更记录和构建可追溯信息；
6. Android Gradle、SDK 版本、APK/AAB、Keystore、签名与 Play 发布基础；
7. iOS Runner、Bundle ID、Certificate、Provisioning Profile、Archive/IPA 与 App Store 发布基础；
8. 插件原生依赖、最低系统版本、Entitlement、权限与隐私声明；
9. 敏感配置不进入客户端、日志或仓库的安全边界；
10. 混淆、资源压缩、App Size、`split-debug-info`、符号留存与崩溃还原；
11. Dart、Flutter、插件、Gradle/Xcode、签名和商店规则的分层排查；
12. CI 中的 format、analyze、test、build、签名、产物校验与留存；
13. 发布说明、内测、灰度、监控、暂停、回滚和版本对应关系。

## L0 概念门禁

- 能画出源码 → 依赖解析 → 编译 → 原生打包 → 签名 → 商店交付的链路；
- 能说明环境配置、客户端秘密、签名材料、产物与符号文件的不同安全边界；
- 能根据日志判断问题属于 Dart/Flutter、插件、Android、iOS、签名还是商店配置。

## L1 引导实验

为同一项目建立 dev/prod 两套配置，分别完成 Android Debug、Android Release、iOS 模拟器和 iOS Release Archive；在 CI 中运行格式化、静态分析、测试并留存未签名或签名构建产物。

## L2 半开放任务

- 制造 SDK 或插件版本冲突；
- 使用错误签名配置；
- 遗漏某个环境变量并从构建日志定位；
- 产物版本、环境或 API 地址与预期不一致；
- 混淆后的 Crash 缺少匹配符号文件；
- CI 能构建但本地失败，或本地成功但 CI 失败。

## L3 综合实战

完成一次双端发布演练：固定 SDK/依赖、运行质量门禁、生成 Android AAB 与 iOS Archive/IPA、验证签名和环境、保存校验值与符号、编写发布说明，并演练灰度监控和回滚决策。若受账号权限阻塞，必须记录缺失权限和已经完成的可验证步骤，不能用模拟器构建替代 Release 验收。

## 交付物与验收

- 可复现构建命令；
- Android Release 产物与签名检查结果；
- iOS Release Archive/IPA 与签名检查结果；
- 版本、依赖、环境、产物校验值和符号文件清单；
- CI 记录、发布/回滚清单和一份构建故障分层排查记录。

通过 L0～L3 后进入 [[07-platform-channel|07：Platform Channel、Plugin、Pigeon 与 FFI 边界]]。
