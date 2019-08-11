# *springBoot笔记*
## 1 观察自动生成的springboot项目
### 1.1 了解Application.java
@SpringBootApplication = (默认属性)@Configuration + @EnableAutoConfiguration + @componentScan
- @Configuration：提到@Configuration经常与@Bean组合使用，使用这两个注解就可以创建一个简单的 Spring 配置类，可以用来替代相应的 XML 配置文件。@Configuration的注解类标识这个类可以使用Spring IoC 容器作为 bean 定义的来源。@Bean注解告诉Spring，一个带有@Bean的注解方法将返回一个对象，该对象应该被注册为在Spring应用程序上下文中的bean。
- @EnableAutoConfiguration：能够自动配置 Spring 的上下文，试图猜测和配置你想要的bean类，通常会自动根据你的类路径和你的bean定义自动配置。
- @ComponentScan：会自动扫描指定包下的全部标有@Component的类，并注册成bean，当然也包括@Component下的子注解@Service、@Repository、@Controller。这些bean一般是结合@Autowired构造函数来注入。
### 1.2编写测试用例
```java
@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
public class HelloControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testHello() throws Exception {
        mockMvc.perform(MockMvcRequestBuilders.get("/hello").accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().string(equalTo("Hello World! Welcome to visit waylau.com!")));
    }
}
```
