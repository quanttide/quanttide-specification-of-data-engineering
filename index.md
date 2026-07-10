# 首页

## 配置目录

遵循约定优先于配置的原则。用户无需手动设置即可使用，但所有路径均可通过环境变量覆盖。

### 目录结构

```
.quanttide/
└── data/
    ├── pipeline/       # 数据管道（CUE 文件）
    ├── blueprint/      # 数据蓝图（CUE 文件）
    ├── contract/       # 数据契约（CUE / YAML / JSON 文件）
    └── catalog/        # 数据目录（registry.json）
```

各目录的详细定义见：[数据管道](pipeline.md)、[数据蓝图](blueprint.md)、[数据契约](contract.md)、[数据目录](catalog.md)。

### 命名规范

所有目录和配置字段遵循 Unix 风格命名：

- 单数 — 目录名用单数，表示"这一类对象的定义"。好：`pipeline/`，不好：`pipelines/`
- 小写 — 全小写字母。好：`blueprint/`，不好：`BluePrint/`
- 连字符 — 单词间用连字符分隔。好：`contract/`，不好：`contracts/`
- 无缩写 — 除非是通用缩写，否则不缩写。好：`catalog/`，不好：`catlg/`

CUE / YAML 文件的字段名也遵循此规范：

```yaml
# 好
name: csv-standard
steps:
  - command: python3

# 不好
name: csvStandard
steps:
  - command: python3
```

### 路径解析规则

1. 优先读取同名环境变量（如 `PIPELINE_DIR`）
2. 环境变量未设置时使用默认路径
3. 默认路径相对于当前工作目录

### 环境变量

- `PIPELINE_DIR` — 默认 `.quanttide/data/pipeline`，数据管道目录
- `BLUEPRINT_DIR` — 默认 `.quanttide/data/blueprint`，数据蓝图目录
- `CONTRACT_DIR` — 默认 `.quanttide/data/contract`，数据契约目录
- `CATALOG_DIR` — 默认 `.quanttide/data/catalog`，数据目录（registry.json）
