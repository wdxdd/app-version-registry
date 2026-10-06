# App Version Registry

跨项目公共版本信息源仓库。

本仓库只保存可公开读取的 App 版本检查元数据，供多个 iOS / Android 项目按稳定项目标识读取。仓库不保存密码、Token、证书、私钥、签名文件或任何其他敏感信息。

## 快速定位

- 项目版本清单：`projects/<project-id>/version-manifest.json`
- 版本清单结构：`schemas/version-manifest.schema.json`
- 项目目录约定：`docs/project-directory-convention.md`
- 更新流程：`docs/update-process.md`
- 智能体协作规则：`AGENTS.md`

当前项目：

- MusePearl：`projects/com.lingzhu.musepearl/version-manifest.json`

## 公开读取

项目客户端只读取自己的项目路径，不读取或推断其他项目的版本信息。

GitHub Raw 地址格式：

```text
https://raw.githubusercontent.com/wdxdd/app-version-registry/main/projects/<project-id>/version-manifest.json
```

## 修改原则

1. 每个项目只使用一个稳定的 `<project-id>` 目录，优先使用应用包名 / Bundle ID。
2. iOS 与 Android 分开维护；测试渠道与正式渠道分开维护。
3. `version` 使用用户可见的语义版本号，例如 `1.0.0`。
4. `buildNumber` 使用平台构建号；测试阶段必须递增。
5. `storeUrl` 必须是该渠道真实可访问的官方分发地址；未确定时使用 `null`，不得编造。
6. 修改 JSON 后必须通过 JSON 解析和 Schema 校验，并在项目历史中记录变更原因。
