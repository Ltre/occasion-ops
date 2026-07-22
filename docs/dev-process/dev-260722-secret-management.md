# 开发进度：密钥与敏感配置管理基线

## 元数据

- 日期：2026-07-22
- 状态：in-progress
- 负责人／Agent：ChatGPT
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 分支来源：当前 GitHub 执行环境
- 关联 Issue：待创建
- 关联 PR：无
- 对应 roadmap：`docs/roadmap/07-security-and-nfr.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-secret-management.md`
- 对应测试记录：`docs/test-log/test-260722-secret-management.md`

## 目标

建立统一的 Secret 管理技术基线，确保任何 API Key、Token、密码、私钥和其他保密配置都不进入代码仓库，并为单机、多节点、CI/CD、区域部署、轮换和泄露处置提供可执行规则。

## 范围

- 新增 Secret 管理技术文档；
- 更新技术文档索引；
- 更新安全与非功能 roadmap；
- 创建 change request、测试记录和执行 Issue；
- 验证仓库零秘密、受限目录和远程加密 Secret Store 分层要求；
- 明确开发、CI、容器和多节点运行时的 Secret 边界。

## 非目标

- 本次不接入真实云厂商 Secret Manager；
- 本次不创建生产密钥；
- 本次不在文档或测试中保存任何真实 Secret；
- 本次不清理尚未确认存在的历史 Git Secret；
- 本次不修改产品代码；
- 本次不作具体云厂商采购决定。

## 当前进度

- [x] 确认仓库零秘密要求；
- [x] 确认单机最低使用仓库外受限目录；
- [x] 确认多节点使用远程加密 Secret Store＋本地受限落地；
- [x] 新增 Secret 管理技术文档；
- [x] 创建 change request；
- [x] 创建本开发进度记录；
- [ ] 创建对应测试记录；
- [ ] 更新 `docs/tech/README.md`；
- [ ] 更新 `docs/roadmap/07-security-and-nfr.md`；
- [ ] 创建执行 Issue；
- [ ] 完成文档一致性验证；
- [ ] 将状态更新为 `completed`。

## 实时工作记录

### 2026-07-22：需求确认

- 完成：确认所有 API 配置、Token、密码、私钥等真实值不得进入代码仓库；
- 完成：确认示例配置只能保存占位符和 Secret 引用；
- 完成：确认单机使用仓库外有限权限目录、只读挂载或 `tmpfs`；
- 完成：确认多节点采用远程加密 Secret Store、工作负载身份和本地短期受限落地；
- 决策：环境变量不作为长期生产 Secret 的首选承载，只允许作为不可避免的短期引导方式；
- 决策：关键 Secret 缺失时安全失败，非关键增强服务可明确降级。

### 2026-07-22：技术文档

- 完成：定义 Secret 范围、仓库零秘密、泄露处置和配置分离；
- 完成：定义本地开发、单机服务、多节点远程存储和分层交付模型；
- 完成：定义最小权限、区域隔离、CI/CD、轮换、日志脱敏和测试要求；
- 完成：定义 `SecretReference` 与 `SecretProvider` 建议接口。

## 已修改或计划修改的文件

- `docs/tech/README.md`
- `docs/tech/secrets-and-sensitive-configuration.md`
- `docs/roadmap/07-security-and-nfr.md`
- `docs/roadmap/change-requests/cr-260722-secret-management.md`
- `docs/dev-process/dev-260722-secret-management.md`
- `docs/test-log/test-260722-secret-management.md`

## 关键决策

1. 仓库、Git 历史、文档、Issue、日志和构建产物中均不得出现真实 Secret；
2. 仓库只保存配置 Schema、占位符和 Secret 引用；
3. 单机最低使用仓库外受限目录或只读挂载；
4. 多节点必须使用远程加密 Secret Store，不人工复制明文文件；
5. 使用服务级最小权限和工作负载身份；
6. 节点本地只在内存、`tmpfs` 或受限只读目录短期落地；
7. 日志、错误、追踪和健康检查统一脱敏；
8. Secret 支持版本、轮换、撤销、审计和泄露事件处置；
9. Secret 不默认跨区域或跨境复制；
10. 前端、PWA、微信小程序和移动端包中不得包含服务端 Secret。

## 风险与阻塞

- 当前无需求阻塞；
- 远程 Secret Store 的具体产品尚未选择，但不阻塞接口和安全边界；
- 历史仓库是否已存在 Secret 尚未执行自动扫描，应由后续 Issue 验证；
- 本次为文档基线，真实权限、轮换和多节点故障行为需代码实现后测试。

## 下一步可执行动作

1. 创建对应 test log；
2. 更新技术索引和安全 roadmap；
3. 创建 Secret 管理执行 Issue；
4. 验证文档对仓库、单机、多节点、CI/CD 和轮换的要求一致；
5. 将 change request、dev process 和 test log 更新为最终状态；
6. 后续由 Issue 拆解 Secret 扫描、Provider、权限校验、日志脱敏和远程存储实现。

## 完成条件

- change request 完成条件全部满足；
- 技术文档与安全 roadmap 一致；
- 执行 Issue 已创建；
- 测试记录状态为 `passed`；
- 本文件状态更新为 `completed`。
