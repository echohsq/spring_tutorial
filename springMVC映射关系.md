# 定义映射关系

**@Controller**

**@RequestMapping**

- path / method指定映射路径与方法
- params / headers 限定映射范围
- Consumes / produces 限定请求与响应格式

**一些快捷方式**

- RestController
- @GetMapping / @PostMapping / @PutMapping / @DeleteMapping / @PatchMapping

# 定义处理方法

- @RequestBody请求响应 / @ResponseBody回复响应 / @ResponseStatus 回复状态码
- @PathVariable / @RequestParam / @RequestHeader  (定义参数)
- HttpEntity / ReponseEntity

**详细参数**

- Https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-arguments

**详细返回**

- Https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-return-types