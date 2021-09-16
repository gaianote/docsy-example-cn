---
title: "分类支持"
linkTitle: "分类支持"
weight: 10
tags: ["Tagging", "Structuring Content", "Labelling"]
categories: ["Taxonomies"]
description: >
  使用标签、类别、标记等分类法来构建内容。
---

Docsy 在其文档和博客部分支持 Hugo 的分类法（请参阅：https://gohugo.io/content-management/taxonomies/）。 您可以看到默认布局，并可以在此页面上测试生成的链接的行为。

## 术语

要了解分类法的用法，您应该了解以下术语：

Taxonomy
:可用于对内容进行分类的分类 - 例如：标签、类别、项目、人员

Term
:分类法中的一个键 - 例如 项目内：项目A、项目B

Value
:分配给术语的一段内容 - 例如 属于特定项目的网站页面

您可以在 Hugo 官方文档中找到电影网站的示例分类法：https://gohugo.io/content-management/taxonomies/#example-taxonomy-movie-website

## 参数

`config.toml` 中有各种参数来控制分类法的功能。

默认情况下，Hugo 中启用了 `tags` 和 `categories` 的分类法（参见：https://gohugo.io/content-management/taxonomies/#default-taxonomies）。 在 Docsy 中，`config.toml` 中的分类法默认为 __disabled__：

```toml
disableKinds = ["taxonomy", "taxonomyTerm"]
```

如果你想在 Docsy 中启用分类法，你必须在你的项目 `config.toml` 中删除（或注释掉）这一行。 然后 Hugo 将为 `tags` 和 `categories` 生成分类页面。 如果你想使用其他分类法，你必须在你的 `config.toml` 中定义它们。 如果你想在你自己的分类法旁边使用默认的分类法`tags`和`categories`，你还必须在你自己的分类法旁边定义它们。 您需要为每个分类法提供复数和单数标签。

通过以下示例，您可以在默认分类法 `tags` 和 `categories` 旁边定义一个额外的分类法 `projects`：

```toml
[taxonomies]
tag = "tags"
category = "categories"
project = "projects"
```

您可以在项目 `config.toml` 中使用以下参数来控制为每篇文章指定的分类术语的输出。 Docsy 中的文档和/或博客部分的页面或 Docsy 右侧栏中的“标签云”：

```toml
[params.taxonomy]
taxonomyCloud = ["projects", "tags"] # set taxonomyCloud = [] to hide taxonomy clouds
taxonomyCloudTitle = ["Our Projects", "Tag Cloud"] # if used, must have same lang as taxonomyCloud
taxonomyPageHeader = ["tags", "categories"] # set taxonomyPageHeader = [] to hide taxonomies on the page headers
```

上面的设置只会在 Docsy 的右侧边栏中显示 `projects` 和 `tags`（标题为“Our Projects”和“Tag Cloud”）的分类云，以及为分类法`tags` 和 `categories` 分配的术语每页。

要禁用任何分类云，您必须设置参数`taxonomyCloud = []` resp。如果您不想显示指定的术语，则必须设置 `taxonomyPageHeader = []`。

默认情况下，分类法的复数标签用作云标题。您可以使用 `taxonomyCloudTitle` 覆盖默认的云标题。但是如果你这样做，你必须为每个启用的分类云定义一个手动标题（`taxonomyCloud` 和 `taxonomyCloudTitle` 必须具有相同的长度！）。

如果你没有设置参数 `taxonomyCloud` resp。 `taxonomyPageHeader` 分类云。将生成所有定义的分类法的指定术语。
##部分

默认情况下用于显示分类法的部分是这样定义的，您应该也可以在自己的布局中轻松使用它们。

### taxonomy_terms_article

部分“taxonomy_terms_article”显示了文章和页面（部分参数“context”，大部分时间是当前页面或上下文“.”）的给定分类法（部分参数“taxo”）的所有指定术语。

