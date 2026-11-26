# Agent Instructions

## 命名规范

所有配置目录和字段遵循 **Unix 风格命名**（单数、小写、连字符、无缩写），此规则适用于本仓库中所有目录名、文件名和配置字段。规则定义见 handbook 仓（quanttide-handbook-of-data-engineering）`index.md` §1.2。

## 规范边界

**本规范定义"是什么"：概念、关系、状态、类型。格式定义（"长什么样"）在 handbook 仓。**

- 本仓保留：四层框架与动词链、术语表、组件定义与相互关系、Contract 类型系统、Volume 状态机、名称与引用解析
- 文件目录、命名规范、路径解析、环境变量、字段结构、验证规则、模板与示例在 handbook 仓
- CLI 命令、API 路由、SDK 调用方式是某一实现的用户文档，两仓均不收录——规范是给所有消费者看的（CLI、Provider、Studio、第三方工具），绑定了特定实现的接口会限制规范的复用性

## 文档组织

本仓库按四层框架组织规范文档：

- `requirement/` — DRD 数据需求文档定义
- `specification/` — Contract 数据契约、Blueprint 数据蓝图定义
- `implementation/` — Catalog 数据目录、Pipeline 数据管道定义

组件规范索引见 [index.md](index.md#4-组件规范索引)；文档地图（规范仓库 vs 运行时目录）见 handbook 仓 `index.md` 第 2 节。新增组件规范文档时，按所属层次放入对应目录，并同步更新 `index.md` 的组件规范索引、`myst.yml` 的 TOC。
