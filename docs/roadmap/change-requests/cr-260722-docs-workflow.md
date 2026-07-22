# 需求变更：建立文档驱动的主动开发流程

## 元数据

- 日期：2026-07-22
- 状态：approved
- 决策人：项目所有者
- 关联 Issue：待创建
- 关联开发进度：`docs/dev-process/dev-260722-docs-workflow.md`
- 关联测试记录：`docs/test-log/test-260722-docs-workflow.md`
- 受影响 roadmap：
  - `docs/roadmap/README.md`
  - `docs/roadmap/08-delivery-plan.md`
  - `docs/roadmap/10-chatgpt-work-handoff.md`

## 变更摘要

项目新增统一的文档驱动开发流程。所有 Agent 必须结合 roadmap、实时开发进度和实时测试记录主动推进工作；已确认需求变更必须留下差异记录、更新原 roadmap，并创建 Issue 推动执行。

## 原来的需求

- `docs/roadmap/` 保存需求和开发计划；
- GitHub Issues 用于拆解和跟踪工作；
- Work 负责规划与文档，Codex 负责代码、测试和 PR；
- 没有统一规定每项开发工作必须保存实时进度文件；
- 没有统一规定每项开发工作必须保存对应测试记录；
- 没有专门目录保存已确定需求的前后差异；
- Agent 的主动推进和中断恢复主要依赖 Issue、聊天和已有 roadmap。

## 改动后的需求

### 开发进度

- 每项开发工作必须在 `docs/dev-process/` 中维护实时进度；
- 文件名使用 `dev-YYMMDD-功能名称或描述.md`；
- `docs/dev-process/README.md` 负责引导 Codex 等 Agent 读取 roadmap、进度、测试、Issue 和代码后主动推进；
- 进度记录必须包含状态、范围、已完成事项、风险、阻塞和下一步可执行动作。

### 测试记录

- 每项开发工作必须在 `docs/test-log/` 中维护对应的实时测试记录；
- 文件名使用 `test-YYMMDD-功能名称或描述.md`；
- 测试文件与开发进度文件使用相同日期和功能描述；
- 没有对应测试记录的工作不得标记完成。

### 需求变更

- 已经确定的需求变更必须保存到 `docs/roadmap/change-requests/`；
- 必须记录原需求、改后需求、原因和影响；
- 可选记录建议如何修改；
- 最新有效需求必须同步更新到原 roadmap 文件；
- 必须创建或更新 Issue 推动设计、实现、测试和迁移。

### docs 总入口

- 新增 `docs/README.md`，统一说明目录职责、事实来源、开发记录、测试记录、变更流程、主动推进和完成定义。

## 变更原因

- 长周期项目会跨 ChatGPT Work、Codex、人员、会话和 PR，单靠聊天上下文容易丢失状态；
- roadmap 描述计划，但不能替代实时实现状态；
- Issue 描述任务，但不一定保存详细的中间决策、已修改文件和恢复动作；
- 测试结果需要成为可追溯证据，不能只写在 CI 或口头结论中；
- 已确定需求变更必须保留历史，同时保证原 roadmap 始终表达当前有效需求；
- Agent 需要明确的读取顺序和继续执行规则，减少重复分析和被动等待。

## 影响分析

### 产品与交互

不直接改变终端产品功能，但会提高需求、实现和验证的一致性。

### 领域与数据

不直接改变业务数据模型。未来涉及领域变更时，必须通过 change request 和 roadmap 同步流程执行。

### API 与实现

所有后续代码任务都需要配套开发进度和测试记录。PR 完成定义需要检查这两类文档。

### 数据迁移与兼容

本次无产品数据迁移。历史任务可按需要补充记录，不要求一次性追溯所有旧工作。

### 测试与验收

需要验证：

- 四个目录入口存在；
- 命名规则一致；
- docs 总说明、roadmap 和 Work/Codex 指引没有冲突；
- 变更、进度、测试和 Issue 可相互追溯。

### 进度与风险

新增少量文档维护成本。风险是记录流于形式，因此要求实时更新、具体命令和可执行下一步，不接受空泛总结。

## 建议如何修改

- 在新 Issue 开始时同时创建 `dev-*` 和 `test-*`；
- 使用相同日期和功能描述关联两个文件；
- 在 PR 模板或 CI 中逐步增加文档完整性检查；
- 后续可添加脚本校验文件名、引用关系和必填章节。

## Roadmap 更新清单

- [ ] 更新 `docs/roadmap/README.md`；
- [ ] 更新 `docs/roadmap/08-delivery-plan.md`；
- [ ] 更新 `docs/roadmap/10-chatgpt-work-handoff.md`；
- [x] 新增 `docs/README.md`；
- [x] 新增 `docs/dev-process/README.md`；
- [x] 新增 `docs/test-log/README.md`；
- [x] 新增 `docs/roadmap/change-requests/README.md`。

## Issue 执行清单

- [ ] 创建文档工作流执行 Issue；
- [ ] 后续评估自动校验脚本或 CI 检查；
- [ ] 在新开发工作中实际使用该流程并根据反馈改进。

## 完成条件

- docs 总入口与三个子目录指南完成；
- roadmap 与 Work/Codex 执行说明完成同步；
- 本次开发进度和测试记录完成；
- GitHub Issue 已创建；
- 文档路径、命名和交叉引用验证通过。
