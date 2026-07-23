# 数据管道

## 什么是数据管道

数据管道（Pipeline）是实现层的可执行数据处理流程。它将处理蓝图（Blueprint）中定义的步骤映射为具体的执行命令、调度配置和运行时参数。

在四层框架中，Pipeline 位于实现层（Implementation），与 Catalog 并列。Blueprint 定义"做什么"，Pipeline 定义"怎么执行"。

## 格式

CUE，可执行部分可以为 Python / Shell / 容器镜像等。

## 文件位置

`.quanttide/data/pipeline/`，可通过 `PIPELINE_DIR` 环境变量覆盖。

## 结构

```cue
// .quanttide/data/pipeline/default.cue
package pipeline

csvStandard: #Pipeline & {
    name:     "csv-standard"
    blueprint: "csv-standard"
    runtime: {
        engine:  "python3"
        version: "3.11"
    }
    schedule: "manual"
    steps: [
        {
            name:    "validate"
            command: "python3 -m processors.validate --input ${INPUT_FILE}"
            image:   "registry.quanttide.com/data/validator:v1.2.0"
        },
        {
            name:    "transform"
            command: "python3 -m processors.transform --input ${INPUT_FILE} --output ${OUTPUT_FILE}"
            image:   "registry.quanttide.com/data/transformer:v1.2.0"
        },
    ]
}
```

## 字段

- **`name`** (string) — 数据管道名称，用于引用
- **`blueprint`** (string) — 关联的处理蓝图名称
- **`runtime`** (object) — 运行时配置
  - **`engine`** (string) — 执行引擎（python3, node, binary 等）
  - **`version`** (string) — 运行时版本
- **`schedule`** (string) — 调度方式（manual / cron / event-driven）
- **`steps`** (list) — 执行步骤列表
  - **`name`** (string) — 步骤名称，对应 Blueprint 中的步骤
  - **`command`** (string) — 可执行命令
  - **`image`** (string, 可选) — 容器镜像（容器化部署时使用）
