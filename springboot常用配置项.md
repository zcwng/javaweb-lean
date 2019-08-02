## mvc

- spring.mvc.async.request-timeout
  设定async请求的超时时间，以毫秒为单位，如果没有设置的话，以具体实现的超时时间为准，比如tomcat的servlet3的话是10秒.
- spring.mvc.date-format
  设定日期的格式，比如dd/MM/yyyy.
- spring.mvc.favicon.enabled
  是否支持favicon.ico，默认为: true
- spring.mvc.ignore-default-model-on-redirect
  在重定向时是否忽略默认model的内容，默认为true
- spring.mvc.locale
  指定使用的Locale.
- spring.mvc.message-codes-resolver-format
  指定message codes的格式化策略(PREFIX_ERROR_CODE,POSTFIX_ERROR_CODE).
- spring.mvc.view.prefix
  指定mvc视图的前缀.
- spring.mvc.view.suffix
  指定mvc视图的后缀.





## messages

- spring.messages.basename
  指定message的basename，多个以逗号分隔，如果不加包名的话，默认从classpath路径开始，默认: messages
- spring.messages.cache-seconds
  设定加载的资源文件缓存失效时间，-1的话为永不过期，默认为-1
- spring.messages.encoding
  设定Message bundles的编码，默认: UTF-8





## mobile

- spring.mobile.devicedelegatingviewresolver.enable-fallback
  是否支持fallback的解决方案，默认false
- spring.mobile.devicedelegatingviewresolver.enabled
  是否开始device view resolver，默认为: false
- spring.mobile.devicedelegatingviewresolver.mobile-prefix
  设定mobile端视图的前缀，默认为:mobile/
- spring.mobile.devicedelegatingviewresolver.mobile-suffix
  设定mobile视图的后缀
- spring.mobile.devicedelegatingviewresolver.normal-prefix
  设定普通设备的视图前缀
- spring.mobile.devicedelegatingviewresolver.normal-suffix
  设定普通设备视图的后缀
- spring.mobile.devicedelegatingviewresolver.tablet-prefix
  设定平板设备视图前缀，默认:tablet/
- spring.mobile.devicedelegatingviewresolver.tablet-suffix
  设定平板设备视图后缀.
- spring.mobile.sitepreference.enabled
  是否启用SitePreferenceHandler，默认为: true





## view

- spring.view.prefix
  设定mvc视图的前缀.
- spring.view.suffix
  设定mvc视图的后缀.





## resource

- spring.resources.add-mappings
  是否开启默认的资源处理，默认为true
- spring.resources.cache-period
  设定资源的缓存时效，以秒为单位.
- spring.resources.chain.cache
  是否开启缓存，默认为: true
- spring.resources.chain.enabled
  是否开启资源 handling chain，默认为false
- spring.resources.chain.html-application-cache
  是否开启h5应用的cache manifest重写，默认为: false
- spring.resources.chain.strategy.content.enabled
  是否开启内容版本策略，默认为false
