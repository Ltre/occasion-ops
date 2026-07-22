# 测试记录：文档分支可移植与默认工作分支规则

## 元数据

- 日期：2026-07-22
- 状态：passed
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 分支来源：当前 GitHub 执行环境
- 被测版本追溯：通过相关 commit 与 Issue #15
- 关联 Issue：[#15 移除固定分支并遵循执行环境工作分支](https://github.com/Ltre/occasion-ops/issues/15)
- 关联 PR：无
- 对应开发进度：`docs/dev-process/dev-260722-branch-selection-policy.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-branch-selection-policy.md`
- 对应 roadmap：
  - `docs/README.md`
  - `docs/roadmap/10-chatgpt-work-handoff.md`

## 测试目标

验证 docs 中的通用规则不再绑定临时开发分支，并能正确引导 Agent 在用户未指定分支时使用 Codex 或执行环境当前工作分支。

## 测试范围

- `docs/README.md`；
- `docs/dev-process/README.md`；
- `docs/test-log/README.md`；
- `docs/roadmap/10-chatgpt-work-handoff.md`；
- 已知包含固定分支的历史 dev/test 记录；
- 本次 change request、dev process 与 Issue；
- 分支选择优先级和禁止事项；
- 最终目录树中是否残留误建临时文件。

## 测试环境

- GitHub 仓库：`Ltre/occasion-ops`；
- 工作分支：由当前 GitHub／执行环境选定；
- 测试方式：GitHub 文件读取、内容审阅、分支差异检查；
- 本地 clone：因环境无法解析 GitHub 域名而不可用；
- 产品代码：本次不涉及。

## 验收标准映射

| 验收标准 | 测试方式 | 状态 | 证据 |
| --- | --- | --- | --- |
| docs 总说明定义分支选择优先级 | 读取文件 | 通过 | `docs/README.md` |
| 用户未指定时采用环境工作分支 | 内容审阅 | 通过 | docs 与 Work/Codex 指引 |
| 不默认切换到 main | 内容审阅 | 通过 | 分支规则与禁止事项 |
| Work 推荐提示不写死临时分支 | 读取文件 | 通过 | `docs/roadmap/10-chatgpt-work-handoff.md` |
| dev 模板不预设具体分支 | 读取文件 | 通过 | `docs/dev-process/README.md` |
| test 模板不预设具体分支 | 读取文件 | 通过 | `docs/test-log/README.md` |
| 已知历史 dev/test 记录不再误导 | 逐文件读取 | 通过 | `dev-260722-docs-workflow.md`、`test-260722-docs-workflow.md` |
| change request、dev、test、Issue 可追溯 | 交叉引用检查 | 通过 | 本次记录与 Issue #15 |
| 临时 `.keep` 和 `.tmp` 不在最终目录树 | 分支差异检查 | 通过 | compare 文件清单无对应路径 |

## 自动化与检索记录

### GitHub 代码搜索

- 查询：历史固定开发分支字样；
- 结果：未返回结果；
- 结论：仓库代码搜索索引不可作为完整证明。

### 本地 clone＋grep

- 操作：尝试 clone 当前仓库后扫描 docs；
- 结果：环境无法解析 `github.com`，clone 失败；
- 结论：未能执行全仓自动扫描。

### GitHub API 逐文件验证

已读取并验证：

- `docs/README.md`：明确用户当次指定优先，否则使用环境工作分支；
- `docs/roadmap/10-chatgpt-work-handoff.md`：删除固定规划分支和固定分支推荐指令；
- `docs/dev-process/dev-260722-docs-workflow.md`：改为当次执行环境分支；
- `docs/test-log/test-260722-docs-workflow.md`：改为当次执行环境分支；
- dev/test 指南模板：不再预设具体分支名。

### 最终分支差异检查

- 操作：比较工作分支与 `main`；
- 结果：受影响文档均存在，误建的 `.keep` 与 `.tmp` 不在最终文件清单；
- 注意：临时文件的创建与删除 commit 会保留在 Git 历史中，但最终树无残留。

## 人工与场景测试

### 场景 1：用户明确指定分支

- 规则：用户当次提示优先于执行环境与历史文档；
- 结果：通过文档规则审阅。

### 场景 2：用户未指定分支

- 规则：使用 Codex 或执行环境已配置、检出或选定的工作分支；
- 结果：通过文档规则审阅；真实 Codex 行为由 Issue #15 继续验证。

### 场景 3：文档合并到 main 后从新分支复用

- 规则：通用文档不要求切回历史开发分支；
- 结果：通过。

### 场景 4：历史记录包含实际分支

- 规则：具体分支只能作为特定历史上下文，不能成为后续默认；
- 结果：已知误导性 dev/test 表述已修正，通过。

### 场景 5：Agent 遇到历史文档和环境分支冲突

- 规则：执行环境当前分支高于历史文档中的分支描述；用户当次指令又高于执行环境；
- 结果：通过文档规则审阅。

## 失败项与缺陷

无阻塞性失败项。

## 未测试项及原因

- 全仓自动扫描：当前无可用 clone 网络和扫描脚本；
- Codex 实际运行时分支选择：需在下一项真实 Codex 代码工作中验证；
- PR／CI 分支与文档门禁：尚未实现。

以上未测试项已由 Issue #15 跟踪，不影响本次文档规则落地。

## 最终结论

分支选择优先级、文档可移植性、开发与测试模板、Work/Codex 交接规则和已知历史记录均已完成修正。

测试状态：`passed`。