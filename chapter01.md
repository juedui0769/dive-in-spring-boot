# chapter01.md

## 1-5

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













