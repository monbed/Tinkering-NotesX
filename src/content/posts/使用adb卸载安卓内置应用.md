---
title: 使用adb卸载安卓内置应用
pubDate: 2025-08-31
categories: ['折腾']
description: ''
---

**1、激活开发者模式，打开USB调试**

**2、连接电脑，右键adb文件夹，打开PowerShell窗口。**

**3、输入.\adb shell进入shell模式。**

**4、获取要卸载的应用的包名，方法如下：**

推荐方法：先将 APP 打开，然后使用 ADB 命令查看当前界面的信息：

```设备名:/ $ dumpsys window | grep mCurrentFocus```

```mCurrentFocus=Window{33613e4 u0 com.baidu.haokan/com.baidu.haokan.app.activity.HomeActivity}```

这里 window{} 中就是这个界面的包名类名，包名就是：com.baidu.haokan
拿到包名之后，接下来就是卸载应用了，命令如下：

```pm uninstall -k --user 0 packageName```

这个命令的意思就是将用户 0 的 packageName 应用卸载掉。以上一步的com.baidu.haokan为例：

```设备名:/ $ pm uninstall -k --user 0 com.baidu.haokan```
```Success```

> -k 表示保存数据，如不需要，可去掉 -k。
> 
> --user 指定用户 id，Android 系统支持多个用户，默认用户只有一个，id=0。
> 
至此，系统预置的应用就被卸载了。部分情况下，有可能在设置 > 应用列表中看到“未针对此用户安装”的字样，这个没有影响，重启一下就没有了。
如果有残留，去应用设置清除数据即可。