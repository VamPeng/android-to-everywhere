---
type: ai-handoff
updated: 2026-08-23
repository: VamPeng/android-to-everywhere
source_of_truth: main
---

# 新会话接管协议

本文件用于让任何新的 AI 会话在**不依赖旧聊天记忆**的情况下，继续维护职业路线、学习内容、周计划与实战证据。

## 用户最短指令

新开会话时，发送：

```text
接管我的职业规划仓库：
https://github.com/VamPeng/android-to-everywhere

先读取 main 分支的 AI_HANDOFF.md，并严格按其中协议工作。
本次任务：检查当前 Week 进度并确定下一步。
具备 GitHub 写权限时，核对后直接更新仓库并提交。
```

需要制定下一周时，把最后两句替换为：

```text
本次任务：复盘当前 Week，并制定下一个 Week。
具备 GitHub 写权限时，直接创建或更新相应文件并提交。
```

## 一、唯一事实来源

1. 以 GitHub `main` 分支中的 Markdown 为准，不以聊天记忆为准。
2. 用户在当前会话提供的新事实优先于仓库旧记录，但必须同步回仓库。
3. 勾选项、Commit、PR、测试、Trace、截图、案例报告等，才是完成证据。
4. 没有证据时，可以记录为“已实现待验证”，不能升级为“已掌握”。
5. 不重新发明整套路线；除非用户明确要求，否则保持现有优先级。
6. 当能力尚未达到独立水平时，不得跳过学习包和引导实验直接布置开放式案例。

## 二、接管时读取顺序

```text
AI_HANDOFF.md
→ CURRENT_STATUS.md
→ CURRENT_STATUS 指向的 weeks/ 当前周文件
→ CURRENT_STATUS 的 current_learning 指向的学习文档（如存在）
→ CURRENT_STATUS 指向的 quarters/ 当前季度文件
→ PROFILE.md
→ ROADMAP.md
→ WORKFLOW.md
→ LEARNING_SYSTEM.md
→ SKILL_MATRIX.md / FEATURE_MATRIX.md
→ 与本次任务有关的 projects/ cases/ evidence/
```

不要一开始遍历所有文件。先根据 `CURRENT_STATUS.md` 缩小范围。

## 三、如何确定当前 Week

按以下顺序判断：

1. 优先读取 `CURRENT_STATUS.md` 的 `active_week`。
2. 核对该周文件的 `start`、`end` 是否与当前日期一致。
3. 状态含义：
   - `planned`：尚未开始；
   - `active`：执行中；
   - `review`：等待复盘；
   - `closed`：已结束。
4. 如果状态页过期，读取 `weeks/` 中日期最新的文件，并明确指出状态不一致。
5. 没有完成本周复盘前，不自动创建下一周，除非用户明确要求提前规划。

## 四、检查本周进度

先依据仓库形成四类结果：

```text
已完成：任务已勾选，并存在必要证据
部分完成：有代码或结果，但验收条件未满足
阻塞：存在明确问题，当前无法继续
未开始：没有记录或证据
```

执行步骤：

1. 读取当前周所有交付物和完成标准。
2. 如果周任务链接了 `learning/` 文档，检查用户是否完成对应观察、解释和证据。
3. 检查对应项目、案例和证据链接。
4. 只向用户确认仓库无法判断的差异，不要求重复描述已记录内容。
5. 更新当前周的复选框、阻塞、复盘和状态。
6. 更新 `CURRENT_STATUS.md` 中的下一步、阻塞、当前学习和最后变更。
7. 只有证据充分时才更新 `SKILL_MATRIX.md` 或 `FEATURE_MATRIX.md`。
8. 提交建议：`docs: update 2026-Wxx progress`。

## 五、确定“下一个任务”

当用户要求继续执行而不是制定新周时：

1. 从当前周尚未完成的交付物中选择任务。
2. 优先选择能在一次工作时段内形成闭环的最小步骤。
3. 不开启当前周明确排除的新方向。
4. 先判断用户是否已经具备执行该任务所需的工具和基础：
   - 已具备：直接进入最小交付；
   - 尚不具备：先读取或创建对应学习包和引导实验。
5. 输出必须包含：

```text
任务目标
→ 需要先理解的最小内容
→ 需要完成的代码或操作
→ 工具中具体观察什么
→ 验收条件
→ 需要留下的证据
→ 完成后更新哪些仓库文件
```

6. 将唯一下一步和 `current_learning` 写入 `CURRENT_STATUS.md`，避免多个会话各自制定不同任务。

## 六、制定下一个 Week

必须先完成当前周复盘，然后：

1. 从当前季度目标中选择，不脱离 `ROADMAP.md`。
2. 使用 `templates/weekly-plan.md` 创建 `weeks/YYYY-Www.md`。
3. 每周最多三个交付物：
   - 一个 Android 深度任务；
   - 一个 Flutter 或 React Native 主攻任务；
   - 一个维护或扩展任务。
4. Flutter 与 React Native 战略优先级一致，但按 Sprint 交替主攻。
5. iOS、HarmonyOS、Vue、Java 后端按计划轮换，不在同一周全面展开。
6. 每个交付物都必须有可验证完成标准和证据要求。
7. 新工具或新能力必须链接 `learning/` 学习文档；没有时先创建学习包。
8. 不使用空泛的“学习某技术”作为任务名称，必须落到可解释、可运行、可验证的实验或工程成果。
9. 同步更新：
   - `CURRENT_STATUS.md`；
   - `00-Dashboard.md` 的当前周与当前学习链接；
   - 必要时更新当前季度文件。
10. 提交建议：`plan: add 2026-Wxx execution week`。

## 七、每次会话结束前必须做的事

```text
1. 更新当前 Week 的真实进度
2. 更新 CURRENT_STATUS.md
3. 补充 Commit / PR / 案例 / 证据链接
4. 确认没有错误升级技能等级
5. 确认 current_learning 和唯一下一步仍然准确
6. 提交到 main，或在无写权限时提供完整补丁
```

## 八、禁止事项

- 不因新会话而从零重新规划。
- 不擅自改变 Android、Flutter、RN 等既定优先级。
- 不同时创建大量课程和任务。
- 不把 AI 生成并成功运行等同于独立掌握。
- 不在不会使用工具时只要求用户提交最终案例。
- 不提交公司内部资料、真实用户数据、Token、密钥或未脱敏日志。
- 不删除历史周计划；历史文件是进度证据。

## 九、常用会话指令

### 检查本周

```text
读取 AI_HANDOFF.md 和 CURRENT_STATUS.md，检查当前 Week 的仓库记录。
如果 CURRENT_STATUS 存在 current_learning，同时检查对应学习文档的观察和证据要求。
先按“已完成 / 部分完成 / 阻塞 / 未开始”汇总，再只确认仓库无法判断的信息。
确认后更新 Week 与 CURRENT_STATUS，并提交。
```

### 给出现在要做的一件事

```text
读取当前 Week、CURRENT_STATUS.current_learning 和 LEARNING_SYSTEM.md。
从未完成内容中选择一个最小闭环任务。
不要默认我已经会工具；给出最小知识、具体观察项、步骤、验收条件和证据要求，
并把它写入 CURRENT_STATUS.md。
```

### 制定下一周

```text
读取当前 Week 和季度目标，先完成周复盘，再根据 WORKFLOW.md 创建下一 Week。
最多三个交付物；新能力必须配套 learning/ 文档。
更新 Dashboard 与 CURRENT_STATUS，并提交。
```
