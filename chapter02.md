
## 走向自动装配

springboot的自动装配来自于spring的手动装配

### 2-2 手动装配

spring模式注解装配
- `@Component`, `@Service`, `@Configuration`
- `<context:component-scan>` (`2.5`) 或  `@ComponentScan` (`3.1`)
- github wiki 模式注解 <https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model#stereotype-annotations>

### 2-3

通过实例 `FirstLevelRepository`, `SecondLevelRepository` 演示 `@Component` 的层次性("派生性")

### 2-4 

> Spring Framework 手动装配

#### Spring @Enable 模块装配

- 举例 : `@EnableWebMvc`, `@EnableAutoConfiguration`
- 实现 : 注解方式、编程方式

### 2-5

条件装配
- `@Profile`, `@Conditional`

### 2-6

`@Profile` 代码演示

### 2-7

> 2019年4月21日14:49:12，看的有点烦躁了。

基于编程方式实现条件装配
- 这一节有点复杂，看懂了一部分。

### 2-8

Spring Boot 自动装配

`SpringFactoriesLoader`
- "META-INF/spring.factories"
    - spring-boot-autoconfigure-2.0.2.RELEASE.jar

### 2-9

自定义自动装配

### 2-10

















































