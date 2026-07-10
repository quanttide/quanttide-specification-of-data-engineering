# 首页

## 配置目录

遵循约定优先于配置的原则。用户无需手动设置即可使用，但所有路径均可通过环境变量覆盖。

### 目录结构

```
.quanttide/
└── data/
    ├── pipeline/       # 管道定义（CUE 文件）
    ├── blueprint/      # 蓝图定义（CUE 文件）
    ├── contract/       # 契约定义（CUE / YAML / JSON 文件）
    └── catalog/        # 数据目录（registry.json）
```

### 命名规范

所有目录和配置字段遵循 **Unix 风格命名**：

- **单数** — 目录名用单数，表示"这一类对象的定义"。好：`pipeline/`，不好：`pipelines/`
- **小写** — 全小写字母。好：`blueprint/`，不好：`BluePrint/`
- **连字符** — 单词间用连字符分隔。好：`contract/`，不好：`contracts/`
- **无缩写** — 除非是通用缩写，否则不缩写。好：`catalog/`，不好：`catlg/`

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

- **`PIPELINE_DIR`** — 默认 `.quanttide/data/pipeline`，管道定义目录
- **`BLUEPRINT_DIR`** — 默认 `.quanttide/data/blueprint`，蓝图定义目录
- **`CONTRACT_DIR`** — 默认 `.quanttide/data/contract`，契约定义目录
- **`CATALOG_DIR`** — 默认 `.quanttide/data/catalog`，数据目录（registry.json）

## 各目录详述

### pipeline/

存放管道定义文件，格式为 CUE。

文件结构示例：

```cue
// .quanttide/data/pipeline/default.cue
package pipeline

csvStandard: #Pipeline & {
    name: "csv-standard"
    steps: [
        {command: "python3 processors/validate.py"},
        {command: "python3 processors/transform.py"},
    ]
}
```

### blueprint/

存放蓝图定义文件，格式为 CUE。蓝图组合 contract 和 pipeline 形成完整处理方案。

```cue
// .quanttide/data/blueprint/default.cue
package blueprint

csvStandardization: #Blueprint & {
    name: "csv-standardization"
    pipeline: "csv-standard"
    contract: "csv-standard"
}
```

### contract/

存放契约定义文件，支持 CUE / YAML / JSON 格式。契约定义数据的输入输出结构约束，不关心物理存储位置。

### catalog/

数据目录，记录已接收/处理/交付的文件（Volume），存储为 `registry.json`。

```json
{
  "cust-001-raw": {
    "name": "cust-001-raw",
    "path": "/tmp/qtcloud-data/cust-001/raw.csv",
    "size": 2340000,
    "received_at": "2026-07-10 12:00:00",
    "status": "received",
    "provider": "dropbox",
    "source": "https://www.dropbox.com/s/xxx/file.csv"
  }
}
```
