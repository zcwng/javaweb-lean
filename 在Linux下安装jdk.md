# 在Linux下安装jdk

作为Java开发人员，在Linux下安装一些开发工具是必备技能，本文以安装jdk为例，详细记录了每一步的操作命令，以供参考。

## 第一种方法

只需要一条命令就可以安装jdk：
yum install java-1.8.0-openjdk* -y
执行了这条命令不需要配置，直接可以用

## 第二种方法

### 0.下载jdk8

登录网址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
选择对应jdk版本下载。（可在Windows下下载完成后，通过文件夹共享到Linux上）



### 1.登录Linux，切换到root用户

su root 获取root用户权限，当前工作目录不变(需要root密码)


或


sudo -i 不需要root密码直接切换成root（需要当前用户密码）



### 2.在usr目录下建立java安装目录

cd /usr


mkdir java



### 3.将jdk-8u60-linux-x64.tar.gz拷贝到java目录下


cp /mnt/hgfs/linux/jdk-8u60-linux-x64.tar.gz /usr/java/



### 4.解压jdk到当前目录


tar -zxvf jdk-8u60-linux-x64.tar.gz


得到文件夹 jdk1.8.0_60



### 5.安装完毕为他建立一个链接以节省目录长度

(我没用这一步)
ln -s /usr/java/jdk1.8.0_60/ /usr/jdk



### 6.编辑配置文件，配置环境变量


vim /etc/profile


添加如下内容：JAVA_HOME根据实际目录来
export JAVA_HOME=/usr/java/jdk1.8.0_60
export CLASSPATH=$JAVA_HOME/lib/
export PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH





### 7.重启机器或执行命令 ：source /etc/profile


sudo shutdown -r now



### 8.查看安装情况

java -version


java version "1.8.0_60"
Java(TM) SE Runtime Environment (build 1.8.0_60-b27)
Java HotSpot(TM) Client VM (build 25.60-b23, mixed mode)

### 



可能出现的错误信息：


bash: ./java: cannot execute binary file


出现这个错误的原因可能是在32位的操作系统上安装了64位的jdk，
查看jdk版本和Linux版本位数是否一致。
查看你安装的Ubuntu是32位还是64位系统：
sudo uname --m
i686 //表示是32位
x86_64 // 表示是64位