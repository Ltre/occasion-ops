# 开发进度：密钥与敏感配置管理基线

## 元数据

- 日期：2026-07-22
- 状态：completed
- 负责人／Agent：ChatGPT
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 分支来源：当前 GitHub 执行环境
- 关联 Issue：[#17 建立仓库零秘密与分层 Secret 管理基线](https://github.com/Ltre/occasion-ops/issues/17)
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
- 本次不执行完整历史 Git Secret 扫描；
- 本次不修改产品代码；
- 本次不作具体云厂商采购决定。

## 当前进度

- [x] 确认仓库零秘密要求；
- [x] 确认单机最低使用仓库外受限目录；
- [x] 确认多节点使用远程加密 Secret Store＋本地受限落地；
- [x] 新增 `docs/tech/secrets-and-sensitive-configuration.md`；
- [x] 更新 `docs/tech/README.md`；
- [x] 更新 `docs/roadmap/07-security-and-nfr.md`；
- [x] 创建 change request；
- [x] 创建开发进度和测试记录；
- [x] 创建执行 Issue #17；
- [x] 完成文档一致性验证；
- [x] 将状态更新为 `completed`。

## 实时工作记录

### 2026-07-22：需求确认

- 完成：确认所有 API 配置、Token、密码、私钥等真实值不得进入代码仓库；
- 完成：确认示例配置只能保存占位符和 Secret 引用；
- 完成：确认单机使用仓库外有限权限目录、只读挂载或 `tmpfs`；
- 完成：确认多节点采用远程加密 Secret Store、工作负载身份和本地短期受限落地；
- 决策：环境变量不作为长期生产 Secret 的首选承载，只允许作为不可避免的短期引导方式；
- 决策：关键 Secret 缺失时安全失败，非关键增强服务可明确降级。

### 2026-07-22：技术与 roadmap 同步

- 完成：定义 Secret 范围、仓库零秘密、泄露处置和配置分离；
- 完成：定义本地开发、单机服务、多节点远程存储和分层交付模型；
- 完成：定义最小权限、区域隔离、CI/CD、轮换、日志脱敏和测试要求；
- 完成：定义 `SecretReference` 与 `SecretProvider` 建议接口；
- 完成：将 P0/P1 实现要求写入安全 roadmap；
- 完成：创建 Issue #17 推动代码、CI 和基础设施实现。

### 2026-07-22：误操作与清理

- 误操作：曾短暂创建 `docs/tech/.placeholder` 和 `docs/tech/.tmp`；
- 处理：两个文件均立即删除；
- 验证：最终分支差异文件清单中不存在这两个路径；
- 影响：无业务内容和最终目录树影响，但创建／删除 commit 会保留在 Git 历史中。

### 2026-07-22：验证完成

- 完成：逐项读取 Secret 技术基线的仓库、单机、多节点、CI/CD、轮换和日志章节；
- 完成：确认技术索引已加入强制安全入口；
- 完成：确认安全 roadmap 已加入 P0/P1 工作项和验收标准；
- 完成：比较工作分支与 `main` 的最终文件清单；
- 结果：文档基线和执行计划完成，代码实现由 Issue #17 跟踪。

## 已修改文件

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

- 当前文档工作无阻塞；
- 远程 Secret Store 的具体产品尚未选择，但不阻塞接口和安全边界；
- 历史仓库是否已存在 Secret 尚未执行自动扫描，由 Issue #17 验证；
- 真实权限、轮换和多节点故障行为需代码和部署环境完成后测试。

## 下一步可执行动作

本工作项已完成。后续由 Issue #17 推动：

1. 建立提交、Git 历史、PR 和构建产物 Secret 扫描；
2. 实现 `SecretReference`、`SecretProvider` 和本地受限目录 Provider；
3. 实现权限校验、日志脱敏和安全失败；
4. 多节点生产前接入远程加密 Secret Store 与工作负载身份；
5. 建立轮换、撤销、审计、告警和恢复测试。

## 完成条件

- [x] change request 完成条件全部满足；
- [x] 技术文档与安全 roadmap 一致；
- [x] 执行 Issue 已创建；
- [x] 测试记录状态为 `passed`；
- [x] 本文件状态更新为 `completed`。