- spring.resources.chain.strategy.content.paths
  指定要应用的版本的路径，多个以逗号分隔，默认为:[/**]
- spring.resources.chain.strategy.fixed.enabled
  是否开启固定的版本策略，默认为false
- spring.resources.chain.strategy.fixed.paths
  指定要应用版本策略的路径，多个以逗号分隔
- spring.resources.chain.strategy.fixed.version
  指定版本策略使用的版本号
- spring.resources.static-locations
  指定静态资源路径，默认为classpath:[/META-INF/resources/,/resources/, /static/, /public/]以及context:/





## multipart

- multipart.enabled
  是否开启文件上传支持，默认为true
- multipart.file-size-threshold
  设定文件写入磁盘的阈值，单位为MB或KB，默认为0
- multipart.location
  指定文件上传路径.
- multipart.max-file-size
  指定文件大小最大值，默认1MB
- multipart.max-request-size
  指定每次请求的最大值，默认为10MB

```
#配置文件传输
spring.servlet.multipart.enabled =true  
spring.servlet.multipart.file-size-threshold =0
#单个数据的大小
spring.servlet.multipart.max-file-size = 100Mb
#总数据的大小
spring.servlet.multipart.max-request-size=100Mb


版本1.5.17：
spring.http.multipart.maxFileSize=10MB
spring.http.multipart.maxRequestSize=10MB


```



## freemarker

- spring.freemarker.allow-request-override
  指定HttpServletRequest的属性是否可以覆盖controller的model的同名项
- spring.freemarker.allow-session-override
  指定HttpSession的属性是否可以覆盖controller的model的同名项
- spring.freemarker.cache
  是否开启template caching.
- spring.freemarker.charset
  设定Template的编码.
- spring.freemarker.check-template-location
  是否检查templates路径是否存在.
- spring.freemarker.content-type
  设定Content-Type.
- spring.freemarker.enabled
  是否允许mvc使用freemarker.
- spring.freemarker.expose-request-attributes
  设定所有request的属性在merge到模板的时候，是否要都添加到model中.
- spring.freemarker.expose-session-attributes
  设定所有HttpSession的属性在merge到模板的时候，是否要都添加到model中.
- spring.freemarker.expose-spring-macro-helpers
  设定是否以springMacroRequestContext的形式暴露RequestContext给Spring’s macro library使用
- spring.freemarker.prefer-file-system-access
  是否优先从文件系统加载template，以支持热加载，默认为true
- spring.freemarker.prefix
  设定freemarker模板的前缀.
- spring.freemarker.request-context-attribute
  指定RequestContext属性的名.
- spring.freemarker.settings
  设定FreeMarker keys.
- spring.freemarker.suffix
  设定模板的后缀.
- spring.freemarker.template-loader-path
  设定模板的加载路径，多个以逗号分隔，默认: ["classpath:/templates/"]
- spring.freemarker.view-names
  指定使用模板的视图列表.





## velocity

- spring.velocity.allow-request-override
  指定HttpServletRequest的属性是否可以覆盖controller的model的同名项
- spring.velocity.allow-session-override
  指定HttpSession的属性是否可以覆盖controller的model的同名项
- spring.velocity.cache
  是否开启模板缓存
- spring.velocity.charset
  设定模板编码
- spring.velocity.check-template-location
  是否检查模板路径是否存在.
- spring.velocity.content-type
  设定ContentType的值
- spring.velocity.date-tool-attribute
  设定暴露给velocity上下文使用的DateTool的名
- spring.velocity.enabled
  设定是否允许mvc使用velocity
- spring.velocity.expose-request-attributes
  是否在merge模板的时候，将request属性都添加到model中
- spring.velocity.expose-session-attributes
  是否在merge模板的时候，将HttpSession属性都添加到model中
- spring.velocity.expose-spring-macro-helpers
  设定是否以springMacroRequestContext的名来暴露RequestContext给Spring’s macro类库使用
- spring.velocity.number-tool-attribute
  设定暴露给velocity上下文的NumberTool的名
- spring.velocity.prefer-file-system-access
  是否优先从文件系统加载模板以支持热加载，默认为true
- spring.velocity.prefix
  设定velocity模板的前缀.
- spring.velocity.properties
  设置velocity的额外属性.
- spring.velocity.request-context-attribute
  设定RequestContext attribute的名.
- spring.velocity.resource-loader-path
  设定模板路径，默认为: classpath:/templates/
- spring.velocity.suffix
  设定velocity模板的后缀.
- spring.velocity.toolbox-config-location
  设定Velocity Toolbox配置文件的路径，比如 /WEB-INF/toolbox.xml.
- spring.velocity.view-names
  设定需要解析的视图名称.





## thymeleaf

- spring.thymeleaf.cache
  是否开启模板缓存，默认true
- spring.thymeleaf.check-template-location
  是否检查模板路径是否存在，默认true
- spring.thymeleaf.content-type
  指定Content-Type，默认为: text/html
- spring.thymeleaf.enabled
  是否允许MVC使用Thymeleaf，默认为: true
- spring.thymeleaf.encoding
  指定模板的编码，默认为: UTF-8
- spring.thymeleaf.excluded-view-names
  指定不使用模板的视图名称，多个以逗号分隔.
- spring.thymeleaf.mode
  指定模板的模式，具体查看StandardTemplateModeHandlers，默认为: HTML5
- spring.thymeleaf.prefix
  指定模板的前缀，默认为:classpath:/templates/
- spring.thymeleaf.suffix
  指定模板的后缀，默认为:.html
- spring.thymeleaf.template-resolver-order
  指定模板的解析顺序，默认为第一个.
- spring.thymeleaf.view-names
  指定使用模板的视图名，多个以逗号分隔.





## mustcache

- spring.mustache.cache
  是否Enable template caching.
- spring.mustache.charset
  指定Template的编码.
- spring.mustache.check-template-location
  是否检查默认的路径是否存在.
- spring.mustache.content-type
  指定Content-Type.
- spring.mustache.enabled
  是否开启mustcache的模板支持.
- spring.mustache.prefix
  指定模板的前缀，默认: classpath:/templates/
- spring.mustache.suffix
  指定模板的后缀，默认: .html
- spring.mustache.view-names
  指定要使用模板的视图名.





## groovy模板

- spring.groovy.template.allow-request-override
  指定HttpServletRequest的属性是否可以覆盖controller的model的同名项
- spring.groovy.template.allow-session-override
  指定HttpSession的属性是否可以覆盖controller的model的同名项
- spring.groovy.template.cache
  是否开启模板缓存.
- spring.groovy.template.charset
  指定Template编码.
- spring.groovy.template.check-template-location
  是否检查模板的路径是否存在.
- spring.groovy.template.configuration.auto-escape
  是否在渲染模板时自动排查model的变量，默认为: false
- spring.groovy.template.configuration.auto-indent
  是否在渲染模板时自动缩进，默认为false
- spring.groovy.template.configuration.auto-indent-string
  如果自动缩进启用的话，是使用SPACES还是TAB，默认为: SPACES
- spring.groovy.template.configuration.auto-new-line
  渲染模板时是否要输出换行，默认为false
- spring.groovy.template.configuration.base-template-class
  指定template base class.
- spring.groovy.template.configuration.cache-templates
  是否要缓存模板，默认为true
- spring.groovy.template.configuration.declaration-encoding
  在写入declaration header时使用的编码
- spring.groovy.template.configuration.expand-empty-elements
  是使用`<br/>`这种形式，还是`<br></br>`这种展开模式，默认为: false)
- spring.groovy.template.configuration.locale
  指定template locale.
- spring.groovy.template.configuration.new-line-string
  当启用自动换行时，换行的输出，默认为系统的line.separator属性的值
- spring.groovy.template.configuration.resource-loader-path
  指定groovy的模板路径，默认为classpath:/templates/
- spring.groovy.template.configuration.use-double-quotes
  指定属性要使用双引号还是单引号，默认为false
- spring.groovy.template.content-type
  指定Content-Type.
- spring.groovy.template.enabled
  是否开启groovy模板的支持.
- spring.groovy.template.expose-request-attributes
  设定所有request的属性在merge到模板的时候，是否要都添加到model中.
- spring.groovy.template.expose-session-attributes
  设定所有request的属性在merge到模板的时候，是否要都添加到model中.
- spring.groovy.template.expose-spring-macro-helpers
  设定是否以springMacroRequestContext的形式暴露RequestContext给Spring’s macro library使用
- spring.groovy.template.prefix
  指定模板的前缀.
- spring.groovy.template.request-context-attribute
  指定RequestContext属性的名.
- spring.groovy.template.resource-loader-path
  指定模板的路径，默认为: classpath:/templates/
- spring.groovy.template.suffix
  指定模板的后缀
- spring.groovy.template.view-names
  指定要使用模板的视图名称.





## http

- spring.hateoas.apply-to-primary-object-mapper
  设定是否对object mapper也支持HATEOAS，默认为: true
- spring.http.converters.preferred-json-mapper
  是否优先使用JSON mapper来转换.
- spring.http.encoding.charset
  指定http请求和相应的Charset，默认: UTF-8
- spring.http.encoding.enabled
  是否开启http的编码支持，默认为true
- spring.http.encoding.force
  是否强制对http请求和响应进行编码，默认为true





## json

- spring.jackson.date-format
  指定日期格式，比如yyyy-MM-dd HH:mm:ss，或者具体的格式化类的全限定名
- spring.jackson.deserialization
  是否开启Jackson的反序列化
- spring.jackson.generator
  是否开启json的generators.
- spring.jackson.joda-date-time-format
  指定Joda date/time的格式，比如yyyy-MM-dd HH:mm:ss). 如果没有配置的话，dateformat会作为backup
- spring.jackson.locale
  指定json使用的Locale.
- spring.jackson.mapper
  是否开启Jackson通用的特性.
- spring.jackson.parser
  是否开启jackson的parser特性.
- spring.jackson.property-naming-strategy
  指定PropertyNamingStrategy (CAMEL_CASE_TO_LOWER_CASE_WITH_UNDERSCORES)或者指定PropertyNamingStrategy子类的全限定类名.
- spring.jackson.serialization
  是否开启jackson的序列化.
- spring.jackson.serialization-inclusion
  指定序列化时属性的inclusion方式，具体查看JsonInclude.Include枚举.
- spring.jackson.time-zone
  指定日期格式化时区，比如America/Los_Angeles或者GMT+10.





## jersey

- spring.jersey.filter.order
  指定Jersey filter的order，默认为: 0
- spring.jersey.init
  指定传递给Jersey的初始化参数.
- spring.jersey.type
  指定Jersey的集成类型，可以是servlet或者filter.

## server配置

- server.address
  指定server绑定的地址
- server.compression.enabled
  是否开启压缩，默认为false.
- server.compression.excluded-user-agents
  指定不压缩的user-agent，多个以逗号分隔，默认值为:text/html,text/xml,text/plain,text/css
- server.compression.mime-types
  指定要压缩的MIME type，多个以逗号分隔.
- server.compression.min-response-size
  执行压缩的阈值，默认为2048
- server.context-parameters.[param name]
  设置servlet context 参数
- server.context-path
  设定应用的context-path.
- server.display-name
  设定应用的展示名称，默认: application
- server.jsp-servlet.class-name
  设定编译JSP用的servlet，默认: org.apache.jasper

.servlet.JspServlet)

- server.jsp-servlet.init-parameters.[param name]
  设置JSP servlet 初始化参数.
- server.jsp-servlet.registered
  设定JSP servlet是否注册到内嵌的servlet容器，默认true
- server.port
  设定http监听端口
- server.servlet-path
  设定dispatcher servlet的监听路径，默认为: /

## cookie、session配置

- server.session.cookie.comment
  指定session cookie的comment
- server.session.cookie.domain
  指定session cookie的domain
- server.session.cookie.http-only
  是否开启HttpOnly.
- server.session.cookie.max-age
  设定session cookie的最大age.
- server.session.cookie.name
  设定Session cookie 的名称.
- server.session.cookie.path
  设定session cookie的路径.
- server.session.cookie.secure
  设定session cookie的“Secure” flag.
- server.session.persistent
  重启时是否持久化session，默认false
- server.session.timeout
  session的超时时间
- server.session.tracking-modes
  设定Session的追踪模式(cookie, url, ssl).

## ssl配置

- server.ssl.ciphers
  是否支持SSL ciphers.
- server.ssl.client-auth
  设定client authentication是wanted 还是 needed.
- server.ssl.enabled
  是否开启ssl，默认: true
- server.ssl.key-alias
  设定key store中key的别名.
- server.ssl.key-password
  访问key store中key的密码.
- server.ssl.key-store
  设定持有SSL certificate的key store的路径，通常是一个.jks文件.
- server.ssl.key-store-password
  设定访问key store的密码.
- server.ssl.key-store-provider
  设定key store的提供者.
- server.ssl.key-store-type
  设定key store的类型.
- server.ssl.protocol
  使用的SSL协议，默认: TLS
- server.ssl.trust-store
  持有SSL certificates的Trust store.
- server.ssl.trust-store-password
  访问trust store的密码.
- server.ssl.trust-store-provider
  设定trust store的提供者.
- server.ssl.trust-store-type
  指定trust store的类型.

## tomcat

- server.tomcat.access-log-enabled
  是否开启access log ，默认: false)
- server.tomcat.access-log-pattern
  设定access logs的格式，默认: common
- server.tomcat.accesslog.directory
  设定log的目录，默认: logs
- server.tomcat.accesslog.enabled
  是否开启access log，默认: false
- server.tomcat.accesslog.pattern
  设定access logs的格式，默认: common
- server.tomcat.accesslog.prefix
  设定Log 文件的前缀，默认: access_log
- server.tomcat.accesslog.suffix
  设定Log 文件的后缀，默认: .log
- server.tomcat.background-processor-delay
  后台线程方法的Delay大小: 30
- server.tomcat.basedir
  设定Tomcat的base 目录，如果没有指定则使用临时目录.
- server.tomcat.internal-proxies
  设定信任的正则表达式，默认:“10\.\d{1,3}\.\d{1,3}\.\d{1,3}| 192\.168\.\d{1,3}\.\d{1,3}| 169\.254\.\d{1,3}\.\d{1,3}| 127\.\d{1,3}\.\d{1,3}\.\d{1,3}| 172\.1[6-9]{1}\.\d{1,3}\.\d{1,3}| 172\.2[0-9]{1}\.\d{1,3}\.\d{1,3}|172\.3[0-1]{1}\.\d{1,3}\.\d{1,3}”
- server.tomcat.max-http-header-size
  设定http header的最小值，默认: 0
- server.tomcat.max-threads
  设定tomcat的最大工作线程数，默认为: 0
- server.tomcat.port-header
  设定http header使用的，用来覆盖原来port的value.
- server.tomcat.protocol-header
  设定Header包含的协议，通常是 X-Forwarded-Proto，如果remoteIpHeader有值，则将设置为RemoteIpValve.
- server.tomcat.protocol-header-https-value
  设定使用SSL的header的值，默认https.
- server.tomcat.remote-ip-header
  设定remote IP的header，如果remoteIpHeader有值，则设置为RemoteIpValve
- server.tomcat.uri-encoding
  设定URI的解码字符集.

## undertow

- - server.undertow.access-log-dir
    设定Undertow access log 的目录，默认: logs
  - server.undertow.access-log-enabled
    是否开启access log，默认: false
  - server.undertow.access-log-pattern
    设定access logs的格式，默认: common
  - server.undertow.accesslog.dir
    设定access log 的目录.
  - server.undertow.buffer-size
    设定buffer的大小.
  - server.undertow.buffers-per-region
    设定每个region的buffer数
  - server.undertow.direct-buffers
    设定堆外内存
  - server.undertow.io-threads
    设定I/O线程数.
  - server.undertow.worker-threads
    设定工作线程数

## datasource

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.datasource.username=root
spring.datasource.password=123456
```



```
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQL5Dialect
```