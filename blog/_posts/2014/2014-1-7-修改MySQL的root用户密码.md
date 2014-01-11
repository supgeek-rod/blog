---
layout: post
title: 修改MySQL的root用户密码
categories:
- Codes
tags:
- MySQL
- root

---
各版本在各种系统中的实际代码可以不一样，遇到问题照着解决问题的思路总是能成功的

## 第一次设置root密码
使用空密码登陆root用户，进行修改root密码

	mysql -u root
	mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('新密码');



## 忘记root密码
忘记了root用户密码的情况，修改起来就麻烦一点。   
第一步，先结束MySQL的进程
第二步，不检查权限的方式启动MySQL

	safe_MySQLd --skip-grant-tables &  
	// safe_MySQLd命令不存在可以是因为版本原因，应该使用下面这条命令
	// MySQLd --skip-grant-tables & 

第三步，使用root用户空密码登陆
第四步，修改密码并提交修改

	MySQL> update MySQL.user set password=PASSWORD('新密码') where User='root';   
    MySQL> flush privileges;   // 千万别忘了这一步,否则修改不会生效
    MySQL> quit  
    
结束MySQL后，再正常启动就可以修改新密码登陆了