---
title: "打印支持"
linkTitle: "打印支持"
weight:  7
description: >
     使打印整个文档部分变得更容易。
---

大多数浏览器都可以很好地打印单个文档页面，因为布局已被设计为从打印输出中省略导航镶边。

在某些站点上，启用“打印整个部分”功能会很有用（如本用户指南中所示）。 选择此选项会以适合打印的格式呈现整个当前顶级部分（例如此页面的内容和自定义）及其所有子页面和部分，并带有该部分的目录。

要启用此功能，请在站点的“config.toml”文件中为“section”类型添加“print”输出格式：

```toml
[outputs]
section = [ "HTML", "RSS", "print" ]
```

然后，该站点应在右侧导航中显示“打印整个部分”链接。

## 进一步定制

### 禁用 ToC

要禁用在可打印视图中显示目录，请将 `disable_toc` 参数设置为 `true`，无论是在页面前端还是在 `config.toml` 中：

```toml
[params.print]
disable_toc = true
```


## 布局钩子

定义了许多布局部分和挂钩，可用于自定义打印格式。 这些可以在“布局/部分/打印”中找到。

钩子可以在每个类型的基础上定义。 例如，您可能想要自定义“博客”页面与“文档”页面的标题布局。 这可以通过创建 `layouts/partials/print/page-heading-<type>.html` 来实现 - 例如。 `page-heading-blog.html`。 它默认使用页面标题和描述作为标题。

同样，每个页面的格式都可以通过创建`layouts/partials/print/content-<type>.html` 来定制。




