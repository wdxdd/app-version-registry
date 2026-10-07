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

## 渠道阶段

每个平台按以下发布阶段维护版本信息；Debug（应用壳）阶段与 Release 候选包共用 `releaseCandidate`，不新增独立渠道：

1. Debug（应用壳）/ `releaseCandidate`：开发 Debug 包或本机安装 Release 候选包，验证版本读取、远程检索和状态逻辑。该阶段可以没有升级地址。
2. `testflight`（iOS）或 `internalTesting`（Android）：通过平台测试分发渠道验证真实升级入口。
3. `production`：通过 App Store 或 Google Play 正式分发。

## 修改原则

1. 每个项目只使用一个稳定的 `<project-id>` 目录，优先使用应用包名 / Bundle ID。
2. iOS 与 Android 分开维护；候选包、测试渠道与正式渠道分开维护。
3. `version` 使用用户可见的语义版本号，例如 `1.0.0`。
4. `buildNumber` 使用平台构建号；测试阶段必须递增。
5. `storeUrl` 必须是该渠道真实可访问的官方分发地址；`releaseCandidate` 没有官方分发地址时使用 `null`，不得编造。
6. JSON 的 canonical 读取路径为 `platforms.ios.<channel>` 或 `platforms.android.<channel>`；客户端不得把平台渠道当作顶层 `ios` / `android`。
7. 修改 JSON、Schema 或客户端解析后必须通过 JSON 解析、Schema 校验和客户端 canonical-path 集成测试，并在项目历史中记录变更原因。

## 候选包阶段边界

`releaseCandidate` 可以用于验证：

- 当前版本读取；
- 当前构建号读取；
- 远程版本源访问；
- `latest` / `update-available` / `unavailable` 状态转换。

如果 `releaseCandidate.storeUrl` 为 `null`，只能验证检查更新状态，不能验证官方升级跳转。客户端应在用户点击升级时提示当前测试构建没有可用的官方升级渠道，不得伪造商店跳转。
