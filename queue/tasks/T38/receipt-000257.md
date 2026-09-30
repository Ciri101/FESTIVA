# T38 交付回执：根契约三处补正

- 执行：claude，2026-09-30
- 自检结论：passed。未独立验证。

## 改动

- AGENTS.md 第 5 节“队列工具测试”：命令改为 `python3 -B -m unittest discover -s gate -p 'test_*.py'`，说明注明含队列与状态包两组、约 3 分钟。
- gate/AGENTS.md：集成测试指引改为指向队列回归、状态包回归两组测试与 gate/checks.md 的命令。
- AGENTS.md 第 17 条：补入“zsh 里别用 `echo` 输出等号开头的整行，开头的 `=` 会被当作查命令路径展开而报错，分隔线加引号”；依据句补指本任务。
- AGENTS.md 第 11 条：补入“用户要求收尾交接时，交接说明在最后一件任务通过之前用 `task handoff` 写进该任务”；把守补“交接时机靠自觉”。放在第 11 条而不是先前建议的第 22 条：第 11 条管收尾，第 22 条是子代理一组里的上下文占用交接。

## 验收标准逐条

| 编号 | 结果 | 证据 |
|---|---|---|
| A1 | 满足 | 在仓库根实跑 `python3 -B -m unittest discover -s gate -p 'test_*.py'`：Ran 90 tests，OK，退出码 0 |
| A2 | 满足 | 根契约第 5 节、gate/AGENTS.md 与 gate/checks.md 第 7 行的命令一致，都覆盖两组测试 |
| A3 | 满足 | 第 11、17 条已写入并标明把守；第 4 节规则仍为 1–22 条。zsh 说法实测：`zsh -c 'echo ====='` 输出 `zsh:1: ==== not found`，退出码 1；加引号的 `echo '====='` 输出 `=====`，退出码 0 |
| A4 | 交付后写入 | 交付后用 `task handoff T38` 写入本会话交接说明，见任务视图“接手说明” |
| A5 | 满足 | `git diff --name-only` 只有 AGENTS.md、gate/AGENTS.md 与机器账；两文件 40 个相对链接，断链 0；U+00A7 零命中；`python3 tool/shell.py doctor`：protection ready，退出码 0 |

## 未验证

- 没有独立审阅者核对，以上读数都是执行者自报。
- 本地提交，未推送。
