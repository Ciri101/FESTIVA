# T0004 文件结构调整与链接更新：验证回执（重新交付）

执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替老师验收。上一轮回执（receipt-000022）只覆盖改名，已随整组撤回失去本轮通过资格。

## 改动（相对 T0004 开始前的提交 425eede）

- `truth/FESTIVA-工程架构文档-草稿.md` → `truth/FESTIVA-工程架构文档.md`
- `truth/FESTIVA-高保真设计文档-草稿.md` → `truth/ui/FESTIVA-高保真设计文档.md`
- 两份文档：一级标题去掉“（草稿）”，状态行以“草稿。”开头；UI 文档内 11 处指向 reference/ 的相对链接由 `../reference/` 改为 `../../reference/`。正文其余部分未改。
- README.md、truth/goals.md、reference/README.md：指向两份文档的链接改到新路径，链接文字去掉“（草稿）”。

## 验收项

- A1 通过：`git diff --cached -M --name-status 425eede -- truth` 显示工程文档为 R098 改名、UI 文档为 R085 移动；逐行差异只有一级标题、状态行和 11 处相对链接路径。
- A2 通过：对 README.md、truth/goals.md、reference/README.md、truth/ui/FESTIVA-高保真设计文档.md、truth/FESTIVA-工程架构文档.md 运行本地相对链接检查，共 24 条相对链接，断链 0。
- A3 通过（附说明）：排除 queue/tasks 与 .shell 后，`git grep` 旧文件名与旧位置无匹配（退出码 1）。旧路径仍出现在：机器账；已封存的 T0002；本任务 T0004 的记录；以及 T0006 被取代的旧批准基线 approval-001.md 与事件记录 task.md。后两处是工具生成的历史记录，不可也不应修改，性质与封存卷相同，但不在验收条件字面列出的范围内，请老师验收时知悉。

## 说明

- README.md 中“两份文档都标为草稿”、reference/README.md 中“见两份草稿”两句仍成立，留给 T0005 与父任务 T0003 的一致性检查处理。
- truth/FESTIVA-产品设计文档.md 尚未创建，归 T0006。
