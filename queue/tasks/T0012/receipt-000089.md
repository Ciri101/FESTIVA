# T0012 克隆 envshell 架构制图机制到 FESTIVA：验证回执

执行者：claude；日期：2026-09-29。以下为 Agent 自检，未独立验证，不代替老师验收。

## 交付物

1. `tool/diagram/`：render-diagrams.mts、export-portable-svg.mts、checks.mts、render-diagrams-accept.mts、package.json、package-lock.json、puppeteer-config.json（承自 envshell packs/diagram@4a439c5）；新写 lib.mts、check.mts、pre-commit.sh、install-hook.sh、registry.json、AGENTS.md。渲染依赖从本机 envshell 的 node_modules 复制（403 MB，未联网），已由 .gitignore 排除，不入库。
2. `truth/architecture/`：AGENTS.md（区规则）、架构设计与制图规范.md、治理细则.md。老师建的空目录 “untitled folder” 未动。
3. 图纸区本次没有产物与清单（按修订后的范围，8 个无名代码块不进图纸区）。
4. 本机钩子：`.git/hooks/pre-commit` 与 `.git/hooks/pre-merge-commit` 两个薄接线（`sh tool/diagram/install-hook.sh` 写入，不入库），队列钩子 `.git/taskqueue-hooks/` 会先调用它们。
5. 登记与指针：tool/catalog.md 登记制图工具；gate/checks.md 增加“FESTIVA 架构图纸检查”；truth/AGENTS.md 增加一行指向 architecture/；.gitignore 排除 /tool/diagram/node_modules/。

## 过程要点

- 第一轮按“现在按现状渲染”在本仓渲染了工程架构文档的 8 个代码块（图1…图8 与可移植版，草稿区截图目检均可读，第 8 张含 T0003 提交后的 U4 标签）。老师看到后决定“先定稿 C1 和 C2 图，然后再评估决策具体要画哪个容器的 C3 图”，并选择调整方案。于是撤回 T0012，修订为“只收具名代码块、撤掉 8 张渲染”后重新批准。8 张渲染从未提交，已删除。
- 与同一工作树的另一会话（执行 T0003、T0011）协调：等它提交 d055e3b 后再做渲染试验；钩子装在它确认没有未提交改动之后；本任务只暂存自己的文件。

## 验收标准逐项

- **A1 通过**：本仓 `node tool/diagram/render-diagrams.mts` 输出“未发现 mermaid 图块。”，不写产物。草稿区本地克隆仓给工程架构文档的 C1 代码块加上 `%% name: festiva-c1`、`%% home: festiva-c1` 后，渲染器只生成 `festiva-c1/festiva-c1.svg`，导出器只生成 `festiva-c1/portable/festiva-c1-portable.svg`，两份清单写入，导出器自检通过；其余 7 个无名代码块未被收集。可移植版截图目检：样式内联、箭头为实心三角、文字可读。
- **A2 通过**：`check.mts`（工作区）与 `check.mts --staged`（本次暂存内容）退出码均为 0。(e)“无图块，跳过；图纸区零孤儿”；(w) 如实报“未声明 settings.l2_diagrams，层二段跳过”；(x) 如实报“跨层链失去基线，如实跳过”。
- **A3 通过**：本仓夹具 `PASS 17 · FAIL 0 · SKIP 9`，9 个 SKIP 为依赖层二声明的 RG5、RR2、RR3、OG1、OG2、OR1–OR4，逐条打印原因；新增 RG7（具名块入列）与 RR4（无名块不入列）通过。草稿区副本把 `settings.l2_diagrams` 填为 `["festiva-c1","festiva-c2"]` 后：`PASS 26 · FAIL 0`。变异验证：在副本中去掉具名规则，RR4 即转 FAIL（收到 3 块：图1.svg、named-one/named-one.svg、图3.svg）。
- **A4 通过**：草稿区本地克隆仓先 `python3 tool/shell.py init` 接入队列钩子，再装制图钩子，doctor 为 protection: ready。S1 给 C1 加图名但不渲染即提交——被拒，(e) 两项红（缺两份清单）；S2 渲染导出后提交——通过；S3 改无名时序图——通过；S4 改具名 C1 的标签不重渲——被拒，(e) 红“图陈旧或缺渲染：festiva-c1/festiva-c1.svg”；S5 只改 object/——不运行制图检查。本仓装上钩子后 `python3 tool/shell.py doctor` 为 `protection: ready`、`protocol: 2`。第一轮另测过“工作区改了图、只暂存正文”的部分提交，按暂存内容判为通过。
- **A5 通过**：对照表见下节。
- **A6 通过**：与 envshell packs/diagram 的差异行数——render-diagrams.mts 16（导入路径、两处帮助文字、克隆注记、具名收集规则）；export-portable-svg.mts 7（导入路径、帮助文字、克隆注记）；checks.mts 3（仅克隆注记，判据代码零改动）；render-diagrams-accept.mts 54（克隆注记、SKIP 处理、RG7／RR4）；puppeteer-config.json 0；package-lock.json 只改包名（依赖逐项一致）。

## 规范搬入对照（A5）

区规则（envshell truth/architecture/AGENTS.md → FESTIVA truth/architecture/AGENTS.md）：

