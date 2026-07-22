# 开发进度：首期客户端与区域对象存储策略

## 元数据

- 日期：2026-07-22
- 状态：completed
- 负责人／Agent：ChatGPT
- 工作分支：由当前执行环境确定；本文档不绑定固定分支
- 分支来源：当前 GitHub 执行环境
- 关联 Issue：[#16 建立 PWA、小程序与区域对象存储技术基线](https://github.com/Ltre/occasion-ops/issues/16)
- 关联 PR：无
- 对应 roadmap：
  - `docs/roadmap/00-product-scope.md`
  - `docs/roadmap/README.md`
- 对应变更申请：`docs/roadmap/change-requests/cr-260722-client-and-storage-platform.md`
- 对应测试记录：`docs/test-log/test-260722-client-and-storage-platform.md`

## 目标

将首期客户端平台和对象存储区域策略正式写入技术文档与 roadmap，消除“只做 PWA”与“默认 S3 存储”的歧义，并形成后续可直接拆解实现的技术基线。

## 范围

- 新增 `docs/tech/README.md`；
- 新增客户端平台策略；
- 新增对象存储与区域部署策略；
- 更新服务端技术架构；
- 更新产品范围和 roadmap 索引；
- 创建 change request、test log 和执行 Issue；
- 验证文档一致性和交叉引用。

## 非目标

- 本次不实现 PWA、微信小程序、Android 或 iOS 代码；
- 本次不采购云资源；
- 本次不最终决定 OSS 与 COS 中哪一家作为生产提供者；
- 本次不创建真实海外部署；
- 本次不提供法律或合规结论；
- 本次不执行附件数据迁移。

## 当前进度

- [x] 确认首期客户端为 PWA 与微信小程序；
- [x] 确认 Android/iOS 延后；
- [x] 确认国内对象存储优先、国际存储可选；
- [x] 新增技术文档索引；
- [x] 新增客户端平台策略；
- [x] 新增对象存储与区域策略；
- [x] 更新服务端技术架构；
- [x] 创建 change request；
- [x] 创建本开发进度记录；
- [x] 创建对应测试记录；
- [x] 更新产品范围与 roadmap 索引；
- [x] 创建执行 Issue #16；
- [x] 完成文档验证；
- [x] 将状态更新为 `completed`。

## 实时工作记录

### 2026-07-22：需求确认

- 完成：确定首期正式客户端为 PWA 与微信小程序；
- 完成：明确 Android/iOS 不阻塞资金 MVP；
- 完成：确定中国大陆部署优先国内对象存储；
- 完成：确定海外部署保留国际对象存储选择；
- 决策：业务层定义自有 `ObjectStorageProvider`，不把 S3 兼容性当作唯一抽象；
- 决策：国内首期生产只需先落地 OSS 或 COS 中一个主适配器，另一厂商和国际 Provider 通过相同契约扩展。

### 2026-07-22：技术文档

- 完成：建立 `docs/tech/README.md`；
- 完成：编写 PWA、微信小程序和后续原生端策略；
- 完成：编写国内、海外和迁移对象存储策略；
- 完成：重写服务端架构相关基线，移除 S3 唯一默认和 PWA 单端表述。

### 2026-07-22：Roadmap 与执行入口

- 完成：更新产品范围，加入客户端和区域存储边界；
- 完成：更新 roadmap 总入口，加入 P0/P1/P2 技术任务；
- 完成：创建 Issue #16，覆盖 Monorepo、PWA、小程序、适配层和存储 Provider；
- 完成：建立 change request、dev process 和 test log 交叉引用。

### 2026-07-22：验证完成

- 完成：逐项读取客户端策略、存储策略、服务端架构和 roadmap；
- 完成：确认 PWA 与小程序均为首期正式端；
- 完成：确认 Android/iOS 延后；
- 完成：确认国内优先、海外可选、Provider 隔离和不默认跨境复制；
- 结果：文档基线一致，代码与云资源实现转交 Issue #16。

## 已修改文件

- `docs/tech/README.md`
- `docs/tech/client-platform-strategy.md`
- `docs/tech/object-storage-and-region-strategy.md`
- `docs/tech/backend-architecture.md`
- `docs/roadmap/00-product-scope.md`
- `docs/roadmap/README.md`
- `docs/roadmap/change-requests/cr-260722-client-and-storage-platform.md`
- `docs/dev-process/dev-260722-client-and-storage-platform.md`
- `docs/test-log/test-260722-client-and-storage-platform.md`

## 关键决策

1. PWA 与微信小程序均为首期正式客户端；
2. 两端共享服务端业务语义和测试标准；
3. Android/iOS 在真实需求出现后启动；
4. 国内生产环境优先使用国内云对象存储；
5. 海外环境按区域选择国际或海外对象存储；
6. 不默认跨境复制；
7. 业务层不直接依赖厂商 SDK；
8. 附件元数据、区域和 Provider 可审计；
9. 一个国内主适配器足以启动首期，适配接口必须从第一版存在。

## 风险与阻塞

- 当前文档工作无阻塞；
- OSS 与 COS 的最终生产选择尚未决定，但不阻塞统一 Provider 和契约设计；
- PWA 与小程序 UI 技术栈尚未最终锁定，由 Issue #16 的代码骨架工作评估；
- 上线前仍需对域名、备案、隐私、数据保护和厂商合同进行专门评审；
- 真实可用性、SDK 行为和网络性能需在后续实现与试点中验证。

## 下一步可执行动作

本工作项已完成。后续由 Issue #16 主动推进：

1. 建立 Monorepo 与共享 API 契约；
2. 建立 PWA 和微信小程序基础壳；
3. 定义客户端平台适配层；
4. 实现本地开发和国内生产对象存储 Provider；
5. 验证一个国际 Provider；
6. 为每个代码工作包创建对应 `dev-*` 和 `test-*` 文件。

## 完成条件

- [x] change request 完成条件全部满足；
- [x] 技术文档与 roadmap 一致；
- [x] 执行 Issue 已建立；
- [x] 测试记录状态为 `passed`；
- [x] 本文件状态更新为 `completed`。
