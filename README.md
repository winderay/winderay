# termux&github pages

--------
# termux和github pages设置学习记录

## 一、termux安装与配置

1.酷安商店下载安装，备选f-droid

2.安装好后，打开。

3.输入命令，更新软件源与升级

	``apt update
	apt upgrede
	apt update
	apt upgrede``

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

2.配置ssh生成密钥
首先检查SSH KEY

`	cd ~/.ssh
	ls`

若是已有密钥，备份并建立新的密钥

`	mkdir key_backup
	cp id_rsa* key_backup
	rm id_rsa*`
生成新密钥

`	ssh-keygen -t rsa -C "email"`

一直回车，然后复制公钥id\_rsa.pub

`	cat id_rsa.pub`

使用cat命令，方便手机端复制公钥。

3.添加SSH Key到github


