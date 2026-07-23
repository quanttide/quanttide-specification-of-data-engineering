# 首页

## 四层框架

量潮数据工程标准定义四个层次，从业务到技术逐层递进：

```
需求层 Requirement（面向客户，动词 clarify）
    ↓
规格层 Specification（面向技术，动词 design）
    ├── Contract（数据契约：输入输出规格）
    └── Blueprint（处理蓝图：工作流步骤）
    ↓
实现层 Implementation（动词 implement）
    ├── Catalog（数据目录：运行时文件注册）
    └── Pipeline（数据管道：可执行的处理流程）
    ↓
任务层 Task（动词 execute）
    ├── Feature（产出）
    └── Observation（观测）
```

## 配置目录

遵循约定优先于配置的原则。用户无需手动设置即可使用，但所有路径均可通过环境变量覆盖。

### 目录结构

```
.quanttide/data/
├── requirement/         # 数据需求文档（Markdown）
├── specification/       # 数据规格书
│   ├── contract/        #   数据契约（CUE / YAML / JSON）
│   └── blueprint/       #   处理蓝图（CUE）
├── catalog/             # 数据目录（registry.json）
└── pipeline/            # 数据管道（CUE / 可执行代码）
```

各目录的详细定义见：[数据需求文档](requirement.md)、[数据契约](contract.md)、[处理蓝图](blueprint.md)、[数据目录](catalog.md)、[数据管道](pipeline.md)。

### 命名规范

所有目录和配置字段遵循 Unix 风格命名：

- 单数 — 目录名用单数，表示"这一类对象的定义"。好：`contract/`，不好：`contracts/`
- 小写 — 全小写字母。好：`blueprint/`，不好：`BluePrint/`
- 连字符 — 单词间用连字符分隔。好：`requirement/`，不好：`requirements/`
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

- `REQUIREMENT_DIR` — 默认 `.quanttide/data/requirement`，数据需求文档目录
- `SPECIFICATION_DIR` — 默认 `.quanttide/data/specification`，数据规格书目录
- `CONTRACT_DIR` — 默认 `.quanttide/data/specification/contract`，数据契约目录
- `BLUEPRINT_DIR` — 默认 `.quanttide/data/specification/blueprint`，处理蓝图目录
- `CATALOG_DIR` — 默认 `.quanttide/data/catalog`，数据目录（registry.json）
- `PIPELINE_DIR` — 默认 `.quanttide/data/pipeline`，数据管道目录

## 术语表

| 术语 | 英文 | 层次 | 定义 |
|------|------|------|------|
| 数据需求文档 | DRD (Data Requirements Document) | 需求层 | 面向客户的业务需求描述，回答"要交付什么" |
| 数据规格书 | Specification | 规格层 | Contract + Blueprint 的统称，面向技术的设计文档 |
| 数据契约 | Contract | 规格层 | 数据的输入输出结构约束，描述数据"长什么样" |
| 处理蓝图 | Blueprint | 规格层 | 数据处理的工作流步骤定义，描述"怎么处理" |
| 数据目录 | Catalog | 实现层 | 运行时文件注册表，记录已接收/处理中/已交付的文件 |
| 数据管道 | Pipeline | 实现层 | 可执行的数据处理流程，将 Blueprint 步骤映射为具体命令 |
