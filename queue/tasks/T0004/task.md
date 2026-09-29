# 文件结构调整与链接更新

```json
{
  "id": "T0004",
  "revision": 31,
  "assignee": null,
  "parent": "T0003",
  "deps": [],
  "round": 2,
  "status": "批准"
}
```

## 登记依据

依据父任务 T0003 记录的裁决 F2（文件名去掉“草稿”，状态写在文档头部），以及老师 2026-09-29 的文档结构调整：高保真设计文档属于 UI 设计，移入老师新建的 truth/ui/。先把文件放到最终位置，后续子任务才能在最终路径上修订，避免重复改动引用。

本任务此前已按原范围完成改名并交付（回执 receipt-000022），随父任务整组撤回登记；已提交的改名保留，本次在其基础上补做移动。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [approval-002.md](approval-002.md)
- [receipt-000022.md](receipt-000022.md)

## 过程记录

- #12｜create｜claude｜{"authority": null, "deps": [], "id": "T0004", "parent": "T0003", "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 两份文档已改名，正文未变 | `git diff --cached -M` 查看改名与差异 | Git 识别为改名；除一级标题与状态行外正文无变化 |\n| A2 | 链接可用 | 本地相对链接检查脚本 | README、goals.md、reference/README.md 与两份文档中无断链 |\n| A3 | 无残留旧路径 | `git grep` 旧文件名 | 只出现在已封存任务卷与机器账中 |\n\n验收安排：Agent 自检后交付；老师验收。", "origin": "依据父任务 T0003 记录的裁决 F2：两份文档的文件名去掉“草稿”，状态写在文档头部。老师于 2026-09-29 采纳全部裁决并同意拆分。先改名，后续子任务才能在最终路径上修订，避免重复改动引用。", "plan": "1. 用 git mv 改名。\n2. 修改两份文档的一级标题与状态行。\n3. 更新三处链接。\n4. 运行检查并交付。", "scope": "- 要交付：把 `truth/FESTIVA-高保真设计文档-草稿.md` 改名为 `truth/FESTIVA-高保真设计文档.md`，把 `truth/FESTIVA-工程架构文档-草稿.md` 改名为 `truth/FESTIVA-工程架构文档.md`；两份文档的一级标题去掉“（草稿）”，头部状态行写明“草稿”；更新 README.md、truth/goals.md、reference/README.md 中指向两份文档的链接与链接文字。\n- 不包含：正文内容修订（归其他子任务）；已封存任务卷和机器账中的历史路径。\n- 允许修改的位置：上述两份文档、README.md、truth/goals.md、reference/README.md。", "title": "文件改名与链接更新"}}
- #17｜approve｜claude｜{"authority": {"basis": "当前对话 2026-09-29：老师指令“采纳全部裁决，登记任务开始修订”，并“同意拆分和依赖”", "by": "用户（老师）"}, "expect": 12, "id": "T0004"}
- #21｜claim｜claude｜{"expect": 17, "id": "T0004"}
- #22｜deliver｜claude｜{"artifacts": [{"path": "truth/FESTIVA-高保真设计文档.md", "sha256": "8e88b6b988f4abfd37323a3d2e2020a6ba71e5ba47b1e40c118cfcc7414ab7b7"}, {"path": "truth/FESTIVA-工程架构文档.md", "sha256": "9232651b504e632c8cf5a9bc147af0e1823793f6bfe9e7875f0f528548b55fff"}, {"path": "README.md", "sha256": "7a0040e63cbada143a7763a15960f7ce218e0e34e6bceb76f2ffa7c0b93959d1"}, {"path": "truth/goals.md", "sha256": "37628fbe9f33ab2dc5de8777c6aa0b47ffe6726f8be79e5c94f886afd69ea18c"}, {"path": "reference/README.md", "sha256": "c49707d41f8e56f994deb50d4071321d88a1a6b7c06735edc058d5b8c950ba55"}], "expect": 21, "id": "T0004", "receipt": "# T0004 文件改名与链接更新：验证回执\n\n执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替老师验收。\n\n## 改动\n\n- `truth/FESTIVA-高保真设计文档-草稿.md` → `truth/FESTIVA-高保真设计文档.md`\n- `truth/FESTIVA-工程架构文档-草稿.md` → `truth/FESTIVA-工程架构文档.md`\n- 两份文档：一级标题去掉“（草稿）”；状态行改为以“草稿。”开头。正文其余部分未改。\n- README.md、truth/goals.md、reference/README.md：更新指向两份文档的链接，链接文字去掉“（草稿）”。\n\n## 验收项\n\n- A1 通过：`git diff --cached -M --stat` 显示两份文档为改名（相似度 98%），差异只有第 1 行标题和状态行，共 5 个文件，9 行增、9 行删。\n- A2 通过：对 README.md、truth/goals.md、reference/README.md 和两份文档运行本地相对链接检查，共 24 条相对链接，断链 0。\n- A3 通过：`git grep` 排除 queue/tasks 与 .shell 后，旧文件名无匹配（退出码 1）。在全部受管文件中，旧文件名只出现在机器账、已封存的 T0002 卷，以及本任务 T0004 自己的任务记录中（描述本次改名），均为历史或本任务说明，不需要修改。\n\n## 说明\n\n- README.md 中“两份文档都标为草稿”和 reference/README.md 中“见两份草稿”两句仍然成立，属于状态描述，留给 T0005 和父任务 T0003 的一致性检查处理。\n", "summary": "两份文档改为不带“草稿”的文件名，状态写在头部；README、goals.md、reference/README.md 链接已更新，链接检查无断链", "verification": "passed"}
- #23｜revoke｜claude｜{"authority": {"basis": "当前对话 2026-09-29：老师“确认结构和分工，授权撤回重新批准”——文档结构调整为产品设计文档与工程架构文档两份核心文档，高保真设计文档移入 truth/ui/，新增 UI 设计文档修订子任务", "by": "用户（老师）"}, "expect": 16, "expect_seq": 22, "id": "T0003", "tree": true}
- #25｜revise｜claude｜{"basis": "当前对话 2026-09-29：老师“确认结构和分工，授权撤回重新批准”——核心文档为产品设计与工程架构，高保真设计文档移入 truth/ui/", "deps": [], "expect": 23, "id": "T0004", "parent": "T0003", "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 文件位于最终位置，正文未变 | 与改名前版本（提交 425eede）做 `git diff -M` | Git 识别为改名或移动；除一级标题、状态行和相对链接路径外正文无变化 |\n| A2 | 链接可用 | 本地相对链接检查脚本 | README、goals.md、reference/README.md 与两份文档中无断链 |\n| A3 | 无残留旧路径 | `git grep` 旧文件名与旧位置 | 只出现在已封存任务卷、机器账和本任务自己的记录中 |\n\n验收安排：Agent 自检后交付；老师验收。", "origin": "依据父任务 T0003 记录的裁决 F2（文件名去掉“草稿”，状态写在文档头部），以及老师 2026-09-29 的文档结构调整：高保真设计文档属于 UI 设计，移入老师新建的 truth/ui/。先把文件放到最终位置，后续子任务才能在最终路径上修订，避免重复改动引用。\n\n本任务此前已按原范围完成改名并交付（回执 receipt-000022），随父任务整组撤回登记；已提交的改名保留，本次在其基础上补做移动。", "plan": "1. 保留已提交的改名。\n2. 用 git mv 把高保真设计文档移入 truth/ui/，修正文档内部相对链接。\n3. 更新三处入口链接。\n4. 运行检查并重新交付。", "scope": "- 要交付：两份文档使用不带“草稿”的文件名，一级标题去掉“（草稿）”，头部状态行写明“草稿”（已完成，保留）；把 `truth/FESTIVA-高保真设计文档.md` 移到 `truth/ui/FESTIVA-高保真设计文档.md`，并修正该文档内部指向 reference/ 的相对链接；更新 README.md、truth/goals.md、reference/README.md 中指向两份文档的链接。\n- 不包含：正文内容修订（归其他子任务）；新建产品设计文档（归产品设计文档编写任务）；已封存任务卷和机器账中的历史路径。\n- 允许修改的位置：truth/FESTIVA-工程架构文档.md、truth/FESTIVA-高保真设计文档.md 及其移入 truth/ui/ 后的新路径、README.md、truth/goals.md、reference/README.md。", "title": "文件结构调整与链接更新"}}
- #31｜approve｜claude｜{"authority": {"basis": "当前对话 2026-09-29：老师“确认结构和分工，授权撤回重新批准”（此前已“采纳全部裁决，登记任务开始修订”并“同意拆分和依赖”）", "by": "用户（老师）"}, "expect": 25, "id": "T0004"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
