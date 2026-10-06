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

- iOS：`testflight`、`production`
- Android：`internalTesting`、`production`

如果项目存在其他受控渠道，必须先在项目 README 中说明，再扩展 Schema；不能临时拼写新渠道名。
