# MusePearl 版本信息源

- 项目 ID：`com.lingzhu.musepearl`
- 显示名称：MusePearl / 灵珠
- 客户端读取文件：`version-manifest.json`
- 当前阶段：Release 候选包版本检查配置已建立；真实 TestFlight / Google Play 地址和版本号待实际分发后填写。

## 平台标识

- iOS Bundle ID：`com.lingzhu.musepearl`
- Android application ID：`com.lingzhu.musepearl`

## 渠道

- iOS：`releaseCandidate`、`testflight`、`production`
- Android：`releaseCandidate`、`internalTesting`、`production`

## 客户端解析契约

客户端 canonical 读取路径：`platforms.ios.<channel>` / `platforms.android.<channel>`；不得使用顶层 `ios` / `android`。

## 当前候选包阶段

当前项目本地真机 Release 候选包使用 `releaseCandidate`。候选包可以没有 `storeUrl`，这时只验证版本检查状态，不执行官方商店升级跳转。

空的 `version` 或 `buildNumber` 不是“已是最新”，而是“暂无法检查”。
