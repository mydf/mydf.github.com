---
layout: post
title: "Goagent 3.1.0更新proxy.ini各项参数介绍 "
comments: true
date: 2013-12-10 19:57
categories: "网络"
tags: goagent
---
 Goagent 3.1.0测试版 proxy.ini各项参数介绍

{% highlight ruby %}

[listen]
#监听ip，如果需要允许局域网/公网使用，设为0.0.0.0即可
ip = 127.0.0.1
#使用GAE服务端的默认8087端口，如有需要你可以修改成其他的 
port = 8087
#启动后goagent窗口是否可见，0为不可见（最小化至托盘），1为不最小化 
visible = 1
#是否显示详细debug信息
debuginfo = 0
#GAE服务端的配置
[gae]
#你的Google app engine AppID,也就是服务器部署的APPID，配置多ID用|隔开
appid = goagent  
#密码,默认为空,你可以在server目录的wsgi.py设定,如果设定了,此处需要与wsgi,py保持一致
password = 123456
#服务端路径,一般不用修改,如果不懂也不要修改.
path = /2
#使用http还是https(SSL加密传输)连接至GAE
mode = https
#是否为IPv6，
ipv6 = 0
#ip评优算法每次选出的ip数量
window = 4
crlf = 1
#是否开启流量混淆
obfuscate = 0
#是否对服务器证书进行验证
validate = 0
# 如果设置为 rc4 则开启rc4加密，需在password设置密码，否则不开启，一般mode为https时无需开启
options =


# 匹配的会使用crlf并且直连，=后留空则使用远程DNS解析，也可以手动指定IP防止因解析失败而无法使用，将IP写等号后面。
# google_hk则表示使用[iplist]中的google_hk下的IP，google_cn则表示使用[iplist]中的google_cn下的IP
[hosts]
code.google.com = google_cn
mail.google.com = google_cn
mail-attachment.googleusercontent.com = google_cn
talk.google.com = 
talk.l.google.com = 
talkx.l.google.com = 
.google.com = google_hk
.googleusercontent.com = google_hk
.googleapis.com = google_hk
.google-analytics.com = google_hk
.googlecode.com = google_hk
.google.com.hk = google_hk
.googlegroups.com = google_hk
.googlesource.com = google_hk
.appspot.com = google_hk
.android.com = google_hk
.dropbox.com:443 = 
.box.com:443 = 
.copy.com:443 =
https?://www\.google\.com/(settings|contacts) = google_hk
https?://www\.google\.com(\.[a-z]{2})?/ = google_cn
https?://.+\.c\.youtube\.com/liveplay = google_cn
[http]
#匹配以此开头的域名强制跳转到https的网站
forcehttps = groups.google.com|code.google.com|docs.google.com#使用伪造的证书
fakehttps = www.google.com#通过GAE的地址
withgae = play.google.com
# 针对IPv6的设置
[ipv6/hosts]
talk.google.com = 
talk.l.google.com = 
talkx.l.google.com = .google.com = google_ipv6.googleusercontent.com = google_ipv6.googleapis.com = google_ipv6.google-analytics.com = google_ipv6.googlecode.com = google_ipv6.google.com.hk = google_ipv6.googlegroups.com = google_ipv6.googlesource.com = google_ipv6.appspot.com = google_ipv6.android.com = google_ipv6.dropbox.com:443 = .box.com:443 = .copy.com:443 =
[ipv6/http]
forcehttps = groups.google.com|code.google.com|docs.google.com
fakehttps = 
withgae = play.google.com
# 用于连接GAE的IP列表
[iplist]
google_cn = 203.208.46.131|203.208.46.132|203.208.46.133|203.208.46.134|203.208.46.135|203.208.46.136|203.208.46.137|203.208.46.138
google_hk = www.google.com|mail.google.com|www.google.com.hk|www.google.com.tw|www.l.google.com|mail.l.google.com
google_ipv6 = 2404:6800:4005:c00::64|2404:6800:4005:c00::65|2404:6800:4005:c00::5e|2404:6800:4005:c00::67|2404:6800:4005:c00::2f
#代理自动配置脚本(Proxy auto-config)设定
[pac]
#是否启用，若启用，浏览器代理自动配置地址填http://127.0.0.1:8086/proxy.pac
enable = 1
# pacserver的监听地址
ip = 127.0.0.1
port = 8086
# pac文件的名称
file = proxy.pac#被墙规则订阅地址
gfwlist = http://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt
#广告拦截规则订阅地址
adblock = http://adblock-chinalist.googlecode.com/svn/trunk/adblock.txt
#自动更新间隔时间
expired = 86400
#使用pass/php的配置
[paas]  #是否启用
enable = 0 #密码,默认为空,你可以在上传的Server设定,如果设定了,此处需要与Server保持一致
password = 123456 
crlf = 0
validate = 0
#本地监听，表示监听本地的IP与端口，使用时浏览器地址设置为这里 
listen = 127.0.0.1:8088
#paas/php server的地址
fetchserver = https://app.com/ 
#二级代理,一般内网会用到
[proxy]  #是否启用
enable = 0 
autodetect = 1
#代理服务器地址
host = 10.64.1.63  #代理服务器端口
port = 8080   #代理服务器登录用户名
username = username#密码  
password = 123456 
# 自动分段下载，需远程服务器支持Rang
[autorange]
#匹配以下域名时自动下载
hosts = *.c.youtube.com|*.atm.youku.com|*.googlevideo.com|*av.vimeo.com|smile-*.nicovideo.jp|video.*.fbcdn.net|s*.last.fm|x*.last.fm|*.x.xvideos.com|*.edgecastcdn.net|*.d.rncdn3.com|cdn*.public.tube8.com|videos.flv*.redtubefiles.com|cdn*.public.extremetube.phncdn.com|cdn*.video.pornhub.phncdn.com|*.mms.vlog.xuite.net|vs*.thisav.com|archive.rthk.hk|video*.modimovie.com|*.c.docs.google.com# 自动对列表中文件类型启用分段下载功能
endswith = .f4v|.flv|.hlv|.m4v|.mp4|.mp3|.ogg|.avi|.exe|.zip|.iso|.rar|.bz2|.xz|.dmg# 禁用分段下载的文件类型
noendswith = .xml|.json|.html|.php|.py|.js|.css|.jpg|.jpeg|.png|.gif|.ico|.webp# 线程数
threads = 3
#一次最大下载量
maxsize = 1048576
#首次读写量
waitsize = 524288
#后续读写量
bufsize = 8192
#DNS模块，可以用来防止DNS劫持/污染
[dns]
enable = 0
#DNS监听地址，使用时将系统DNS设置为127.0.0.1
listen = 127.0.0.1:53
#远程DNS查询服务器
remote = 8.8.8.8|8.8.4.4|114.114.114.114|114.114.115.115
#缓存大小
cachesize = 5000
#超时时间
timeout = 2
#模拟用户浏览器类型,在User-Agent里提交给服务器你的浏览器操作系统等信息
[useragent]  #是否启用
enable = 0 #可自行修改的，前提是你知道怎么改
string = Mozilla/5.0 (iPhone; U; CPU like Mac OS X; en) AppleWebKit/420+ (KHTML, like Gecko) Version/3.0 Mobile/1A543a Safari/419.3   
[fetchmax]  local =                 
server =                 
#不用理会,显示在控制台上方的公益广告
[love]   #不愿意看到这广告就把1改成0
enable = 1  
timestamp = 1347983481
tip = \u8bf7\u5173\u6ce8\u5317\u4eac\u5931\u5b66\u513f\u7ae5~~
{% endhighlight %}
