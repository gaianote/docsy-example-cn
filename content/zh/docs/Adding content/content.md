---
title: "添加内容"
linkTitle: "添加内容"
weight: 1
description: >
  向您的 Docsy 站点添加不同类型的内容。
---

所以你已经有了一个带有 Docsy 的新 Hugo 网站，现在是时候添加一些内容了！此页面告诉您如何使用主题来添加和构建站点内容。

## 内容根目录

您在 Hugo 站点项目的 **content root directory** 下为站点添加内容 - `content/` 或 [language-specific](/docs/language/) 根目录，如 `content/en/`。此处的主要例外是您不希望将静态文件内置到您的站点中：您可以在下面的 [添加静态内容](#adding-static-content) 中找到有关在何处添加这些文件的更多信息。您的内容根目录中的文件通常分组在与您网站的部分和模板相对应的子目录中，我们将在 [内容部分和模板](#content-sections-and-templates) 中查看这些子目录。

你可以在【目录结构说明】(https://gohugo.io/getting-started/directory-structure/#directory-structure-explained)中找到更多关于 Hugo 目录结构的信息。

## 内容部分和模板

Hugo 使用您提供的内容文件以及您网站主题提供的任何模板来构建您的网站页面。这些模板（或 Hugo 术语中的“布局”*）包括页面的页眉、页脚、导航和样式表链接等内容：基本上，除了页面特定内容之外的所有内容。模板又可以由 *partials* 组成：用于页眉、搜索框等页面元素的可重用 HTML 的小片段。

由于大多数技术文档站点针对不同类型的内容具有不同的部分，因此 Docsy 主题随附 [以下模板](https://github.com/google/docsy/tree/master/layouts) 用于顶级站点部分你可能需要：

* [`docs`](https://github.com/google/docsy/tree/master/layouts/docs) 适用于您网站的文档部分中的页面。
* [`blog`](https://github.com/google/docsy/tree/master/layouts/blog) 适用于您网站博客中的页面。
* [`community`](https://github.com/google/docsy/tree/master/layouts/community) 适用于您网站的社区页面。

它还提供了一个[默认的“登陆页面”类型的模板](https://github.com/google/docsy/tree/master/layouts/_default) 带有站点页眉和页脚，但没有左导航，你可以用于任何其他部分。在本站点和我们的示例站点中，它用于站点 [主页](/) 和 [关于](/about/) 页面。

您站点中的每个顶级 **section** 都对应于站点内容根目录中的一个 **directory**。 Hugo 会自动为该部分应用适当的 **template**，具体取决于内容所在的文件夹。例如，此页面位于站点内容根目录 `content/en/` 的 `docs` 子目录中，因此 Hugo自动应用`docs` 模板。您可以通过为特定页面显式指定模板或内容类型来覆盖它。

如果您复制了示例站点，则您已经为使用 Docsy 的模板适当命名了顶级部分目录，每个目录都有一个索引页面（`_index.md` 或 `index.html`）页面供用户登陆。这些顶级部分也出现在示例网站的 [顶级菜单](/docs/adding-content/navigation/#top-level-menu) 中。

### 自定义部分

如果您复制了示例站点并且*不想*使用提供的内容部分之一，只需删除相应的内容子目录。同样，如果您想添加顶级部分，只需添加一个新的子目录，但您需要在每个页面的 [frontmatter](#page-frontmatter) 中明确指定布局或内容类型，如果您想使用除默认模板之外的任何现有 Docsy 模板。例如，如果您创建一个新目录 `content/en/amazing` 并希望该自定义部分中的一个或多个页面使用 Docsy 的 `docs` 模板，则将 `type: docs` 添加到每个页面的前端：

```yaml
---
title: "My amazing new section"
weight: 1
type: docs
description: >
  A special section with a docs layout.
---
```

或者，根据现有模板之一，在项目的 `layouts` 目录中为新部分创建自己的页面模板。

您可以在 [Hugo Templates](https://gohugo.io/templates/) 中找到更多关于 Hugo 页面布局如何工作的信息。本页的其余部分将告诉您如何添加内容以及如何使用 Docsy 的每个模板。

### 替代网站结构

如上所述，默认情况下，您的站点有一个主页（使用`_default` 布局）、`/docs/` 下的文档部分、`/blog/` 下的博客部分和`/community/` 下的社区部分.每个部分的[类型](https://gohugo.io/content-management/types/)（决定其使用的布局）与其目录名称匹配。

在某些情况下，您可能希望使用不同的目录结构，但仍要使用 Docsy 的布局。一个常见的例子是“docs 站点”，其中大多数页面（包括主页）使用 docs 布局，或者您可能希望使用博客布局处理一个 `/news/` 目录。

从 Hugo 0.76 开始，这已经变得实用，无需将布局复制到您的站点，也无需通过使用 [目标特定级联前端问题](https://gohugo.io/content-) 在每个页面上指定“类型：博客”管理/前沿问题/#target-specific-pages）。

例如，对于`/news/`部分，您可以在索引页面中指定以下前端内容，这将更改该部分及其下方所有内容的类型为“博客”：

```yaml
---
title: "Latest News"
linkTitle: "News"
menu:
  main:
    weight: 30

cascade:
- type: "blog"
---
```

如果你想创建一个“docs”站点，在顶级`_index.md`中指定类似以下内容将设置所有顶级部分都被视为“docs”，除了“news”：

```yaml
---
title: "My Wonderful Site"

cascade:
- type: "blog"
  toc_root: true
  _target:
    path: "/news/**"
- type: "docs"
  _target:
    path: "/**"
---
```

注意这里添加了 `toc_root`。 将某个部分设置为 true 会使其被视为站点的一个单独部分，并具有自己的左侧导航菜单。

可以在 [主要文档](https://github.com/gwatts/mostlydocs/) 存储库中找到使用此技术的基于文档的示例站点。

## 页面前端

Hugo 站点中的每个页面文件都有元数据 frontmatter，用于告诉 Hugo 有关该页面的信息。 您可以在 TOML、YAML 或 JSON（我们的示例站点和此站点使用 YAML）中指定页面 frontmatter。 使用 frontmatter 指定页面标题、描述、创建日期、链接标题、模板、菜单权重，甚至页面使用的任何资源（例如图像）。 您可以在 [Front Matter](https://gohugo.io/content-management/front-matter/) 中查看可能的页面 frontmatter 的完整列表。

例如，这里是这个页面的frontmatter：

```yaml
---
title: "Adding Content"
linkTitle: "Adding Content"
weight: 1
description: >
  Add different types of content to your Docsy site.
---
```

您需要提供的最低要求是标题：其他一切都取决于您！但是，如果您省略了页面权重，您的 [navigation](/docs/adding-content/navigation) 可能会变得有点混乱。您可能还想包含 `description`，因为 Docsy 使用它来生成搜索引擎使用的元 `description` 标签。有关详细信息，请参阅 [搜索引擎优化 (SEO) 元标记]({{< ref "feedback#search-engine-optimization-meta-tags" >}})。


## 页面内容和标记

默认情况下，您在 Docsy 站点中创建页面作为简单的 [Markdown 或 HTML 文件](https://gohugo.io/content-management/formats/) 和 [page frontmatter](#page-frontmatter)，如上所述。 0.60 之前的 Hugo 版本使用 [BlackFriday](https://github.com/russross/blackfriday) 作为其 Markdown 解析器。从 0.60 开始，Hugo 默认使用 [Goldmark](https://github.com/yuin/goldmark/) 作为 Markdown 解析器。

{{% alert title="提示" %}}
如果您一直在使用早期版本的 Hugo，您可能需要对您的站点进行一些小的更改以使用当前的 Markdown 解析器。特别是，如果您克隆了我们示例站点的早期版本，请将以下内容添加到您的 `config.toml` 以允许 Goldmark 呈现原始 HTML 和 Markdown：


```
[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
```

或者，如果您想继续使用 Blackfriday，您可以按照 [Hugo 文档](https://gohugo.io/getting-started/configuration-markup#blackfriday) 中的说明更改 Markdown 解析器。
{{% /alert %}}

除了标记文本之外，您还可以使用 Hugo 和 Docsy 的 [shortcodes](/docs/adding-content/shortcodes)：可重用的 HTML 块，可用于快速构建页面。在 [Docsy Shortcodes](/docs/adding-content/shortcodes) 中了解有关短代码的更多信息。

{{% alert title="Note" color="info" %}}
Hugo 还支持使用 [external parser as helpers](https://gohugo.io/content-management/formats/#additional-formats-through-external-helpers) 使用其他标记添加内容。例如，您可以使用 `rst2html` 作为外部解析器在 RST 中添加内容（但请注意，这并不支持所有类型的 RST，例如 Sphinx RST）。同样，您可以使用 `asciidoctor` 解析 Asciidoc 文件，或使用 `pandoc` 解析其他格式。

外部解析器可能不适用于所有部署选项，因为您需要安装外部解析器并自己运行 Hugo 来生成您的站点（例如，您将无法使用 [Netlify 的持续部署功能](/docs/deployment/#deployment-with-netlify))。此外，添加外部解析器可能会导致构建更大站点的性能问题。
{{% /alert %}}

### 使用链接

Hugo 允许您使用正常的 Markdown 语法指定链接，但请记住，您需要指定相对于站点根 URL 的链接，并且 Hugo 在站点生成的 HTML 中保持相对 URL 不变。

或者，您可以使用 Hugo 的帮助程序 [`ref` 和 `relref` 短代码](https://gohugo.io/content-management/cross-references/) 来创建解析为正确 URL 的内部链接。但是，请注意，这意味着如果用户在您生成的站点之外查看您的页面，您的链接将根本不会显示为链接，例如使用 GitHub 的 Web UI 中呈现的 Markdown 功能。

您可以在 [Hugo Tips](/docs/best-practices/site-guides) 中找到（或添加！）使用 Hugo 链接的技巧和陷阱。

### 内容样式

我们不要求您的页面内容具有任何特定的样式。但是，如果您需要有关如何编写和格式化清晰、简洁的技术文档的指导，我们建议您阅读 [Google 开发者文档样式指南](https://developers.google.com/style/)，尤其是 [样式指南亮点](https://developers.google.com/style/highlights)。

## 页面包

您可以将站点页面创建为其部分或子部分目录中的独立文件，或者创建为内容位于文件夹索引页中的文件夹。为您的页面创建一个文件夹可以让您[捆绑](https://gohugo.io/content-management/page-bundles/) 图像和其他资源以及内容。

您可以在此站点和我们的示例站点中查看这两种方法的示例。例如，此页面的源只是一个独立文件 `/content/en/docs/adding-content.md`。然而，本网站中 [Docsy Shortcodes](/docs/adding-content/shortcodes/) 的源代码位于`/content/en/docs/adding-content/shortcodes/index.md`，其图像资源由页面在同一个 `/shortcodes/` 目录中。在 Hugo 术语中，这被称为 *leaf bundle*，因为它是一个包含单个站点页面的所有数据的文件夹，没有任何子页面（并且使用不带下划线的 `index.md`）。

您可以在 [Page Bundles](https://gohugo.io/content-management/page-bundles/) 中找到更多关于使用 Hugo bundles 管理资源的信息。

## 添加文档和博客文章

您可能最常使用的模板是 [`docs` 模板](https://github.com/google/docsy/blob/master/layouts/docs/baseof.html)（在本页中使用）或非常相似的 [`blog` 模板](https://github.com/google/docsy/blob/master/layouts/blog/baseof.html)。这两个模板都包括：

* 左导航
* GitHub 链接（根据您的站点配置填充）供读者编辑页面或创建问题
* 一个页面菜单

以及所有站点页面使用的通用页眉和页脚。应用哪个模板取决于您是否已将内容添加到 `blog` 或 `docs` 内容目录。您可以在 [导航和搜索](/docs/adding-content/navigation/) 中找到有关如何创建导航和页面菜单的更多信息。

### 组织您的文档

虽然 Docsy 的顶级部分允许您为不同类型的内容创建站点部分，但您可能还希望在您的“文档”部分中组织您的文档内容。例如，本站的`docs`部分目录下有多个子目录，分别是**Getting Started**、**Content and Customization**等。每个子目录都有一个 `_index.md`（它也可以是一个 `_index.html`），它充当一个部分索引页面并告诉 Hugo 相关目录是你的文档的一个子部分。

Docsy 的 `docs` 布局为您提供了一个左侧导航窗格，其中包含一个基于您的 `docs` 文件结构自动生成的嵌套菜单。 `docs/` 目录中的每个独立页面或小节 `_index.md` 或 `_index.html` 页面都会获得一个顶级菜单项，使用来自页面或索引的链接名称和 `weight` 元数据。

要将文档添加到小节，只需将您的页面文件添加到相关子目录。除了小节索引页面之外，您添加到小节的任何页面都将出现在子菜单中（向左看可以看到一个正在运行的页面！），再次按页面“权重”排序。在 [导航和搜索](/docs/adding-content/navigation/) 中了解有关添加 Docsy 导航元数据的更多信息

如果您复制了示例站点，那么您的 `docs` 目录中已经有一些建议的子目录，以及有关将哪些类型的内容放入其中的指南以及一些示例 Markdown 页面。您可以在 [Organizing Your Content](/docs/best-practices/organizing-content/) 中找到有关使用 Docsy 组织内容的更多信息。

#### 文档部分登录页面

默认情况下，文档部分登录页面（部分目录中的“_index.md”或“_index.html”）使用一种布局，该布局将链接的格式化列表添加到该部分中的页面，以及它们的前端描述。本网站中的[内容和自定义](/docs/adding-content/) 登录页面就是一个很好的例子。

要显示指向该部分页面的简单项目符号列表，请在登录页面的 frontmatter 中指定 `simple_list: true`：

```
---
title: "Simple List Page"
simple_list: true
weight: 20
---
```

要完全不显示链接，请在登录页面的 frontmatter 中指定 `no_list: true`：

```
---
title: "No List Page"
no_list: true
weight: 20
---
```

### 组织您的博客文章

Docsy 的`blog` 布局还为您提供了一个左侧导航菜单（如`docs` 布局），以及一个适用于`/blog/_index.md` 的博客列表型索引页面，并自动显示您最近使用的所有片段。 帖子按时间倒序排列。

要创建不同的博客类别来组织您的帖子，请在“blog/”中创建子文件夹。 例如，在我们的 [示例站点](https://github.com/google/docsy-example/tree/master/content/en/blog) 中，我们有 `news` 和 `releases`。 每个类别都需要有自己的 `_index.md` 或 `_index.html` 登录页面文件，指定类别标题，以便在左侧导航和顶级博客登录页面中正确显示。 这是`releases`的索引页面：
```
---
title: "New Releases"
linkTitle: "Releases"
weight: 20
---
```

To add author and date information to blog posts, add them to the page frontmatter:

```
---
date: 2018-10-06
title: "Easy documentation with Docsy"
linkTitle: "Announcing Docsy"
description: "The Docsy Hugo theme lets project maintainers and contributors focus on content, not on reinventing a website infrastructure from scratch"
author: Riona MacNamara
resources:
- src: "**.{png,jpg}"
  title: "Image #:counter"
  params:
    byline: "Photo: Riona MacNamara / CC-BY-CA"
---
```

如果您复制了示例站点，但不需要博客部分，或者想要链接到外部博客，只需删除 `blog` 子目录。


## 使用顶级登录页面。

Docsy 的[默认页面模板](https://github.com/google/docsy/blob/master/layouts/docs/baseof.html) 没有左导航，对于为您的网站创建主页或其他“登陆" 类型页面。

### 自定义示例站点页面

如果您复制了示例站点，则在`content/en/_index.html` 中已经有一个简单的站点登录页面。这是由 Docsy 提供的 Hugo 短代码 [页面块](/docs/adding-content/shortcodes/#shortcode-blocks) 组成的。

要自定义位于 [cover](/docs/adding-content/shortcodes/#blockscover) 块中的大型着陆图像，请将项目中的 `content/en/featured-background.jpg` 文件替换为您自己的图像（只要文件名中包含“背景”，就可以随意称呼它）。您可以根据需要删除或添加任意数量的块，以及添加您自己的自定义内容。

示例站点在 `content/en/about/_index.html` 中还有一个关于页面，使用相同的 Docsy 模板。同样，这是由 [页面块](/docs/adding-content/shortcodes/#shortcode-blocks) 组成，包括在 `content/en/about/featured-background.jpg` 中的另一个背景图像。与站点登录页面一样，您可以替换图像、删除或添加块，或者只添加您自己的内容。

### 构建您自己的登陆页面

如果您刚刚使用该主题，您仍然可以使用 Docsy 提供的所有 [页面块](/docs/adding-content/shortcodes/#shortcode-blocks)（或您想要的任何其他内容）来构建您自己的登录页面相同的文件位置。

## 添加社区页面

`community` 登录页面模板具有自动填充项目名称和在 `config.toml` 中指定的社区链接的样板内容，为您的用户提供资源的快速链接，帮助他们参与您的项目。默认情况下，相同的链接也会添加到您的站点页脚。

```toml
[params.links]
# End user relevant links. These will show up on left side of footer and in the community page if you have one.
[[params.links.user]]
	name = "User mailing list"
	url = "https://example.org/mail"
	icon = "fa fa-envelope"
        desc = "Discussion and help from your fellow users"
[[params.links.user]]
	name ="Twitter"
	url = "https://example.org/twitter"
	icon = "fab fa-twitter"
        desc = "Follow us on Twitter to get the latest news!"
[[params.links.user]]
	name = "Stack Overflow"
	url = "https://example.org/stack"
	icon = "fab fa-stack-overflow"
        desc = "Practical questions and curated answers"
# Developer relevant links. These will show up on right side of footer and in the community page if you have one.
[[params.links.developer]]
	name = "GitHub"
	url = "https://github.com/google/docsy"
	icon = "fab fa-github"
        desc = "Development takes place here!"
[[params.links.developer]]
	name = "Slack"
	url = "https://example.org/slack"
	icon = "fab fa-slack"
        desc = "Chat with other project developers"
[[params.links.developer]]
	name = "Developer mailing list"
	url = "https://example.org/mail"
	icon = "fa fa-envelope"
        desc = "Discuss development issues around the project"
``` 

如果您正在创建自己的站点并希望使用此模板添加页面，请在您的内容根目录中添加一个 `/community/_index.md` 文件。如果您复制了示例站点并且*不*想要社区页面，只需删除项目存储库中的`/content/en/community/` 目录。

## 添加静态内容

您可能希望与您的站点一起提供一些非 Hugo 构建的内容：例如，如果您使用 Doxygen、Javadoc 或其他文档生成工具生成了参考文档。

要添加要“按原样”提供的静态内容，只需将内容作为文件夹和/或文件添加到站点的 `static` 目录中。部署站点后，此目录中的内容将在站点根路径中提供。因此，例如，如果您在 `/static/reference/cpp/` 添加了内容，则用户可以通过 `http://{server-url}/reference/cpp/` 访问该内容，并且您可以链接到这个目录来自`/reference/cpp/{file name}` 的其他页面。

您还可以将此目录用于项目使用的其他文件，包括图像文件。您可以在 [静态文件](https://gohugo.io/content-management/static-files/) 中找到有关提供静态文件的更多信息，包括为静态内容配置多个目录。

## RSS订阅

默认情况下，Hugo 将为主页和任何部分创建一个 RSS 提要。对于主要的 RSS 提要，您可以通过在您的 `config.toml` 中设置站点参数来控制要包含的部分。这是默认配置：

```toml
rss_sections = ["blog"]
```
To disable all RSS feeds, add the following to your `config.toml`:

```toml
disableKinds = ["RSS"]
```

{{% alert title="Note" color="info" %}}
如果您在 `config.toml` 中启用了我们的 [打印功能](/docs/adding-content/print/) 或其他指定的节级输出格式，请确保将 `"RSS"` 列为输出格式， 否则，您将无法获得部分级别的 RSS 提要（并且您的博客部分将无法获得漂亮的橙色 RSS 按钮）。 你的 `config.toml` 规范覆盖了 Hugo 默认的 [输出格式](https://gohugo.io/templates/output-formats/) 部分，即 HTML 和 RSS。

```toml
[outputs]
section = [ "HTML", "RSS", "print" ]
```
{{% /alert %}}

## 站点地图

默认情况下，Hugo 会为您生成的站点创建一个 `sitemap.xml` 文件：例如，[这里是站点地图](/sitemap.xml) 用于此站点。

您可以在“config.toml”中配置站点地图的更新频率、站点地图文件名和默认页面优先级：

```toml
[sitemap]
  changefreq = "monthly"
  filename = "sitemap.xml"
  priority = 0.5
```

要覆盖给定页面的任何这些值，请在页面 frontmatter 中指定它：

```yaml
---
title: "Adding Content"
linkTitle: "Adding Content"
weight: 1
description: >
  Add different types of content to your Docsy site.
sitemap:
  priority: 1.0
---
```

要了解有关配置站点地图的更多信息，请参阅 [站点地图模板](https://gohugo.io/templates/sitemap-template/)。
