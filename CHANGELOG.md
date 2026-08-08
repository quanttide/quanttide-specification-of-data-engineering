# CHANGELOG

## [0.0.4] - 2026-08-08

### Added

- `index.md`：新增"项目与根目录"（1.4 节）——项目边界、根目录解析顺序
- `index.md`：新增"名称与引用解析"（1.5 节）——组件 name 唯一性范围、引用解析顺序、违规判定
- `catalog.md`：新增 Volume 状态机（3.3 节）——合法转移表与终态规则
- `blueprint.md`：Step 新增 `from` / `to` / `depends` 字段，定义步骤执行语义（3.3 节）
- `pipeline.md`：新增 cron 字段定义（3.4 节）、engine 合法值枚举、image 格式规范

### Changed

- `contract.md`：类型系统闭合——`integer` 为 `number` 子集及使用规则、`datetime` 精确格式（ISO 8601 UTC 变体）、null 空语义声明、enum 元素类型约束、input/output 字段重叠规则
- `requirement.md`：三问题与六章节映射显式化；约束改为可判定表述；"MAY 存在/MAY 省略"去重
- `catalog.md`：`received_at` 时间格式与 Contract `datetime` 对齐（`YYYY-MM-DDTHH:MM:SSZ`）
- `index.md`：RFC 2119 关键词表补充 REQUIRED/SHALL NOT/RECOMMENDED/OPTIONAL；0.x 阶段版本规则声明

### Fixed

- `blueprint.md`：删除"步骤顺序 MUST 保持文件顺序"的不可判定规则，改为有实际约束的 depends 规则
- `pipeline.md`："合法的执行引擎标识符"改为显式枚举；"一一对应"改为可判定（数量相同且 name 一致）
- `requirement.md`：示例补"输入要求"章节，与模板对齐

## [0.0.3] - 2026-08-08

### Changed

- 文档目录按四层框架重组：`requirement/`、`specification/`、`implementation/`，更新 `myst.yml` TOC 与 `index.md` 组件索引
- 术语统一："处理蓝图"改为"数据蓝图"（`index.md` 术语表、`blueprint.md`、`CHANGELOG.md`）

### Added

- `index.md`：新增文档地图（4.1 节，规范仓库目录 vs 运行时目录对应关系）
- `index.md`：术语表补充 Task/Feature/Observation/Volume
- `index.md`：明确"动词"概念（1.2 节）与组件名称中英文使用约定（1.3 节）
- `catalog.md`：补全为统一组件模板（头部标注、字段表、验证规则、结构/示例）

### Fixed

- `AGENTS.md`：命名规范去重，改为引用 `index.md`；补充文档组织说明
- 数字章节引用改为锚点链接；组件文档间交叉引用互链
- 结构骨架精简，注释去除冗余，字段约束以第 3 节字段表为准

## [0.0.2] - 2026-08-08

### Changed

- **Breaking**: 四层框架重构——需求层(Requirement) → 规格层(Specification) → 实现层(Implementation) → 任务层(Task)
- 新增 `requirement.md`：数据需求文档（DRD）规范定义
- 重定义 `blueprint.md`：从"完整处理方案"改为规格层的"数据蓝图"（工作流步骤），与 Contract 并列
- 重定义 `contract.md`：明确为 Specification 组成部分，增加输入/输出契约区分
- 重定义 `pipeline.md`：从规格层移至实现层，增加运行时配置和容器化字段
- 更新 `index.md`：四层框架总览 + 术语表 + 新目录结构
- 全部组件文档升级为正式规范格式（RFC 2119 关键词：MUST/SHOULD/MAY）
- `index.md`：新增引言、文档约定、版本兼容性章节。CUE 示例替换为 YAML
- `requirement.md`：增加正式字段定义表、验证规则、标准模板和完整示例
- `contract.md`：增加正式类型系统（7种类型 + enum 约束）、字段级约束/承诺定义、验证规则和完整 YAML 示例。CUE 替换为 YAML
- `blueprint.md`：增加正式字段定义表、step 级 description/expectation 规范、验证规则和完整 YAML 示例。CUE 替换为 YAML
- `pipeline.md`：增加 runtime 子结构定义、step 级 image/env 扩展、调度方式枚举、验证规则和完整 YAML 示例。CUE 替换为 YAML

### Migration

旧目录结构 → 新目录结构:
- `blueprint/`（旧 Blueprint 定义）→ `specification/`（规格书，含 contract + blueprint）
- `contract/` → `specification/contract/`
- `pipeline/`（旧处理步骤）→ `specification/blueprint/`（数据蓝图）
- 新增 `.quanttide/data/pipeline/` 为实现层数据管道

### Removed

- CUE 格式已弃用，统一使用 YAML

## [0.0.1] - 2026-07-10

### Added

- 首页：配置目录结构、Unix 风格命名规范、路径解析规则、环境变量说明
- 数据管道定义（pipeline.md）：格式、结构示例、字段说明
- 数据蓝图定义（blueprint.md）：格式、结构示例、字段说明
- 数据契约定义（contract.md）：格式说明
- 数据目录定义（catalog.md）：Volume 结构示例、字段说明
- myst.yml：MyST 项目配置
