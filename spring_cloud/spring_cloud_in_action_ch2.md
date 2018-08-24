# Spring Cloud in Action Learning Notes

## Chapter 2 Spring Boot

1. Spring Boot Maven配置分析。
    - 父项目parent配置定义了Spring Boot版本的基础依赖以及一些默认配置内容，比如，配置文件application.properties的位置等。
2. Spring Boot配置。
    - 在命令行启动时可以使用--对application.properties中的属性值进行重新赋值。java -jar xx.jar --server.port=8888命令，等价于在application.properties中添加属性server.port=8888。
    - 多环境配置。
        1. 多环境配置的文件名需要满足application-{profile}.properties的格式，其中{profile}对应环境标识。
        2. 在application.properties中设置application.profiles.active来决定哪个配置文件会被加载。application.profiles.active=test就会加载application-test.properties。可以在命令行时重写application.profiles.active。
    - 配置文件可从外部取得，可从Spring Boot的属性加载顺序看出。这是Spring Cloud Config的基础。
    ![属性加载顺序1](https://ws1.sinaimg.cn/large/e2989da6ly1fuktglp55wj20sk09o420.jpg)
    ![属性加载顺序2](https://ws1.sinaimg.cn/large/e2989da6ly1fukthay6ywj20sq0brdll.jpg)
3. Spring Boot的监控与管理。
    - 引入spring-boot-starter-actuator依赖。
    - 原生端点可分为应用配置，度量指标，操作控制，3个大类。
    ![3类原生端点](https://ws1.sinaimg.cn/large/e2989da6ly1fukudym65wj20sq05tq5z.jpg)
    - 如果加了spring security，某些端点可能需要"ACTUATOR"的role才能访问。
    - 应用配置类。
        1. /autoconfig。
