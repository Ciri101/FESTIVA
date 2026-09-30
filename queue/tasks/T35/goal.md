# 升级根契约：借 envshell 骨架，全局规则归一处

## 范围

- 要交付：
  - 根目录 AGENTS.md 改写为“FESTIVA 根契约”，分六节：身份、地图（含事实住址）、开工三步、规则、命令、附表（用语）。
  - 规则一节收录：charter 原 8 条基本约定；原入口“开始前”“执行与收尾”各条；协作纪律（原 T34 的内容，恢复原文第一句，改指本仓的“汇报说人话”）；新增上述四条纪律。每条标明把守方式。
  - charter/AGENTS.md 改为只管 config.json 与修改常设规则的手续。
  - 随之更新的措辞：各区契约末尾“返回公共入口”改称根契约；README 的“文件夹用途”表改为指向根契约第 2 节；tool/queue-usage.md 中常设规则的去处与需单独阅读的规则文件两句；tool/AGENTS.md 的模板差异清单补记这一处。
- 不包含：truth 文档；队列工具与制图工具的代码；引入 codex 调用工具；推送到 GitHub。
- 允许修改的位置：AGENTS.md、charter/AGENTS.md、README.md、tool/queue-usage.md、tool/AGENTS.md；以及 truth/AGENTS.md、truth/architecture/AGENTS.md、object/AGENTS.md、queue/AGENTS.md、gate/AGENTS.md、eval/AGENTS.md、reference/AGENTS.md、tool/diagram/AGENTS.md 末尾的返回链接；队列文件经工具维护。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 根契约六节齐全 | 阅读 AGENTS.md | 身份、地图、开工三步、规则、命令、附表六节在位；每条规则标明把守方式 |
| A2 | 原有规则一条不丢 | 回执附新旧对照表：charter 原 8 条与“修改本区”、原入口各条、协作纪律逐条对应到新位置 | 每条都有落点；协作纪律除恢复的首句外与 T34 交付的文字一致 |
| A3 | 四条纪律按决定写入 | 阅读规则一节 | 汇报说人话、验证代跑与汇报、验收余项一次清、子代理派发在位；子代理派发按任务形态写，Claude Code 与 Codex 通用，不设异源评审 |
| A4 | charter 只留配置与改规则手续 | 阅读 charter/AGENTS.md | 不再有全局规则正文 |
| A5 | 旧称已全仓替换、链接可用 | 全仓检索“公共入口”“协作边界”（任务历史除外）；本地相对链接检查 | 零命中；改动文件无断链 |
| A6 | 未越界、无违禁字符、队列可用 | `git diff --stat`；检索 U+00A7；`python3 gate/test_task_queue.py`；`python3 tool/shell.py doctor` | 只改允许的位置；零命中；测试通过；protection: ready |
| A7 | 不写协作者身份 | 检查新增文字 | 执行者只写工具名，不写人员身份与关系 |

验收安排：Agent 自检后交付，标“未独立验证”；用户验收。
