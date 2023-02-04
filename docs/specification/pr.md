# Pull Request 信息格式规范[^1]

对于 Pull Request，请遵守以下几点要求：

1. 标题请写明本次 PR 的目的（做了 **什么** 工作，修复了 **什么** 问题）。
2. 内容请简要叙述修改的内容。如果修复了一个 issue 的问题，请在内容中添加 `fix #xxxx` 字段，其中 `xxxx` 代表 issue 的编号。
3. 推荐删除 pull request message 中的模板信息（“首先，十分感谢……”这一段）。

对于 Pull Request 的标题，推荐使用如下格式书写：

```plain
<修改类型>(<文件名>): <修改的内容> (<对应 issue 的编号>)
```

修改类型分为如下几类：

- `feat`：用于添加内容的情况。
- `fix`：用于修正现有内容错误的情况。
- `refactor`：用于对一个页面进行重构（较大规模的更改）的情况。
- `revert`：用于回退之前更改的情况。

示例：

- `fix(sepecification/specification): 修改代码注释使描述更清晰`
- `fix: plugins/xxx 不在目录中 (#2)`
- `feat(software/mathpix): official website`
- `refactor(specification/template): 整理页面内容`

[^1]: 修改自 [OI-wiki: 如何参与](https://oi-wiki.org/intro/htc/#pull-request-%E4%BF%A1%E6%81%AF%E6%A0%BC%E5%BC%8F%E8%A7%84%E8%8C%83)
