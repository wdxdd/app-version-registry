# 版本信息更新与验证流程

## 版本清单与客户端解析契约

版本清单必须使用以下 canonical 结构：

```text
platforms.ios.<channel>
platforms.android.<channel>
```

`releaseCandidate`、`testflight`、`internalTesting` 和 `production` 都必须由 Schema 明确定义。修改版本清单或客户端解析时，必须同时执行 JSON 解析、Schema 校验和真实 canonical JSON 读取测试；不能只测试版本比较函数。

## 渠道阶段

### 1. Release 候选包

本机安装的 Release 候选包使用 `releaseCandidate`。该阶段用于验证当前版本、构建号、远程 JSON 和三种状态。由于包可能通过 Xcode / adb 本机安装，`storeUrl` 可以为 `null`。

如果候选包发现新构建但没有 `storeUrl`，客户端可以显示“有可用更新”，但点击升级时必须明确提示当前测试构建没有可用的官方升级渠道。

### 2. 测试分发

- iOS TestFlight 使用 `testflight`。
- Android Google Play 内部测试使用 `internalTesting`。

这两个阶段必须填写真实测试分发地址，才能验证“去升级”跳转。

### 3. 正式分发

iOS App Store 和 Android Google Play 正式分发使用 `production`，填写正式商店地址。

## 发布前

1. 确认目标项目目录和平台渠道。
2. 确认 `version`、`buildNumber` 与实际构建产物一致。
3. 确认 `storeUrl` 与渠道匹配；候选包无官方分发地址时允许为 `null`。
4. 检查 JSON 语法、Schema 和 BOM / CRLF。
5. 在本地读取公开文件并核对字段。

## 状态规则

- 获取失败、字段缺失、平台或渠道不匹配：`unavailable`
- 当前版本和构建号不低于目标版本：`latest`
- 当前版本或同版本构建号低于目标版本：`update-available`

## 更新地址规则

版本清单中的 `storeUrl` 是分发渠道地址。客户端负责优先使用原生商店协议；HTTPS 地址只作为系统无法处理原生协议时的降级入口。`releaseCandidate` 的空地址不应被替换成虚假商店链接。
