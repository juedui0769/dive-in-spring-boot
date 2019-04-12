# chapter01.md

## 1-5

- <https://docs.spring.io/spring-boot/docs/2.0.9.RELEASE/reference/htmlsingle/#getting-started-first-application-code>
    - 视频中老师打开的文档页面已经找不到了。但是上面的连接可以打开，差不多！
- 视频中老师打开的页面是 <https://projects.spring.io/spring-boot>

### 注解
- `@EnableAutoConfiguration`
- `@SpringBootApplication`
    - `@SpringBootApplication` 包含 `@EnableAutoConfiguration` 注解

### spring.factories
- IDEA shortcut `ctrl + shift + N` 搜索 `spring.factories`
    - 会有很多
- 选择来自 `spring-boot-autoconfig-xxx-RELEASE.jar` 中的， 会发现所有和 `EnableAutoConfiguration` 相关的类都列举在这里。
    - 比如 `WebMvcAutoConfiguration` , `Ctrl + N` 可以定位到这个类

### actuator
- 监控相关

## 1-6

- 没什么价值

## 1-7

### 传统servlet应用

- ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  ```
- 传统servlet应用，需要添加上面的依赖，spirngboot中的子模块都是以`spring-boot-starter-`开头的。

### Whitelabel Error Page

- This application has no explicit mapping for /error, so you are seeing this as a fallback.

### 代码

- **实现** : 使用 `@WebServlet`
- 子包 `web.servlet` , 完整包名 `com.imooc.diveinspringboot.web.servlet`
- ```java
  @WebServlet(urlPatterns = "/my/servlet")
  public class MyServlet extends HttpServlet {
      //...
  }
  ```
- **注册** : 使用`@ServletComponentScan`, 如下 (下面类位于上次目录，包名为`com.imooc.diveinspringboot`)
- ```java
  @SpringBootApplication
  @ServletComponentScan(basePackages = "com.imooc.diveinspringboot.web.servlet")
  public class DiveInSpringBootApplication {
      // ...
  }
  ```

## 1-8

### 异步Servlet

```java
@WebServlet(urlPatterns = "/my/servlet",
    asyncSupported=true)
public class MyServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
        throws ServletException, IOException {

        AsyncContext ctx = req.startAsync();

        ctx.start(() -> {
            try {
                resp.getWriter().println("Hello, World");
                ctx.complete();
            } catch(IOException e) {
                e.printStackTrace();
            }
        });
    }
}
```

- 以上代码有几个关注点
    - 注解中需要设置 `asyncSupported=true` 以表示支持异步, 默认是`false`
    - 异步的写法完全不同， `req.startAsync()` 有点像 `Thread.start()`
    - `ctx.complete();` 这句非常关键，放到 `try{}finally{ ctx.complete(); }` 是最好的，表明完成任务后主动触发'complete'

## 1-9

### ViewResolver

- `ViewResolver` 位于 `org.springframework.web.servlet` 包下，
- 项目中有多个模板引擎共存时，需要'内容协商' `ContentNegotiatingViewResolver`

### 异常处理

- `@ExceptionHandler`
- `HandlerExceptionResolver` , `ExceptionHandlerExceptionResolver`
- `BasicErrorController`
    - 'Whitelabel Error Page' 就是由这个类产生的？

### 资源服务

- @RequstMapping
    - @GetMapping, @PostMapping, @PutMapping, @DeleteMapping
- @ResponseBody
- @RequestBoby

### 资源跨域

- 传统解决方案
    - iframe
    - JSONP
- `@CrossOrigin` : 注解驱动
- `WebMvcConfigurer#addCorsMappings` : 接口编程

## 1-10 WebFlux

- Reactor基础 ： Java Lambda , Mono, Flux

- Web Flux核心： Web MVC注解、函数式声明、异步非阻塞

- 使用场景： Web Flux 优势和限制

## 1-11 Web Server

tomcat, jetty, 

`WebServerFactoryCustomizer` : 这个接口是 `2.0` 才添加的, 它是一个总接口，既包含传统的tomcat、jetty，又包含WebFlux
- `TomcatServletWebServerFactoryCustomizer`
- `ReactiveWebServerFactoryCustomizer`
- ...

## 1-12 数据相关

- JDBC

- JPA
- 事务

可以在`spring.factories`(spring-boot-autoconfigure)中找到下面的配置

```
org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JdbcTemplateAutoConfiguration,\
```

视频中使用的`transction`是下面的依赖。

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
</dependency>
```

在2.9.0官方文档中，[38. Distributed Transactions with JTA](https://docs.spring.io/spring-boot/docs/2.0.9.RELEASE/reference/htmlsingle/#boot-features-jta)
使用的不一样。可以选择
- `spring-boot-starter-jta-atomikos`
- `spring-boot-starter-jta-bitronix`
- `spring-boot-starter-jta-narayana`
可以在文档中搜索'transaction'了解更多内容。

## 1-13 功能扩展

- Spring Application 失败分析、事件监听
- 外部化配置、Profile、配置属性
- Starter开发、最佳实践

`FailureAnalysisReporter`

`SpringApplication.run(clazz, args)` -> `new SpringApplicationBuilder(clazz).run(args)`

### 外部化配置

`2.0`之前使用 `PropertySources`, `2.0`之后使用 `ConfigurationProperty`
- `PropertySources` 有两个，一个是接口，一个是注解。

[24. Externalized Configuration](https://docs.spring.io/spring-boot/docs/2.0.1.RELEASE/reference/htmlsingle/#boot-features-external-config)
- 这节文档中列举了`17`配置（小马哥说不止17种）

`@Profile` -> `@Conditional` : 又profile进化为conditional

## 1-14 运维管理

Spring Boot Actuator
- 端点 ： web endpoints , JMX endpoints
- 健康检查
- 指标 metrics

`application.properties`开放所有的 Web Endpoints, 如下(可以在官方文档中搜索)

```
management.endpoints.web.exposure.include=*
```


## end

chapter01 完结