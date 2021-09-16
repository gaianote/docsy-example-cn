---
title: "存储库链接"
linkTitle: "存储库链接"
weight: 9
description: >
  帮助您的用户与您的源存储库进行交互。
---

Docsy [文档和博客布局](/docs/adding-content/content/#adding-docs-and-blog-posts) 包含供读者编辑页面或通过您网站的源存储库为您的文档或项目创建问题的链接.当前为每个文档或博客页面生成的链接是：

* **编辑此页面**：将用户带到他们的文档存储库的分支（如果可用）中的页面内容的可编辑版本。如果用户没有您的文档存储库的当前分支，则邀请他们在进行编辑之前创建一个分支。然后，用户可以为您的文档创建拉取请求。
* **创建子页面**：将用户带到他们的文档存储库分支中的创建新文件表单。新文件将作为他们单击链接的页面的子文件定位。该表单将预先填充一个模板，用户可以编辑该模板以创建他们的页面。您可以通过将 `assets/stubs/new-page-template.md` 添加到您自己的项目来更改此设置。
* **创建文档问题**：将用户带到文档存储库中的新问题表单，并将当前页面的名称作为问题的标题。
* **创建项目问题**（可选）：将用户带到项目存储库中的新问题表单。如果您有单独的项目和文档存储库，并且您的用户想要针对正在讨论的项目功能而不是您的文档提交问题，这会很有用。

此页面向您展示如何使用您的 `config.toml` 文件配置这些链接。

目前 Docsy 仅支持“开箱即用”的 GitHub 存储库链接。如果您正在使用其他存储库（例如 Bitbucket）并希望生成存储库链接，请随时[添加功能请求或更新我们的主题](/docs/contribution-guidelines/)。

## 链接配置

您可以在 `config.toml` 中配置四个变量来设置链接，还有一个在页面元数据中。

### `github_repo`

您站点的源代码库的 URL。这用于生成**编辑此页面**、**创建子页面** 和**创建文档问题** 链接。

```toml
github_repo = "https://github.com/google/docsy"
```

### `github_subdir`（可选）

如果您的内容目录不在存储库的根目录中，请在此处指定一个值。 例如，该站点位于其 repo 的 `userguide` 子目录中。 设置此值意味着您的编辑链接将转到正确的页面。

```toml
github_subdir = "userguide"
```

### `github_project_repo`（可选）

如果您有一个单独的项目存储库，并且您希望您的用户能够从相关文档针对您的项目创建问题，请在此处指定一个值。 **创建项目问题** 链接仅在设置时出现。

```toml
github_project_repo = "https://github.com/google/docsy"
```

### `github_branch`（可选）

如果您想为其他 github 设置（如 **Edit this page** 或 **Create project issue**）引用不同的分支，请在此处指定一个值。

```toml
github_branch = "release"
```

### `github_url` (optional)

在您的页面元数据**中为此** 指定一个值，以为此页面设置特定的编辑 URL，如下例所示：

```yaml
---
title: "Example Page"
linkTitle: "Example Page"
date: 2017-01-05
github_url: "https://github.com/MyUsername/myrepo/edit/main/README.md"
description: >
  An example page.
---
```

如果您在多个 Git 存储库中有页面源文件，或者需要非 GitHub URL，这会很有用。 使用此值的页面只有 **Edit this page** 链接。
