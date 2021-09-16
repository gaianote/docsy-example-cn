---
title: "文档版本控制"
date: 2020-02-02
weight: 4
description: >
   为文档的多个版本自定义导航和横幅。
---

根据您项目的版本和版本控制，您可能希望让您的用户访问您的文档的先前版本。 您如何部署以前的版本取决于您。 此页面描述了 Docsy 功能，您可以使用这些功能在不同版本的文档之间提供导航并在存档站点上显示信息横幅。

## Adding a version drop-down menu

如果你在 `config.toml` 中添加一些 `[params.versions]`，Docsy 主题会在顶级菜单中添加一个版本选择器下拉菜单。 您为要添加到菜单中的每个版本指定 URL 和名称，如下例所示：

```
# Add your release versions here
[[params.versions]]
  version = "master"
  url = "https://master.kubeflow.org"

[[params.versions]]
  version = "v0.2"
  url = "https://v0-2.kubeflow.org"

[[params.versions]]
  version = "v0.3"
  url = "https://v0-3.kubeflow.org"
```

请记住添加您当前的版本，以便用户可以返回！

版本下拉菜单的默认标题是 **Releases**。 要更改标题，更改`config.toml`中的`version_menu`参数：

```
version_menu = "Releases"
```

You can read more about Docsy menus in the guide to
[navigation and search](/docs/adding-content/navigation/).

## 在存档的文档站点上显示横幅

如果您为旧版本的文档创建存档快照，您可以在存档文档的每一页顶部添加注释，让读者知道他们看到的是未维护的快照，并为他们提供指向最新版本的链接。

例如，请参阅 [Kubeflow v0.6](https://v0-6.kubeflow.org/docs/) 的存档文档：

<figure>
  <img src="/images/version-banner.png"
       alt="A text box explaining that this is an unmaintained snapshot of the docs."
       class="mt-3 mb-3 border border-info rounded" />
  <figcaption>Figure 1. The banner on the archived docs for Kubeflow v0.6
  </figcaption>
</figure>

要将横幅添加到您的文档站点，请在您的
`config.toml` 文件：

1. 将 `archived_version` 参数设置为 `true`：

    ```
    archived_version = true
    ```

1. 将 `version` 参数设置为归档文档集的版本。 为了
   例如，如果存档的文档适用于 0.1 版：

    ```
    version = "0.1"
    ```

1. 确保 `url_latest_version` 包含您要引导读者访问的网站的 URL。 在大多数情况下，这应该是最新版本文档的 URL：
    ```
    url_latest_version = "https://your-latest-doc-site.com"
    ```
