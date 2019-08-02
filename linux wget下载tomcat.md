# linux wget下载tomcat

### 选择要下载的版本

去tomcat库查看想要下载的版本 
<https://mirrors.cnnic.cn/apache/tomcat/>



#### 下载

进入想要下载的本地路径，执行下列命令

wget +空格+版本地址

wget https://mirrors.cnnic.cn/apache/tomcat/tomcat-9/v9.0.7/bin/apache-tomcat-9.0.7.tar.gz

## 解压

```
tar xzf apache-tomcat-9.0.7.tar.gz

## 测试
cd apache-tomcat-9.0.7/
sh bin/startup.sh

## 访问8080端口看成功与否
## 关闭
sh bin/shutdown.sh
```

## 配置环境变量

```
## 查看当前路径
pwd   
## 我的路径是/usr/local/tomcat/apache-tomcat-9.0.7
## 修改配置文件
vim /etc/profile
# 在配置文件末尾增加tomcat配置
TOMCAT_HOME=/usr/local/tomcat/apache-tomcat-9.0.7
PATH=$PATH:$TOMCAT_HOME/bin
export TOMCAT_HOME PATH

# 刷新配置
source /etc/profile
## 
```

## 验证,进入tomcat的bin目录

```
cd /usr/local/webserver/tomcat9/bin/

./startup.sh	## 启动tomcat
./shutdown.sh	## 关闭tomcat
```

