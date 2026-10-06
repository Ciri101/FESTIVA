# 状态包缓存：清理旧版本，并让工具自动只留最近几份

## 范围

- 要交付：
  - tool/state_pack.py：`state get` 送达并自检成功后，清理旧版本目录。保留规则：当前状态的版本不论分片尺寸全部保留；过期版本只保留最近 2 个（按上次取包时间），其余删除。清理在队列锁内进行；只处理 `.shell/local/state/` 下名称符合版本格式的目录，不跟随符号链接；删除失败不影响本次取包。返回结果增加 `pruned`（本次删除的目录数）。
  - gate/test_state_queue.py：新增回归测试，覆盖保留规则、不同分片尺寸并存、格式不符的目录与符号链接不被删除、删除失败时取包仍成功。
  - 文档：tool/queue-usage.md 写明缓存保留规则；tool/AGENTS.md 的模板差异清单补记；tool/catalog.md 的“写入”一栏补上清理过期缓存。
  - 现有旧目录的清理：改好的工具第一次取包时一次清掉，不另写一次性删除命令；清理前后的目录数与大小记入回执。
- 不包含：改成固定文件名覆盖写；改写入时的缓存核对逻辑或“不同尺寸独立保存”的承诺；在 charter/config.json 新增配置键（保留份数写成工具内常量）；推送到 GitHub。
- 允许修改的位置：tool/state_pack.py、gate/test_state_queue.py、tool/queue-usage.md、tool/AGENTS.md、tool/catalog.md；本机 `.shell/local/state/` 下的过期缓存目录（删除）；队列文件经工具维护。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 现有旧缓存已清理 | 改动前后各统计一次 `.shell/local/state/` 的目录数与大小 | 清理后只剩当前状态的版本与至多 2 个过期版本 |
| A2 | 保留规则正确 | 新增回归测试 | 连续产生多个版本后，只剩预期的目录；最近 2 个过期版本仍在 |
| A3 | 原有承诺不破 | `python3 gate/test_state_queue.py`；`python3 gate/test_task_queue.py` | 两组全部通过，含 test_10、test_11 |
| A4 | 删除有边界、失败不拦取包 | 新增回归测试 | 格式不符的目录、指向外部的符号链接不删、不跟随；删除失败时 `state get` 仍成功 |
| A5 | 文档一致 | 阅读 queue-usage、tool/AGENTS.md、catalog.md | 写明保留规则，并记为与模板的差异 |
| A6 | 未越界、队列可用 | `git diff --stat`；`python3 tool/shell.py doctor` | 只改允许的位置；protection: ready |

验收安排：Agent 自检后交付，标“未独立验证”；用户验收。
