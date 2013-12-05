---
layout: post
title: "Lantern常用资源"
comments: true
date: 2012-12-06 19:57
categories: "网络"
tags: [墙,lantern]
---
{% include JB/setup %}
 
###**GFW代理列表文件**
第一次用 #Lantern 登上`youtube`的同学，会发现页面加载不完整，这是因为软件自设的代理地址不够，需要找一个完整的gfw列表替换掉
原有列表，中国用户用这个列表文件 GFW.list：  
[印象笔记](https://www.evernote.com/shard/s67/sh/8a28e65c-c32a-44e2-bf01-eeec714e983d/afc48748a8295ee97729675580a74069)  
[Dropbox](https://dl.dropboxusercontent.com/u/3898221/lantern/GFWlist%20for%20Lantern.txt)

     
###**Lantern完整离线安装包**  

Mac版本        [https://s3.amazonaws.com/lantern/latest.dmg](https://s3.amazonaws.com/lantern/latest.dmg)  

Windows版本    [https://s3.amazonaws.com/lantern/latest.exe](https://s3.amazonaws.com/lantern/latest.exe)  

ubuntu32位版本 [https://s3.amazonaws.com/lantern/latest-32.deb](https://s3.amazonaws.com/lantern/latest-32.deb)  

ubuntu64位版本 [https://s3.amazonaws.com/lantern/latest-64.deb](https://s3.amazonaws.com/lantern/latest-64.deb)  


更新：已经提供最新的  Lantern 1.0.0-rc1 的完整安装程序，欢迎试用。
需要正常使用请确保已经安装JRE（1.6以上）或JDK
当前版本：`Lantern 1.0.0-rc1`
####改变：
    1、”处于代理站点”增加一些新的站点
    2、提供新版本Lantern完整包的下载地址
    3、被邀请的人是否打开邀请邮件了，被邀请的人是否安装客户端了，之前没有统计，从这个版本开始统计
    4、客户端左上方不显示你的邮箱地址
    5、增加如何更新的说明(卸载旧版本，重新运行那个90多KB的文件)
    6、支持多国语言

####修复：
    
    1、添加好友的时候，总是提示添加失败
    2、右下角出现别人添你为好友的信息，朋友的名字有时候是乱码
    3、Ubuntu系统下，chromium浏览器的路径有问题
    4、【重大BUG】连接云服务器还是连接自己的好友取决于邀请你的人，现在取消这个规则(之前Lantern官方是这么决定的：网友A注册成功了，A连上的云服务器是1，然后A邀请了网友B和C，那么B和C只能连跟A一样的云服务器1,而不是2、3等服务器)
    5、facebook等网站图片不能正常显示


