# AGENTS.md

## 仓库职责

本仓库是跨项目公共 App 版本信息源。它只维护公开、非敏感的版本元数据，不维护应用业务源码，也不保存任何密码、Token、证书、私钥、Provisioning Profile 或签名材料。

## 目录职责

- `projects/<project-id>/version-manifest.json`：单个项目当前可发布渠道的版本信息。
- `projects/<project-id>/history/`：该项目版本信息变更记录与说明。
- `schemas/`：版本清单 JSON Schema 及 Schema 说明。
- `docs/`：跨项目使用、修改、验证和检索规则。

## 渠道阶段

每个平台的版本清单按阶段维护：

- `releaseCandidate`：本机安装 Release 候选包，验证版本检查流程；可以没有 `storeUrl`。
- `testflight`：iOS TestFlight 测试分发。
- `internalTesting`：Android Google Play 内部测试分发。
- `production`：正式 App Store / Google Play 分发。

`testflight` 只用于 iOS，`internalTesting` 只用于 Android。`releaseCandidate` 和 `production` 可按平台使用。

## 智能体检索规则

1. 先读取根目录 `README.md` 与本文件。
2. 使用当前项目的稳定项目标识定位 `projects/<project-id>/`。
3. 只读取该项目的 `version-manifest.json`，不得用其他项目目录推断当前项目版本。
4. 先按 `Platform.OS` 选择 `ios` 或 `android`，再按构建渠道选择 `releaseCandidate`、`testflight`、`internalTesting` 或 `production`。
5. 渠道必须与构建产物和分发方式一致：本机 Release 候选包使用 `releaseCandidate`，TestFlight 使用 `testflight`，Google Play 测试使用 `internalTesting`，正式商店使用 `production`。
6. 缺少平台、渠道、版本或构建号时，客户端必须返回“暂无法检查”，不得当作“已是最新”。
7. 版本比较先比较 `version`，同版本时比较 `buildNumber`。
8. 只有明确为更新可用且有可用 `storeUrl` 时，才允许展示可执行的“去升级”。
9. 版本清单 canonical 路径为 `platforms.ios.<channel>` / `platforms.android.<channel>`；客户端不得依赖顶层 `ios` / `android` 路径。
10. 只有明确为更新可用且有可用 `storeUrl` 时，才允许展示可执行的“去升级”。
11. `releaseCandidate` 没有 `storeUrl` 时仍可返回“有可用更新”，但点击升级必须提示当前测试构建没有可用的官方升级渠道，不得打开伪造地址。

## 修改规则

- 所有文本使用 UTF-8 无 BOM、LF 行尾、文件末尾保留换行。
- JSON 必须能被标准 JSON 解析器解析。
- 修改公共版本源前，必须检查目标项目目录、项目 ID、平台、渠道和地址是否正确。
- 不得在提交中写入 Secret、Token、密码、证书或私有链接。
- 仓库变更必须先本地验证，再推送。
