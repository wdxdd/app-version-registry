# AGENTS.md

## 仓库职责

本仓库是跨项目公共 App 版本信息源。它只维护公开、非敏感的版本元数据，不维护应用业务源码，也不保存任何密码、Token、证书、私钥、Provisioning Profile 或签名材料。

## 目录职责

- `projects/<project-id>/version-manifest.json`：单个项目当前可发布渠道的版本信息。
- `projects/<project-id>/history/`：该项目版本信息变更记录与说明。
- `schemas/`：版本清单 JSON Schema 及 Schema 说明。
- `docs/`：跨项目使用、修改、验证和检索规则。

## 智能体检索规则

1. 先读取根目录 `README.md` 与本文件。
2. 使用当前项目的稳定项目标识定位 `projects/<project-id>/`。
3. 只读取该项目的 `version-manifest.json`，不得用其他项目目录推断当前项目版本。
4. 先按 `Platform.OS` 选择 `ios` 或 `android`，再按构建渠道选择 `testflight`、`internalTesting` 或 `production`。
5. 缺少平台、渠道、版本、构建号或有效分发地址时，客户端必须返回“暂无法检查”，不得当作“已是最新”。
6. 版本比较先比较 `version`，同版本时比较 `buildNumber`。
7. 只有明确为更新可用且有可用 `storeUrl` 时，才允许展示“去升级”。

## 修改规则

- 所有文本使用 UTF-8 无 BOM、LF 行尾、文件末尾保留换行。
- JSON 必须能被标准 JSON 解析器解析。
- 修改公共版本源前，必须检查目标项目目录、项目 ID、平台、渠道和地址是否正确。
- 不得在提交中写入 Secret、Token、密码、证书或私有链接。
- 仓库变更必须先本地验证，再推送。
