# 开发进度记录指南

本目录保存 OccasionOps 每项开发工作的实时进度，使 ChatGPT Work、Codex 和其他 Agent 能够在跨会话、跨人员或跨 PR 的情况下准确恢复并主动推进。

## 1. 文件命名

统一使用：

```text
dev-YYMMDD-功能名称或描述.md
```

示例：

```text
dev-260722-money-quick-entry.md
```

对应测试记录必须位于：

```text
docs/test-log/test-260722-money-quick-entry.md
```

## 2. 创建时机

以下情况必须创建或更新进度文件：

- 开始实现新的 GitHub Issue；
- 修改已有功能且范围明确；
- 执行数据库迁移、架构调整或重要重构；
- 落实已批准的需求变更；
- 工作预计跨多个 commit、PR、会话或 Agent；
- 因阻塞暂停，需要为后续 Agent 留下恢复信息。

## 3. Agent 工作顺序

开始工作前：

1. 阅读 `docs/README.md`；
2. 阅读相关 roadmap 和 change request；
3. 阅读本目录中最新相关进度文件；
4. 阅读对应 test log；
5. 核对 Issue、PR、commit 和代码状态；
6. 更新进度文件的状态、计划和下一步；
7. 再开始修改代码。

只要没有必须由项目所有者决定的阻塞项，Agent 应继续执行下一条明确任务，而不是停留在建议阶段。

## 4. 状态

- `planned`
- `in-progress`
- `blocked`
- `in-review`
- `completed`
- `cancelled`

## 5. 推荐模板

```markdown
# 开发进度：功能名称

## 元数据

- 日期：YYYY-MM-DD
- 状态：in-progress
- 负责人／Agent：
- 分支：
- 关联 Issue：
- 关联 PR：
- 对应 roadmap：
- 对应变更申请：
- 对应测试记录：`docs/test-log/test-YYMMDD-功能名称或描述.md`

## 目标

## 范围

## 非目标

## 当前进度

- [ ] 待完成事项
- [x] 已完成事项

## 实时工作记录

### YYYY-MM-DD HH:mm

- 完成：
- 发现：
- 决策：
- 下一步：

## 已修改或计划修改的文件

## 关键决策

## 风险与阻塞

## 下一步可执行动作

## 完成条件
```

## 6. 实时更新要求

- 开始实现前写入目标和范围；
- 每完成一个可验证步骤，更新勾选项和工作记录；
- 发现新风险或需求差异时立即记录；
- 代码、迁移、测试和文档路径必须具体；
- 暂停时必须写明下一条命令、文件或决策动作；
- PR 创建后补充链接；
- 完成后把状态改为 `completed`，并确认测试记录已经完成。

## 7. 不得标记完成的情况

- 没有对应测试记录；
- 验收标准未逐项验证；
- 仍有未说明的数据迁移风险；
- 关键权限、审计、幂等或恢复场景未测试；
- roadmap 或 change request 尚未同步；
- 未完成事项只写在备注里，没有独立 Issue。
