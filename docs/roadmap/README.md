# OccasionOps 开发路线图

本目录用于沉淀 OccasionOps 的需求分析、领域边界、分阶段开发计划和已确认需求变更。

文档按主题拆分，避免把所有需求堆在一个文件中；各专题文档既描述“为什么需要”，也给出“第一阶段做什么、后续做什么、如何验收”。

所有 Agent 在使用 roadmap 前，必须先阅读 [`docs/README.md`](../README.md)，并结合实时开发进度与测试记录推进工作。

## 初代版本决策

OccasionOps 初代版本以**资金流水记录及其正确性保障**为唯一首要目标。

初代必须做到：

- 用生活化入口在数秒内记录收款、支出、内部转移、垫付、报销和备用金；
- 允许先留下不完整事实，但不把未确认内容混入正式余额；
- 从模型上区分真实收支、内部转移、垫付和报销；
- 通过幂等、防重复、成对流水、校验、审计和盘点保证结构及业务规则正确；
- 即使 AI 不可用，也能完成全部核心资金流程。

首版实施细节以 [初代资金流水 MVP](./11-initial-money-mvp.md) 为准。采购、物料、任务、施工和 AI 不得阻塞第一个资金试点。

## 客户端与区域技术基线

- **首期正式客户端：PWA + 微信小程序**；
- **后续客户端：Android / iOS，在资金 MVP 和真实试点稳定后评估**；
- PWA 与微信小程序共享服务端 API、资金语义、权限、审计和核心测试；
- 中国大陆生产环境优先使用阿里云 OSS、腾讯云 COS 等国内对象存储；
- 海外部署保留 AWS S3、Cloudflare R2 等国际存储选择；
- 业务代码通过统一 `ObjectStorageProvider` 隔离厂商，不把 S3 作为唯一默认；
- 不默认跨境复制，部署环境必须明确主数据区域。

技术细节见：

- [`docs/tech/README.md`](../tech/README.md)
- [`docs/tech/client-platform-strategy.md`](../tech/client-platform-strategy.md)
- [`docs/tech/object-storage-and-region-strategy.md`](../tech/object-storage-and-region-strategy.md)
- [`docs/tech/backend-architecture.md`](../tech/backend-architecture.md)

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
13. [已确认需求变更](./change-requests/README.md)

## 文档驱动开发流程

### 实时开发进度

每项开发工作必须在 `docs/dev-process/` 中维护实时记录：

```text
dev-YYMMDD-功能名称或描述.md
```

进度文件必须说明当前状态、已完成事项、风险、阻塞、修改文件和下一步可执行动作。Agent 开始或恢复任务时，应先读取最新相关进度文件。

### 实时测试记录

每项开发工作必须在 `docs/test-log/` 中维护对应测试记录：

```text
test-YYMMDD-功能名称或描述.md
```

开发与测试文件使用相同日期和功能描述。没有对应测试记录的功能，不得标记完成。

### 已确定需求变更

已确定的需求变更必须：

1. 在 `docs/roadmap/change-requests/` 中记录原需求、改后需求、原因和影响；
2. 更新受影响的原 roadmap 文件，使其表达最新有效需求；
3. 创建或更新 GitHub Issue 推动设计、实现、测试和迁移；
4. 在对应开发进度与测试记录中引用该变更申请。

Change request 用于保留差异与决策历史，不能替代原 roadmap 的更新。

### Agent 主动推进

只要不存在必须由项目所有者决定的阻塞项，Agent 应持续执行：

```text
读取 roadmap 与 change request
→ 读取最新 dev process 与 test log
→ 确认最小可交付切片
→ 更新实时记录
→ 实现并测试
→ 回写文档、Issue、PR 与结果
→ 继续下一条无阻塞任务
```

完整规则见：

- [`docs/README.md`](../README.md)
- [`docs/dev-process/README.md`](../dev-process/README.md)
- [`docs/test-log/README.md`](../test-log/README.md)
- [`docs/roadmap/change-requests/README.md`](./change-requests/README.md)

