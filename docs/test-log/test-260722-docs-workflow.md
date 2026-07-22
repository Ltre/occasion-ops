# 测试记录：文档驱动开发流程

## 元数据

- 日期：2026-07-22
- 状态：in-progress
- 分支：`dev/2607C-newcode`
- 关联 Issue：待创建
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
- 分支：`dev/2607C-newcode`；
- 测试方式：GitHub 文件读取、分支差异检查和人工内容审阅；
- 产品代码和运行环境：本次不涉及。

## 验收标准映射

| 验收标准 | 测试方式 | 状态 | 证据 |
| --- | --- | --- | --- |
| 存在 docs 总入口 | 读取文件 | 待验证 | `docs/README.md` |
| 开发进度使用 `dev-` 前缀 | 路径与内容检查 | 待验证 | `docs/dev-process/` |
| 测试记录使用 `test-` 前缀 | 路径与内容检查 | 待验证 | `docs/test-log/` |
| 开发与测试文件日期和描述配对 | 路径比较 | 待验证 | 本次两个记录文件 |
| 已确定变更有 change request | 读取文件 | 待验证 | `cr-260722-docs-workflow.md` |
| 原 roadmap 已同步更新 | 读取差异 | 待验证 | `docs/roadmap/README.md` 等 |
| Agent 引导包含主动推进规则 | 内容审阅 | 待验证 | docs 与 dev-process README |
| 已创建执行 Issue | GitHub Issue 检查 | 待验证 | 待创建 |
| 文档之间可相互追溯 | 链接与路径检查 | 待验证 | 相关文档 |

## 自动化测试记录

当前无产品代码测试命令。本次将在文档全部写入后，通过 GitHub 分支差异和逐文件读取验证结构与内容。

## 人工与场景测试

待完成：

1. 模拟 Codex 从 `docs/README.md` 进入；
2. 验证能找到 roadmap、change request、最新 dev process 和对应 test log；
3. 验证暂停后能从“下一步可执行动作”恢复；
4. 验证需求变更流程同时要求更新 roadmap 和 Issue；
5. 验证开发进度和测试记录命名不会混淆。

## 权限、安全与审计测试

本次不修改产品权限或数据。GitHub 写入通过当前集成执行，commit 可追溯。

## 幂等、并发、弱网与恢复测试

不适用于本次文档结构变更。文档规范要求后续产品开发必须记录这些测试。

## 失败项与缺陷

当前无已知失败项。

## 未测试项及原因

- 自动命名和必填章节校验：尚未实现脚本或 CI；
- PR 门禁：尚未建立 PR 模板或 GitHub Actions；
- 多 Agent 实际长期协作：需要在后续真实开发工作中验证。

## 最终结论

待完成 roadmap 更新、Issue 创建和最终分支差异验证后填写。
