# 任务编号改为自然增长，不再补零

```json
{
  "id": "T0033",
  "revision": 232,
  "assignee": "claude",
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "交付"
}
```

## 登记依据

2026-09-30，用户要求追加一个环境治理任务：新任务编号改为自然增长的 T1、T2、…、T10、…，取消固定四位补零（当前对话）。

现状（Agent 清查）：
- 编号的写法由队列工具写死：tool/queue_model.py 的 `task_id` 只接受 `T{n:04d}`；登记时的新编号在 tool/task_queue.py 生成、在 queue_model.py 重放校验，两处都写成四位补零。
- 有几处按编号排序时用的是字符串顺序，改为不补零后会出现 T10 排在 T9 前面。已知的有：queue_v2.py 的窗口占用列表、queue_model.py 的依赖列表，以及状态包中任务文件的顺序。
- 测试 gate/test_task_queue.py、gate/test_state_queue.py 断言了四位编号。
- queue/AGENTS.md 以“tasks/T0001/”为例说明任务目录。

约束：机器账只追加，已通过的任务卷封存，文档中有大量指向 queue/tasks/T00xx/ 的链接，所以现有编号不能改写。改完后新旧两种写法长期并存：已有的四位编号照旧有效，新任务不补零，编号数值连续，不复用。本任务按现行工具登记，编号为 T0033；改完后下一件新任务是 T34。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000232.md](receipt-000232.md)

## 过程记录

