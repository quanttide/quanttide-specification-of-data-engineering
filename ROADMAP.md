# ROADMAP

> 格式：Keep a Changelog + checkbox 任务清单。
> ROADMAP 面向未来计划；发布后将已完成条目迁移到 CHANGELOG。
> 当前：spec/v0.0.2（四层框架重构 + RFC 2119 规范升级已发布）；目标 v0.1.0：正式规范发布。

## [0.1.0]

> 核心目标：发布 v0.1.0 正式版——四层框架（Requirement → Specification → Implementation → Task）与 RFC 2119 规范格式落定，各消费者（CLI、Provider、Studio、案例库）对齐新规范。满足发布预检即发 v0.1.0，不按时间排期。

### Added

- [x] 四层框架重构：`requirement.md`（DRD 规范）新增，`blueprint.md`/`contract.md`/`pipeline.md` 重定义（已随 v0.0.2 发布，见 `CHANGELOG.md`）
- [x] 正式规范格式升级：全部组件文档 RFC 2119 关键词（MUST/SHOULD/MAY），CUE 示例替换为 YAML（已随 v0.0.2 发布，见 `CHANGELOG.md`）

### Changed

- [ ] 发布 v0.1.0 正式版：更新 `index.md` 版本号，创建 tag 与 GitHub Release
- [ ] 各消费者对齐 v0.1.0：CLI/Provider/Studio 按新目录结构与 YAML 格式调整（见 `data/context/engineering-standards.md` 版本对应关系）
- [ ] 案例库对齐：`docs/gallery` 案例的 `specification.yaml` 与 `contract.md`/`blueprint.md` 字段定义核对

### Fixed

- [ ] 规范与实现差异核对：`specification.yaml` 实际案例与规范字段定义逐项比对，差异修正到规范或案例
