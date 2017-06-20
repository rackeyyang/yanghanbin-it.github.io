---
title: centos安装mysql
categories: Linux
tags: [Linux,centos,mysql,mariadb]
date: 
---

mariadb简介MariaDB数据库管理系统是MySQL的一个分支，主要由开源社区在维护，采用GPL授权许可 MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。在存储引擎方面，使用XtraDB（英语：XtraDB）来代替MySQL的InnoDB。 MariaDB由MySQL的创始人Michael Widenius（英语：Michael Widenius）主导开发，他早前曾以10亿美元的价格，将自己创建的公司MySQL AB卖给了SUN，此后，随着SUN被甲骨文收购，MySQL的所有权也落入Oracle的手中。MariaDB名称来自Michael Widenius的女儿Maria的名字。

在centos7.0后,系统默认使用mariabd代替mysql.

### 安装mariadb

1. 通过Yum安装
``` shell
yum install mariadb mariadb-server
```

![image.png](http://upload-images.jianshu.io/upload_images/4990482-c0487bae7a42486c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. mariadb相关命令
``` shell
systemctl start mariadb  #启动MariaDB
systemctl stop mariadb  #停止MariaDB
systemctl restart mariadb  #重启MariaDB
systemctl enable mariadb  #设置开机启动

```

3. 启动mariadb并设置开机启动
``` shell 
systemctl start mariadb  #启动MariaDB
systemctl enable mariadb  #设置开机启动
```

4. 进入mariadb,命令和mysql一模一样
``` shell
mysql -u root -p 
...
```

5. 修改root的密码
``` shell
update mysql.user set password=PASSWORD('yhb123456') where user='root';
// 更新权限
flush privileges; 
```
6. 新建用户
``` shell
// create user  '用户名'@'主机' identified by '密码'   如果只允许本机访问 @'localhost'  , 或者指定一个ip  @'192.xx.xx.xx' 或者使用通配: @'%'
create user 'read_visa'@'%' identified by '123456';
```

7. 给用户分配权限
``` shell
// grant 操作类型 on 数据库.表 to 用户@'主机'   数据库,表,主机都支持通配符 grant select, insert on *.* to  'read_visa'@'%'
// grant all on visa.* to 'read_visa'@'%'; // all 表示所有权限
grant select on visa.* to 'read_visa'@'%';
```