# blueprint

## 什么是 blueprint

blueprint 是完整处理方案的定义，组合一个 contract 和一个 pipeline。contract 定义输入输出约束，pipeline 定义处理步骤。

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

- **`name`** (string) — blueprint 名称
- **`pipeline`** (string) — 引用的 pipeline 名称
- **`contract`** (string) — 引用的 contract 名称
