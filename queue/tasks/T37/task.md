# 状态包缓存：清理旧版本，并让工具自动只留最近几份

```json
{
  "id": "T37",
  "revision": 254,
  "assignee": null,
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "通过"
}
```

## 登记依据

2026-09-30，用户在当前对话中问：`.shell/local/state/` 为什么有这么多记录。Agent 查明：

- `state get` 把每个版本的状态包存进单独的目录 `.shell/local/state/<版本号>-<分片尺寸>/`，队列工具（tool/state_pack.py、tool/task_queue.py）没有任何清理旧目录的代码。当时共 243 个目录、39 MB，对应机器账第 8 到 249 笔操作。
- 除当前状态的版本外，旧目录不会再被任何命令用到：写入时只接受当前版本。
- envshell 用固定文件名覆盖写，交接备忘另按保留份数轮转（history_keep），所以不堆积。
- 本仓不宜整体改成覆盖写：写入时工具要核对所带版本的缓存是否完整（`state_cache`，测试 test_10）；用法承诺不同分片尺寸独立保存（测试 test_11）；分目录还保证读到一半不会被换成新版本。

用户指令：“两样都做，登记成一件任务”——即手动清理一次现有旧目录，并改工具让它自动只留最近几份（当前对话）。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000253.md](receipt-000253.md)

## 过程记录

