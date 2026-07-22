# 开发进度：文档分支可移植与默认工作分支规则

## 元数据

- 日期：2026-07-22
- 状态：completed
- 负责人／Agent：ChatGPT
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 分支来源：当前 GitHub 执行环境
- 关联 Issue：[#15 移除固定分支并遵循执行环境工作分支](https://github.com/Ltre/occasion-ops/issues/15)
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
- 更新开发进度和测试指南及模板；
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
- [x] 创建对应测试记录；
- [x] 更新 `docs/README.md`；
- [x] 更新 `docs/dev-process/README.md`；
- [x] 更新 `docs/test-log/README.md`；
- [x] 更新 `docs/roadmap/10-chatgpt-work-handoff.md`；
- [x] 修正已有开发与测试记录；
- [x] 创建执行 Issue #15；
- [x] 完成验证并将状态更新为 `completed`。

## 实时工作记录

### 2026-07-22：需求确认

- 发现：通用 Work 交接说明将临时开发分支写成固定规划分支；
- 发现：既有 dev/test 记录也直接写入固定分支，可能被后续 Agent 当作默认；
- 决策：文档统一改用“当前工作分支”或“执行环境指定分支”；
- 决策：分支选择顺序为用户当场指令优先，其次 Codex／执行环境当前分支；
- 决策：除非明确要求，不默认切换到 `main`，不擅自创建分支。

### 2026-07-22：文档更新

- 完成：在 `docs/README.md` 中建立分支选择和文档可移植性规则；
- 完成：修改 dev/test 模板，记录分支来源而不是预设分支；
- 完成：重写 Work/Codex 推荐提示，删除固定分支；
- 完成：修正上一轮 dev/test 记录中的误导性固定分支；
- 完成：创建 Issue #15。

### 2026-07-22：误操作与清理

- 误操作：曾短暂创建 `docs/roadmap/change-requests/.keep` 和 `.tmp`；
- 处理：两个文件均立即删除；
- 验证：最终分支差异文件清单中不存在这两个路径；
- 影响：无业务内容和最终目录树影响，但相关创建／删除 commit 会保留在 Git 历史中。

### 2026-07-22：验证完成

- 完成：逐项读取 docs 总规则、Work/Codex 指引和历史 dev/test 元数据；
- 完成：比较工作分支与 `main` 的最终文件清单；
- 结果：已知误导性固定分支全部改为环境工作分支规则；
- 限制：本地环境无法解析 GitHub 域名，未能通过 clone＋grep 做全仓自动扫描；
- 后续：Issue #15 跟踪真实 Codex 任务验证和自动扫描。

## 已修改文件

- `docs/README.md`
- `docs/dev-process/README.md`
- `docs/test-log/README.md`
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
6. PR、commit 和 Issue 是实际分支与变更的主要追溯证据；
7. 具体分支名只有在需求、迁移或历史证据需要时才写入，并必须说明上下文。

## 风险与阻塞

- 当前无阻塞；
- GitHub 代码搜索索引未返回结果，不能作为完整扫描证明；
- 本地环境无法解析 GitHub 域名，不能通过 clone＋grep 做全仓扫描；
- 后续应由文档校验脚本补充固定分支检测；
- 真实 Codex 环境中的默认分支行为仍需下一项代码任务验证。

## 下一步可执行动作

本次文档修正已完成。后续由 Issue #15 推动：

1. 在下一项真实 Codex 代码任务中验证用户指定与环境分支优先级；
2. 增加通用文档固定分支扫描；
3. 考虑在 PR 模板或 CI 中检查分支规则；
4. 根据真实协作反馈更新规范。

## 完成条件

- [x] 变更申请完成条件全部满足；
- [x] 通用文档明确分支选择优先级；
- [x] 已知误导性固定分支已移除；
- [x] 测试记录状态为 `passed`；
- [x] Issue #15 已创建；
- [x] 本文件状态更新为 `completed`。