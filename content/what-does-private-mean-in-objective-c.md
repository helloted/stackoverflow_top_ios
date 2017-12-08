# @private在Objective-C里是什么意思？
[What does “@private” mean in Objective-C?](https://stackoverflow.com/questions/844658/what-does-private-mean-in-objective-c)

___



> 1

这是一个可用标志符，它表示由`@private`声明的实例变量只能由同类的实例对象来访问，

私有成员不能被子类或者其他类访问

```
@interface MyClass : NSObject
{
    @private
    int someVar;  // 只能被MyClass访问

    @public
    int aPublicVar;  // 可以被任意对象访问
}
@end
```

Objective-C中有一个隐藏的公开声明