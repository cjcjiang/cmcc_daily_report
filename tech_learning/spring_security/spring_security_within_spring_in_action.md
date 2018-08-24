# Spring Security Within Spring In Action

## CH9 保护WEB应用

1. 于spring boot中只需引入spring-boot-starter-security依赖。
2. 于使用spring框架的web应用中集成spring security的第一步是配置filter。
    - 于web.xml中配置DelegatingFilterProxy。
    ![xml配置filter](https://ws1.sinaimg.cn/large/e2989da6ly1fuhejg33hkj20gv03j3yt.jpg)
    - 使用java code配置DelegatingFilterProxy。
    ![javacode配置filter](https://ws1.sinaimg.cn/large/e2989da6ly1fuhembxghqj20je03674p.jpg)
3. 启用安全拦截的方法为扩展WebSecurityConfigurerAdapter类，并加入@EnableWebSecurity注解。这个配置类一般放入config包中。
    - 最简单配置类，启用安全拦截。
    ![启用安全拦截](https://ws1.sinaimg.cn/large/e2989da6ly1fuhewyhdv1j20ig05wmyt.jpg)
    - 通过重载WebSecurityConfigurerAdapter的三个configure()方法来配置Web安全性。
    ![重载方法配置web安全](https://ws1.sinaimg.cn/large/e2989da6ly1fuheyfn3etj20py084wf3.jpg)
    - 配置web安全的一般步骤。
        1. 配置用户存储。
        2. 指定哪些请求需要认证，哪些请求不需要认证，以及所需要的权限。
        3. 提供一个自定义的登录页面，替代原来简单的默认登录页。
4. 使用基于内存的用户存储。
    - 示例。
    ![内存用户存储示例](https://ws1.sinaimg.cn/large/e2989da6ly1fuhfehtks3j20iz07g760.jpg)
    - 调用AuthenticationManagerBuilder类的实例auth的inMemoryAuthentication()启用内存用户存储。
    - 调用withUser()方法为内存用户存储添加新的用户，这个方法的参数是username。withUser()方法返回的是UserDetailsManagerConfigurer.UserDetailsBuilder，这个对象提供了多个进一步配置用户的方法，包括设置用户密码的password()方法以及为给定用户授予一个或多个角色权限的roles()方法。and()方法能够将多个用户的配置连接起来。
    - roles()方法是authorities()方法的简写形式。roles()方法所给定的值都会添加一个“ROLE_”前缀，并将其作为权限授予给用户。使用roles()方法与以下实例功能相同。
    ![authorities方法示例](https://ws1.sinaimg.cn/large/e2989da6ly1fuhflkp74mj20i9038wet.jpg)
    - UserDetailsManagerConfigurer.UserDetailsBuilder对象所有可用的方法。
    ![所有可用方法](https://ws1.sinaimg.cn/large/e2989da6ly1fuhfo2dvzhj20n70jbta8.jpg)
5. 基于数据库表进行认证。
    - 示例。DataSource是通过自动装配得到的。
    ![数据库表认证](https://ws1.sinaimg.cn/large/e2989da6ly1fuhfs7m97mj20i30580t3.jpg)
    - Spring Security默认的SQL查询语句。
    ![默认sql查询](https://ws1.sinaimg.cn/large/e2989da6ly1fuhgmkl7r2j20i407sgmy.jpg)
    - 自定义sql查询方式。在本例中只重写了认证和基本权限的查询语句，但是通过调用groupAuthoritiesByUsername()方法，也能够将群组权限重写为自定义的查询语句。需要遵循查询的基本协议，所有查询都将用户名作为唯一的参数。
    ![自定义sql查询方式](https://ws1.sinaimg.cn/large/e2989da6ly1fuhgpq6f5cj20jb06xgn7.jpg)
6. 指定密码转换器。
    - 示例。Spring Security的加密模块包括了三个PasswordEncoder接口的实现：BCryptPasswordEncoder、NoOpPasswordEncoder、StandardPasswordEncoder。
    ![密码转码示例](https://ws1.sinaimg.cn/large/e2989da6ly1fui9nivrwhj20il07dab2.jpg)
    - 可以自行实现PasswordEncoder接口。数据库中的密码是永远不会解码的。所采取的策略与之相反，用户在登录时输入的密码会按照相同的算法进行转码，然后再与数据库中已经转码过的密码进行对比。转码算法由encode()方法实现。对比是在PasswordEncoder的matches()方法中进行的。
    ![pe接口](https://ws1.sinaimg.cn/large/e2989da6ly1fuia2vr9blj20id02amxc.jpg)
7. 基于LDAP进行认证。
    - 示例。
    ![LDAP认证](https://ws1.sinaimg.cn/large/e2989da6ly1fuia9m9ao3j20if04jq3b.jpg)
    - 其它详见书。
8. 使用其它用户存储用于认证，如Mongo或Neo4j。
    - 提供自定义的UserDetailsService接口的实现。要做的就是实现loadUserByUsername()方法。根据给定的用户名来查找用户。loadUserByUsername()方法会返回代表给定用户的UserDetails对象。
    ![uds接口](https://ws1.sinaimg.cn/large/e2989da6ly1fuiafijk7tj20ia026jri.jpg)
    - 示例。
    ![自定义用户存储](https://ws1.sinaimg.cn/large/e2989da6ly1fuiaud8jwlj20ll0l7jxy.jpg)
    ![应用自定义用户存储](https://ws1.sinaimg.cn/large/e2989da6ly1fuiavwwlmxj20ih05674r.jpg)
9. 重载configure(HttpSecurity)方法，对每个请求进行细粒度安全性控制。
    - 示例。
    ![请求级安全控制示例](https://ws1.sinaimg.cn/large/e2989da6ly1fuibd9809tj20h504j74s.jpg)
    - antMatchers()方法中设定的路径支持Ant风格的通配符。可以使用通配符来指定路径。
    ![ant通配符](https://ws1.sinaimg.cn/large/e2989da6ly1fuic0c9n06j20c300ma9y.jpg)
    - 可以在一个对antMatchers()方法的调用中指定多个路径。
    ![ant指定多个路径](https://ws1.sinaimg.cn/large/e2989da6ly1fuic2w6g95j20hx00naa3.jpg)
    - regexMatchers()方法则够接受正则表达式来定义请求路径。
    ![正则匹配方法](https://ws1.sinaimg.cn/large/e2989da6ly1fuigubmqi9j20d600l0sp.jpg)
    - 通过authenticated()和permitAll()来定义该如何保护路径。authenticated()要求在执行该请求时，必须已经登录了应用。如果用户没有认证的话，Spring Security的Filter将会捕获该请求，并将用户重定向到应用的登录页面。同时，permitAll()方法允许请求没有任何的安全限制。其它用来定义如何保护路径的配置方法。
    ![保护路径配置方法](https://ws1.sinaimg.cn/large/e2989da6ly1fuihzle18kj20h50jsq4y.jpg)
    - 可以将任意数量的antMatchers()、regexMatchers()和anyRequest()连接起来，这些规则会按给定的顺序发挥作用。故应将最为具体的请求路径放在前面，而最不具体的路径，如anyRequest()放在最后面。如果不这样做的话，那不具体的路径配置将会覆盖掉更为具体的路径配置。
    - 使用Spring表达式可以突破一维的限制，也就是说可以使用hasRole()方法限制某个特定角色的同时，使用hasIpAddress()限制只有特定ip的request才可以进入。同时可以利用Spring表达式进行一些特殊的限制，比如限制某个角色只能在星期二进行访问。
    ![多限制条件](https://ws1.sinaimg.cn/large/e2989da6ly1fuiiszcf5aj20hq0153yi.jpg)
    ![spel支持的部分语句](https://ws1.sinaimg.cn/large/e2989da6ly1fuiituoskbj20h50hymyr.jpg)
10. 强制通道的安全性，即强制使用https通道。
    - 使用requiresChannel()方法为选定的URL强制使用HTTPS。
    ![强制https](https://ws1.sinaimg.cn/large/e2989da6ly1fuiiztt107j20jc0680u9.jpg)
11. 防止跨站请求伪造。
    - spring security默认启用csrf防护。关闭的方法为http.csrf().disable()。
    ![关csrf防护](https://ws1.sinaimg.cn/large/e2989da6ly1fuijwylm1bj20h203y0t8.jpg)
12. 登录页面。
    - 在http中调用formLogin()方法，启用默认的登录页面。
    ![默认登录页面](https://ws1.sinaimg.cn/large/e2989da6ly1fuik3rcpugj20i707e0ua.jpg)
    - 添加自定义的登录页。向formLogin()方法传入自定义的页面位置作为参数。作为Rest Server时应启用HTTP Basic认证。
    ![自定义登录页](https://ws1.sinaimg.cn/large/e2989da6ly1fuikhk4hfwj20gb05yaad.jpg)
    - 启用Remember-me功能。http上调用rememberMe()方法，可以设置token的有效时间与私钥。
    ![记住我功能](https://ws1.sinaimg.cn/large/e2989da6ly1fuikn9c1sij20gt063dg9.jpg)
    - 让登录请求包含一个名为remember-me的参数，这样就会将登录状态保存下来。
13. 退出功能。
    - 退出功能是通过Servlet容器中的Filter实现的，这个Filter会拦截针对"/logout"的请求。因此，为应用添加退出功能只需添加到/logout的链接。用户对/logout发起请求后，这个请求会被spring security的LogoutFilter所处理。用户会退出应用，所有的记住我token都会被清除掉。在退出完成后，用户浏览器将会重定向到"/login?logout"，从而允许用户进行再次登录。
    - 可在logout后定向到其它页面，配置http即可。调用logout().logoutSuccessUrl("/")方法，指定重定向页面。
    ![登出页面重定向](https://ws1.sinaimg.cn/large/e2989da6ly1fuilktbrruj20gc05i3ys.jpg)
    - 调用logoutUrl()方法，自定义LogoutFilter的拦截路径，例如从/logout到/signout。
    ![自定义登出路径](https://ws1.sinaimg.cn/large/e2989da6ly1fuiloo19ugj206l01zq2v.jpg)
14. spring security可以与thymeleaf或jsp耦合，提供视图级别的显示控制，详见书。

## CH14 保护方法应用

1. 启用基于注解的方法安全性。
    - 配置类扩展GlobalMethodSecurityConfiguration类。需要在配置类上使用@EnableGlobalMethodSecurity注解。
    ![启用注解](https://ws1.sinaimg.cn/large/e2989da6ly1fujgf33helj20di02tweo.jpg)
    - @EnableGlobalMethodSecurity注解的属性securedEnabled设置为true，开启了@Secured注解的使用。
2. 安全配置中设置用于认证的用户存储。
    - 重载参数为auth的configure()方法，设置用户存储。
    ![设置用户存储](https://ws1.sinaimg.cn/large/e2989da6ly1fujgli6ot5j20fr03w0t1.jpg)
3. 使用@Secured注解限制方法调用。
    - 需要单一角色。
    ![单一角色](https://ws1.sinaimg.cn/large/e2989da6ly1fujgpnnzhej20b502dt8o.jpg)
    - 至少具备其中一个角色。
    ![角色之一](https://ws1.sinaimg.cn/large/e2989da6ly1fujgr03j1aj20ba02e74a.jpg)
    - 如果方法被没有认证的用户或没有所需权限的用户调用，保护这个方法的切面将抛出一个Spring Security异常（可能是AuthenticationException或AccessDeniedException的子类）。它们是非检查型异常，但这个异常最终必须要被捕获和处理。如果被保护的方法是在Web请求中调用的，这个异常会被Spring Security的过滤器自动处理。否则的话，你需要编写代码来处理这个异常。
4. 使用JSR-250的@RolesAllowed注解。
    - 将@EnableGlobalMethodSecurity的jsr250Enabled属性设置为true，以开启@RolesAllowed的使用。此设置与securedEnabled设置为true不冲突，二者可同时启用。
    ![开启jsr注解](https://ws1.sinaimg.cn/large/e2989da6ly1fujgwssktaj20di02tq35.jpg)
    - 需要单一角色。
    ![jsr单一角色](https://ws1.sinaimg.cn/large/e2989da6ly1fujgzkfhm5j20b5027dft.jpg)
5. 使用带有SpEL表达式的注解。
    - 将@EnableGlobalMethodSecurity注解的prePostEnabled属性设置为true从而启用这些注解。
    - 4个接收SpEL表达式的注解。
    ![使用SpEL](https://ws1.sinaimg.cn/large/e2989da6ly1fujm9jxjq8j20p30apab8.jpg)
    - @PreAuthorize实例。Spittle是传入的对象。
    ![prea实例](https://ws1.sinaimg.cn/large/e2989da6ly1fujmddkevsj20hn03i74k.jpg)
    - @PostAuthorize实例。Spring Security在SpEL中提供了名为returnObject的变量。此例中返回对象是一个spittle对象，通过.直接访问username属性。表达式还内置principal对象，从中取出其username属性。principal是另一个Spring Security内置的特殊名称，它代表了当前认证用户的主要信息（通常是用户名）。
    ![posta实例](https://ws1.sinaimg.cn/large/e2989da6ly1fujmywk311j20if02b74e.jpg)
    - 事后对方法的返回值进行过滤。@PostFilter注解过滤返回的list，确保非管理员只能看到属于自己的Spittle。filterObject对象引用的是这个方法返回list中的某一个元素。
    ![返回值过滤](https://ws1.sinaimg.cn/large/e2989da6ly1fujnsdd3okj20gv03iq3a.jpg)
    - 事先对方法的参数进行过滤。targetObject是Spring Security提供的另外一个值，它代表了要进行计算的当前列表元素。
    ![入参过滤](https://ws1.sinaimg.cn/large/e2989da6ly1fujob3z0dlj20gk02b3yx.jpg)
6. 自定义的许可计算器。
    - 实现自定义的许可计算器。需要实现PermissionEvaluator接口。
    ![许可计算器实例](https://ws1.sinaimg.cn/large/e2989da6ly1fujoujukp2j20jt0k0wki.jpg)
    - 重载扩展了GlobalMethodSecurityConfiguration类的配置类的createExpressionHandler()方法。
    ![注册表达式处理者](https://ws1.sinaimg.cn/large/e2989da6ly1fujoy52xrpj20ie04i0tf.jpg)
    - 于注解中使用注册的表达式处理者。
    ![使用表达式处理者](https://ws1.sinaimg.cn/large/e2989da6ly1fujp1musinj20fw01st90.jpg)
