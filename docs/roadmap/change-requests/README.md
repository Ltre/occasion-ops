# 需求变更申请指南

本目录用于记录**已经确定**的需求变更，保存“原来是什么、现在改成什么、为什么改、会影响什么”的决策历史。

候选想法、尚未确认的问题和调研事项应先记录在相关 roadmap 或 `09-open-questions.md`，不得提前写成已批准变更。

## 1. 文件命名

建议使用：

```text
cr-YYMMDD-功能名称或描述.md
```

例如：

```text
cr-260722-docs-workflow.md
```

如果同一天同一主题有多次独立变更，可以增加序号或更具体的描述。

## 2. 必须记录的内容

每份变更申请至少包含：

- 状态：proposed、approved、implemented、rejected 或 superseded；
- 变更日期和决策人；
- 原来的需求；
- 改动后的需求；
- 变更原因；
- 影响范围；
- 受影响的 roadmap 文件；
- 关联 Issue、开发进度、测试记录和 PR；
- 可选：建议如何实现、迁移或兼容。

## 3. 执行顺序

当变更已经批准时：

1. 创建 change request；
2. 更新原 roadmap 文件，使其体现最新有效需求；
3. 更新领域或技术设计；
4. 创建或更新 GitHub Issue；
5. 创建对应开发进度与测试记录；
6. 实施代码、迁移和测试；
7. 完成后把 change request 状态更新为 `implemented`。

不得只创建 change request 而不更新原 roadmap。change request 是历史记录，roadmap 才是当前有效需求。

## 4. 推荐模板

```markdown
# 需求变更：变更名称

## 元数据

- 日期：YYYY-MM-DD
- 状态：approved
- 决策人：
- 关联 Issue：
- 关联开发进度：
- 关联测试记录：
- 受影响 roadmap：

## 变更摘要

## 原来的需求

## 改动后的需求

## 变更原因

## 影响分析

### 产品与交互

### 领域与数据

### API 与实现

### 数据迁移与兼容

### 测试与验收

### 进度与风险

## 建议如何修改（可选）

## Roadmap 更新清单

## Issue 执行清单

## 完成条件
```

## 5. 状态说明

- `proposed`：已记录，尚未确认；
- `approved`：已确认，必须更新 roadmap 并安排执行；
- `implemented`：roadmap、实现、测试和文档全部完成；
- `rejected`：确认不执行；
- `superseded`：被后续变更替代，必须链接替代文件。
