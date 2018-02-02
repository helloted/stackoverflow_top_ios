# Swizzle 类方法
[How to swizzle a class method on iOS?](https://stackoverflow.com/questions/3267506/how-to-swizzle-a-class-method-on-ios)

___



> 1

这是实例方法的swizzle:

```objc
static void SwizzleMethod(Class cls, SEL ori, SEL rep) {
    Method oriMethod = class_getInstanceMethod(cls, ori);
    Method repMethod = class_getInstanceMethod(cls, rep);

    BOOL flag = class_addMethod(cls, ori, method_getImplementation(repMethod), method_getTypeEncoding(repMethod));

    if (flag) {
        class_replaceMethod(cls, rep, method_getImplementation(oriMethod), method_getTypeEncoding(oriMethod));
    } else {
        method_exchangeImplementations(oriMethod, repMethod);
    }
}
```

Class还有一个用来获取类方法的`class_getClassMethod`，

所以如果是要swizzle类方法的话，将`class_getInstanceMethod`换成`class_getClassMethod`即可，也就是

```objc
static void SwizzleMethod(Class cls, SEL ori, SEL rep) {
    Method oriMethod = class_getClassMethod(cls, ori);
    Method repMethod = class_getClassMethod(cls, rep);

    BOOL flag = class_addMethod(cls, ori, method_getImplementation(repMethod), method_getTypeEncoding(repMethod));

    if (flag) {
        class_replaceMethod(cls, rep, method_getImplementation(oriMethod), method_getTypeEncoding(oriMethod));
    } else {
        method_exchangeImplementations(oriMethod, repMethod);
    }
}
```

但是，我们再来看看`class_getClassMethod`的源码

```objc
Method class_getClassMethod(Class cls, SEL sel)
{
    if (!cls  ||  !sel) return nil;

    return class_getInstanceMethod(cls->getMeta(), sel);
}
```

实际上还是调用的`class_getInstanceMethod`,只是这个类变成了元类

所以，用`class_getInstanceMethod`也可以获取到类方法，在调用swizzlingMethod时，传入元类；

```objc
SwizzleMethod(object_getClass([Foo class]), @selector(bar), @selector(swz_bar));
```

