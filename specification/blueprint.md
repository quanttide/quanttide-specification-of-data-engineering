# Blueprint — 数据蓝图

> 层次：Specification | 动词：design | 受众：工程师

---

## 1. 定义

数据蓝图（Blueprint）是数据处理工作流的有序步骤定义。它描述"怎么处理"——数据从输入格式转换到输出格式需要经过哪些处理环节。

Blueprint 是 Specification 的组成部分，与 [Contract](contract.md) 并列。一个 Blueprint MUST 关联一个 Contract：
- Contract 定义此蓝图处理的**数据结构**
- Blueprint 定义此数据的**转换步骤**

---

## 2. 步骤执行语义

- steps 按列表顺序串行执行；存在 `depends` 时，被依赖步骤 MUST 在依赖步骤之前执行（若与列表顺序冲突，以 `depends` 为准）
- `from` / `to` 描述步骤间的数据流；步骤的输出（`to`）可以作为后续步骤的输入（`from`）

---

格式规范（文件格式与位置、字段结构、验证规则、YAML 模板与示例）见 handbook 仓（quanttide-handbook-of-data-engineering）`specification/blueprint.md`。
