## 热部署

当我们修改文件和创建文件时，都需要重新启动项目。这样频繁的操作很浪费时间，配置热部署可以让项目自动加载变化的文件，省去的手动操作。

在 pom.xml 文件中添加如下配置：

```xml
<!-- 热部署 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
    <scope>true</scope>
</dependency>
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <!-- 没有该配置，devtools 不生效 -->
                <fork>true</fork>
            </configuration>
        </plugin>
    </plugins>
</build>
```

配置好 pom.xml 文件后，我们启动项目，随便创建/修改一个文件并保存，会发现控制台打印 springboot 重新加载文件的信息。



## 多环境切换

application.properties 是 springboot 在运行中所需要的配置信息。

当我们在开发阶段，使用自己的机器开发，测试的时候需要用的测试服务器测试，上线时使用正式环境的服务器。

这三种环境需要的配置信息都不一样，当我们切换环境运行项目时，需要手动的修改多出配置信息，非常容易出错。

为了解决上述问题，springboot 提供多环境配置的机制，让开发者非常容易的根据需求而切换不同的配置环境。

在 src/main/resources 目录下创建三个配置文件:

```
application-dev.properties：用于开发环境
application-test.properties：用于测试环境
application-prod.properties：用于生产环境
```

我们可以在这个三个配置文件中设置不同的信息，application.properties 配置公共的信息。

在 application.properties 中配置：

```properties
spring.profiles.active=dev
```

表示激活 application-dev.properties 文件配置， springboot 会加载使用 application.properties 和 application-dev.properties 配置文件的信息。

同理，可将 spring.profiles.active 的值修改成 test 或 prod 达到切换环境的目的。



## 配置日志

### 5.1 配置 logback（官方推荐使用）

#### 5.1.1 配置日志文件

spring boot 默认会加载 classpath:logback-spring.xml 或者 classpath:logback-spring.groovy。

如需要自定义文件名称，在 application.properties 中配置 logging.config 选项即可。

在 src/main/resources 下创建 logback-spring.xml 文件，内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- 文件输出格式 -->
    <property name="PATTERN" value="%-12(%d{yyyy-MM-dd HH:mm:ss.SSS}) |-%-5level [%thread] %c [%L] -| %msg%n" />
    <!-- test文件路径 -->
    <property name="TEST_FILE_PATH" value="d:/test.log" />
    <!-- pro文件路径 -->
    <property name="PRO_FILE_PATH" value="/opt/test/log" />
    
    <!-- 开发环境 -->
    <springProfile name="dev">
        <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
            <encoder>
                <pattern>${PATTERN}</pattern>
            </encoder>
        </appender>
        <logger name="com.light.springboot" level="debug" />
        <root level="info">
            <appender-ref ref="CONSOLE" />
        </root>
    </springProfile>
    
    <!-- 测试环境 -->
    <springProfile name="test">
        <!-- 每天产生一个文件 -->
        <appender name="TEST-FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
            <!-- 文件路径 -->
            <file>${TEST_FILE_PATH}</file>
            <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
                <!-- 文件名称 -->
                <fileNamePattern>${TEST_FILE_PATH}/info.%d{yyyy-MM-dd}.log</fileNamePattern>
                <!-- 文件最大保存历史数量 -->
                <MaxHistory>100</MaxHistory>
            </rollingPolicy>
            <layout class="ch.qos.logback.classic.PatternLayout">
                <pattern>${PATTERN}</pattern>
            </layout>
        </appender>
        <root level="info">
            <appender-ref ref="TEST-FILE" />
        </root>
    </springProfile>
    
    <!-- 生产环境 -->
    <springProfile name="prod">
        <appender name="PROD_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
            <file>${PRO_FILE_PATH}</file>
            <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
                <fileNamePattern>${PRO_FILE_PATH}/warn.%d{yyyy-MM-dd}.log</fileNamePattern>
                <MaxHistory>100</MaxHistory>
            </rollingPolicy>
            <layout class="ch.qos.logback.classic.PatternLayout">
                <pattern>${PATTERN}</pattern>
            </layout>
        </appender>
        <root level="warn">
            <appender-ref ref="PROD_FILE" />
        </root>
    </springProfile>
</configuration>
```

其中，springProfile 标签的 name 属性对应 application.properties 中的 spring.profiles.active 的配置。

即 spring.profiles.active 的值可以看作是日志配置文件中对应的 springProfile 是否生效的开关。



###  5.2 配置 log4j2

#### 5.2.1 添加依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-log4j2</artifactId>
</dependency>
```

#### 5.2.2 配置日志文件

spring boot 默认会加载 classpath:log4j2.xml 或者 classpath:log4j2-spring.xml。

如需要自定义文件名称，在 application.properties 中配置 logging.config 选项即可。

log4j2.xml 文件内容如下：

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <properties>
        <!-- 文件输出格式 -->
        <property name="PATTERN">%d{yyyy-MM-dd HH:mm:ss.SSS} |-%-5level [%thread] %c [%L] -| %msg%n</property>
    </properties>
    <appenders>
        <Console name="CONSOLE" target="system_out">
            <PatternLayout pattern="${PATTERN}" />
        </Console>
    </appenders>
    <loggers>
        <logger name="com.light.springboot" level="debug" />
        <root level="info">
            <appenderref ref="CONSOLE" />
        </root>
    </loggers>
</configuration>
```

log4j2 不能像 logback 那样在一个文件中设置多个环境的配置数据，只能命名 3 个不同名的日志文件，分别在 application-dev，application-test 和 application-prod 中配置 logging.config 选项。

级别：debug、info、warn、error、严重

除了在日志配置文件中设置参数之外，还可以在 application-*.properties 中设置，日志相关的配置：

```
logging.config                    # 日志配置文件路径，如 classpath:logback-spring.xml
logging.exception-conversion-word # 记录异常时使用的转换词
logging.file                      # 记录日志的文件名称，如：test.log
logging.level.*                   # 日志映射，如：logging.level.root=WARN，logging.level.org.springframework.web=DEBUG
logging.path                      # 记录日志的文件路径，如：d:/
logging.pattern.console           # 向控制台输出的日志格式，只支持默认的 logback 设置。
logging.pattern.file              # 向记录日志文件输出的日志格式，只支持默认的 logback 设置。
logging.pattern.level             # 用于呈现日志级别的格式，只支持默认的 logback 设置。
logging.register-shutdown-hook    # 初始化时为日志系统注册一个关闭钩子
```

## 打包运行

打包的形式有两种：jar 和 war。

### 6.1 打包成可执行的 jar 包

默认情况下，通过 maven 执行 package 命令后，会生成 jar 包，且该 jar 包会内置了 tomcat 容器，因此我们可以通过 java -jar 就可以运行项目，如下图：

![image](http://images.extlight.com/springboot-basic-6-2.jpg)

### 6.2 打包成部署的 war 包

让 SpringbootApplication 类继承 SpringBootServletInitializer 并重写 configure 方法，如下：

```
@SpringBootApplication
public class SpringbootApplication extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(SpringbootApplication.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(SpringbootApplication.class, args);
    }
}
```

修改 pom.xml 文件，将 jar 改成 war，如下：

```
<packaging>war</packaging>
```

打包成功后，将 war 包部署到 tomcat 容器中运行即可。





