# 将 devtemplate 适配为 FESTIVA 项目模板

```json
{
  "id": "T0001",
  "revision": 9,
  "assignee": null,
  "parent": null,
  "deps": [],
  "round": 1,
  "status": "通过"
}
```

## 登记依据

用户于当前对话提供 https://github.com/mychmly/devtemplate，并要求把链接里的模板内容改成 FESTIVA 项目内容，生成在“留学生派对”文件夹。目标是让现有项目获得可读的项目入口、区域契约和可运行的本地任务队列，同时保留现有参考图和文档草稿。

## 任务包

- [规划目标](goal.md)
- [执行计划](plan.md)

## 批准基线与回执

- [approval-001.md](approval-001.md)
- [receipt-000004.md](receipt-000004.md)

## 过程记录

- #2｜create｜codex｜{"authority": {"basis": "当前对话：把 https://github.com/mychmly/devtemplate 的模板内容改成 FESTIVA 项目内容并生成在“留学生派对”文件夹", "by": "用户"}, "deps": [], "id": "T0001", "parent": null, "proposal": {"criteria": "| 编号 | 可观察的结果 | 验证方法 | 通过条件 |\n|---|---|---|---|\n| A1 | 项目入口与目标描述 FESTIVA，引用原有文档和参考图 | 阅读 README、truth/goals.md、object/AGENTS.md、reference/README.md | 内容属于 FESTIVA，草稿状态明确，现有图片和草稿未丢失 |\n| A2 | 模板队列可用 | 用 Python 3.12 运行 `tool/shell.py doctor` | protection: ready 且 protocol: 2 |\n| A3 | 模板工具与许可完整 | 比对来源清单并运行 Python 编译检查 | 必需工具和 LICENSE 存在，工具脚本可编译 |\n| A4 | 不指向模板仓库作为 FESTIVA 的推送目标 | 检查 `git remote -v` | 不保留 mychmly/devtemplate 为本项目 origin |\n\n验收安排：Agent 自行核对文件与工具，交付待用户审阅；不代用户记录通过。", "origin": "用户于当前对话提供 https://github.com/mychmly/devtemplate，并要求把链接里的模板内容改成 FESTIVA 项目内容，生成在“留学生派对”文件夹。目标是让现有项目获得可读的项目入口、区域契约和可运行的本地任务队列，同时保留现有参考图和文档草稿。", "plan": "1. 在项目外读取 GitHub 模板并核对当前项目状态。\n2. 逐项合入规则、工具和许可证，改写 FESTIVA 项目信息。\n3. 初始化队列、移除不适合作为项目推送目标的模板远端，运行检查并交付。", "scope": "- 要交付：模板的规则、文档、队列工具与许可证；FESTIVA 的 README、目标、对象说明、参考来源说明和文档检查方法；初始化后的本地队列。\n- 不包含：FESTIVA iOS App 的实现、远端仓库创建或推送、产品文档批准、替用户验收本任务。\n- 允许修改的位置：项目根目录的模板入口、charter、queue、tool、gate、eval、object、reference 的说明文件、truth/goals.md、.shell 队列数据与本地 Git 接线；保留 reference 中用户图片及 truth 中既有两份草稿。", "title": "将 devtemplate 适配为 FESTIVA 项目模板"}}
- #3｜claim｜codex｜{"expect": 2, "id": "T0001"}
- #4｜deliver｜codex｜{"artifacts": [{"path": "README.md", "sha256": "7a6ce5be6e43c9b283b604f953abf059992c99dd47a1b1950f5c22ae57f3d56e"}, {"path": "AGENTS.md", "sha256": "48ebc29d64ce9b64f5bb895259da336ef4ba3fd24baff0c7e58c5060dd8227b7"}, {"path": "truth/goals.md", "sha256": "0c16442ab2648d2005ea08e12f1749284ce961a35da193b0fbd0db8c1d0a0935"}, {"path": "object/AGENTS.md", "sha256": "f2edc767bcde3d2c15ca6e5209ac797344c74361fcf3c00668dd56379ea74fc2"}, {"path": "reference/README.md", "sha256": "1ff2a60a8fac10d7819ae2584f1afea9e2f8fb79072f5e238e6e8b9e0de8945f"}, {"path": "gate/checks.md", "sha256": "5892e147ef5dfa278619b5cf897e6cca4519ea89945ddf39341d4a4d471e0f97"}, {"path": "tool/shell.py", "sha256": "9f3a9ffba3d570dc0bb40aa2b114ac0fbc34b8a70193a825fd8104e1d37b2726"}, {"path": "LICENSE", "sha256": "58d1e17ffe5109a7ae296caafcadfdbe6a7d176f0bc4ab01e12a689b0499d8bd"}], "expect": 3, "id": "T0001", "receipt": "# FESTIVA 模板接入验证回执\n\n执行者：codex；日期：2026-09-28。以下为本次自检，未独立验证，也不代替用户验收。\n\n- A1：已阅读 FESTIVA README、目标、对象说明和参考来源说明；确认 C4 图、10 张高保真 JPG 与两份既有草稿仍在原位。项目文字明确将草稿和示例数据与已批准/已实现能力区分。\n- A2：使用本机 Python 3.12 执行 `tool/shell.py init` 和 `doctor`；返回 `protection: ready`、`protocol: 2`。`state get` 与任务登记、批准、领取亦成功。\n- A3：对照在项目外获取的 devtemplate 来源，29 个模板文件均存在；5 个队列工具 Python 文件与来源哈希一致，语法解析通过；LICENSE 保留。新写入的 4 份项目 Markdown 的本地相对链接检查通过。\n- A4：`git remote -v` 无输出，已移除指向 mychmly/devtemplate 的本地 origin；未创建新远端、未推送。\n- 限制：模板完整回归测试未完成；运行超过三分钟仍在执行大量子进程测试，因本次未修改队列程序而中止。不能据此宣称全套回归测试通过。已有 Git 历史保留，尚未替换为 FESTIVA 自有仓库历史。\n", "summary": "已将模板接入并改写为 FESTIVA 项目，队列可运行；完整模板回归测试未完成", "verification": "passed"}
- #9｜close｜claude｜{"authority": {"basis": "当前对话 2026-09-29：老师指令“T0001 和 T0002 现在通过”", "by": "用户（老师）"}, "expect": 4, "id": "T0001"}

## 接手说明

尚无接手说明。

> 工具生成；状态来自机器账，不可直接编辑。授权为 Agent 代书，未独立见证。
