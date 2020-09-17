---
layout: post
title: "Github Pages & Jekyll"
author: "yuruj"
catelog: true
header-style: text
tags:
  - Git
  - 学习笔记
---

# GitHub Pages使用入门

## 关于GitHub Pages

### 关于GitHub Pages

GitHub Pages是一项静态站点托管服务，他直接从GitHub上的仓库获取HTML、CSS和JavaScript文件，（可选）通过构建过程运行文件，然后发布网站

你可以在GitHub的`github.io`域或自己的自定义域上托管站点

### GitHub Pages站点的类型

项目站点：连接到GitHub上托管的特定项目

用户站点：必须创建名为 `<user>.github.io` 的用户帐户所拥有的仓库

组织站点：必须创建名为 `<organization>.github.io` 的组织所拥有的仓库

除非您使用自定义域，否则用户和组织站点位于 `http(s)://<username>.github.io` 或 `http(s)://<organization>.github.io`

只能为每个GitHub账号创建一个用户或组织站点

### GitHub Pages站点的发布来源

GitHub Pages站点将成为互联网上的公开内容，即使其仓库是私有的或内部的。如果站点的仓库中有敏感数据，您可能想要在发布前删除它

### 静态站点生成器

GitHub Pages 会发布您推送到仓库的任何静态文件。 您可以创建自己的静态文件或使用静态站点生成器为您构建站点。 您还可以在本地或其他服务器上自定义自己的构建过程。 我们建议使用 Jekyll，它是一个静态站点生成器，内置 GitHub Pages 支持和简化的构建流程

默认情况下，GitHub Pages 将使用 Jekyll 来构建您的站点。 如果您想使用除 Jekyll 以外的静态站点生成器，通过在发布来源的根目录中创建一个名为 `.nojekyll` 的空文件来禁用 Jekyll 构建过程，然后按照静态站点生成器的说明在 本地构建站点。

GitHub Pages 不支持服务器端语言，例如 PHP、Ruby 或 Python

### 使用GitHub Pages的指南

2016年6月15日后创建并使用github.io域的GitHub Pages站点通过HTTPS提供服务

使用限制：

- GitHub Pages 源仓库建议的限制为 1GB
- 发布的 GitHub Pages 站点不得超过 1 GB
- GitHub Pages 站点的*软*带宽限制为每月 100GB
- GitHub Pages 站点的*软*限制为每小时 10 次构建

如果您的站点超出这些使用配额，我们可能无法为您的站点提供服务

### GitHub Pages上的MIME类型

MIME类型是服务器发送到浏览器的标头，提供有关浏览器所请求文件性质和格式的信息

GitHub Pages 支持数千种文件扩展名中 750 多种 MIME 类型。虽然无法基于每个文件或每个仓库指定自定义 MIME 类型，但您可以添加或修改 MIME 类型以在 GitHub Pages 上使用

## 创建GitHub Pages站点

### 为站点创建仓库

1、在任何页面的右上角，使用 下拉菜单选择 **New repository（新建仓库）**

2、使用 **Owner（所有者）**下拉菜单选择你想要拥有仓库的帐户

3、输入仓库的名称和说明（可选）。 如果您创建的是用户或组织站点，仓库名称必须为 `<user>.github.io` 或 `<organization>.github.io`

4、Choose a repository visibility

5、选择选择 **Initialize this repository with a README（使用自述文件初始化此仓库）**

6、Click Create repository

### 创建站点

1、在GitHub上，导航到站点的仓库

2、Decide which publishing source you want to use

3、如果所选发布源已经存在，请导航到发布源。如果所选发布源不存在，则创建发布源

4、在发布源的根目录中，创建一个名为index.md、包含要在网站主页上显示的内容的文件

5、Configure your publishing source

6、在仓库名称下，单击Settings

7、要查看您已发布的站点，请在“GitHub Pages”下点击您的站点 URL

对站点的更改在推送到GitHub上，最长可能需要20分钟才会发布

### 后续步骤

可以通过创建更多新文件向网站添加更多页面。每个文件都将在网站上与发布源相同的目录结构中。例如，例如，如果项目网站的发布源是 `gh-pages` 分支，并且您在 `gh-pages` 分支上创建了名为 `/about/contact-us.md` 的新文件，该文件将在 `https://<user>.github.io/<repository>/about/contact-us.md` 下

还可以添加主题以自定义网站的外观

要更多地自定义您的站点，你可以使用Jekyl-内置GitHub Pages支持的静态站点生成器

## 使用主题选择器将主题添加到GitHub Pages站点

拥有仓库管理员权限的人可以使用主题选择器向GitHub Pages站点添加主题

### 关于主题选择器

主题选择器可用于向仓库添加 Jekyll 主题

主题选择器如何工作取决于您的资源库是公共的还是私有的

- 如果已为仓库启用 GitHub Pages，主题选择器会将主题添加到当前发布源
- 如果您的仓库是公共的，并且已对仓库禁用 GitHub Pages，则必须先通过配置发布源来启用 GitHub Pages，然后才可使用主题选择器

