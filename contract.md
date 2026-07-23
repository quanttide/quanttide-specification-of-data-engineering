# 数据契约

## 什么是数据契约

数据契约（Contract）是数据规格书（Specification）的组成部分，定义数据的输入输出结构约束。它描述数据"长什么样"——字段名、类型、约束条件、质量承诺。

在四层框架中，Contract 位于规格层（Specification），与 Blueprint 并列。Contract 定义结构约束，Blueprint 定义处理流程。两者共同构成 Specification。

## 定位

| 维度 | 输入契约 | 输出契约 |
|------|---------|---------|
| **回答的问题** | 客户需要提供什么规格的数据 | 我们将交付什么规格的数据 |
| **责任方** | 客户 | 数据工程师 |
| **约束类型** | 必填、格式、枚举值 | 去重率、空值率、完整性 |

## 格式

CUE / YAML / JSON 均可。

## 文件位置

`.quanttide/data/specification/contract/`，可通过 `CONTRACT_DIR` 环境变量覆盖。

## 结构

```cue
// .quanttide/data/specification/contract/default.cue
package contract

csvStandard: #Contract & {
    name: "csv-standard"
    input: {
        raw_user_id: {
            type:       "string"
            doc:        "用户唯一标识"
            constraint: "required, non-numeric"
        }
        raw_age: {
            type:       "number"
            doc:        "用户年龄"
            constraint: "required, range 0-120"
        }
    }
    output: {
        standard_user_id: {
            type:       "string"
            doc:        "标准化用户ID"
            guarantee:   "去重，非空，长度固定16位"
        }
        age_group: {
            type:       "string"
            doc:        "年龄段"
            guarantee:   "枚举值 [18-25, 26-35, 36-45, 46-55, 56+]"
        }
    }
}
```

## 字段

- **`name`** (string) — 契约名称，用于引用
- **`input`** (map) — 输入字段定义
  - **`type`** (string) — 数据类型
  - **`doc`** (string) — 业务含义
  - **`constraint`** (string, 可选) — 约束条件（必填、格式、枚举值等）
- **`output`** (map) — 输出字段定义
  - **`type`** (string) — 数据类型
  - **`doc`** (string) — 业务含义
  - **`guarantee`** (string, 可选) — 质量承诺（去重率、空值率等）
