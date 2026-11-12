<!-- CODEGRAPH_START -->

## CodeGraph

In repositories indexed by CodeGraph (a `.codegraph/` directory exists at the repo root), reach for it BEFORE grep/find or reading files when you need to understand or locate code:

- **MCP tools** (when available): `codegraph_explore` answers most code questions in one call — the relevant symbols' verbatim source plus the call paths between them. `codegraph_node` returns one symbol's source + callers, or reads a whole file with line numbers. If the tools are listed but deferred, load them by name via tool search.
- **Shell** (always works): `codegraph explore "<symbol names or question>"` and `codegraph node <symbol-or-file>` print the same output.

If there is no `.codegraph/` directory, skip CodeGraph entirely — indexing is the user's decision.

<!-- CODEGRAPH_END -->

#

--- project-doc ---

## 项目简介

TODO（项目定制）：待补充项目目标、范围和主要产出。

## 技术栈与数据边界

TODO（项目定制）：待补充技术栈、业务数据边界、数据存储、服务端职责、通信方式、隐私保护与数据保留规则。

## 项目目录地图

- 项目根目录：放项目级 Agent 工作约定、全局说明和配置。
- `doc/requirements/`：存放跨任务维护的产品需求、已确认规则和验收标准；涉及产品行为时优先读取这里。
- `doc/design/`：存放跨任务维护的已确认 UI、交互和技术设计资料。
- `doc/tasks/`：存放用户要求新增的项目任务；每个任务的文件夹集中存放该任务的需求、设计和调研文件。
- `doc/decisions/`：存放项目各模块的实现决策；根索引文件为 `doc/decisions/index.md`。
- `doc/memory.md`：存放用户明确要求记录且经用户批准的分类记忆。
- `doc/reviews/archive/YYYY-MM/`：按月份归档阶段性评审、调研和其他中间材料，特别是无需长期维护的材料。此处内容仅供参考，不作为当前产品规则的唯一来源。
- `assets/requirements/`：存放需求和设计文档引用的截图、图片等素材。

## 工作规则

- 除非用户明确要求，禁止创建、委派或使用子智能体；不得仅因任务可并行而主动创建子智能体。
- Git 提交说明使用简短、准确的中文。
- 测试优先编写集成测试，覆盖关键业务流程和组件协作；仅在需要验证独立逻辑或集成测试难以覆盖的边界情况时补充单元测试，避免为实现细节编写大量单元测试。
- 文件或资料不知道该放在哪个目录时，先询问用户，不要自行猜测或创建新目录。
- 当用户要求新增项目任务时，在 `doc/tasks/` 下创建以该任务名称命名的文件夹，并将该任务相关的 requirements、design、research 文件统一放入该文件夹；此规则不适用于 App 中的 Todo。
- 当用户明确要求“记下”或“记住”某项内容时，先检查 `doc/memory.md`，整理拟记录的内容并确定所属类别，然后向用户展示拟写入内容并征求批准；获得批准后才能写入。按类别维护记忆，不要直接在文件末尾追加：若内容已存在或用户是在修正旧记忆，应更新或合并对应条目；保留其他仍有效的记忆，仅在确有需要时新增类别。
- 使用 UI 原型实现界面时，必须先实际运行原型，并对待实现的界面和关键状态截图，再依据截图实现视觉效果。对于需要交互才能出现的弹窗或其他界面状态，必须使用 Playwright 操作原型、触发对应状态并截图。实现时还须还原原型的交互方式；具体业务逻辑则以 `doc/requirements/`、`doc/design/` 及相关 `doc/tasks/<任务名>/` 中已确认的文件为准，不用参考ui原型。
- 所有任务汇报，问题的回答默认使用i-have-adhd技能

## 项目决策记录

- 开始涉及项目代码、设计或文档变更的任务前，先读取 `doc/decisions/index.md`，再根据索引按需读取相关模块的决策文件。
- 决策按模块分层组织。根据当前项目结构、已有决策和本次任务确定模块划分与层级；根索引维护模块及其决策位置。
- 新增或更新决策时，先扫描根索引定位模块，再将内容写入该模块的恰当位置；不得直接追加到文件末尾。
- 每项决策须是可约束后续同类开发的长期模块规则；单次任务、用例或文件的具体实现，不作为决策。
- 每项决策包含状态（已确认、暂定或已废弃）、日期、决策内容、理由或约束，以及关联文件（如有）。“关联文件”是该决策直接依据、约束、修改或影响的需求文档、设计文档、源代码、配置或测试文件的项目相对路径；尚无具体文件时可省略。
- 新决策与已有决策明确冲突时，暂停写入，说明旧决策、新提议及影响，提出建议并请求用户指示；信息不完整但未明确冲突时，标记为“暂定”并说明待确认事项。
- 某模块的决策内容超过 80 行时，将其详细决策拆分到独立 Markdown 文件；根索引保留简短结论、相对路径和具体标题位置。
- 被替代的历史决策标记为“已废弃”，并注明或链接替代决策。
