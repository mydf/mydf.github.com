---
layout: post
title: "Ubuntu使用 dnsmasq作本地DNS缓存"
comments: true
date: 2013-12-11 19:57
categories: "备忘"
tags: Ubuntu
---
### 安装 dnsmasq加速网络访问速度

    sudo apt-get install dnsmasq
###配置 dnsmasq

**修改`/etc/resolv.conf`文件。**将原有的内容全部注释，然后在第一行写上  

      nameserver 127.0.0.1
也可以使用ubuntu的网络管理小程序“Network Manager”在桌面右上角有一个它的图标，右键点击该图标，选择“编辑连接”，选择你所使用的连接，点击编辑，在“IPv4设置”标签的“DNS服务器”输入框中，把原有的DNS服务器删除，输入 127.0.0.1  

**在/etc目录下新建resolv.dnsmasq文件。** 文件的内容为DNS服务器的地址，是真正的DNS服务器，如我的文件内容是：

    nameserver 199.91.73.222
    nameserver 42.120.21.30
    nameserver 8.8.8.8

**可以不按帮助文档所说的执行“dnsmasq-r/etc/resolv.dnsmasq”命令**，如果这样，岂不是每次都得在命令行里输入，非常麻烦，当然，可以考虑把这个命令写入“/etc/rc.local”文件中，让系统每次启动时帮你运行。 我所使用的方法是编辑“/etc/dnsmasq.conf”文件。  

    sudo gedit /etc/dnsmasq.conf

找到下面这一项  

    #resolv-file=

用下面的一条语句替换

    resolv-file=/etc/resolv.dnsmasq

其实也就是执行dnsmasq命令中-r参数后面的内容。  

**编辑 /etc/dhcp3/dhclient.conf **

    sudo gedit /etc/dhcp3/dhclient.conf 

找到下面这一项

    #prepend domain-name-servers 127.0.0.1

将前面的“#”删除。这么做的目的是为了在使用自动连接时，能在/etc/resolv.conf文件的第一行添加上“nameserver 127.0.0.1”，这样，`dns缓存依然有效。`  

**编辑 /etc/ppp/peers/dsl-provider**  

    sudo gedit /etc/ppp/peers/dsl-provider 
    
可能有的系统没有“/etc/ppp/peers/dsl-provider”文件，而是“/etc/ppp/peers/provider”文件，找到下面这一项  

    usepeerdns
在前面增加“#”，也就是把这条语句注释掉，`以防resolv.conf的设置被pppoe复盖。`  
**对于12.04版本**  
由于该版本已经安装dnsmasq-base，则必须先修改/etc/NetworkManager/NetworkManager.conf文件  

    sudo gedti /etc/NetworkManager/NetworkManager.conf  
找到dns=dnsmasq，在前面增加“#”，`也就是把这句注释掉。`  

    sudo gedit /etc/default/dnsmasq
找到IGNORE_RESOLVCONF=yes，`这一条要删除注释，删掉#号。`
###重启服务：  

    sudo /etc/init.d/dnsmasq restart
或者   

    sudo service dnsmasq restart
###测试结果：
随便找一个网址，测试两次就能看出查询时间的差异：  

    dig google.com
两次返回结果的时间不一样，第二次一般是0ms；多试几个网址，证明成功了。


