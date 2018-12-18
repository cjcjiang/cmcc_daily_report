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
    - 切点类型。
    ![切点类型](https://ws1.sinaimg.cn/large/e2989da6ly1fuxktemnnrj20lt0jewo2.jpg)
    - 切面类型。
        1. Advisor。代表一般切面。
        2. PointcutAdvisor。代表具有切点的切面。
        3. IntroductionAdvisor。代表引介切面。
        4. 切面类继承关系。
        ![切面类继承关系](https://ws1.sinaimg.cn/large/e2989da6ly1fuxl2jd07kj20fo0aftbe.jpg)
    - PointcutAdvisor的6个实现类。都是通过扩展对应的Pointcut实现类并实现PointcutAdvisor接口进行定义的。
    ![切面实现类1](https://ws1.sinaimg.cn/large/e2989da6ly1fuxlk75r7sj20lz08sjuy.jpg)
    ![切面实现类2](https://ws1.sinaimg.cn/large/e2989da6ly1fuxlkgisjwj20lr03u0ua.jpg)
13. 利用StaticMethodMatcherPointcutAdvisor，实现静态普通方法名匹配切面。
    - 示例。只匹配Waiter的greetTo方法。
        1. 要被增强的类。
        ![waiter类](https://ws1.sinaimg.cn/large/e2989da6ly1fuxmqgxxtqj20gf06qn0r.jpg)
        ![seller类](https://ws1.sinaimg.cn/large/e2989da6ly1fuxmr10g4yj20gh051go0.jpg)
        2. 切面类。定义要被增强的类和方法。扩展StaticMethodMatcherPointcutAdvisor类。必须重写matches方法，匹配特定方法。默认匹配所有类，重写getClassFilter方法，从而限定被增强的类。
        ![切面类](https://ws1.sinaimg.cn/large/e2989da6ly1fuxmzozwq1j20m0094n4q.jpg)
        3. 增强类。
        ![增强类](https://ws1.sinaimg.cn/large/e2989da6ly1fuxn6821gbj20my07cgrg.jpg)
        4. xml配置切面。
        ![xml配置切面](https://ws1.sinaimg.cn/large/e2989da6ly1fuxnafwj6fj20m808rqa6.jpg)
        5. 测试增强是否被织入。
        ![织入测试](https://ws1.sinaimg.cn/large/e2989da6ly1fuxqh6s1ouj20k404kgoz.jpg)
14. 利用RegexpMethodPointcutAdvisor，实现静态正则表达式方法匹配切面。
    - 示例。RegexpMethodPointcutAdvisor类已是功能齐备的实现类，一般情况下无需扩展该类。
        1. xml定义切面。patterns中的匹配模式串匹配的是目标类方法的全限定名。
        ![xml定义切面](https://ws1.sinaimg.cn/large/e2989da6ly1fuyh0i0xbkj20lk097dn1.jpg)
        2. 测试增强是否被织入。
        ![正则织入测试](https://ws1.sinaimg.cn/large/e2989da6ly1fuyh6k373yj20k003cjto.jpg)
    - 简单正则表达式语法，详见书。
15. 动态切面。切面用DefaultPointcutAdvisor，切点用DynamicMethodMatcherPointcut定义。从而在运行时，动态检查方法的入参，决定是否织入增强。
    - 示例。
        1. 切点。扩展DynamicMethodMatcherPointcut类，重写方法设置切点。先进行静态切点检查，只有通过静态检查的才会进行动态检查，从而提高效率。
        ![切点](https://ws1.sinaimg.cn/large/e2989da6ly1fuynxv5ae2j20mt0hd7je.jpg)
        2. xml配置切面。
        ![xml配置切面](https://ws1.sinaimg.cn/large/e2989da6ly1fuynzox3qxj20lh0a3wm4.jpg)
        3. 测试增强是否被织入。
        ![测试织入1](https://ws1.sinaimg.cn/large/e2989da6ly1fuyo5m3o9pj20ja058n0t.jpg)
        ![测试织入2](https://ws1.sinaimg.cn/large/e2989da6ly1fuyo5v32q1j20f201owf0.jpg)
        4. spring在创建代理织入切面时，对目标类中的所有方法进行静态切面检查。生成代理对象后，第一次调用代理类的每一个方法时都会进行一次静态切点检查，如果本次检查就能从候选者列表中将该方法排除，则以后对该方法的调用就不再执行静态切点检查；对于那些在静态切点检查时匹配的方法，在后续调用该方法时，将执行动态切点检查。
16. 流程切面。切面用DefaultPointcutAdvisor。切点用ControlFlowPointcut定义。只有由特定流程，如只有从某方法被调用时才织入增强，需使用流程切面。
    - 示例。
        1. 需织入逻辑的类是Waiter。发起调用Waiter的类是WaiterDelegate类的service方法。
        ![WaiterDelegate发起调用](https://ws1.sinaimg.cn/large/e2989da6gy1fxup5qwt0mj20ox0a4jzt.jpg)
        2. 切点。使用ControlFlowPointcut类，直接在构造函数中即可指定流程切点的触发类及触发方法。
        ![切点](https://ws1.sinaimg.cn/large/e2989da6gy1fxuttsl9jfj20s805mgrj.jpg)
        3. xml配置流程切面。
        ![xml配置流程切面](https://ws1.sinaimg.cn/large/e2989da6gy1fxutw34muxj20s60fh4ei.jpg)
        4. 增强织入测试。
        ![织入测试1](https://ws1.sinaimg.cn/large/e2989da6gy1fxuu503u76j20p407hn3i.jpg)
        ![织入测试2](https://ws1.sinaimg.cn/large/e2989da6gy1fxuu5e7cqbj20lj07bafw.jpg)
17. 复合切点切面。使用ComposablePointcut类来组合2个切点。
    - 组合方法。
        1. ComposablePointcut类的构造函数。
        ![构造函数](https://ws1.sinaimg.cn/large/e2989da6gy1fxvp520cetj20rg08iadx.jpg)
        2. ComposablePointcut类提供的3个交集运算方法。
        ![交集运算](https://ws1.sinaimg.cn/large/e2989da6gy1fxvp74ca8kj20rf078wi8.jpg)
        3. ComposablePointcut类提供的2个并集运算方法。
            - ![并集运算1](https://ws1.sinaimg.cn/large/e2989da6gy1fxvpbou34dj20rn02ijsd.jpg)
            - ![并集运算2](https://ws1.sinaimg.cn/large/e2989da6gy1fxvpc9ad4aj20s202zt9w.jpg)
        4. 可以直接使用Pointcuts工具类提供的静态方法进行2个切点的交或并集运算。
        ![工具类静态](https://ws1.sinaimg.cn/large/e2989da6gy1fxvpkdonioj20rl04zgo3.jpg)
    - 示例。
        1. 流程切点，WaiterDelegate类的service方法调用Waiter类时织入。方法名匹配切点，调用Waiter类的greetTo方法是织入。
        2. 使用ComposablePointcut类组合2个切点。
        ![切点组合](https://ws1.sinaimg.cn/large/e2989da6gy1fxvpn1avbhj20t20e6dv2.jpg)
        3. xml配置复合切面。
        ![配置复合切面](https://ws1.sinaimg.cn/large/e2989da6gy1fxvpp5gvs9j20sn0ac7es.jpg)
18. 引介切面。
    - 引介切面的2个实现类。DefaultIntroductionAdvisor和DeclareParentsAdvisor。后者用于实现使用AspectJ语言的DeclareParent注解表示的引介切面。
    - DefaultIntroductionAdvisor的3个构造函数。
    ![引介切面构造函数](https://ws1.sinaimg.cn/large/e2989da6gy1fy2l1df7wkj20rf09q43k.jpg)
    - 配置引介切面。
    ![配置引介切面](https://ws1.sinaimg.cn/large/e2989da6gy1fy2l4y5aojj20sp09bn6u.jpg)
19. 自动创建代理。
    - 三种基于BeanPostProcessor的自动代理创建器实现类。
        1. BeanNameAutoProxyCreator。为一组特定配置名的Bean自动创建代理实例。
        2. DefaultAdvisorAutoProxyCreator。对所有的Advisor进行扫描，自动将这些切面应用到匹配的Bean中。
        3. AnnotationAwareAspectJAutoProxyCreator。为包含AspectJ注解的Bean自动创建代理实例。
    - 自动代理创建器实现类的类继承图。
    ![类继承图](https://ws1.sinaimg.cn/large/e2989da6gy1fyamo5j6isj20vx0iq7eo.jpg)
20. BeanNameAutoProxyCreator的使用方法。
    - 配置方法。
    ![bean名自动1](https://ws1.sinaimg.cn/large/e2989da6gy1fyan8zgqljj213j05pn57.jpg)
    ![bean名自动2](https://ws1.sinaimg.cn/large/e2989da6gy1fyan9fql6fj20yb04m7ac.jpg)
    - optimize属性为true则强制使用cglib动态代理。
    - 获取代理类方法。
    ![bean名获取代理](https://ws1.sinaimg.cn/large/e2989da6gy1fyanerw0p9j20yk06kaip.jpg)
21. DefaultAdvisorAutoProxyCreator的使用方法。
    - 配置方法。
    ![切面自动创建](https://ws1.sinaimg.cn/large/e2989da6gy1fyanlnlei4j210c0b4ncu.jpg)
    - 获取代理类方法。
    ![切面获取代理](https://ws1.sinaimg.cn/large/e2989da6gy1fyano0b22uj20yo07y12y.jpg)
22. 被代理的类有内部方法调用时，被调用的方法无法应用被织入的增强。
