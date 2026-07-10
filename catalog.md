# catalog

## 什么是 catalog

catalog 记录已接收、处理中、已交付的文件（Volume）。它是运行时元数据，与声明式定义（pipeline / blueprint / contract）分离存放。

## 文件位置

`.quanttide/data/catalog/registry.json`，可通过 `CATALOG_DIR` 环境变量覆盖。

## Volume 结构

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

## 字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `name` | string | volume 名称 |
| `path` | string | 文件绝对路径 |
| `size` | number | 文件大小（字节） |
| `received_at` | string | 注册时间 |
| `status` | string | 状态：received / processing / processed / delivered |
| `provider` | string (可选) | 来源 provider |
| `source` | string (可选) | 来源 URL |
