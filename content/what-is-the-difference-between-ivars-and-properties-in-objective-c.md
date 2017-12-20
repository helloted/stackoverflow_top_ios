# 实例变量(iVar)与属性(property)的区别
[What is the difference between ivars and properties in Objective-C](https://stackoverflow.com/questions/4172810/what-is-the-difference-between-ivars-and-properties-in-objective-c)

[Property vs. ivar in times of ARC](https://stackoverflow.com/questions/7836182/property-vs-ivar-in-times-of-arc)

```objc
  // MyObject.h
  @interface MyObject 
  
  @proptery(nonatomic, copy)NSString *foo;
```

```objc
  // MyObject.h
  @interface MyObject {
        NSString *foo;
  }
```

___



> 1

许久以前，如果你有一个实例变量iVar, 如果你想让其他的类来访问这个变量(获取或者设置)，你就必须自己分别在.h和.m文件里去定义一个getter方法和setter方法，比如 getter (i.e., `-(NSString *)foo)` ， setter (i.e., `-(void)setFoo:(NSString *)aFoo;`)

属性做的就是让你从实例变量的setter和getter方法里解放出来，当你定义了一个属性，编译器会自动帮你生成setter和getter方法，你也可以自定义setter和getter方法。

为什么属性会foo会变成实例变量_foo，这是`@synthesize`做的，许多人会 @synthesize foo=_foo; 这意味着给属性foo生成一个实例变量 `_foo`  ，这样的话，你就可以直接使用_foo来访问变量，而不需要通过self.foo(也就是setter和getter方法)。

在Xcode 4.6之后,你不需要使用 `@synthesize` 编译器会自动做这步操作，并且在变量前面添加 `_`.

> 2

- 除非自己去.h和.m文件里生成setter和getter方法，其他类不能访问实例变量
- 除非自己去setter方法里实现KVO监听，实例变量没有KVO功能
- 实例变量不能对对象进行属性修饰，比如NString，ARC会默认用strong修饰。如果用属性则可以用copy修饰。