如果以前曾手动向仓库添加 Jekyll 主题，则这些文件在使用主题选择器后也可能应用。 为避免冲突，请先删除所有手动添加的主题文件夹和文件，然后再使用主题选择器。

### 使用主题选择器添加主题

1、在GitHub上，导航到站点的仓库

2、在仓库名称下，单击Settings

3、在GitHub Pages下，单击Choose a theme或Change theme

4、在页面顶部单击所需的主题，然后单击Select theme（选择主题）

5、系统可能会提示您编辑站点的README.md文件

您选择的主题将自动应用到仓库中的MarkDown文件。要将主题应用到仓库中的HTML文件，您需要添加YAML前页，以指定每个文件的布局

## 配置GitHub Pages站点的发布源

如果您使用GitHub Pages站点的默认发布源，您的站点将自动发布

You can also choose to publish your site from a different branch or folder

People with admin or maintainer permissions for a repository can configure a publishing source for a GitHub Pages site

### 选择发布源

Before you configure a publishing source, make sure the branch you want to use as your publishing source already exists in your repository

1、在GitHub上，导航到站点的仓库

2、在仓库名称下，单击Settings

3、Under "GitHub Pages", use the **None** or **Branch** drop-down menu and select a publishing source

4、Optionally, use the drop-down menu to select a folder for your publishing source

5、单击Save

### GitHub Pages站点发布问题疑难排解

If your site has not published automatically, make sure someone with admin permissions and a verified email address has pushed to the publishing source

f you choose the `docs` folder on any branch as your publishing source, then later remove the `/docs` folder from that branch in your repository, your site won't build and you'll get a page build error message for a missing `/docs` folder

## 为GitHub Pages站点创建自定义404界面

可以自定义在人们尝试访问站点上不存在的页面时显示的404错误页面

1、在Github上，导航到站点的仓库

2、导航到站点的发布来源

3、Above the list of files, using the Add file drop-down, click Create new file

4、在文件名字段中，键入404.html或404.md

5、如果将文件命名为404.md，请将以下YAML前页添加到文件的开头

```text
---
permalink: /404.html
---
```

6、在YAML前页（如果存在）下方添加要在404页面上显示的内容

7、在页面底部，输入一条简短、有意义的提交信息，描述您对文件所做的更改。您可以在提交消息中将提交归于多个作者

8、以下是提交消息字段，请单击电子邮件地址下拉菜单并选择 Git 作者电子邮件地址。 只有经过验证的电子邮件地址才会出现在此下拉菜单中。 如果您启用了电子邮件地址隐私保护，则 `<username>@users.noreply.github.com` 为默认的提交作者电子邮件地址

9、在提交消息字段下面，确定是要将提交添加到当前分支还是新分支。 If your current branch is the default branch, you should choose to create a new branch for your commit and then create a pull request

10、单击Propose new file（提议新文件）

## 使用HTTPS保护GitHub Pages站点

HTTPS增加一层加密，用于防止其他人窥探或篡改您的站点的流量。您可对GitHub Pages站点强制实施HTTPS，从而将所有HTTPS请求透明的重定向到HTTPS

拥有仓库管理员权限的人可对GitHub Pages站点实施HTTPS

### 关于HTTPS和GitHub Pages

所有 GitHub Pages 站点（包括使用自定义域正确配置的站点）均支持 HTTPS 和 HTTPS 强制实施

对于使用 2016 年 1 月 15 日后创建的 `github.io` 域的 GitHub Pages 站点，需要强制实施 HTTPS。 如果您在 2016 年 6 月 15 日之前创建了站点，则可以手动启用实施 HTTPS

GitHub Pages 站点不应该用于敏感事务，例如发送密码或信用卡号码

### 对您的GitHub Pages站点强制实施HTTPS

1、在GitHub上，导航到站点的仓库

2、在仓库名称下，单击Settings

3、在GitHub Pages下，选择Enforce HTTPS（实施HTTPS）

### 解决具有混合内容的问题

如果您对 GitHub Pages 站点启用了 HTTPS，但站点的 HTML 仍通过 HTTP 引用图像、CSS 或 JavaScript，则您的站点将提供*混合内容*。 提供混合内容可能会降低站点的安全性，并导致在加载资产时出现问题

要删除站点的混合内容，请在站点的 HTML 中将 `http://` 更改为 `https://`，确保所有资产都通过 HTTPS 提供

资产通常位于以下位置：

- 如果您的站点使用 Jekyll，则 HTML 文件可能位于 *_layouts* 文件夹中
- CSS 通常位于 HTML 文件的 `<head>` 部分
- JavaScript 通常位于 `<head>` 部分或结束 `</body>` 标记之前
- 图像通常位于 `<body>` 部分

![](/img/typora-user-images/截屏2020-09-06 下午4.24.28.png)

## 将子模块用于GitHub Pages

如果 GitHub Pages 站点的仓库包含子模块，则在构建站点时会自动拉取其内容

