# 任务编号改为自然增长，不再补零

## 范围

- 要交付：
  1. 队列工具：
     - 编号校验接受两种写法：账本中已有的四位补零编号，以及不补零的自然编号。同一数值只能对应一个任务。
     - 新建编号取账本中最大数值加一，写成 T 加不补零的数字。task_queue.py 的生成与 queue_model.py 的重放校验保持一致。
     - 凡按编号排序的地方都按数值排序，逐处核对不遗漏；已知有窗口占用列表、依赖列表、状态包中的任务文件顺序。
  2. 测试：
     - 断言四位编号的地方改为新写法。
     - 新增用例：含四位编号的旧账继续登记，得到自然编号并能重放；T9 与 T10 按数值排序；同一数值的两种写法冲突时被拒绝。
  3. 规则与用法：queue/AGENTS.md 的目录示例与编号说明；tool/queue-usage.md 写明编号格式及新旧并存；其他提到编号格式的规则文件逐处核对。
  4. 现有 T0001–T0033 的编号、目录与账本记录都不改。
- 不包含：改写既有编号或目录；队列协议升级；推送到 GitHub。
- 允许修改的位置：
  - tool/queue_model.py、tool/queue_v2.py、tool/task_queue.py、tool/state_pack.py：只改编号的校验、生成与排序。
  - gate/test_task_queue.py、gate/test_state_queue.py。
  - queue/AGENTS.md、tool/queue-usage.md、tool/AGENTS.md。
  - 队列文件经工具维护。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 新任务编号不补零 | 测试中用真实命令行在临时项目登记；本仓改完后运行 `task status` | 新编号为 T 加不补零的数字，接续最大数值；重放与提交检查通过 |
| A2 | 旧编号继续有效 | 测试含四位编号的旧账；本仓运行 `doctor`，提交时运行 `check --staged` | 旧任务的状态、历史、任务包与封存卷照常；doctor 为 protection: ready、protocol: 2 |
| A3 | 按数值排序 | 新增测试 | 窗口列表、依赖列表、状态输出与状态包中，T9 排在 T10 前 |
| A4 | 同一数值不重复 | 新增测试 | 同一数值的两种写法冲突时被拒绝 |
| A5 | 全部测试通过 | `python3 -B -m unittest discover -s gate -p 'test_*.py' -v` | 全部通过 |
| A6 | 规则与用法一致 | 阅读 queue/AGENTS.md、tool/queue-usage.md | 写明编号格式与新旧并存，与工具行为一致 |
| A7 | 没有越界 | `git diff` | 只改允许的位置 |

验收安排：Agent 自检后交付；用户验收。
