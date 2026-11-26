# 量潮数据工程标准（QuantTide Data Engineering Specification）

> 版本：v0.0.2 | 日期：2026-08-08
> 本文档定义量潮数据工程的四层框架及其组件规范。

---

## 1. 引言

本文档是量潮数据工程标准的正式规范。它定义了数据工程项目的四个抽象层次以及每层的概念、组件定义与交互规则。

本文档中的关键词 "MUST"、"MUST NOT"、"SHOULD"、"SHOULD NOT"、"MAY" 遵循 [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) 的解释。

### 1.1 四层框架

量潮数据工程标准将数据项目分解为四个层次，从业务需求到技术执行逐层递进：

```
Requirement（需求层）
    │ 动词: clarify  输入: 客户上下文  输出: DRD
    │ 受众: 客户、业务方  语言: 自然语言
    ↓
Specification（规格层）
    │ 动词: design  输入: DRD  输出: Contract + Blueprint
    │ 受众: 工程师  语言: YAML（结构化）
    │
    ├── Contract  回答: 数据长什么样（输入/输出结构）
    └── Blueprint  回答: 数据怎么处理（工作流步骤）
    ↓
Implementation（实现层）
    │ 动词: implement  输入: Specification  输出: Catalog + Pipeline
    │ 受众: 运行时
    │
    ├── Catalog  回答: 有哪些数据（运行时文件注册）
    └── Pipeline  回答: 怎么执行（可执行处理流程）
    ↓
Task（任务层）
    │ 动词: execute  输入: Pipeline + Catalog
    │
    ├── Feature（产出）
    └── Observation（观测）
```

### 1.2 完整流程链

```
Context → clarify → Requirements (DRD)
    → design → Specification (Contract + Blueprint)
    → implement → Catalog + Pipeline
    → execute → Task
    → report → transfer → Delivery
```

**动词**是各层对外提供的人工/工具动作，也是 CLI 等实现暴露的命令入口：`clarify`（需求澄清）、`design`（规格设计）、`implement`（实现落地）、`execute`（任务执行）。`report`（报告）与 `transfer`（交付传输）衔接 Task 层到最终交付，属于流程链的收尾动作。

### 1.3 文档约定

本规范使用 RFC 2119 关键词的大写形式，语义遵循 [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt)：

| 约定 | 含义 |
|------|------|
| `MUST` / `REQUIRED` | 符合规范的实现必须满足的要求 |
| `MUST NOT` / `SHALL NOT` | 符合规范的实现绝对不能做的事 |
| `SHOULD` / `RECOMMENDED` | 推荐满足的要求，在特定上下文中可以忽略，但忽略前 SHOULD 理解其影响 |
| `SHOULD NOT` | 不推荐的做法，但允许有理由的例外 |
| `MAY` / `OPTIONAL` | 可选的能力，实现者自行决定 |

组件名称使用约定：正文首次出现时使用中文全称（可附英文，如"数据契约（Contract）"），后续可使用英文短名（如 Contract）。本仓库文件名与规范关键词使用英文（Contract / Blueprint / Catalog / Pipeline / DRD）。

### 1.4 项目与根目录

本规范中的**项目**（Project）指一个独立的数据工程交付单元。项目边界由项目根目录定义：

- 项目根目录 MUST 包含 `.quanttide/` 目录
- 运行时目录树 MUST 位于项目根目录的 `.quanttide/data/` 下
- 项目根目录解析顺序见 handbook 仓（quanttide-handbook-of-data-engineering）`index.md` §1.3

所有"项目内唯一"、"引用已存在的组件"等约束，均以项目根目录为边界解析。

### 1.5 名称与引用解析

- 同类组件（Contract / Blueprint / Pipeline）的 `name` MUST 在项目内唯一
- 引用字段（`blueprint.contract`、`pipeline.blueprint`）按以下顺序解析：
  1. 目标组件文件中的 `name` 字段
  2. 目标组件文件名（不含扩展名）
- 解析范围：项目内对应组件的全部文件（如 Contract 引用扫描 `.quanttide/data/specification/contract/` 下所有文件）
- 引用无法解析 MUST 视为规范违规

---

## 2. 配置目录

目录结构、命名规范、路径解析与环境变量属格式规范，已分解至 handbook 仓（quanttide-handbook-of-data-engineering）`index.md` 第 1 节。

---

## 3. 术语表

| 术语 | 英文 | 层次 | 定义 |
|------|------|------|------|
| 数据需求文档 | DRD (Data Requirements Document) | Requirement | 面向客户的业务需求描述。使用自然语言，回答"要交付什么"。通过 `clarify` 动作从客户上下文生成。 |
| 数据规格书 | Specification | Specification | Contract 和 Blueprint 的统称。面向技术的设计文档集合。通过 `design` 动作从 DRD 生成。 |
| 数据契约 | Contract | Specification | 数据输入/输出结构的正式定义。描述每个字段的类型、约束和业务含义。 |
| 数据蓝图 | Blueprint | Specification | 数据处理工作流的有序步骤定义。描述从输入到输出的转换路径。 |
| 数据目录 | Catalog | Implementation | 运行时文件注册表。记录 Volume 的接收状态、处理进度和交付信息。 |
| 数据管道 | Pipeline | Implementation | 可执行的数据处理流程定义。将 Blueprint 步骤映射为具体运行时配置和命令。 |
| 任务 | Task | Task | 一次具体执行的实例。通过 `execute` 动作从 Pipeline + Catalog 生成。 |
| 特征 | Feature | Task | 任务产出物（如生成的数据文件、报告）。 |
| 观测 | Observation | Task | 任务执行过程中的观测记录（日志、指标）。 |
| 数据卷 | Volume | Implementation | Catalog 中注册的一个数据文件。含路径、大小、接收时间、处理状态。 |

---

## 4. 组件规范索引

| 组件 | 规范文档 | 层次 |
|------|---------|------|
| DRD | [requirement/index.md](requirement/index.md) | Requirement |
| Contract | [specification/contract.md](specification/contract.md) | Specification |
| Blueprint | [specification/blueprint.md](specification/blueprint.md) | Specification |
| Catalog | [implementation/catalog.md](implementation/catalog.md) | Implementation |
| Pipeline | [implementation/pipeline.md](implementation/pipeline.md) | Implementation |

> Task 层（Feature / Observation）规范待定义，见 [ROADMAP.md](ROADMAP.md)。
> 文档地图（规范仓库 vs 运行时目录）见 handbook 仓 `index.md` 第 2 节。

---

## 5. 版本兼容性

### 5.1 语义化版本

本规范使用 [Semantic Versioning 2.0.0](https://semver.org/lang/zh-CN/)：

- **MAJOR**（主版本号）：不兼容的规范变更（如移除层次、重命名核心概念）
- **MINOR**（次版本号）：向后兼容的新增（如新增可选字段、新增组件）
- **PATCH**（修订号）：向后兼容的修正。仅限不改变语义的修改（如措辞澄清、示例修正）；若措辞修改改变了约束语义，按 MINOR 或 MAJOR 处理

本规范当前处于 **0.x 阶段**：MINOR 版本（如 0.1.0）可以包含不兼容变更，但 MUST 在 CHANGELOG 中提供迁移说明。进入 1.x 后按上述 MAJOR/MINOR/PATCH 规则执行。

### 5.2 迁移策略

v0.0.x → v0.1.x 的迁移指南见 [CHANGELOG.md](CHANGELOG.md)。
