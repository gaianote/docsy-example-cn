---
title: "分析、用户反馈、SEO"
date: 2019-06-05
weight: 8
description: >
  将 Google Analytics 跟踪添加到您的网站，使用“此页面有帮助吗？” 小部件数据，禁用单个小部件页面或所有页面，并更改响应文本。 查看哪些数据用于为 SEO 创建“元描述”标签
---

## 添加分析

Docsy 主题通过 Hugo 的 [内部模板](https://gohugo.io/templates/internal/#google) 包含对 [Google Analytics](https://analytics.google.com/analytics/web/) 的内置支持 -analytics），包含在主题中。 按如下所述设置 Google Analytics（分析）后，您网站的使用信息（例如页面浏览量）将发送到您的 Google Analytics（分析）帐户。

### 设置

1. 确保您已为您的网站 [设置 Google Analytics 属性](https://support.google.com/analytics/answer/1042508)：这会为您提供一个 Analytics ID 以添加到您的配置中，然后 Docsy 添加到您网站的所有页面。
1. 打开`config.toml`。
1. 通过将跟踪 ID 属性设置为您网站的分析 ID 来启用 Google Analytics。

        [services.googleAnalytics]
        id = "UA-00000000-0"

1. 保存并关闭`config.toml`。
1. 确保您的站点是使用 `HUGO_ENV="production"` 构建的，因为 Docsy 仅将 Analytics 跟踪添加到生产就绪站点。 您可以将此变量指定为 Hugo 的命令行标志： 

    ```
    $ env HUGO_ENV="production" hugo
    ```

    Alternatively, if you're using Netlify, you can specify it as a Netlify [deployment setting](https://www.netlify.com/docs/continuous-deployment/#build-environment-variables) in `netlify.toml` or the Netlify UI, along with the Hugo version.


## 用户反馈

默认情况下，Docsy 会显示“此页面有帮助吗？” 每个底部的反馈小部件文档页面，如图1所示。

<figure>
  <img src="/images/feedback.png"
       alt="The user is presented with the text 'Was this page helpful?' followed
            by 'Yes' and 'No' buttons."/>
  <figcaption>Figure 1. The feedback widget, outlined in red</figcaption>
</figure>

单击 **Yes** 后，用户应该会看到如图 2 所示的响应。您可以配置`config.toml` 中的响应文本。

<figure>
  <img src="/images/yes.png"
       alt="After clicking 'Yes' the widget responds with 'Glad to hear it!
            Please tell us how we can improve.' and the second sentence is a link which,
            when clicked, opens GitHub and lets the user create an issue on the
            documentation repository."/>
  <figcaption>
    Figure 2. An example <b>Yes</b> response
  </figcaption>
</figure>

### How is this data useful?

当您有很多文档，而没有足够的时间更新所有文档时，您可以使用“此页面有帮助吗？” 反馈数据可帮助您决定优先处理哪些页面。 一般来说，从浏览量大、评分低的页面开始。 在此上下文中，“低评分”表示用户点击 **No** --- 该页面没有帮助 --- 比 **Yes** --- 该页面有帮助的频率更高。 您还可以研究评分较高的页面，以围绕用户认为它们有帮助的原因提出假设。

一般来说，如果您尽可能在文档中引入孤立的更改，您可以更加确定用户认为哪些模式有用或无用。 例如，假设您找到一个不再与产品匹配的教程。 你更新说明，一个月后再回来查看，分数提高了。 您现在可以在最新的说明和更高的评级之间建立关联。 或者，假设您研究了评分较高的页面并发现它们都是从代码示例开始的。 您发现其他 10 个页面的代码示例位于底部，将示例移动到顶部，然后发现每个页面的分数都有所提高。 由于这是您在每个页面上引入的唯一更改，因此更有理由相信您的用户会发现页面顶部的代码示例很有帮助。 换句话说，应用于技术写作的科学方法！

### 设置

1. 打开`config.toml`。
1. 确保已启用 Google Analytics，如[上文](#setup) 所述。
1. 设置用户点击**是**或**否**后看到的响应文本。

        [params.ui.feedback]
        enable = true
        yes = 'Glad to hear it! Please <a href="https://github.com/USERNAME/REPOSITORY/issues/new">tell us how we can improve</a>.'
        no = 'Sorry to hear that. Please <a href="https://github.com/USERNAME/REPOSITORY/issues/new">tell us how we can improve</a>.'
1. 保存并关闭`config.toml`。

### 访问反馈数据

本节假设您基本熟悉 Google Analytics。例如，如果您可以访问多个文档站点，您应该知道如何检查特定时间范围内的综合浏览量并在帐户之间导航。

1. 打开谷歌分析。
1. 打开**行为** > **事件** > **概览**。
1. 在 **Event Category** 表中，单击 **Helpful** 行。点击**查看完整报告**如果
   您没有看到 **Helpful** 行。
1. 单击**事件标签**。您现在可以逐页细分评分。

以下是 4 列代表的内容：

* **总事件数** 是用户点击* * **是** 或**否** 的总次数。
* **Unique Events** 粗略地表明用户对您的网页进行评分的频率
  会议。例如，假设您的 **Total Events** 为 5000，而 **Unique Events** 为 2500。
  这意味着您有 2500 个用户，每个会话对 2 个页面进行评分。
* **事件值** 没有那么有用。
* **平均。值** 是该页面的汇总评分。该值始终在 0 之间
  和 1. 当用户点击 **No** 时，0 值被发送到 Google Analytics。当用户点击
  **是** 发送值 1。你可以把它想象成一个百分比。如果一个页面有
  **平均。值**为 0.67，表示 67% 的用户点击了 **Yes**，33% 的用户点击了 **No**。

[events]: https://developers.google.com/analytics/devguides/collection/analyticsjs/events
[PR]: https://github.com/google/docsy/pull/1/files

存储“此页面有用吗？”的底层 Google Analytics 基础架构。 数据称为[事件][事件]。 请参阅 [docsy pull request #1][PR] 以确切了解当用户单击 **Yes** 或 **No** 时会发生什么。 它只是一个 `click` 事件监听器
触发 Google Analytics JavaScript 函数以记录事件，禁用 **Yes** 和 **No** 按钮，并显示响应文本。

### 在单个页面上禁用反馈

将 `hide_feedback: true` 添加到页面的前端。

### 禁用所有页面上的反馈

在 `config.toml` 中将 `params.ui.feedback.enable` 设置为 `false`：

    [params.ui.feedback]
    enable = false

## 搜索引擎优化元标记

查看 Google 的 [搜索引擎优化 (SEO) 入门指南](https://developers.google.com/search/docs/beginner/seo-starter-guide)，了解如何针对 SEO 优化您的网站。

Google [推荐](https://developers.google.com/search/docs/beginner/seo-starter-guide?hl=en%2F#descriptionmeta) 使用 `description` 元标记告诉搜索引擎您的页面是什么 关于。 Docsy 主题会在 `layouts/partials/head.html` 文件中为你创建并填充这个元标记：

```html
{{ if .Page.Description }}
  <meta name="description" content="{{ .Page.Description }}">
{{ else }}
  {{ $desc := (.Page.Content | safeHTML | truncate 150) }}
  <meta name="description" content="{{ $desc }}">
{{ end }}
```

`.Page.Description` 是来自 `description` [frontmatter field]({{< ref "content#page-frontmatter" >}}) 的文本。 如果页面的前端没有“描述”，则使用页面内容的前 150 个字符代替。

例如，如果您的前言 `description` 是：

```markdown
---
description: >
  Add Google Analytics tracking to your site.
---
```

那么渲染页面上的元`description`标签是：

```html
<meta name="description" content="Add Google Analytics tracking to your site.">
```

您可以将其他元标记添加到您自己的 `head-end.html` 部分副本中。 有关详细信息，请参阅 [自定义模板]({{< ref "lookandfeel#customizing-templates" >}})。
