---
layout: post
title: Spring学习之AOP
date: 2021-03-25 19:48:00 +0900
category: java
---
### 撰写缘由 
>这两天在学Spring，关于AOP的学习上遇到了争论，差点打起来(笑)。故此记录一下。话不多说，进入正文。

***

> - Q1:什么是SpringAOP？
>   - A:说的简单点就是面向切面编程。对照Spring的官方文档，官方是这么解释的：<br>
> 官方说AOP(面向切面编程)是对OOP(面向对象编程)的补充，有别于我们过去在OOP中对类的模块化，AOP是对切面的模块化。AOP是Spring的关键组件之一，IOC容器不依赖于AOP，你爱用不用，但是AOP是对SpringIOC的强大补充，提供了一个非常强大的中间件解决方案。(潜台词是我这么优秀，多用用)。
> - Q2：AOP的五大通知类型有哪些？
>   - A：先贴上官方的一段文字，如下所示：
>       - Before advice: Advice that runs before a join point but that does not have the ability to prevent execution flow proceeding to the join point (unless it throws an exception).
>       - After returning advice: Advice to be run after a join point completes normally (for example, if a method returns without throwing an exception).
>       - After throwing advice: Advice to be run if a method exits by throwing an exception.
>       - After <span style="color:red;">(**finally**)</span> advice: Advice to be run regardless of the means by which a join point exits (normal or exceptional return).
>       - Around advice: Advice that surrounds a join point such as a method invocation. This is the most powerful kind of advice. Around advice can perform custom behavior before and after the method invocation. It is also responsible for choosing whether to proceed to the join point or to shortcut the advised method execution by returning its own return value or throwing an exception.<br />
>   - A2: 简单说就是Before、After returning、After throwing、After、Around。
> - Q3: 为什么能差点干起来？
>   - A:我们看上文，AOP的五大通知类型，其中After就占3样，Before和Around都没啥争议，焦点就在这个After里。
> - Q4：3种After的区别是什么？
>   - A: 在讲解过程中老师是这么说的，他将After returning 解释为返回后通知，返回数据后执行；将After throwing 解释为后置通知，抛出异常后通知；将After解释为后置通知，方法执行后执行。争论焦点就在于这三种After的执行先后顺序。经过进一步的验证得知，After throwing方法只有在有异常的时候会执行，故不再提。当用注解方式执行AOP操作的话，After returning执行要早于After。类似代码如下：

```java
    @After("execution(* com.yiyun..*Service.*(..))")
    public void doAfter(JoinPoint joinPoint){
        System.out.println("执行doAfter");
    }

    @AfterReturning("execution(* com.yiyun..*Service.*(..))")
    public void doAfterReturning(JoinPoint joinPoint){
        System.out.println("doAfterReturning");
    }    
```
>    - 程序运行结果如下：
```java
    doAfterReturning
    执行doAfter
```
而当我们使用AOP的XML配置式执行时，After和After returning取决于你在配置文件中的先后顺序。换言之，当你使用XML配置式使用AOP框架时，你想让After先执行就把它配在前面，你想让它后执行就配在后面。
如下所示配置：
```xml
        <!--返回后通知 方法执行完毕后执行-->
    <aop:after-returning method="doAfterReturning" returning="ret" pointcut-ref="pointcut" />
        <!--后置通知 方法执行后执行-->
    <aop:after method="doAfter" pointcut-ref="pointcut" />
```
这种配置说明当切面同时存在after和after-returning方法是，最后执行After方法，如果将after方法配置在after-returning方法之前，则先执行after后执行after-returning。

---
>其实仔细看官方文档的话我们会发现官方在AOP的五种通知中给After特别加上了(finally)。原来官方早已看穿了这一切。<br>
> 培训老师指出，在工作中，看具体应用场景，在AOP中应用最多的是Around方法，在around方法中，我们可以较为方便的插入切面方法运行前、后、异常时的代码块，使用比较灵活。
><span style="display:block;text-align:right;color:black;"> **终** </span>





