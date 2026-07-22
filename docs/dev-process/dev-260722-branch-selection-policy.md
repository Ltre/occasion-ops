# 开发进度：文档分支可移植与默认工作分支规则

## 元数据

- 日期：2026-07-22
- 状态：in-progress
- 负责人／Agent：ChatGPT
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 关联 Issue：待创建
- 关联 PR：无
- 对应 roadmap：
  - `docs/README.md`
  - `docs/roadmap/10-chatgpt-work-handoff.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-branch-selection-policy.md`
- 对应测试记录：`docs/test-log/test-260722-branch-selection-policy.md`

## 目标

移除 docs 中会误导 Agent 的固定开发分支引用，并建立统一规则：用户当场指定分支时优先遵从，否则使用 Codex 或执行环境已选定的工作分支。

## 范围

- 更新 docs 总说明中的分支规则；
- 更新开发进度指南及模板；
- 更新 Work/Codex 交接说明；
- 修正已知历史开发与测试记录中的误导性固定分支；
- 创建 change request、测试记录和执行 Issue；
- 验证通用文档不再绑定临时分支。

## 非目标

- 不重命名或删除现有 Git 分支；
- 不改变仓库默认分支；
- 不修改产品代码；
- 不要求历史 commit、PR 或链接隐藏真实分支信息；
- 不在文档中替 Codex 环境预先选择工作分支。

## 当前进度

- [x] 确认需求与分支选择优先级；
- [x] 创建 change request；
- [x] 创建本开发进度文件；
- [ ] 创建对应测试记录；
- [ ] 更新 `docs/README.md`；
- [ ] 更新 `docs/dev-process/README.md`；
- [ ] 更新 `docs/roadmap/10-chatgpt-work-handoff.md`；
- [ ] 修正已有开发与测试记录；
- [ ] 创建执行 Issue；
- [ ] 验证并将状态更新为 `completed`。

## 实时工作记录

### 2026-07-22

- 发现：通用 Work 交接说明将临时开发分支写成固定规划分支；
- 发现：既有 dev/test 记录也直接写入固定分支，可能被后续 Agent 当作默认；
- 决策：文档统一改用“当前工作分支”或“执行环境指定分支”；
- 决策：分支选择顺序为用户当场指令优先，其次 Codex／执行环境当前分支；
- 决策：除非明确要求，不默认切换到 `main`，不擅自创建分支。

## 已修改或计划修改的文件

- `docs/README.md`
- `docs/dev-process/README.md`
- `docs/roadmap/10-chatgpt-work-handoff.md`
- `docs/dev-process/dev-260722-docs-workflow.md`
- `docs/test-log/test-260722-docs-workflow.md`
- `docs/roadmap/change-requests/cr-260722-branch-selection-policy.md`
- `docs/dev-process/dev-260722-branch-selection-policy.md`
- `docs/test-log/test-260722-branch-selection-policy.md`

## 关键决策

1. `docs/` 是跨分支复用的文档体系，不绑定临时分支；
2. 用户当次明确分支高于环境设置；
3. 用户未指定时，采用 Codex 或当前执行环境的工作分支；
4. 文档中出现的历史分支不得被解释成默认操作分支；
5. Agent 不得擅自默认写入 `main` 或创建新分支；
6. PR、commit 和 Issue 是实际分支与变更的主要追溯证据。

## 风险与阻塞

- 当前无阻塞；
- GitHub 代码搜索索引未返回结果，因此需结合已知文件和逐文件读取验证；
- 本地环境无法解析 GitHub 域名，不能通过 clone＋grep 做全仓扫描；
- 后续可由文档校验脚本补充硬编码分支检测。

## 下一步可执行动作

1. 创建对应 test log；
2. 更新受影响文档；
3. 创建 Issue；
4. 逐文件读取确认规则和已知引用；
5. 更新 change request、dev process 和 test log 最终状态。

## 完成条件

- 变更申请完成条件全部满足；
- 通用文档明确分支选择优先级；
- 已知误导性固定分支已移除；
- 测试记录状态为 `passed`；
- Issue 已创建；
- 本文件状态更新为 `completed`。