---
title: Hyper-V安装Linux开启增强会话
pubDate: 2025-08-31
categories: ['折腾']
description: ''
---

## Ubuntu版本：
```
wget https://raw.githubusercontent.com/Microsoft/linux-vm-tools/master/ubuntu/18.04/install.sh
sudo chmod +x install.sh
sudo ./install.sh
```

这是由于xrdp不再支持use_vsock=yes，所以需要修改默认的xrdp配置文件

修改```/etc/xrdp/xrdp.ini```文件

将```port=3389```修改为```port=vsock://-1:3389```

将```use_vsock=true```修改为```use_vsock=false```

保存之后重启虚拟机，然后关闭虚拟机。

## Manjaro版本：

进入命令行，输入6中创建的用户名 和 密码。然后执行：
````
sudo pacman –Sy
sudo pacman –S git
cd Downloads (or wherever you want to download it to)
git clone https://github.com/Microsoft/linux-vm-tools.git ./linux-vm-tools
cd linux-vm-tools/arch
./makepkg.sh
sudo ./install.sh
````
整个过程除了上面的命令行之外，还会有提示，让你输入Y（或者直接敲回车）。下载安装包的过程也很漫长。

安装好linux-vm-tools from Microsoft之后，编辑.xinitrc文件，把```--exit-with-session```删除。

```local dbus_args=(--sh-syntax --exit-with-session)```修改为```local dbus_args=(--sh-syntax)```

最后在主机中执行下面的命令
```Set-VM -VMName <你虚拟机的名称> -EnhancedSessionTransportType HvSocket```

#### 将<你虚拟机的名称>整体替换为在Hyper-V中虚拟机的名称，不要保留<>

#### 可以通过下面命令检查是否设置成功，显示HvSocket即可：

``(Get-VM -VMName <你虚拟机的名称>).EnhancedSessionTransportType``

最后启动虚拟机即可。**注意:虚拟机不要开启自动登录。**