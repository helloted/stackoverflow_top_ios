# NSobject的+load +initialize做了什么？
[NSObject +load and +initialize - What do they do?](https://stackoverflow.com/questions/13326435/nsobject-load-and-initialize-what-do-they-do)

___



> 1

#### The `load` message

在类对象被加载入进程的的地址空间内之后很快，运行时发送load消息到每一个类对象。如果类是程序执行文件的一部分，运行时在进程生命周期很早的时候就发送了load消息。如果类在一个静态加载库中，运行时会在静态库被加载入进程的地址空间内发送load消息。

此外，只有当类实现了load方法，运行时才会发送load消息给类对象，例如

```Objc
@interface Superclass : NSObject
@end

@interface Subclass : Superclass
@end

@implementation Superclass

+ (void)load {
    NSLog(@"in Superclass load");
}

@end

@implementation Subclass

// ... load not implemented in this class

@end
```

运行时会发送 `load` 消息给 `Superclass` .不会发送 `load` 消息给 `Subclass` 对象，尽管`Subclass` 继承自 `Superclass`.

运行时会在一个类的所有父类已经发送load消息之后(如果父类有声明load方法)，才发送load消息给这个类，但是你无法知道这些类是否已经收到了load消息。

每个加载进进程地址空间的的类（声明了load方法）都会收到load消息，不管这个类是否有被用到

可以看看运行时如何查看`load` 在 `_class_getLoadMethod` of [`objc-runtime-new.mm`](http://opensource.apple.com/source/objc4/objc4-532.2/runtime/objc-runtime-new.mm), 直接调用 `call_class_loads`in [`objc-loadmethod.mm`](http://opensource.apple.com/source/objc4/objc4-532.2/runtime/objc-loadmethod.mm).

当运行时加载category是，也会运行load方法。如果两个category声明了同样的方法，其中一个会胜出并且被使用，另外一个永远不会被调用

#### The `initialize` Method

运行时会调用 `initialize` 方法在发送其他所有消息之前（除了load方法），消息发送用的是寻常机制，所以如果你的类没有声明 `initialize` ，但是父类有声明，那么这个类会用父类的 `initialize` 。

运行时首先会发送 `initialize` 给这个类的所有父类。

```objc
@interface Superclass : NSObject
@end

@interface Subclass : Superclass
@end

@implementation Superclass

+ (void)initialize {
    NSLog(@"in Superclass initialize; self = %@", self);
}

@end

@implementation Subclass

// ... initialize not implemented in this class

@end

int main(int argc, char *argv[]) {
    @autoreleasepool {
        Subclass *object = [[Subclass alloc] init];
    }
    return 0;
}
```

```
2012-11-10 16:18:38.984 testApp[7498:c07] in Superclass initialize; self = Superclass
2012-11-10 16:18:38.987 testApp[7498:c07] in Superclass initialize; self = Subclass
```

权威的声明方式应该是这样

```objc
@implementation Someclass

+ (void)initialize {
    if (self == [Someclass class]) {
        // do whatever
    }
}
```

这种方式的重点在于，可以避免Someclass重复initialize它自己，当它的其中一个子类没有声明 `initialize` 

运行时发送 `initialize` 消息在 `_class_initialize`  [`objc-initialize.mm`](http://opensource.apple.com/source/objc4/objc4-532.2/runtime/objc-initialize.mm). 