# Questions in Spring in Action

1. dispatchservlet的getServletMappings()方法无法用/成为默认sevlet。路径"/"始终加载index.jsp。
2. "/*"，这个是wild card是什么意思？
    - < url-pattern > / : 会匹配到/login这样的路径型url，不会匹配到模式为.jsp这样的后缀型url，即：.jsp不会进入spring的 DispatcherServlet类
    - < url-pattern > /* : 会匹配.jsp，会出现返回jsp视图时再次进入spring的DispatcherServlet 类，导致找不到对应的controller所以报404错。总之，/* 会匹配所有url：路径型的和后缀型的url(包括/login,.jsp,.js和*.html等)