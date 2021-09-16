---
title: "入门"
linkTitle: "入门"
weight: 2
date: 2018-07-30
description: >
  这个页面告诉你如何开始使用 Docsy 主题，包括安装和基本配置。
---

## 先决条件和安装

### 使用我们的 Docker 镜像

我们提供了一个 Docker 镜像，您可以使用它来运行和测试您的 Docsy 本地站点，而无需安装所有 Docsy 的依赖项。

您可以按照我们的 [Docker 快速入门教程](快速入门-docker)。如果你不想使用 Docker，按照以下说明安装 Hugo 和 PostCSS。

### 安装 Hugo

你需要一个[最近 **extended** 版本](https://github.com/gohugoio/hugo/releases)（我们推荐 0.75.0 或更高版本）的 [Hugo](https://gohugo.io/) 对使用 Docsy 的站点（如本站点）进行本地构建和预览。如果从发布页面安装，请确保获取支持 [SCSS](https://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html) 的 `extended` Hugo 版本；您可能需要向下滚动版本列表才能看到它。

有关完整的 Hugo 文档，请参阅 [gohugo.io](https://gohugo.io/)。

#### Linux

小心使用`sudo apt-get install hugo`，因为它[不会为所有 Debian/Ubuntu 版本提供`extended` 版本](https://gohugo.io/getting-started/installing/#debian-and-ubuntu)，并且可能不是最新的 Hugo 版本。

如果您已经安装了 Hugo，请检查您的版本：`hugo version`

如果结果是 `v0.75` 或更早版本，或者没有看到 `Extended`，则需要安装最新版本。你可以在 [Install Hugo](https://gohugo.io/getting-started/installing/#linux) 中看到 Linux 安装选项的完整列表。下面展示了如何从发布页面安装 Hugo：

1.  进入[Hugo 发布](https://github.com/gohugoio/hugo/releases) 页面。
2.  在最新版本中，向下滚动直到找到**扩展**版本。下载最新的扩展版本（`hugo_extended_0.5X_Linux-64bit.tar.gz`）。
3.  创建一个新目录：

        mkdir hugo

4.  将您下载的文件解压到 `hugo`。

5.  切换到新目录：

        cd hugo

6.  安装 Hugo:

        sudo install hugo /usr/bin

#### 苹果系统

使用 [Brew](https://gohugo.io/getting-started/installing/#homebrew-macos) 安装 Hugo。

#### 作为一个 `npm` 模块

您可以使用 [`hugo-bin`](https://www.npmjs.com/package/hugo-bin) 将 Hugo 安装为 `npm` 模块。 这会将 `hugo-bin` 添加到您的 `node_modules` 文件夹并将依赖项添加到您的 `package.json` 文件中。 要安装 Hugo 的扩展版本：

```
npm install hugo-extended --save-dev
```

有关使用详细信息，请参阅 [`hugo-bin` 文档](https://www.npmjs.com/package/hugo-bin)。

### 安装 PostCSS

要构建或更新站点的 CSS 资源，您还需要 [`PostCSS`](https://postcss.org/) 来创建最终资产。 如果您需要安装它，您必须在您的机器上安装最新版本的 [NodeJS](https://nodejs.org/en/)，以便您可以使用 Node 包管理器 `npm`。 默认情况下，`npm` 会在你运行的目录下安装工具 [`npm install`](https://docs.npmjs.com/cli/v6/commands/npm-install#description)：

```
sudo npm install -D autoprefixer
sudo npm install -D postcss-cli
```

从[`postcss-cli`的第8版](https://github.com/postcss/postcss-cli/blob/master/CHANGELOG.md)开始，你还必须单独安装`postcss`：

```
sudo npm install -D postcss
```

请注意，如果 [globally](https://flaviocopes.com/npm-packages-local-global/) 安装，5.0.1 以后的 `PostCSS` 版本将不会加载 `autoprefixer`，您必须使用本地安装。

## 使用主题

要使用 Docsy Hugo 主题，您有两个选择：

- **复制和编辑 [Docsy 示例站点](https://github.com/google/docsy-example) 的源代码。** 这种方法为您的站点提供了一个框架结构，包括顶层和文档您可以根据需要修改的部分和模板。示例站点使用 Docsy 作为 [Git 子模块](https://git-scm.com/book/en/v2/Git-Tools-Submodules)，因此很容易[保持最新](/docs/updating/)。
- **使用 Docsy 主题构建您自己的网站。** 像任何其他 [Hugo 主题](https://gohugo.io/themes) 一样指定 [Docsy 主题](https://github.com/google/docsy) /) 创建或更新您的网站时。使用此选项，您将获得 Docsy 外观、导航和其他功能，但您需要指定自己的站点结构。

### 选项 1：复制 Docsy 示例站点

[示例站点](https://example.docsy.dev) 为您提供了构建文档站点的良好起点，并且是
预先配置为使用 Docsy 主题作为 Git 子模块。 您可以通过以下方式复制示例站点：

- [使用 GitHub 用户界面](#using-the-github-ui)
- [使用命令行](#using-the-command-line)

#### 使用 GitHub 用户界面

这是最简单的方法，因为 Docsy 示例站点 repo 是一个 [模板存储库](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/)。 要创建您自己的 Docsy 示例站点存储库副本：

1. 进入【repo page】(https://github.com/google/docsy-example)，点击**Use this template**。

1. 在 **Repository name** 字段中输入您为新存储库选择的名称。 您还可以添加可选的 **Description**。

1. 单击**从模板创建存储库** 以创建您的新存储库。 恭喜，您现在拥有一个 Docsy 站点存储库！

1. 要使用 Hugo 在本地测试您复制的站点，或进行本地编辑，您还需要制作新存储库的本地副本。 为此，请使用 `git clone`，将 `https://github.com/my/example.git` 替换为你的 repo 的网址（不要忘记使用 `--recurse-submodules` 否则你不会 拉下生成工作站点所需的一些代码）：


<pre>
git clone --recurse-submodules --depth 1 <em>https://github.com/my/example.git</em>
</pre>

您现在可以编辑站点源文件的本地版本。 要预览您的站点，请转到站点根目录并运行 `hugo server`（[查看 MacOS 上的已知问题](#known-issues)）。 默认情况下，您的站点将在 http://localhost:1313/ 上可用。 要将更改推送到新存储库，请转到站点根目录并使用 `git push`。

#### 使用命令行

要复制示例站点：

1. 直接使用`git clone`制作示例站点的本地工作副本：

        git clone https://github.com/google/docsy-example.git

1.  切换到克隆项目的根目录，例如：

        cd docsy-example

1.  获取项目子模块的本地副本，以便您可以在本地构建和运行您的站点：

        git submodule update --init --recursive

1.  建立您的网站：

        hugo server

1. 在浏览器中预览您的站点：http://localhost:1313/。 您可以随时使用`Ctrl + c` 来停止 Hugo 服务器。
     [查看 MacOS 上的已知问题](#known-issues)。

1. 现在您有一个站点正在运行，您可以将其推送到一个新的存储库：

     1. [在GitHub中新建仓库](https://help.github.com/en/articles/create-a-repo)
         使用您选择的回购名称为您的网站。 为清楚起见，您可能还想重命名根
         要匹配的工作副本的目录（`docsy-example`），尽管一切仍然
         即使你不工作也能工作。

     1. 配置
         [`origin`](https://help.github.com/en/articles/configuring-a-remote-for-a-fork) 在你的项目中。 从您站点的根目录中，将 `origin` 的 URL 设置为您的新存储库（否则您将尝试将更改推送到 `google/docsy` 而不是您的存储库）：

              git remote set-url origin https://github.com/MY-SITE/EXAMPLE.git

    1.  通过运行以下命令验证您的遥控器是否配置正确：

             git remote -v

    1.  将您的 Docsy 站点推送到您的存储库：

             git push -u origin master

### 选项 2：在您自己的站点中使用 Docsy 主题

在创建或更新您的网站时，像任何其他 Hugo 主题一样指定 [Docsy 主题](https://github.com/google/docsy)。这为您提供了所有主题的优点，但您需要指定自己的站点结构。您可以将主题用作子模块（我们推荐的用于轻松更新的方法），也可以将主题克隆到项目的“themes”子目录中。

无论您使用哪种方法，为简单起见，我们建议您为您的项目复制和编辑我们的[示例站点配置](#basic-site-configuration)，否则在您尝试构建站点时可能会因缺少参数和值而出现 Hugo 错误。

#### 使用 Docsy 主题作为子模块

将 Docsy 添加为 Git 子模块是我们推荐的使用主题的方法，因为这意味着您的项目
总是在您选择的修订版中引用 Docsy 存储库版本，而不是您拥有自己的副本
当您尝试更新它时，您的存储库可能会导致合并冲突。这是我们使用的方法
[示例项目](https://github.com/google/docsy-example)。

要创建新的 Hugo 站点项目，然后将 Docs 主题添加为子模块，请从项目的根目录运行以下命令。

```shell
hugo new site myproject
cd myproject
git init
git submodule add https://github.com/google/docsy.git themes/docsy
echo 'theme = "docsy"' >> config.toml
git submodule update --init --recursive
```

要将 Docsy 主题添加到现有站点，请从项目的根目录运行以下命令：

```
git submodule add https://github.com/google/docsy.git themes/docsy
echo 'theme = "docsy"' >> config.toml
git submodule update --init --recursive
```

#### 将 Docsy 主题克隆到项目的`themes` 子目录中

如果您不想使用子模块（例如，如果您想直接自定义和维护您自己的主题副本，或者您的部署选择要求您在存储库中包含该主题的副本），您可以克隆 将主题添加到您的项目中。

要将 Docsy 克隆到项目的“theme”文件夹中，请从项目的根目录运行以下命令：

```
cd themes
git clone https://github.com/google/docsy
```

如果您想[本地](/docs/deployment/#serving-your-site-locally) 构建和/或服务您的站点，您还需要获取主题自己子模块的本地副本：

```
git submodule update --init --recursive
```

有关更多信息，请参阅 [Hugo](https://gohugo.io) 站点上的 [主题组件](https://gohugo.io/hugo-modules/theme-components/)。

#### 预览您的网站

要在本地构建和预览您的站点：

```
cd myproject
hugo server
```

默认情况下，您的站点将在 http://localhost:1313/ 上可用。 [查看 MacOS 上的已知问题](#known-issues)。

## 基本站点配置

站点范围的配置详细信息和参数在项目的 `config.toml` 文件中定义。其中包括您选择的 Hugo 主题（当然是 Docsy！）、项目名称、社区链接、Google Analytics 配置和 Markdown 解析器参数。有关如何添加此信息，请参阅示例项目中 [`config.toml` 中的注释示例](https://github.com/google/docsy-example/blob/master/config.toml)。 **我们建议复制这个 `config.toml` 并编辑它，即使你只是使用主题而不是复制整个 Docsy 示例站点**。

Docsy 示例站点带有一些您可能希望立即删除或自定义的默认值：

### 国际化

Docsy 示例站点支持英语、挪威语和波斯语内容。您可以在 [多语言支持](/docs/language/) 中了解有关 Docsy 如何支持多语言内容的更多信息。

如果您不打算翻译您的网站，您可以通过从 `config.toml` 中删除以下几行来删除语言切换器：

```
[languages.no]
title = "Docsy"
description = "Docsy er operativsystem for skyen"
languageName ="Norsk"
contentDir = "content/no"
time_format_default = "02.01.2006"
time_format_blog = "02.01.2006"

[languages.fa]
title = "اسناد گلدی"
description = "یک نمونه برای پوسته داکسی"
languageName ="فارسی"
contentDir = "content/fa"
time_format_default = "2006.01.02"
time_format_blog = "2006.01.02"
```

要删除已翻译的源文件，请同时删除 `docsy-example/content/no` 和 `docsy-example/content/fa` 目录。

### 搜索

默认情况下，Docsy 示例站点使用自己的 [Google 自定义搜索引擎](https://cse.google.com/cse/all)。 要禁用此站点搜索，请删除或注释掉以下几行：

```
# Google Custom Search Engine ID. Remove or comment out to disable search.
gcs_engine_id = "011737558837375720776:fsdu1nryfng"
```

要使用您自己的自定义搜索引擎，请将 `gcs_engine_id` 中的值替换为您自己的搜索引擎的 ID。 或者[选择另一个搜索选项](/docs/adding-content/navigation/#site-search-options)。

## 已知的问题

### 苹果系统

#### 错误：`太多打开的文件` 或`致命错误：管道失败`

默认情况下，MacOS 允许少量打开的文件描述符。 对于较大的站点，或者当您同时运行多个应用程序时，
当您运行 [`hugo server`](https://gohugo.io/commands/hugo_server/) 在本地预览您的站点时，您可能会收到以下错误之一：

- POSTCSS v7 及更早版本：

  ```
  ERROR 2020/04/14 12:37:16 Error: listen tcp 127.0.0.1:1313: socket: too many open files
  ```

- POSTCSS v8 及更高版本：

  ```
  fatal error: pipe failed
  ```

##### 解决办法

暂时允许更多打开的文件：

1. 通过运行查看您当前的设置：

   ```
   sudo launchctl limit maxfiles
   ```

2. 通过运行以下命令将限制增加到`65535` 个文件。 如果您的站点文件较少，您可以设置选择设置较低的软（`65535`）和硬（`200000`）限制。

   ```shell
   sudo launchctl limit maxfiles 65535 200000
   ulimit -n 65535
   sudo sysctl -w kern.maxfiles=200000
   sudo sysctl -w kern.maxfilesperproc=65535
   ```

请注意，您可能需要为每个新 shell 设置这些限制。
[详细了解这些限制以及如何使它们永久化](https://www.google.com/search?q=mac+os+launchctl+limit+maxfiles+site%3Aapple.stackexchange.com&oq=mac+os+launchctl+limit+maxfiles+site%3Aapple.stackexchange.com)。

### Windows 子系统 Linux (WSL)

如果您使用 WSL，请确保您在文件系统的 Linux 安装上运行 `hugo`，而不是 Windows 安装，否则您可能会遇到意外错误。

## 下一步是什么？

- [添加内容并自定义您的网站](/docs/adding-content/)
- 从我们的 [示例站点](https://github.com/google/docsy-example) 和其他 [示例](/docs/examples/) 中获取一些想法。
- [发布您的网站](/docs/deployment/)。
