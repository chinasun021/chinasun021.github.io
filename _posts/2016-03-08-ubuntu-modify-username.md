---
layout: post
title: "ubuntu modify username"
date:   2016-03-08 12:24:40
categories:
---
Ubuntu下创建的用户如果需要修改用户名，可以通过如下方式执行:
1.使用系统中另一个用户登录，然后以root权限执行usermod -l newuser olduser -d /home/newuser
2.将原先用户的主目录/home/olduser修改为/home/newuser:mv /home/olduser /home/newuser
3.这时就可以注销当前用户，以新用户来登录了，注意：这时的新用户属组名可能还是原来的，如果需要修改，可以编辑/etc/group