# Schema 说明

`version-manifest.schema.json` 定义各项目版本清单的最小结构。

字段说明：

- `projectId`：稳定项目标识，必须与目录名一致。
- `displayName`：项目显示名称。
- `platforms.ios` / `platforms.android`：平台渠道集合。
- `version`：语义版本号；未确定时可为 `null`，客户端必须降级为无法检查。
- `buildNumber`：构建号；未确定时可为 `null`，客户端必须降级为无法检查。
- `storeUrl`：渠道分发地址；未确定时可为 `null`，客户端不得伪造升级入口。
