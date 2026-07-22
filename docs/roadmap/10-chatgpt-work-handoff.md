# ChatGPT Work、Codex 与 Agent 交接执行说明

## 1. 用途

本文档用于把 OccasionOps 从需求分析平滑交接到 ChatGPT Work、Codex 和其他 Agent 持续推进。

所有 Agent 必须先阅读 `docs/README.md`。GitHub 继续作为事实来源，关键需求、变更、进度、测试、决策和验收结果必须最终回写仓库。

ChatGPT Work 主要负责：

- 持续整理需求与决策；
- 根据 roadmap 拆解工作包；
- 跟踪 GitHub Issues 和交付状态；
- 输出领域模型、原型说明、测试场景和验收报告；
- 维护 change request、开发进度和测试记录；
- 在需要实现代码时，将清晰技术任务交给 Codex。

Codex 主要负责：

- 项目代码、数据库、API 和前端实现；
- 自动化测试、迁移、命令、调试和 CI；
- 持续更新实时开发进度和测试记录；
- 提交 commit、推送分支和创建 PR。

## 2. 当前项目状态

- 仓库：`Ltre/occasion-ops`
- 文档总入口：`docs/README.md`
- 需求与开发计划：`docs/roadmap/`
- 实时开发进度：`docs/dev-process/`
- 实时测试记录：`docs/test-log/`
- 已确定需求变更：`docs/roadmap/change-requests/`
- 当前阶段：初代资金流水 MVP 定义与实现拆解
- 初代最高优先级：最简单、可核对、可追溯的资金流水记录
- 根 README 由项目所有者维护，除非明确要求，不应修改

本说明不绑定固定开发分支。`docs/` 会合并到 `main` 并随未来各分支继续复用。

## 3. 分支选择规则

开始任何写入操作前，按以下顺序确定工作分支：

1. 用户在当次提示中明确指定的分支；
2. Codex 环境已经配置、检出或选定的工作分支；
3. 当前执行 Agent 或集成已经选定的工作分支或目标分支。

用户未在当次提示指定分支时，直接使用执行环境当前工作分支，不需要因历史文档中的分支名切换分支。

除非用户明确要求，不得：

- 默认写入 `main`；
- 擅自创建新分支；
- 因旧 roadmap、dev process 或 test log 中出现过某个分支名而切换；
- 把临时分支写入通用模板或长期规则。

如果执行环境无法确定目标分支，且继续写入存在明显风险，应在 dev process 中记录阻塞、恢复条件和需要项目所有者决定的问题。

## 4. 当前产品决策

初代版本不平均推进资金、采购、物料、任务、施工和 AI。

初代主线是：

1. 用最少操作记录收款、支出、内部转移、垫付、报销和备用金；
2. 通过资金位置、成对流水、幂等、防重复、确认状态、审计和盘点保证结构及业务规则正确；
3. 不完整记录允许先保存，但不直接混入正式余额；
4. 采购、物料和任务只保留与资金关联所需的最小对象；
5. AI 不得成为任何核心资金流程的前置依赖。

初代事实来源优先阅读：

- `docs/README.md`
- `docs/roadmap/README.md`
- `docs/roadmap/11-initial-money-mvp.md`
- `docs/roadmap/02-finance-and-ledger.md`
- `docs/roadmap/05-field-ux.md`
- `docs/roadmap/07-security-and-nfr.md`
- `docs/roadmap/01-domain-model.md`
- 相关 change request、dev process、test log 和 GitHub Issue

## 5. Agent 开始或恢复任务时的读取顺序

每次必须按以下顺序读取：

1. `docs/README.md`；
2. `docs/roadmap/README.md`；
3. 当前功能的 roadmap 文件；
4. `docs/roadmap/change-requests/` 中相关已批准变更；
5. `docs/dev-process/` 中该功能最新的 `dev-*` 文件；
6. `docs/test-log/` 中对应的 `test-*` 文件；
7. GitHub Issue、PR、commit 和现有代码；
8. 当前执行环境的工作分支状态。

如果开发进度或测试记录尚不存在，必须在实际改代码前创建：

```text
docs/dev-process/dev-YYMMDD-功能名称或描述.md
docs/test-log/test-YYMMDD-功能名称或描述.md
```

两个文件使用相同日期和功能描述。

## 6. Work 首次进入时的推荐指令

在 ChatGPT 顶部切换到 Work，从保存 OccasionOps 上下文的同一个 Project 中启动新 Work 对话，然后使用：

```text
继续推进 GitHub 仓库 Ltre/occasion-ops。

初代版本以资金流水记录及正确性保障为唯一首要目标。

分支规则：
- 若我在本次提示中明确指定分支，使用该分支；
- 否则使用 Codex 或当前执行环境已经配置、检出或选定的工作分支；
- 不要根据历史文档中的分支名切换分支；
- 不要默认写入 main 或擅自创建新分支。

先阅读：
- docs/README.md
- docs/roadmap/README.md
- docs/roadmap/11-initial-money-mvp.md
- docs/roadmap/10-chatgpt-work-handoff.md
- 相关 change request
- 相关最新 dev process 与对应 test log
- GitHub Issue #6、#9 及当前执行 Issue

工作规则：
1. 不修改根 README，除非我明确要求；
2. 优先完成资金 MVP 所需最小 P0；
3. 未确认记录不能无提示进入正式余额；
4. 内部转移、垫付、报销和押金不得重复计入真实收支；
5. 每项开发必须创建或更新 dev-* 和对应 test-* 文件；
6. 每个 Issue 必须包含背景、范围、非目标、验收标准和依赖；
7. 已确定需求变更必须先记录 change request，并更新原 roadmap；
8. 涉及代码、测试、迁移和命令时形成清晰任务并交给 Codex；
9. 没有项目所有者决策阻塞时，主动继续下一条可执行任务；
10. AI 不得自动确认高风险资金事实。

先检查开放 Issues、当前工作分支、分支差异、最新开发进度和测试状态，然后开始执行本次最小切片。
```

