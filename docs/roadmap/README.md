# OccasionOps 开发路线图

本目录用于沉淀 OccasionOps 的需求分析、领域边界和分阶段开发计划。

文档按主题拆分，避免把所有需求堆在一个文件中；各专题文档既描述“为什么需要”，也给出“第一阶段做什么、后续做什么、如何验收”。

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

## 执行入口

GitHub 总追踪 Issue：[#9 OccasionOps P0/P1 执行总追踪](https://github.com/Ltre/occasion-ops/issues/9)

### P0：基础阻塞项

- [#1 建立领域术语、流水类型与状态词典](https://github.com/Ltre/occasion-ops/issues/1)
- [#2 收集真实业务故事并建立场景测试集](https://github.com/Ltre/occasion-ops/issues/2)
- [#3 定稿活动、成员、角色与数据范围模型](https://github.com/Ltre/occasion-ops/issues/3)
- [#4 设计统一流水、关联、更正与审计基础](https://github.com/Ltre/occasion-ops/issues/4)
- [#5 设计资源位置、幂等与并发一致性机制](https://github.com/Ltre/occasion-ops/issues/5)

### P1：MVP 工作包

- [#6 实现资金、垫付、报销与结算 MVP](https://github.com/Ltre/occasion-ops/issues/6)
- [#7 实现礼金、采购与物料闭环 MVP](https://github.com/Ltre/occasion-ops/issues/7)
- [#8 实现现场快捷入口、临时用户与弱网工作台](https://github.com/Ltre/occasion-ops/issues/8)

## 总体优先级

- **P0：必须先建立的基础**：活动、成员、角色、统一流水、资源位置、附件证据、修改历史。
- **P1：首个可用闭环**：多账户资金、内部转移、垫付报销、采购到货、物料流转、任务交接和现场入口。
- **P2：现场效率与自动整理**：语音图片候选、待整理工作台、自动匹配、闭环检查和每日简报。
- **P3：增强与扩展**：复杂场地施工、车辆调度、商家协同、自然语言查询、跨活动模板。

## 开发原则

1. 先解决“事实是否被可靠记录”，再解决复杂审批和报表。
2. 先建立统一流水与关联关系，再开发各类管理视图。
3. 现场端必须允许不完整记录，后台再整理确认。
4. 重要数据采用追加、更正和作废，不做无痕覆盖。
5. AI 只提供建议和匹配，不直接替代关键事实确认。
6. 每个阶段都必须能形成可演示、可验收的业务闭环。
7. 每项执行工作必须关联 GitHub Issue，关键决策必须回写 roadmap 或 ADR。
8. Work 负责长期规划、研究、文档和任务推进；Codex 负责代码、测试、命令和 PR。
