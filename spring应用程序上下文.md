# spring的应用程序的上下文

![spring](/Volumes/moveDisk/files/markdown/spring_tutorial/images/屏幕快照 2019-12-19 21.22.54.png)

## 关于上下文常用的接口及其实现

- BeanFactory （基础spring context）
  - DefaultListableBeanFactor
- ApplicationContext （springboot 中的 spring context）
  - ClassPathXmlApplicationContext
  - FileSystemXmlApplicationContext
  - AnnotationConfigApplicationContext
- WebApplicationContext

## web上下文层次

![spring web](/Volumes/moveDisk/files/markdown/spring_tutorial/images/屏幕快照 2019-12-19 21.48.02.png)

**如果要对services以及repository进行aop增强，需要将拦截器放到root层下。**

### 配置web上下文

1.xml方式：

```xml
<web-app>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <context-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>/WEB-INF/app-context.xml</param-name>
    </context-param>
    <servlet>
        <servlet-namme>app</servlet-namme>
        <servlet-class>org.springframework.web.servlet.DispatherServlet</servlet-class>
        <init-param>
            <para-name>contextConfigLocation</para-name>
            <param-value></param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-namme>app</servlet-namme>
        <url-pattern>/app/*</url-pattern>
    </servlet-mapping>
</web-app>
```

2.代码方式：

```java
public class MyWebAppInitializer extends
  AbstractAnnotationConfigDispatcherServletInitializer{
      @Override
      protected Class<?>[] getRootConfigClasses() {
        return new Class<?>[] {RootConfig.class};
      }
      @Override
      protected Class<?>[] getServletConfigClasses() {
        return new Class<?>[] {App1Config.class};
      }
      @Override
      protected String[] getServletMappings() {
        return new String[] {"/app1/*"};
      }
}
```

**上下文举例：**

FooConfig.java：父上下文（parent application context）。
applicationContext.xml：子上下文（child application context）。

FooConfig.java 中定义两个 testBean，分别为 testBeanX(foo) 和 testBeanY(foo)。
applicationContext.xml 定义了一个 testBeanX(bar)。

委托机制：在自己的 context 中找不到 bean，会委托父 context 查找该 bean。

\----------

代码解释：
fooContext.getBean("testBeanX")，在父上下文查找 testBeanX，命中直接返回 testBeanX(foo)。
barContext.getBean("testBeanX")，在子上下文查找 testBeanX，命中直接返回 testBeanX(bar)。
barContext.getBean("testBeanY")，在子上下文查找 testBeanY，未命中；委托父上下文查找，命中，返回 testBeanY(foo)。

\----------

场景一：
父上下文开启 @EnableAspectJAutoProxy 的支持
子上下文未开启 <aop: aspectj-autoproxy />
切面 fooAspect 在 FooConfig.java 定义（父上下文增强）

输出结果：
testBeanX(foo) 和 testBeanY(foo) 均被增强。
testBeanX(bar) 未被增强。

结论：
在父上下文开启了增强，父的 bean 均被增强，而子的 bean 未被增强。

\----------

场景二：
父上下文开启 @EnableAspectJAutoProxy 的支持
子上下文开启 <aop: aspectj-autoproxy />
切面 fooAspect 在 applicationContext.xml 定义（子上下文增加）

输出结果：
testBeanX(foo) 和 testBeanY(foo) 未被增强。
testBeanX(bar) 被增强。

结论：
在子上下文开启增强，父的 bean 未被增强，子的 bean 被增强。

\----------

根据场景一和场景二的结果，有结论：“各个 context 相互独立，每个 context 的 aop 增强只对本 context 的 bean 生效”。如果想将切面配置成通用的，对父和子上下文的 bean 均支持增强，则：
\1. 切面 fooAspect 定义在父上下文。
\2. 父上下文和子上下文，均要开启 aop 的增加，即 @EnableAspectJAutoProxy 或<aop: aspectj-autoproxy /> 的支持。