| 上游 | 落点 |
|---|---|
| 住：四类图纸、每图一目录三件同名、C1／C2 住承载文档代码块、C3 同名成对、机制视图、外系统视图、两份清单、两份细则 | “住什么、不住什么”逐项保留；承载文档改为工程架构文档 |
| 不住：手绘图、生产资料、不进状态包 | 保留；另加 FESTIVA 规则“无名代码块不进本区” |
| 关键不变量：单向机械链、图文对齐 (w)、产物一致与孤儿 (e)、跨层链 (x)、机制视图准入（休眠）、外系统视图、设计对错归评审 | 关键规则 1–5、7 与“住”中的外系统视图；另加关键规则 6“先定 C1、C2，再评估 C3” |
| 转移图型休眠，“未声明图种的 stateDiagram 响亮红” | 不列为规则：上游工具未实装此检查，见《治理细则》第 5 节 |
| schema／命名：`%% name`／`%% home`、产物前缀、头部六字段、边表、豁免记号闭集、指针表记号 | “命名与文件”与关键规则 4；头部字段注明 FESTIVA 不机检 |
| 登记表形态：两份清单、域包登记表 settings | 清单保留；settings 改指 tool/diagram/registry.json |
| 指针 | “怎么用”与各处链接 |

《架构设计与制图规范》：

| 上游节 | 落点 |
|---|---|
| 1 适用判据与本环境对照表 | 1：判据逐条保留；对照表改为 FESTIVA 读法，注明取自工程架构文档草稿、不是设计决定 |
| 2 输入与既有裁决 | 2：保留；既有决定改为 FESTIVA 任务中的裁决记录，并写明先 C1、C2 |
| 3 划边界 | 3：逐条保留 |
| 4 定职责与接口 | 4：逐条保留；接口归属示例改为 App→API 服务、AI 编排服务→云端大模型 |
| 5 图样式语义 | 5：逐条保留；本族改为 FESTIVA；加注现有草稿图的配色不受本节约束 |
| 6 组件命名标准 | 6：七条保留；例名改为示意名；“跨仓命名统一”改为 FESTIVA 术语来源 |
| 7 边表与注记体例 | 7：保留；补写边表列结构与端点解析；耦合第四值改用 FESTIVA 示例；跨仓口径不搬（无对应仓） |
| 8 制图与渲染生产规范 | 8：逐条保留，路径改为 tool/diagram；增“只收具名代码块” |
| 9 评审清单 | 9：逐条保留；违反项落点改为任务回执 |
| 10 回述与交接 | 10：逐条保留；落点改为设计说明与任务回执 |
| 11 机制视图（休眠） | 11：保留，注明 FESTIVA 无实例、无接线 |
| 12 旧节号对照 | 不搬：只服务 envshell 自身历史引用 |

《治理细则》：

| 上游节 | 落点 |
|---|---|
| 1 职责来由 | 1：保留 |
| 2 更新顺序与实时 | 2：保留 |
| 3 跨层判定细则（含本仓现态） | 3：保留；现态改为 FESTIVA（design_doc 已登记、l2_diagrams 待声明） |
| 4 机制视图反查 | 4：保留，注明休眠 |
| 5 转移图型沿革 | 5：保留；如实写明 stateDiagram 条款未实装 |
| 6 细则拆层理由 | 6：保留 |
| 7 本系统四图的正本归属 | 7 本仓现状：改写（EnvShell 专有） |
| 8 自举前验证法（已退场） | 8 与 envshell 的差异：改写（上游内容已退场且只关于 envshell） |
| 9 机检化候选 | 9：保留 |

## 需要老师留意

1. **学生电脑**：钩子是本机配置，不随仓库分发；学生 clone 后要自己运行 `sh tool/diagram/install-hook.sh`。只做检查需要 Node.js 22.6 以上；要渲染还需 `cd tool/diagram && npm ci`（联网下载约 400 MB），由使用者自己决定。
2. **浏览器路径**：`puppeteer-config.json` 沿用 macOS 上 Google Chrome 的标准路径；学生电脑装在别处时要改这一行。
3. **夹具的 9 个 SKIP** 在正式架构图任务声明 `settings.l2_diagrams` 之后应为 0；gate/checks.md 已写入这条通过条件。
4. **设计说明头部六字段**与 registry.json 的 entries 没有机检（envshell 由其机检器检查），靠评审。
5. **钩子可以用 `--no-verify` 绕过**，不是安全边界。
6. 规范中的 FESTIVA 读法对照表与例名只作示意，不是组件定名；定名在正式架构图任务中由老师确认。
7. 两份细则的状态标为“草稿”；老师确认后，可以在本任务返工时改为“已确认”再交付。

## 下一步建议（不在本任务范围）

登记“定稿 C1、C2”任务：按规范第 5 节重画工程架构文档第 2、3 节的两张图（`%% name`／`%% home` 取 festiva-c1、festiva-c2，本系统一族声明，带标签的三型线），各配编号边表并写跨层锚；在 settings 声明两张图名；在工程架构文档加容器指针表；附评审清单回执；老师逐张确认后定稿。C2 定稿后再逐个容器评估 C3。

## 未验证

- 没有独立审阅者；以上均为 Agent 自检。
- 未在学生电脑上安装与运行。
- 本仓尚无具名图，本仓内的渲染与导出只在草稿区克隆仓中实测过。
