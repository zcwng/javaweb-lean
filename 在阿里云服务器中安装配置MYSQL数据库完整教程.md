# [在阿里云服务器中安装配置MYSQL数据库完整教程](https://www.cnblogs.com/ljysy/p/10324854.html)

阿里云ECS服务器CentOS7上安装MySql服务

(可选)1.确保服务器系统处于最新状态
[root@localhost ~]# yum -y update
如果显示以下内容说明已经更新完成
Replaced:
grub2.x86_64 1:2.02-0.64.el7.centos grub2-tools.x86_64 1:2.02-0.64.el7.centos
Complete!

（可选）2.重启服务器
[root@localhost ~]# reboot

3.首先检查是否已经安装，如果已经安装先删除以前版本，以免安装不成功
[root@localhost ~]# php -v
或
[root@localhost ~]# rpm -qa | grep mysql
或
[root@localhost ~]# yum list installed | grep mysql

如果显示以下内容说明没有安装服务
-bash: gerp: command not found

如果有![img](https://img2018.cnblogs.com/blog/1374263/201810/1374263-20181009201959870-284215372.png)

就删除

![img](https://img2018.cnblogs.com/blog/1374263/201810/1374263-20181009202050875-1020031368.png)

```
4.下载MySql安装包（不靠谱）
[root@localhost ~]# rpm -ivh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
或
[root@localhost ~]# rpm -ivh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm

5.安装MySql
[root@localhost ~]# yum install -y mysql-server
或
[root@localhost ~]# yum install mysql-community-server
如果显示以下内容说明安装成功
Complete!
```

**下载mysql安装包：**

　　　　下载地址：http://dev.mysql.com/downloads/mysql/5.6.html#downloads

　　　　下载版本：我这里选择的5.6.33，通用版，linux下64位

　　　　也可以直接复制64位的下载地址，通过命令

```
wget http://dev.mysql.com/get/Downloads/MySQL-5.6/mysql-5.6.33-linux-glibc2.5-x86_64.tar.gz --no-check-certificate

tar -xvf mysql-5.6.33-linux-glibc2.5-x86_64.tar.gz
```

6.设置开机启动Mysql
[root@localhost ~]# systemctl enable mysqld.service

7.检查是否已经安装了开机自动启动
[root@localhost ~]# systemctl list-unit-files | grep mysqld
如果显示以下内容说明已经完成自动启动安装
mysqld.service enabled

8.设置开启服务
[root@localhost ~]# systemctl start mysqld.service

9.查看MySql默认密码
[root@localhost ~]# grep 'temporary password' /var/log/mysqld.log

10.登陆MySql，输入用户名和密码
[root@localhost ~]# mysql -uroot -p

11.修改当前用户密码
mysql>SET PASSWORD = PASSWORD('Abc123!_');

注：直接复制粘贴上边的命令，会报错，错误如下：

![img](https://img2018.cnblogs.com/blog/1173001/201901/1173001-20190126202759357-406719673.png)

解决方案如下：

原因：mysql为了安全，有自己的策略要求，如果我们想将其设置为我们常用的root或者123456这样的密码，需要修改策略要求，具体命令如下：

1.设置密码的验证强度等级，设置 validate_password_policy 的全局参数为 LOW 即可，
输入设值语句 “ set global validate_password_policy=LOW; ” 进行设值

2.当前密码长度为 8 ，如果不介意的话就不用修改了，按照通用的来讲，设置为 6 位的密码，设置 validate_password_length 的全局参数为 6 即可，
输入设值语句 “ set global validate_password_length=6; ” 进行设值

3.现在可以为 mysql 设置简单密码了，只要满足六位的长度即可，
输入修改语句 “ ALTER USER 'root'@'localhost' IDENTIFIED BY '123456'; ” 可以看到修改成功，表示密码策略修改成功了！！！

12.开启远程登录，授权root远程登录
mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'a123456!' WITH GRANT OPTION;

13.命令立即执行生效
mysql>flush privileges;

 

Mysql是为了安全考虑，初始的时候并没有开启Root用户的远程访问权限，Root只能本地localhost，127.0.0.1访问，但是我们操作起来实在是不方便，下面我们就使用Xshell连接Linux服务器操作Mysql给Root用户添加远程访问权限。
我们先试用Xshell链接我们的远程Linux服务器：

2、然后输入

-> mysql -u root -p

回车会出现 Enter password: 然后将我们的root用户密码输入进去再次回车：

别忘了要切换到mysql数据库

-> use mysql

3、接下来我们可以查看一下现有用户及连接权限

-> select user, password, host from user;

 

mysql是为了安全考虑所以初始的时候远程是不能访问的，只能本地localhost，127.0.0.1访问。
4、下面我们就再添加一个root用户，密码暂时为空，允许任意Ip访问'%'     
   -> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '你的密码不能太简单' WITH GRANT OPTION;

5、接下来我们修改一下root用户的密码

-> update user set password=PASSWORD('123456') where user='root';

6、然后我们刷新一下mysql的权限

-> flush privileges; 
然后就大功告成了，远程任意ip都可以进行访问。

 

 

\# 检查并且显示Apache相关安装包
[root@localhost ~]# rpm -qa | grep mysql

\# 删除MySql
[root@localhost ~]# yum remove -y mysql mysql mysql-server mysql-libs compat-mysql51
或
[root@localhost ~]# rpm -e mysql-community-libs-5.7.20-1.el7.x86_64 --nodeps
或
[root@localhost ~]# yum -y remove mysql-community-libs-5.7.20-1.el7.x86_64

\# 查看MySql相关文件
[root@localhost ~]# find / -name mysql

\# 重启MySql服务
[root@localhost ~]# service mysqld restart

\# 查看MySql版本
[root@localhost ~]# yum repolist all | grep mysql

\# 查看当前的启动的 MySQL 版本
[root@localhost ~]# yum repolist enabled | grep mysql

\# 通过Yum来安装MySQL,会自动处理MySQL与其他组件的依赖关系
[root@localhost ~]# yum install mysql-community-server

\# 查看MySQL安装目录
[root@localhost ~]# whereis mysql

\# 启动MySQL服务
[root@localhost ~]# systemctl start mysqld

\# 查看MySQL服务状态
[root@localhost ~]# systemctl status mysqld

\# 关闭MySQL服务
[root@localhost ~]# systemctl stop mysqld

\# 测试MySQL是否安装成功
[root@localhost ~]# mysql

\# 查看MySql默认密码
[root@localhost ~]# grep 'temporary password' /var/log/mysqld.log

\# 查看所有数据库
mysql>show databases;

\# 退出登录数据库
mysql>exit;

\# 查看所有数据库用户
mysql>SELECT DISTINCT CONCAT('User: ''',user,'''@''',host,''';') AS query FROM mysql.user

 