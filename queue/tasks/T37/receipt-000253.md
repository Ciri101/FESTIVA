# T37 交付回执：状态包缓存清理与自动只留最近几份

- 执行：claude，2026-09-30
- 自检结论：passed。未独立验证。

## 改动

- tool/state_pack.py：新增 `prune`。`state get` 送达并自检成功后，在队列锁内清理 `.shell/local/state/`：
  - 当前状态的版本不论分片尺寸全部保留（写入时仍可用）；
  - 过期版本按上次取包时间（manifest 的修改时间）只留最近 2 个（常量 `KEEP_STALE = 2`），其余用 `shutil.rmtree` 删除；
  - 只处理名称符合“64 位十六进制-分片尺寸”格式的真实目录，跳过符号链接和其他条目；
  - 删除失败吞掉异常，不影响本次送达；返回结果新增 `pruned`（本次删除数）。
  - 另把缓存路径收为常量 `STATE_CACHE`，`cached` 与 `get` 共用。
- gate/test_state_queue.py：新增 test_25、test_26（见下）。
- tool/queue-usage.md：写明保留规则与 `pruned`；tool/AGENTS.md：模板差异清单补记；tool/catalog.md：“写入”一栏补上删除过期缓存。

## 验收标准逐条

| 编号 | 结果 | 证据 |
|---|---|---|
| A1 | 满足 | 清理前：245 个目录，文件合计 32.55 MB，`du -sh` 39M。改好后在本仓运行一次 `python3 tool/shell.py state get`：退出码 0，`pruned 243`。清理后：3 个目录（当前 seq 252 的版本，加 seq 250、251 两个过期版本），文件合计 0.46 MB，`du -sh` 528K。再取一次 `pruned 0` |
| A2 | 满足 | test_25：连续 4 次写入后缓存只剩 3 个目录（写入过程中的取包已在清理）；再取当前版本与另一分片尺寸，删除 1 个最旧的，剩下 2 个最新过期版本与当前两种尺寸，共 4 个，两种尺寸 `state check` 都通过 |
| A3 | 满足 | `python3 gate/test_state_queue.py`：Ran 26 tests，OK，退出码 0（含 test_10、test_11）；`python3 gate/test_task_queue.py`：Ran 64 tests，OK，退出码 0 |
| A4 | 满足 | test_26：版本格式的符号链接指向缓存外的目录、名为 notes 的普通目录（两者时间都设为最旧）均未被删除，外部文件完好；一个过期目录设为不可删除，`state get` 仍成功，`pruned 0`，该目录仍在 |
| A5 | 满足 | 三份文档已写明保留规则，tool/AGENTS.md 记为与模板的差异 |
| A6 | 满足 | `git diff --stat` 只有 tool/state_pack.py、gate/test_state_queue.py、tool/queue-usage.md、tool/AGENTS.md、tool/catalog.md 与机器账；`python3 tool/shell.py doctor`：protection ready，退出码 0 |

## 测试是否真能发现问题（变异检查）

在临时副本中故意改坏代码，只跑对应测试：

- `KEEP_STALE = 99`（等于不清理）：test_25 失败（`AssertionError: 4 != 3`），退出码 1。
- 去掉目录名格式检查：test_26 失败（`AssertionError: False is not true`，notes 目录被删），退出码 1。

去掉符号链接跳过这一条，test_26 仍会通过：`shutil.rmtree` 本身拒绝对符号链接操作，外部文件照样完好。符号链接因此有两层保护，但第一层单独失效时测试发现不了，如实记录。

## 未验证

- 没有独立审阅者核对，以上读数都是执行者自报。
- 删除失败的测试靠目录权限模拟，Windows 与 root 用户下跳过。
- 本地提交，未推送。
