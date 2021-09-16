---
title: "Logos 与图片"
linkTitle: "Logos 与图片"
date: 2017-01-05
weight: 6
description: >
  在项目中添加和自定义徽标、图标和图像。
---

## 添加您的 logo

在您的项目中将您的项目 logo 添加为 `assets/icons/logo.svg`。 这会覆盖主题中的默认 Docsy logo。 如果您不想要项目 logo，请在您的“config.toml”中将“navbar_logo”设置为“false”（或删除该变量）：

```
navbar_logo = false
```

如果您稍后决定要向导航栏添加 logo，则可以将参数设置为“true”：

```
navbar_logo = true
```

{{% alert title="Tip" %}}
您的 logo 作为内联 SVG 包含在默认 Docsy 导航栏中，具有以下 CSS 样式（来自 [`_nav.scss`](https://github.com/google/docsy/blob/master/assets/scss/_nav.scss))：

```
svg {
    display: inline-block;
    margin: 0 10px;
    height: 30px;
}
```

为了确保您的徽标正确显示，您可能需要调整它的大小，确保它没有高度和宽度属性，以便其大小完全响应，或者使用您自己的 CSS 覆盖默认样式。
{{% /alert %}}

## 添加您的收藏夹

最简单的方法是通过 http://cthedot.de/icongen（它允许您从单个图像创建大量图标大小和选项）和/或 [https://favicon .io](https://favicon.io)，并将它们放在您站点项目的`static/favicon`目录中。 这将覆盖主题中的默认图标。

请注意，https://favicon.io 创建的尺寸范围不如 Icongen，但确实可以让您从文本快速创建收藏夹图标：如果您想创建文本收藏夹图标，您可以使用此站点生成它们，然后使用 Icongen 从生成的“.png”文件中创建更多尺寸（如有必要）。

如果您有特殊的网站图标要求，您可以使用您的链接创建自己的 `layouts/partials/favicons.html`。

## 添加图片

### 登陆页面

Docsy 的 [`blocks/cover` 简码](/docs/adding-content/shortcodes/#blocks-cover) 可以轻松地将大型封面图片添加到您的着陆页。 短代码在着陆页的 [Page Bundle](https://gohugo.io/content-management/page-bundles/) 中查找名称中带有“背景”一词的图像 - 例如，如果您 已经复制了示例站点，`content/en/_index.html` 中的着陆页图片是`content/en/featured-background.jpg`。

您可以使用块的 `height` 参数指定封面块容器（及其图像）的首选显示高度。 要获得完整的视口高度，请使用“full”：

```html
{{</* blocks/cover title="Welcome to the Docsy Example Project!" image_anchor="top" height="full" color="orange" */>}}
...
{{</* /blocks/cover */>}}
```

对于较短的图像，如示例站点的“关于”页面中，使用 `min`、`med`、`max` 或 `auto`（图像的实际高度）之一：

```html
{{</* blocks/cover title="About the Docsy Example" image_anchor="bottom" height="min" */>}}
...
{{</* /blocks/cover */>}}
```

### 其他页面

要将内嵌图像添加到其他页面，请使用 [`imgproc` 简码](/docs/adding-content/shortcodes/#imgproc)。 或者，如果您愿意，只需使用常规 Markdown 或 HTML 图像并将您的图像文件添加到项目的“静态”目录中。 您可以在 [添加静态内容](/docs/adding-content/content/#adding-static-content) 中找到有关使用此目录的更多信息。

## 本网站使用的图片

本站用作背景图片的图片属于[公共领域](https://commons.wikimedia.org/wiki/User:Bep/gallery#Wed_Aug_01_16:16:51_CEST_2018)，可以自由使用。 示例站点中的粥图片是来自<a href="https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=531209"> Pixabay </a> 的 <a href="https://pixabay.com/users/iha31-560629/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=531209">iha31</a>
