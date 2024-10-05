+++
author = "coucou"
title = "泰山派Ubuntu屏幕映射 + LVGL显示测试"
date = "2024-10-05"
description = "泰山派Ubuntu屏幕映射 + LVGL显示测试"
categories = [
    "学习类资源合集"
]
tags = [
    "学习类资源合集"
]
image = "1.jpg"

+++


# 泰山派Ubuntu屏幕映射 + LVGL显示测试

### **xRDP  +  xfce4 实现 RDP 远程桌面**

> **说明！！！**
>
> **windows和泰山派要在同一个网段，即windows可以 ping通 泰山派**

#### 一、泰山派配置 xRDP  +  xfce4

1. **更新 Linux 开发板的包管理器**

   ```
   sudo apt update && sudo apt upgrade
   ```
2. **安装 xRDP** 和 **桌面环境**

   ```
   sudo apt install xrdp
   sudo apt install xfce4 xfce4-goodies
   ```
3. **配置 xRDP 使用桌面环境**

   ```
   echo xfce4-session > ~/.xsession
   ```
4. **编辑 `/etc/xrdp/startwm.sh` 文件，找到以下两行：**

   ```
   test -x /etc/X11/Xsession && exec /etc/X11/Xsession
   exec /bin/sh /etc/X11/Xsession
   ```

   **将它们注释掉，并添加以下两行来使用 **`xfce`：

   ```
   unset DBUS_SESSION_BUS_ADDRESS
   startxfce4
   ```
5. **启动并启用 xRDP 服务**
   **启动 **`xRDP` 并让它开机自启：

   ```
   sudo systemctl enable xrdp
   sudo systemctl start xrdp
   sudo systemctl status xrdp
   ```

#### 二、 Windows 远程桌面连接

> * **按 **`Win + R` 键打开“运行”窗口，输入 `mstsc`，然后按下回车，打开远程桌面连接工具。
> * **输入 IP+端口， ****3389**（xRDP 的默认端口）是开放的：
