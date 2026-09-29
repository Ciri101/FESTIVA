# 更新 README 与参考资料说明中过时的正文

```json
{
  "id": "T0011",
  "revision": 84,
  "assignee": null,
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "通过"
}
```

## 登记依据

T0003 集成检查中发现三处过时正文，不是链接，超出 T0003 批准范围（只允许改 README.md 与 reference/README.md 中的链接）。老师于 2026-09-29 在当前对话中选择“另立 T0011”：登记并批准一个小任务，只改这三处正文，T0003 之后接着做。

1. README.md 第 12 行“两份文档都标为草稿……”：现在 truth/ 有四份文档，状态各不相同（产品设计文档第 1–10 节与 UI 设计文档第 1–4 节、附录 A、B 已确认，工程架构文档与 Demo 架构方案为草稿）。
2. README.md“项目如何协作”一段写“此机器的系统 python3 是 3.9”，并给出指向学生电脑的 Python 路径（/Users/shixinyue/…）；在其他机器上不成立，也不应出现在开源仓库中。
3. reference/README.md 末句“相关未确定事项见两份草稿”：同样按旧的两份文档表述。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000083.md](receipt-000083.md)

## 过程记录

- #76｜create｜claude｜{"authority": {"basis": "当前对话 2026-09-29：T0003 集成检查中，老师对“README 与 reference/README 的三处过时正文超出 T0003 范围，怎么处理”选择“另立 T0011：现在登记并批准一个小任务，只改这三处正文，T0003 之后接着做”", "by": "用户（老师）"}, "deps": [], "id": "T0011", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 三处正文已更新 | 阅读 README.md 与 reference/README.md | 不再有“两份文档”“两份草稿”的说法；没有个人电脑路径 |\n| A2 | 没有改动其他内容 | `git diff` 两个文件 | 只有上述三处变化（T0003 已提交的链接改动不计） |\n| A3 | 链接可用 | 本地相对链接检查 | 两个文件无断链 |\n\n验收安排：Agent 自检后交付；老师验收。", "origin": "T0003 集成检查中发现三处过时正文，不是链接，超出 T0003 批准范围（只允许改 README.md 与 reference/README.md 中的链接）。老师于 2026-09-29 在当前对话中选择“另立 T0011”：登记并批准一个小任务，只改这三处正文，T0003 之后接着做。\n\n1. README.md 第 12 行“两份文档都标为草稿……”：现在 truth/ 有四份文档，状态各不相同（产品设计文档第 1–10 节与 UI 设计文档第 1–4 节、附录 A、B 已确认，工程架构文档与 Demo 架构方案为草稿）。\n2. README.md“项目如何协作”一段写“此机器的系统 python3 是 3.9”，并给出指向学生电脑的 Python 路径（/Users/shixinyue/…）；在其他机器上不成立，也不应出现在开源仓库中。\n3. reference/README.md 末句“相关未确定事项见两份草稿”：同样按旧的两份文档表述。", "plan": "1. 等 T0003 交付后领取。\n2. 按范围修改三处正文，运行检查并交付。", "scope": "- 要交付：\n  1. README.md 第 12 行：改为说明各文档逐节标注状态，确认前的内容不是已批准的决定。不写具体哪些章节已确认，避免与各文档头部重复维护。\n  2. README.md 的 Python 说明：改为“队列需要 Python 3.10+ 和 Git；系统 python3 低于 3.10 时，用任意 3.10+ 的解释器运行”，示例命令用 `python3 tool/shell.py doctor`，删除个人电脑路径。\n  3. reference/README.md 末句：改为未确定事项见 truth/ 中各文档的待确认章节。\n- 不包含：README.md 与 reference/README.md 的其他内容（链接由 T0003 处理）；根目录 AGENTS.md 中“此机器可用的 Python 3.12 路径见 README”一句（属于公共入口，需老师另行决定）。\n- 允许修改的位置：README.md、reference/README.md，仅限上述三处正文。", "title": "更新 README 与参考资料说明中过时的正文"}}
- #82｜claim｜claude｜{"expect": 76, "id": "T0011"}
- #83｜deliver｜claude｜{"artifacts": [{"path": "README.md", "sha256": "e36f9d2840bcfc1bd8c6aab847fee6671008864a7d3fc9ce424f6c5f2308d14f"}, {"path": "reference/README.md", "sha256": "63ab6f3f9460ace26a1f889cb43f6b847bbc69e2eee9b45e4de64b63161195bf"}], "expect": 82, "id": "T0011", "receipt": "# T0011 更新 README 与参考资料说明中过时的正文：验证回执\n\n执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替老师验收。\n\n## 改动\n\n1. README.md 第 14 行（登记时为第 12 行，T0003 在其上方加了两条链接）：“两份文档都标为草稿……”改为“各文档在头部和每节开头标注状态：标为‘已确认’的章节经过逐节确认；标为‘草稿’的章节和列出的待确认事项，在用户确认前都不是已批准的产品或技术决定。”没有写具体哪些章节已确认，避免与各文档头部重复维护。\n2. README.md“项目如何协作”：改为“队列需要 Python 3.10+ 和 Git；系统 python3 低于 3.10 时，用任意 3.10+ 的解释器运行”，示例命令改为 `python3 tool/shell.py doctor`；删除 /Users/shixinyue/… 个人电脑路径。\n3. reference/README.md 末句：“相关未确定事项见两份草稿”改为“相关未确定事项见 truth/ 中各文档的待确认章节”（truth/ 为相对链接）。\n\n## 验收标准逐项\n\n- A1 通过：`grep -n '两份\\|shixinyue\\|/Users/\\|3\\.9' README.md reference/README.md` 无结果。\n- A2 通过：`git diff -U0 README.md reference/README.md` 只显示 README 第 14、30、33 行与 reference/README 第 10 行，对应上述三处（第 2 处包括说明段和示例命令两行）。\n- A3 通过：本地相对链接检查 README.md 8 个、reference/README.md 7 个相对链接，退出码 0。\n\n## 范围外、需要老师决定\n\n根目录 AGENTS.md 写“实际运行队列时使用 Python 3.10+；此机器可用的 Python 3.12 路径见 README”。README 已不再给出具体路径，这句现在与 README 不一致。按批准范围未改。\n\n## 未验证\n\n没有独立审阅者核对；老师验收前，以上均为 Agent 自检。\n", "summary": "README 与 reference/README 三处过时正文已更新，删除个人电脑路径；Agent 自检 A1–A3 通过，未独立验证；根目录 AGENTS.md 的 Python 指针待老师决定", "verification": "passed"}
- #84｜close｜claude｜{"authority": {"basis": "当前对话 2026-09-29：老师回复“T0011 通过”", "by": "用户（老师）"}, "expect": 83, "id": "T0011"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
