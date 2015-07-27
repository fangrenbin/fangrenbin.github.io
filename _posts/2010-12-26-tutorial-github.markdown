---
author: fangrenbin
comments: true
date: 2010-12-26 13:33:30+00:00
layout: post
slug: tutorial-github
title: github快速体验git
wordpress_id: 239
categories:
- git
tag:
- git
- github
---

学习c也有一段时间了，写了一堆练习用的代码，放在硬盘里乱糟糟的。虽然代码也没有什么实质性的用处，但是我还是想把它们好好管理一下，以前见过一些网友用google code，来管理自己的项目。但是，我刚开始问了一个网友，他给我荐了一个更好的东西，就是git还给了我一本书，叫我自己研究。
最近，由于各种原因没能好好研究，今天总算有时间来研究一下。

本文也只是参考那本书来作的。书的地址：http://progit.org/book/

关于git的优点，在这里不多写，书里面写的很清楚，在这里我只是记录一下我安装http://frb.name/wp-admin/post.php?post=239&action=edit&message=10过程，以及安装的时候遇到的一些问题，由于我也是刚开始研究，对很多问题都不是特别的清楚，如果有什么错误的地方，希望看到的朋友给予指正。

<!-- more -->

我的环境：

ＯＳ：ubuntu 10.04

<!-- more -->

一、安装git：

由于我使用的是ubuntu，安装就比较方便了。

使用apt-get，就可以顺利安装。

$ sudo apt-get install git-core

更多系统安装方法见：[http://progit.org/book/zh/ch1-4.html](http://progit.org/book/zh/ch1-4.html)

安装好了以后进行一些简单的设置：

设置用户信息：

git config --global user.name "fangrenbin"

git config --global user.email fangrenbin@gmail.com

设置编辑器：

git config --global core.editor emacs

查看配置信息：git config --list

$ git config --list
user.name=fangrenbin
user.email=fangrenbin@gmail.com
user.mail=fangrenbin@gmail.com
core.editor=emacs
merge.tool=vimdiff

获取帮助：

$ git help <verb>

比如config命令：$git help config

目前关于git的设置就先到这里，更多更详细的用法，还是参考那本书。

<!-- more -->

二、注册github.com

登陆：[https://github.com/](https://github.com/)，点击Plans, Pricing and Signup。选择Free for open source　这项后面的 Create a free account。

填写完注册信息后就可以登陆。

<!-- more -->

三、ssh公钥（生成，以及添加）

有了帐号以后还需要SSH公钥才能够提交代码。

１、SSH公钥生成

$ ssh-keygen

如果一切顺利的话，大概会出现下面这个图像：

[![](http://frb.name/wp-content/uploads/2010/12/ssh-keygen-300x216.png)](http://frb.name/wp-content/uploads/2010/12/ssh-keygen.png)

２、添加SSH公钥

在添加之前我们需要查看一下具体生成的公钥，用cat就好了。

$ cat ~/.ssh/id_rsa.pub


[![](http://frb.name/wp-content/uploads/2010/12/cat-ssh.png)](http://frb.name/wp-content/uploads/2010/12/cat-ssh.png)


然后开始添加SSH公钥：


[![](http://frb.name/wp-content/uploads/2010/12/ssh-set.png)](http://frb.name/wp-content/uploads/2010/12/ssh-set.png)


点击添加新的公钥：标题随便输，然后把刚才的公钥复制到“公钥”。

此时公钥就添加成功了。

然后测试一下：

$ ssh git@github.com

fangrenbin@fangrenbin-laptop:~$ ssh git@github.com
PTY allocation request failed on channel 0
Hi fangrenbin! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
如果出现这样的情况，那说明就成功了。

如果不成功的话请参考：[](http://help.github.com/troubleshooting-ssh/)

[http://help.github.com/troubleshooting-ssh/](http://help.github.com/troubleshooting-ssh/)

[http://help.github.com/linux-key-setup/](http://help.github.com/linux-key-setup/)

我刚开始也验证不成功，搞了我好长时间才搞好。多参考一下。后面又发现了GitHub token config　这一项没有设置，又设置了一下。最后搞的总算测试成功了。

<!-- more -->

四、创建仓库[ Create a Repository](https://github.com/repositories/new)

创建仓库：

项目名称之类的自己添好自己想要添的名称。


[![](http://frb.name/wp-content/uploads/2010/12/create-repositories.png)](http://frb.name/wp-content/uploads/2010/12/create-repositories.png)


很快一个仓库就创建好了。然后就可以上传你的项目了。

<!-- more -->

五、上传项目

由于我自己也没有什么项目，我就把我自己平常练习写的一些代码传上去了，记录自己写的程序还是很不错地。虽然，大部分代码都是从书上搞的。

当创建一个仓库，初次打开仓库，未上传过东西的时候，他就会有操作提示。

像这个：


Global setup:




Download and install Git
git config --global user.name "fangrenbin"
git config --global user.email fangrenbin@gmail.com




Next steps:
mkdir the_c_code
cd the_c_code
git init
touch README
git add README
git commit -m 'first commit'
git remote add origin git@github.com:fangrenbin/the_c_code.git
git push origin master
Existing Git Repo?
cd existing_git_repo
git remote add origin git@github.com:fangrenbin/the_c_code.git
git push origin master


这段命令打下来，就可以传代码了。


[![](http://frb.name/wp-content/uploads/2010/12/git-view.png)](http://frb.name/wp-content/uploads/2010/12/git-view.png)
