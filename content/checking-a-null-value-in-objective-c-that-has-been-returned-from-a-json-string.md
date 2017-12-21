# JSON字符串里的null处理
[Checking a null value in Objective-C that has been returned from a JSON string](https://stackoverflow.com/questions/4839355/checking-a-null-value-in-objective-c-that-has-been-returned-from-a-json-string)

___



> 1

Json字符串里的null，如果放到字典里，会被解析成`[NSNull null]`,如果打印的话，log会是<null>，所以可以这样进行辨别

```
if (tel == (id)[NSNull null]) {
    // tel is null
}
或者
if ([tel isKindOfClass:[NSNull class]])
```

究其原因，是因为在Objective-c里，不能有nil，空元素一律用[NSNull null]来表示