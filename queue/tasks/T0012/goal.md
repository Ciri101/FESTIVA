# 克隆 envshell 架构制图机制到 FESTIVA

## 范围

- 要交付：
  1. `tool/diagram/`：逐件搬入 envshell packs/diagram 实例版的 render-diagrams.mts、export-portable-svg.mts、checks.mts、render-diagrams-accept.mts、package.json、package-lock.json、puppeteer-config.json，只改导入路径与面向用户的路径文字，加来源注记；新写 lib.mts（替代 envshell tool/lib.mts 中用到的 ROOT、truth 目录、listMdFiles、readDoc、docBase）、check.mts（独立检查入口：装载三项检查，支持对暂存内容检查，红即非零退出）、pre-commit.sh（提交钩子逻辑，暂存改动触及 truth/ 或 tool/diagram/ 时才运行）、install-hook.sh（本机接线脚本）；registry.json（settings 按 FESTIVA 填写：arch_zone＝truth/architecture，design_doc＝truth/FESTIVA-工程架构文档.md，product_prefix＝空串，l2_diagrams 暂空待正式架构图任务声明）；AGENTS.md（按 FESTIVA 改写的工具区规则与用法）。渲染依赖从本机 envshell 的 node_modules 复制（不联网），不入库。
  2. `truth/architecture/`：AGENTS.md（区规则）、《架构设计与制图规范.md》、《治理细则.md》——规则条目全部保留；EnvShell 专有内容（本环境对照表、跨仓命名统一、条款号、T 编号沿革、EnvShell 现态）换成 FESTIVA 的对应说法或注明不适用；工具未实装的条目如实标注。
  3. 按现状渲染工程架构文档的 8 张图：`truth/architecture/` 下 8 张 SVG（暂名 图1…图8）、`portable/` 下 8 张可移植 SVG、manifest.json 与 portable-manifest.json（由工具生成）。
  4. 本机提交钩子：`.git/hooks/pre-commit` 与 `pre-merge-commit` 两个薄接线，调用 tool/diagram/pre-commit.sh；现有队列钩子会先执行它们。
  5. 登记与指针：tool/catalog.md 登记制图工具；gate/checks.md 增加制图检查项；truth/AGENTS.md 增加一行指向 architecture/；.gitignore 排除 tool/diagram/node_modules/。
- 不包含：按规范重画 FESTIVA 正式架构图、声明层二图名与容器指针表（另立任务）；修改工程架构文档等其他 truth 文档；搬入 envshell 自己的四张图；README.md（其链接与说明归 T0003 一致性检查）；推送到 GitHub；联网安装依赖；学生电脑上的安装（只写安装说明）。
- 允许修改的位置：truth/architecture/（新增内容；老师建的空目录 “untitled folder” 不动）、tool/diagram/（新增）、tool/catalog.md、gate/checks.md、truth/AGENTS.md、.gitignore、本机 .git/hooks/pre-commit 与 .git/hooks/pre-merge-commit（不入库）；队列文件经工具维护。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 工具在本仓可运行 | 运行 `node tool/diagram/render-diagrams.mts` 与 `node tool/diagram/export-portable-svg.mts` | 生成 8 张 SVG 与 8 张可移植 SVG，两份清单写入；导出器自检通过 |
| A2 | 三项检查在本仓为绿 | 运行 `node tool/diagram/check.mts` 与 `node tool/diagram/check.mts --staged` | (e)(w)(x) 无红；层二未声明而跳过的部分如实报告 |
| A3 | 夹具通过 | 在本仓运行 render-diagrams-accept.mts；另在草稿区用 settings 填满层二的副本运行一次 | 本仓：未跳过的用例全部 PASS，跳过项写明原因；副本：全部 PASS |
| A4 | 提交钩子生效 | 在草稿区的本地克隆仓装上钩子，分别提交合规改动、陈旧图改动和不涉及 truth/ 的改动；本仓运行 `python3 tool/shell.py doctor` | 合规提交通过；陈旧图被拒绝并显示 (e) 红；不涉及 truth/ 的提交不跑检查；doctor 仍为 protection: ready |
| A5 | 规范完整搬入 | 对照 envshell 三份规则文档逐节核对，回执附对照表 | 每节有落点（保留、改写或注明不适用及理由）；EnvShell 专有内容不作为 FESTIVA 规则残留 |
| A6 | 工具代码与上游一致 | `diff` envshell packs/diagram 与 tool/diagram 的同名 .mts | 差异只在导入路径、面向用户的路径文字与来源注记 |

验收安排：Agent 自检后交付，标明未独立验证的部分；老师验收。
