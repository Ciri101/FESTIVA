# 更新 README 与参考资料说明中过时的正文

```json
{
  "id": "T0011",
  "revision": 76,
  "assignee": null,
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "批准"
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

## 过程记录

- #76｜create｜claude｜{"authority": {"basis": "当前对话 2026-09-29：T0003 集成检查中，老师对“README 与 reference/README 的三处过时正文超出 T0003 范围，怎么处理”选择“另立 T0011：现在登记并批准一个小任务，只改这三处正文，T0003 之后接着做”", "by": "用户（老师）"}, "deps": [], "id": "T0011", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 三处正文已更新 | 阅读 README.md 与 reference/README.md | 不再有“两份文档”“两份草稿”的说法；没有个人电脑路径 |\n| A2 | 没有改动其他内容 | `git diff` 两个文件 | 只有上述三处变化（T0003 已提交的链接改动不计） |\n| A3 | 链接可用 | 本地相对链接检查 | 两个文件无断链 |\n\n验收安排：Agent 自检后交付；老师验收。", "origin": "T0003 集成检查中发现三处过时正文，不是链接，超出 T0003 批准范围（只允许改 README.md 与 reference/README.md 中的链接）。老师于 2026-09-29 在当前对话中选择“另立 T0011”：登记并批准一个小任务，只改这三处正文，T0003 之后接着做。\n\n1. README.md 第 12 行“两份文档都标为草稿……”：现在 truth/ 有四份文档，状态各不相同（产品设计文档第 1–10 节与 UI 设计文档第 1–4 节、附录 A、B 已确认，工程架构文档与 Demo 架构方案为草稿）。\n2. README.md“项目如何协作”一段写“此机器的系统 python3 是 3.9”，并给出指向学生电脑的 Python 路径（/Users/shixinyue/…）；在其他机器上不成立，也不应出现在开源仓库中。\n3. reference/README.md 末句“相关未确定事项见两份草稿”：同样按旧的两份文档表述。", "plan": "1. 等 T0003 交付后领取。\n2. 按范围修改三处正文，运行检查并交付。", "scope": "- 要交付：\n  1. README.md 第 12 行：改为说明各文档逐节标注状态，确认前的内容不是已批准的决定。不写具体哪些章节已确认，避免与各文档头部重复维护。\n  2. README.md 的 Python 说明：改为“队列需要 Python 3.10+ 和 Git；系统 python3 低于 3.10 时，用任意 3.10+ 的解释器运行”，示例命令用 `python3 tool/shell.py doctor`，删除个人电脑路径。\n  3. reference/README.md 末句：改为未确定事项见 truth/ 中各文档的待确认章节。\n- 不包含：README.md 与 reference/README.md 的其他内容（链接由 T0003 处理）；根目录 AGENTS.md 中“此机器可用的 Python 3.12 路径见 README”一句（属于公共入口，需老师另行决定）。\n- 允许修改的位置：README.md、reference/README.md，仅限上述三处正文。", "title": "更新 README 与参考资料说明中过时的正文"}}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
