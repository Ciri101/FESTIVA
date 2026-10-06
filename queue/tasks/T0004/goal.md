# 文件结构调整与链接更新

## 范围

- 要交付：两份文档使用不带“草稿”的文件名，一级标题去掉“（草稿）”，头部状态行写明“草稿”（已完成，保留）；把 `truth/FESTIVA-高保真设计文档.md` 移到 `truth/ui/FESTIVA-高保真设计文档.md`，并修正该文档内部指向 reference/ 的相对链接；更新 README.md、truth/goals.md、reference/README.md 中指向两份文档的链接。
- 不包含：正文内容修订（归其他子任务）；新建产品设计文档（归产品设计文档编写任务）；已封存任务卷和机器账中的历史路径。
- 允许修改的位置：truth/FESTIVA-工程架构文档.md、truth/FESTIVA-高保真设计文档.md 及其移入 truth/ui/ 后的新路径、README.md、truth/goals.md、reference/README.md。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 文件位于最终位置，正文未变 | 与改名前版本（提交 425eede）做 `git diff -M` | Git 识别为改名或移动；除一级标题、状态行和相对链接路径外正文无变化 |
| A2 | 链接可用 | 本地相对链接检查脚本 | README、goals.md、reference/README.md 与两份文档中无断链 |
| A3 | 无残留旧路径 | `git grep` 旧文件名与旧位置 | 只出现在已封存任务卷、机器账和本任务自己的记录中 |

验收安排：Agent 自检后交付；老师验收。
