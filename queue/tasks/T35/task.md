# 升级根契约：借 envshell 骨架，全局规则归一处

```json
{
  "id": "T35",
  "revision": 245,
  "assignee": "claude",
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "交付"
}
```

## 登记依据

2026-09-30，用户在当前对话中要求：初始化后摸底 envshell 仓的根契约（该仓根目录 AGENTS.md，v1.91），然后升级本仓的根契约文档。

摸底结论：envshell 的根契约由机读正本渲染而成，分身份、地图、规则、命令、附表五部分；每条规则标明由谁把守（机器拒绝还是只靠自觉）；开工分三步并交固定格式的回执；另有几条实例级纪律。它的条款登记表、出厂件、发行、流水账、生成工具等机制本仓没有，不搬。

本仓现状的问题：根目录 AGENTS.md 写“常设规则归对应区域契约”，8 条跨区规则住 charter/AGENTS.md；而用户指明根契约是根目录 AGENTS.md，任务 T34 起初因此写错位置。本任务把全局规则收归根契约，消除这一分歧。

用户就方案作出的决定（当前对话）：

1. 取消 T34（协作纪律写入根契约，已交付、未验收），其内容并入本任务。
2. 全局规则全部进根契约；charter/AGENTS.md 只留 config.json 与修改常设规则的手续。
3. 手写 Markdown，借 envshell 的骨架，不引入机读正本与生成工具。
4. 搬入四条纪律：汇报说人话（envshell 称“两个世界，两套规矩”）、验证代跑与汇报、验收余项一次清、子代理派发。
5. 子代理派发：本仓的执行者有 Claude Code 与 Codex 两种，各自只用自家模型，不存在异源评审；规则按任务形态写，不绑定执行者。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000245.md](receipt-000245.md)

## 过程记录

