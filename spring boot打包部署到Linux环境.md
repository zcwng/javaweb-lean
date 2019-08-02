## [spring boot打包部署到Linux环境](https://www.cnblogs.com/wuxun1997/p/10557924.html)

　　打包部署说白了就两步：打包、部署。废话不多说，直接拿spring boot自动生成的项目骨架，再添加一个文件用来演示：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
package com.crocodile.springboot;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class PDFController {
    @RequestMapping(value = "hello", method = RequestMethod.GET)
    public String helloWorld() {
        return "hello, world.";
    }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　还要在配置文件application.properties里加两个配置项：

```
#修改tomcat的默认的端口号，将8080改为8888
server.port=8888

#切换配置文件
spring.profiles.active=test
```

　　最后打包，直接跑Maven生成jar包就好了。

　　打完包就要部署了。因为spring boot有内置tomcat容器，这点比较方便，省去了tomcat的部署。我们直接把jar包扔到linux上。这里你可以通过FTP工具，也可以使用下面这个命令行的小工具，先安装：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 yum -y install lrzsz
Loaded plugins: fastestmirror
Determining fastest mirrors
base                                                                                                                                             | 3.6 kB  00:00:00     
epel                                                                                                                                             | 4.7 kB  00:00:00     
extras                                                                                                                                           | 3.4 kB  00:00:00     
updates                                                                                                                                          | 3.4 kB  00:00:00     
(1/2): epel/x86_64/updateinfo                                                                                                                    | 1.0 MB  00:00:00     
(2/2): epel/x86_64/primary_db                                                                                                                    | 6.6 MB  00:00:00     
Package lrzsz-0.12.20-36.el7.x86_64 already installed and latest version
Nothing to do
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　再上传：

```
rz -y
rz waiting to receive.
 zmodem trl+C ȡ
```

　　它会弹出一个界面让你选择具体文件的，你选择maven打好的jar后点击发送就ok了。

　　接着就是执行jar包，这里通过一个脚本来执行：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
#!/bin/sh
JAR_NAME=springboot-0.0.1-SNAPSHOT.jar

tpid=`ps -ef|grep $JAR_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
if [ ${tpid} ]; then
echo 'Stop Process...'
fi
sleep 5
tpid=`ps -ef|grep $JAR_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
if [ ${tpid} ]; then
echo 'Kill Process!'
kill -9 $tpid
else
echo 'Stop Success!'
fi

tpid=`ps -ef|grep $JAR_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
if [ ${tpid} ]; then
        echo 'App is running.'
else
        echo 'App is NOT running.'
fi

rm -f tpid
nohup java -jar ./$JAR_NAME --spring.profiles.active=test >/dev/null 2>&1 &
echo $! > tpid
echo 'Start Success!'
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　这个脚本的作用就是通过jar命令来执行jar包，前面是先通过grep命令看是否已有jar包在跑，有的话就杀掉再拉起，没有就直接跑。注意上面的JAR_NAME需要根据你的jar包名称赋值。另外最重要的一行就是通过nohup命令起一个后台线程跑该jar，并把生成的nohup.out指向一个黑洞当垃圾扔掉。对了，保存好脚本后还得给这个脚本加权限：

```
chmod +x start.sh
```

　　打完收工，你可以直接用它跑了：

```
 ./start.sh 
Stop Process...
Kill Process!
App is NOT running.
Start Success!
```

　　上面是我已经把jar起好了，再次执行start.sh后，它先停掉进程后又拉了起来。可以看下日志

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
tail -30 nohup.out
2019-03-19 10:09:54.447  INFO 25554 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.16]
2019-03-19 10:09:54.462  INFO 25554 --- [           main] o.a.catalina.core.AprLifecycleListener   : The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: [/usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib]
2019-03-19 10:09:54.553  INFO 25554 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-19 10:09:54.553  INFO 25554 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1581 ms
2019-03-19 10:09:54.823  INFO 25554 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-19 10:09:55.038  INFO 25554 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8888 (http) with context path ''
2019-03-19 10:09:55.130  INFO 25554 --- [           main] c.c.springboot.SpringbootApplication     : Started SpringbootApplication in 2.812 seconds (JVM running for 3.304)
2019-03-19 10:10:08.733  INFO 25554 --- [nio-8888-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2019-03-19 10:10:08.733  INFO 25554 --- [nio-8888-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2019-03-19 10:10:08.739  INFO 25554 --- [nio-8888-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 6 ms

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-19 12:47:40.163  INFO 867 --- [           main] c.c.springboot.SpringbootApplication     : Starting SpringbootApplication v0.0.1-SNAPSHOT on iZbp11ahvmlfioymoo7u3bZ with PID 867 (/home/wlf/springboot-0.0.1-SNAPSHOT.jar started by root in /home/wlf)
2019-03-19 12:47:40.166  INFO 867 --- [           main] c.c.springboot.SpringbootApplication     : The following profiles are active: test
2019-03-19 12:47:41.534  INFO 867 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8888 (http)
2019-03-19 12:47:41.572  INFO 867 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-19 12:47:41.572  INFO 867 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.16]
2019-03-19 12:47:41.595  INFO 867 --- [           main] o.a.catalina.core.AprLifecycleListener   : The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: [/usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib]
2019-03-19 12:47:41.695  INFO 867 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-19 12:47:41.695  INFO 867 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1434 ms
2019-03-19 12:47:41.898  INFO 867 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-19 12:47:42.164  INFO 867 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8888 (http) with context path ''
2019-03-19 12:47:42.169  INFO 867 --- [           main] c.c.springboot.SpringbootApplication     : Started SpringbootApplication in 2.637 seconds (JVM running for 3.064)
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　浏览器敲下linux外网ip和端口即可访问hello：

![img](https://img2018.cnblogs.com/blog/1102402/201903/1102402-20190319125339562-546898339.png)