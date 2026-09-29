# 工具清单

## 本地任务队列（模板必备）

- 入口：[shell.py](shell.py)；旧 [task_queue.py](task_queue.py) 兼容入口执行相同检查。
- 规则与格式：[queue_model.py](queue_model.py)（旧协议重放）、[queue_v2.py](queue_v2.py)（五态与窗口）；状态包：[state_pack.py](state_pack.py)。
- 用法：[queue-usage.md](queue-usage.md)。
- 依赖：Python 3.10+、Git；无第三方包、网络或后台服务。
- 写入：初始化接入本机 Git 钩子；维护机器账、任务视图和本机恢复数据。不会自行修改对象产物、提交或推送。
- 验证：[队列回归](../gate/test_task_queue.py)和[状态包与窗口回归](../gate/test_state_queue.py)。

## 项目专用工具

确实需要时写明用途、位置、来源与版本、调用方式、前置条件、副作用及授权要求，不把本次执行结果写在此处。

### 制图工具（tool/diagram/）

- 用途：把架构图纸区 `truth/architecture/` 的 mermaid 图源渲染为 SVG 与可移植 SVG，并跑三项检查——(e) 图源与产物一致、(w) 图文对齐、(x) 跨层对齐；可接为本机提交钩子。
- 位置与说明：[tool/diagram/AGENTS.md](diagram/AGENTS.md)；实例设置在 `tool/diagram/registry.json` 的 `settings`。
- 来源与版本：envshell 仓 `packs/diagram/`（提交 4a439c5），由任务 T0012 克隆；渲染引擎 `@mermaid-js/mermaid-cli` 按 `tool/diagram/package-lock.json` 钉版。
- 前置条件：Node.js 22.6 以上；渲染与导出另需 `cd tool/diagram && npm ci` 安装的依赖与本机 Chrome（路径在 `tool/diagram/puppeteer-config.json`）；只做检查不需要依赖。
- 副作用：渲染器与导出器写 `truth/architecture/` 下的 SVG 与两份清单；`install-hook.sh` 写本机 `.git/hooks/pre-commit` 与 `pre-merge-commit`；检查只读。
- 授权：`npm ci` 需联网下载，属于安装动作；接线本机钩子会改变提交行为。二者都需使用者自己决定，不因登记在此而视为已获准。
- 验证：修改本工具后运行 `tool/diagram/render-diagrams-accept.mts`（红绿夹具，不联网、不起浏览器）。
