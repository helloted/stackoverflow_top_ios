# Assertion vs. Exception vs. Error
[Objective-C: Assertion vs. Exception vs. Error](https://stackoverflow.com/questions/5009597/objective-c-assertion-vs-exception-vs-error)

___



> 1

```
#define NSAssert(condition, desc, ...)
```

NSAssert（断言）是一个宏定义，它会抛出一个Exception异常当condition条件不成立时，所以NSAssert很简短方便地去确认代码里的一个假设。

NSException是一个可以自定义的异常，你可以`@throw`一个异常使运行停止，你也可以`@catch`一个异常，使得代码可以继续运行。

NSError应该在你的交互有错误而不是编程错误时使用，这个错误是可以被修复的，你可以在里面存放错误代码，错误信息。