## 执行入口

GitHub 总追踪 Issue：[#9 OccasionOps 初代资金 MVP 执行总追踪](https://github.com/Ltre/occasion-ops/issues/9)

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

P0 技术基础还包括：

- PWA 与微信小程序共享 API 契约和业务类型；
- 客户端平台适配接口；
- 附件元数据和 `ObjectStorageProvider`；
- 一个国内生产存储适配器和本地开发适配器；
- 跨端资金场景和存储 Provider 契约测试框架。

### P1：初代资金 MVP

- [#6 交付初代资金流水 MVP](https://github.com/Ltre/occasion-ops/issues/6)
  - [#10 最简资金记录入口与确认摘要](https://github.com/Ltre/occasion-ops/issues/10)
  - [#11 资金守恒、幂等、防重复与审计](https://github.com/Ltre/occasion-ops/issues/11)
  - [#12 垫付、报销与备用金闭环](https://github.com/Ltre/occasion-ops/issues/12)
  - [#13 资金盘点、差异处理与未结事项](https://github.com/Ltre/occasion-ops/issues/13)

P1 交付必须同时在 PWA 与微信小程序通过核心资金验收，并完成国内对象存储的附件上传、私有访问和弱网恢复。

### P2：资金试点后扩展

- [#7 扩展礼金、采购与物料闭环](https://github.com/Ltre/occasion-ops/issues/7)
- [#8 扩展完整现场协同与临时入口](https://github.com/Ltre/occasion-ops/issues/8)

其中 #8 与资金直接相关的快捷记录、待确认、幂等和弱网能力应提前纳入 #6；非资金任务入口可以延后。

P2 还包括：

- 国际对象存储适配器和海外环境验证；
- PWA 与微信小程序体验加固；
- 根据真实需求评估 Android/iOS。

## 总体优先级

- **P0：资金与跨端基础**：最小活动与成员、资金术语、统一资金流水、资金位置、附件证据、权限、审计、幂等、共享 API 契约和存储 Provider。
- **P1：初代可用产品**：PWA 与微信小程序上的收、支、转、垫付、报销、备用金、余额、盘点、待确认、异常和附件。
- **P2：资金增强与区域扩展**：礼金归属、商家结算、采购付款、临时入口、国际存储、海外部署验证和原生端评估。
- **P3：完整活动运营**：物料、任务、施工、车辆、AI 自动整理、自然语言查询和跨活动模板。

## 开发原则

1. 初代优先解决钱的流水记录和正确性，不平均分配研发资源给其他模块。
2. 前台使用生活化动作，后台使用平衡、可追溯的资金模型。
3. PWA 与微信小程序共享业务规则，不在客户端分别定义资金语义。
4. Android/iOS 不阻塞首轮试点，只按真实触发条件启动。
5. 中国大陆部署优先国内云存储，海外部署保留国际存储选择。
6. 业务代码依赖项目存储抽象，不直接绑定单一厂商 SDK。
7. 先解决“事实是否被可靠记录”，再解决复杂审批和报表。
8. 现场端允许不完整记录，但未确认内容不能无提示地进入正式余额。
9. 内部转移、垫付、报销、押金等性质必须由模型保证不会重复计入收支。
10. 重要数据采用追加、更正和作废，不做无痕覆盖。
11. AI 只提供建议和匹配，不直接替代关键资金事实确认。
12. 每个阶段必须形成可演示、可对账、可恢复的业务闭环。
13. 每项执行工作必须关联 GitHub Issue，关键决策必须回写 roadmap、change request 或 ADR。
14. 每项开发必须维护实时 `dev-*` 进度文件和对应的 `test-*` 测试文件。
15. Work 负责长期规划、研究、文档和任务推进；Codex 负责代码、测试、命令和 PR。
16. Agent 在没有决策阻塞时必须主动继续推进，并在暂停时留下精确恢复动作。
