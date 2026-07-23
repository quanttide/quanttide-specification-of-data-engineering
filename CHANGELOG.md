# CHANGELOG

## [0.1.0] - 2026-07-23

### Changed

- **Breaking**: 四层框架重构——需求层(Requirement) → 规格层(Specification) → 实现层(Implementation) → 任务层(Task)
- 新增 `requirement.md`：数据需求文档（DRD）规范定义
- 重定义 `blueprint.md`：从"完整处理方案"改为规格层的"处理蓝图"（工作流步骤），与 Contract 并列
- 重定义 `contract.md`：明确为 Specification 组成部分，增加输入/输出契约区分和 CUE 结构示例
- 重定义 `pipeline.md`：从规格层移至实现层，增加运行时配置和容器化字段
- 更新 `index.md`：新四层框架总览 + 术语表 + 更新目录结构和环境变量
- 更新 `myst.yml`：TOC 增加 requirement.md

### Migration

旧目录结构 → 新目录结构:
- `blueprint/`（旧 Blueprint 定义）→ `specification/`（规格书，含 contract + blueprint）
- `contract/` → `specification/contract/`
- `pipeline/`（旧处理步骤）→ `specification/blueprint/`（处理蓝图）
- 新增 `.quanttide/data/pipeline/` 为实现层数据管道

## [0.0.1] - 2026-07-10

### Added

- 首页：配置目录结构、Unix 风格命名规范、路径解析规则、环境变量说明
- 数据管道定义（pipeline.md）：格式、结构示例、字段说明
- 数据蓝图定义（blueprint.md）：格式、结构示例、字段说明
- 数据契约定义（contract.md）：格式说明
- 数据目录定义（catalog.md）：Volume 结构示例、字段说明
- myst.yml：MyST 项目配置
