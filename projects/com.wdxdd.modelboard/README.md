# ModelBoard 版本信息源

- 项目 ID：`com.wdxdd.modelboard`
- 显示名称：ModelBoard
- iOS Bundle ID / Android application ID：`com.wdxdd.modelboard`
- 客户端读取文件：`version-manifest.json`

## 渠道

- iOS：`releaseCandidate`、`testflight`、`production`
- Android：`releaseCandidate`、`internalTesting`、`production`
- Debug（应用壳）与本机 Release 候选包共用 `releaseCandidate`。

## 当前登记

当前本机工程版本为 iOS `1.0 (1)`、Android `1.0 (1)`；版本清单按 schema 要求以 `1.0.0` 保存 marketing version。候选包阶段的 `storeUrl` 为空，只验证版本检查状态，不伪造升级入口。版本或构建号变更时，须先核对实际平台构建产物并追加 history。
