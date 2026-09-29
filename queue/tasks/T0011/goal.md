# 更新 README 与参考资料说明中过时的正文

## 范围

- 要交付：
  1. README.md 第 12 行：改为说明各文档逐节标注状态，确认前的内容不是已批准的决定。不写具体哪些章节已确认，避免与各文档头部重复维护。
  2. README.md 的 Python 说明：改为“队列需要 Python 3.10+ 和 Git；系统 python3 低于 3.10 时，用任意 3.10+ 的解释器运行”，示例命令用 `python3 tool/shell.py doctor`，删除个人电脑路径。
  3. reference/README.md 末句：改为未确定事项见 truth/ 中各文档的待确认章节。
- 不包含：README.md 与 reference/README.md 的其他内容（链接由 T0003 处理）；根目录 AGENTS.md 中“此机器可用的 Python 3.12 路径见 README”一句（属于公共入口，需老师另行决定）。
- 允许修改的位置：README.md、reference/README.md，仅限上述三处正文。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 三处正文已更新 | 阅读 README.md 与 reference/README.md | 不再有“两份文档”“两份草稿”的说法；没有个人电脑路径 |
| A2 | 没有改动其他内容 | `git diff` 两个文件 | 只有上述三处变化（T0003 已提交的链接改动不计） |
| A3 | 链接可用 | 本地相对链接检查 | 两个文件无断链 |

验收安排：Agent 自检后交付；老师验收。
