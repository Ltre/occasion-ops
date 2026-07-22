# 测试记录：文档分支可移植与默认工作分支规则

## 元数据

- 日期：2026-07-22
- 状态：in-progress
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 关联 Issue：待创建
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
- `docs/roadmap/10-chatgpt-work-handoff.md`；
- 已知包含固定分支的历史 dev/test 记录；
- 本次 change request、dev process 与 Issue；
- 分支选择优先级和禁止事项。

## 测试环境

- GitHub 仓库：`Ltre/occasion-ops`；
- 工作分支：由当前 GitHub／执行环境选定；
- 测试方式：GitHub 文件读取、内容审阅、分支差异检查；
- 本地 clone：因环境无法解析 GitHub 域名而不可用；
- 产品代码：本次不涉及。

## 验收标准映射

| 验收标准 | 测试方式 | 状态 | 证据 |
| --- | --- | --- | --- |
| docs 总说明定义分支选择优先级 | 读取文件 | 待验证 | `docs/README.md` |
| 用户未指定时采用环境工作分支 | 内容审阅 | 待验证 | docs 与 Work/Codex 指引 |
| 不默认切换到 main | 内容审阅 | 待验证 | 分支规则与禁止事项 |
| Work 推荐提示不写死临时分支 | 读取文件 | 待验证 | `10-chatgpt-work-handoff.md` |
| dev 模板不预设具体分支 | 读取文件 | 待验证 | `docs/dev-process/README.md` |
| 已知历史 dev/test 记录不再误导 | 逐文件读取 | 待验证 | `dev-260722-docs-workflow.md`、`test-260722-docs-workflow.md` |
| change request、dev、test、Issue 可追溯 | 交叉引用检查 | 待验证 | 本次记录 |

## 自动化与检索记录

- GitHub 代码搜索查询 `dev/2607C-newcode` 未返回结果，仓库代码搜索索引不可作为完整证明；
- 本地 `git clone` 因 DNS 失败不可用；
- 最终验证采用已知文件逐项读取和 GitHub 分支差异检查；
- 后续建议在 CI 或脚本中扫描通用文档的固定分支字样。

## 人工与场景测试

### 场景 1：用户明确指定分支

期望：Agent 使用用户当次指定分支，不被历史文档覆盖。

状态：待验证。

### 场景 2：用户未指定分支

期望：Agent 使用 Codex 或执行环境已配置、检出或选定的工作分支。

状态：待验证。

### 场景 3：文档合并到 main 后从新分支复用

期望：文档不包含要求切回某个历史开发分支的规则。

状态：待验证。

### 场景 4：历史记录包含实际分支

期望：实际分支只能作为特定历史上下文，不得表述成后续默认分支；误导性引用应被改写。

状态：待验证。

## 失败项与缺陷

当前无已确认失败项。

## 未测试项及原因

- 全仓自动扫描：尚无脚本，且当前本地网络无法 clone；
- Codex 实际运行时分支选择：需在下一项真实 Codex 代码工作中验证；
- PR／CI 门禁：尚未实现。

## 最终结论

待文档更新、Issue 创建和逐项验证完成后填写。