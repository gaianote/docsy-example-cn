
---
title: "Welcome to Docsy"
linkTitle: "Documentation"
menu:
  main:
    weight: 20
    pre: <i class='fas fa-book'></i>
type: docs

---

欢迎使用 Docsy 主题用户指南！本指南向您展示如何开始使用 Docsy 创建技术文档站点，包括站点自定义以及如何使用 Docsy 的块和模板。

## Docsy 是什么？

Docsy 是 [Hugo](https://gohugo.io/) 静态站点生成器的主题，专为技术
文档集并内置了许多最佳实践。使用 Docsy 获得有效且可靠的文档
网站快速启动并运行，然后重新专注于为您的用户提供优质内容。
[了解有关 Docsy 的更多信息](/about)。

除了主题本身之外，我们还提供了一个 [示例站点](https://github.com/google/docsy-example)，它使用了许多 Docsy 功能并具有有用的骨架站点结构（以及关于放置内容的建议）它！）用于大型技术文档集。您可以复制整个站点并为您自己的项目编辑它，或者只是浏览站点及其源以查看 Docsy 可以做什么。您当前正在阅读的站点也使用 Docsy，它是一个较小的 Docsy 文档集的有用示例：如果它比“大”示例更适合您的需求，请随意复制或借用它。

Docsy 本身不**不**提供：

* **源代码托管和管理**：我们的主题和站点源文件位于 [GitHub](https://github.com/) 上，这是大多数项目最简单的方法。但是，您也可以将项目文件保存在 [GitLab](https://about.gitlab.com/)、[BitBucket](https://bitbucket.org/product)、本地或任何您喜欢的地方。请注意，源文件所在的位置可能会影响您可以使用的 Docsy 功能（例如让用户提交文档问题）和站点部署选项。
* **站点部署**：您可以在[预览和部署](./deployment/)中找到有关部署选项的信息。本网站使用[Netlify](https://www.netlify.com/)。

Docsy 实际上也不会生成您网站的 HTML 文件：那是 Hugo 的工作！ Hugo 将您的 Markdown 或 HTML 文档源文件和 Docsy 的主题文件构建到一个静态站点中以进行部署。您可以在 [Hugo 文档](https://gohugo.io/documentation/) 中找到有关 Hugo 及其工作原理的更多信息。

## Docsy 适合我吗？

Docsy 对于包含 20 多页文档和/或多种类型的文档和页面的大中型技术文档集特别有用：教程、参考文档、博客文章、社区页面等。

如果您有一个只有几页文档的较小项目，因此需要更简单的导航需求，Docsy 对您来说可能是一个重量级的解决方案。相反，请考虑：

* 更简单的 Hugo 或 Jekyll 主题：找出 Github Pages 的 [内置 Jekyll 选项](https://pages.github.com/themes/) 和 [Hugo 主题库](https://themes) 中可用的内容.gohugo.io/）。
* 一个很好的 README 文件，它告诉用户你的项目做了什么并链接到一些例子。

如果您有一个非常大的文档项目，我们的示例站点结构也可能不够用，但您仍然可以使用我们的主题，可能需要更多的自定义。

如果你想使用 Docsy 的布局但更喜欢使用 Jekyll，[vsoch](https://github.com/vsoch) 已经创建了一个 [Docsy Jekyll 端口](https://github.com/vsoch/docsy- jekyll），其中包括 Docsy 的许多功能（尽管这是一个单独的项目，它不会与 Docsy 一起自动更新）。

## 准备好开始了吗？

在 [Getting Started](./getting-started/) 中了解如何构建和服务您的第一个站点。或者访问 [示例站点](https://example.docsy.dev) 和 [它的 repo](https://github.com/google/docsy-example) 并开始探索！