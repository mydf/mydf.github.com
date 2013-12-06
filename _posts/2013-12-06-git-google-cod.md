---
layout: post
title: "用GoAgent配合Git使用Google Code的代码托管"
comments: true
date: 2013-12-06 10:57
categories: "技术"
tags: git
---

###安装git：  
    sudo apt-get install git
###安始化git：    
    git init 
###代码仓库加入到git：    
    git add . 
###提交：   
    git commit -m "repo"
###密码：   
  在home目录下建立一个文件名为：.netrc的文件，把<https://code.google.com/hosting/settings>上的登录名和密码复制粘贴到文件中，形如:      
    machine code.google.com login bjaky3801@gmail.com password ytkGJ3fh23fkd 
###代理：   
    git config --global http.proxy "127.0.0.1:8087"   
###上传：   
    git push https://code.google.com/p/YOUPROJECT/ master 
这时你会看到输出告诉你正在上传，搞定。  
