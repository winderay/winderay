---
layout: post
title: termux和github pages设置学习记
---
--------
# termux和github pages设置学习记录

## 一、termux安装与配置

1.酷安商店下载安装，备选f-droid

2.安装好后，打开。

3.输入命令，更新软件源与升级

`	apt update`
<!-- more -->
`	apt upgrade`

`	apt update`

`	apt upgrade`

4.移除表头简介文字

`	vi .hushlogin`

输入:wq保存退出

5.美化终端
安装ZSH的oh-my-zsh

`	apt install curl`

输入下列代码安装

`sh -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"`

默认设置一路enter

## 二、必备软件与配置

1.安装必备软件

`	apt install openssh git vim`

vim支持中文方法`vi ~/.vimrc`输入`set enc=uft8`然后:wq即可。

2.配置ssh生成密钥
首先检查SSH KEY

`	cd ~/.ssh`

`	ls`

若是已有密钥，备份并建立新的密钥

`	mkdir key_backup`

`	cp id_rsa* key_backup`

`	rm id_rsa*`

生成新密钥

`	ssh-keygen -t rsa -C "email"`

一直回车，然后复制公钥id\_rsa.pub

`	cat id_rsa.pub`

使用cat命令，方便手机端复制公钥。

3.添加SSH Key到github

* 首先要有github账号，没有的话，就先注册，然后登录。
* 点击右上角头像，点选击settings，左侧列表点击SSH
* 右侧点击添加新KEY
* 将复制的公钥粘贴到框内，确定。

4.配置终端git

在终端输入下列代码用于github验证

`	git config --global user.name “your_username”`

`	git config --global user.email “your_email”`

> 取消全局设置方法`git config --global --unset user.email`
> 添加config：` git config --local user.email "email"`

测试是否成功

`	ssh -T git@github.com`

输入`yes`链接成功

5.配置github与终端项目

在github创建`username.github.io`项目，默认配置就可以。

在终端新建库

`	mkdir usename`

`	cd ./username`

初始化git

`	git init`

6.clone项目

终端新建项目库

`	mkdir username.github.io`

`	cd ./username.github.io`

clone项目到本地，由于不同库有两种方式(此处的username为目标项目名字)：

`git clone git@github.com:username/username.github.io.git`

`git clone git@github.com:username/reponame.git`

修改本地项目后，准备推送到自己的github库

7.关联仓库与推送

在本地仓库执行下列命令

`git remote add origin git@github.com:username.github.io.git`

将本地库推送到远程库

`git push -u origin master`

> 把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
> 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
> 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改。

8.推送更新

`git add filename`

`git commit -m "备注"`

`git push origin filename`


