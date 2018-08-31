# Spring in Company Learning Notes

## Chapter 7 Spring AOP Base

1. AOP术语。
    - 连接点。Spring仅支持将方法作为连接点。连接点包含2部分。方法名，由切点定义。方位，即方法前中后，于增强类型中定义。
    - 切点。定位到某个方法上。
    - 增强。描述一段程序代码。描述执行点的方位。
    - 目标对象。
    - 引介。一种特殊的增强。为业务类添加原本没有的接口实现逻辑。
    - 织入。将增强添加到目标类的具体连接点上的过程。3种织入方式，编译期织入（AspectJ），类装载期织入（AspectJ），动态代理织入（Spring）。
    - 代理。织入增强后产生的结果类。
    - 切面。由切点和增强组成。
2. JDK动态代理。
    - 代理示例。
        1. 移除性能监视横切代码。
        ![移除性能监视横切代码](https://ws1.sinaimg.cn/large/e2989da6ly1fuqkb25ks6j20m90gz4c3.jpg)
        2. 利用反射，处理业务逻辑的调用。
        ![InvocationHandler](https://ws1.sinaimg.cn/large/e2989da6ly1fuqkd2129bj20mf0cggvq.jpg)
        3. 创建代理实例。
        ![创建代理实例](https://ws1.sinaimg.cn/large/e2989da6ly1fuqkfukdt1j20le0ein8b.jpg)
    - 代理实例的方法调用时序图。
    ![时序图](https://ws1.sinaimg.cn/large/e2989da6ly1fuqki39pndj20m10f8juy.jpg)
3. CGLib动态代理。
    - JDK动态代理的局限，只能为接口创建代理实例。可从Proxy的接口方法newProxyInstance(ClassLoader loader, Class[] interfaces, InvocationHandler h)中看出，第二个入参只接受接口列表。
    - CGLib采用底层的字节码技术，可以为一个类创建子类，在子类中采用方法拦截的技术拦截所有父类方法的调用并顺势织入横切逻辑。CGLib动态代理的局限是不能对目标类中的final或private方法进行代理。
    - 代理示例。
        1. 子类代理工厂。
        ![子类代理工厂](https://ws1.sinaimg.cn/large/e2989da6ly1fuqloyt9ecj20n20emn97.jpg)
        2. 创建代理实例。
        ![子类代理实例](https://ws1.sinaimg.cn/large/e2989da6ly1fuqlqbl4kmj20k309c0z6.jpg)
4. 使用SpringAOP比直接使用JDK或CGLib的好处。
    - 普通代理难做到的3点。
    ![普通代理改进](https://ws1.sinaimg.cn/large/e2989da6ly1fuqmdahx4bj20mz05rdif.jpg)
    - SpringAOP的解决办法。
    ![SpringAOP的解决办法](https://ws1.sinaimg.cn/large/e2989da6ly1fuqmfe2v66j20my05l41m.jpg)
5. 增强的类型。
    - 带<\<spring\>>标识的接口是Spring所定义的扩展增强接口。带<\<aoppalliance\>>标识的接口则是AOP联盟定义的接口。
    ![增强接口继承](https://ws1.sinaimg.cn/large/e2989da6ly1fuqoflv5g8j20j70ae427.jpg)
    - 按照增强在目标方法中的连接点位置，可以分为如下5类。
    ![5类增强](https://ws1.sinaimg.cn/large/e2989da6ly1fuqoidwo4oj20lt0ah793.jpg)
6. 前置增强。
    - 实例。
        1. 前置增强需实现MethodBeforeAdvice接口，重写before方法。
        ![前置增强](https://ws1.sinaimg.cn/large/e2989da6ly1fuqooh3q65j20mh072n2y.jpg)
        2. 前置增强应用。
        ![前置增强应用](https://ws1.sinaimg.cn/large/e2989da6ly1fuqoqooc7xj20fh0dh464.jpg)
    - 可以使用addAdvice(Advice)方法添加多个增强，形成一个增强链。调用顺序和添加顺序一致。
    - 使用xml配置前置增强。
        1. 示例。
        ![xml配置前置增强示例](https://ws1.sinaimg.cn/large/e2989da6ly1furkmvtketj20lo05faeb.jpg)
        2. ProxyFactoryBean的几个常用的可配置属性。
        ![代理xml属性1](https://ws1.sinaimg.cn/large/e2989da6ly1furkx71mafj20ls06h0vf.jpg)
        ![代理xml属性2](https://ws1.sinaimg.cn/large/e2989da6ly1furkxijxv4j20ly05owh3.jpg)
        3. 将ProxyTargetClass设置为true后，强制使用cglib代理。即使配置proxyInterfaces属性也会被ProxyFactoryBean忽略。
        ![强制使用子类代理](https://ws1.sinaimg.cn/large/e2989da6ly1furl0jl2w3j20l703540t.jpg)
7. ProxyFactory的解析。
    - 返回真实Proxy的流程，实际理解需阅读源码。调用ProxyFactory的getProxy()方法。创建AopProxyFactory，创建AopProxy，创建真实Proxy并返回。
    - AopProxy类结构。
    ![AopProxy类结构](https://ws1.sinaimg.cn/large/e2989da6ly1fuqtd17qblj20dq04pgmh.jpg)
    - 指定对接口进行代理，将使用jdk动态代理技术。
    ![指定接口](https://ws1.sinaimg.cn/large/e2989da6ly1fuqti39sbnj20jw03q413.jpg)
    - 启用代理优化。将使用Cglib2AopProxy代理。
    ![cglib代理](https://ws1.sinaimg.cn/large/e2989da6ly1fuqtjuoz00j20k403c40w.jpg)
8. 后置增强。
    - 实例。
        1. 后置增强需实现AfterReturningAdvice接口，重写afterReturning方法。returnObj为目标实例方法返回的结果。method为目标类的方法。args为目标实例方法的入参。obj为目标类实例。
        ![后置增强实现](https://ws1.sinaimg.cn/large/e2989da6ly1furutddq2rj20kx07yjx7.jpg)
        2. 假设后置增强中抛出异常，如果该异常是目标方法声明的异常，则该异常归并到目标方法中。如果不是目标方法所声明的异常，则spring将其转为运行期异常抛出。
    - 使用xml配置后置增强。
    ![xml后置增强](https://ws1.sinaimg.cn/large/e2989da6ly1furuz5xmyfj20la060gq2.jpg)
    - interceptorNames是String[]类型的。接收名称，而非Advice实例。因ProxyBeanFactory内部在生成代理类时，需要Class而非，创建后的实例。
        - 可使用\<idref local=""\>标签，IDE会发现配置错误。
        ![idref标签](https://ws1.sinaimg.cn/large/e2989da6ly1furv7slu9rj20at03mdh4.jpg)
        - 亦可使用逗号。
        ![逗号分隔](https://ws1.sinaimg.cn/large/e2989da6ly1furv8qektqj20js00t74l.jpg)
9. 环绕增强。
    - 环绕增强实例。实现MethodInterceptor接口，重写invoke方法。MethodInvocation封装了目标方法及其入参数组，还封装了目标方法所在的实例对象。通过MethodInvocation的getArguments()方法可以获取目标方法的入参数组，通过proceed()方法反射调用目标实例相应的方法。
    ![环绕增强实现](https://ws1.sinaimg.cn/large/e2989da6ly1furys520zxj20mw0az48a.jpg)
    - 于xml中配置环绕增强。
    ![环绕增强xml配置](https://ws1.sinaimg.cn/large/e2989da6ly1furz0fm78dj20l3056dj8.jpg)
10. 异常抛出增强。
    - 异常抛出增强实例。实现ThrowsAdvice标签接口，采用afterThrowing方法的形式定义异常抛出的增强方法。
    ![异常抛出增强实例](https://ws1.sinaimg.cn/large/e2989da6ly1furzcasa1uj20jw08zq9j.jpg)
    - 前3入参要么都提供，要么都不提供。最后一个入参必须是Throwable的子类。
    - 可以定义多个afterThrowing方法，spring会自动选用最匹配的增强方法。
    - 于xml中配置异常抛出增强。
    ![异常抛出增强xml](https://ws1.sinaimg.cn/large/e2989da6ly1furzmixdm5j20kd03wwhj.jpg)
11. 引介增强。
    - 引介增强的典型应用场景。性能监视逻辑会影响性能。应让用户选择是否开启此功能。此开关可由引介增强实现。
    - 实例。
        1. 性能监视接口。
        ![性能监视接口](https://ws1.sinaimg.cn/large/e2989da6ly1fusmugzp1nj20bh02lt9l.jpg)
        2. 扩展DelegatingIntroductionInterceptor类。应用Monitorable接口。重写setMonitorActive与invoke方法。
        ![引介增强实现1](https://ws1.sinaimg.cn/large/e2989da6ly1fusn7ql13zj20mq0g5nap.jpg)
        ![引介增强实现2](https://ws1.sinaimg.cn/large/e2989da6ly1fusn8c1uicj20e8020gmb.jpg)
        3. 因为引介增强是单例，开关变量使引介增强变为线程不安全。故用ThreadLocal包装，让每个线程单独使用一个状态。
        4. 实际开启监视。需对接口进行一次强制转型。
        ![开启引介增强](https://ws1.sinaimg.cn/large/e2989da6ly1fusq28w29jj20m90bcwog.jpg)
    - 于xml中配置引介增强。引介增强必须通过创建子类生成代理，故强制使用cglib，否则报错。
    ![xml引介增强](https://ws1.sinaimg.cn/large/e2989da6ly1fuspmxmvpqj20mr05l79d.jpg)
12. Pointcut类关系。
    - Pointcut由ClassFilter和MethodMatcher构成。ClassFilter定位到某些特定类。MethodMatcher定位到某些特定方法。
    ![切点类关系图](https://ws1.sinaimg.cn/large/e2989da6ly1fusqnu82krj20fr07nadc.jpg)
    - 有静态和动态2种方法匹配器。静态仅匹配方法名签名。动态还需匹配参数的值。故动态需多次匹配，效率较差。
