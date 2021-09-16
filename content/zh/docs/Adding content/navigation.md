---
title: "导航和搜索"
date: 2017-01-05
weight: 3
description: >
   自定义站点导航并搜索您的 Docsy 站点。
---

## 顶级菜单

顶级菜单（出现在整个网站顶部导航栏中的菜单）使用您网站的 [`main` 菜单](https://gohugo.io/content-management/menus/)。 所有 Hugo 站点都有一个菜单项的“主”菜单数组，可通过“.Site.Menus”站点变量访问，并可通过页面前端内容或站点的“config.toml”填充。

要将页面或部分添加到此菜单中，请将其添加到站点的“主”菜单中的“config.toml”或目标页面的前端（在“_index.md”或“_index.html”中的部分， 因为那是部分登录页面）。 例如，以下是我们如何将文档部分登录页面添加到此站点的主菜单中：

```yaml
---
title: "Welcome to Docsy"
linkTitle: "Documentation"
menu:
  main:
    weight: 20
    pre: <i class='fas fa-book'></i>
---
```

菜单按页面“重量”从左到右排序。 因此，例如，带有“weight: 30”的部分索引或页面会出现在菜单中的“文档”部分之后，而带有“weight：10”的部分会出现在它之前。

如果您想在此菜单中添加指向外部站点的链接，请将其添加到 `config.toml` 中，并指定 `weight`。


```yaml
[[menu.main]]
    name = "GitHub"
    weight = 50
    url = "https://github.com/google/docsy/"
```

### 将图标添加到顶级菜单

如 [Hugo docs](https://gohugo.io/content-management/menus/#add-non-content-entries-to-a-menu) 中所述，您可以通过以下方式将图标添加到顶级菜单 将 pre 和/或 post 参数用于您站点的 `config.toml` 中定义的主菜单项或通过页面前端问题。 例如，以下配置将 GitHub 图标添加到 GitHub 菜单项，以及 **New!** 警报以指示这是菜单的新增功能。

```yaml
[[menu.main]]
    name = "GitHub"
    weight = 50
    url = "https://github.com/google/docsy/"
    pre = "<i class='fab fa-github'></i>"
    post = "<span class='alert'>New!</span>" 
```

您可以在 [FontAwesome 文档](https://fontawesome.com/icons?d=gallery&p=2) 中找到要使用的完整图标列表。 Docsy 默认包含免费的 FontAwesome 图标。

### 添加版本下拉列表

如果你在 `config.toml` 中添加了一些 `[params.versions]`，Docsy 主题会添加一个
版本选择器下拉到顶级菜单。

您可以在指南中找到更多信息
[版本控制您的文档](/docs/adding-content/versioning/)。

### 添加语言下拉菜单

如果你在 `config.toml` 中配置了不止一种语言，Docsy 主题会在顶级菜单中添加一个语言选择器下拉菜单。选择一种语言会将用户带到当前页面的翻译版本或给定语言的主页。

您可以在 [多语言支持](/docs/language/) 中找到更多信息。

## 部分菜单

“文档”部分左侧显示的部分菜单是根据“内容”树自动构建的。与顶级菜单一样，它按页面或部分索引“权重”（如果未设置“权重”，则按页面创建“日期”排序），与页面或索引的“标题”或“链接标题”（如果不同） , 作为它在菜单中的链接标题。如果部分子文件夹包含除 `_index.md` 或 `_index.html` 之外的页面，这些页面将显示为子菜单，再次按 `weight` 排序。例如，下面是这个页面的元数据，显示了它的 `weight` 和 `title`：

```yaml
---
title: "Navigation and Search"
linkTitle: "Navigation and Search"
date: 2017-01-05
weight: 3
description: >
  Customize site navigation and search for your Docsy site.
---
```

要从左侧导航菜单隐藏页面或部分，请在前面设置 `toc_hide: true`。

要在 [文档部分登录页面]({{< ref "content#docs-section-landing-pages" >}}) 上的部分摘要中隐藏页面，请在前面设置 `hide_summary: true`。 如果您想同时从目录菜单和部分摘要列表中隐藏页面，则需要在前面的内容中将 `toc_hide` 和 `hide_summary` 都设置为 `true`。

```yaml
---
title: "My Hidden Page"
weight: 99
toc_hide: true
hide_summary: true
description: >
  Page hidden from both the TOC menu and the section summary list.
---
```

### 部分菜单选项

默认情况下，部分菜单显示当前部分完全向下展开。这可能会使左侧导航太长并且难以扫描更大的站点。尝试在 `config.toml` 中设置站点参数 `ui.sidebar_menu_compact = true`。

使用紧凑菜单 (`.ui.sidebar_menu_compact = true`)，仅显示当前页面的祖先、兄弟和直接后代。您可以使用可选参数 `.ui.ul_show` 将所需的菜单深度设置为始终可见。例如，`.ui.ul_show = 1` 总是显示第一级菜单。

除了完全展开和紧凑的菜单选项，您还可以通过在`config.toml` 中设置站点参数`ui.sidebar_menu_foldable = true` 来创建可折叠菜单。可折叠菜单允许用户通过切换菜单中父节旁边的箭头图标来展开和折叠菜单节。

在大型网站（默认：> 2000 页）上，不会为每个页面生成部分菜单，而是为整个部分缓存。然后使用 JS 设置用于标记活动菜单项（和菜单路径）的 HTML 类。您可以使用可选参数 `.ui.sidebar_cache_limit` 调整激活缓存部分菜单的限制。

### 将图标添加到部分菜单

您可以通过在页面前端设置 `icon` 参数（例如 `icon: fas fa-tools`）将图标添加到侧边栏中的部分菜单。

您可以在 [FontAwesome 文档](https://fontawesome.com/icons?d=gallery&p=2) 中找到要使用的完整图标列表。 Docsy 默认包含免费的 FontAwesome 图标。

开箱即用，如果您想使用图标，您应该为同一菜单级别上的所有项目定义图标，以确保适当的外观。如果图标的使用方式不同，则可能需要单独调整 CSS。

### 将手动链接添加到部分菜单

默认情况下，部分菜单完全从您的部分页面生成。如果您想添加到此菜单的手动链接，例如指向外部站点或站点不同部分中的页面的链接，您可以通过在文档层次结构中创建一个*占位符页面文件*元数据（frontmatter）中的权重和一些特殊参数来指定链接详细信息。

要创建占位符页面，请像往常一样在您希望链接显示在菜单中的目录中创建一个页面文件，并将“manualLink”参数添加到其元数据中。如果页面在其元数据中有 `manualLink`，Docsy 会在该页面的部分菜单和部分索引（登录页面上某个部分的子页面列表 - 请参阅 [Docsy 中的描述] docs](/docs/adding-content/content/#docs-section-landing-pages))，但链接目的地被替换为 `manualLink` 的值。链接文本是占位符页面的`title`（或`linkTitle`，如果设置）。您还可以选择使用参数 `manualLinkTitle` 设置链接的 `title` 属性，并使用 `manualLinkTarget` 设置链接目标 - 例如，如果您希望在新选项卡中打开外部链接，则可以将链接目标设置为 ` _空白`。 Docsy 自动将 `rel=noopener` 添加到打开新选项卡的链接中，作为安全最佳实践。

 您还可以使用`manualLink` 向您网站的另一个现有页面添加额外的交叉引用。对于内部链接，您可以选择使用参数 `manualLinkRelref` 而不是 `manualLink` 来使用内置的 Hugo 函数 [relref](https://gohugo.io/functions/relref/ "External link to official Hugo Docs" ）。如果 `relref` 无法在您的站点中找到唯一的页面，Hugo 会抛出错误消息。

 {{% alert title="Note" %}}
尽管所有基于占位符文件生成的菜单和登录页面链接都是根据参数 `manualLink` 或 `manualLinkRelref` 设置的，但 Hugo 仍然为该文件生成一个常规的 HTML 站点页面，尽管没有生成指向它的链接。 为避免在用户意外登陆生成的占位符页面时造成混淆，我们建议在页面的正常内容和/或页面描述中指定外部链接的 URL。
 {{% /alert %}}

## 面包屑导航

默认情况下启用面包屑导航。要禁用面包屑导航，请在 `config.toml` 中设置站点参数 `ui.breadcrumb_disable = true`。

## 站点搜索选项

Docsy 提供了多种选项，让您的读者可以搜索您的网站内容，因此您可以选择适合您需求的选项。您可以选择：

* [Google 自定义搜索引擎](#configure-search-with-a-google-custom-search-engine) (GCSE)，默认选项，它使用 Google 对您的公共网站的索引来生成搜索结果页面。
* [Algolia DocSearch](#configure-algolia-docsearch)，它使用 Algolia 的索引和搜索机制，并在您的读者使用搜索框时提供有组织的搜索结果下拉列表。 Algolia DocSearch 对于公共文档站点是免费的。
* [使用 Lunr 进行本地搜索](#configure-local-search-with-lunr)，它使用 Javascript 来索引和搜索您的站点，而无需连接到外部服务。此选项不要求您的网站是公开的。

如果您在 `config.toml` 中启用这些搜索选项中的任何一个，搜索框将显示在顶部导航栏的右侧。默认情况下，左侧导航窗格中部分菜单的顶部还会显示一个搜索框，如果您愿意，或者如果您使用的搜索选项仅适用于顶部搜索框，您可以将其禁用。

请注意，如果您不小心在 `config.toml` 中启用了多个搜索选项，您可能会得到意想不到的结果（例如，如果您为 Algolia DocSearch 添加了 `.js`，如果您启用，您将获得 Algolia 结果GCSE 搜索但忘记禁用 Algolia 搜索）。

### 禁用侧边栏搜索框

默认情况下，搜索框同时出现在顶部导航栏和侧边栏左侧导航窗格的顶部。如果你不想要侧边栏搜索框，在 `config.toml` 中将 `sidebar_search_disable` 设置为 `true`：

```
sidebar_search_disable = true
```

## 使用 Google 自定义搜索引擎配置搜索

默认情况下，Docsy 使用 [Google 自定义搜索引擎](https://cse.google.com/cse/all) (GCSE) 来搜索您的网站。要启用此功能，您首先需要确保已构建并部署了[站点的生产版本](/docs/deployment#build-environments-and-indexing)，否则您的站点将无法抓取并编入索引。

### 设置站点搜索

1. 单击[自定义搜索页面](https://cse.google.com/cse/all) 上的**新搜索引擎** 并按照说明为您部署的站点创建 Google 自定义搜索引擎。记下新搜索引擎的 ID。
1. 使用**编辑搜索引擎** 选项将您想要的任何进一步配置添加到您的搜索引擎。特别是您可能想要执行以下操作：

    * 选择**外观**。将默认的 **Overlay** 布局更改为 **Results only**，因为此选项意味着您的搜索结果会嵌入到您的搜索页面中，而不是出现在单独的框中。单击**保存**以保存您的更改。
    * 编辑默认结果链接行为，以便您网站的搜索结果不会在新选项卡中打开。为此，请选择 **搜索功能** - **高级** - **网络搜索设置**。在**链接目标** 字段中，键入“\_parent”。单击**保存**以保存您的更改。
    
{{% alert title="Tip" %}}
您的站点搜索结果应该会在几天内显示出来。 如果需要更长的时间，您可以通过[通过 Google Search Console 提交站点地图](https://support.google.com/webmasters/answer/183668?hl=en) 手动请求将您的网站编入索引。
{{% /alert %}}

### 添加搜索页面

设置好搜索引擎后，您可以将该功能添加到您的网站：

1. 确保您在 `content/en/search.md` 中有一个 Markdown 文件（如果需要，还有一个其他语言）来显示您的搜索结果。 它只需要一个标题和 `layout: search`，如下例所示：

    ```
    ---
    title: Search Results
    layout: search
    ---
    ```

1. 将您的 Google 自定义搜索引擎 ID 添加到 `config.toml` 中的站点参数。 如果需要，您可以为每种语言添加不同的值。

    ```
    # Google Custom Search Engine ID. Remove or comment out to disable search.
    gcs_engine_id = "011737558837375720776:fsdu1nryfng"
    ```

### 禁用 GCSE 搜索

如果您没有为您的项目指定 Google 自定义搜索引擎 ID，并且没有启用任何其他搜索选项，搜索框将不会出现在您的网站中。 如果您使用示例站点中的默认 `config.toml` 并且想要禁用搜索，只需注释掉或删除相关行。

## 配置 Algolia DocSearch

作为 GCSE 的替代方案，您可以使用带有此主题的 [Algolia DocSearch](https://community.algolia.com/docsearch/)。 Algolia DocSearch 对于公共文档站点是免费的。

### 注册 Algolia DocSearch

在 [https://community.algolia.com/docsearch/#join-docsearch-program](https://community.algolia.com/docsearch/#join-docsearch-program) 上填写表格。

如果您被该计划接受，您将通过电子邮件收到来自 Algolia 的 JavaScript 代码以添加到您的文档站点。

### 添加 Algolia DocSearch

1. 在 `config.toml` 中启用 Algolia DocSearch。

    ```
    # Enable Algolia DocSearch
    algolia_docsearch = true
    ```

2. 删除或注释掉 `config.toml` 中的任何 GCSE ID，并确保本地搜索设置为 `false`，因为您只能启用一种类型的搜索。请参阅[禁用 GCSE 搜索](#disabling-gcse-search)。

3. 禁用`config.toml` 中的侧边栏搜索，因为 Algolia DocSearch 目前不支持。请参阅[禁用侧边栏搜索框](#disabling-the-sidebar-search-box)。

3. 将 Algolia 提供给您的 JavaScript 代码添加到您网站上每个页面的头部和正文中。有关详细信息，请参阅[将代码添加到头部或正文结束之前](/docs/adding-content/lookandfeel/#add-code-to-head-or-before-body-end)。

4. 使用适当的 CSS 选择器更新主体端 Javascript 中的 `inputSelector` 字段（例如，`.td-search-input` 以使用该主题的默认 CSS）。

完成这些步骤后，应该在您的站点上启用 Algolia 搜索。搜索结果显示为搜索框下方的下拉列表，因此您无需添加任何搜索结果页面。

## 使用 Lunr 配置本地搜索

[Lunr](https://lunrjs.com/) 是一种基于 Javascript 的搜索选项，可让您为网站编制索引并使其可搜索，而无需外部服务器端搜索服务。这是一个不错的选择，特别是对于较小的或非公共站点。

要将 Lunr 搜索添加到您的 Docsy 站点：

1. Enable local search in `config.toml`.

    ```
    # Enable local search
    offlineSearch = true
    ```

2. 删除或注释掉 `config.toml` 中的任何 GCSE ID，并确保 Algolia DocSearch 设置为 `false`，因为您只能启用一种类型的搜索。 请参阅[禁用 GCSE 搜索](#disabling-gcse-search)。

完成这些步骤后，将为您的站点启用本地搜索，并且当您使用搜索框时，结果会显示在下拉列表中。

{{% alert title="Tip" %}}
如果您正在 [本地测试](/docs/deployment/#serving-your-site-locally) 使用 Hugo 的本地服务器功能，您需要首先通过运行构建您的 `offline-search-index.xxx.json` 文件 `雨果`。 如果你在构建 `offline-search-index.xxx.json` 时运行 Hugo 服务器，你可能需要停止服务器并重新启动它才能看到你的搜索结果。
{{% /alert %}}

### 更改本地搜索结果的摘要长度

您可以通过在 `config.toml` 中设置 `offlineSearchSummaryLength` 来自定义摘要长度。

```
#Enable offline search with Lunr.js
offlineSearch = true
offlineSearchSummaryLength = 200
```

### 改变本地搜索的最大结果计数

您可以通过在 `config.toml` 中设置 `offlineSearchMaxResults` 来自定义最大结果计数。

```
#Enable offline search with Lunr.js
offlineSearch = true
offlineSearchMaxResults = 25
```

### 更改本地搜索结果弹出框的宽度

搜索结果弹出框的宽度会根据内容自动加宽。

如果要限制宽度，在`assets/scss/_variables_project.scss`中加入如下scss。

```scss
body {
    .popover.offline-search-result {
        max-width: 460px;
    }
}
```

### 从本地搜索结果中排除页面

要从本地搜索结果中排除页面，请将 `exclude_search: true` 添加到每个页面的前端：

```yaml
---
title: "Index"
weight: 10
exclude_search: true
---
```
