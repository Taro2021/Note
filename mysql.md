```shell
#删除
#首先查询系统是否安装了MySQL
rpm -qa | grep -i mysql

#查看MySQL服务运行状态
service mysql status
#停止MySQL服务
service mysql stop

#查看MySQL对应的文件夹
find / -name mysql

#卸载并删除MySQL安装的组键服务
rpm -ev mysql-community-common-5.6.44-2.el7.x86_64
rpm -ev mysql-community-release-el7-5.noarch
rpm -ev mysql-community-client-5.6.44-2.el7.x86_64
rpm -ev mysql-community-server-5.6.44-2.el7.x86_64
rpm -ev mysql-community-libs-5.6.44-2.el7.x86_64
#rpm -ev 加上--nodeps：--nodeps就是安装时不检查依赖关系

#删除系统中MySQL的所有文件夹
rm -rf /etc/selinux/targeted/active/modules/100/mysql
rm -rf /var/lib/mysql
rm -rf /var/lib/mysql/mysql
rm -rf /usr/share/mysql

#最后验证MySQL是否删除完成
rpm -qa | grep -i mysql


#Mysql8.0安装 (YUM方式)
#首先删除系统默认或之前可能安装的其他版本的mysql
for i in $(rpm -qa|grep mysql);do rpm -e $i --nodeps;done
rm -rf /var/lib/mysql && rm -rf /etc/my.cnf

# rpm
wget https://dev.mysql.com/get/mysql80-community-release-el8-1.noarch.rpm
sudo rpm -ivh mysql80-community-release-el8-1.noarch.rpm
#yum 安装
sudo yum install -y mysql-server

#设置开机启动
sudo systemctl enable --now mysqld

#查看mysql状态
sudo systemctl status mysqld

#启动
sudo systemctl start mysqld.service

#初始化
mysqld --initialize

#查看 mysql 的默认密码
grep 'temporary password' /var/log/mysqld.log

#若默认无密码，无密码登录
mysql -u root
#修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Mypwd123!';

#新建本地用户
mysql> CREATE USER 'test'@'localhost' IDENTIFIED BY '123456';

#新建远程用户
mysql> CREATE USER 'test'@'%' IDENTIFIED BY '123456';

#赋予指定账户指定数据库远程访问权限
mysql> GRANT ALL PRIVILEGES ON mydb.* TO 'test'@'%';

#赋予指定账户对所有数据库远程访问权限
mysql> GRANT ALL PRIVILEGES ON *.* TO 'test'@'%';

#赋予指定账户对所有数据库本地访问权限
mysql> GRANT ALL PRIVILEGES ON *.* TO 'test'@'localhost';

#刷新权限
mysql> FLUSH PRIVILEGES;
```

