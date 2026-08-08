# Agent Instructions

## 命名规范

所有配置目录和字段遵循 **Unix 风格命名**（单数、小写、连字符、无缩写），详见 [index.md](index.md#22-命名规范)。此规则适用于本仓库中所有目录名、文件名和配置字段。

## 规范边界

**规范定义"有什么"和"长什么样"，不定义"怎么用"。**

- 规范只描述目录结构、文件格式、命名规则
- CLI 命令、API 路由、SDK 调用方式是某一实现的用户文档，不应出现在规范中
- 规范是给所有消费者看的（CLI、Provider、Studio、第三方工具），绑定了特定实现的接口会限制规范的复用性

## 文档组织

本仓库按四层框架组织规范文档，目录与文档对应关系见 [index.md](index.md#41-文档地图规范仓库-vs-运行时目录) 4.1 节：

- `requirement/` — DRD 数据需求文档规范
- `specification/` — Contract 数据契约、Blueprint 数据蓝图规范
- `implementation/` — Catalog 数据目录、Pipeline 数据管道规范

新增组件规范文档时，按所属层次放入对应目录，并同步更新 `index.md` 的组件规范索引、`myst.yml` 的 TOC。
