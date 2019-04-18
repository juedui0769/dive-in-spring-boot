
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






































