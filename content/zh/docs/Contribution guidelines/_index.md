---
title: "贡献指南"
linkTitle: "贡献指南"
weight: 9
description: >
  如何为 Docsy 做贡献
---

Docsy 是一个开源项目，我们喜欢获得补丁和贡献，以使 Docsy 及其文档变得更好。

## 为 Docsy 做贡献

Docsy 主题本身位于 <https://github.com/google/docsy>。

### 贡献者许可协议

对该项目的贡献必须附有贡献者许可证
协议。您（或您的雇主）保留对您的贡献的版权；
这只是允许我们使用和重新分配您的贡献
项目的一部分。前往 <https://cla.developers.google.com/> 查看
您当前存档的协议或签署新协议。

你一般只需要提交一次 CLA，所以如果你已经提交了一个
（即使是针对不同的项目），您可能不需要这样做
再次。

### 代码审查

所有提交，包括项目成员提交的提交，都需要审查。我们
为此目的使用 GitHub 拉取请求。咨询
[GitHub 帮助](https://help.github.com/articles/about-pull-requests/) 了解更多
有关使用拉取请求的信息。

### 预览您的更改

由于 Docsy 是一个主题而不是站点，因此您无法直接提供主题来检查您的更改是否有效。而是在 Docsy 示例站点的本地副本中使用更新的本地主题（在`themes/docsy` 目录中复制或进行更改）并从那里 [预览](/docs/deployment/)。或者，克隆 [Docsy 主题存储库](https://github.com/google/docsy) 并在此站点的本地副本中测试您的更改，如下所述（#previewing-your-changes-locally）。

### 社区准则

该项目遵循
[Google 的开源社区准则](https://opensource.google.com/conduct/)。

### 创建问题

或者，如果您希望在 Docsy 中看到某些内容（或者如果您发现某些内容没有按照您期望的方式工作），但您不确定如何自己修复它，请创建一个 [问题]（https://github.com/google/docsy/issues）。

## 为这些文档做贡献

本用户指南与我们的示例站点一样，是一个使用 Hugo 静态站点生成器的 Docsy 站点。我们欢迎更新文档！

我们使用 [Netlify](https://www.netlify.com/) 来管理站点的部署并提供文档更新的预览。此处的说明假定您熟悉基本的 GitHub 工作流程。

### Netlify 快速入门

1. 在 GitHub 上分叉 [Docsy repo](https://github.com/google/docsy)：该站点的文件位于 `userguide` 子目录中。
1. 进行更改并发送拉取请求 (PR)。
1. 如果您还没有准备好进行审核，请在 PR 名称中添加“WIP”以表明
  这是一项正在进行的工作。 (**不要**添加 Hugo 属性
  “draft = true”到页面前端很重要，因为这可以防止
  下一点中描述的内容预览的自动部署。）
1. 等待自动化 PR 工作流程进行一些检查。准备好后，
  你应该会看到这样的评论：**deploy/netlify — Deploy preview ready！**
1.点击“Deploy preview ready”右侧的**Details**查看预览
  你的更新。
1. 继续更新您的文档并推送您的更改，直到您满意为止
  内容。
1. 当您准备好进行审核时，向 PR 添加评论，并删除任何评论
  “WIP”标记。

### 更新单个页面

如果您在使用文档时发现了想要更改的内容，Docsy 为您提供了一个快捷方式：

1. 点击页面右上角的**编辑此页面**。
1. 如果您还没有项目 repo 的最新 fork，系统会提示您获取一键 - 单击 **Fork this repository and proposal changes** 或 **Update your Fork** 以获取最新版本要编辑的项目的日期版本。分叉中的相应页面以编辑模式显示。
1. 按照上面的[使用 Netlify 快速入门](#quick-start-with-netlify) 流程的其余部分进行操作并预览您的更改。


### 在本地预览您的更改

如果您想运行自己的本地 Hugo 服务器以在工作时预览您的更改：

1. 按照[入门](/docs/getting-started) 中的说明安装 Hugo 和您需要的任何其他工具。
1. 将 [Docsy](https://github.com/google/docsy) 存储库分叉到您自己的项目中，然后使用 `git clone` 创建一个本地副本。不要忘记使用`--recurse-submodules`，否则您将无法下拉生成工作站点所需的一些代码。

    ```
    git clone --recurse-submodules --depth 1 https://github.com/google/docsy.git
    ```

1. 切换到`userguide`目录并运行以下Hugo命令来构建站点并启动Hugo服务器。
    请注意，您需要 `themesDir` 标志，因为站点文件位于主题存储库中。

    ```
    cd userguide
    hugo server --themesDir ../..
    ```
    
    默認情況下，您的站點將在 http://localhost:1313/ 上可用。現在您正在本地為您的站點提供服務，Hugo 將監視內容的更改並自動刷新您的站點。
   

1. 繼續使用通常的 GitHub 工作流程來編輯文件、提交文件、推送文件
  更改到您的分叉，並創建拉取請求。

### 創建問題

如果您想在文檔中看到某些內容，但不確定如何自行修復，請在 [此存儲庫](https://github.com/google/docsy) 中創建問題。您還可以通過單擊頁面右上角的 **Create Issue** 按鈕來創建有關特定頁面的問題。
