---
layout: post
title: "Intellij IDEA import project from WSL2"
date: 2021-08-12 21:36:02 +0800
categories: ["idea","java","wsl2"]
tags: ["tools"]
---

# 



# 背景

公司里的项目有自己的打包脚本，因为同事都是用的mac，所以用`bash`打包，但是我用的是Windows没办法打包，后来就想到用`WSL2`来打包，但是每次要打包的时候都要把最新的代码拷贝到`WSL2`中，然后把打包的结果复制回Windows，很麻烦。

后来发现新版本的IDEA可以打开`WSL2`中的项目，但是试了之后发现这速度太慢了，构建索引都要半小时左右，根本不可用，后来发现原因是因为Windows和`WSL2`互相访问文件极慢导致的，因此只要解决两个系统间的文件访问问题就可以了。

# 在WSL2中配置好开发环境

第一步安装好`git`,`maven`,`jdk`这三个必要的开发工具。

# IDEA中配置jdk和maven

打开IDEA设置 `SDKs`

![设置jdk](/assets/img/pictures/Snipaste_2021-08-12_21-57-13.png)

可以添加多个JDK，这样设置是因为用`WSL2`自己的jdk编译项目，不会产生跨系统的文件访问



设置`maven`

![设置maven](/assets/img/pictures/Snipaste_2021-08-12_22-01-38.png)

这里的`Maven home path`,`User settings`和`Local reposit`都必须设置为`WSL2`中的路径，这样加载依赖和用maven编译的时候都是在WSL中完成，不会发生跨系统的文件访问。



到这里就基本完成了，接下来就是导入项目就可以了。



# 总结

这里的解决思路就是将开发、编译等过程全部放到WSL中执行，这样就可以解决跨系统访问文件很慢的问题。亲自测了一下，在WSL系统下相同的项目编译速度提高了30%左右，还是很有效果的。
