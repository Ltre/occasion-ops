# 测试记录：文档驱动开发流程

## 元数据

- 日期：2026-07-22
- 状态：passed
- 工作分支：由当次执行环境确定；本文档不指定后续默认分支
- 被测版本追溯：通过本工作关联 commit 和 Issue
- 关联 Issue：[#14 强制维护实时开发进度、测试记录与需求变更闭环](https://github.com/Ltre/occasion-ops/issues/14)
- 关联 PR：无
- 对应开发进度：`docs/dev-process/dev-260722-docs-workflow.md`
- 对应 roadmap：
  - `docs/roadmap/README.md`
  - `docs/roadmap/10-chatgpt-work-handoff.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-docs-workflow.md`

## 测试目标

验证新的 docs 工作流在结构、命名、内容和交叉引用上保持一致，能够引导 ChatGPT Work、Codex 和其他 Agent 结合 roadmap、开发进度、测试记录、需求变更和 Issues 主动推进。

## 测试范围

- `docs/README.md`；
- `docs/dev-process/README.md`；
- `docs/test-log/README.md`；
- `docs/roadmap/change-requests/README.md`；
- 本次 change request；
- 本次开发进度与测试记录；
- roadmap 和 Work/Codex 交接文档；
- GitHub Issue 与文档的关联。

## 测试环境

- GitHub 仓库：`Ltre/occasion-ops`；
- 工作分支：由当次执行环境选定；本记录不设定项目默认分支；
- 测试方式：GitHub 文件读取、工作分支与基准分支差异检查和人工内容审阅；
- 产品代码和运行环境：本次不涉及。

## 验收标准映射

| 验收标准 | 测试方式 | 状态 | 证据 |
| --- | --- | --- | --- |
| 存在 docs 总入口 | 读取文件 | 通过 | `docs/README.md` |
| 开发进度使用 `dev-` 前缀 | 路径与内容检查 | 通过 | `docs/dev-process/dev-260722-docs-workflow.md` |
| 测试记录使用 `test-` 前缀 | 路径与内容检查 | 通过 | `docs/test-log/test-260722-docs-workflow.md` |
| 开发与测试文件日期和描述配对 | 路径比较 | 通过 | 两个文件均为 `260722-docs-workflow` |
| 已确定变更有 change request | 读取文件 | 通过 | `cr-260722-docs-workflow.md` |
| 原 roadmap 已同步更新 | 读取差异 | 通过 | `docs/roadmap/README.md`、`10-chatgpt-work-handoff.md` |
| Agent 引导包含主动推进规则 | 内容审阅 | 通过 | docs、dev-process 与 Work/Codex 指南 |
| 已创建执行 Issue | GitHub Issue 检查 | 通过 | Issue #14 |
| 文档之间可相互追溯 | 链接与路径检查 | 通过 | change request、dev、test 与 Issue 互相引用 |

## 自动化测试记录

本次没有产品代码测试命令。

### 2026-07-22：GitHub 分支差异检查

- 操作：比较当次工作分支与基准分支；
- 结果：工作分支可读取，新增文档均存在；
- 重点确认：
  - `docs/README.md`；
  - `docs/dev-process/README.md`；
  - `docs/test-log/README.md`；
  - `docs/roadmap/change-requests/README.md`；
  - `dev-260722-docs-workflow.md`；
  - `test-260722-docs-workflow.md`；
  - roadmap 与 Work/Codex 交接更新。

### 2026-07-22：分支表述复核

- 操作：检查本测试记录和对应开发进度是否把历史工作分支写成后续默认规则；
- 结果：已改为“由当次执行环境确定”，实际版本通过 commit、PR 或 Issue 追溯；
- 关联变更：`docs/roadmap/change-requests/cr-260722-branch-selection-policy.md`。

## 人工与场景测试

### 场景 1：Codex 从 docs 入口开始

- 从 `docs/README.md` 可以找到 roadmap、change request、dev process、test log、domain 和 tech；
- 结果：通过。

### 场景 2：恢复一项中断工作

- 从 dev process 可读取状态、已完成内容、风险和下一步可执行动作；
- 从对应 test log 可读取测试状态、失败项和未测项；
- 结果：通过。

### 场景 3：处理已确定需求变更

- change request 指南要求记录原需求、改后需求、原因和影响；
- roadmap 指南要求同步更新原文件并创建 Issue；
- 结果：通过。

### 场景 4：检查命名配对

- 开发记录：`dev-260722-docs-workflow.md`；
- 测试记录：`test-260722-docs-workflow.md`；
- 日期与功能描述一致；
- 结果：通过。

### 场景 5：Agent 主动推进

- docs、dev-process 和 Work/Codex 指南均要求无决策阻塞时继续下一任务；
- 暂停时必须留下阻塞、恢复条件和精确下一步；
- 结果：通过。

## 权限、安全与审计测试

本次不修改产品权限或业务数据。GitHub 写入产生可追溯 commit，Issue #14 记录后续执行要求。

## 幂等、并发、弱网与恢复测试

不适用于本次文档结构变更。规范已明确要求后续资金及产品功能在各自 test log 中记录这些测试。

## 失败项与缺陷

无阻塞性失败项。

## 未测试项及原因

- 自动命名和必填章节校验：尚未实现脚本或 CI；
- PR 门禁：尚未建立 PR 模板或 GitHub Actions；
- 多 Agent 长期协作：需在下一项真实代码开发中持续验证。

以上未测试项已由 Issue #14 跟踪，不影响本次文档工作流基础落地。

## 最终结论

本次文档驱动开发流程的目录、命名、交叉引用、roadmap 同步和执行 Issue 均已验证通过。

本记录仅描述当次测试上下文，不指定后续工作的默认分支。

测试状态：`passed`。