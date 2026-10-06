# 项目目录约定

## 项目标识

`project-id` 使用项目在分发平台上的稳定标识，优先级如下：

1. Android application ID / iOS Bundle ID 相同：使用该值，例如 `com.lingzhu.musepearl`。
2. 两个平台标识不同：使用 `ios.<bundle-id>` 与 `android.<application-id>` 分目录，或在项目文档中登记唯一映射。
3. 禁止使用易变化的产品显示名作为唯一标识。

## 标准目录

```text
projects/
└── <project-id>/
    ├── README.md
    ├── version-manifest.json
    └── history/
        └── README.md
```

## 标准渠道

- 通用候选包：`releaseCandidate`
- iOS 测试分发：`testflight`
- Android 测试分发：`internalTesting`
- 正式分发：`production`

`releaseCandidate` 表示本机安装的 Release 候选包，不等于 TestFlight 或 Google Play 测试轨道。它可以没有 `storeUrl`，用于验证版本检查状态；要验证“去升级”，必须配置真实分发地址。
