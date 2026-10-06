# 版本信息更新与验证流程

## 发布前

1. 确认目标项目目录和平台渠道。
2. 确认 `version`、`buildNumber` 与实际构建产物一致。
3. 确认 `storeUrl` 指向该渠道的官方分发入口。
4. 检查 JSON 语法、Schema 和 BOM / CRLF。
5. 在本地读取公开文件并核对字段。

## 测试阶段

TestFlight 与 Android Internal Testing 必须分别维护。测试版本可以和正式版使用同一状态机，但不得把测试地址写入 production 渠道。

## 状态规则

- 获取失败、字段缺失、平台或渠道不匹配：`unavailable`
- 当前版本和构建号不低于目标版本：`latest`
- 当前版本或同版本构建号低于目标版本：`update-available`

## 更新地址规则

版本清单中的 `storeUrl` 是分发渠道地址。客户端负责优先使用原生商店协议；HTTPS 地址只作为系统无法处理原生协议时的降级入口。
