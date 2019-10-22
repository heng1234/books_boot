# springboot访问路径配置和Profile配置说明

### Spring Boot匹配指定后缀*.action *.do的路径访问

(项目地址:https://github.com/heng1234/springboot2.x/tree/master/boot_banner_yml)

新建个配置文件MyWebMvcConfigurer

```java
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.DispatcherServlet;
import org.springframework.web.servlet.config.annotation.PathMatchConfigurer;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

/**
 * @author : kaifa
 * create at:  2019-10-18  17:07
 * @description: WebMvcConfigurer配置类
 */
@Configuration
public class MyWebMvcConfigurer implements WebMvcConfigurer {
    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        //开启路径后缀匹配
        configurer.setUseRegisteredSuffixPatternMatch(true);
    }
    /**
     * 设置匹配*.action后缀请求
     * @param dispatcherServlet
     * @return
     */
    @Bean
    public ServletRegistrationBean servletRegistrationBean(DispatcherServlet dispatcherServlet) {
        ServletRegistrationBean<DispatcherServlet> servletServletRegistrationBean = new ServletRegistrationBean<>(dispatcherServlet);
        servletServletRegistrationBean.addUrlMappings("*.action","*.do");
        return servletServletRegistrationBean;
    }

}
```

只有后缀是.action 和.do的才能访问controller到





## Profile配置

Profile用来针对不同的环境下使用不同的配置文件，多环境配置文件必须以`application-{profile}.properties`的格式命，其中`{profile}`为环境标识。比如定义两个配置文件：

- application-dev.properties：开发环境

  ```
  server.port=8080
  ```

- application-prod.properties：生产环境

  ```
  server.port=8081
  ```

至于哪个具体的配置文件会被加载，需要在application.properties文件中通过`spring.profiles.active`属性来设置，其值对应`{profile}`值。

如：`spring.profiles.active=dev`就会加载application-dev.properties配置文件内容。可以在运行jar文件的时候使用命令`java -jar xxx.jar --spring.profiles.active={profile}`切换不同的环境配置。



[下一章:pringboot2.x集成mybatis(druid+xml方式)](../mybatis/mybatis.md)