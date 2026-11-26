# Contract — 数据契约

> 层次：Specification | 动词：design | 受众：工程师

---

## 1. 定义

数据契约（Contract）是数据输入/输出结构的正式定义。它描述数据"长什么样"——字段名、数据类型、约束条件和质量承诺。

Contract 是 Specification 的组成部分，与 [Blueprint](blueprint.md) 并列。Contract 定义结构约束，Blueprint 定义处理流程。两者共同构成完整的 Specification。

Contract MUST 区分两种方向：

| 方向 | 责任方 | 回答的问题 |
|------|--------|-----------|
| **输入契约（input）** | 客户 | "客户需要提供什么规格的数据" |
| **输出契约（output）** | 数据工程师 | "我们将交付什么规格的数据" |

input 与 output 的字段名 MAY 重叠；重叠表示同一数据项在处理前后的两种形态。除字段名重叠外，input 与 output 之间不存在强制推导关系。

---

## 2. 类型系统

`type` 字段 MUST 使用以下值之一：

| 类型 | 说明 | 示例值 |
|------|------|--------|
| `string` | 文本 | `"user_001"` |
| `number` | 数值（整数或浮点） | `28`, `30.37` |
| `integer` | 整数。`integer` 是 `number` 的子集；值域为整数的字段 MUST 使用 `integer`，可能为小数的字段 MUST 使用 `number` | `1024` |
| `boolean` | 布尔值 | `true` |
| `date` | 日期，格式 MUST 为 `YYYY-MM-DD` | `2024-01-15` |
| `datetime` | 日期时间，格式 MUST 为 ISO 8601 的 UTC 变体 `YYYY-MM-DDTHH:MM:SSZ`（T 分隔符、Z 时区后缀，无本地时区偏移） | `2024-01-15T14:30:00Z` |
| `enum` | 枚举值。MUST 附带 `values` 子字段列出合法值。`values` MUST 为非空 string 列表且无重复元素 | `["M", "F"]` |

字段值的空语义：字段值 MAY 为 `null`，但 MUST 在 `doc`、`constraint` 或 `guarantee` 中显式声明允许；未声明时，字段值 MUST NOT 为 `null`。字段缺失（键不存在）与字段值为 `null` 是两种不同状态。

---

格式规范（文件格式与位置、字段结构、验证规则、YAML 模板与示例）见 handbook 仓（quanttide-handbook-of-data-engineering）`specification/contract.md`。
