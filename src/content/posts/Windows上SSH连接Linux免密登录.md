---
title: Windows上SSH连接Linux免密登录
pubDate: 2025-08-31
categories: ['折腾']
description: ''
---

## 1、生成公钥文件（Windows）

**在命令提示符上输入以下指令：**

```ssh-keygen -t rsa```

**直接回车到底。**

## 2、上传公钥文件（Windows）

找到公钥文件的路径，第1步出现：```“Your public key has been saved in %USERPROFILE%/.ssh/id_rsa.pub.”```

所以公钥文件的路径：是```"%USERPROFILE%/.ssh/id_rsa.pub"```

上传密钥到：```~/.ssh```文件夹

替换为：```.ssh/authorized_keys```

修改文件权限

```
chmod 600 .ssh/authorized_keys

chmod 700 .ssh
```

## 3、修改SSH配置文件（Linux）

这个配置文件一般是只读文件，需要root权限

```sudo vim /etc/ssh/sshd_config```

保证这三句不被注释掉，如果没有则添加新的对应的语句。"
```
RSAAuthentication yes 

PubkeyAuthentication yes 

AuthorizedKeysFile .ssh/authorized_keys
```
保存退出。

## 4、重新启动SSH服务（Linux）

```sudo service sshd restart```