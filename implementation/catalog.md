# Catalog — 数据目录

> 层次：Implementation | 动词：implement | 受众：运行时 | 格式：JSON

---

## 1. 定义

数据目录（Catalog）是运行时文件注册表。它记录已接收、处理中、已交付的文件（Volume），回答"有哪些数据"。

Catalog 是 Implementation 的组成部分，与 Pipeline 并列：
- Pipeline 定义**怎么执行**（运行时配置 + 命令映射）
- Catalog 记录**执行了什么**（运行时文件注册）

Catalog 与声明式定义（DRD / Contract / Blueprint / Pipeline）分离存放：声明式定义描述"应该长什么样"，Catalog 记录"实际发生了什么"。

---

## 2. 格式与位置

### 2.1 格式

Catalog MUST 使用 JSON 格式。Catalog 的受众是运行时和审计方，MUST 可被机器解析和验证。

### 2.2 文件位置

Catalog 文件 MUST 存放在 `.quanttide/data/catalog/registry.json`。可通过 `CATALOG_DIR` 环境变量覆盖。

---

## 3. 结构定义

### 3.1 顶层结构

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| 键 | string | MUST 存在，MUST 唯一 | Volume 名称，即注册表条目键 |
| 值 | object | MUST 存在 | Volume 记录。字段定义见 3.2 节 |

### 3.2 Volume 记录字段

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| `name` | string | MUST 存在，MUST 与顶层键一致 | Volume 名称 |
| `path` | string | MUST 存在，MUST 为绝对路径 | 文件绝对路径 |
| `size` | number | MUST 存在，MUST 非负 | 文件大小（字节） |
| `received_at` | string | MUST 存在 | 注册时间（`YYYY-MM-DD HH:MM:SS`） |
| `status` | enum | MUST 存在 | 状态。合法值：`received` / `processing` / `processed` / `delivered` |
| `provider` | string | MAY 存在 | 来源 provider |
| `source` | string | MAY 存在 | 来源 URL |

---

## 4. 验证规则

符合本规范的 Catalog MUST 满足以下规则：

1. 顶层键 MUST 非空且唯一
2. 每个 Volume 记录的 `name` MUST 与顶层键一致
3. `status` MUST 为 `received`、`processing`、`processed`、`delivered` 之一
4. `path` MUST 为绝对路径

---

## 5. 结构

```json
{
  "<volume-name>": {
    "name": "<volume-name>",
    "path": "<绝对路径>",
    "size": <字节数>,
    "received_at": "<YYYY-MM-DD HH:MM:SS>",
    "status": "received|processing|processed|delivered",
    "provider": "<来源 provider>",
    "source": "<来源 URL>"
  }
}
```

---

## 6. 示例

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
