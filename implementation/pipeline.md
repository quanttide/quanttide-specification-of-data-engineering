# Pipeline — 数据管道

> 层次：Implementation | 动词：implement | 受众：运行时

---

## 1. 定义

数据管道（Pipeline）是实现层的可执行数据处理流程定义。它将 Blueprint 中定义的步骤映射为具体的运行时命令、环境配置和调度规则。

Pipeline 是 Implementation 的组成部分，与 [Catalog](catalog.md) 并列：
- Pipeline 定义**怎么执行**（运行时配置 + 命令映射）
- Catalog 记录**执行了什么**（运行时文件注册）

一个 Pipeline MUST 关联一个 [Blueprint](../specification/blueprint.md)。Pipeline 是 Blueprint 的运行时实现。

---

格式规范（文件格式与位置、字段结构、验证规则、YAML 模板与示例）见 handbook 仓（quanttide-handbook-of-data-engineering）`implementation/pipeline.md`。
