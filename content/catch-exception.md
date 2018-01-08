# 捕获异常
___



> 1

实现一个异常捕获

```
NSSetUncaughtExceptionHandler(&UncaughtExceptionHandler);
```

```objc
void UncaughtExceptionHandler(NSException *exception) {
    NSArray *arr = [exception callStackSymbols];
    NSString *reason = [exception reason];
    NSString *name = [exception name];
    NSLog(@"异常：%@\n%@\n%@",arr, reason, name);
}
```

