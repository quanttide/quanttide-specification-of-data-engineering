# pipeline

## 什么是 pipeline

pipeline 是一组处理步骤的有序列表，定义数据从原始形态到最终产物的转换路径。

## 格式

CUE

## 文件位置

`.quanttide/data/pipeline/`，可通过 `PIPELINE_DIR` 环境变量覆盖。

## 结构

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

## 字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `name` | string | pipeline 名称，用于引用 |
| `steps` | list | 处理步骤列表，每步指定可执行命令 |
