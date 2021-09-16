---
title: "多语言支持"
linkTitle: "多语言支持"
weight: 7
description: >
  在您的站点中支持多种语言。
---

如果您想提供多种语言的网站内容，Docsy 主题和 Hugo 可以轻松添加翻译内容并让您的用户在语言版本之间导航。

## 内容和配置

要添加多种语言的内容，您首先需要在站点配置的“语言”部分定义可用语言。 每种语言都可以有自己的特定于语言的配置。 例如，Docsy 示例站点配置指定它提供英语和挪威语的内容，并且访问者将默认看到的语言版本是英语：

```toml
contentDir = "content/en"
defaultContentLanguage = "en"
defaultContentLanguageInSubdir = false
...
[languages]
[languages.en]
title = "Docsy"
description = "Docsy does docs"
languageName ="English"
# Weight used for sorting.
weight = 1
[languages.no]
title = "Docsy"
description = "Docsy er operativsystem for skyen"
languageName ="Norsk"
contentDir = "content/no"
time_format_default = "02.01.2006"
time_format_blog = "02.01.2006"
```

任何未在 `[languages]` 块中定义的设置都将回退到该设置的全局值：因此，例如，除非用户选择挪威语，否则用于上述站点的内容目录将是 `content/en`选项。

更新站点配置后，您可以在源代码库中为每个语言版本创建一个内容根目录，例如“content/en”用于英文文本，并添加您的 [content](/docs/adding-content/content /） 照常。有关多语言支持的更多信息，请参阅 [Hugo Docs](https://gohugo.io/content-management/multilingual)。

{{% alert title="Tip" %}}
如果您的网站有可能被翻译成其他语言，请考虑在特定语言的子目录中使用您的内容创建您的网站，因为这意味着如果您添加另一种语言，则无需移动它。
{{% /alert %}}

要添加其他网站元素（例如按钮文本）的多种语言版本，请参阅下面的 [国际化捆绑包](#internationalization-bundles) 部分。

## 选择语言

如果你在 `config.toml` 中配置了不止一种语言，Docsy 主题会在顶级菜单中添加一个语言选择器下拉菜单。选择一种语言会将用户带到当前页面的翻译版本或给定语言的主页。

## 国际化包

所有 UI 字符串（按钮文本等）都捆绑在主题中的 `/i18n` 中，每种语言都有一个 `.toml` 文件。

如果您选择的语言当前不在主题中，并且您为所有常见的 UI 字符串创建了自己的 `.toml` 文件（例如，如果您将 UI 文本翻译成日语并创建名为`jp.toml`)，我们建议您**在主题中**而不是在您自己的项目中执行此操作，以便其他人可以重复使用。任何额外的字符串或覆盖的值都可以添加到项目的`/i18n` 文件夹中。

{{% alert title="Hugo Tip" %}}
在进行翻译工作时运行 `hugo server --i18n-warnings`，因为它会给你关于缺少哪些字符串的警告。
{{% /alert %}}


