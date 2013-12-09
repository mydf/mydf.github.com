---
layout: post
title: "低配置VPS安装Ubuntu及Lantern详细过程"
date: 2013-12-09 18:41
category: "网络"
tags: [lantern,ubuntu,VPS,墙]
---
在服务商后台安装Ubuntu 12.04，测试发现目前这个版本比较稳定

    ssh root@你的IP

安装远程桌面所需要的东西：

    sudo apt-get update
    sudo apt-get install ubuntu-desktop  gnome-core vnc4server

Chrome不能直接在root下运行，要建立一个新用户，如我的是：

    adduser wenyunchao

输入及验证密码，资料可以直接回车确认。

将用户到用管理员组：

    echo “wenyunchao ALL=(ALL) ALL”  >>  /etc/sudoers

改变操作用户

    su - wenyunchao

设置VNC远程桌面密码

    vncpasswd

编辑远程桌面配置文件

    sudo nano ~/.vnc/xstartup

把下面的粘贴到文件里（#==========之前的这些）

    #!/bin/sh
    
    unset SESSION_MANAGER
    unset DBUS_SESSION_BUS_ADDRESS
    
    [-x /etc/vnc/xstartup ]&&exec/etc/vnc/xstartup
    [-r $HOME/.Xresources]&& xrdb $HOME/.Xresources
    xsetroot -solid grey
    vncconfig -iconic &
    x-terminal-emulator -geometry 80×24+10+10-ls -title ”$VNCDESKTOP Desktop”&
    
    export DESKTOP_SESSION=gnome
    export GDMSESSION=gnome
    export STARTUP=”/usr/bin/gnome-session –session=gnome”
    
    $STARTUP
    
    #==========

更改配置文件权限

    sudo chmod 755 ~/.vnc/xstartup

启动远程桌面

    vncserver

关闭时用 

    vncserver -kill :1

安装OPEN JAVA

    sudo apt-get install openjdk-7-jre

安装Chrome

    wget -q -O – https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
    sudo sh -c ‘echo “deb http://dl.google.com/linux/chrome/deb/ stable main” >> /etc/apt/sources.list.d/google-chrome.list’
    sudo apt-get update
    sudo apt-get install google-chrome-stable

更改交换文件至4G

    sudo dd if=/dev/zero of=/swapfile bs=64M count=64
    sudo mkswap /swapfile
    sudo swapon /swapfile

减少内存使用：

    sudo sysctl vm.swappiness=100
    
    sudo nano /etc/sysctl.conf

最后加入一行

    vm.swappiness=100

大功告成。

可以用vnc客户端登入试试，服务器地址是 你的IP:5901，然后打开Chrome,下载Lantern并安装。