- #229｜create｜claude｜{"authority": null, "deps": [], "id": "T0033", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 新任务编号不补零 | 测试中用真实命令行在临时项目登记；本仓改完后运行 `task status` | 新编号为 T 加不补零的数字，接续最大数值；重放与提交检查通过 |\n| A2 | 旧编号继续有效 | 测试含四位编号的旧账；本仓运行 `doctor`，提交时运行 `check --staged` | 旧任务的状态、历史、任务包与封存卷照常；doctor 为 protection: ready、protocol: 2 |\n| A3 | 按数值排序 | 新增测试 | 窗口列表、依赖列表、状态输出与状态包中，T9 排在 T10 前 |\n| A4 | 同一数值不重复 | 新增测试 | 同一数值的两种写法冲突时被拒绝 |\n| A5 | 全部测试通过 | `python3 -B -m unittest discover -s gate -p 'test_*.py' -v` | 全部通过 |\n| A6 | 规则与用法一致 | 阅读 queue/AGENTS.md、tool/queue-usage.md | 写明编号格式与新旧并存，与工具行为一致 |\n| A7 | 没有越界 | `git diff` | 只改允许的位置 |\n\n验收安排：Agent 自检后交付；用户验收。", "origin": "2026-09-30，用户要求追加一个环境治理任务：新任务编号改为自然增长的 T1、T2、…、T10、…，取消固定四位补零（当前对话）。\n\n现状（Agent 清查）：\n- 编号的写法由队列工具写死：tool/queue_model.py 的 `task_id` 只接受 `T{n:04d}`；登记时的新编号在 tool/task_queue.py 生成、在 queue_model.py 重放校验，两处都写成四位补零。\n- 有几处按编号排序时用的是字符串顺序，改为不补零后会出现 T10 排在 T9 前面。已知的有：queue_v2.py 的窗口占用列表、queue_model.py 的依赖列表，以及状态包中任务文件的顺序。\n- 测试 gate/test_task_queue.py、gate/test_state_queue.py 断言了四位编号。\n- queue/AGENTS.md 以“tasks/T0001/”为例说明任务目录。\n\n约束：机器账只追加，已通过的任务卷封存，文档中有大量指向 queue/tasks/T00xx/ 的链接，所以现有编号不能改写。改完后新旧两种写法长期并存：已有的四位编号照旧有效，新任务不补零，编号数值连续，不复用。本任务按现行工具登记，编号为 T0033；改完后下一件新任务是 T34。", "plan": "1. 逐处核对工具中编号的校验、生成与排序，先写失败的测试，再改代码。\n2. 改规则与用法。\n3. 运行全部测试与本仓 doctor，交付。", "scope": "- 要交付：\n  1. 队列工具：\n     - 编号校验接受两种写法：账本中已有的四位补零编号，以及不补零的自然编号。同一数值只能对应一个任务。\n     - 新建编号取账本中最大数值加一，写成 T 加不补零的数字。task_queue.py 的生成与 queue_model.py 的重放校验保持一致。\n     - 凡按编号排序的地方都按数值排序，逐处核对不遗漏；已知有窗口占用列表、依赖列表、状态包中的任务文件顺序。\n  2. 测试：\n     - 断言四位编号的地方改为新写法。\n     - 新增用例：含四位编号的旧账继续登记，得到自然编号并能重放；T9 与 T10 按数值排序；同一数值的两种写法冲突时被拒绝。\n  3. 规则与用法：queue/AGENTS.md 的目录示例与编号说明；tool/queue-usage.md 写明编号格式及新旧并存；其他提到编号格式的规则文件逐处核对。\n  4. 现有 T0001–T0033 的编号、目录与账本记录都不改。\n- 不包含：改写既有编号或目录；队列协议升级；推送到 GitHub。\n- 允许修改的位置：\n  - tool/queue_model.py、tool/queue_v2.py、tool/task_queue.py、tool/state_pack.py：只改编号的校验、生成与排序。\n  - gate/test_task_queue.py、gate/test_state_queue.py。\n  - queue/AGENTS.md、tool/queue-usage.md、tool/AGENTS.md。\n  - 队列文件经工具维护。", "title": "任务编号改为自然增长，不再补零"}}
- #230｜approve｜claude｜{"authority": {"basis": "当前对话 2026-09-30：用户回复“批准 T0033 开工”", "by": "用户"}, "expect": 229, "id": "T0033"}
- #231｜claim｜claude｜{"expect": 230, "id": "T0033"}
- #232｜deliver｜claude｜{"artifacts": [{"path": "gate/test_state_queue.py", "sha256": "1ad0b572e27fc006a3a9542754d4c95b6887d022834b29f7a624a31362a033bc"}, {"path": "gate/test_task_queue.py", "sha256": "818cf956879c7de0e7792ec5dfeef25aa9a43afbb1dc3982cf0974572a7e60ba"}, {"path": "queue/AGENTS.md", "sha256": "be03b08019549c94452b9cc05a196fcdfd006f429baf49c72a896841c9375315"}, {"path": "tool/AGENTS.md", "sha256": "2c7f9c1d0ce22091948d1fd080a1d4e552f09585540b29f5b0ae77d29cd86c4d"}, {"path": "tool/queue-usage.md", "sha256": "3dc04094f69942bd1d5f545967fbafbbe0e1d1463a036d1d067c250c2c0d10c0"}, {"path": "tool/queue_model.py", "sha256": "73e9dd4dfdd24e2d24aa61a5a645d44a6ed3465a51429f947422aeb508d47b3c"}, {"path": "tool/queue_v2.py", "sha256": "6cc927d4235c707d70c3f1375a6be9ef48abaa4a897a667ef67b894aebe64879"}, {"path": "tool/state_pack.py", "sha256": "e27175477565a1f2250a5d0ff157dd4e10a0b68cf1c732ed858acdc7454de06c"}, {"path": "tool/task_queue.py", "sha256": "aa47398d8f612c75cfc3a0eb8d4db67bd4a90aaeb2b5ea6b19cc373253e672bc"}], "expect": 231, "id": "T0033", "receipt": "# T0033 交付回执：任务编号改为自然增长\n\n- 执行：claude，2026-09-30\n- 自检结论：passed。全部 88 个测试通过；本仓 doctor 正常，已有账本照常重放，下一件新任务为 T34。未独立验证。\n\n## 一、改了什么（对应范围第 1–3 项）\n\n**1. 队列工具**（只改编号的校验、生成与排序）\n- `tool/queue_model.py`\n  - `task_id` 接受两种写法：T 加不补零的数字（T1、T10），以及账本里已有的四位补零编号（T0001）。其他写法拒绝，例如 T01、T09。\n  - 新增 `task_number`（取编号数值）与 `next_task_id`（最大数值加一，不补零）。\n  - 重放登记时，按数值核对是否连续分配。\n  - 导入时按数值查重，同一数值的两种写法视为重复。\n  - 依赖列表、撤销与取消的处理顺序按数值排序。\n- `tool/task_queue.py`：登记时用 `next_task_id` 生成编号；状态输出按数值排序。\n- `tool/queue_v2.py`：窗口占用列表按数值排序。\n- `tool/state_pack.py`：状态包中的任务文件按编号数值排序，其他文件仍按路径排序。\n\n**2. 测试**\n- `gate/test_task_queue.py`\n  - 断言编号的地方改为新写法：test_10 与 test_19 的期望编号；test_35 登记后得到 T4。\n  - test_35 新增三个断言：旧编号 T0003 照常可查、`doctor` 正常、提交通过。\n  - test_39 与 test_42 写死的首件目录由 `T0001` 改为 `T1`。清查时漏了这两处，是全量测试失败后才发现的。\n  - 新增 test_19b：编号为 T1–T10；`--dep T0009` 指向不存在的任务被拒；`--dep T09` 格式被拒；T11 依赖 T10、T9；窗口、状态输出、阻塞原因与状态包中，T9 都排在 T10 前；`doctor` 与提交通过。\n  - 新增 test_35b：旧目录 T0001 与 T1 同时存在时，迁移预检因编号重复被拒，不写账。\n- `gate/test_state_queue.py`：两处期望编号改为 T9、T3。\n\n**3. 规则与用法**\n- `queue/AGENTS.md`：任务目录示例改为 `tasks/<编号>/`；新增“编号”一段，说明新旧写法并存、按数值排序、引用时照写原样编号。\n- `tool/queue-usage.md`：同样写明编号格式。\n- `tool/AGENTS.md`：记下本仓与 devtemplate 队列工具的差异。\n\n**4. 不改的**：现有 T0001–T0033 的编号、目录与账本记录。\n\n## 二、测试夹具修正（范围之外的前置问题，改动在允许的测试文件内）\n\n- 改动前的基线：`python3 -B -m unittest discover -s gate -p 'test_*.py'` 共 86 个测试，失败 73 个。\n- 原因：任务 T0003（提交 d055e3b）把四份主文档加进了 `charter/config.json` 的白名单，但测试夹具只复制 `truth/goals.md` 到临时仓库，读状态包时报“白名单文件缺失”。这与编号无关，自 T0003 起就存在。\n- 修正：夹具在临时仓库写入模板默认配置（白名单只有 `truth/goals.md`，窗口 8），不复制本仓的配置。\n- 修正后，在改编号之前的代码上重跑：86 个全部通过。\n\n## 三、验证记录（实测）\n\n- 新测试先写，并确认在旧代码上失败：test_19b 期望 T1–T10、实得 T0001–T0010；test_35b 期望“重复”、实得“任务号格式错误”；test_10 期望 T2、实得 T0002。改代码后，以上三个与 test_35 都通过。\n- 全量测试：`python3 -B -m unittest discover -s gate -p 'test_*.py'`。第一次全量有 2 个未过（test_39、test_42，原因是写死了 T0001 目录，单独重跑三次都稳定复现）。改正后再跑全量：Ran 88 tests in 168.3s，OK。\n- 本仓：\n  - `python3 tool/shell.py doctor` → `{\"ok\": true, \"protection\": \"ready\", \"seq\": 231, \"tasks\": 33, \"protocol\": 2}`。\n  - `state get` 正常。\n  - `task status T0001` → 通过。\n  - 用新代码重放本仓账本：33 件任务，首件 T0001，末件 T0033，下一件 T34，窗口 ['T0033']。\n- 提交时由钩子运行 `check --staged` 再检查。\n\n## 四、验收标准逐条\n\n| 编号 | 结果 | 证据 |\n|---|---|---|\n| A1 | 满足 | test_19b、test_35、test_10 实测新编号不补零、接续最大数值；本仓下一件为 T34 |\n| A2 | 满足 | test_35 中旧编号 T0001、T0003 照常可查，doctor 正常，提交通过；本仓 doctor 为 protection: ready、protocol: 2 |\n| A3 | 满足 | test_19b 验证窗口、状态输出、阻塞原因与状态包中 T9 排在 T10 前 |\n| A4 | 满足 | test_35b 验证同一数值的两种写法被拒；test_19b 验证 T0009 在只有 T9 时被当作不存在 |\n| A5 | 满足 | 全量 88 个测试通过 |\n| A6 | 满足 | queue/AGENTS.md 与 tool/queue-usage.md 写明编号格式、新旧并存、按数值排序、引用照写原样，与工具行为一致 |\n| A7 | 满足 | `git diff --stat` 只涉及允许的 9 个文件 |\n\n## 五、未验证与另行处理\n\n- 重放时，新登记的事件用四位还是不补零写法都会接受，只核对数值是否连续。工具生成的编号一律不补零；手改账本不在工具保证之内。\n- `gate/checks.md` 所说的隔离 Agent 使用验收（空白上下文的真实 Agent 测试）没有做。本次只改编号格式，属于用法的小变化。\n- 没有独立审阅者核对。本地提交未推送。\n", "summary": "新任务编号改为不补零的自然编号（下一件 T34），旧的四位编号照旧有效，按数值排序；全部 88 个测试通过；另修正了自 T0003 起失效的测试夹具配置", "verification": "passed"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
