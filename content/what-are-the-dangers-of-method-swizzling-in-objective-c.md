# 使用Method-swizzling的危险？
https://stackoverflow.com/questions/5339276/what-are-the-dangers-of-method-swizzling-in-objective-c

___



> 1

使用Method-swizzling会有以下陷阱：

- Method-swizzling非原子性
- 是一个更改非所有权的代码的行为
- 可能引发命名冲突
- Swizzling 改变了方法的实际参数
- Swizzles的顺序导致的麻烦
- 理解困难（看起来像递归）
- debug困难

#### Method-swizzling非原子性

我还没有看到一个Method-swizzling的方法实现在并发时是安全的，一般来说，你只是简单地想要替换一个方法，而你希望替换后的方法可以再项目的整个生命周期中使用，这意味着，你应该在`+(void)load`方法中做Method-swizzling,`load`这个类方法在APP开始阶段执行，如果你在这里进行方法替换，你可以不用担心并发。

如果你在`+(void)initialize`方法中进行方法替换，你可能让你的方法替换处于一个竞争环境，运行时会以一个诡异的状态结束。

#### 更改非所有权的代码的行为

大家之所以会把这个任务是一个大问题，是因为你不仅仅改变了一个NSButton的实例，而是替换了程序中所有的NSButton的实例，出于这个原因，当你swizzle你应该小心，但你不需要完全避免它。

#### 可能引发命名冲突

命名冲突出现在整个Cocoa中，我们频繁地使用前缀在方法名称中。在方法替换中，我们只需要更改一下我们之前的方式。大部分的Swilling如下：

```
@interface NSView : NSObject
- (void)setFrame:(NSRect)frame;
@end

@implementation NSView (MyViewAdditions)

- (void)my_setFrame:(NSRect)frame {
    // do custom work
    [self my_setFrame:frame];
}

+ (void)load {
    [self swizzle:@selector(setFrame:) with:@selector(my_setFrame:)];
}

@end
```

如果`my_setFrame`方法在其他地方声明了，就会有问题了，我们可以解决它：

```
@implementation NSView (MyViewAdditions)

static void MySetFrame(id self, SEL _cmd, NSRect frame);
static void (*SetFrameIMP)(id self, SEL _cmd, NSRect frame);

static void MySetFrame(id self, SEL _cmd, NSRect frame) {
    // do custom work
    SetFrameIMP(self, _cmd, frame);
}

+ (void)load {
    [self swizzle:@selector(setFrame:) with:(IMP)MySetFrame store:(IMP *)&SetFrameIMP];
}

@end
```

上面的示例可以避免命名冲突，同样可以做到方法替换。

方法替换是这样定义的：

```
typedef IMP *IMPPointer;

BOOL class_swizzleMethodAndStore(Class class, SEL original, IMP replacement, IMPPointer store) {
    IMP imp = NULL;
    Method method = class_getInstanceMethod(class, original);
    if (method) {
        const char *type = method_getTypeEncoding(method);
        imp = class_replaceMethod(class, original, replacement, type);
        if (!imp) {
            imp = method_getImplementation(method);
        }
    }
    if (imp && store) { *store = imp; }
    return (imp != NULL);
}

@implementation NSObject (FRRuntimeAdditions)
+ (BOOL)swizzle:(SEL)original with:(IMP)replacement store:(IMPPointer)store {
    return class_swizzleMethodAndStore(self, original, replacement, store);
}
@end
```

#### 更改方法名导致的更改方法的实际参数

在我看来，这是一个大问题。你正在更改传递给原来方法声明的参数。整个过程是这样的：

```
[self my_setFrame:frame];
```

```
objc_msgSend(self, @selector(my_setFrame:), frame);
```

运行时会在方法IMP列表里查找``my_setFrame:`，一但IMP找到了，它会用给的相同参数来调用IMP。运行时找到的IMP是原来的IMP`setFrame:`，所以它会在前面给调用，但是_cmd的实际参数并不是`setFrame:`而是`my_setFrame:`,原来的IMP被调用了它没有预料到它会接受的参数，这样并不好。

有一个简单的解决方案：用刚才上面的定义，可以保证实际参数永远不会被改变

#### Swizzles的顺序导致的麻烦

想象一下下面这种情况：

```
[NSButton swizzle:@selector(setFrame:) with:@selector(my_buttonSetFrame:)];
[NSControl swizzle:@selector(setFrame:) with:@selector(my_controlSetFrame:)];
[NSView swizzle:@selector(setFrame:) with:@selector(my_viewSetFrame:)];
```

NSButton也swizzle了会发生什么？

当你在一个button上面调用了`setFrame:`，将会调用已经替换后的方法，然后，直接跳到NSView里原来声明的`setFrame:`，NSControl和NSView被替换的方法不会被调用。

但是如果顺序是这样：

```
[NSView swizzle:@selector(setFrame:) with:@selector(my_viewSetFrame:)];
[NSControl swizzle:@selector(setFrame:) with:@selector(my_controlSetFrame:)];
[NSButton swizzle:@selector(setFrame:) with:@selector(my_buttonSetFrame:)];
```

因为NSView的方法替换是最先做的，NSControl的将会拿到正确的方法，同样的，NSButton也会从NSControl那里拿到方法`setFrame:`.这样有点困惑，但是这是正确的顺序，如何来保证这些呢？

同样的，还是要用load方法，如果你只在+load方法里进行替换，你就会安全的，load方法保证了父类加载方法在子类加载之前，这样就会拿到正确的顺序。

#### 理解困难（看起来像递归）

用传统的方式来swizzled方法，会让人困惑，但是如果用我们上面的流程来替换方法，就比较容易理解了

#### debug困难

debug困难是因为很难记得实际声明是什么，所以做好文档。

#### 总结

如果使用得当，Method-swizzling是安全的，一个安全稳定的操作就是在load方法里进行替换操作。就如同编程中的许多事情，也许会有危险，但是理解清楚就能使用得当。

