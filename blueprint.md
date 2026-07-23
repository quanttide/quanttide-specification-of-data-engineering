# 处理蓝图

## 什么是处理蓝图

处理蓝图（Blueprint）是数据规格书（Specification）的组成部分，定义数据处理的工作流步骤。它描述"怎么处理"——数据从输入格式转换到输出格式需要经过哪些处理环节。

在四层框架中，Blueprint 位于规格层（Specification），与 Contract 并列。Contract 定义"长什么样"，Blueprint 定义"怎么处理"。

## 格式

CUE

## 文件位置

`.quanttide/data/specification/blueprint/`，可通过 `BLUEPRINT_DIR` 环境变量覆盖。

## 结构

```cue
// .quanttide/data/specification/blueprint/default.cue
package blueprint

csvStandard: #Blueprint & {
    name:        "csv-standard"
    description: "CSV 数据标准化处理：校验→清洗→转换"
    contract:    "csv-standard"
    steps: [
        {
            name:        "数据格式校验"
            command:     "python3 processors/validate.py"
            description: "检查必填字段和格式合规性"
        },
        {
            name:        "数据清洗与转换"
            command:     "python3 processors/transform.py"
            description: "缺失值处理和字段标准化映射"
        },
    ]
}
```

## 字段

- **`name`** (string) — 处理蓝图名称，用于引用
- **`description`** (string) — 业务逻辑概述，用自然语言描述整体处理目标
- **`contract`** (string) — 关联的数据契约名称（定义此蓝图处理的数据结构）
- **`steps`** (list) — 处理步骤的有序列表
  - **`name`** (string) — 步骤名称，面向业务的可读描述
  - **`command`** (string) — 可执行命令或入口
  - **`description`** (string, 可选) — 该步骤的业务逻辑说明和预期产出
