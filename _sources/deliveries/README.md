# 数据交付物

本章定义数据集、数据模型、数据记录等对数据建模的数据实体。

## 目的

- 统一表达结构化和半结构化数据，用以打通人工标记和代码处理流程。
- 抽象出业务意义的单元，以方便统一流程的语言、进而方便编排和DataOps。

## 模型

- 基本模型`DataDelivery`

数据集：
- 数据集`DataSet`：类似一个SQL Database。
- 数据模型`DataSchema`：类似一个SQL Schema，由一个或者多个SQL表存储的、表达一类数据的。
- 数据记录`DataRecord`：类似一个SQL Row，由一个或者多个SQL表存储的、。

数据应用：
- 数据应用`DataApplication`
- 数据视图`DataView`