- #251｜create｜claude｜{"authority": {"basis": "当前对话 2026-09-30：用户就状态包缓存堆积的处理指令“两样都做，登记成一件任务”（手动清理一次旧目录＋改工具自动只留最近几份）", "by": "用户"}, "deps": [], "id": "T37", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 现有旧缓存已清理 | 改动前后各统计一次 `.shell/local/state/` 的目录数与大小 | 清理后只剩当前状态的版本与至多 2 个过期版本 |\n| A2 | 保留规则正确 | 新增回归测试 | 连续产生多个版本后，只剩预期的目录；最近 2 个过期版本仍在 |\n| A3 | 原有承诺不破 | `python3 gate/test_state_queue.py`；`python3 gate/test_task_queue.py` | 两组全部通过，含 test_10、test_11 |\n| A4 | 删除有边界、失败不拦取包 | 新增回归测试 | 格式不符的目录、指向外部的符号链接不删、不跟随；删除失败时 `state get` 仍成功 |\n| A5 | 文档一致 | 阅读 queue-usage、tool/AGENTS.md、catalog.md | 写明保留规则，并记为与模板的差异 |\n| A6 | 未越界、队列可用 | `git diff --stat`；`python3 tool/shell.py doctor` | 只改允许的位置；protection: ready |\n\n验收安排：Agent 自检后交付，标“未独立验证”；用户验收。", "origin": "2026-09-30，用户在当前对话中问：`.shell/local/state/` 为什么有这么多记录。Agent 查明：\n\n- `state get` 把每个版本的状态包存进单独的目录 `.shell/local/state/<版本号>-<分片尺寸>/`，队列工具（tool/state_pack.py、tool/task_queue.py）没有任何清理旧目录的代码。当时共 243 个目录、39 MB，对应机器账第 8 到 249 笔操作。\n- 除当前状态的版本外，旧目录不会再被任何命令用到：写入时只接受当前版本。\n- envshell 用固定文件名覆盖写，交接备忘另按保留份数轮转（history_keep），所以不堆积。\n- 本仓不宜整体改成覆盖写：写入时工具要核对所带版本的缓存是否完整（`state_cache`，测试 test_10）；用法承诺不同分片尺寸独立保存（测试 test_11）；分目录还保证读到一半不会被换成新版本。\n\n用户指令：“两样都做，登记成一件任务”——即手动清理一次现有旧目录，并改工具让它自动只留最近几份（当前对话）。", "plan": "1. 登记、批准并领取本任务；记录清理前读数。\n2. 改 tool/state_pack.py，补回归测试，改三份文档。\n3. 跑两组测试；运行一次 `state get` 完成清理并记录读数；写回执，交付并提交；不推送。", "scope": "- 要交付：\n  - tool/state_pack.py：`state get` 送达并自检成功后，清理旧版本目录。保留规则：当前状态的版本不论分片尺寸全部保留；过期版本只保留最近 2 个（按上次取包时间），其余删除。清理在队列锁内进行；只处理 `.shell/local/state/` 下名称符合版本格式的目录，不跟随符号链接；删除失败不影响本次取包。返回结果增加 `pruned`（本次删除的目录数）。\n  - gate/test_state_queue.py：新增回归测试，覆盖保留规则、不同分片尺寸并存、格式不符的目录与符号链接不被删除、删除失败时取包仍成功。\n  - 文档：tool/queue-usage.md 写明缓存保留规则；tool/AGENTS.md 的模板差异清单补记；tool/catalog.md 的“写入”一栏补上清理过期缓存。\n  - 现有旧目录的清理：改好的工具第一次取包时一次清掉，不另写一次性删除命令；清理前后的目录数与大小记入回执。\n- 不包含：改成固定文件名覆盖写；改写入时的缓存核对逻辑或“不同尺寸独立保存”的承诺；在 charter/config.json 新增配置键（保留份数写成工具内常量）；推送到 GitHub。\n- 允许修改的位置：tool/state_pack.py、gate/test_state_queue.py、tool/queue-usage.md、tool/AGENTS.md、tool/catalog.md；本机 `.shell/local/state/` 下的过期缓存目录（删除）；队列文件经工具维护。", "title": "状态包缓存：清理旧版本，并让工具自动只留最近几份"}}
- #252｜claim｜claude｜{"expect": 251, "id": "T37"}
- #253｜deliver｜claude｜{"artifacts": [{"path": "tool/state_pack.py", "sha256": "a6835507d96a6fe8c38b78c0db79c92c5a21ce49eefbb3959220777dde7ba0c5"}, {"path": "gate/test_state_queue.py", "sha256": "28347e9c17b33dd49b0707f8c6dfb6f96cf2b9270bf60dfc9d28cbf17e2d5516"}, {"path": "tool/queue-usage.md", "sha256": "d7392c139b51ebc157af1cfe509040ebd2c6c1ae708c5cbd4779a6330e0fa4ca"}, {"path": "tool/AGENTS.md", "sha256": "23224005bdb1148dcbf44cf4f765461fd8f2e1c5317c67a704db2ac7c041052b"}, {"path": "tool/catalog.md", "sha256": "67463d2752367e95dec68b39dfec5fd22e7fa8ed4a09c8af2b0214607a7f9001"}], "expect": 252, "id": "T37", "receipt": "# T37 交付回执：状态包缓存清理与自动只留最近几份\n\n- 执行：claude，2026-09-30\n- 自检结论：passed。未独立验证。\n\n## 改动\n\n- tool/state_pack.py：新增 `prune`。`state get` 送达并自检成功后，在队列锁内清理 `.shell/local/state/`：\n  - 当前状态的版本不论分片尺寸全部保留（写入时仍可用）；\n  - 过期版本按上次取包时间（manifest 的修改时间）只留最近 2 个（常量 `KEEP_STALE = 2`），其余用 `shutil.rmtree` 删除；\n  - 只处理名称符合“64 位十六进制-分片尺寸”格式的真实目录，跳过符号链接和其他条目；\n  - 删除失败吞掉异常，不影响本次送达；返回结果新增 `pruned`（本次删除数）。\n  - 另把缓存路径收为常量 `STATE_CACHE`，`cached` 与 `get` 共用。\n- gate/test_state_queue.py：新增 test_25、test_26（见下）。\n- tool/queue-usage.md：写明保留规则与 `pruned`；tool/AGENTS.md：模板差异清单补记；tool/catalog.md：“写入”一栏补上删除过期缓存。\n\n## 验收标准逐条\n\n| 编号 | 结果 | 证据 |\n|---|---|---|\n| A1 | 满足 | 清理前：245 个目录，文件合计 32.55 MB，`du -sh` 39M。改好后在本仓运行一次 `python3 tool/shell.py state get`：退出码 0，`pruned 243`。清理后：3 个目录（当前 seq 252 的版本，加 seq 250、251 两个过期版本），文件合计 0.46 MB，`du -sh` 528K。再取一次 `pruned 0` |\n| A2 | 满足 | test_25：连续 4 次写入后缓存只剩 3 个目录（写入过程中的取包已在清理）；再取当前版本与另一分片尺寸，删除 1 个最旧的，剩下 2 个最新过期版本与当前两种尺寸，共 4 个，两种尺寸 `state check` 都通过 |\n| A3 | 满足 | `python3 gate/test_state_queue.py`：Ran 26 tests，OK，退出码 0（含 test_10、test_11）；`python3 gate/test_task_queue.py`：Ran 64 tests，OK，退出码 0 |\n| A4 | 满足 | test_26：版本格式的符号链接指向缓存外的目录、名为 notes 的普通目录（两者时间都设为最旧）均未被删除，外部文件完好；一个过期目录设为不可删除，`state get` 仍成功，`pruned 0`，该目录仍在 |\n| A5 | 满足 | 三份文档已写明保留规则，tool/AGENTS.md 记为与模板的差异 |\n| A6 | 满足 | `git diff --stat` 只有 tool/state_pack.py、gate/test_state_queue.py、tool/queue-usage.md、tool/AGENTS.md、tool/catalog.md 与机器账；`python3 tool/shell.py doctor`：protection ready，退出码 0 |\n\n## 测试是否真能发现问题（变异检查）\n\n在临时副本中故意改坏代码，只跑对应测试：\n\n- `KEEP_STALE = 99`（等于不清理）：test_25 失败（`AssertionError: 4 != 3`），退出码 1。\n- 去掉目录名格式检查：test_26 失败（`AssertionError: False is not true`，notes 目录被删），退出码 1。\n\n去掉符号链接跳过这一条，test_26 仍会通过：`shutil.rmtree` 本身拒绝对符号链接操作，外部文件照样完好。符号链接因此有两层保护，但第一层单独失效时测试发现不了，如实记录。\n\n## 未验证\n\n- 没有独立审阅者核对，以上读数都是执行者自报。\n- 删除失败的测试靠目录权限模拟，Windows 与 root 用户下跳过。\n- 本地提交，未推送。\n", "summary": "state get 送达后自动清理过期状态包缓存（当前状态各尺寸全留，过期版本只留最近 2 个）；本仓 245 个目录已清到 3 个，39M 降到 528K", "verification": "passed"}
- #254｜close｜claude｜{"authority": {"basis": "当前对话 2026-09-30：用户指令“T37 通过”", "by": "用户"}, "expect": 253, "id": "T37"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
