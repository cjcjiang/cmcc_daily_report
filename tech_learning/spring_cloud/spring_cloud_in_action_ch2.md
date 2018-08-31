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
        1. /autoconfig。获取应用的自动化配置报告。
        2. /beans。获取应用上下文中创建的所有Bean。
        3. /configprops。获取应用中配置的属性信息报告。
        4. /env。获取应用所有可用的环境属性报告。
        5. /mappings。返回所有Spring MVC的控制器映射关系报告。
        6. /info。返回一些应用自定义的信息。
    - 度量指标类。
        1. /metrics。返回当前应用的各类重要度量指标，比如内存信息，线程信息，垃圾回收信息等。直接用这个接口一次获得全部指标，略显粗暴。故可使用/metrics/{name}接口来获取单一的度量信息。
        2. /health。获取应用的各类健康指标信息。
        ![自带健康检测器](https://ws1.sinaimg.cn/large/e2989da6ly1fuoc3zs144j20kv074acy.jpg)
        3. 自定义健康检测器。
            - 应用HealthIndicator接口，重写health()方法。
            - 检测RocketMQ的示例。
            ![RocketMQ健康监测](https://ws1.sinaimg.cn/large/e2989da6ly1fuocaivbvtj20mv0bhake.jpg)
            - 接口返回的信息。
            ![健康接口返回](https://ws1.sinaimg.cn/large/e2989da6ly1fuocbkykvrj2053026dg1.jpg)
        4. /dump。暴露程序运行中的线程信息。
        5. /trace。返回基本的HTTP跟踪信息。
    - 操作控制类。
        1. /shutdown。需加入配置endpoints.shutdown.enabled=true开启此控制。
