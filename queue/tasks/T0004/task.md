# 文件改名与链接更新

```json
{
  "id": "T0004",
  "revision": 17,
  "assignee": null,
  "parent": "T0003",
  "deps": [],
  "round": 1,
  "status": "批准"
}
```

## 登记依据

依据父任务 T0003 记录的裁决 F2：两份文档的文件名去掉“草稿”，状态写在文档头部。老师于 2026-09-29 采纳全部裁决并同意拆分。先改名，后续子任务才能在最终路径上修订，避免重复改动引用。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)

## 过程记录

- #12｜create｜claude｜{"authority": null, "deps": [], "id": "T0004", "parent": "T0003", "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 两份文档已改名，正文未变 | `git diff --cached -M` 查看改名与差异 | Git 识别为改名；除一级标题与状态行外正文无变化 |\n| A2 | 链接可用 | 本地相对链接检查脚本 | README、goals.md、reference/README.md 与两份文档中无断链 |\n| A3 | 无残留旧路径 | `git grep` 旧文件名 | 只出现在已封存任务卷与机器账中 |\n\n验收安排：Agent 自检后交付；老师验收。", "origin": "依据父任务 T0003 记录的裁决 F2：两份文档的文件名去掉“草稿”，状态写在文档头部。老师于 2026-09-29 采纳全部裁决并同意拆分。先改名，后续子任务才能在最终路径上修订，避免重复改动引用。", "plan": "1. 用 git mv 改名。\n2. 修改两份文档的一级标题与状态行。\n3. 更新三处链接。\n4. 运行检查并交付。", "scope": "- 要交付：把 `truth/FESTIVA-高保真设计文档-草稿.md` 改名为 `truth/FESTIVA-高保真设计文档.md`，把 `truth/FESTIVA-工程架构文档-草稿.md` 改名为 `truth/FESTIVA-工程架构文档.md`；两份文档的一级标题去掉“（草稿）”，头部状态行写明“草稿”；更新 README.md、truth/goals.md、reference/README.md 中指向两份文档的链接与链接文字。\n- 不包含：正文内容修订（归其他子任务）；已封存任务卷和机器账中的历史路径。\n- 允许修改的位置：上述两份文档、README.md、truth/goals.md、reference/README.md。", "title": "文件改名与链接更新"}}
- #17｜approve｜claude｜{"authority": {"basis": "当前对话 2026-09-29：老师指令“采纳全部裁决，登记任务开始修订”，并“同意拆分和依赖”", "by": "用户（老师）"}, "expect": 12, "id": "T0004"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
