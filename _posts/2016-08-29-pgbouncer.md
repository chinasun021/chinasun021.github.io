---
layout: post
title: "pgbouncer安装和使用"
date:   2016-08-29 10:37:08
categories: 技术学习
---

## 安装
* 系统：Centos6.5 x64
* 安装libevent，yum install libevent libevent-devel
* 下载pgbouncer，这里使用的是pgbouncer-1.5.4.tar.gz
* 解压缩pgbouncer-1.5.4.tar.gz，然后依次执行：

	./configure --prefix=/usr/local/pgbouncer
	make
	make install

* 将pgbouncer可执行文件加软链接到/usr/bin目录：

	ln -s /usr/local/pgbouncer/bin/pgbouncer /usr/bin/pgbouncer

## 配置
* 在/usr/local/pgbouncer目录下新建一个文件pgbouncer.ini，内容参考如下：

	[databases]
	temp1= host=127.0.0.1 port=5432 dbname=mydb user=postgres password=test

	[pgbouncer]
	listen_port = 6432
	listen_addr = 127.0.0.1
	auth_type = md5
	auth_file = /usr/local/pgbouncer/user.txt
	logfile = /var/log/pgbouncer/pgbouncer.log
	pidfile = /var/logl/pgbouncer/pgbouncer.pid
	admin_users = admin
	pool_mode = Transaction
	max_client_conn = 2000
	default_pool_size = 60

* 并创建一个授权文件/usr/local/pgbouncer/user.txt（admin为pgbouncer用户，password为用户密码）

	"admin" "password"

* 新建一个文件夹/var/log/pgbouncer，然后对该文件夹授权,chmod 777 -R /var/log/pgbouncer

## 启动
* 启动pgbouncer，以postgres用户启动，不可以通过root用户启动

	[root@wx-srv-test pgbouncer]#pgbouncer -d /usr/local/pgbouncer/pgbouncer.ini -u postgres
	2016-08-29 09:55:56.374 8685 LOG File descriptor limit: 1024 (H:4096), max_client_conn: 5000, max fds possible: 5410

* 登录

	psql -p 6432 -h 127.0.0.1 -U admin temp1                       //admin为pgbouncer用户，temp1为pgbouncer配置的数据库
	psql -p 6432 -h 127.0.0.1 -U admin pgbouncer                //登录pgbouncer数据库，这时不连接实际的postgresql数据库，可以自己选择需要连接的数据库
