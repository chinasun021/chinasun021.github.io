---
layout: post
title: "pgbouncer��װ��ʹ��"
date:   2016-08-29 10:37:08
categories:����ѧϰ
---
##��װ
* ϵͳ��Centos6.5 x64
* ��װlibevent��yum install libevent libevent-devel
* ����pgbouncer������ʹ�õ���pgbouncer-1.5.4.tar.gz
* ��ѹ��pgbouncer-1.5.4.tar.gz��Ȼ������ִ�У�

	./configure --prefix=/usr/local/pgbouncer
	make
	make install

* ��pgbouncer��ִ���ļ��������ӵ�/usr/binĿ¼��

	ln -s /usr/local/pgbouncer/bin/pgbouncer /usr/bin/pgbouncer

##����
* ��/usr/local/pgbouncerĿ¼���½�һ���ļ�pgbouncer.ini�����ݲο����£�

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

* ������һ����Ȩ�ļ�/usr/local/pgbouncer/user.txt��adminΪpgbouncer�û���passwordΪ�û����룩

	"admin" "password"

* �½�һ���ļ���/var/log/pgbouncer��Ȼ��Ը��ļ�����Ȩ,chmod 777 -R /var/log/pgbouncer

##����
* ����pgbouncer����postgres�û�������������ͨ��root�û�����

	[root@wx-srv-test pgbouncer]#pgbouncer -d /usr/local/pgbouncer/pgbouncer.ini -u postgres
	2016-08-29 09:55:56.374 8685 LOG File descriptor limit: 1024 (H:4096), max_client_conn: 5000, max fds possible: 5410

* ��¼

	psql -p 6432 -h 127.0.0.1 -U admin temp1                       //adminΪpgbouncer�û���temp1Ϊpgbouncer���õ����ݿ�
	psql -p 6432 -h 127.0.0.1 -U admin pgbouncer                //��¼pgbouncer���ݿ⣬��ʱ������ʵ�ʵ�postgresql���ݿ⣬�����Լ�ѡ����Ҫ���ӵ����ݿ�
