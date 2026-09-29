# 仓库内容去除协作者身份关系，并设为常设规则

```json
{
  "id": "T0014",
  "revision": 96,
  "assignee": "claude",
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "交付"
}
```

## 登记依据

2026-09-29，用户在当前对话中指出：协作者之间的现实身份关系只是背景交代，与 FESTIVA 产品无关，不应该进入仓库内容，以后也不要再出现在项目仓库中，因为这很容易污染产品内容。

盘点结果（排除“国际学生”“在校学生身份”“Verified student”等产品用词）：项目文档与规则文件中有 37 行把决定、确认或备注归到某个身份，例如“某身份采纳的裁决”“某身份备注”“由某身份逐节确认”；另有大量同类说法在任务记录与机器账中。

目的：把这类说法从当前的项目文档与规则文件中去掉，只保留决定本身及其所在任务；并写入常设规则，使以后的文档、代码与任务记录都不再写协作者的身份关系。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000096.md](receipt-000096.md)

## 过程记录

- #94｜create｜claude｜{"authority": {"basis": "当前对话 2026-09-29：用户指出协作者之间的身份关系只是背景交代、与产品无关，要求它不进入仓库内容、以后不再出现在项目仓库中，以免污染产品内容", "by": "用户"}, "deps": [], "id": "T0014", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 当前仓库内容不再有协作者身份关系 | 在 queue/ 与 .shell/ 以外的全部受管文件中检索身份用词，排除上述产品用词 | 结果为 0 |\n| A2 | 含义不变 | 逐行阅读 `git diff` | 只有身份说法、版本号与新增规则变化，没有改动任何规则、字段或状态 |\n| A3 | 常设规则生效 | 阅读 charter/AGENTS.md | 新规则写明适用范围、授权人写法与既有记录的处理 |\n| A4 | 检查与链接正常 | 本地相对链接检查；提交时的制图检查；`python3 tool/shell.py doctor` | 无断链；制图检查为绿；protection: ready |\n\n验收安排：Agent 自检后交付；用户验收。", "origin": "2026-09-29，用户在当前对话中指出：协作者之间的现实身份关系只是背景交代，与 FESTIVA 产品无关，不应该进入仓库内容，以后也不要再出现在项目仓库中，因为这很容易污染产品内容。\n\n盘点结果（排除“国际学生”“在校学生身份”“Verified student”等产品用词）：项目文档与规则文件中有 37 行把决定、确认或备注归到某个身份，例如“某身份采纳的裁决”“某身份备注”“由某身份逐节确认”；另有大量同类说法在任务记录与机器账中。\n\n目的：把这类说法从当前的项目文档与规则文件中去掉，只保留决定本身及其所在任务；并写入常设规则，使以后的文档、代码与任务记录都不再写协作者的身份关系。", "plan": "1. 写入常设规则。\n2. 逐文件改写身份说法，版本号递增。\n3. 运行检查并交付。", "scope": "- 要交付：\n  1. charter/AGENTS.md“基本约定”新增一条：仓库内容（文档、代码与注释、任务记录与回执）不写协作者的现实身份与彼此关系；任务记录中的授权人写“用户”，引用用户指令时只概述指令内容；项目文档只写决定本身及所在任务，不写决定人。既有任务记录与机器账是只追加的历史，不为此改写。\n  2. 以下文件中的身份说法改为中性措辞，含义不变：truth/goals.md、truth/FESTIVA-产品设计文档.md、truth/FESTIVA-工程架构文档.md、truth/ui/FESTIVA-高保真设计文档.md、truth/demo/FESTIVA-Demo架构方案.md、truth/architecture/AGENTS.md、truth/architecture/架构设计与制图规范.md、truth/architecture/治理细则.md、object/AGENTS.md、gate/checks.md、tool/diagram/render-diagrams.mts（只改一行注释）。项目文档里“用户”指 App 用户，因此不用“用户”替代，而是省去决定人，例如“经确认的裁决”“（B1 及其备注）”“2026-09-29 决定”。\n  3. 改动的四份项目文档（产品、工程、UI、Demo）版本号递增。\n- 不包含：queue/tasks/ 下的任务记录、批准基线、回执与 .shell/queue/ledger.jsonl（工具维护、只追加）；Git 历史与已推送到 GitHub 的内容；“国际学生”“在校学生身份”“Verified student”等产品用词；“裁决单”等流程用词；T0013 的施工内容。\n- 允许修改的位置：上述第 1、2 项列出的文件，仅限身份说法、版本号与新增规则。", "title": "仓库内容去除协作者身份关系，并设为常设规则"}}
- #95｜claim｜claude｜{"expect": 94, "id": "T0014"}
- #96｜deliver｜claude｜{"artifacts": [{"path": "charter/AGENTS.md", "sha256": "7711d0f5f0f91da12ff7169dabba08a1aeb8eca8093c3799dd21cdbd5ea2ec72"}, {"path": "truth/goals.md", "sha256": "660949b3d0db8627d125fdcbca5660c85c71be9d221e70031241666b7b2bbf54"}, {"path": "truth/FESTIVA-产品设计文档.md", "sha256": "ac2fbbf9164a51273c9ec679ce448eee1c424f431970f5e25de203523255705b"}, {"path": "truth/FESTIVA-工程架构文档.md", "sha256": "85cf92b7b40e18cd844120325da97806e68b45564059b8f45421f88d358257bb"}, {"path": "truth/ui/FESTIVA-高保真设计文档.md", "sha256": "d700bc4d265b0a7f5e165fba91c562140afee0ab6dfbf13a25da6a6073f8832e"}, {"path": "truth/demo/FESTIVA-Demo架构方案.md", "sha256": "12ef331a5afbb5daae164c89f9948115179b26bb264c07e271bce5107170fefc"}, {"path": "truth/architecture/AGENTS.md", "sha256": "cf93b420e0083c6523f147918a14954c4cf24ca015066f93998c498455ad3499"}, {"path": "truth/architecture/架构设计与制图规范.md", "sha256": "74caa2eec9f5e6c3084b4deccc06b225be7383a7245ba43b50d52e463be7b395"}, {"path": "truth/architecture/治理细则.md", "sha256": "8f61c52d70e8f1d9851b8b212a539b64746b8be2fcacd45154410ee04db9bd8f"}, {"path": "object/AGENTS.md", "sha256": "d65100d9248a1ff3ffa174f342b94a07b1a1aeeb890e24228894c7caded846d1"}, {"path": "gate/checks.md", "sha256": "82487a76d705ad5e5e32f961aab89a29f2b046229edddc03c7abf35f0830c9cf"}, {"path": "tool/diagram/render-diagrams.mts", "sha256": "af70d9b74e4715007c72b5679b8b05daf3898a6760950377927044e55ec49606"}], "expect": 95, "id": "T0014", "receipt": "# T0014 仓库内容去除协作者身份关系，并设为常设规则：验证回执\n\n执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替用户验收。\n\n## 改动\n\n1. charter/AGENTS.md“基本约定”新增第 8 条“不写协作者身份”：仓库内容（文档、代码与注释、任务记录与回执）不写协作者的现实身份与彼此关系；任务记录中的授权人写“用户”，引用用户指令时只概述内容；项目文档只写决定本身及所在任务，不写决定人；既有任务记录与机器账不为此改写。追加在第 7 条之后，原有条目编号不变。\n2. 11 个文件共 32 处替换（脚本逐条断言命中次数后才写入）。项目文档中“用户”指 App 用户，所以不用“用户”替代，而是省去决定人：\n   - “某身份采纳的 38 项裁决”改为“经确认的 38 项裁决”（goals、产品、工程、UI、Demo 头部）；\n   - “由某身份逐节确认”改为“已逐节确认”；“章节确认人为某身份（第 N 轮裁决单），某身份通过任务验收”改为“章节经第 N 轮裁决单逐节确认，并通过任务验收”（产品、UI）；\n   - “某身份备注”改为“备注”或“其备注”（产品 11 处、工程 4 处、Demo 2 处）；\n   - UI 第 3、5 节与附录 B 的“由某身份整体采纳 / 暂缓 / 决定”改为“整体采纳 / 暂缓 / 另行决定”；Demo 第 13 节“某身份自有的图片”改为“项目自有的图片”；\n   - truth/architecture 三份文档、object/AGENTS.md、gate/checks.md、tool/diagram/render-diagrams.mts 注释中的“某身份 2026-09-29 决定 / 验收 / 建的目录”改为不写决定人的说法。\n3. 版本号：产品设计文档 0.4 → 0.5，工程架构文档 0.4 → 0.5，高保真设计文档 0.4 → 0.5，Demo 架构方案 0.2 → 0.3。\n\n## 验收标准逐项\n\n- A1 通过：对 queue/ 与 .shell/ 以外全部 57 个受管文本文件逐行检索身份用词，排除“国际学生”“在校学生”“学生身份”“学生验证”“学生邮箱”“Verified student”等产品用词，结果为 0。\n- A2 通过：逐行阅读 `git diff`。变化只有身份说法、四个版本号与新增的第 8 条规则；没有改动任何规则、字段、状态或章节确认状态。\n- A3 通过：charter/AGENTS.md 第 8 条写明适用范围、授权人写法、项目文档写法与既有记录的处理，并链接本任务作为依据。\n- A4 通过：本地相对链接检查覆盖改动的 11 个 Markdown 文件，退出码 0；`node --experimental-strip-types tool/diagram/check.mts` 无红（当前无具名图）；`python3 tool/shell.py doctor` 为 protection: ready。\n\n## 未处理（按范围）\n\n- queue/tasks/ 下既有任务记录与 .shell/queue/ledger.jsonl 中仍有大量同类说法：它们由工具维护、只追加，改写会被队列检查拒绝。按新规则，以后的记录不再写。\n- Git 历史与已推送到 GitHub 的内容未改动；已推送的版本中没有这层身份关系的描述。\n- 待施工的 T0013 的批准基线中仍有同类说法（登记于本规则之前）；执行 T0013 时按新规则写回执与文档。\n\n## 未验证\n\n没有独立审阅者核对；用户验收前，以上均为 Agent 自检。\n", "summary": "新增常设规则“不写协作者身份”；11 个文件 32 处身份说法改为中性措辞，含义不变；受管文件（队列以外）检索为 0；Agent 自检，未独立验证；既有任务记录与机器账按规则不改写", "verification": "passed"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
