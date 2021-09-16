---
title: "更新 Docsy"
linkTitle: "更新 Docsy"
weight: 8
description: >
 保持主题更新。
type: docs
---

我们希望继续改进主题[与 Docsy 社区一起](/docs/contribution-guidelines/)。
如果您已克隆示例站点（或以其他方式使用主题作为子模块），则可以更新 Docsy 主题
你自己。

更新 Docsy 意味着您的站点将在“HEAD”使用最新版本的 Docsy 构建并包括
自您最初添加 Docsy 的时间点以来已合并的所有新提交或更改
子模块，或上次更新。更新不会影响您在自己的项目中所做的任何修改
[覆盖 Docsy 外观](/docs/adding-content/lookandfeel/)，作为您的覆盖
不要修改主题本身。有关主题更改的详细信息，请参阅
[文档提交](https://github.com/google/docsy/commits/master)。

根据您选择使用 Docsy 的方式，按照相应的步骤更新主题：

## 更新一个 Docsy 子模块

如果您在项目中使用 Docsy 主题作为子模块（例如，如果您复制了我们的示例站点），则更新子模块：

1. 导航到本地项目的根目录，然后运行：

        git submodule update --remote

    
1. Add and then commit the change to your project:

        git add themes/
        git commit -m "Updating theme submodule"


1. Push the commit to your project repo. For example, run:

        git push origin master

    
## 更新您的 Docsy 克隆

如果您 [克隆 Docsy 主题](/docs/getting-started/#cloning-the-docsy-theme-to-your-projects-themes-subdirectory) 到
项目中的`themes` 文件夹，然后使用`git pull` 命令：

1. 导航到本地项目中的“themes”目录：

        cd themes

1.确保`origin`设置为`https://github.com/google/docsy.git`：

        git remote -v

1. 更新您的本地克隆：

        git pull origin master

如果您对克隆的主题进行了任何本地更改，则必须手动解决任何合并冲突。
