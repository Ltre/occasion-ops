# OccasionOps 技术文档索引

`docs/tech/` 用于保存已经确定或正在评审的技术架构、平台策略、基础设施约束和实现边界。

所有 Agent 在实施技术任务前，应先阅读：

1. `docs/README.md`；
2. 相关 roadmap 与 change request；
3. 本目录中的相关技术文档；
4. 对应的 `docs/dev-process/dev-*.md` 与 `docs/test-log/test-*.md`；
5. GitHub Issue、PR 与现有代码。

## 当前技术文档

- [服务端技术架构](./backend-architecture.md)
- [客户端平台策略](./client-platform-strategy.md)
- [对象存储与区域部署策略](./object-storage-and-region-strategy.md)

## 文档职责

技术文档负责描述：

- 当前技术决定及适用阶段；
- 为什么这样选择；
- 明确的实现边界和非目标；
- 可替换点与演进触发条件；
- 安全、数据、迁移和测试要求；
- 与 roadmap、change request 和 Issue 的关联。

技术文档不能替代 roadmap。产品范围或优先级发生变化时，必须同步更新相关 roadmap；已经确认的变化必须先记录到 `docs/roadmap/change-requests/`。

## 分支规则

本目录是跨分支复用的长期文档，不绑定某个临时开发分支。实际修改分支按以下顺序确定：

1. 用户在当次提示中明确指定的分支；
2. Codex 环境已经配置、检出或选定的工作分支；
3. 当前执行 Agent 或集成已经选定的目标分支。

除非用户明确要求，不得因历史技术文档中的分支名切换分支，也不得默认写入 `main` 或擅自创建新分支。