- #243｜create｜claude｜{"authority": {"basis": "当前对话 2026-09-30：用户要求摸底 envshell 根契约后升级本仓根契约，并选定：取消 T34 并入；全局规则全部进根契约，charter 只留配置与改规则手续；手写 Markdown 借 envshell 骨架；搬入汇报说人话、验证代跑与汇报、验收余项一次清、子代理派发（按任务形态写，Claude Code 与 Codex 通用，不设异源评审）", "by": "用户"}, "deps": [], "id": "T35", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 根契约六节齐全 | 阅读 AGENTS.md | 身份、地图、开工三步、规则、命令、附表六节在位；每条规则标明把守方式 |\n| A2 | 原有规则一条不丢 | 回执附新旧对照表：charter 原 8 条与“修改本区”、原入口各条、协作纪律逐条对应到新位置 | 每条都有落点；协作纪律除恢复的首句外与 T34 交付的文字一致 |\n| A3 | 四条纪律按决定写入 | 阅读规则一节 | 汇报说人话、验证代跑与汇报、验收余项一次清、子代理派发在位；子代理派发按任务形态写，Claude Code 与 Codex 通用，不设异源评审 |\n| A4 | charter 只留配置与改规则手续 | 阅读 charter/AGENTS.md | 不再有全局规则正文 |\n| A5 | 旧称已全仓替换、链接可用 | 全仓检索“公共入口”“协作边界”（任务历史除外）；本地相对链接检查 | 零命中；改动文件无断链 |\n| A6 | 未越界、无违禁字符、队列可用 | `git diff --stat`；检索 U+00A7；`python3 gate/test_task_queue.py`；`python3 tool/shell.py doctor` | 只改允许的位置；零命中；测试通过；protection: ready |\n| A7 | 不写协作者身份 | 检查新增文字 | 执行者只写工具名，不写人员身份与关系 |\n\n验收安排：Agent 自检后交付，标“未独立验证”；用户验收。", "origin": "2026-09-30，用户在当前对话中要求：初始化后摸底 envshell 仓的根契约（该仓根目录 AGENTS.md，v1.91），然后升级本仓的根契约文档。\n\n摸底结论：envshell 的根契约由机读正本渲染而成，分身份、地图、规则、命令、附表五部分；每条规则标明由谁把守（机器拒绝还是只靠自觉）；开工分三步并交固定格式的回执；另有几条实例级纪律。它的条款登记表、出厂件、发行、流水账、生成工具等机制本仓没有，不搬。\n\n本仓现状的问题：根目录 AGENTS.md 写“常设规则归对应区域契约”，8 条跨区规则住 charter/AGENTS.md；而用户指明根契约是根目录 AGENTS.md，任务 T34 起初因此写错位置。本任务把全局规则收归根契约，消除这一分歧。\n\n用户就方案作出的决定（当前对话）：\n\n1. 取消 T34（协作纪律写入根契约，已交付、未验收），其内容并入本任务。\n2. 全局规则全部进根契约；charter/AGENTS.md 只留 config.json 与修改常设规则的手续。\n3. 手写 Markdown，借 envshell 的骨架，不引入机读正本与生成工具。\n4. 搬入四条纪律：汇报说人话（envshell 称“两个世界，两套规矩”）、验证代跑与汇报、验收余项一次清、子代理派发。\n5. 子代理派发：本仓的执行者有 Claude Code 与 Codex 两种，各自只用自家模型，不存在异源评审；规则按任务形态写，不绑定执行者。", "plan": "1. 取消 T34，登记、批准并领取本任务，提交队列变更。\n2. 改写根契约与 charter，更新相关措辞。\n3. 跑检查，写回执（含新旧对照表），交付并提交；不推送。", "scope": "- 要交付：\n  - 根目录 AGENTS.md 改写为“FESTIVA 根契约”，分六节：身份、地图（含事实住址）、开工三步、规则、命令、附表（用语）。\n  - 规则一节收录：charter 原 8 条基本约定；原入口“开始前”“执行与收尾”各条；协作纪律（原 T34 的内容，恢复原文第一句，改指本仓的“汇报说人话”）；新增上述四条纪律。每条标明把守方式。\n  - charter/AGENTS.md 改为只管 config.json 与修改常设规则的手续。\n  - 随之更新的措辞：各区契约末尾“返回公共入口”改称根契约；README 的“文件夹用途”表改为指向根契约第 2 节；tool/queue-usage.md 中常设规则的去处与需单独阅读的规则文件两句；tool/AGENTS.md 的模板差异清单补记这一处。\n- 不包含：truth 文档；队列工具与制图工具的代码；引入 codex 调用工具；推送到 GitHub。\n- 允许修改的位置：AGENTS.md、charter/AGENTS.md、README.md、tool/queue-usage.md、tool/AGENTS.md；以及 truth/AGENTS.md、truth/architecture/AGENTS.md、object/AGENTS.md、queue/AGENTS.md、gate/AGENTS.md、eval/AGENTS.md、reference/AGENTS.md、tool/diagram/AGENTS.md 末尾的返回链接；队列文件经工具维护。", "title": "升级根契约：借 envshell 骨架，全局规则归一处"}}
- #244｜claim｜claude｜{"expect": 243, "id": "T35"}
- #245｜deliver｜claude｜{"artifacts": [{"path": "AGENTS.md", "sha256": "4fbd2d91a598ca37157dec57ad78de0b7df3070b7e596f9b1f4efb6f4c77509e"}, {"path": "charter/AGENTS.md", "sha256": "aa7b47a6bbf066abb47400d1079056d5f15b8cd288383d02eb190147586ba183"}, {"path": "README.md", "sha256": "96f628c28cfdad14ba8b5477a7687c3bb97d343e6099f8e1aa76b02d726e8483"}, {"path": "tool/queue-usage.md", "sha256": "ed5e92da9df7f1e2d10a0d1c6dd95828bfd65f995cff2091cb3ed17e2fda9470"}, {"path": "tool/AGENTS.md", "sha256": "c77e550dd501eaf7867f9e25ba51ceaa2e82b6ad29d86d87b4dc9ac6616eb5c2"}, {"path": "truth/AGENTS.md", "sha256": "d4fe8ad4484afb5c636d99a7192dea0b0e06dae686c6339294d095d923396681"}, {"path": "truth/architecture/AGENTS.md", "sha256": "3981120c7e720425bcf143881e07f44510941f71e70eb411305618c6214d1a1e"}, {"path": "object/AGENTS.md", "sha256": "af2200a28811094ac959a08a0fc4bc9d305da976e5c5cb96c200a8af72d1e47e"}, {"path": "queue/AGENTS.md", "sha256": "a6f148accfca96212cc3f742e703375e102f018605eb42a4fef99275e986af5c"}, {"path": "gate/AGENTS.md", "sha256": "280bef33a08cdd427de2239c1f649142d5031235b336f193fdc20810150e9093"}, {"path": "eval/AGENTS.md", "sha256": "264c2c874cf8b45de1d2b53fcdca2b001a49c4727e34326775b1769ccaa725b2"}, {"path": "reference/AGENTS.md", "sha256": "e9874f726b99c377b9367832a5f80da735a439f8889303fbf6cb28f158d5185a"}, {"path": "tool/diagram/AGENTS.md", "sha256": "8b6916ede6d11f676b664ca1ecab8187efcc059854f03e9cc7097f7a2aaad2bb"}], "expect": 244, "id": "T35", "receipt": "# T35 交付回执：升级根契约\n\n- 执行：claude，2026-09-30\n- 自检结论：passed。未独立验证。\n\n## 写入\n\n- 根目录 AGENTS.md 改写为“FESTIVA 根契约”，六节：1 身份、2 地图（含事实住址）、3 开工三步、4 规则（22 条，分授权与边界、任务与队列、记录与汇报、协作纪律、子代理派发五组，每条标明把守方式）、5 命令、6 附表：用语。\n- charter/AGENTS.md 改为“配置与规则变更”：只管 config.json 与修改常设规则的手续。\n- 九份区契约末尾的“返回公共入口”改为“返回根契约”；README 的“文件夹用途”表改为指向根契约第 2 节；tool/queue-usage.md 两句改指根契约；tool/AGENTS.md 的模板差异清单补记这一处。\n\n## 新旧对照（A2）\n\n| 原位置与内容 | 新位置 |\n|---|---|\n| 原入口开头：用户下指令、Agent 代书，不要求用户编辑机器账或重复批准 | 第 4 节第 1 条 |\n| 原入口开头：仓库以文档和参考图为主，草稿不当已实现 | 根契约开头段 |\n| 原入口开头：Python 3.10+，低于时见 README | 第 1 节“任务管线” |\n| 开始前 1：读 charter、object、goals；核对指令、位置、可写范围；常设规则与单次授权的归属；不猜权限；不另建接入表 | 第 3 节第一步第 3 项（goals 经状态包送达，charter 改为改规则或配置前读）、第二步第 3 项；第 2 节事实住址；第 13 条 |\n| 开始前 2：读队列规则与用法，doctor 的期望值，未初始化的做法 | 第 3 节第一步第 1、3 项 |\n| 开始前 3：state get 读完全文、正文范围；task status；没有任务时登记，已授权可一并记录 | 第 3 节第一步第 2 项、第二步第 1、3 项 |\n| 开始前 4：汇报本轮任务、所读、冲突与下一步；触及某区前读该区契约 | 第 3 节第三步；第二步第 2 项 |\n| 执行与收尾 1、2：机器账由工具维护；经工具操作、稳定请求号与重试 | 第 7 条 |\n| 执行与收尾 3：携带读过的 context；多个 Agent 同一主工作树；对象并行须协调 | 第 8、9 条 |\n| 执行与收尾 4：验证事实与用户验收分开 | 第 10 条 |\n| 执行与收尾 5：收尾同批暂存、不绕过钩子 | 第 11 条 |\n| 协作纪律（T34） | 第 17 条：正文一字未改；恢复原文首句，改指第 14 条；依据改指 T35 |\n| 原入口结尾：人类读者从 README 开始；上级优先、冲突说明、不用模板扩大授权 | 根契约开头段；第 2 条 |\n| charter 开头：常设规则在本契约，区专属归区，不另建接入表，不存进度与设计 | 根契约开头段；charter 新开头；第 13 条 |\n| charter 第 1 条 授权归用户 | 第 1 条 |\n| charter 第 2 条 一件事实只维护一处（事实住址、config 与状态包） | 第 2 节事实住址；第 13 条；config 部分在 charter“config.json”一节 |\n| charter 第 3 条 按任务工作 | 第 6 条 |\n| charter 第 4 条 共享写入分两类 | 第 9 条 |\n| charter 第 5 条 事实与判断分开 | 第 12 条 |\n| charter 第 6 条 敏感内容不入记录 | 第 4 条（凭据）、第 3 条（外部动作） |\n| charter 第 7 条 规则也有边界 | 第 2 条 |\n| charter 第 8 条 不写协作者身份 | 第 5 条（文字不变，链接路径随位置调整） |\n| charter“修改本区”：核对已有契约、写入位置、占位表；安装联网等未授权不视为允许 | charter“修改常设规则”第 1 项；第 3 条 |\n| charter“修改本区”：新增或变更须用户同意、链接依据、不改成永久权限 | charter“修改常设规则”第 2 项 |\n| charter“修改本区”：上级优先；批准后更新规则 | 第 2 条；charter“修改常设规则”第 3 项 |\n\n新增内容：第 1 节身份、第 2 节地图、第 5 节命令、第 6 节用语；第 14 条汇报说人话、第 15 条验证代跑与汇报、第 16 条验收余项一次清；第 4.5 节子代理派发（第 18–22 条：按任务形态写，Claude Code 与 Codex 通用，不设异源评审，型号不写死；Codex 的多代理功能 `multi_agent` 已用 `codex features list` 核实为 stable）。\n\n行为上的一处变化：charter/AGENTS.md 不再有全局规则，所以不再列为每次开工必读，改为改规则或配置前读。\n\n## 验收标准逐条\n\n| 编号 | 结果 | 证据 |\n|---|---|---|\n| A1 | 满足 | AGENTS.md 六节在位；第 4 节 22 条规则各带“把守”说明（第 4.5 节在节首统一说明） |\n| A2 | 满足 | 上表逐条对照。协作纪律用脚本比对 T34 提交 6d2378f 中的原文：去掉新加的首句与依据句后，逐字一致（输出 `T34 正文（除依据句）一致： True`） |\n| A3 | 满足 | 第 14、15、16 条与第 18–22 条在位 |\n| A4 | 满足 | charter/AGENTS.md 只剩开头段、“config.json”“修改常设规则”两节 |\n| A5 | 满足 | 在任务历史 queue/tasks/ 与 .shell/ 以外检索“公共入口”“协作边界”：命中文件 0；13 个改动文件共 77 个相对链接，断链 0 |\n| A6 | 满足 | `git diff --stat` 只列 13 个允许的文件；已跟踪文件（任务历史与机器账除外）中 U+00A7 命中 0；`python3 gate/test_task_queue.py`：Ran 64 tests，OK，退出码 0；`python3 tool/shell.py doctor`：protection ready、protocol 2，退出码 0；另跑制图检查 `tool/diagram/check.mts`：(e)(w)(x) 三项绿，无红，退出码 0 |\n| A7 | 满足 | 检索新增行中的人员身份用语，只命中第 5 条规则本身的“上下级”一词；执行者只写 Claude Code 与 Codex |\n\n## 未验证\n\n- 没有独立审阅者核对，以上读数都是执行者自报。\n- 第 21 条列表项里的表格、各表在 GitHub 上的显示效果没有目检。\n- 本地提交，未推送。\n", "summary": "根契约按 envshell 骨架改写为六节，全局规则收归根契约（22 条，标明把守方式），charter 只留配置与改规则手续；并入 T34 的协作纪律", "verification": "passed"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
