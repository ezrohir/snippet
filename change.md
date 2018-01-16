### SSL/TLS

+ [SSL/TLS协议运行机制的概述](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)
+ [SSL/TLS 握手过程详解](http://www.jianshu.com/p/7158568e4867)
+ [数字签名](http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html)



### HTTP2.0
+ [HTTP/2 简介](https://developers.google.com/web/fundamentals/performance/http2/?hl=zh-cn)


### 页面性能相关
+ [iOS 使用 Method Swizzling 进行性能统计](https://testerhome.com/topics/4519)
+ [looking-to-understand-the-ios-uiviewcontroller-lifecycle](https://stackoverflow.com/questions/5562938/looking-to-understand-the-ios-uiviewcontroller-lifecycle)









#### Method Swizzling
Object-C 对 AOP (Method Swizzling) 的支持非常容易:
Runtime 支持方法名和方法实现的分离, Object-C 的方法名类型是 SEL ,方法实现类型是 IMP.

一个 Objective-C 方法 [self setFilled:Yes] 完全可以用下面的代码替代:
```
SEL aSelector = @selector(setFilled:);
IMP aIMP = [self methodForSelector:aSelector];
void (*setter)(id,SEL,BOOL) = (void(*)(id,SEL,BOOL))aIMP;
setter(self,aSelector,YES);
```

Method Swizzling 的陷阱:
+ Method swizzling is not atomic

  在 +(void)load里,并在应用程序一开始调用执行能有些避免.放在 +(void)initialize 初始化方法中进行swizzle, runtime可能出于一种诡异状态.


#### load 和 initialize
+load 方法是当类或分类被添加到 Objective-C runtime 时被调用的,实现这个方法可以让我们在类加载的时候执行一些类相关的行为.
+initialize 方法是在类或它的子类收到第一条消息之前被调用的,这里所指的消息包括实例方法和类方法的调用.


#### runtime
+ [iOS Runtime 详解]https://njafei.github.io/2017/05/04/runtime/

如果是普通的C语言代码,我们使用的是传统的编译运行,那么一个函数的执行内容,在编译阶段其实就确定了,执行的时候只要去执行对应的内存地址的程序就好.

而在runtime中,编译阶段只能确定最终要执行的函数名,但是具体执行的时候,执行的是什么程序,是在运行的时候才能确定,大大增加了程序的灵活性.
