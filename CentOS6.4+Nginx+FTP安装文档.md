# 安装Nginx服务



## 基础环境

yum install -y gcc-c++
yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
yum install -y openssl openssl-devel

将nginx-1.8.0.tar.gz文件传到root目录：
cd /root
tar -zxvf nginx-1.8.0.tar.gz
cd /root/nginx-1.8.0

## 配置Nginx（整段复制）

```shell
./configure \
--prefix=/usr/local/nginx \
--pid-path=/var/run/nginx/nginx.pid \
--lock-path=/var/lock/nginx.lock \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--with-http_gzip_static_module \
--http-client-body-temp-path=/var/temp/nginx/client \
--http-proxy-temp-path=/var/temp/nginx/proxy \
--http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
--http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
--http-scgi-temp-path=/var/temp/nginx/scgi
```



## 编译与安装

```shell
make
make  install
```



## 创建目录

```shell
mkdir /var/temp
mkdir /var/temp/nginx/
mkdir /var/temp/nginx/client
```



## 启动

```shell
cd /usr/local/nginx/sbin/
./nginx 
```



## 配置nginx服务

创建一个名为nginx的文件

```shell
#!/bin/bash
# nginx Startup script for the Nginx HTTP Server
# it is v.0.0.2 version.
# chkconfig: - 85 15
# description: Nginx is a high-performance web and proxy server.
#              It has a lot of features, but it's not for everyone.
# processname: nginx
# pidfile: /var/run/nginx.pid
# config: /usr/local/nginx/conf/nginx.conf
nginxd=/usr/local/nginx/sbin/nginx
nginx_config=/usr/local/nginx/conf/nginx.conf
nginx_pid=/var/run/nginx.pid
RETVAL=0
prog="nginx"
# Source function library.
. /etc/rc.d/init.d/functions
# Source networking configuration.
. /etc/sysconfig/network
# Check that networking is up.
[ ${NETWORKING} = "no" ] && exit 0
[ -x $nginxd ] || exit 0
# Start nginx daemons functions.
start() {
if [ -e $nginx_pid ];then
   echo "nginx already running...."
   exit 1
fi
   echo -n $"Starting $prog: "
   daemon $nginxd -c ${nginx_config}
   RETVAL=$?
   echo
   [ $RETVAL = 0 ] && touch /var/lock/subsys/nginx
   return $RETVAL
}
# Stop nginx daemons functions.
stop() {
        echo -n $"Stopping $prog: "
        killproc $nginxd
        RETVAL=$?
        echo
        [ $RETVAL = 0 ] && rm -f /var/lock/subsys/nginx /var/run/nginx.pid
}
# reload nginx service functions.
reload() {
    echo -n $"Reloading $prog: "
    #kill -HUP `cat ${nginx_pid}`
    killproc $nginxd -HUP
    RETVAL=$?
    echo
}
# See how we were called.
case "$1" in
start)
        start
        ;;
stop)
        stop
        ;;
reload)
        reload
        ;;
restart)
        stop
        start
        ;;
status)
        status $prog
        RETVAL=$?
        ;;
*)
        echo $"Usage: $prog {start|stop|restart|reload|status|help}"
        exit 1
esac
exit $RETVAL

```



把我们写好的nginx文件传到/etc/init.d/目录即可

为创建好的nginx文件授权：

```shell
chmod a+x /etc/init.d/nginx
```

如果提示文件不存在，说明编码不对，需要转码：

```shell
yum install -y dos2unix
dos2unix /etc/init.d/nginx
```

启动nginx服务

```
service nginx restart
```

开机自启动

```
chkconfig nginx on
```

防火墙：

```
service iptables stop
chkconfig iptables off
```

用浏览器访问http://当前服务器地址

------------------------------
# 安装FTP服务

## 安装与启动

```shell
yum install -y vsftpd
service vsftpd start
chkconfig vsftpd on
useradd -s /sbin/nologin -d /usr/local/nginx/html ftpuser
useradd -d /usr/local/nginx/html ftpuser
passwd 123456
chmod o+w /usr/local/nginx/html/
```

编辑/etc/vsftpd/vsftpd.conf文件，
注意不要出现空格，且保证文档类型为unix格式，
修改配置：anonymous_enable=NO
添加配置：reverse_lookup_enable=NO
保存重启：service vsftpd restart


查看selinux信息：
getsebool -a|grep ftp

设置selinux权限：
setsebool -P allow_ftpd_full_access on
setsebool -P ftp_home_dir on

------

yum 卸载：
rpm -qa | grep 程序包名称
rpm -e 文件名

```
rpm -qa | grep vsftpd
#可以查出文件名称 例如 vsftp-2.2.xxxxxxx
rpm -e vsftp-2.2.xxxxxxx
#卸载完成
```



---------------------------
使用Java连接FTP服务器，可以使用apache的commons-net包中的FtpClient对象，
开源FTP连接池：https://github.com/XiaZengming/FtpClientPool



# linux下nginx首次安装远程无法访问

所谓的本地机器，就是你安装了nginx软件的那一台机器，输入命令：

```
curl http://192.168.241.129/
```

```
[root@Pluto ~]# curl http://47.94.218.62
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>

​```
body {
    width: 35em;
    margin: 0 auto;
    font-family: Tahoma, Verdana, Arial, sans-serif;
}
​```
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
[root@Pluto ~]# 
```

显然安装成功！！！