# T0011 更新 README 与参考资料说明中过时的正文：验证回执

执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替老师验收。

## 改动

1. README.md 第 14 行（登记时为第 12 行，T0003 在其上方加了两条链接）：“两份文档都标为草稿……”改为“各文档在头部和每节开头标注状态：标为‘已确认’的章节经过逐节确认；标为‘草稿’的章节和列出的待确认事项，在用户确认前都不是已批准的产品或技术决定。”没有写具体哪些章节已确认，避免与各文档头部重复维护。
2. README.md“项目如何协作”：改为“队列需要 Python 3.10+ 和 Git；系统 python3 低于 3.10 时，用任意 3.10+ 的解释器运行”，示例命令改为 `python3 tool/shell.py doctor`；删除 /Users/shixinyue/… 个人电脑路径。
3. reference/README.md 末句：“相关未确定事项见两份草稿”改为“相关未确定事项见 truth/ 中各文档的待确认章节”（truth/ 为相对链接）。

## 验收标准逐项

- A1 通过：`grep -n '两份\|shixinyue\|/Users/\|3\.9' README.md reference/README.md` 无结果。
- A2 通过：`git diff -U0 README.md reference/README.md` 只显示 README 第 14、30、33 行与 reference/README 第 10 行，对应上述三处（第 2 处包括说明段和示例命令两行）。
- A3 通过：本地相对链接检查 README.md 8 个、reference/README.md 7 个相对链接，退出码 0。

## 范围外、需要老师决定

根目录 AGENTS.md 写“实际运行队列时使用 Python 3.10+；此机器可用的 Python 3.12 路径见 README”。README 已不再给出具体路径，这句现在与 README 不一致。按批准范围未改。

## 未验证

没有独立审阅者核对；老师验收前，以上均为 Agent 自检。
