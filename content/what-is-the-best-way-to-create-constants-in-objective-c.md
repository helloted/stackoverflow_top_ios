# Objective-C声明常量的最好方式
[What is the best way to create constants in Objective-C](https://stackoverflow.com/questions/17228334/what-is-the-best-way-to-create-constants-in-objective-c)

___



> 1

如果常量是具体的而且在一个类的内部使用，这种常量的声明应该用`static const` ，放在.m文件的顶部位置

```objc
static NSString *const MyThingNotificationKey = @"MyThingNotificationKey";
```

如果常量属于一个类，但是要被其他类引用，声明的时候用 `extern` 在头文件里，然后在 .m文件里定义:

```objc
//.h
extern NSString *const MyThingNotificationKey;

//.m
NSString *const MyThingNotificationKey = @"MyThingNotificationKey";
```

如果它们应该是全局的，则在头文件中声明它们，并在相应的模块中定义它们，特别是那些常量。

你可以根据常量的使用级别来分类这些常量 - 你可以把它们放在单独的模块中，每个模块都有自己的头文件，如果你觉得有必要的话。

#### 为什么不用 `#define`?

debugger并不清楚你的宏，在一个debugger命令里，你不能用 `[myThing addObserver:self forKey:MyThingNotificationKey]` 如果 `MyThingNotificationKey` 是一个宏; debugger 只能知道是否是个变量。

#### 为什么不用 `enum`?

 `enum` 只能定义数字常量. 

如果想要定义诸如序列标识符号码，位掩码，四字节代码等你应该用`enum`  (最好用 [the `NS_ENUM` and `NS_OPTIONS` macros](http://nshipster.com/ns_enum-ns_options/).) 