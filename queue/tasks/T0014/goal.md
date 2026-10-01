# 仓库内容去除协作者身份关系，并设为常设规则

## 范围

- 要交付：
  1. charter/AGENTS.md“基本约定”新增一条：仓库内容（文档、代码与注释、任务记录与回执）不写协作者的现实身份与彼此关系；任务记录中的授权人写“用户”，引用用户指令时只概述指令内容；项目文档只写决定本身及所在任务，不写决定人。既有任务记录与机器账是只追加的历史，不为此改写。
  2. 以下文件中的身份说法改为中性措辞，含义不变：truth/goals.md、truth/FESTIVA-产品设计文档.md、truth/FESTIVA-工程架构文档.md、truth/ui/FESTIVA-高保真设计文档.md、truth/demo/FESTIVA-Demo架构方案.md、truth/architecture/AGENTS.md、truth/architecture/架构设计与制图规范.md、truth/architecture/治理细则.md、object/AGENTS.md、gate/checks.md、tool/diagram/render-diagrams.mts（只改一行注释）。项目文档里“用户”指 App 用户，因此不用“用户”替代，而是省去决定人，例如“经确认的裁决”“（B1 及其备注）”“2026-09-29 决定”。
  3. 改动的四份项目文档（产品、工程、UI、Demo）版本号递增。
- 不包含：queue/tasks/ 下的任务记录、批准基线、回执与 .shell/queue/ledger.jsonl（工具维护、只追加）；Git 历史与已推送到 GitHub 的内容；“国际学生”“在校学生身份”“Verified student”等产品用词；“裁决单”等流程用词；T0013 的施工内容。
- 允许修改的位置：上述第 1、2 项列出的文件，仅限身份说法、版本号与新增规则。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 当前仓库内容不再有协作者身份关系 | 在 queue/ 与 .shell/ 以外的全部受管文件中检索身份用词，排除上述产品用词 | 结果为 0 |
| A2 | 含义不变 | 逐行阅读 `git diff` | 只有身份说法、版本号与新增规则变化，没有改动任何规则、字段或状态 |
| A3 | 常设规则生效 | 阅读 charter/AGENTS.md | 新规则写明适用范围、授权人写法与既有记录的处理 |
| A4 | 检查与链接正常 | 本地相对链接检查；提交时的制图检查；`python3 tool/shell.py doctor` | 无断链；制图检查为绿；protection: ready |

验收安排：Agent 自检后交付；用户验收。