## 7. Work 与 Codex 的职责边界

### Work 更适合

- 资金场景研究与规则定稿；
- 快速记录流程和确认摘要设计；
- 资金状态机、异常和对账规则；
- roadmap 与 change request 维护；
- 产品原型说明；
- 测试案例与验收清单；
- Issue 拆解和优先级调整；
- 阶段总结、风险清单和决策记录。

### Codex 更适合

- 建立项目代码骨架；
- 数据库、API 和前端实现；
- 编写单元测试、集成测试和迁移脚本；
- 运行命令、调试和修复 CI；
- 提交代码、推送分支和创建 PR。

职责不同不表示文档责任可转移。Work 和 Codex 都必须维护相关 `dev-*` 与 `test-*` 文件，并回写 Issue。

## 8. 主动工作循环

每个资金工作包按以下循环推进：

1. **读取事实来源**：docs 总入口、roadmap、change request、进度、测试、Issue、PR 和代码；
2. **确认工作分支**：用户当次指定优先，否则使用执行环境当前分支；
3. **确认范围**：动作、最小字段、默认值、异常、依赖和验收标准；
4. **建立记录**：创建或更新 dev process 与 test log；
5. **产出设计**：流程、状态机、资金位置、成对流水、接口或页面说明；
6. **建立测试**：正常、重复、弱网、冲突、超额、负余额和盘点差异；
7. **实现代码**：完成最小可交付切片；
8. **验证结果**：余额守恒、收支性质、权限、审计、幂等、恢复和可用性；
9. **回写仓库**：更新 dev process、test log、Issue、PR、roadmap 或 ADR；
10. **主动继续**：没有决策阻塞时进入下一明确任务。

暂停时，进度文件必须记录：

- 当前精确状态；
- 已完成和未完成内容；
- 阻塞原因；
- 恢复条件；
- 下一条命令、文件修改或决策动作。

## 9. 需求变更流程

已经确定的需求变更必须按顺序执行：

1. 创建 `docs/roadmap/change-requests/cr-*.md`；
2. 记录原需求、改后需求、原因、影响和可选实现建议；
3. 更新受影响的原 roadmap 文件；
4. 创建或更新 GitHub Issue；
5. 创建或更新对应 dev process 与 test log；
6. 完成实现、迁移和验证；
7. 将 change request 状态更新为 `implemented`。

尚未确定的想法不得伪装成 approved change request。

## 10. 事实来源优先级

发生冲突时，按以下顺序处理：

1. 用户最新明确指令；
2. 已批准的 change request、ADR 或 GitHub Issue 决策；
3. `docs/roadmap/11-initial-money-mvp.md`；
4. 其他 `docs/roadmap` 业务规则；
5. `docs/domain` 和 `docs/tech`；
6. 最新 `docs/dev-process` 与 `docs/test-log`；
7. 代码中的历史行为；
8. 根 README 的项目介绍。

分支选择属于执行上下文：用户当次分支指令高于执行环境；执行环境当前分支高于历史文档中的分支描述。

若代码与已确认业务规则不一致，应先记录差异，再决定迁移或兼容策略，而不是默认为代码正确。

## 11. 每个 Issue 的完成定义

Issue 完成至少满足：

- 范围内验收标准全部通过；
- 关键边界和异常有测试；
- 资金方向和余额守恒可验证；
- 权限、审计、幂等和恢复要求已覆盖；
- 快速记录流程完成可用性验证；
- 新规则已写入相应 roadmap、change request 或 ADR；
- 对应 dev process 状态为 `completed`；
- 对应 test log 状态为 `passed`，或未通过项已有明确 Issue；
- 没有遗留未说明的数据迁移或分支风险；
- 相关 PR、commit、测试和演示互相链接；
- 未完成事项已拆为新 Issue，而不是隐藏在评论中。

## 12. 当前最优执行顺序

1. 定义初代六类资金动作及最小必填字段；
2. 建立不少于 30 个资金正常与异常场景；
3. 定稿资金位置、交易性质和正式／待确认状态；
4. 定稿最小角色权限、附件、更正和审计；
5. 实现“收到一笔、花了一笔、钱换地方了”；
6. 实现幂等、防重复、理论余额和流水时间线；
7. 实现“我先垫付、给人报销、领／交备用金”；
8. 实现盘点、差异、异常和未结事项；
9. 完成弱网、适老化和连续录入加固；
10. 通过模拟活动和小规模真实活动试点；
11. 试点稳定后，再扩展礼金归属、采购物料和任务协同；
12. 最后进入 AI 候选整理和自动匹配。

任何阶段均不应因为 AI、采购、库存或任务功能尚未完成而阻塞核心资金流程。