`layouts/docs/list.html` 中文档部分每个页面标题的示例用法：

```go-html-template
{{ $context := . }}
{{ range $taxo, $taxo_map := .Site.Taxonomies }}
  {{ partial "taxonomy_terms_article.html" (dict "context" $context "taxo" $taxo ) }}
{{ end }}
```

这将为您在当前页面（或上下文）定义的分类法中为您提供一个包含所有指定术语的列表：

```html
<div class="taxonomy taxonomy-terms-article taxo-categories">
  <h5 class="taxonomy-title">Categories:</h5>
  <ul class="taxonomy-terms">
    <li><a class="taxonomy-term" href="//localhost:1313/categories/taxonomies/" data-taxonomy-term="taxonomies"><span class="taxonomy-label">Taxonomies</span></a></li>
  </ul>
</div>
<div class="taxonomy taxonomy-terms-article taxo-tags">
  <h5 class="taxonomy-title">Tags:</h5>
  <ul class="taxonomy-terms">
    <li><a class="taxonomy-term" href="//localhost:1313/tags/tagging/" data-taxonomy-term="tagging"><span class="taxonomy-label">Tagging</span></a></li>
    <li><a class="taxonomy-term" href="//localhost:1313/tags/structuring-content/" data-taxonomy-term="structuring-content"><span class="taxonomy-label">Structuring Content</span></a></li>
    <li><a class="taxonomy-term" href="//localhost:1313/tags/labelling/" data-taxonomy-term="labelling"><span class="taxonomy-label">Labelling</span></a></li>
  </ul>
</div>
```

### taxonomy_terms_cloud

部分 `taxonomy_terms_cloud` 显示您站点的给定分类法（部分参数 `taxo`）的所有使用术语（部分参数 `context`，大部分时间是当前页面或上下文 `.`）并带有参数 `title` 作为标题。

部分“taxonomy_terms_clouds”中的示例用法，用于显示所有定义的分类法及其术语：

```go-html-template
{{ $context := . }}
{{ range $taxo, $taxo_map := .Site.Taxonomies }}
  {{ partial "taxonomy_terms_cloud.html" (dict "context" $context "taxo" $taxo "title" ( humanize $taxo ) ) }}
{{ end }}
```

例如，这将为您提供以下分类法“categories”的 HTML 标记：
```html
<div class="taxonomy taxonomy-terms-cloud taxo-categories">
  <h5 class="taxonomy-title">Cloud of Categories</h5>
  <ul class="taxonomy-terms">
    <li><a class="taxonomy-term" href="//localhost:1313/categories/category-1/" data-taxonomy-term="category-1"><span class="taxonomy-label">category 1</span><span class="taxonomy-count">3</span></a></li>
    <li><a class="taxonomy-term" href="//localhost:1313/categories/category-2/" data-taxonomy-term="category-2"><span class="taxonomy-label">category 2</span><span class="taxonomy-count">1</span></a></li>
    <li><a class="taxonomy-term" href="//localhost:1313/categories/category-3/" data-taxonomy-term="category-3"><span class="taxonomy-label">category 3</span><span class="taxonomy-count">2</span></a></li>
    <li><a class="taxonomy-term" href="//localhost:1313/categories/category-4/" data-taxonomy-term="category-4"><span class="taxonomy-label">category 4</span><span class="taxonomy-count">6</span></a></li>
  </ul>
</div>
```

### taxonomy_terms_clouds

部分 `taxonomy_terms_clouds` 是部分 `taxonomy_terms_cloud` 的包装器，带有唯一的参数 `context`（大部分时间是当前页面或上下文 `.`）并检查你项目的分类参数 `config.toml` 以循环 将所有列出的分类法扔到参数 `taxonomyCloud` 中。 如果未设置`taxonomyCloud`，则所有定义的页面分类法。

## 对分类法的多语言支持

与内容相关的分类术语仅在语言内进行计数和链接！ 分类支持的控制参数也可以获得指定的特定语言。