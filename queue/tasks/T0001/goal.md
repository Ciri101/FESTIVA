# 将 devtemplate 适配为 FESTIVA 项目模板

## 范围

- 要交付：模板的规则、文档、队列工具与许可证；FESTIVA 的 README、目标、对象说明、参考来源说明和文档检查方法；初始化后的本地队列。
- 不包含：FESTIVA iOS App 的实现、远端仓库创建或推送、产品文档批准、替用户验收本任务。
- 允许修改的位置：项目根目录的模板入口、charter、queue、tool、gate、eval、object、reference 的说明文件、truth/goals.md、.shell 队列数据与本地 Git 接线；保留 reference 中用户图片及 truth 中既有两份草稿。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 项目入口与目标描述 FESTIVA，引用原有文档和参考图 | 阅读 README、truth/goals.md、object/AGENTS.md、reference/README.md | 内容属于 FESTIVA，草稿状态明确，现有图片和草稿未丢失 |
| A2 | 模板队列可用 | 用 Python 3.12 运行 `tool/shell.py doctor` | protection: ready 且 protocol: 2 |
| A3 | 模板工具与许可完整 | 比对来源清单并运行 Python 编译检查 | 必需工具和 LICENSE 存在，工具脚本可编译 |
| A4 | 不指向模板仓库作为 FESTIVA 的推送目标 | 检查 `git remote -v` | 不保留 mychmly/devtemplate 为本项目 origin |

验收安排：Agent 自行核对文件与工具，交付待用户审阅；不代用户记录通过。
