# SpringImpl_v1.0  （请移步prototype分支，propertype分支较为完善，分支因为冲突过多还没有合并，等有时间好好整理下，O(∩_∩)O~）

##ps：看了很多别人写的项目，很多项目都很不错，但是却没有一个详细项目说明（我的一开始也是，好感概啊！）导致你的项目再好，别人的理解成本是很高的；
##    来github也有很长的一段时间了，在这里也收获了很多，既然它是一个开源的社区，那么核心自然是分享，我也希望我的这个小demo能友好的分享给大家，我##   也会尽量写好项目说明（如果有什么不好的地方给我提建议，我会改正），降低别人学习成本；我也会将写出高质量易读的代码作为我前行的目标！加油
##   ↖(^ω^)↗

##项目简介：
    一直在学习Spring，这个是模仿SpringIOC的实现原理仿制的一个框架，希望能在不断地构建以及重构这个框架的过程中不断地学习Spring，在这个过程中一窥Spring的精髓，以及我们要如何设计一个可用性高，高拓展的项目，它会教会我们如何去设计一个软件，而不是如何去写代码。我也会在今后不断的学习中更新这个项目，将自己的理解注入我的IOC容器。当然，基于题主才疏学浅，固然框架有很多不好的地方，如有朋友能提供一些指导和建议，不胜感激。
    



##安装：
    本项目采用maven构建，你可以直接git项目到本地：
    git clone https://github.com/MySixGod/SpringImpl_v1.0.git  或者fork我的项目


##文档：<a href="https://github.com/MySixGod/SpringImpl_v1.0/wiki/%E9%A1%B9%E7%9B%AE%E7%9A%84%E8%AF%A6%E7%BB%86%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E">
项目使用详细说明</a>

##版本历史：
    版本1.0，还只实现了默认的DefaultListableBeanFactory，后续的话会添加更多容器实现
    
    版本1.1：新增增加AutowireApplicationContext容器，添加@Component注解，实现自动注入功能
    
    版本2.0：已经实现xml下bean依赖顺序的问题（无论xmlbean定义的顺序如何，DefaultListableBeanFactory的getbean方法总能得到完整的bean），
            接下来我会解决注解注入中bean依赖顺序的问题以及如何处理出现bean循环依赖的问题，2.0版本还不完整，还存在许多小问题，也暂时取消了基本属性               的入（只能注入bean），接下的版本我会一一完善
    
    版本2.1：已经解决了循环依赖以及bean依赖顺序的问题，妈妈再也不用担心我配错bean的顺序啦！也加入了基本属性的注入，不过必须配置为完整的包装类型，
      例如：  <!-- 注入基本的类型的xml配置方法 ,需要配置三个属性:
              1. field的name，
              2. 需要注入的属性类型，（填写包装类型）
              3. 需要注入的value
         -->
         <property name="foodName"  type="java.lang.String"  value="西红柿" ></property>
         因为我是通过反射来注入基本类型的，另外现在框架通过beandefinition生成对象的实例过程中只通过set方法去设置bean的依赖，所以暂时只能通过单一的
         set方法进行注入，我会在后续的版本中添加更多的支持，进一步完善！！！
            
            <br>
            <br>
               <br>
               
##项目整体结构图：

src
├── main
│   └── java
│       └── com
│           └── lonton
│               ├── anntotion  框架注解包，目前实现了@autowired和@component注解
│               ├── beans     
│               │   ├── config  这里面放的是beandefinition类
│               │   └── factory  核心ioc容器实现全在这里啦！最核心的容器DefaultListableBeanFactory，AbstractBeanFactory，重点
│               ├── context      context容器包，
│               ├── core
|               |   ├── aop     aop假装实现了下，其实就是写了下java动态代理，忽略吧
│               │   └── io      这里面放的是核心的resource包，容器将通过它来获取beandefinition
│               ├── enums       一些枚举常量包，比如single，prototype等
│               ├── exception   异常包
│               ├── ioc         核心容器包
│               └── tools       一些通用的工具类
├── resource
│   ├── log4j.properties        日志文件
│   └── test.xml
└── test                        下面是一些测试用例，写的比较少，好吧，估计还有很多bug
    └── java
        ├── com
        │   └── lonton
        │       ├── annotation
        │       ├── bean
        │       ├── beans
        │       ├── classForTest
        │       ├── context
        │       └── core
        └── spring
            └── SpringImpl
                ├── AppTest.java
                └── test.java

            <br>
            <br>
            <br> 
             #项目类图：（类的关系有些地方还有待商榷，有不清晰的地方，后续在慢慢改正）
             BeanDefinition:
            ![Image text]( https://github.com/MySixGod/SpringImpl_v2.0/blob/property/ModelGoonImage/BeanDefinition.png)
            Resource类图：
            ![Image text]( https://github.com/MySixGod/SpringImpl_v2.0/blob/property/ModelGoonImage/IO.png)
            核心容器类图：
             ![Image text]( https://github.com/MySixGod/SpringImpl_v2.0/blob/property/ModelGoonImage/BeanFactory.png)
             异常处理类图（命名以及结构有些随意，后续改进）：
              ![Image text]( https://github.com/MySixGod/SpringImpl_v2.0/blob/property/ModelGoonImage/exception.png)
              
          
##联系方式：
    邮箱：woshi6ye@gmail.com
    qq：1491758730
    使用的过程中如果有任何问题或者建议的话，可以联系我，我会及时给予解答
    如果觉得还不错，或者是给我一些鼓励的话，请给一颗小星星作为鼓励哦，我也会把这个框架做的越来越好
    
   

