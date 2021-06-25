---
layout: post
title: "使用Jekyll部署Github Pages"
date: 2021-06-25 19:18:02 +0800
categories: ["jekyll","github pages"]
tags: ["blog"]
---
#  安装Ruby

推荐使用`Ruby Version Manager(RVM)`管理`Ruby`

```bash
# 安装GPG keys
gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
# 安装RVM
curl -sSL https://get.rvm.io | bash -s stable
# 安装Ruby，推荐安装2.7版本，试了最新的3.0版本对Jekyll支持不好，启动不了
rvm install 2.7
# 使用Ruby 2.7
rvm use 2.7
```

*使用`RVM`的时候需要将`Terminal`的`Command`选项卡中的`Run command as a login shell`勾选上*

# 安装Jekyll

```bash
# 安装jekyll
gem install jekyll bundle
# 创建一个博客文件夹，jekyll new . 安装到当前目录，如果当前目录非空则使用jekyll new . --force
jekyll new myblog
# 启动界面
jekyll serve
```

# 使用主题

按照上面的步骤已经可以获取一个基本的博客服务器了，但是界面很丑，我们可以去[官网](http://jekyllthemes.org/)上挑一下自己喜欢的主题，这里我选择了[Chiryp](http://jekyllthemes.org/themes/jekyll-theme-chirpy/)主题。

首先把这个代码克隆到本地并切换到一个稳定版的`tag`(当前最新的是4.0.2)，按照使用说明执行一下步骤

```bash
# 克隆代码到本地的korov.github.io文件夹
git clone git@github.com:cotes2020/jekyll-theme-chirpy.git korov.github.io
# 进入文件夹，并将v4.0.2这个稳定版的tag切出来
cd korov.github.io
git switch -c tag-v4.0.2 v4.0.2
# 安装依赖
bundle
bash tools/init.sh
# 启动，需要确保ruby版本是2.7版本
jekyll server
```

# 部署到Github

修改部署配置，将`.github/workflows/pages-deploy.yml`中的`on.push.branches`设置为自己的推送分支，例如我的就是`main`分支

在github上创建一个仓库，仓库的名字例如`korov.github.io`，需要你用自己的名字作为前缀。

```bash
# 将之前别人的远端切换为自己的
git remote remove origin
git remote add origin git@github.com:Korov/korov.github.io.git
git fetch origin
git switch -c main
git push origin main
git branch -u origin/main
```

完成上面的操作之后你的本地代码已经部署到你的github仓库上面了，接下需要进行如下操作，github界面上进入仓库，`Settings → Options → GitHub Pages`，然后将`Source`的`branch`设置为`gh-pages`。就可以访问自己的[页面](https://korov.github.io/)了

# 常用命令

重新生成：`jekyll build`

