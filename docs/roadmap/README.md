# OccasionOps 开发路线图

本目录用于沉淀 OccasionOps 的需求分析、领域边界和分阶段开发计划。

文档按主题拆分，避免把所有需求堆在一个文件中；各专题文档既描述“为什么需要”，也给出“第一阶段做什么、后续做什么、如何验收”。

## 初代版本决策

OccasionOps 初代版本以**资金流水记录及其正确性保障**为唯一首要目标。

初代必须做到：

- 用生活化入口在数秒内记录收款、支出、内部转移、垫付、报销和备用金；
- 允许先留下不完整事实，但不把未确认内容混入正式余额；
- 从模型上区分真实收支、内部转移、垫付和报销；
- 通过幂等、防重复、成对流水、校验、审计和盘点保证结构及业务规则正确；
- 即使 AI 不可用，也能完成全部核心资金流程。

首版实施细节以 [初代资金流水 MVP](./11-initial-money-mvp.md) 为准。采购、物料、任务、施工和 AI 不得阻塞第一个资金试点。

## 文档索引

1. [产品范围与原则](./00-product-scope.md)
2. [统一流水与领域模型](./01-domain-model.md)
3. [资金、礼金与结算](./02-finance-and-ledger.md)
4. [采购、供应商与物料](./03-procurement-and-inventory.md)
5. [人员、任务、场地与施工](./04-people-tasks-venue.md)
6. [现场交互与低门槛体验](./05-field-ux.md)
7. [AI 辅助与自动整理](./06-ai-and-automation.md)
8. [权限、安全、审计与非功能要求](./07-security-and-nfr.md)
9. [阶段交付计划](./08-delivery-plan.md)
10. [开放问题与调研清单](./09-open-questions.md)
11. [ChatGPT Work 交接与执行说明](./10-chatgpt-work-handoff.md)
12. [初代资金流水 MVP](./11-initial-money-mvp.md)

## 执行入口

GitHub 总追踪 Issue：[#9 OccasionOps P0/P1 执行总追踪](https://github.com/Ltre/occasion-ops/issues/9)

P0 领域词典：

- [领域术语表](../domain/glossary.md)
- [流水类型词典](../domain/flow-types.md)
- [状态词典](../domain/statuses.md)
- [关联关系词典](../domain/relations.md)

### P0：资金实现所需基础

- [#1 建立领域术语、流水类型与状态词典](https://github.com/Ltre/occasion-ops/issues/1)
- [#2 收集真实业务故事并建立场景测试集](https://github.com/Ltre/occasion-ops/issues/2)
- [#3 定稿活动、成员、角色与数据范围模型](https://github.com/Ltre/occasion-ops/issues/3)
- [#4 设计统一流水、关联、更正与审计基础](https://github.com/Ltre/occasion-ops/issues/4)
- [#5 设计资源位置、幂等与并发一致性机制](https://github.com/Ltre/occasion-ops/issues/5)

P0 不要求先设计所有业务领域，只需优先定稿资金 MVP 会使用的概念、权限、流水、位置、审计和一致性规则。

### P1：初代资金 MVP

- [#6 实现资金、垫付、报销与结算 MVP](https://github.com/Ltre/occasion-ops/issues/6)

### P2：资金试点后扩展

- [#7 实现礼金、采购与物料闭环 MVP](https://github.com/Ltre/occasion-ops/issues/7)
- [#8 实现现场快捷入口、临时用户与弱网工作台](https://github.com/Ltre/occasion-ops/issues/8)

其中 #8 与资金直接相关的快捷记录、待确认、幂等和弱网能力应提前纳入 #6；非资金任务入口可以延后。

## 总体优先级

- **P0：资金基础**：最小活动与成员、资金术语、统一资金流水、资金位置、附件证据、权限、修改历史、幂等和恢复。
- **P1：初代可用产品**：最简单的收、支、转、垫付、报销、备用金、余额、盘点、待确认和异常处理。
- **P2：资金增强与关联领域**：礼金归属、商家结算增强、采购付款关联、临时入口和弱网体验加固。
- **P3：完整活动运营**：物料、任务、施工、车辆、AI 自动整理、自然语言查询和跨活动模板。

## 开发原则

1. 初代优先解决钱的流水记录和正确性，不平均分配研发资源给其他模块。
2. 前台使用生活化动作，后台使用平衡、可追溯的资金模型。
3. 先解决“事实是否被可靠记录”，再解决复杂审批和报表。
4. 现场端允许不完整记录，但未确认内容不能无提示地进入正式余额。
5. 内部转移、垫付、报销、押金等性质必须由模型保证不会重复计入收支。
6. 重要数据采用追加、更正和作废，不做无痕覆盖。
7. AI 只提供建议和匹配，不直接替代关键资金事实确认。
8. 每个阶段必须形成可演示、可对账、可恢复的业务闭环。
9. 每项执行工作必须关联 GitHub Issue，关键决策必须回写 roadmap 或 ADR。
10. Work 负责长期规划、研究、文档和任务推进；Codex 负责代码、测试、命令和 PR。
