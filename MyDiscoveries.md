

## @ResponseBody

- `@ResponseBody` 的源码非常简洁(大多数注解都是这样的)
- 在 IDEA 使用 `Alt + F7`, 发现 `RequestResponseBodyMethodProcessor#supportsReturnType`
- 对 `supportsReturnType` 使用 `Alt + F7` 会定位到
    - `HandlerMethodReturnValueHandlerComposite`,
    - `ModelAndViewResolverMethodReturnValueHandler`






