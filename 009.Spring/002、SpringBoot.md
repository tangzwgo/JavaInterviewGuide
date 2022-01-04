### **1、谈谈@SpringBootApplication注解**

首先看@SpringBootApplication的定义：

```
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
        @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
    @AliasFor(annotation = EnableAutoConfiguration.class)
    Class<?>[] exclude() default {};
    @AliasFor(annotation = EnableAutoConfiguration.class)
    String[] excludeName() default {};
    @AliasFor(annotation = ComponentScan.class, attribute = "basePackages")
    String[] scanBasePackages() default {};
    @AliasFor(annotation = ComponentScan.class, attribute = "basePackageClasses")
    Class<?>[] scanBasePackageClasses() default {};
    @AliasFor(annotation = Configuration.class)
    boolean proxyBeanMethods() default true;
}
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {
    @AliasFor(annotation = Configuration.class)
    boolean proxyBeanMethods() default true;
}
```

从定义中可以看出，@SpringBootApplication注解可以理解成是@Configuration、@EnableAutoConfiguration、@ComponentScan三个注解的合体，这三个注解的作用分别是：

- @Configuration：允许在上下文中注册额外的bean或导入其他配置类；
- @EnableAutoConfiguration：启用SpringBoot的自动配置机制；
- ComponentScan：扫描被@Component (@Service,@Controller)注解的 bean，注解默认会扫描该类所在的包下所有的类。

### **2、SpringBoot自动装配原理？**

https://www.cnblogs.com/javaguide/p/springboot-auto-config.html

SpringBoot 定义了一套接口规范，这套规范规定：SpringBoot 在启动时会扫描外部引用 jar 包中的META-INF/spring.factories文件，将文件中配置的类型信息加载到 Spring 容器（此处涉及到 JVM 类加载机制与 Spring 的容器知识），并执行类中定义的各种操作。对于外部 jar 来说，只需要按照 SpringBoot 定义的标准，就能将自己的功能装置进 SpringBoot。

自动装配的流程：

- 首先从@SpringBootApplication注解开始，@SpringBootApplication注解可以理解成是@Configuration、@EnableAutoConfiguration、@ComponentScan三个注解的合体，其中@EnableAutoConfiguration注解就表示开启自动装配机制。
- @EnableAutoConfiguration注解中会通过@Import注解导入AutoConfigurationImportSelector类，而AutoConfigurationImportSelector类则是实现自动装配的核型。
- AutoConfigurationImportSelector类实现了ImportSelector接口，其中定义了selectImports()方法，该方法的作用就是获取所有符合条件的类的全限定类名，这些类需要被加载到IoC容器中。
- selectImports方法的实现中调用了getAutoConfigurationEntry方法，这个方法主要负责加载自动配置类。
- 第一步：判断自动装配开关是否打开；
- 第二步：获取EnableAutoConfiguration注解中的 exclude 和 excludeName；
- 第三步：获取需要自动装配的所有配置类，读取META-INF/spring.factories；
- 第四步：spring.factories中有很多配置，但是并不是启动时就全部加载，而是会经历依次筛选，只有@ConditionalOnXXX 注解中的条件都满足，该类才会生效。