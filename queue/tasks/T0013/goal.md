# 定稿 C1 系统语境图与 C2 容器图

## 范围

- 要交付：
  1. 工程架构文档第 2、3 节的两个代码块，按规范第 5–8 节重画：自报 `%% name` 与 `%% home`（festiva-c1、festiva-c2）；本系统一族用 `class … shell` 声明并用族色；线型只用三型，每条边带六字以内的标签；节点只含名称、一句职责与技术标签；名称与第 1 节“统一命名”表一致。
  2. 每张图之后一节编号边表：端点、线型、标签与图源逐边等价；语义栏按规范第 7 节写（实线：接口｜归属｜同步或异步｜耦合；虚线：供给｜触发），依据写裁决编号；C2 的外沿边写“C1 边 N”锚，C1 每条边都被 C2 回指。
  3. 工程架构文档增加“容器指针表”（表头：容器｜详设文档｜图源），在 C3 评估之前为空表并注明原因。
  4. tool/diagram/registry.json：`settings.l2_diagrams` 声明 `["festiva-c1", "festiva-c2"]`；确需时登记端点别名。两张图都写好后一并声明，否则检查 (w) 会因缺图报红。
  5. 渲染与导出：truth/architecture/festiva-c1/ 与 festiva-c2/ 下的 SVG、可移植 SVG，以及两份清单。
  6. 设计说明：truth/architecture/festiva-c1/festiva-c1.md 与 festiva-c2/festiva-c2.md（头部六字段、视图注记、C2 的容器注记含“类”栏、规范第 9 节评审清单逐条回执、第 10 节回述五项）。
  7. 工程架构文档第 1–3 节的图例与相关文字随之同步；更新头部版本、章节状态与附录对照；老师逐张确认后，第 2、3 节标“已确认”。
- 不包含：C3（第 4 节的三个组件图继续作为说明图；C2 定稿后另立任务逐个容器评估）；部署视图；工程架构文档第 4–15 节的内容；产品规则；Demo 架构方案；推送到 GitHub。
- 允许修改的位置：truth/FESTIVA-工程架构文档.md（头部、章节状态、第 1–3 节、附录对照）；truth/architecture/festiva-c1/、truth/architecture/festiva-c2/、truth/architecture/manifest.json、truth/architecture/portable-manifest.json（后两者由工具生成）；tool/diagram/registry.json（只改 settings.l2_diagrams 与必要的别名）；队列文件经工具维护。

## 验收标准与验证方法

| 编号 | 可观察的结果 | 验证方法 | 通过条件 |
|---|---|---|---|
| A1 | 两张图按规范重画 | 对照规范第 5–8 节阅读两个图源 | 具名且归巢；本族声明与族色正确；只用三型线且每条边有标签；节点只含名称、职责、技术标签；名称与统一命名表一致 |
| A2 | 三项检查为绿，且确实覆盖两张图 | 运行 `tool/diagram/check.mts` 与夹具 `tool/diagram/render-diagrams-accept.mts` | (w) 报 festiva-c1、festiva-c2 逐边等价；(x) 报外沿边锚齐、语境边全被回指；(e) 两张产物与可移植版一致、零残留；夹具 FAIL 0、SKIP 0 |
| A3 | 设计经得起评审 | 设计说明中的第 9 节评审清单回执与第 10 节回述五项 | 逐条作答；违反项、假设与未定义的边界列为待确认，交老师决定 |
| A4 | 图可读 | 目检两张 SVG 与可移植版 | 文字不截断，每条线可追踪 |
| A5 | 老师逐张确认 | 老师在对话中确认 | C1、C2 各有明确确认；第 2、3 节状态据此标“已确认” |
| A6 | 没有越界 | `git diff` | 只改允许的位置 |

验收安排：Agent 自检后交付，标明未独立验证的部分；老师逐张确认并验收。
