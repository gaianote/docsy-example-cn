---
title: "Docker 快速开始"
linkTitle: "Docker 快速开始"
weight: 3
date: 2018-07-30
description: >
  此页面可帮助您在 5 分钟内使用 Docker 设置和运行本地 Docsy 站点。
---

## 安装先决条件

1. 在 Mac 和 Windows 上，下载并安装[Docker 桌面](https://www.docker.com/get-started)。 在 Linux 上，安装 [Docker 引擎](https://docs.docker.com/engine/install/#server) 和 [Docker 撰写](https://docs.docker.com/compose/install/)。安装可能需要您重新启动计算机以更改生效。
1. [安装 git](https://github.com/git-guides/install-git)。

## 从 docsy-example 模板创建您的存储库

docsy-example 存储库提供了您可以使用的基本站点结构作为创建自己的文档的起点。

1.使用[docsy-example 模板](https://github.com/google/docsy-example)
[创建您自己的存储库]（https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template）。

1. 通过[克隆你新创建的存储库](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository)

1. 将您的工作目录更改为新创建的文件夹：

   ```bash
   cd docsy-example
   ```

## 构建并运行容器

docsy-example 存储库包括一个[Dockerfile](https://docs.docker.com/engine/reference/builder/) 你可以用于运行您的网站。

1. 构建 docker 镜像：

   ```bash
   docker-compose build
   ```

1. 运行构建的镜像：

   ```bash
   docker-compose up
   ```

1. 在浏览器中打开地址 `http://localhost:1313` 加载 docsy-example 主页。 您现在可以更改源文件，那些更改将实时重新加载到您的浏览器中。

## 清理

要清理系统并删除容器映像，请按照以下步骤操作。

1. 使用 **Ctrl + C** 停止 Docker Compose。

1.删除生成的图像

```bash
docker-compose rm
```

## 下一步是什么？

- 了解 [Docsy 的基本设置和配置](/docs/getting-started/)。
- [添加内容并自定义您的网站](/docs/adding-content/)
- [发布您的网站](/docs/deployment/)。
