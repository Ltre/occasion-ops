# 开发进度：文档驱动开发流程

## 元数据

- 日期：2026-07-22
- 状态：in-progress
- 负责人／Agent：ChatGPT
- 分支：`dev/2607C-newcode`
- 关联 Issue：待创建
- 关联 PR：无
- 对应 roadmap：
  - `docs/roadmap/README.md`
  - `docs/roadmap/08-delivery-plan.md`
  - `docs/roadmap/10-chatgpt-work-handoff.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-docs-workflow.md`
- 对应测试记录：`docs/test-log/test-260722-docs-workflow.md`

## 目标

建立一套可供 ChatGPT Work、Codex 和其他 Agent 持续使用的文档工作流，使开发计划、实时进度、测试证据、需求变更和 GitHub Issues 相互关联，并支持中断恢复和主动推进。

## 范围

- 新增 `docs/README.md`；
- 新增 `docs/dev-process/README.md`；
- 新增 `docs/test-log/README.md`；
- 新增 `docs/roadmap/change-requests/README.md`；
- 新增本次 change request、开发进度与测试记录；
- 更新 roadmap 和 Work/Codex 交接规则；
- 创建 GitHub Issue 推动流程长期执行；
- 验证目录、命名和交叉引用。

## 非目标

- 本次不实现自动文档校验脚本；
- 本次不修改产品代码；
- 本次不补写全部历史开发工作的日志；
- 本次不创建完整 PR 模板或 CI 门禁。

## 当前进度

- [x] 确认开发记录命名为 `dev-YYMMDD-功能名称或描述.md`；
- [x] 确认测试记录命名为 `test-YYMMDD-功能名称或描述.md`；
- [x] 新增 `docs/README.md`；
- [x] 新增 `docs/dev-process/README.md`；
- [x] 新增 `docs/test-log/README.md`；
- [x] 新增 `docs/roadmap/change-requests/README.md`；
- [x] 新增本次 change request；
- [x] 新增本开发进度文件；
- [ ] 新增对应测试记录；
- [ ] 更新 `docs/roadmap/README.md`；
- [ ] 更新 `docs/roadmap/08-delivery-plan.md`；
- [ ] 更新 `docs/roadmap/10-chatgpt-work-handoff.md`；
- [ ] 创建执行 Issue；
- [ ] 完成路径、命名和内容验证；
- [ ] 将状态更新为 `completed`。

## 实时工作记录

### 2026-07-22

- 完成：确认文档目录、命名和主动推进要求；
- 完成：建立 docs 总说明、开发进度指南、测试指南和变更申请指南；
- 完成：记录已批准的流程变更；
- 发现：用户早先已明确测试前缀为 `test-`，后续消息中的 `teat-` 属于笔误，因此统一使用 `test-`；
- 决策：开发进度与测试记录使用相同日期和功能描述，以不同前缀配对；
- 下一步：更新原 roadmap 文件和 Work/Codex 交接说明，创建 Issue，完成验证。

## 已修改或计划修改的文件

### 已新增或更新

- `docs/README.md`
- `docs/dev-process/README.md`
- `docs/test-log/README.md`
- `docs/roadmap/change-requests/README.md`
- `docs/roadmap/change-requests/cr-260722-docs-workflow.md`
- `docs/dev-process/dev-260722-docs-workflow.md`

### 待新增或更新

- `docs/test-log/test-260722-docs-workflow.md`
- `docs/roadmap/README.md`
- `docs/roadmap/08-delivery-plan.md`
- `docs/roadmap/10-chatgpt-work-handoff.md`

## 关键决策

1. `docs/README.md` 是所有 Agent 的文档入口；
2. roadmap 表达当前有效需求，change request 表达变更历史；
3. 开发进度和测试记录必须实时维护且成对存在；
4. 没有测试记录的功能不得完成；
5. Agent 在无决策阻塞时必须继续推进；
6. 暂停必须留下精确、可执行的恢复动作；
7. 已确定需求变更必须更新原 roadmap，并创建或更新 Issue。

## 风险与阻塞

- 当前无外部阻塞；
- 尚无自动校验，短期依赖 Agent 和评审遵守流程；
- 后续需评估脚本或 CI 门禁，避免文档遗漏或命名错误。

## 下一步可执行动作

1. 创建 `docs/test-log/test-260722-docs-workflow.md`；
2. 更新三个受影响 roadmap 文件；
3. 创建 GitHub Issue；
4. 获取分支差异并逐项验证文件与命名；
5. 更新测试记录为最终结果；
6. 更新本文件状态为 `completed`。

## 完成条件

- 变更申请中的完成条件全部满足；
- docs 目录指南与 roadmap 规则一致；
- 开发与测试记录命名及交叉引用正确；
- Issue 创建完成；
- 验证结果写入对应测试记录；
- 本文件状态更新为 `completed`。
