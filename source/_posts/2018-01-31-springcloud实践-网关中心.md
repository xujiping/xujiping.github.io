---
title: 2018-01-31-springcloud实践(网关中心)
date: 2018-01-31 10:00:49
tags: 
- java
- spring cloud
categories: 
- spring cloud
---

## 网关中心（zuul）

1. pom.xml添加如下配置： 
    ```xml
    <parent>
        <groupId>com.dobi</groupId>
        <artifactId>cloud</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    </parent>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-eureka</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zuul</artifactId>
        </dependency>
    </dependencies>
    ```
2. 主类加上注解 **@EnableZuulProxy**  

3. 配置application.yml  
    ```yaml
    server:
      port: 8810
    spring:
      application:
        name: gateway
    eureka:
      instance:
        hostname: gateway
      client:
        service-url:
          defaultZone: http://localhost:8760/eureka/
    ```
4. 测试  
    访问：http://GATEWAY:GATEWAY_PORT/想要访问的Eureka服务id的小写/**
  
5. 自定义路径配置
    ```yaml
    # 下面整个树都非必须，如果不配置，将默认使用 http://GATEWAY:GATEWAY_PORT/想要访问的Eureka服务id的小写/** 路由到：http://想要访问的Eureka服务id的小写:该服务端口/**
    zuul:
      routes:
        user:                                               # 可以随便写，在zuul上面唯一即可；当这里的值 = service-id时，service-id可以不写。
          path: /user/**                                    # 想要映射到的路径
          service-id: microservice-provider-user            # Eureka中的serviceId
    ```

6. 忽略服务
    ```yaml
    zuul:
      ignored-services: microservice-provider-user          # 需要忽视的服务(配置后将不会被路由)
    ```
    
