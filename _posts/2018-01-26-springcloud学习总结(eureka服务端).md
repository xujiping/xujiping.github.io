## 创建父maven项目  
<img src="/img/cloud1-1.png" />

## 提交代码至GitHub
<img src="/img/cloud1-2.png" />

## 创建eureka-server-1
项目搭建两种方式：
1. 父pom中继承spring-boot-starter-parent，子pom中直接结成父pom。该方式比较方便，但子项目都是spring boot项目了。
2. 父项目不需要继承spring-boot-starter-parent，子pom中通过使用scope = import依赖关系。  

{% highlight xml linenos %}
    <dependencyManagement>
         <dependencies>
                <dependency>
                    <!-- Import dependency management from Spring Boot -->
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-dependencies</artifactId>
                    <version>1.5.1.RELEASE</version>
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>   
        </dependencies>
    </dependencyManagement>
{% endhighlight %}

*参考文档*<http://tengj.top/2017/02/26/springboot1/>

EurekaServer1Application中声明@EnableEurekaServer

**在默认情况下，Eureka会将自己也作为客户端尝试注册，所以在单机模式下，我们需要禁止该行为**

## 创建eureka-server-2
1. 修改host文件，C:\WINDOWS\system32\drivers\etc\hosts，新增  
127.0.0.1 eureka1 eureka2  
2. 修改application.yml文件，如下为eureka2中的部分配置，eureka1修改同理。
{% highlight xml linenos %}
    spring:
        profiles:
            active: eureka2
    eureka:
        instance:
            #主机名
            hostname: eureka2
        client:
            register-with-eureka: false
            fetch-registry: false
            service-url:
                #将自己注册到eureka1
                defaultZone: http://eureka1:8761/
{% endhighlight %}

3. 将服务注册到高可用eureka中心，修改如下即可。
{% highlight xml linenos %}
eureka:
  client:
    serviceUrl:
      defaultZone: http://peer1:8761/eureka/,http://peer2:8762/eureka  
{% endhighlight %}