只能使用指向公共仓库的子模块，因为 GitHub Pages 服务器无法访问私有仓库

对子模块（包括嵌套子模块）使用 `https://` 只读 URL。 您可以在 *.gitmodules* 文件中进行此更改

## 取消发布GitHub Pages站点

1、在GitHub上，导航到仓库的主页面

2、在仓库名称下，单击Settings

3、Under GitHub Pages, use the Branch drop-down menu and select None

4、如果为站点启用了自定义域，为避免域名被占用，请更新您的DNS设置

# 使用Jekyll设置GitHub Pages站点

## 关于GitHub Pages和Jekyll

### 关于Jekyll

Jekyll是一个静态站点生成器，内置GitHub Pages支持和简化的构建过程

Jekyll使用Markdown和HTML文件，并根据您选择的布局创建完整静态网站。Jekyll支持Markdown和Lick，这是一种可在网站上加载动态内容的模版语言

Windows并未正式支持Jekyll

我们建议将Jekyll用于GitHub Pages。如果您喜欢，可以使用其他静态站点生成器或者在本地或其他服务器上自定义构建过程

### 在GitHub Pages网站中配置Jekyll

可以通过编辑_config.yml文件来配置大多数Jekyll设置，例如网站的主题和插件

![](/img/typora-user-images/截屏2020-09-08 下午9.09.10.png)

![](/img/typora-user-images/截屏2020-09-08 下午9.09.59.png)

### 前页附属资料

要为网站上的页面或帖子设置变量和原数据，例如标题和布局，可以讲YAML前页添加到任意MarkDown或HTML文件的顶部

可以添加site.github到帖子或页面，以将任何仓库引用元数据添加到您的网站

### 主题

您可以将Jekyll主题添加到GitHub Pages站点，以自定义站点的外观

您可以在GitHub上添加支持的主题到站点

要使用GitHub上托管的任何其他开源Jekyll主题，您可以手动添加主题

您可以通过编辑主题文件来覆盖任何主题的默认值

### 插件

可以下载或创建Jekyll插件，以便为您的网站拓展Jekyll的功能

例如， [jemoji](https://github.com/jekyll/jemoji) 插件允许您在站点的任何页面上使用 GitHub 风格的表情符号，就像在 GitHub 上使用一样

![](/img/typora-user-images/截屏2020-09-09 上午9.44.39.png)

可以通过在_config.yml文件中添加插件的gem到`plugins`设置来启用额外的插件

GitHub Pages无法使用不支持的插件构建网站。如果想使用不支持的插件，请在本地生成网站，然后将网站的静态文件推送到GitHub

### 语法突显

为了使网站更容易读取，代码片段在GitHub Pages上突显，就像在GitHub上突显一样

![](/img/typora-user-images/截屏2020-09-09 上午9.52.32.png)

### 本地构建网站

当更改合并到站点的发布源时，对站点的更改将自动发布。如果想先预览您的更改，可以在本地而不是GitHub上进行更改，然后在本地测试站点

## 使用Jekyll创建GitHub Pages站点（Mac）

可以使用Jekyll在新仓库或现有仓库中创建GiHub Pages站点

拥有仓库管理员权限的人员可以使用Jekyll创建GitHub Pages站点

### 基本要求

必须安装Jekyll和Git后才可使用Jekyll创建GitHub Pages站点

建议使用Bundler安装和运行Jekyll。Bunder可管理Ruby gem依赖项，减少Jekyll构建错误和组织环境相关的漏洞

[Jekyll的安装](https://jekyllrb.com/docs/installation/)

Jekyll是可以在大多数系统上安装的Ruby Gem

Ruby是一种跨平台、面向对象的动态类型编程语言。

### 为站点创建仓库

### 创建站点

# Jekyll 官方文档

Jekyll是静态站点生成器。它采用您喜欢的标记语言编写的文本，并使用布局创建静态网站。您可以调整网站的外观，URL，页面上显示的数据等。

## Ruby 101

Jekyll用Ruby编写

### Gem

Gem是包含在Ruby项目中的代码。Gem包装的特定功能。您可以在多个项目中或与他人共享宝石。宝石可以执行以下操作：

* 将Ruby对象转换为JSON
* 分页
* 与GitHub等API交互

Jekyll是一个Gem，许多Jekyll插件也是Gem

### Gemfile

网站使用的Gem列表。每个Jekyll站点的主文件夹中都有一个Gemfile

### Bundler

Bundler是一种宝石，可在您的电脑上安装所有gems in your Gemfile

While you don’t have to use `Gemfile` and `bundler`, it is highly recommended as it ensures you’re running the same version of Jekyll and its plugins across different environments.

Install Bundler using `gem install bundler`. You only need to install it once, not every time you create a new Jekyll project.

要使用Bundler在Gemfile中安装gem，请在具有Gemfile的目录中运行以下命令：

```shell
bundle install
bundle exec jekyll serve
```

要在不使用Gemfile的情况下绕过Bundler，请运行`jekyll serve`

### Step by Step Tutorial

