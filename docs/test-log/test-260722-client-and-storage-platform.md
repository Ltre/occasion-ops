# 测试记录：首期客户端与区域对象存储策略

## 元数据

- 日期：2026-07-22
- 状态：passed
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 分支来源：当前 GitHub 执行环境
- 被测版本追溯：通过相关 commit 与 Issue #16
- 关联 Issue：[#16 建立 PWA、小程序与区域对象存储技术基线](https://github.com/Ltre/occasion-ops/issues/16)
- 关联 PR：无
- 对应开发进度：`docs/dev-process/dev-260722-client-and-storage-platform.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-client-and-storage-platform.md`
- 对应 roadmap：
  - `docs/roadmap/00-product-scope.md`
  - `docs/roadmap/README.md`

## 测试目标

验证客户端平台和对象存储区域策略在技术文档、服务端架构与 roadmap 中表达一致，能够引导后续 Agent 正确拆解 PWA、微信小程序、Android/iOS 以及国内／海外存储实现。

## 测试范围

- `docs/tech/README.md`；
- `docs/tech/client-platform-strategy.md`；
- `docs/tech/object-storage-and-region-strategy.md`；
- `docs/tech/backend-architecture.md`；
- `docs/roadmap/00-product-scope.md`；
- `docs/roadmap/README.md`；
- 本次 change request、dev process 和 GitHub Issue #16。

## 测试环境

- GitHub 仓库：`Ltre/occasion-ops`；
- 工作分支：由当前 GitHub 执行环境选定；
- 测试方式：逐文件读取、内容审阅、交叉引用和分支差异检查；
- 产品运行环境：本次不涉及；
- 云厂商真实账号：本次不涉及。

## 验收标准映射

| 验收标准 | 测试方式 | 状态 | 证据 |
| --- | --- | --- | --- |
| 首期客户端明确为 PWA + 微信小程序 | 读取技术与 roadmap 文档 | 通过 | 客户端策略、产品范围、roadmap 索引 |
| Android/iOS 明确延后 | 内容审阅 | 通过 | 客户端策略、产品范围 |
| 两端共享业务 API 与资金规则 | 内容审阅 | 通过 | 客户端策略、服务端架构 |
| 国内生产存储优先国内云 | 内容审阅 | 通过 | 存储策略、服务端架构、产品范围 |
| 海外部署保留国际存储选择 | 内容审阅 | 通过 | 存储策略、产品范围 |
| S3 不再是唯一默认抽象 | 内容审阅 | 通过 | Provider 设计、服务端架构 |
| 默认不跨境复制 | 内容审阅 | 通过 | 存储策略、产品范围 |
| change request、dev、test、Issue 可追溯 | 交叉引用检查 | 通过 | 本次记录与 Issue #16 |
| roadmap 与 tech 没有冲突 | 对照审阅 | 通过 | 产品范围、roadmap 索引、技术文档 |

## 自动化测试记录

本次没有运行产品代码测试，因为工作范围是技术决策与文档基线。

后续 Issue #16 的实现阶段必须新增：

- PWA 与微信小程序 API 契约测试；
- 跨端资金场景测试；
- `ObjectStorageProvider` 契约测试；
- OSS/COS 和 S3/R2 适配器测试；
- 上传、下载、短期凭证、幂等和迁移测试。

## 人工与场景测试

### 场景 1：中国大陆首期上线

期望：PWA 和微信小程序访问同一服务端；附件默认进入国内云对象存储；业务代码不直接依赖厂商 SDK。

验证结果：技术文档与 roadmap 均明确该模式。

状态：通过。

### 场景 2：海外环境部署

期望：应用可选择海外区域和国际对象存储，资金和附件语义不因 Provider 改变。

验证结果：存储策略保留 S3、R2 等国际 Provider，并要求统一契约。

状态：通过。

### 场景 3：未来开发 Android/iOS

期望：原生客户端复用 API 契约、领域类型和场景测试，不重新定义资金规则。

验证结果：客户端策略明确原生端触发条件和复用要求。

状态：通过。

### 场景 4：更换对象存储厂商

期望：通过 Provider 适配和迁移流程切换；对象键、哈希、权限和业务关联可验证。

验证结果：存储策略定义 Provider 接口、存储配置、迁移状态、哈希校验和回退流程。

状态：通过。

### 场景 5：未配置跨区域复制

期望：系统不会自动把中国大陆附件复制到海外，或把海外附件复制到中国大陆。

验证结果：技术文档和 roadmap 均明确“不默认跨境复制”。

状态：通过。

## 权限、安全与审计测试

已确认技术文档明确：

- 附件默认私有；
- 服务端鉴权后签发短期凭证；
- 对象键不包含敏感个人信息；
- 存储配置、区域、迁移和删除可审计；
- 微信或浏览器客户端不能绕过服务端权限；
- 资金和附件唯一业务事实保存在 PostgreSQL 元数据和正式领域记录中。

状态：通过。

## 幂等、并发、弱网与恢复测试

已确认技术文档明确：

- 客户端上传和资金提交使用幂等机制；
- 弱网重试不能重复生成附件或资金流水；
- 上传完成回调必须幂等；
- 数据库恢复后附件仍需可定位；
- 存储迁移失败可重试和回退；
- PWA 与小程序本地实现可以不同，但状态语义一致。

状态：通过。

## 分支差异检查

- 新增 `docs/tech/README.md`；
- 新增 `docs/tech/client-platform-strategy.md`；
- 新增 `docs/tech/object-storage-and-region-strategy.md`；
- 更新 `docs/tech/backend-architecture.md`；
- 更新 `docs/roadmap/00-product-scope.md`；
- 更新 `docs/roadmap/README.md`；
- 新增 change request、dev process 和 test log；
- 创建 Issue #16。

## 失败项与缺陷

无阻塞性失败项。

## 未测试项及原因

- PWA 与微信小程序真实运行：尚未实现代码；
- OSS、COS、S3 或 R2 的真实 SDK：尚未接入；
- 中国大陆和海外真实网络性能：需要部署后测试；
- 备案、隐私和数据保护合规：需要上线前专门评审；
- 厂商成本比较：需要结合实际用量和采购条件；
- OSS 与 COS 的最终选择：由后续实现和采购条件决定。

以上未测试项由 Issue #16 及后续拆分任务跟踪，不影响本次技术文档基线通过。

## 最终结论

首期客户端、后续原生端、国内／海外对象存储、Provider 抽象、私有访问和区域原则已经在技术文档与 roadmap 中一致表达。

测试状态：`passed`。
