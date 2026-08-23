---
type: guide
updated: 2026-08-23
---

# Obsidian 配置

## 1. 打开仓库

```bash
git clone https://github.com/VamPeng/android-to-everywhere.git
cd android-to-everywhere
```

在 Obsidian 中选择：

```text
Open folder as vault
→ 选择 android-to-everywhere 根目录
```

`00-Dashboard.md` 是首页。可将它固定在标签页或加入书签。

## 2. 推荐插件

### Dataview

用于读取各文件的 YAML 属性，并自动生成能力表格、任务和案例列表。安装后，`00-Dashboard.md` 中的查询会自动渲染。

### Obsidian Git（可选）

适合日常简单 Pull、Commit 和 Push。发生冲突、改分支或批量重构时，仍使用终端或 IDE。

## 3. Git 操作

开始记录前：

```bash
git pull --rebase
```

完成本周记录后：

```bash
git add .
git commit -m "docs: update weekly progress"
git push
```

## 4. `.obsidian` 目录

本仓库默认忽略 `.obsidian/`，避免提交个人窗口状态、插件缓存和本地设置。Markdown 内容不依赖 Obsidian，可随时使用 GitHub、VS Code 或其他编辑器读取。

## 5. Dataview 元数据约定

技能页使用：

```yaml
---
type: skill
priority: P1
order: 40
current: "AI 辅助做过"
target: "中级独立开发"
status: active
evidence_count: 0
---
```

案例页使用：

```yaml
---
type: case
area: Android
problem: 页面滑动卡顿
status: draft
date: 2026-08-30
---
```

## 6. 安全边界

仓库是公开的。提交日志、截图和 Trace 前必须脱敏，不保存 Token、Cookie、密钥、真实用户信息、公司内部接口或受保密约束的内容。
