# FESTIVA

FESTIVA 是面向国际学生的 iOS 节日聚会项目，目标是帮助用户发现、创建和参加小型聚会，并清楚判断活动的时间、地点、花费和参加条件。目前仓库以设计与工程文档、参考图和项目协作工具为主；不能把高保真截图当作已经运行的 App。

## 从哪里看起

- [项目目标](truth/goals.md)：当前目标、范围和待决定问题。
- [高保真设计文档（草稿）](truth/FESTIVA-高保真设计文档-草稿.md)：10 张界面图所呈现的页面、路径与设计问题。
- [工程架构文档（草稿）](truth/FESTIVA-工程架构文档-草稿.md)：C4 图中的系统、容器、数据流与工程待确认事项。
- [参考图](reference/)：C4 图与 `high-fi/` 高保真图片。

两份文档都标为草稿。用户确认前，其中的建议和待确认事项不是已批准的产品或技术决定。

## 文件夹用途

| 位置 | 用途 |
| --- | --- |
| `truth/` | 长期目标，以及带明确状态的产品、设计和工程文档 |
| `reference/` | 有来源的 C4 图、高保真图片和其他参考资料 |
| `object/` | 后续源码或正式工作产物的默认位置 |
| `queue/`、`.shell/queue/` | 由工具维护的任务视图与机器账 |
| `charter/`、`AGENTS.md` | 协作规则与公共入口 |
| `gate/`、`eval/` | 检查方法与效果评价方法 |
| `tool/` | 本地任务队列工具及说明 |

## 项目如何协作

用户直接描述要做的事，Agent 负责整理方案、执行和记录。任务队列是本地项目管理工具，不是 FESTIVA App 的运行部分。队列使用 Python 3.10+ 和 Git；此机器的系统 `python3` 是 3.9。当前可用的 Python 3.12 位于 `/Users/shixinyue/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/bin/python3`。例如在项目根目录运行：

```sh
/Users/shixinyue/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/bin/python3 tool/shell.py doctor
```

详细命令见[队列用法](tool/queue-usage.md)。

模板来源：[mychmly/devtemplate](https://github.com/mychmly/devtemplate)，本项目基于其结构改写；保留原模板的 [Apache-2.0 许可证](LICENSE)。模板工具的运行记录不能证明 FESTIVA 产品已经完成，用户验收也不由工具替代。
