# 如何声明一个全局常量？
[Constants in Objective-C](https://stackoverflow.com/questions/538996/constants-in-objective-c)

问题：如何声明一个全局的常量字符串

___



> 1

你可以在.h文件里这样

```
// Constants.h
FOUNDATION_EXPORT NSString *const MyFirstConstant;
FOUNDATION_EXPORT NSString *const MySecondConstant;
//etc.
```

如果不是C/C++混编，你可以用 `extern` 替换 `FOUNDATION_EXPORT` 。需要将.h文件导入到需要使用这个常量的文件中

在.m文件里则这样声明：

```
// Constants.m
NSString *const MyFirstConstant = @"FirstConstant";
NSString *const MySecondConstant = @"SecondConstant";
```

这种声明比`#define`有一个优势在于(`stringInstance == MyFirstConstant`) 来指针比较而不是 (`[stringInstance isEqualToString:MyFirstConstant]`)进行字符串比较，前者效率更高且易读。