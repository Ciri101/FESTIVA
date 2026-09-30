# tool/diagram：制图工具

本目录是架构图纸区 [truth/architecture/](../../truth/architecture/AGENTS.md) 的生产与检查工具：把 mermaid 图源渲染成 SVG、派生可移植 SVG、跑三项检查、在提交时把关。承自 envshell 仓 `packs/diagram/`（提交 4a439c5），由任务 [T0012](../../queue/tasks/T0012/task.md) 克隆；与上游的差异见[《治理细则》](../../truth/architecture/治理细则.md)第 8 节。

## 住什么、不住什么

- 住：渲染器、可移植 SVG 导出器、三项检查、检查入口、提交闸脚本与本机接线脚本、红绿夹具、登记表（`registry.json`，其 `settings` 是本仓全部实例差异）、渲染依赖的钉版（`package.json`、`package-lock.json`）与浏览器路径（`puppeteer-config.json`）。
- 不住：图源、SVG 与清单本身（住图纸区）；渲染依赖的安装目录 `node_modules/`（本机安装，不入库）。

## 关键规则

- 文本图源是唯一正本，SVG 是机器生成的投影，不手改；改了下次渲染就会被覆盖。
- 渲染默认配置头的正本只在渲染器常量 `DEFAULT_HEADER` 一处；图源写了显式头则以显式为准，残缺的头直接报错。清单按注入默认头之后的文本记哈希，所以默认头一变，全部图都要重渲。
- 图源发现逻辑只在渲染器一处，检查复用它，不另写一份。承载文档里只收自报 `%% name:` 的代码块（FESTIVA 规则）。
- 本仓的实例差异全部经 `registry.json` 的 `settings` 进入；改 settings 是填空，改代码是改机制，须按任务进行并跑夹具。
- 外部依赖只住本目录；队列工具保持零依赖。

## 用语对照

各 `.mts` 文件沿用上游注释，读注释时按下表理解：

| 上游用语 | 在 FESTIVA 中指 |
|---|---|
| 本包、制图域包 | `tool/diagram/` |
| 本包登记表、登记表 settings | `tool/diagram/registry.json` 及其 `settings` |
| 机检器、判据插件 | `tool/diagram/check.mts` 装载的 `checks.mts` |
| 提交闸、经提交闸 | `tool/diagram/pre-commit.sh`（本机接线后生效） |
| 图纸区、`settings.arch_zone` | `truth/architecture/` |
| 承载文档、`settings.design_doc` | `truth/FESTIVA-工程架构文档.md` |
| 层一、层二、层三 | C1、C2、C3 |
| 域包装卸、元工具、三池、领域登记表 | envshell 的机制，FESTIVA 不设 |

## 安装（每台电脑一次）

1. Node.js 22.6 或更高（`node --version` 查看）。
2. 渲染依赖：在仓库根运行 `cd tool/diagram && npm ci`。这一步要联网下载约 400 MB，属于安装动作，需使用者自己决定。只做检查不需要这一步，只有渲染和导出需要。
3. 浏览器：`puppeteer-config.json` 的 `executablePath` 填本机 Chrome 的路径，默认是 macOS 上 Google Chrome 的标准位置。渲染器用它渲染，导出器用它烘焙；路径不对时导出器会直接报错。
4. 提交钩子：在仓库根运行 `sh tool/diagram/install-hook.sh`。它在本机 `.git/hooks/` 写入 `pre-commit` 与 `pre-merge-commit` 两个薄接线；队列工具（`python3 tool/shell.py init`）装的钩子会先调用它们。拆下用 `sh tool/diagram/install-hook.sh --uninstall`。钩子是本机配置，不随仓库分发，每个 clone 都要装一次。

## 常用命令

在仓库根运行；下文用 `node-ts` 代指 `node --experimental-strip-types --disable-warning=ExperimentalWarning`。

| 做什么 | 命令 |
|---|---|
| 渲染图源为 SVG，更新 `manifest.json` | `node-ts tool/diagram/render-diagrams.mts` |
| 派生可移植 SVG，更新 `portable-manifest.json` | `node-ts tool/diagram/export-portable-svg.mts` |
| 检查工作区 | `node-ts tool/diagram/check.mts` |
| 检查暂存区（提交钩子就是这样跑的） | `node-ts tool/diagram/check.mts --staged` |
| 查看三项检查各判什么 | `node-ts tool/diagram/check.mts --criteria` |
| 修改本工具后跑夹具 | `node-ts tool/diagram/render-diagrams-accept.mts` |

三项检查：**(e)** 图源与渲染产物一致（含可移植 SVG 与零残留）；**(w)** 架构图文对齐（边表与图源逐边等价）；**(x)** 架构跨层对齐（C1↔C2↔C3 锚点）。检查退出码：0 无红，1 有红，2 检查本身无法运行。

## 画或改一张图的顺序

1. 在任务里取得用户的决定（结构变化先有决定）。
2. 改图源：C1、C2 改承载文档里带 `%% name:` 与 `%% home:` 的代码块；C3、部署视图改 `truth/architecture/<图名>/<图名>.mmd`。
3. 改设计说明里的编号边表与注记，写法见《架构设计与制图规范》第 7 节。新图第一次声明为 C1、C2 时，同时在 `registry.json` 的 `settings.l2_diagrams` 登记图名（语境图在前、容器图在后）。
4. 渲染并导出：先跑 `render-diagrams.mts`，再跑 `export-portable-svg.mts`。
5. 检查：`check.mts` 无红。
6. 目检：打开 SVG 看一遍是否可读（检查不证明可读）。
7. 一起暂存图源、设计说明、`truth/architecture/` 下的产物与清单，再提交；提交钩子会再检查一次暂存内容。

## 提交钩子的行为

- 本次暂存的改动不涉及 `truth/` 与 `tool/diagram/`：不检查，直接放行，交给队列检查。
- 涉及时：找不到 Node.js 22.6 以上就拒绝提交；否则把暂存区里的 `truth/` 导出到临时目录，跑三项检查，有红就拒绝，并提示修法。
- 因为检查的是暂存内容，工作区里没暂存的改动不影响这次提交；但 `registry.json` 读的是工作区版本，改了它要一并暂存。
- 钩子可以被刻意绕过（例如 `--no-verify`），它不是安全边界；绕过等于跳过了图纸区的规则。

## 修改本工具

- 按任务进行；改完跑夹具。夹具在 `settings.l2_diagrams` 声明两张图之前会把 9 个用例记为 SKIP，声明之后 SKIP 须为 0。
- 与 envshell 同步上游时，保留各 `.mts` 开头的克隆注记，并重放其中列出的改动。

返回 [tool 区](../AGENTS.md) · [根契约](../../AGENTS.md)。
