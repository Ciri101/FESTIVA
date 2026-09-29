# 文件改名与链接更新

## 范围

- 要交付：把 `truth/FESTIVA-高保真设计文档-草稿.md` 改名为 `truth/FESTIVA-高保真设计文档.md`，把 `truth/FESTIVA-工程架构文档-草稿.md` 改名为 `truth/FESTIVA-工程架构文档.md`；两份文档的一级标题去掉“（草稿）”，头部状态行写明“草稿”；更新 README.md、truth/goals.md、reference/README.md 中指向两份文档的链接与链接文字。
- 不包含：正文内容修订（归其他子任务）；已封存任务卷和机器账中的历史路径。
- 允许修改的位置：上述两份文档、README.md、truth/goals.md、reference/README.md。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 两份文档已改名，正文未变 | `git diff --cached -M` 查看改名与差异 | Git 识别为改名；除一级标题与状态行外正文无变化 |
| A2 | 链接可用 | 本地相对链接检查脚本 | README、goals.md、reference/README.md 与两份文档中无断链 |
| A3 | 无残留旧路径 | `git grep` 旧文件名 | 只出现在已封存任务卷与机器账中 |

验收安排：Agent 自检后交付；老师验收。
