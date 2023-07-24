# 量潮数据工程规范

## 构建

假设工作目录是项目根目录。

下载`jupyter-book`工具：

```shell
pip install jupyter-book
```

构建文档：

```shell
jb build .
```

## 发布

### 生成CHANGELOG

下载`git-changelog`工具

```shell
pip install git-changelog
```

生成CHANGELOG到控制台：

```shell
git-changelog
```

再进行整理编辑即可。
