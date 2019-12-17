# Spring MVC

## 编写第一个Spring MVC Controller

### 认识Spring MVC

**DispatcherServlet（请求入口）**

- Controller （每个请求怎样去处理它的一个逻辑）
- xxxResolver（各种解析器）
  - ViewResolver
  - HandlerExceptionResolver
  - MultipartResolver
- HandlerMapping（处理请求如何映射到Controller上面）

### Spring MVC中的常用注解

- @Controller（控制器）
  - @RestController
- @RequestMapping（映射器）
  - @GetMapping / @PostMapping
  - @PutMapping / @DeleteMapping
- @RequestBody / @ResponseBody / @ResponseStatus（请求报文相关）