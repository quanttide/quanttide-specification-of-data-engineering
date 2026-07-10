# 数据蓝图

## 什么是数据蓝图

数据蓝图是完整处理方案的定义，组合一个契约和一个数据管道。契约定义输入输出约束，数据管道定义处理步骤。

## 格式

CUE

## 文件位置

`.quanttide/data/blueprint/`，可通过 `BLUEPRINT_DIR` 环境变量覆盖。

## 结构

```cue
// .quanttide/data/blueprint/default.cue
package blueprint

csvStandardization: #Blueprint & {
    name: "csv-standardization"
    pipeline: "csv-standard"
    contract: "csv-standard"
}
```

## 字段

- **`name`** (string) — 数据蓝图名称
- **`pipeline`** (string) — 引用的数据管道名称
- **`contract`** (string) — 引用的契约名称
