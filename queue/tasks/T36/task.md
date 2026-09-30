# 区契约去重与 README 瘦身

```json
{
  "id": "T36",
  "revision": 249,
  "assignee": "claude",
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "交付"
}
```

## 登记依据

2026-09-30，任务 T35 把全局规则收归根契约后，用户在当前对话中追问：根目录 README 能否退役，各区契约是否需要统一升级。Agent 的答复：

- README 不删，因为 GitHub 首页只显示它，项目又要开源、作为作品申请，且根契约与队列测试都引用它；但它的“从哪里看起”文档清单与 truth/goals.md 的“文档结构”重复，应瘦身。
- 各区契约不按 envshell 格式整体重写，只做去重：gate、eval、tool、reference、queue 五份区契约里各有几句是根契约第 4 节全局规则的重复。
- T35 留下一处重叠：根契约第 7、8、11 条与队列规则“一致性”一节讲同一件事，违反根契约第 13 条“一件事实只维护一处”。
- object/AGENTS.md 留到 iOS 实现开工时随第一个实现任务升级。

用户指令：“登记成一件任务，一次做完”（当前对话）。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000249.md](receipt-000249.md)

## 过程记录

- #247｜create｜claude｜{"authority": {"basis": "当前对话 2026-09-30：用户就“README 瘦身、区契约去重、根契约与队列规则分工”的建议指令“登记成一件任务，一次做完”", "by": "用户"}, "deps": [], "id": "T36", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | README 瘦身 | 阅读 README.md | 不再有逐份列出的文档清单，改为指向 goals.md“文档结构”；简介、状态说明、协作与许可证仍在 |\n| A2 | 区契约不再复述全局规则 | 回执附逐句对照表：原句、处理方式、对应根契约条目 | 答复中列出的重复句全部处理；本区特有的内容没有被删 |\n| A3 | 根契约与队列规则分工清楚 | 阅读根契约第 7、8、11 条与队列规则“一致性” | 操作细节只在队列规则；根契约只留原则与指向 |\n| A4 | 指向准确 | 脚本抽出所有“根契约第 N 条”，核对所指条目的标题 | 全部指向预期的规则；规则编号未变 |\n| A5 | 未越界、链接可用、无违禁字符、队列可用 | `git diff --stat`；本地相对链接检查；检索 U+00A7；`python3 gate/test_task_queue.py`；`python3 tool/shell.py doctor` | 只改允许的位置；无断链；零命中；测试通过；protection: ready |\n\n验收安排：Agent 自检后交付，标“未独立验证”；用户验收。", "origin": "2026-09-30，任务 T35 把全局规则收归根契约后，用户在当前对话中追问：根目录 README 能否退役，各区契约是否需要统一升级。Agent 的答复：\n\n- README 不删，因为 GitHub 首页只显示它，项目又要开源、作为作品申请，且根契约与队列测试都引用它；但它的“从哪里看起”文档清单与 truth/goals.md 的“文档结构”重复，应瘦身。\n- 各区契约不按 envshell 格式整体重写，只做去重：gate、eval、tool、reference、queue 五份区契约里各有几句是根契约第 4 节全局规则的重复。\n- T35 留下一处重叠：根契约第 7、8、11 条与队列规则“一致性”一节讲同一件事，违反根契约第 13 条“一件事实只维护一处”。\n- object/AGENTS.md 留到 iOS 实现开工时随第一个实现任务升级。\n\n用户指令：“登记成一件任务，一次做完”（当前对话）。", "plan": "1. 登记、批准并领取本任务。\n2. 改 README、五份区契约与根契约三条。\n3. 跑检查，写回执（含逐句对照表），交付并提交；不推送。", "scope": "- 要交付：\n  - README：删去“从哪里看起”的文档清单，改为一句话指向 truth/goals.md 的“文档结构”与 reference/；保留项目简介、文档状态说明、文件夹指引、协作方式与许可证。\n  - 区契约去重：gate、eval、tool、reference、queue 中重复根契约全局规则的句子，删去或改为指向根契约对应条目；本区特有的内容保留。\n  - 根契约与队列规则分工：根契约第 7、8、11 条保留原则并指向队列规则“一致性”，不再复述请求号、重试等操作细节；队列规则中重复根契约第 1、2、10、11 条的句子改为指向根契约。\n  - 根契约规则编号不变。\n- 不包含：object/AGENTS.md；truth 文档与 truth 下的区契约；charter；队列与制图工具的代码；推送到 GitHub。\n- 允许修改的位置：README.md、AGENTS.md（第 4 节第 7、8、11 条）、queue/AGENTS.md、gate/AGENTS.md、eval/AGENTS.md、tool/AGENTS.md、reference/AGENTS.md；队列文件经工具维护。", "title": "区契约去重与 README 瘦身"}}
- #248｜claim｜claude｜{"expect": 247, "id": "T36"}
- #249｜deliver｜claude｜{"artifacts": [{"path": "README.md", "sha256": "1d7d4b8d058de6241f67caca8f35975a72b2cf8f56b7e8f69c1e285379210252"}, {"path": "AGENTS.md", "sha256": "57c586bf577677c2cf5af394fbb8ec6dad795d7fe189c0980809bb9aac553665"}, {"path": "queue/AGENTS.md", "sha256": "3927fd333df3b666eeb4bd164f6f3d95fd81adfa5f76b496c8acc6724f00a832"}, {"path": "gate/AGENTS.md", "sha256": "5a622145575eeaf0cd7e367a781ea4b7e5698b087803174ef137941bfd7ffbb1"}, {"path": "eval/AGENTS.md", "sha256": "b0d76384caa19bc130c4b07d31aadf25abe174f29177c48b2e9b94fe4e9d5041"}, {"path": "tool/AGENTS.md", "sha256": "75af08a6ab621fa563ec9dfe8dea06486ffec4a53c0ecc4e0fd79fa544ef3d0e"}, {"path": "reference/AGENTS.md", "sha256": "a9aed231b07fa75bfe01f58effe068e8f704956475600afdf05f8cc0fca5e101"}], "expect": 248, "id": "T36", "receipt": "# T36 交付回执：区契约去重与 README 瘦身\n\n- 执行：claude，2026-09-30\n- 自检结论：passed。未独立验证。\n\n## 逐句对照（A1–A3）\n\n| 文件 | 原句 | 处理 | 对应 |\n|---|---|---|---|\n| README.md | “从哪里看起”下逐份列出的五份文档与参考图 | 改为一句话：先读项目目标及其“文档结构”一节；参考图在 reference/ | goals.md“文档结构” |\n| queue/AGENTS.md | 开头：不直接编辑任务、批准基线、回执或手动添加附件 | 改为“只经命令树操作”加指向 | 根契约第 7 条 |\n| queue/AGENTS.md | 用户明确授权才能批准；通过须用户验收依据，测试通过不等于用户通过；Agent 代书，不重复批准 | 改为指向 | 根契约第 1、10 条 |\n| queue/AGENTS.md | 一致性：机器账、配置、任务视图及相关交付工件同批暂存，不绕过钩子 | 改为指向 | 根契约第 11 条 |\n| queue/AGENTS.md | 一致性：语义判断、真实授权及业务结果仍由 Agent 与用户负责 | 改为指向 | 根契约第 2 条 |\n| gate/AGENTS.md | Agent 按批准方案实际运行，记录原样命令、退出码和结果，缺条件标未验证 | 保留“由 Agent 按批准方案实际运行并汇报”，汇报方式改为指向 | 根契约第 15 条 |\n| gate/AGENTS.md | 钩子可被刻意绕过，机器检查不构成独立安全边界，也不认证用户身份或验证申报的真实性 | 保留本区特有的“只核对记录、配置与指纹，不验证申报的真实性”，边界改为指向 | 根契约第 2 条 |\n| eval/AGENTS.md | 未独立验证应明确标注；不授权安装工具、联网或付费 | 删去“未独立验证”；授权改为指向；保留“主观评价与样本不足应明确标注”“登记不等于已经执行” | 根契约第 12、3 条 |\n| tool/AGENTS.md | 凭据只记录名称，不记录值 | 删去 | 根契约第 4 条 |\n| tool/AGENTS.md | 登记工具不等于获准安装或执行 | 保留并加指向 | 根契约第 3 条 |\n| tool/AGENTS.md | 测试输出不能当作用户验收 | 删去 | 根契约第 10 条 |\n| reference/AGENTS.md | 不因一份参考资料说“应该做”就把它当作用户授权或项目规则 | 并入末条：“参考资料不构成授权”加指向 | 根契约第 1 条 |\n| AGENTS.md 第 7 条 | 稳定请求号、重试沿用、先看结果 | 删去细节，改为指向队列规则“一致性” | queue/AGENTS.md“一致性” |\n| AGENTS.md 第 8 条 | 携带 context、过期重取并读变化、认领与版本以工具为准 | 保留原则“只凭自己读过的状态包写入，不借其他会话的已读标记”，细节改为指向 | queue/AGENTS.md“一致性” |\n| AGENTS.md 第 11 条 | 同批暂存机器账、任务视图和相关工件 | 原则保留，补上原在队列规则中的“配置”；暂存范围与收尾写法指向队列用法“快速收尾” | tool/queue-usage.md“快速收尾” |\n\n分工结果：操作细节（版本、revision、请求号、重试、repair）只在队列规则与队列用法；根契约只留原则与指向。提交要求的正本在根契约第 11 条，因为它同时涉及队列检查与制图检查，队列规则指向它。\n\n## 验收标准逐条\n\n| 编号 | 结果 | 证据 |\n|---|---|---|\n| A1 | 满足 | README 不再逐份列文档，指向 goals.md“文档结构”；简介、状态说明、文件夹指引、协作方式与许可证仍在 |\n| A2 | 满足 | 上表逐句处理；用 12 个原句片段检索五份区契约与根契约，`grep` 退出码 1（零命中） |\n| A3 | 满足 | 根契约第 7、8、11 条只留原则与指向；`git diff -U0 AGENTS.md` 只改这三行 |\n| A4 | 满足 | 脚本抽出 11 处“第 N 条”，逐一核对标题全部对应预期规则；规则仍为 1–22 条，编号未变 |\n| A5 | 满足 | `git diff --name-only` 只有允许的 7 个文件与机器账；7 个改动文件 57 个相对链接，断链 0；U+00A7 零命中；`python3 gate/test_task_queue.py`：Ran 64 tests，OK，退出码 0；`python3 tool/shell.py doctor`：protection ready，退出码 0 |\n\n## 未验证\n\n- 没有独立审阅者核对，以上读数都是执行者自报。\n- 本地提交，未推送。\n", "summary": "README 瘦身为指向 goals.md；五份区契约去掉重复的全局规则，改指根契约；根契约第 7、8、11 条与队列规则分工", "verification": "passed"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
