---
layout: post
title:  "windows7 添加多个 git 账号"
categories: [Git]
tag:
---

* content
{:toc}


参考链接：

[https://www.cnblogs.com/popfisher/p/5731232.html](https://www.cnblogs.com/popfisher/p/5731232.html)
[https://www.cnblogs.com/liuguanglin/p/8351616.html](https://www.cnblogs.com/liuguanglin/p/8351616.html)

注意：设置之后我不能用 git@xxxx 地址进行操作，只能使用 ssl 方式进行操作，否则会出现下列错误：

    $ git clone git@github.com:xxxx/test-test_sub-test_sun.git
    Cloning into 'test-test_sub-test_sun'...
    Permission denied (publickey).
    fatal: Could not read from remote repository.
    
    Please make sure you have the correct access rights
    and the repository exists.

## 1 生成公钥和私钥

以管理员模式打开命令终端，执行命令：

    ssh-keygen -t rsa -C xxxxxxx@xxx.com
    
创建对应的 sshkey，命名为 id_rsa_1。

用同样的方式生成另一个 sshkey，命名为 id_rsa_1。

把生成的公钥和私钥文件拷贝到 C:\Users\xxx\.ssh 中。

## 2 添加公钥到对应的 github 账号 或者其他平台账号中

** github 平台**：账号->Settings->SSH and GPG keys->New SSH key

## 3 在 .ssh 目录中创建 config 文本文件

文件内容如下：

    # 配置user1 
    Host u1.github.com
    HostName github.com
    IdentityFile C:\\Users\\Administrator\\.ssh\\id_rsa
    PreferredAuthentications publickey
    User user1
    
    # 配置user2
    Host u2.github.com
    HostName github.com
    IdentityFile C:\\Users\\Administrator\\.ssh\\id_rsa2
    PreferredAuthentications publickey
    User user2

各字段说明：

- HostName：这个是真实的域名地址
- IdentityFile：这里是id_rsa的地址
- PreferredAuthentications：配置登录时用什么权限认证--可设为publickey,password publickey,keyboard-interactive等
- User：配置使用用户名

可以通过下列命令来测试 SSH key 是否有效：

    ssh -T git@u1.github.com
    ssh -T git@u2.github.com