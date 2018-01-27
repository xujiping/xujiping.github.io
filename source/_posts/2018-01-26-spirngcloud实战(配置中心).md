---
title: spring cloud实战 2-配置中心
date: 2018-01-26
tags: 
- java
- spring cloud
categories: 
- spring cloud
---

1. 修改hosts文件C:\WINDOWS\system32\drivers\etc\hosts:  

    127.0.0.1 config-server  
    
2. git仓库中创建配置文件：  
    创建配置文件：config-server-dev.properties  
      
```properties
profile=dev-1.0  
    foo=test    
```
3. pom.xml  

```xml
<dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-server</artifactId>
    </dependency>
```

4. 启动类增加注解：@EnableConfigServer  

5. 配置文件增加git仓库配置： 
    
```yaml
spring:
    cloud:
        config:
        server:
            git:
                uri: https://github.com/eacdy/spring-cloud-study/     # 配置git仓库的地址
                search-paths: config-repo                             # git仓库地址下的相对地址，可以配置多个，用,分割。
                username:                                             # git仓库的账号
                password:    # git仓库的密码
```
              
6. 访问http://config-server:8800/config-client-dev.properties  



