---

layout: post
title: 同一台电脑，多个Github账户的SSHkey切换

---

    一台电脑有一个SSH key，在连接github时，会设置为全局密钥，当再想链接第二个账户时就会出现错误。这时我们就需要学习如何设置多个密钥，链接不同的账户。
<!-- more -->
## 一、取消git全局设置并修改

第一次跟随教程设置会用到配置*全局用户名和邮箱*，如下代码

` git config --global user.name "自定义用户名"`

` git config --global user.email "邮箱"`

要想配置多个账户需要先取消全局配置。

` git config --global --unset user.name`

` git config --global --unset user.email`

此时就可以分别在不同的库，配置各自的用户名和邮箱，以下操作在
各自库文件下进行。

` git config --local user.name`

` git config --local user.email`

## 二、生成第一个or新的KEY

` ssh-keygen -t rsa -C "Your email"`

    一路回车就会在~/.ssh/生成一对公私密钥id_rsa.pub和id_rsa。
    但是如果已经生成过密钥就会要求命名新的密钥名字，例如输入new_rsa，一路回车就会生成名为new_rsa.pub和new_rsa的密钥。

    复制新的/两对密钥中的公钥（.pub结尾）内容。添加到github账号中去。

## 三、新建SSH配置文件

` cd ~/.ssh/`

` vim config`

输入下列内容

> Host github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa  
  
> Host xxx.github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/new_rsa

保存。

## 四、测试配置是否正确

` ssh -T git@github.com`

` ssh -T git@xxx.github.com`

    若是分别返回Hi [不同名字]!You've successfully authenticated，则说明配置成功。

## 五、提交和clone修改

1.clone仓库对应的账户

` git clone git@xxx.github.com:username/repo.git`

2.本地已有库或clone

    打开本地库内.git/config修改remote "origin"项中url内容

` url=git@xxx.github.com:username/repo.git`

    或者提交内容时，修改remote

` git remote rm origin`

` git rwmote add origin git@xxx.github.com:username/repo.git`

## 以上

