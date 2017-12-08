# 什么情况下使用NSInteger或者Int？
[When to use NSInteger vs. int](https://stackoverflow.com/questions/4445173/when-to-use-nsinteger-vs-int)

___



> 1

当你不知道你的处理器架构的时候，你应该使用 `NSInteger` ，这样的话，在有些情况下会得到比 `int` 更大的类型, 因为在32位CPU里是 `int`, 但是在64位系统里则是 `long`.

我坚持使用 `NSInteger` 而不是 `int`/`long` ，除非你真的特别需要.

`NSInteger`/`NSUInteger` 的定义是动态类型 `typedef`:

```
#if __LP64__ || TARGET_OS_EMBEDDED || TARGET_OS_IPHONE || TARGET_OS_WIN32 || NS_BUILD_32_LIKE_64
typedef long NSInteger;
typedef unsigned long NSUInteger;
#else
typedef int NSInteger;
typedef unsigned int NSUInteger;
#endif
```