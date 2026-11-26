# Catalog — 数据目录

> 层次：Implementation | 动词：implement | 受众：运行时

---

## 1. 定义

数据目录（Catalog）是运行时文件注册表。它记录已接收、处理中、已交付的文件（Volume），回答"有哪些数据"。

Catalog 是 Implementation 的组成部分，与 Pipeline 并列：
- Pipeline 定义**怎么执行**（运行时配置 + 命令映射）
- Catalog 记录**执行了什么**（运行时文件注册）

Catalog 与声明式定义（DRD / Contract / Blueprint / Pipeline）分离存放：声明式定义描述"应该长什么样"，Catalog 记录"实际发生了什么"。

---

## 2. Volume 状态机

Volume 记录 `status` 的合法转移如下（仅允许以下转移）：

| 当前状态 | 可转移至 | 说明 |
|---------|---------|------|
| `received` | `processing` | 开始处理 |
| `processing` | `processed` | 处理完成 |
| `processing` | `received` | 处理失败回退（如采集/清洗失败） |
| `processed` | `delivered` | 交付完成 |
| `delivered` | — | 终态，MUST NOT 再转移 |

未列出的转移（如 `received` → `delivered`、`processed` → `received`）MUST NOT 发生。

状态变更记录不在 Catalog 中持久化（Catalog 只保存当前状态）；转移合法性由写入方（Pipeline 实现）负责校验。

---

格式规范（文件格式与位置、字段结构、验证规则、JSON 模板与示例）见 handbook 仓（quanttide-handbook-of-data-engineering）`implementation/catalog.md`。
