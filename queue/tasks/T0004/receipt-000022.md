# T0004 文件改名与链接更新：验证回执

执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替老师验收。

## 改动

- `truth/FESTIVA-高保真设计文档-草稿.md` → `truth/FESTIVA-高保真设计文档.md`
- `truth/FESTIVA-工程架构文档-草稿.md` → `truth/FESTIVA-工程架构文档.md`
- 两份文档：一级标题去掉“（草稿）”；状态行改为以“草稿。”开头。正文其余部分未改。
- README.md、truth/goals.md、reference/README.md：更新指向两份文档的链接，链接文字去掉“（草稿）”。

## 验收项

- A1 通过：`git diff --cached -M --stat` 显示两份文档为改名（相似度 98%），差异只有第 1 行标题和状态行，共 5 个文件，9 行增、9 行删。
- A2 通过：对 README.md、truth/goals.md、reference/README.md 和两份文档运行本地相对链接检查，共 24 条相对链接，断链 0。
- A3 通过：`git grep` 排除 queue/tasks 与 .shell 后，旧文件名无匹配（退出码 1）。在全部受管文件中，旧文件名只出现在机器账、已封存的 T0002 卷，以及本任务 T0004 自己的任务记录中（描述本次改名），均为历史或本任务说明，不需要修改。

## 说明

- README.md 中“两份文档都标为草稿”和 reference/README.md 中“见两份草稿”两句仍然成立，属于状态描述，留给 T0005 和父任务 T0003 的一致性检查处理。
