---
title: "预览和部署"
linkTitle: "预览和部署"
weight: 7
description: >
  部署您的 Docsy 站点。
---

部署 Hugo 站点有多种可能的选择，包括 Netlify、Firebase Hosting、Bitbucket with Aerobatic 等；您可以在 [托管和部署](https://gohugo.io/hosting-and-deployment/) 中阅读有关它们的全部信息。 Hugo 还可以轻松地在本地部署您的站点，以便快速预览您的内容。

## 在本地为您的网站提供服务

根据您的部署选择，您可能希望在开发期间在本地为您的站点提供服务以预览内容更改。要在本地为您的站点提供服务：

1. 确保您拥有从您的存储库克隆的站点文件的最新本地副本。不要忘记使用`--recurse-submodules`，否则您将无法提取生成工作站点所需的一些代码。

    ``
    git clone --recurse-submodules --depth 1 https://github.com/my/example.git
    ``
   
    {{% alert title="Note" color="primary" %}}
如果您刚刚将主题作为子模块添加到站点的本地版本中，并且尚未将其提交到存储库，则必须在为站点提供服务之前获取主题自身子模块的本地副本。
    
    git 子模块更新 --init --recursive
    {{％ /警报 ％}}

1. 确保您在本地机器上安装了[先决条件和安装](/docs/getting-started/#prerequisites-and-installation) 中描述的工具，包括“postcss-cli”（您需要它来生成第一次运行服务器时的站点资源）。
1. 在您的站点根目录中运行 `hugo server` 命令。默认情况下，您的站点将在 http://localhost:1313/ 上可用。

现在您正在本地为您的站点提供服务，Hugo 将监视内容的更改并自动刷新您的站点。如果您有多个本地 git 分支，当您在 git 分支之间切换时，本地网站会反映当前分支中的文件。

## 构建环境和索引

默认情况下，使用 `hugo` 构建的 Hugo 站点（而不是使用 `hugo server` 在本地提供服务）具有 Hugo 构建环境 `production`。使用“生产”版本部署的 Docsy 站点可以被搜索引擎索引，包括 [Google 自定义搜索引擎](/docs/adding-content/navigation/#configure-search-with-a-google-custom-search-engine)。生产版本还针对实时部署优化了 JavaScript 和 CSS（例如，缩小了 JS 而不是更清晰的原始源代码）。

如果您不希望您部署的站点被搜索引擎索引（例如，如果您仍在开发您的实时站点），或者您希望构建站点的开发版本以供离线分析，您可以设置您的 Hugo 构建环境到其他内容，例如“development”（使用“hugo server”进行本地部署的默认值）、“test”或您选择的其他环境名称。

设置它的最简单方法是在指定或运行你的 `hugo` 命令时使用 `-e` 标志，如下例所示：

``
雨果 -e 开发
``


## 使用 Netlify 部署

我们建议使用 [Netlify](https://www.netlify.com/) 作为一种特别简单的方式，通过 [持续部署](https:// www.netlify.com/docs/continuous-deployment/)、当您或您的用户针对文档存储库创建拉取请求时生成的站点的预览等等。 Netlify 可免费用于开源项目，如果您需要更多支持，可以使用高级层。

在使用 Netlify 进行部署之前，请确保按照 [使用主题](/docs/getting-started/#using-the-theme ）。

然后按照 [Host on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/) 中的说明设置一个 Netlify 帐户（如果您还没有）并授权访问您的 GitHub 或其他 Git 提供商帐户。登录后：

1. 单击**来自 Git 的新站点**。
1. 单击您选择的 Git 提供商，然后从您的存储库列表中选择您的站点存储库。
1. 在**部署设置**页面：
   1. 对于你的 **Build 命令**，指定 `cd themes/docsy && git submodule update -f --init && cd ../.. && hugo`。您需要指定它而不仅仅是 `hugo`，以便 Netlify 可以使用主题的子模块。如果你不希望你的网站被搜索引擎索引，你可以添加一个环境标志来指定一个非`生产`环境，如[构建环境和索引](/#build-environments-and-indexing ）。
   1. 单击**显示高级**。
   1. 在 **Advanced build settings** 部分，单击 **New variable**。
   1. 指定 `HUGO_VERSION` 作为新变量的 **Key**，并指定 `0.53` 或更高版本作为其 **Value**。
1. 单击**部署站点**。

{{% alert title="Note" color="primary" %}}
在构建站点之前，Netlify 使用站点 repo 的 `package.json` 文件来安装任何 JavaScript 依赖项（如 `postcss`）。如果您还没有复制我们示例站点的此文件的版本，请确保您已指定我们所有的 [先决条件](/docs/getting-started/#install-postcs

```
  "devDependencies": {
    "autoprefixer": "^9.8.6",
    "postcss-cli": "^8.0.0",
    "postcss": "^8.0.0"
  }
```
{{% /alert %}}

或者，您可以按照相同的说明进行操作，但在 [`netlify.toml` 文件](https://docs.netlify.com/configure-builds/file-based-configuration/) 中指定您的 **Deploy settings** 您的存储库而不是在 **Deploy settings** 页面中。 您可以在 [Docsy 主题存储库](https://github.com/google/docsy/blob/master/netlify.toml) 中看到一个示例（但请注意，此处的构建命令有点不寻常，因为 Docsy 用户指南*在*主题存储库内）。

如果您有现有部署，则可以通过从 Netlify 中的站点列表中选择站点，然后单击 **站点设置** - **构建和部署**来查看和更新相关信息。 确保在 **Build image selection** 部分中选择了 **Ubuntu Xenial 16.04** - 如果您正在创建新部署，默认情况下会使用它。 您需要使用此映像来运行 Hugo 的扩展版本。

