---
title: "Hugo 内容提示"
linkTitle: "Hugo 内容提示"
weight: 9
description: >
  为您的 Docsy 主题 Hugo 站点创作内容的技巧。
---

Docsy 是 [Hugo](https://gohugo.io/) 静态站点的主题
发电机。如果你还不熟悉 Hugo，特别是它的 Markdown 版本，这个页面提供了一些
为您的网站添加和编辑内容的有用提示和潜在问题。随意添加你自己的！

## 嵌套列表

Hugo 目前使用的是 [Blackfriday](https://github.com/russross/blackfriday) Markdown 处理器，可以
当涉及到深度嵌套在列表中的内容时很敏感。特别要注意的是
[这个已知问题](https://github.com/russross/blackfriday/issues/329) 如果或当您有多个作者并且
其他可能在缩进列表时混用“制表符”和“空格”或无法正确缩进的贡献者。

这里的另一个因素是，由于 GitHub 使用不同的 Markdown 处理器，GitHub Markdown 和编辑器 UI 可能
正确呈现一些嵌套列表，而 Blackfriday 可能无法很好地呈现相同的内容。例如，在一个计数
编号列表可能会重新启动，或者列表中的嵌套内容未缩进
（显示为对等元素而不是嵌套的子元素）。你可能想在你的贡献指南中推荐
（[正如我们所做的](/docs/contribution-guidelines/#contributing-to-se-docs)），贡献者可以使用 Hugo 预览他们的内容
（或者使用 Netlify 的 PR 预览功能，如果这是您选择的部署工具）以确保其内容正确呈现
与黑色星期五。

{{% alert title="Tip" %}}
[对已知问题的评论](https://github.com/russross/blackfriday/issues/329#issuecomment-277602856)，一些
用户发现使用 4 个空格而不是“制表符”会产生一致的行为。例如，考虑
配置您的本地编辑器以在按下 **Tab** 键时使用 4 个空格。
{{% /alert %}}

## 链接

默认情况下，链接中的常规相对 URL 由 Hugo 保持不变（它们仍然是您网站生成的 HTML 中的相对链接），因此一些硬编码的相对链接，如 `[relative cross-link](../../peer-folder /sub-file.md)` 的行为与它们在本地文件系统上的工作方式相比可能会出乎意料。您可能会发现使用 Hugo 的一些内置 [链接短代码](https://gohugo.io/content-management/cross-references/#use-ref-and-relref) 来避免生成的链接中的断开链接很有帮助地点。例如 Hugo 中的 `{{</* ref "filename.md" */>}}` 链接实际上将
查找并自动链接到名为“filename.md”的文件。

但是请注意，`ref` 和`relref` 链接不适用于`_index` 或`index` 文件（例如，此站点的[内容登陆页面](/docs/adding-content/)）：您需要使用常规的 Markdown 链接到部分着陆页或其他索引页。指定这些相对于站点根 URL 的链接，例如：`/docs/adding-content/`。

[了解有关链接的更多信息](/docs/adding-content/content/#working-with-links)。