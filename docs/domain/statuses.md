# OccasionOps 状态词典

> 对应 [Issue #1](https://github.com/Ltre/occasion-ops/issues/1)。状态描述“当前可以做什么”，流水描述“已经发生了什么”。同一对象可以同时具有记录状态、业务状态和结算状态，不应塞进一个万能状态字段。

## 1. 状态设计规则

- 状态变化必须由有权限的操作触发并生成审计事件。
- “待整理”表示信息不完整；“待确认”表示事实或责任尚未确认，两者不可混用。
- “已完成”不等于“已验收”，“已付款”不等于“已结清”。
- 作废是终止原记录参与计算，不是删除；更正产生新版本并指向原记录。
- 有争议是附加状态，可以与待确认、已确认或结算中并存；争议期间的可执行操作由权限规则限制。
- 状态名称面向领域；界面可使用更生活化文案，但 API 和测试使用稳定编码。

## 2. 通用记录状态

| 状态 | 编码 | 进入条件 | 允许操作 | 退出条件 |
| --- | --- | --- | --- | --- |
| 草稿 | `DRAFT` | 用户尚未提交，数据只在草稿范围内 | 编辑、删除草稿、提交 | 提交为待整理、待确认或已确认候选 |
| 待整理 | `NEEDS_ORGANIZATION` | 已保留事实或原始输入，但必要结构字段缺失 | 补充字段、拆分候选、关联对象、作废 | 达到确认所需最小字段后进入待确认 |
| 待确认 | `PENDING_CONFIRMATION` | 结构已形成，但金额、数量、归属、交接或责任尚需确认 | 确认、驳回、补充证据、更正候选、提出争议 | 确认为已确认；驳回为已拒绝或作废 |
| 已确认 | `CONFIRMED` | 有权限的人确认事实可进入正式投影 | 关联、更正、作废、提出争议 | 更正后原记录标记已被更正；或作废 |
| 已拒绝 | `REJECTED` | 候选、申请或待确认事实被明确拒绝 | 查看、重新创建候选 | 终态；不进入正式投影 |
| 已被更正 | `SUPERSEDED` | 新的更正记录生效并替代原记录参与计算 | 查看历史、追踪更正链 | 终态；不得恢复为当前记录 |
| 已作废 | `VOIDED` | 有权限的人给出原因并作废 | 查看、审计 | 终态；若需恢复，创建新的正式记录 |

### 通用转换

```text
DRAFT -> NEEDS_ORGANIZATION -> PENDING_CONFIRMATION -> CONFIRMED
   |              |                    |                |---> SUPERSEDED
   |              |                    |                '---> VOIDED
   |              |                    '---> REJECTED
   |              '---> VOIDED
   '---> 删除草稿（仅限尚未提交的本地/个人草稿）
```

AI 候选默认只能进入 `PENDING_CONFIRMATION` 或 `NEEDS_ORGANIZATION`，不得直接进入 `CONFIRMED` 的高风险资金、礼金、库存、权限或责任投影。

## 3. 活动状态

| 状态 | 编码 | 进入条件 | 主要允许操作 |
| --- | --- | --- | --- |
| 筹备中 | `PLANNING` | 活动已创建，主要工作尚在准备 | 成员、需求、预算、任务和场地准备 |
| 执行中 | `ACTIVE` | 现场活动已经开始 | 全部授权现场流水和任务操作 |
| 收尾中 | `WRAP_UP` | 主体活动结束，仍有清场、归还和交接 | 清场、盘点、归还、补录和待办处理 |
| 结算中 | `SETTLING` | 现场工作基本结束，仍有财务或商家事项 | 报销、尾款、退款、押金、差异处理 |
| 已归档 | `ARCHIVED` | 关键闭环完成，负责人确认归档 | 默认只读；经授权可补充更正和审计说明 |

活动归档不得自动关闭未结事项；系统必须在归档前展示未报销、未交账、未退款、未归还和未验收清单，并由负责人明确选择处理或带未结项归档。

## 4. 资金义务与结算状态

### 垫付/报销

| 状态 | 编码 | 进入条件 | 退出条件 |
| --- | --- | --- | --- |
| 待核实 | `ADVANCE_PENDING` | 垫付已提交但事实或用途未确认 | 确认后进入待报销；拒绝后终止 |
| 待报销 | `ADVANCE_UNREIMBURSED` | 垫付已确认且待偿余额大于零 | 部分付款或全部结清 |
| 部分报销 | `ADVANCE_PARTIALLY_REIMBURSED` | 已报销金额大于零且小于应报金额 | 继续报销或经确认调整应报金额 |
| 已报销 | `ADVANCE_REIMBURSED` | 已确认报销分配合计等于应报金额 | 终态；后续退款走更正/反向记录 |
| 有争议 | `ADVANCE_DISPUTED` | 金额、用途或责任被提出争议 | 解决后回到相应结算状态 |

### 备用金

`PENDING_ISSUE`（待发放）→ `OUTSTANDING`（已领待交账）→ `PARTIALLY_ACCOUNTED`（部分交账）→ `SETTLED`（支出、转交与余款已闭合）。

### 订单资金

| 状态 | 编码 | 含义 |
| --- | --- | --- |
| 未付款 | `UNPAID` | 已确认应付但尚无有效付款分配 |
| 部分付款 | `PARTIALLY_PAID` | 有效付款小于当前应付 |
| 已付款 | `PAID` | 有效付款达到当前应付，但交付、退款或押金可能未完成 |
| 待退款 | `REFUND_DUE` | 已确认存在商家应退金额 |
| 部分退款 | `PARTIALLY_REFUNDED` | 已退金额小于应退金额 |
| 待退押金 | `SECURITY_DEPOSIT_DUE` | 押金仍由商家占用且未达到最终处理状态 |
| 结算中 | `SETTLEMENT_IN_PROGRESS` | 应付、应退或扣款仍在处理中 |
| 已结清 | `SETTLED` | 当前版本订单的应付、退款和押金义务均为零 |

## 5. 交接状态

| 状态 | 编码 | 进入条件 | 允许操作 |
| --- | --- | --- | --- |
| 待发起方确认 | `PENDING_SENDER` | 接收方先录入或代理录入交接 | 发起方确认、驳回 |
| 待接收方确认 | `PENDING_RECEIVER` | 发起方已提交交接 | 接收方确认差异、接受、驳回 |
| 双方已确认 | `ACCEPTED_BY_BOTH` | 双方对金额、数量、责任和时间一致 | 进入正式位置/责任投影 |
| 单方确认 | `ACCEPTED_UNILATERALLY` | 业务规则允许单方确认且已记录理由 | 可被复核或提出争议 |
| 有差异 | `MISMATCHED` | 双方确认内容不一致 | 修正交接、拆分差异、提出争议 |
| 已取消 | `CANCELLED` | 交接未生效前被取消 | 终态，不改变当前位置 |

现金、钥匙、设备、车辆和重要物料是否必须双方确认，由数据范围与风险规则决定；不得在实现中写死为所有事项相同。

## 6. 采购需求与订单状态

### 采购需求

`DRAFT`（草稿）→ `PENDING_CONFIRMATION`（待确认）→ `READY_TO_BUY`（待采购）→ `IN_PROGRESS`（采购中）→ `ORDERED`（已下单）→ `FULFILLED`（需求已满足）→ `CLOSED`（相关交付和结算已闭环）。

任一未关闭状态可在给出原因后进入 `CANCELLED`；先买后补录可直接创建 `ORDERED`，但必须标记绕过的前置环节和实际发生时间。

### 采购订单

订单至少分开维护以下状态维度：

| 维度 | 状态 |
| --- | --- |
| 确认 | `PENDING_CONFIRMATION`、`CONFIRMED`、`CANCELLED` |
| 付款 | `UNPAID`、`PARTIALLY_PAID`、`PAID`、`REFUND_DUE`、`PARTIALLY_REFUNDED`、`REFUNDED` |
| 交付 | `NOT_DELIVERED`、`PARTIALLY_DELIVERED`、`DELIVERED`、`RETURN_IN_PROGRESS`、`PARTIALLY_RETURNED`、`RETURNED` |
| 验收 | `NOT_INSPECTED`、`PARTIALLY_ACCEPTED`、`ACCEPTED`、`REJECTED`、`EXCEPTION` |
| 总体结算 | `OPEN`、`SETTLEMENT_IN_PROGRESS`、`SETTLED`、`CLOSED` |

只有交付、验收、应付、退款和押金均满足闭环规则后，订单才可从 `SETTLED` 进入 `CLOSED`。

## 7. 物料义务状态

| 对象 | 状态序列 |
| --- | --- |
| 借入/租赁归还 | `IN_USE` → `RETURN_DUE` → `PARTIALLY_RETURNED` → `RETURNED` |
| 损坏处理 | `DAMAGE_REPORTED` → `ASSESSING` → `COMPENSATION_DUE`/`REPAIRING` → `RESOLVED` |
| 遗失处理 | `LOSS_REPORTED` → `SEARCHING` → `FOUND`/`COMPENSATION_DUE`/`WRITTEN_OFF` |
| 盘点差异 | `VARIANCE_OPEN` → `INVESTIGATING` → `EXPLAINED`/`CORRECTED`/`ACCEPTED_LOSS` → `RESOLVED` |

“已归还”必须由有效归还数量与应归还数量计算，不允许仅修改状态绕过数量校验。

## 8. 任务与验收状态

| 状态 | 编码 | 进入条件 | 退出条件 |
| --- | --- | --- | --- |
| 待确认 | `PENDING_ACCEPTANCE` | 已指派但负责人尚未接受 | 接受、转派或取消 |
| 待开始 | `READY` | 责任已明确且可开始 | 开始、阻塞、取消 |
| 进行中 | `IN_PROGRESS` | 已发生实际执行 | 完成、暂停、阻塞、转交 |
| 等待资源 | `WAITING_FOR_RESOURCE` | 明确缺少资金、物料、车辆或商家 | 资源到位后恢复 |
| 等待他人 | `WAITING_FOR_PERSON` | 等待批准、协助、前置任务或外部反馈 | 条件满足后恢复 |
| 暂停 | `PAUSED` | 主动暂停且有原因 | 恢复、转交或取消 |
| 转交中 | `HANDOVER_PENDING` | 已发起责任转交但尚未生效 | 接收后回到相应执行状态 |
| 已完成待验收 | `COMPLETED_PENDING_VERIFICATION` | 执行人声明完成且该类型需要验收 | 验收通过、退回整改 |
| 已完成 | `COMPLETED` | 无需验收，或验收已通过 | 终态；后续问题另建异常/更正 |
| 异常 | `EXCEPTION` | 出现质量、事故、争议或无法按原计划完成 | 解决后恢复、取消或完成 |
| 已取消 | `CANCELLED` | 给出取消原因 | 终态 |

施工、装饰、清场和商家服务默认需要验收；普通跑腿任务是否需要验收由任务类型决定。

## 9. 争议状态（附加维度）

`NONE` → `OPEN` → `UNDER_REVIEW` → `RESOLVED` 或 `DISMISSED`。

提出争议时必须记录争议对象、提出人、理由和证据。解决争议只记录结论；若结论改变正式数据，仍须通过更正、退款、差异处理或责任变更流水执行。

## 10. 待确认项

- 现金交接和重要物料交接的双确认阈值；
- 活动带未结项归档时的默认权限和提醒周期；
- 采购需求是否在小额紧急场景下省略“待确认”；
- 任务类型的默认验收规则；
- 超时是否作为状态、标签或派生属性（首选派生属性，避免覆盖真实执行状态）。
