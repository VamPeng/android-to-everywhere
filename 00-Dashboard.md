---
type: dashboard
updated: 2026-08-23
---

# Android to Everywhere

## 当前执行

- 长期路线：[[ROADMAP]]
- 当前能力：[[PROFILE]]
- 当前状态：[[CURRENT_STATUS]]
- 当前季度：[[quarters/2026-Q3|2026 Q3]]
- 当前周：[[weeks/2026-W35|2026 W35]]
- 当前学习：[[learning/android-performance/01-ui-jank-guided-lab|UI 卡顿 Trace 引导实验]]
- 主实战项目：[[projects/PRIMARY_PROJECT|Everywhere Lab]]
- 执行规则：[[WORKFLOW]]
- 学习系统：[[LEARNING_SYSTEM]]

## 优先级

```text
P0  Android 深度：持续不断
P1  Flutter = React Native：必须达到中级独立开发
P2  iOS + HarmonyOS：基础原生业务开发
P3  Vue 管理后台 + Java 后端：常规业务独立开发
横切 AI：理解、修改、验证、排障，而不是盲目生成
```

## 能力总览

> 安装 Dataview 后，下面内容会自动渲染为表格。

```dataview
TABLE
  priority AS "优先级",
  current AS "当前",
  target AS "目标",
  status AS "状态",
  evidence_count AS "证据数"
FROM "skills"
WHERE type = "skill"
SORT order ASC
```

## 未完成任务

```dataview
TASK
FROM "weeks" OR "quarters"
WHERE !completed
GROUP BY file.link
```

## 最近案例

```dataview
TABLE
  area AS "方向",
  problem AS "问题",
  status AS "状态",
  file.mtime AS "最后更新"
FROM "cases"
WHERE type = "case"
SORT file.mtime DESC
LIMIT 8
```

## 导航

- [[learning/README|学习内容]]
- [[SKILL_MATRIX|能力矩阵]]
- [[FEATURE_MATRIX|多平台功能矩阵]]
- [[projects/PROJECT_INDEX|项目索引]]
- [[cases/README|实战案例]]
- [[decisions/README|技术决策]]
- [[evidence/README|证据管理]]
- [[OBSIDIAN_SETUP|Obsidian 设置]]
