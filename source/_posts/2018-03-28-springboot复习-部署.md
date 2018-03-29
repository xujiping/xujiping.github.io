---
title: 2018-02-05-springboot复习(部署)
date: 2018-03-28 15:01:00
tags: springboot java
---

### 部署到应用服务器  
1. maven中配置
```xml
    <packaging>war</packaging>
```
2. SpringBootServletInitializer是一个支持Spring Boot的Spring WebApplicationInitializer实现。继承SpringBootServletInitializer，覆盖configure方法指定Spring配置类：
```java
    import org.springframework.boot.builder.SpringApplicationBuilder;
    import org.springframework.boot.context.web.SpringBootServletInitializer;
        public class ReadingListServletInitializer extends SpringBootServletInitializer {
            @Override
            protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
                return builder.sources(Application.class);
        }
    }
```  
3. 打包：
```jshelllanguage
mvn package
```
4. 将war包重命名放入tomcat的webapps中。
5. war文件仍然可以直接运行：
```jshelllanguage
java -jar ***.war
```  
